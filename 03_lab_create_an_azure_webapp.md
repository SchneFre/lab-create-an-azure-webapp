<!-- # LAB: Creating a New Web App Using Azure Portal -->

<!-- # Lab: Create a New Web App Using the Azure Portal -->

In this hands-on lab, you will learn how to **create and deploy a simple web application** using the **Azure Portal**. By the end of this lab, you'll have a functional web app hosted on Azure's App Service, accessible via a web browser. This lab specifically deploys the [Pokfinner/noderino](https://github.com/Pokfinner/noderino) Node.js application, but you can adapt it for your own projects. Let’s get started!

## Prerequisites

Before you begin, ensure you have the following:

1. **Azure Account**: If you don't have one, [sign up for a free Azure account](https://azure.microsoft.com/free/).
2. **Azure Portal Access**: Familiarity with navigating the [Azure Portal](https://portal.azure.com/).
3. **Basic Web Application Code**: For this lab, we will use the [noderino](https://github.com/Pokfinner/noderino) Node.js repository, which contains a simple Node.js server (`server.js`) and a `README`. You can fork this repo or simply reference it in Azure.


## Step 1: Log in to the Azure Portal

1. **Navigate to the Azure Portal**:
   - Open your web browser and go to [https://portal.azure.com](https://portal.azure.com).
2. **Sign In**:
   - Enter your Azure account credentials to log in.

## Step 2: Create a Resource Group

A **Resource Group** is a container that holds related resources for an Azure solution. Organizing resources into resource groups helps manage and monitor them collectively.

1. **Navigate to Resource Groups**:
   - In the left-hand sidebar, click on **"Resource groups"**.
   - If it's not visible, use the search bar at the top and type **"Resource groups"**.

2. **Create a New Resource Group**:
   - Click the **"Add"** button.

3. **Configure the Resource Group**:
   - **Subscription**: Choose your desired Azure subscription.
   - **Resource Group Name**: Enter a name for your resource group (e.g., `MyWebAppRG`).
   - **Region**: Select a region close to your user base or where you want to host your resources (e.g., `East US`).

4. **Review and Create**:
   - Click **"Review + create"**.
   - After validation passes, click **"Create"**.
   
   *Note: The creation may take a few moments. You can check status in the “Notifications” area.*



   <!-- ![Create Resource Group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/media/create-resource-group/portal-create-resource-group.png) -->

## Step 3: Create a New Web App

Azure App Service is a fully managed platform for building, deploying, and scaling web apps. Here’s how to create a new web app to host our Node.js application:

### Basic Configuration

1. **Navigate to App Services**:
   - In the left-hand sidebar, click on **"App Services"**.
   - If it's not visible, use the search bar and type **"App Services"**.

2. **Create a New Web App**:
   - Click the **"Add"** button.

3. **Configure the Web App**:

   - **Basics Tab**:
     - **Subscription**: Ensure your desired subscription is selected.
     - **Resource Group**: Select the resource group you created earlier (`MyWebAppRG`).
     - **Name**: Enter a globally unique name for your web app (e.g., `myuniquewebapp123`). This name will be part of your app's URL (`myuniquewebapp123.azurewebsites.net`).
     - **Publish**: Publish: Choose **“Code**”.
     - **Runtime Stack**: Select “**Node**” (choose the version that best matches your application’s requirements, e.g., Node 16 or 18).
     - **Operating System**: Choose “**Linux**” or “**Windows**”. (Node apps often run on Linux for simplicity.)
     - **Region**: Confirm the region matches your resource group or select as needed.

   <!-- ![Create Web App Basics](https://docs.microsoft.com/en-us/azure/app-service/media/quickstart-create-dotnet-app/portal-create-web-app-01.png) -->

### Hosting Configuration

4. **Configure the Hosting Settings**:
   - **App Service Plan**:
     - Click **"Create new"** to define a new App Service Plan or choose an existing one.
     - **Name**: Enter a name for the plan (e.g., `MyAppServicePlan`).
     - **Operating System**: Should match your earlier selection.
     - **Region**: Should match your resource group.
     - **Pricing Tier**: Click **"Change size"** to select a pricing tier. For beginners, **"Free (F1)"** or **"Basic (B1)"** is suitable. **Free** allows limited usage, while **Basic** provides more features like custom domains.

   <!-- ![Create Web App Hosting](https://docs.microsoft.com/en-us/azure/app-service/media/quickstart-create-dotnet-app/portal-create-web-app-02.png) -->

### Deployment Options (Optional)

5. **Deployment Settings**:
   - **Deployment**: You can enable continuous deployment options now or later. For this lab, we will configure GitHub deployment in a later step.
   - **Monitoring**: You can enable Application Insights for monitoring your app's performance and usage.
   - **Tags**: Optionally, add tags to organize your resources.

6. **Review and Create**:
   - Click **"Review + create"**.
   - After validation passes, click **"Create"** to start the deployment.

   <!-- ![Review and Create Web App](https://docs.microsoft.com/en-us/azure/app-service/media/quickstart-create-dotnet-app/portal-create-web-app-03.png) -->

   **Note**: The deployment process may take a few minutes. You can monitor progress in the **"Notifications"** (bell icon) area.

## Step 4: Deploy Your Web App

Once your web app is created, you need to deploy your **Node.js** code. Azure App Service supports multiple deployment methods, including GitHub, Local Git, FTP, and more. This lab covers **GitHub deployment** and **Local Git deployment** using the *noderino* sample app.

### Using GitHub for Deployment

1. **Navigate to Your Web App**:
   - In the Azure Portal, go to **"App Services"**.
   - Select your newly created web app (e.g., `myuniquewebapp123`).

2. **Set Up Deployment from GitHub**:
   - In the left-hand menu under **"Deployment"**, click **"Deployment Center"**.
   - **Source Control**: Choose **"GitHub"**.
   - **Repository**: Click “**Authorize**” (if needed) to allow Azure to access your GitHub repositories.
   - **Select Repository**: Choose **Pokfinner/noderino** (or your fork of it) and the branch you want to deploy, typically **main**.
   - **Build Provider**: Select **“GitHub Actions**” for a fully integrated CI/CD experience.
   - **Configuration**: If prompted, ensure the Node.js version matches the runtime stack selected when creating the app.

   <!-- ![Deployment Center](https://docs.microsoft.com/en-us/azure/app-service/media/deploy-continuous-deployment/github-actions-deployment-center.png) -->

3. **Complete the Setup**:
   - Click **"Finish"** to start the deployment process.
   - Azure will set up a GitHub Actions workflow in your repository to handle future deployments automatically.

4. **Verify Deployment**:
   - Once the workflow completes, navigate back to your web app’s **"Overview"** page.
   - Click on the “**Browse**” button or use the URL `https://myuniquewebapp123.azurewebsites.net` to view your deployed application.
   - If everything worked, you should see a message like `Hello from /diogo number 0!` (the default path and number in the noderino app).

### Using Local Git Deployment

If you prefer deploying directly from your local machine, follow these steps:

1. **Enable Local Git Deployment**:
   - In your web app's left-hand menu, under **"Deployment"**, click **"Deployment Center"**.
   - **Source**: Choose **"Local Git"**.
   - **Build Provider**: Select “**None**” (or a Node build provider if your code requires one).
   - Click **"Continue"**, then **"Finish"**.

2. **Retrieve Git Clone URL**:
   - After enabling Local Git, Azure will provide a **Git clone URL**. Copy this URL for use in your local Git repository.


3. **Configure Deployment Credentials**:
   - In the left-hand menu, under “**Deployment Center**”, you can also find or set up a **deployment username** and **password** for the Git push.

4. **Deploy via Git**:
   - On your local machine, navigate to your cloned *noderino* project directory (or another Node.js project).
   - Initialize Git if you haven't:
     ```bash
     git init
     git add .
     git commit -m "Initial commit"
     ```
   - Add the Azure remote repository (substitute your actual Azure Git URL)::
     ```bash
     git remote add azure https://<deployment-username>@myuniquewebapp123.scm.azurewebsites.net/myuniquewebapp123.git
     ```
   - Push your code to Azure:
     ```bash
     git push azure master
     ```
   - Enter your **deployment password** when prompted.

5. **Verify Deployment**:
   - After the push completes, navigate to `https://myuniquewebapp123.azurewebsites.net` to see your deployed application.

## Step 5: Access and Test Your Web App

The `noderino` application includes environment variables that customize the server:

- `DESIRED_PATH` — changes the path the server listens on (default `/diogo`).
- `PORT` — changes the port the server listens on (default `8080`). In Azure, this is generally managed by App Service, so you can leave this alone.
- `NUMBER` — changes an arbitrary number displayed on the page (default `0`).

1. **Access Your Web App in a Browser**:

   - Navigate to `https://<Your-Web-App-Name>.azurewebsites.net` (e.g., `https://myuniquewebapp123.azurewebsites.net`).
   - You should see a page saying something like `Hello from /diogo number 0!`.

2. **Set Environment Variables (Optional)**:

   - In the Azure Portal, under your App Service, navigate to **“Configuration”**.
   - Under “**Application settings**”, add new environment variables (e.g., `DESIRED_PATH`, `NUMBER`) and save.
   - Restart the web app or wait for Azure to apply changes automatically. Then refresh your site. If you changed `DESIRED_PATH` to `/hello`, you’d see the message at `https://yourwebapp.azurewebsites.net/hello`.

3. **Verify Functionality**:

   - Ensure that your Node.js web app loads correctly and the path/number display is as expected.

## Step 6: Monitor Your Web App

Azure provides robust monitoring tools to track the performance and health of your web app.

1. **Application Insights**:
   - If you enabled **Application Insights** during setup, it provides detailed telemetry about your application’s performance, user behavior, and exceptions.
   - Access it via **"Monitoring"** > **"Application Insights"** in your web app's menu.

2. **Azure Monitor**:
   - Offers a comprehensive view of your app’s metrics and logs.
   - Set up **Alerts** to notify you of performance issues or outages.

3. **Scaling**:
   - Navigate to **"Scale up (App Service plan)"** or **"Scale out (App Service plan)"** to adjust your app's resources based on demand.

   <!-- ![Scale Web App](https://docs.microsoft.com/en-us/azure/app-service/media/manage-scale-up-scale-out/portal-scale-webapp-02.png) -->

## Step 7: Cleanup (Optional)

To avoid incurring unnecessary charges, it’s recommended to delete the resources you no longer need.

1. **Delete the Web App**:
   - In the Azure Portal, go to **"App Services"**.
   - Select your web app (e.g., `myuniquewebapp123`).
   - Click the **"Delete"** button at the top.
   - Confirm the deletion by typing the web app's name and clicking **"Delete"** again.

2. **Delete the Resource Group** (if no longer needed):
   - Navigating to **"Resource groups"** in the Azure Portal.
   - Select your resource group (`MyWebAppRG`).
   - Click **"Delete resource group"**.
   - Type the resource group name to confirm and click **"Delete"**.

   **Note**: Deleting the resource group will remove all resources contained within it, including the web app, App Service Plan, and any associated resources.

## Best Practices

1. **Use Strong Authentication**:
   - Implement Azure Active Directory (AAD) authentication for your web app to secure access.

2. **Enable HTTPS**:
   - Always use HTTPS to encrypt data in transit. Azure App Service provides free SSL certificates for custom domains.

3. **Configure Auto-Scaling**:
   - Set up auto-scaling rules based on metrics like CPU usage or HTTP queue length to handle traffic spikes efficiently.

4. **Implement CI/CD Pipelines**:
   - Automate deployments using GitHub Actions, Azure DevOps Pipelines, or other CI/CD tools for consistent and reliable releases.

5. **Monitor and Log Effectively**:
   - Regularly review application performance and error logs to maintain optimal functionality and user experience.

6. **Backup and Recovery**:
   - Set up regular backups of your web app and associated databases to prevent data loss.

7. **Optimize Performance**:
   - Utilize Azure CDN, caching strategies, and performance tuning to enhance your web app’s responsiveness and load times.

## **Deliverables**

* **Azure evidence**

  * Screenshot from **App Service → Overview** showing app name, **URL**, region, and status **Running**.
  * Screenshot from **App Service → App Service plan** showing the **plan/tier** (e.g., F1/B1).
  * (If used) Screenshot from **Configuration → Application settings** showing `DESIRED_PATH` / `NUMBER`.

* **Deployment evidence**

  * **GitHub Actions** deployment:

    * Screenshot of **Deployment Center** showing GitHub as the source and the connected repo/branch.
    * Screenshot of a **successful Actions run** (green check) for the workflow created.
  * **OR Local Git** deployment:

    * The **Azure Git remote URL** you used.
    * Terminal output (screenshot or snippet) of `git push azure master` completing successfully.

* **Functional proof**

  * Screenshot of your app responding at
    `https://<your-app-name>.azurewebsites.net`
    (and, if you set it, `/<DESIRED_PATH>`), showing the noderino message (e.g., `Hello from /diogo number 0!`).

* **Optional (nice to have)**

  * Screenshot from **Monitoring → Application Insights** (if enabled) or **Logs/Live Metrics** showing activity.

## **Submission**

Upon completion, add your deliverables to git. Then commit git and push your branch to the remote. Make a pull request and paste the PR link in the submission field in the Student Portal.


## Summary

In this lab, you successfully:

1. **Created a Resource Group** to organize your Azure resources.
2. **Set Up a New Web App** using the Azure Portal, configuring essential settings such as runtime stack, region, and App Service Plan.
3. **Deployed Your Web Application** from the `noderino` GitHub repository (or your own fork) using GitHub Actions or Local Git.
4. **Accessed and Verified** your web app to ensure it was functioning correctly.
5. **Monitored** your web app’s performance and health using Azure’s monitoring tools.
6. **Cleaned Up** resources to manage costs effectively (if needed).


**Congratulations!** You’ve mastered the basics of creating and deploying a Node.js web application on Azure using the Azure Portal. This foundational skill enables you to build, deploy, and manage scalable web applications in the cloud. Feel free to experiment with environment variables and advanced Azure services to further enhance your app.

<br>

*Happy Cloud Deployments! :tada:*