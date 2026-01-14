# AWS App Runner

## Links
- [AWS App Runner Console](https://console.aws.amazon.com/apprunner/home)
- [AWS App Runner Documentation](https://docs.aws.amazon.com/apprunner/latest/dg/manage-create.html)
- [AWS Toolkit for VS Code - ECR and App Runner](https://docs.aws.amazon.com/toolkit-for-vscode/latest/userguide/ecr-apprunner.html)
- [AWS App Runner Environment Variables](https://docs.aws.amazon.com/apprunner/latest/dg/env-variable.html)
- [AWS App Runner Environment Variable Management](https://docs.aws.amazon.com/apprunner/latest/dg/env-variable-manage.html)
- [AWS App Runner VPC Configuration](https://docs.aws.amazon.com/apprunner/latest/dg/network-vpc.html)
- [New for App Runner: VPC Support](https://aws.amazon.com/blogs/aws/new-for-app-runner-vpc-support/)
- [AWS App Runner Custom Domains](https://docs.aws.amazon.com/apprunner/latest/dg/manage-custom-domains.html)
- [AWS App Runner API: Associate Custom Domain](https://docs.aws.amazon.com/apprunner/latest/api/API_AssociateCustomDomain.html)

## Set up your website on AWS App Runner (from an existing ECR image)

### 1) Create the App Runner service from your ECR image
1. AWS Console → **App Runner** → **Create service**
2. **Source**: *Container registry* → *Amazon ECR*
3. Select your **ECR repository** and the image tag/digest you want to deploy.
4. Provide an **ECR access role** so App Runner can pull from your private ECR repository. [1][2]
5. Set the **port** your container listens on.
6. Configure **health check**
   - TCP is simplest; HTTP is better if you have a path like `/health`.
7. Create the service and wait until status is **Running**.

### 2) Configure runtime environment variables and secrets


**A) Non-sensitive environment variables**
- App Runner → your service → **Configuration** → **Environment variables** → add plain key/value entries.

**B) Sensitive values (recommended)**
- Store secrets in **AWS Secrets Manager** or **SSM Parameter Store**, then reference them as environment variables in App Runner. [3][4]
- Create/attach an **instance role** to the App Runner service that allows reading those secrets/parameters. [3][4]

Notes:
- If you rotate/update a referenced secret/parameter, redeploy the service to pick up the new value. [3]

### 3) Connect App Runner to your private RDS (high-level)
Because your PostgreSQL RDS is in a VPC, configure **App Runner outgoing traffic** to use a **VPC connector**:
1. App Runner → **Network configuration** → **Outgoing traffic** → **Create VPC connector**
2. Choose the **same VPC** as your RDS and select appropriate **subnets** + (optionally) **security groups**.
3. Attach that VPC connector to your App Runner service’s outgoing traffic settings. [5]

If your app also needs outbound access to the public internet (external APIs), ensure your VPC routing supports it (typically via NAT for private subnets). [6]

### 4) (Optional) Add a custom domain
1. App Runner → your service → **Custom domains** → **Add domain**
2. App Runner provides:
   - a **DNS target** record for your domain mapping, and
   - **certificate validation CNAME records**
3. Add the provided CNAME records in your DNS provider and wait for validation to complete. [7][8]

### 5) Deploy/update workflow
- To deploy a new version, push a new image tag/digest to ECR, then trigger a new App Runner deployment (manual or configured automation).
- Use App Runner service logs/health status to confirm the new revision is healthy.
