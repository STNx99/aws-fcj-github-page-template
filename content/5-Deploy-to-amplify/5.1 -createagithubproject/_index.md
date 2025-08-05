---
title: "Create github OAuth, testing it on local and create a github project"
date: "`r Sys.Date()`"
weight: 5
chapter: false
pre: " <b> 5.1 </b> "
---

In this step, you will learn how to create a GitHub OAuth application, test its authentication flow locally, and set up a new GitHub project. This process is essential for enabling secure authentication and integrating your application with GitHub services, which will be useful for future deployment and collaboration.

---

### Setting up Oauth on github and setting up a new project

1. Go to [github](github.com)

2. Go to settings
   ![Github settings](/images/5.github/001-github.png)

3. Go to developer settings
   ![Dev settings] (/images/5.github/002-github.png)

4. Click on OAuth Apps and Click New OAuth App
   ![New OAuth Apps] (/images/5.github/003-github.png)

5. Setting up your OAuth:

   - Enter an application name (e.g: webdeploy)
   - Hompage URL: http://localhost:3000
   - Authorization callback URL: http://localhost:3000/api/auth/callback/github
   - Click Register application
     ![Creating a Auth] (/images/5.github/004-github.png)

6. Generate a client secret

   - Click on Generate a new client secret
   - Copy the client secret and store it in a safe place
     ![Generate Client Secret] (/images/5.github/005-github.png)

7. Go to the cloned repository from `https://github.com/TanPhat23/awscode`:
   - If you haven't cloned the repository yet, do so by running:
     ```bash
     git clone
     ```
   - Go to the `webdeploy` folder and create a `.env` file.
   - Open the `.env` file in the root directory of the project.
   - Add the following lines to the `.env` file:
     ```plaintext
     NEXTAUTH_SECRET=
     NEXTAUTH_URL=http://localhost:3000
     GITHUB_CLIENT_ID= your_client_id
     GITHUB_CLIENT_SECRET= your_client_secret
     NEXT_PUBLIC_AWS_API_GATEWAY= your_aws_api_gateway
     NEXT_PUBLIC_AWS_BUCKET_URL= your_aws_bucket_url/dist
     ```
   - Replace `your_client_id` and `your_client_secret` with the values you copied from GitHub.
   - For `NEXTAUTH_SECRET`, you can generate a random string or use a secure secret management tool.
   - Save the `.env` file.
8. Start the development server:

   - Open a terminal and navigate to the webdeploy folder.
   - Ensure you have Node.js and npm installed if not go to [NodeJS](https://nodejs.org/en) for installation.
   - Run the following command to start the development server:
     ```bash
     npm run dev
     ```
   - This will start the Next.js application on `http://localhost:3000`.

9. Test the authentication flow:
   - Open your web browser and navigate to `http://localhost:3000`.
   - Click on the "Sign in with GitHub" button.
   - You should be redirected to GitHub for authentication.
   - After successful authentication, you will be redirected back to your application.
   - Click to show all your repositories.
   - You should see a list of your GitHub repositories displayed in the application.
     ![List repository](/images/5.github/006-github.png)

### Create a react project to deploy on GitHub

1. Go to an empty folder on your computer where you want to create the GitHub project.
2. Open a terminal in that folder and run the following commands:

   ```bash
   npm create vite@latest my-react-app
   ```

   - This command will prompt you to select a framework. Choose `React` and then select `JavaScript` or `TypeScript` based on your preference.
   - After the project is created, navigate into the project directory:

   ```bash
   cd my-react-app
   npm install
   npm run dev
   ```

   - This will create a new React project using Vite, install the necessary dependencies, and start the development server.

3. Create a vite config file in the root directory of your project:

   - Create a file named `vite.config.js` in the root directory of your project.
   - Add the following content to the `vite.config.js` file:

     ```javascript
     import { defineConfig } from "vite";
     import react from "@vitejs/plugin-react";

     // https://vitejs.dev/config/
     export default defineConfig({
       plugins: [react()],
       base: process.env.VITE_BASE_PATH || "./",
     });
     ```

   - Install dotenv package to manage environment variables:

   ```bash
   npm install dotenv
   ```

   - This configuration sets up Vite to use React and specifies the base path for your application.

4. Create a github project:

   - Go to [github](https://github.com) and create a new repository.
   - Name your repository (e.g: staticwebsite).
   - Initialize the repository with a README file.
   - Click on "Create repository".
     ![Create staticwebsite](/images/5.github/007-github.png)
   - After creating the repository, go to the your project directory and run the following commands to push your project to GitHub:

     ```bash
     git init
     git add .
     git commit -m "first commit"
     git branch -M main
     git remote add origin `Your repository URL`
     git push -u origin main
     ```

   - Replace `Your repository URL` with the URL of your newly created GitHub repository.

5. Testing the deployment feature:

   - Go to your NextJS project in the `webdeploy` folder and run the project
   - After the project is running, go to your browser and navigate to `http://localhost:3000`.
   - Choose the `staticwebsite` that you just created.
   - Click on the `Upload` button (Ensure that you has CORS setup in your API Gateway for this to work).

   ![Deploying a static website](/images/5.github/008-github.png)

6. After the upload is complete, you can view your static website by clicking on the link provided in the application.
   ![Deployment](/images/5.github/009-github.png)
