# AWS CloudFront-Lambda-RDS Model

## Links
- [AWS S3 + CloudFront Frontend Hosting]()

## CloudFront + S3 Frontend Hosting

### The "True Free" Strategy: S3 + CloudFront

By using **Origin Access Control (OAC)**, the S3 bucket is entirely private from the public internet, ensuring that only CloudFront can see your files. This is the industry-standard "secure" way to host static sites.

---

### Step 1: Prepare Your React Build
Before touching the AWS console, you need your production-ready files. In your project folder, run the build command.
```bash
npm run build
```

---

### Step 2: Create a Private S3 Bucket
1. Log in to the **S3 Console**.
2. Click **Create bucket**. 
3. **Bucket name:** Choose something unique (e.g., `my-react-app-2026`).
4. **Object Ownership:** Keep "ACLs disabled."
5. **Block Public Access:** Leave all boxes checked (Keep it **ON**). We want this bucket private.
6. Click **Create bucket**, then open it and **Upload** all files inside your local `dist/` or `build/` folder.

---

### Step 3: Create the CloudFront Distribution
This is the "engine" that serves your site over HTTPS and gives you the 1TB free data transfer.

1. Go to the **CloudFront Console** and click **Create distribution**.
2. **Origin domain:** Select your S3 bucket from the dropdown.
3. **Origin access:** Select **Origin access control settings (recommended)**.
   * Click **Create control setting** and just hit **Create** (leave defaults).
4. **Web Application Firewall (WAF):** For a free setup, select **Do not enable security protections** (to avoid WAF costs).
5. **Default root object:** Type `index.html`. 
6. Click **Create distribution**.

---

### Step 4: Update the S3 Bucket Policy
Once the distribution is created, CloudFront will show a yellow banner saying "The S3 bucket policy needs to be updated." 

1. Click **Copy policy** from that banner.
2. Go back to your **S3 Bucket** > **Permissions** tab > **Bucket policy**.
3. Click **Edit** and paste the JSON policy provided by CloudFront.

```json
{
    "Version": "2012-10-17",
    "Statement": {
        "Sid": "AllowCloudFrontServicePrincipalReadOnly",
        "Effect": "Allow",
        "Principal": {
            "Service": "cloudfront.amazonaws.com"
        },
        "Action": "s3:GetObject",
        "Resource": "arn:aws:s3:::your-bucket-name/*",
        "Condition": {
            "StringEquals": {
                "AWS:SourceArn": "arn:aws:cloudfront::your-account-id:distribution/your-dist-id"
            }
        }
    }
}
```
---

### Step 5: Fix React Router "404 on Refresh"
If you use `react-router-dom`, refreshing a page like `/dashboard` will cause a 403/404 error because S3 thinks you're looking for a file named "dashboard."

1. In your **CloudFront Distribution**, go to the **Error pages** tab.
2. Click **Create custom error response**.
3. **HTTP error code:** Select `403: Forbidden` (or `404`).
4. **Customize error response:** Select **Yes**.
5. **Response page path:** Type `/index.html`.
6. **HTTP Response code:** Select `200: OK`.
7. Click **Create**. This forces CloudFront to let React handle the routing.

---

### Verification
Wait about 3–5 minutes for the "Status" to change from *Deploying* to *Enabled*. Copy the **Distribution domain name** (e.g., `d123.cloudfront.net`) and paste it into your browser. Your React app is now live and 100% free under standard usage!

Would you like me to show you how to connect your backend API (on Lambda) to this frontend using CloudFront "Behaviors" to avoid CORS issues?

