# React App on AWS S3 with Static Hosting + CloudFront | Practical AWS Project

This README provides step-by-step instructions to deploy a React application on AWS S3 using Static Hosting and CloudFront for CDN distribution. This is a practical AWS project that demonstrates how to host your React app efficiently on AWS.

---

## Table of Contents

- [Prerequisites](#prerequisites)
- [Step 1: Create React App](#step-1-create-react-app)
- [Step 2: Build React App for Production](#step-2-build-react-app-for-production)
- [Step 3: Create an S3 Bucket for Static Hosting](#step-3-create-an-s3-bucket-for-static-hosting)
- [Step 4: Upload React App to S3](#step-4-upload-react-app-to-s3)
- [Step 5: Configure S3 Bucket for Static Website Hosting](#step-5-configure-s3-bucket-for-static-website-hosting)
- [Step 6: Set up CloudFront Distribution](#step-6-set-up-cloudfront-distribution)
- [Step 7: Update S3 Bucket Policy](#step-7-update-s3-bucket-policy)
- [Step 8: Test the React App](#step-8-test-the-react-app)

---

## Prerequisites

Before starting, make sure you have the following:

- An AWS account
- AWS CLI installed and configured with access keys
- Node.js and npm installed
- A React app ready to be deployed

---

## Step 1: Create React App

If you don't already have a React app, you can quickly set one up using `create-react-app`:

```bash
npx create-react-app my-react-app
cd my-react-app
```

---

## Step 2: Build React App for Production

React apps need to be optimized before deployment. Run the following command to build your app for production:

```bash
npm run build
```

This will create a `build/` directory with optimized production assets.

---

## Step 3: Create an S3 Bucket for Static Hosting

1. Log in to the [AWS Management Console](https://aws.amazon.com/console/).
2. Navigate to **S3**.
3. Click on **Create Bucket**.
4. Provide a unique bucket name (e.g., `my-react-app-bucket`).
5. Select a region for the bucket (preferably the one closest to your users).
6. Click **Create Bucket**.

---

## Step 4: Upload React App to S3

Upload the contents of your `build/` directory to your S3 bucket:

1. Go to your S3 bucket in the AWS Management Console.
2. Click on **Upload**.
3. Select all the files in the `build/` directory and upload them to the S3 bucket.

---

## Step 5: Configure S3 Bucket for Static Website Hosting

1. In the AWS Management Console, go to your S3 bucket.
2. Navigate to the **Properties** tab.
3. Under **Static website hosting**, click **Enable**.
4. Set the following options:
   - **Index document**: `index.html`
   - **Error document**: `index.html` (optional, helps with React Router)

5. Click **Save changes**.

---

## Step 6: Set up CloudFront Distribution

1. Go to **CloudFront** in the AWS Management Console.
2. Click **Create Distribution**.
3. Under **Web**, click **Get Started**.
4. For the **Origin Domain Name**, select your S3 bucket.
5. Set the **Viewer Protocol Policy** to **Redirect HTTP to HTTPS** for better security.
6. Under **Default Cache Behavior Settings**, leave other options as default.
7. Click **Create Distribution**.

CloudFront will take a few minutes to deploy your distribution.

---

## Step 7: Update S3 Bucket Policy

In order to make your React app publicly accessible, you'll need to update the S3 bucket policy.

1. Go to your S3 bucket.
2. Click on the **Permissions** tab.
3. Under **Bucket Policy**, click **Edit** and add the following policy:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": [
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws:s3:::your-bucket-name/*"
            ]
        }
    ]
}
```

**Note**: Replace `your-bucket-name` with the actual name of your S3 bucket.

4. Click **Save changes**.

---

## Step 8: Test the React App

After the CloudFront distribution is deployed, you can access your React app using the CloudFront domain name. You can find this URL in the **CloudFront** console:

- Go to **CloudFront**.
- Click on the distribution you created.
- Copy the **Domain Name** (e.g., `d1234abcd5678.cloudfront.net`).
- Visit the URL `https://d1234abcd5678.cloudfront.net` in your browser to view your deployed React app.

---

## Conclusion

Congratulations! You've successfully deployed a React app using AWS S3 for static hosting and AWS CloudFront for content distribution. This setup offers high performance, scalability, and low latency for serving static assets.

You can now continue to work on your app, and every time you make changes, you can build the app again and upload the updated build to S3.

---

## Further Enhancements

- **Custom Domain**: You can configure a custom domain (e.g., `www.example.com`) with your CloudFront distribution by adding a CNAME and updating your DNS settings.
- **SSL**: CloudFront provides free SSL certificates using Amazon's ACM (AWS Certificate Manager) for HTTPS encryption.

---

Feel free to customize and expand upon this project. Happy coding!
