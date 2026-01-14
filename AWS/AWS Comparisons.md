## Amazon S3 and CloudFront + Lambda + RDS Free Tier: The "True Free" Architecture (Serverless)
This is the best way to keep your bill at $0.00 as long as you stay within the free tier limits.

### Frontend (React)
Use AWS Amplify Hosting or Amazon S3 + CloudFront.

Why: S3 stores your static files, and CloudFront delivers them. CloudFront has an "Always Free" tier of 1TB of data transfer per month.

### Backend (API)
Use AWS Lambda (with a framework like Lambda Web Adapter or Express).

Why: Unlike App Runner, Lambda only charges when code actually runs. You get 1 million free requests per month, which never expires.

### Database (PostgreSQL)
Use the RDS Free Tier.

You get 750 hours/month of a db.t3.micro or db.t4g.micro for the first 12 months.

## AWS Lightsail - The "Predictable Price" Architecture 
If you find the "New AWS Free Tier" credit system (the $200 credit model) confusing and want to avoid surprise bills, Lightsail is your best bet.

### Setup
Deploy a single "Virtual Private Server" (VPS).

Cost: Starts at $3.50 or $5.00/month.

Free Tier Benefit: New accounts often get the first 3 months free on select bundles.

Why: You can host your React files (using Nginx), your Node/Python backend, and even a small Dockerized PostgreSQL database all on one single instance. This avoids the $15/month starting price of a managed RDS database.