[How to deploy your react app to AWS S3 and CloudFront](https://www.youtube.com/watch?v=IuxrOjjE2A4)

This video walks through the technical setup of S3 and CloudFront, which is essential for understanding how to host your React frontend without the high costs of App Runner.

## Automating Frontend Deployment with GitHub Actions
### Automating Deployment with GitHub Actions
Since your code is already in a Git repo (likely GitHub), using **GitHub Actions** is the most seamless way to automate this. It avoids the complexity of AWS-native tools like CodePipeline while staying well within the free tier.

The goal is: **You push code to your `main` branch $\rightarrow$ GitHub builds the React app $\rightarrow$ GitHub syncs files to S3 $\rightarrow$ GitHub tells CloudFront to clear its cache.**

---

### Step 1: Create an IAM User for GitHub
You need to give GitHub "permission" to talk to your AWS account.
1. Go to the **IAM Console** > **Users** > **Create user**.
2. **User name:** `github-deployer`.
3. **Permissions:** Choose "Attach policies directly." Search for and select:
   * **AmazonS3FullAccess** (or a custom policy limited to your specific bucket).
   * **CloudFrontFullAccess** (needed to clear the cache).
4. **Retrieve Keys:** Once the user is created, click on the user name > **Security credentials** > **Create access key**. Select "Command Line Interface (CLI)" and save your **Access Key ID** and **Secret Access Key**.

---

### Step 2: Store Secrets in GitHub
Never put your AWS keys directly into your code!
1. Go to your GitHub repository.
2. Click **Settings** > **Secrets and variables** > **Actions**.
3. Create the following **Repository secrets**:
   * `AWS_ACCESS_KEY_ID`: Paste your key.
   * `AWS_SECRET_ACCESS_KEY`: Paste your secret.
   * `AWS_S3_BUCKET`: The name of your bucket (e.g., `my-react-app-2026`).
   * `CLOUDFRONT_DISTRIBUTION_ID`: Found in the CloudFront console (e.g., `E1ABC123EXAMPLE`).

---

### Step 3: Create the Workflow File
In your React project, create a folder structure `.github/workflows/` and create a file named `deploy.yml` inside it.
```yaml
name: Deploy Frontend

on:
  push:
    branches:
      - main  # Only deploy when pushing to main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Set up Node.js
        uses: actions/setup-node@v4
        with:
          node-version: 20

      - name: Install dependencies
        run: npm install

      - name: Build React app
        run: npm run build

      - name: Configure AWS Credentials
        uses: aws-actions/configure-aws-credentials@v4
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: us-east-1 # Change to your region

      - name: Sync files to S3
        run: |
          aws s3 sync dist/ s3://${{ secrets.AWS_S3_BUCKET }} --delete

      - name: Invalidate CloudFront Cache
        run: |
          aws cloudfront create-invalidation \
            --distribution-id ${{ secrets.CLOUDFRONT_DISTRIBUTION_ID }} \
            --paths "/*"
```

### Why the "Invalidate" Step Matters?
CloudFront is a Content Delivery Network (CDN). It "remembers" your old files to make your site fast. If you upload new files to S3 but don't **Invalidate**, your users will keep seeing the old version of your site for up to 24 hours. The command `--paths "/*"` tells CloudFront to forget everything and fetch the newest files from S3 immediately.

---

### How to Test It
1. Commit the `.github/workflows/deploy.yml` file to your repo.
2. Push it to GitHub: `git push origin main`.
3. Go to the **Actions** tab in your GitHub repo.
4. You will see a live log of GitHub installing Node, building your app, and pushing it to AWS.


## Lambda

### Why Use the "AWS Lambda Web Adapter"?
The biggest headache with Spring Boot on Lambda is converting "Lambda Events" into "HTTP Requests" that Spring understands. Traditionally, you had to rewrite your code using specific AWS libraries.

In 2026, the best practice is to use the **AWS Lambda Web Adapter**. It is a tiny "sidecar" that sits inside your Lambda; it takes the Lambda event, turns it into a standard HTTP call, and sends it to your Spring Boot app running on port 8080. **You don't have to change a single line of your Java code.**



---

### Step 1: Prepare your Spring Boot App
You need to ensure your app listens on a specific port and excludes the heavy Tomcat server if you want to save memory (though standard Spring Boot works fine too).

In your `application.properties` or `application.yml`, ensure you have:
```properties
server.port=8080
# Optional: Faster startup
spring.main.lazy-initialization=true
```
---

### Step 2: Create a Dockerfile
Since you've never used Lambda, the **Container Image** approach is the most reliable. It packages everything your app needs. Create a file named `Dockerfile` in your project root:

```dockerfile
# Step 1: Use the Web Adapter as a layer
COPY --from=public.ecr.aws/awsguru/aws-lambda-adapter:0.8.4 /lambda-adapter /opt/extensions/lambda-adapter

# Step 2: Use a standard Java base image
FROM eclipse-temurin:21-jre-alpine

# Step 3: Copy your built JAR file
COPY target/your-app-name.jar /app.jar

# Step 4: Define the port and start command
ENV PORT=8080
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "/app.jar"]
```
---

### Step 3: Deploy to AWS Lambda
1.  **Build and Push:** Build your image locally and push it to **Amazon ECR** (Elastic Container Registry).
2.  **Create Function:** In the Lambda Console, click **Create function** > **Container image**.
3.  **Select Image:** Browse ECR and select the image you just pushed.
4.  **Memory:** Set memory to at least **1024MB or 2048MB**. Java needs room to breathe during startup.

---

### Step 4: Connect to RDS (The VPC Setup)
Since your RDS is private (for security), your Lambda needs to be in the same **VPC** to "see" it.

1.  In the Lambda Console, go to **Configuration** > **VPC**.
2.  Select the **same VPC** where your RDS is located.
3.  Select at least two **Private Subnets**.
4.  **Security Group:** Ensure the Lambda's Security Group allows **Outbound** traffic to the RDS port (5432).
    > **Warning:** Attaching a VPC to a Lambda used to cause long cold starts, but in 2026, AWS uses "Hyperplane" networking which makes this almost instantaneous.

---

### Step 5: Activate SnapStart (Crucial for Java)
By default, a Spring Boot app might take 10 seconds to start (a "Cold Start"). This is unacceptable for a web app. 

1.  In the Lambda Console, go to **Configuration** > **General configuration**.
2.  Find **SnapStart** and set it to **PublishedVersions**.
3.  **Publish a Version:** You must click **Versions** > **Publish new version** for SnapStart to take effect.
4.  **Result:** Your startup time will drop from ~10 seconds to **under 1 second**.

---

### Step 6: Add a "Function URL" (The Entry Point)
Instead of setting up a complex API Gateway, use the simpler **Function URL**:

1.  Go to **Configuration** > **Function URL**.
2.  Click **Create function URL**.
3.  Auth type: **NONE** (since this is a public website backend).
4.  **CORS:** Enable CORS and allow your S3/CloudFront domain to talk to it.

You will get a URL like `https://random-id.lambda-url.us-east-1.on.aws/`. This is your backend API!

Would you like me to show you the **CORS configuration** settings specifically for your React frontend so you don't get "Blocked by CORS" errors?

[How to optimize Spring Boot on AWS Lambda with SnapStart](https://www.youtube.com/watch?v=hukHKoztPh0)

This video compares different ways to run Spring Boot on Lambda and specifically highlights how SnapStart and the Web Adapter can make Java feel as fast as Node.js in a serverless environment.
