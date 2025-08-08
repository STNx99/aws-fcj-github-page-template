---
title: "Deploying the Project to Amplify"
date: "`r Sys.Date()`"
weight: 5
chapter: false
pre: " <b> 5.2 </b> "
---

In this step, you will learn how to deploy your project to AWS Amplify. This process will help you host your application and make it accessible over the internet.

#### Preparing for Deployment

1. Deploy to github:

- Go to the cloned repository from `https://github.com/TanPhat23/awscode`
- Find the `webdeploy` folder
- Open the terminal in the `webdeploy` folder
- Create a new repository on GitHub:
  - Go to [GitHub](https://github.com)
  - Click on the "+" icon in the top right corner and select "New repository"
  - Name your repository (e.g., `dewebdeploy`)
  - Set it to public or private as per your preference
  - Click "Create repository"
- Run the following commands in the folder where the `webdeploy` folder is located:
  ```bash
  git init
  git add .
  git commit -m "Initial commit"
  git branch -M main
  git remote add origin `Your repository URL`
   git push -u origin main
  ```

2. Deploy to Amplify:

- Go to the [AWS Amplify Console](https://console.aws.amazon.com/amplify/home)
- Click "Deploy an app"
  ![Deploy an app](/images/5.github/001-amplify.png)
- Select "GitHub" as the source provider
- Click "Next"
  ![Connect GitHub](/images/5.github/002-github.png)
- Authorize AWS Amplify to access your GitHub account
- Select the repository you created earlier (e.g., `dewebdeploy`)
- Choose the branch you want to deploy (usually `main`)
- Click "Next"
  ![Configure build settings](/images/5.github/003-amplify.png)
- Config your environment variables:
  - Click on "Edit" in the Environment variables section
  - Add the following environment variables:
    - `NEXTAUTH_SECRET`
    - `NEXTAUTH_URL` = `a`
    - `GITHUB_CLIENT_ID`
    - `GITHUB_CLIENT_SECRET`
    - `NEXT_PUBLIC_AWS_API_GATEWAY`
    - `NEXT_PUBLIC_AWS_BUCKET_URL`
  - Set the values for these variables as per your `.env` file
    ![Configure environment variables](/images/5.github/004-amplify.png)
- Click "Next"
- Review your settings and click "Save and deploy"

3. Configure build settings:

- Go to the "Build settings" section under "Hosting"
  ![Configure build settings](/images/5.github/005-amplify.png)
- Click "Edit" to modify the build settings
  ![Edit build settings](/images/5.github/006-amplify.png)
- Add the following build commands:
  ```yaml
  version: 1
  frontend:
    phases:
      preBuild:
        commands:
          - npm ci --cache .npm --prefer-offline
      build:
        commands:
          - echo "NEXTAUTH_SECRET=$NEXTAUTH_SECRET" >> .env
          - echo "GITHUB_CLIENT_ID=$GITHUB_CLIENT_ID" >> .env
          - echo "GITHUB_CLIENT_SECRET=$GITHUB_CLIENT_SECRET" >> .env
          - echo "NEXTAUTH_URL=$NEXTAUTH_URL" >> .env
          - echo "NEXT_PUBLIC_AWS_API_GATEWAY=$NEXT_PUBLIC_AWS_API_GATEWAY" >> .env
          - echo "NEXT_PUBLIC_AWS_BUCKET_URL=$NEXT_PUBLIC_AWS_BUCKET_URL" >> .env
          - npm run build
    artifacts:
      baseDirectory: .next
      files:
        - '**/*'
    cache:
      paths:
        - .next/cache/**/*
        - .npm/**/*
  ```
- Click "Save" to apply the changes
  ![Configure build settings](/images/5.github/007-amplify.png)
4. Update variables in the Amplify Console:
- Go to the "Environment variables" section under "Hosting"
- Click "Edit" to modify the environment variables
- Update the values for the following variables:
  - `NEXTAUTH_URL` = `https://your-amplify-app-id.amplifyapp.com`
- Update GithubOath:
  - Go to your GitHub OAuth App settings
  - Update the "Homepage URL" to `https://your-amplify-app-id.amplifyapp.com`
  - Update the "Authorization callback URL" to `https://your-amplify-app-id.amplifyapp.com/api/auth/callback/github`
  - Click "Update application"
- After updatiing the variables and build settings, go back to the Amplify Console
- Click "Redeploy this version" to apply the changes
  ![Redeploy this version](/images/5.github/008-amplify.png)
5. Add domain to API Gateway CORS Policy:
- Go to the [API Gateway Console](https://console.aws.amazon.com/apigateway/home)
- Select your API (e.g., `DeployAPI`)
- Go to the "CORS" section
- Add the following domain to the allowed origins:
  - `https://your-amplify-app-id.amplifyapp.com`
-Save the changes
![Add domain to API Gateway CORS Policy](/images/5.github/009-amplify.png)
6. Test your application:
- Open your web browser and navigate to your Amplify app URL (e.g., `https://your-amplify-app-id.amplifyapp.com`)
- Click on the "Sign in with GitHub" button
- You should be redirected to GitHub for authentication
- After successful authentication, you will be redirected back to your application
- You can now access your application hosted on AWS Amplify
#### Conclusion
Congratulations! You have successfully deployed your Next.js application to AWS Amplify. Your application is now live and accessible over the internet. You can continue to develop and push changes to your GitHub repository, and Amplify will automatically deploy those changes for you.
  