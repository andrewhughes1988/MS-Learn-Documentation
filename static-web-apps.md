# Overview

# What is Azure Static Web Apps?

Azure Static Web Apps is a service that automatically deploys full stack web apps to Azure from a code repository.

The workflow of Azure Static Web Apps is tailored to a developer's daily workflow. Apps are built and deployed based on code changes.

When you create an static web app, Azure interacts directly with GitHub or Azure DevOps to monitor a branch of your choice. Every time you push commits or accept pull requests into the watched branch, a build automatically runs and your app and API deploys to Azure.

Static web apps are commonly built using libraries and web frameworks like Angular, React, Svelte, Vue, or Blazor where server side rendering isn't required. These apps include HTML, CSS, JavaScript, and image assets that make up the application. With a traditional web server, these assets are served from a single server alongside any required API endpoints.

With Static Web Apps, static assets are separated from a traditional web server and are instead served from points geographically distributed around the world. This distribution makes serving files much faster as files are physically closer to end users. In addition, API endpoints are hosted using a [serverless architecture](../azure-functions/functions-overview.md), which avoids the need for a full back-end server altogether.

## Key features

- **Web hosting** for static content like HTML, CSS, JavaScript, and images.

- **Integrated API** support provided by managed Azure Functions, with the option to link an existing function app, web app, container app, or API Management instance using a standard account.  If you need your API in a region that doesn't support [managed functions](apis-functions.md), you can [bring your own functions](functions-bring-your-own.md) to your app.

- **First-class GitHub and Azure DevOps integration** that allows repository changes to trigger builds and deployments.

- **Globally distributed** static content, putting content closer to your users.

- **Free SSL certificates**, which are automatically renewed.

- **Custom domains** to provide branded customizations to your app.

- **Seamless security model** with a reverse-proxy when calling APIs, which requires no CORS configuration.

- **Authentication provider integrations** with Microsoft Entra ID and GitHub.

- **Customizable authorization role definition** and assignments.

- **Back-end routing rules** enabling full control over the content and routes you serve.

- **Generated staging versions** powered by pull requests enabling preview versions of your site before publishing.

- **CLI support** through the [Azure CLI](/cli/azure/staticwebapp) to create cloud resources, and via the [Azure Static Web Apps CLI](https://github.com/Azure/static-web-apps-cli#azure-static-web-apps-cli) for local development.

## What you can do with Static Web Apps

- **Build modern web applications** with JavaScript frameworks and libraries like [Angular](getting-started.md?tabs=angular), [React](getting-started.md?tabs=react), [Svelte](/training/modules/publish-app-service-static-web-app-api/), [Vue](getting-started.md?tabs=vue), or using [Blazor](./deploy-blazor.md) to create WebAssembly applications, with an [Azure Functions](apis-functions.md) back-end.

- **Publish static sites** with frameworks like [Gatsby](publish-gatsby.md), [Hugo](publish-hugo.md), [VuePress](publish-vuepress.md).

- **Deploy web applications** with frameworks like [Next.js](nextjs.md) and [Nuxt.js](deploy-nuxtjs.md).

## Next steps

> [!div class="nextstepaction"]

> [Build your first static app](getting-started.md)


# Getting Started

# Quickstart: Build your first static site with Azure Static Web Apps

Azure Static Web Apps publishes a website by building an app from a code repository. In this quickstart, you deploy an application to Azure Static Web apps using the Visual Studio Code extension.

If you don't have an Azure subscription, [create a free trial account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Prerequisites

- [GitHub](https://github.com) account

- [Azure](https://portal.azure.com) account

- [Visual Studio Code](https://code.visualstudio.com)

- [Azure Static Web Apps extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurestaticwebapps)

- [Install Git](https://www.git-scm.com/downloads)

[!INCLUDE [create repository from template](../../includes/static-web-apps-get-started-create-repo.md)]

[!INCLUDE [clone the repository](../../includes/static-web-apps-get-started-clone-repo.md)]

Next, open Visual Studio Code and go to **File > Open Folder** to open the cloned repository in the editor.

## Install Azure Static Web Apps extension

If you don't already have the [Azure Static Web Apps extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurestaticwebapps) extension, you can install it in Visual Studio Code.

1. Select **View** > **Extensions**.

1. In the **Search Extensions in Marketplace**, type **Azure Static Web Apps**.

1. Select **Install** for **Azure Static Web Apps**.

## Create a static web app

1. Inside Visual Studio Code, select the Azure logo in the Activity Bar to open the Azure extensions window.

> [!NOTE]

> You are required to sign in to Azure and GitHub in Visual Studio Code to continue. If you are not already authenticated, the extension prompts you to sign in to both services during the creation process.

1. Select <kbd>F1</kbd> to open the Visual Studio Code command palette.

1. Enter **Create static web app** in the command box.

1. Select *Azure Static Web Apps: Create static web app...*.

1. Select your Azure subscription.

1. Enter **my-first-static-web-app** for the application name.

1. Select the region closest to you.

1. Enter the settings values that match your framework choice.

# [No Framework](#tab/vanilla-javascript)

| Setting | Value |

| --- | --- |

| Framework | Select **Custom** |

| Location of application code | Enter `/src` |

| Build location | Enter `/src` |

# [Angular](#tab/angular)

| Setting | Value |

| --- | --- |

| Framework | Select **Angular** |

| Location of application code | Enter `/` |

| Build location | Enter `dist/angular-basic` |

# [Blazor](#tab/blazor)

| Setting | Value |

| --- | --- |

| Framework | Select **Blazor** |

| Location of application code | Enter `Client` |

| Build location | Enter `wwwroot` |

# [React](#tab/react)

| Setting | Value |

| --- | --- |

| Framework | Select **React** |

| Location of application code | Enter `/` |

| Build location | Enter `build` |

# [Vue](#tab/vue)

| Setting | Value |

| --- | --- |

| Framework | Select **Vue.js** |

| Location of application code | Enter `/` |

| Build location | Enter `dist` |

---

1. Once the app is created, a confirmation notification is shown in Visual Studio Code.

If GitHub presents you with a button labeled **Enable Actions on this repository**, select the button to allow the build action to run on your repository.

As the deployment is in progress, the Visual Studio Code extension reports the build status to you.

Once the deployment is complete, you can navigate directly to your website.

1. To view the website in the browser, right-click the project in the Static Web Apps extension, and select **Browse Site**.

## Clean up resources

If you're not going to continue to use this application, you can delete the Azure Static Web Apps instance through the extension.

In the Visual Studio Code Azure window, return to the _Resources_ section and under _Static Web Apps_, right-click **my-first-static-web-app** and select **Delete**.

## Related content

* [Video series: Deploy websites to the cloud with Azure Static Web Apps](https://aka.ms/azure/beginnervideos/learn/swa)

## Next steps

> [!div class="nextstepaction"]

> [Add an API](add-api.md)


# Deploy Blazor

# Deploy a Blazor app on Azure Static Web Apps

Azure Static Web Apps publishes a website to a production environment by building apps from a GitHub repository supported by a serverless backend. The following tutorial shows how to deploy C# Blazor WebAssembly app that displays weather data returned by a serverless API.

> [!NOTE]

## Prerequisites

- [GitHub](https://github.com) account

- [Azure](https://portal.azure.com) account. If you don't have an Azure subscription, [create a free trial account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## 1. Create a repository

This article uses a GitHub template repository to make it easy for you to get started. The template features a starter app that you can deploy to Azure Static Web Apps.

1. Make sure you're signed in to GitHub and go to the following location to create a new repository:

[https://github.com/staticwebdev/blazor-starter/generate](https://github.com/login?return_to=/staticwebdev/blazor-starter/generate)

2. Name your repository **my-first-static-blazor-app**.

## 2. Create a static web app

Now that the repository is created, create a static web app from the Azure portal.

1. Go to the [Azure portal](https://portal.azure.com).

1. Select **Create a Resource**.

1. Search for **Static Web Apps**.

1. Select **Static Web App**.

1. Select **Create**.

1. On the _Basics_ tab, enter the following values.

| Property | Value |

| --- | --- |

| _Subscription_ | Your Azure subscription name. |

| _Resource group_ | **my-blazor-group**  |

| _Name_ | **my-first-static-blazor-app** |

| _Plan type_ | **Free** |

| _Region for Azure Functions API and staging environments_ | Select a region closest to you. |

| _Source_ | **GitHub** |

5. Select **Sign in with GitHub** and authenticate with GitHub, if you're prompted.

6. Enter the following GitHub values.

| Property | Value |

| --- | --- |

| _Organization_ | Select your desired GitHub organization. |

| _Repository_ | Select **my-first-static-blazor-app**. |

| _Branch_ | Select **main**. |

> [!NOTE]

> If you don't see any repositories, you may need to authorize Azure Static Web Apps on GitHub. Then browse to your GitHub repository and go to **Settings > Applications > Authorized OAuth Apps,** select **Azure Static Web Apps**, and then select **Grant**. For organization repositories, you must be an owner of the organization to grant the permissions.

7. In the _Build Details_ section, select **Blazor** from the _Build Presets_ drop-down and the following values are populated.

| Property | Value | Description |

| --- | --- | --- |

| App location | **Client** | Folder containing the Blazor WebAssembly app |

| API location | **Api** | Folder containing the Azure Functions app |

| Output location | **wwwroot** | Folder in the build output containing the published Blazor WebAssembly application |

8. Select **Review + Create** to verify the details are all correct.

9. Select **Create** to start the creation of the static web app and provision a GitHub Actions for deployment.

10. Once the deployment is completed, select **Go to resource**.

11. Select **Go to resource**.

## 3. View the website

There are two aspects to deploying a static app. The first provisions the underlying Azure resources that make up your app. The second is a GitHub Actions workflow that builds and publishes your application.

Before you can go to your new static web app, the deployment build must first finish running.

The Static Web Apps overview window displays a series of links that help you interact with your web app.

1. Select the banner that says, _Click here to check the status of your GitHub Actions runs_ to see the GitHub Actions running against your repository. Once you verify the deployment job is complete, then you can go to your website via the generated URL.

2. Once GitHub Actions workflow is complete, you can select the _URL_ link to open the website in new tab.

## 4. Understand the application overview

Together, the following projects make up the parts required to create a Blazor WebAssembly application running in the browser supported by an Azure Functions API backend.

|Visual Studio project |Description |

|---------|---------|

|Api   | The C# Azure Functions application implements the API endpoint that provides weather information to the Blazor WebAssembly app. The **WeatherForecastFunction** returns an array of `WeatherForecast` objects.        |

|Client    |The front-end Blazor WebAssembly project. A [fallback route](#fallback-route) is implemented to ensure client-side routing is functional.         |

|Shared    | Holds common classes referenced by both the Api and Client projects, which allow data to flow from API endpoint to the front-end web app. The [`WeatherForecast`](https://github.com/staticwebdev/blazor-starter/blob/main/Shared/WeatherForecast.cs) class is shared among both apps.        |

**Blazor static web app**

### Fallback route

The app exposes URLs like `/counter` and `/fetchdata`, which map to specific routes of the app. Since this app is implemented as a single page, each route is served the `index.html` file. To ensure that requests for any path return `index.html`, a [fallback route](./configuration.md#fallback-routes) gets implemented in the `staticwebapp.config.json` file found in the client project's root folder.

```json

{

"navigationFallback": {

"rewrite": "/index.html"

}

}

```

The JSON configuration ensures that requests to any route in the app return the `index.html` page.

## Deploy from Visual Studio

As an alternative to deploying via GitHub Actions, you can deploy to Azure Static Web Apps directly from Visual Studio. Create a publish profile for Azure Static Web Apps:

1. In Visual Studio's **Publish** UI, select **Target** > **Azure** > **Specific Target** > **Azure Static Web Apps** to create a [publish profile](/aspnet/core/host-and-deploy/visual-studio-publish-profiles).

1. In the publish profile configuration, provide the **Subscription name**. Select an existing instance, or select **Create a new instance**. When creating a new instance in the Azure portal's **Create Static Web App** UI, set the **Deployment details** > **Source** to **Other**. Wait for the deployment to complete in the Azure portal before proceeding.

1. In the publish profile configuration, select the Azure Static Web Apps instance from the instance's resource group. Select **Finish** to create the publish profile. If Visual Studio prompts to install the Static Web Apps (SWA) CLI, install the CLI by following the prompts. The SWA CLI requires [npm/Node.js (Visual Studio documentation)](/visualstudio/javascript/npm-package-management).

After the publish profile is created, deploy the app to the Azure Static Web Apps instance using the publish profile by selecting the **Publish** button.

## Clean up resources

If you're not going to use this application, you can delete the Azure Static Web Apps instance through the following steps:

1. Open the [Azure portal](https://portal.azure.com).

2. Search for **my-blazor-group** from the top search bar.

3. Select on the group name.

4. Select **Delete**.

5. Select **Yes** to confirm the delete action.

## Next steps

> [!div class="nextstepaction"]

> [Authenticate and authorize](./authentication-authorization.yml)

## Related articles

- [Set up authentication and authorization](authentication-authorization.yml)

- [Configure app settings](application-settings.yml)

- [Enable monitoring](monitor.md)

- [Azure CLI](https://github.com/Azure/static-web-apps-cli)


# Publish Gatsby

# Deploy a Gatsby site to Azure Static Web Apps

This article demonstrates how to create and deploy a [Gatsby](https://www.gatsbyjs.com/docs/) web application to [Azure Static Web Apps](overview.md). The final result is a new Static Web Apps site (with the associated GitHub Actions) that give you control over how the app is built and published.

In this tutorial, you learn how to:

> [!div class="checklist"]

>

> - Create a Gatsby app

> - Setup an Azure Static Web Apps site

> - Deploy the Gatsby app to Azure

[!INCLUDE [quickstarts-free-trial-note](~/reusable-content/ce-skilling/azure/includes/quickstarts-free-trial-note.md)]

## Prerequisites

- An Azure account with an active subscription. If you don't have one, you can [create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- A GitHub account. If you don't have one, you can [create an account for free](https://github.com/join).

- A Git setup installed. If you don't have one, you can [install Git](https://www.git-scm.com/downloads).

- [Node.js](https://nodejs.org) installed.

## Create a Gatsby App

Create a Gatsby app using the Gatsby Command Line Interface (CLI):

1. Open a terminal

1. Use the [npx](https://www.npmjs.com/package/npx) tool to create a new app with the Gatsby CLI. This may take a few minutes.

```bash

npx gatsby new static-web-app

```

1. Go to the newly created app

```bash

cd static-web-app

```

1. Initialize a Git repo

```bash

git init

git add -A

git commit -m "initial commit"

```

> [!NOTE]

> If you are using the latest version of Gatsby you may need to modify the package.json to include

> "engines": {

> "node": ">=18.0.0"

> },

## Push your application to GitHub

You need to have a repository on GitHub to create a new Azure Static Web Apps resource.

1. Create a blank GitHub repository (don't create a README) from [https://github.com/new](https://github.com/new) named **gatsby-static-web-app**.

1. Next, add the GitHub repository you just created as a remote to your local repo. Make sure to add your GitHub username in place of the `<YOUR_USER_NAME>` placeholder in the following command.

```bash

git remote add origin https://github.com/<YOUR_USER_NAME>/gatsby-static-web-app

```

1. Push your local repository up to GitHub.

```bash

git push --set-upstream origin main

```

## Deploy your web app

The following steps show you how to create a new static site app and deploy it to a production environment.

### Create the application

1. Go to the [Azure portal](https://portal.azure.com)

1. Select **Create a Resource**

1. Search for **Static Web Apps**

1. Select **Static Web Apps**

1. Select **Create**

1. On the _Basics_ tab, enter the following values.

| Property | Value |

| --- | --- |

| _Subscription_ | Your Azure subscription name. |

| _Resource group_ | **my-gatsby-group**  |

| _Name_ | **my-gatsby-app** |

| _Plan type_ | **Free** |

| _Region for Azure Functions API and staging environments_ | Select a region closest to you. |

| _Source_ | **GitHub** |

1. Select **Sign in with GitHub** and authenticate with GitHub.

1. Enter the following GitHub values.

| Property | Value |

| --- | --- |

| _Organization_ | Select your desired GitHub organization. |

| _Repository_ | Select **gatsby-static-web-app**. |

| _Branch_ | Select **main**. |

> [!NOTE]

> If you don't see any repositories, you may need to authorize Azure Static Web Apps on GitHub.

> Browse to your GitHub repository and go to **Settings > Applications > Authorized OAuth Apps**, select **Azure Static Web Apps**, and then select **Grant**. For organization repositories, you must be an owner of the organization to grant the permissions.

1. In the _Build Details_ section, select **Gatsby** from the _Build Presets_ drop-down and keep the default values.

### Review and create

1. Select **Review + Create** to verify the details are all correct.

2. Select **Create** to start the creation of the App Service Static Web App and provision a GitHub Actions for deployment.

3. Once the deployment completes, select **Go to resource**.

4. On the resource screen, select the _URL_ link to open your deployed application. You may need to wait a minute or two for the GitHub Actions to complete.

## Clean up resources

[!INCLUDE [cleanup-resource](../../includes/static-web-apps-cleanup-resource.md)]

## Next steps

> [!div class="nextstepaction"]

> [Add a custom domain](custom-domain.md)


# Publish Jekyll

# Deploy a Jekyll site to Azure Static Web Apps

This article demonstrates how to create and deploy a [Jekyll](https://jekyllrb.com/) web application to [Azure Static Web Apps](overview.md).

In this tutorial, you learn how to:

> [!div class="checklist"]

>

> - Create a Jekyll website

> - Setup an Azure Static Web Apps resource

> - Deploy the Jekyll app to Azure

[!INCLUDE [quickstarts-free-trial-note](~/reusable-content/ce-skilling/azure/includes/quickstarts-free-trial-note.md)]

## Prerequisites

- Install [Jekyll](https://jekyllrb.com/docs/installation/)

- You can use the Windows Subsystem for Linux and follow Ubuntu instructions, if necessary.

- An Azure account with an active subscription. If you don't have one, you can [create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- A GitHub account. If you don't have one, you can [create an account for free](https://github.com/join).

- A Git setup installed. If you don't have one, you can [install Git](https://www.git-scm.com/downloads).

## Create Jekyll App

Create a Jekyll app using the Jekyll Command Line Interface (CLI):

1. From the terminal, run the Jekyll CLI to create a new app.

```bash

jekyll new static-app

```

1. Go to the newly created app.

```bash

cd static-app

```

1. Initialize a new Git repository.

```bash

git init

```

1. Commit the changes.

```bash

git add -A

git commit -m "initial commit"

```

## Push your application to GitHub

Azure Static Web Apps uses GitHub to publish your website. The following steps show you how to create a GitHub repository.

1. Create a blank GitHub repo (don't create a README) from [https://github.com/new](https://github.com/new) named **jekyll-azure-static**.

1. Add the GitHub repository as a remote to your local repo. Make sure to add your GitHub username in place of the `<YOUR_USER_NAME>` placeholder in the following command.

```bash

git remote add origin https://github.com/<YOUR_USER_NAME>/jekyll-azure-static

```

1. Push your local repo up to GitHub.

```bash

git push --set-upstream origin main

```

> [!NOTE]

> Your git branch may be named differently than `main`. Replace `main` in this command with the correct value.

## Deploy your web app

The following steps show you how to create a new static site app and deploy it to a production environment.

### Create the application

1. Go to the [Azure portal](https://portal.azure.com)

1. Select **Create a Resource**

1. Search for **Static Web Apps**

1. Select **Static Web Apps**

1. Select **Create**

1. On the _Basics_ tab, enter the following values.

| Property | Value |

| --- | --- |

| _Subscription_ | Your Azure subscription name. |

| _Resource group_ | **jekyll-static-app**  |

| _Name_ | **jekyll-static-app** |

| _Plan type_ | **Free** |

| _Region for Azure Functions API and staging environments_ | Select a region closest to you. |

| _Source_ | **GitHub** |

1. Select **Sign in with GitHub** and authenticate with GitHub.

1. Enter the following GitHub values.

| Property | Value |

| --- | --- |

| _Organization_ | Select your desired GitHub organization. |

| _Repository_ | Select **jekyll-static-app**. |

| _Branch_ | Select **main**. |

> [!NOTE]

> If you don't see any repositories, you may need to authorize Azure Static Web Apps on GitHub.

> Browse to your GitHub repository and go to **Settings > Applications > Authorized OAuth Apps**, select **Azure Static Web Apps**, and then select **Grant**. For organization repositories, you must be an owner of the organization to grant the permissions.

1. In the _Build Details_ section, select **Custom** from the _Build Presets_ drop-down and keep the default values.

1. In the _App location_ box, enter **./**.

1. Leave the _Api location_ box empty.

1. In the _Output location_ box, enter **_site**.

### Review and create

1. Select **Review + Create** to verify the details are all correct.

2. Select **Create** to start the creation of the App Service Static Web App and provision a GitHub Actions for deployment.

3. Once the deployment completes, select **Go to resource**.

4. On the resource screen, select the _URL_ link to open your deployed application. You may need to wait a minute or two for the GitHub Actions to complete.

#### Custom Jekyll settings

When you generate a static web app, a [workflow file](./build-configuration.md) is generated which contains the publishing configuration settings for the application.

To configure environment variables, such as `JEKYLL_ENV`, add an `env` section to the Azure Static Web Apps GitHub Actions in the workflow.

```yaml

- name: Build And Deploy

id: builddeploy

uses: Azure/static-web-apps-deploy@v1

with:

azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN }}

repo_token: ${{ secrets.GITHUB_TOKEN }} # Used for GitHub integrations (i.e. PR comments)

action: "upload"

###### Repository/Build Configurations - These values can be configured to match you app requirements. ######

# For more information regarding Static Web App workflow configurations, please visit: https://aka.ms/swaworkflowconfig

app_location: "/" # App source code path

api_location: "" # Api source code path - optional

output_location: "_site" # Built app content directory - optional

###### End of Repository/Build Configurations ######

env:

JEKYLL_ENV: production

```

## Clean up resources

[!INCLUDE [cleanup-resource](../../includes/static-web-apps-cleanup-resource.md)]

## Next steps

> [!div class="nextstepaction"]

> [Add a custom domain](custom-domain.md)


# Publish Hugo

# Deploy a Hugo site to Azure Static Web Apps

This article demonstrates how to create and deploy a [Hugo](https://gohugo.io/) web application to [Azure Static Web Apps](overview.md). The final result is a new Azure Static Web App with associated GitHub Actions that give you control over how the app is built and published.

In this tutorial, you learn how to:

> [!div class="checklist"]

>

> - Create a Hugo app

> - Setup an Azure Static Web Apps

> - Deploy the Hugo app to Azure

[!INCLUDE [quickstarts-free-trial-note](~/reusable-content/ce-skilling/azure/includes/quickstarts-free-trial-note.md)]

## Prerequisites

- An Azure account with an active subscription. If you don't have one, you can [create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- A GitHub account. If you don't have one, you can [create an account for free](https://github.com/join).

- A Git setup installed. If you don't have one, you can [install Git](https://www.git-scm.com/downloads).

## Create a Hugo App

Create a Hugo app using the Hugo Command Line Interface (CLI):

1. Follow the [installation guide](https://gohugo.io/getting-started/installing/) for Hugo on your OS.

1. Open a terminal

1. Run the Hugo CLI to create a new app.

```bash

hugo new site static-app

```

1. Go to the newly created app.

```bash

cd static-app

```

1. Initialize a Git repo.

```bash

git init

```

1. Ensure that your branch is named `main`.

```bash

git branch -M main

```

1. Next, add a theme to the site by installing a theme as a git submodule and then specifying it in the Hugo config file.

```bash

git submodule add https://github.com/budparr/gohugo-theme-ananke.git themes/ananke

echo 'theme = "ananke"' >> config.toml

```

1. Commit the changes.

```bash

git add -A

git commit -m "initial commit"

```

## Push your application to GitHub

You need a repository on GitHub to connect to Azure Static Web Apps. The following steps show you how to create a repository for your site.

1. Create a blank GitHub repo (don't create a README) from [https://github.com/new](https://github.com/new) named **hugo-static-app**.

1. Add the GitHub repository as a remote to your local repo. Make sure to add your GitHub username in place of the `<YOUR_USER_NAME>` placeholder in the following command.

```bash

git remote add origin https://github.com/<YOUR_USER_NAME>/hugo-static-app

```

1. Push your local repo up to GitHub.

```bash

git push --set-upstream origin main

```

## Deploy your web app

The following steps show you how to create a new static site app and deploy it to a production environment.

### Create the application

1. Go to the [Azure portal](https://portal.azure.com)

1. Select **Create a Resource**

1. Search for **Static Web Apps**

1. Select **Static Web Apps**

1. Select **Create**

1. On the _Basics_ tab, enter the following values.

| Property | Value |

| --- | --- |

| _Subscription_ | Your Azure subscription name. |

| _Resource group_ | **my-hugo-group**  |

| _Name_ | **hugo-static-app** |

| _Plan type_ | **Free** |

| _Region for Azure Functions API and staging environments_ | Select a region closest to you. |

| _Source_ | **GitHub** |

1. Select **Sign in with GitHub** and authenticate with GitHub.

1. Enter the following GitHub values.

| Property | Value |

| --- | --- |

| _Organization_ | Select your desired GitHub organization. |

| _Repository_ | Select **hugo-static-app**. |

| _Branch_ | Select **main**. |

> [!NOTE]

> If you don't see any repositories, you may need to authorize Azure Static Web Apps on GitHub.

> Browse to your GitHub repository and go to **Settings > Applications > Authorized OAuth Apps**, select **Azure Static Web Apps**, and then select **Grant**. For organization repositories, you must be an owner of the organization to grant the permissions.

1. In the _Build Details_ section, select **Hugo** from the _Build Presets_ drop-down and keep the default values.

### Review and create

1. Select **Review + Create** to verify the details are all correct.

2. Select **Create** to start the creation of the App Service Static Web App and provision a GitHub Actions for deployment.

3. Once the deployment completes, select **Go to resource**.

4. On the resource screen, select the _URL_ link to open your deployed application. You may need to wait a minute or two for the GitHub Actions to complete.

#### Custom Hugo version

When you generate a Static Web App, a [workflow file](./build-configuration.md) is generated which contains the publishing configuration settings for the application. You can designate a specific Hugo version in the workflow file by providing a value for `HUGO_VERSION` in the `env` section. The following example configuration demonstrates how to set Hugo to a specific version.

```yaml

jobs:

build_and_deploy_job:

if: github.event_name == 'push' || (github.event_name == 'pull_request' && github.event.action != 'closed')

runs-on: ubuntu-latest

name: Build and Deploy Job

steps:

- uses: actions/checkout@v3

with:

submodules: true

- name: Build And Deploy

id: builddeploy

uses: Azure/static-web-apps-deploy@v1

with:

azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN }}

repo_token: ${{ secrets.GITHUB_TOKEN }} # Used for GitHub integrations (i.e. PR comments)

action: "upload"

###### Repository/Build Configurations - These values can be configured to match you app requirements. ######

# For more information regarding Static Web App workflow configurations, please visit: https://aka.ms/swaworkflowconfig

app_location: "/" # App source code path

api_location: "api" # Api source code path - optional

output_location: "public" # Built app content directory - optional

###### End of Repository/Build Configurations ######

env:

HUGO_VERSION: 0.58.0

```

#### Alternative deployment using SWA CLI

If your Hugo application has dependencies requiring additional setup, such as GoLang modules, you can use the Azure Static Web Apps CLI for deployment directly. Below is an example GitHub Actions workflow that installs the CLI and deploys your application:

```yaml

jobs:

build_and_deploy_job:

runs-on: ubuntu-latest

name: Build and Deploy with SWA CLI

steps:

- name: Checkout code

uses: actions/checkout@v3

with:

submodules: true

- name: Install SWA CLI

run: npm install -g @azure/static-web-apps-cli

- name: Build Hugo site

run: |

# Install Hugo modules

hugo mod get

# Minify the supported output formats

hugo --minify

- name: Deploy with SWA CLI

env:

AZURE_STATIC_WEB_APPS_API_TOKEN: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN }}

run: |

swa deploy ./public --api-location ./api --env production

```

This workflow builds the Hugo site and deploys it using the Azure Static Web Apps CLI. It assumes the `go.mod` file is located in the root directory of your project to manage dependencies and module configurations.

#### Use the Git Info feature in your Hugo application

If your Hugo application uses the [Git Info feature](https://gohugo.io/methods/page/gitinfo/#prerequisites), the default [workflow file](./build-configuration.md) created for the Static Web App uses the [checkout GitHub Action](https://github.com/actions/checkout) to fetch a _shallow_ version of your Git repository, with a default depth of **1**. In this scenario, Hugo sees all your content files as coming from a _single commit_, so they have the same author, last modification timestamp, and other `.GitInfo` variables.

Update your workflow file to [fetch your full Git history](https://github.com/actions/checkout/blob/main/README.md#fetch-all-history-for-all-tags-and-branches) by adding a new parameter under the `actions/checkout` step to set the `fetch-depth` to `0` (no limit):

```yaml

- uses: actions/checkout@v3

with:

submodules: true

fetch-depth: 0

```

Fetching the full history increases the build time of your GitHub Actions workflow, but your `.Lastmod` and `.GitInfo` variables are accurate and available for each of your content files.

## Clean up resources

[!INCLUDE [cleanup-resource](../../includes/static-web-apps-cleanup-resource.md)]

## Next steps

> [!div class="nextstepaction"]

> [Add a custom domain](custom-domain.md)


# Deploy Nextjs Static Export

# Deploy static-rendered Next.js websites on Azure Static Web Apps

In this tutorial, learn to deploy a [Next.js](https://nextjs.org) generated static website to [Azure Static Web Apps](overview.md). For more information about Next.js specifics, see the [starter template readme](https://github.com/staticwebdev/nextjs-starter#readme).

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- A GitHub account. [Create an account for free](https://github.com/join).

- [Node.js](https://nodejs.org) installed.

## 1. Set up a Next.js app

Rather than using the Next.js CLI to create your app, you can use a starter repository. The starter repository contains an existing Next.js app that supports dynamic routes.

To begin, create a new repository under your GitHub account from a template repository.

1. Go to [https://github.com/staticwebdev/nextjs-starter/generate](https://github.com/login?return_to=/staticwebdev/nextjs-starter/generate)

1. Name the repository **nextjs-starter**

1. Next, clone the new repo to your machine. Make sure to replace `<YOUR_GITHUB_ACCOUNT_NAME>` with your account name.

```bash

git clone http://github.com/<YOUR_GITHUB_ACCOUNT_NAME>/nextjs-starter

```

1. Go to the newly cloned Next.js app.

```bash

cd nextjs-starter

```

1. Install dependencies.

```bash

npm install

```

1. Start Next.js app in development.

```bash

npm run dev

```

1. Go to `http://localhost:3000` to open the app, where you should see the following website open in your preferred browser:

When you select a framework or library, you see a details page about the selected item:

## 2. Create a static app

The following steps show how to link your app to Azure Static Web Apps. Once in Azure, you can deploy the application to a production environment.

1. Go to the [Azure portal](https://portal.azure.com).

1. Select **Create a Resource**.

1. Search for **Static Web Apps**.

1. Select **Static Web App**.

1. Select **Create**.

1. On the _Basics_ tab, enter the following values.

| Property | Value |

| --- | --- |

| _Subscription_ | Your Azure subscription name. |

| _Resource group_ | **my-nextjs-group**  |

| _Name_ | **my-nextjs-app** |

| _Plan type_ | **Free** |

| _Region for Azure Functions API and staging environments_ | Select a region closest to you. |

| _Source_ | **GitHub** |

1. Select **Sign in with GitHub** and authenticate with GitHub, if prompted.

1. Enter the following GitHub values.

| Property | Value |

| --- | --- |

| _Organization_ | Select the appropriate GitHub organization. |

| _Repository_ | Select **nextjs-starter**. |

| _Branch_ | Select **main**. |

1. In the _Build Details_ section, select **Custom** from the _Build Presets_. Add the following values as for the build configuration.

| Property | Value |

| --- | --- |

| _App location_ | Enter **/** in the box. |

| _Api location_ | Leave this box empty. |

| _Output location_ | Enter **out** in the box. |

## 3. Review and create

1. Select **Review + Create** to verify the details are all correct.

1. Select **Create** to start the creation of the App Service Static Web App and provision a GitHub Actions for deployment.

1. Once the deployment completes select, **Go to resource**.

1. On the _Overview_ window, select the *URL* link to open your deployed application.

If the website doesn't load immediately, then the build is still running. To check the status of the Actions workflow, navigate to the Actions dashboard for your repository:

```url

https://github.com/<YOUR_GITHUB_USERNAME>/nextjs-starter/actions

```

Once the workflow is complete, you can refresh the browser to view your web app.

Now any changes made to the `main` branch start a new build and deployment of your website.

## 4. Sync changes

When you created the app, Azure Static Web Apps created a GitHub Actions file in your repository. Synchronize with the server by pulling down the latest to your local repository.

Return to the terminal and run the following command `git pull origin main`.

### Configuring Static Rendering

By default, the application is treated as a hybrid rendered Next.js application, but to continue using it as a static site generator, you need to update the deployment task.

1. Open the repository in Visual Studio Code.

1. Navigate to the GitHub Actions file that Azure Static Web Apps added to your repository at `.github/workflows/azure-static-web-apps-<your site ID>.yml`

1. Update the _Build and Deploy_ job to have an environment variable of `IS_STATIC_EXPORT` set to `true`:

### [GitHub Actions](#tab/github-actions)

```yaml

- name: Build And Deploy

id: swa

uses: azure/static-web-apps-deploy@latest

with:

azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_TOKEN }}

repo_token: ${{ secrets.GITHUB_TOKEN }} # Used for GitHub integrations (i.e. PR comments)

action: "upload"

app_location: "/" # App source code path

api_location: "" # Api source code path - optional

output_location: "" # Built app content directory - optional

env: # Add environment variables here

IS_STATIC_EXPORT: true

```

### [Azure Pipelines](#tab/azure-pipelines)

```yaml

- task: AzureStaticWebApp@0

inputs:

azure_static_web_apps_api_token: $(AZURE_STATIC_WEB_APPS_TOKEN)

###### Repository/Build Configurations - These values can be configured to match your app requirements. ######

# For more information regarding Static Web App workflow configurations, please visit: https://aka.ms/swaworkflowconfig

app_location: "/" # App source code path

api_location: "" # Api source code path - optional

output_location: "" # Built app content directory - optional

is_static_export: true # For running Static Next.js file - optional

```

1. Commit the changes to git and push them to GitHub.

```bash

git commit -am "Configuring static site generation" && git push

```

Once the build has completed, the site will be statically rendered.

## Clean up resources

If you're not going to continue to use this app, you can delete the Azure Static Web Apps instance through the following steps.

1. Open the [Azure portal](https://portal.azure.com).

1. Search for **my-nextjs-group** from the top search bar.

1. Select on the group name.

1. Select **Delete**.

1. Select **Yes** to confirm the delete action.

## Next steps

> [!div class="nextstepaction"]

> [Set up a custom domain](custom-domain.md)

## Related articles

- [Set up authentication and authorization](authentication-authorization.yml)

- [Configure app settings](application-settings.yml)

- [Enable monitoring](monitor.md)

- [Azure CLI](https://github.com/Azure/static-web-apps-cli)


# Deploy Nextjs Hybrid

# Deploy hybrid Next.js websites on Azure Static Web Apps (Preview)

In this tutorial, you learn to deploy a [Next.js](https://nextjs.org) website to [Azure Static Web Apps](overview.md), using the support for Next.js features such as React Server Components, Server-Side Rendering (SSR), and API routes.

>[!NOTE]

> Next.js hybrid support is in preview.

## Prerequisites

| Resource | Description |

|---|---|

| [Azure account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) | If you don't have an Azure account with an active subscription, you can [create one for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). |

| [GitHub account](https://github.com/join) | If you don't have a GitHub account, you can [create an account for free](https://github.com/join). |

| [Node.js](https://nodejs.org) | Install the latest version of Node.js. |

| [Next.js CLI](https://nextjs.org/docs/getting-started) | Install the latest version of the Next.js CLI. See the [Next.js Getting Started guide](https://nextjs.org/docs/getting-started) for details. |

[!INCLUDE [Unsupported Next.js features](../../includes/static-web-apps-nextjs-unsupported.md)]

## Create a repository

This article uses a GitHub template repository to make it easy for you to get started. The template features a starter app to deploy to Azure Static Web Apps.

1. Navigate to the following location to create a new repository.

[https://github.com/staticwebdev/nextjs-hybrid-starter/generate](https://github.com/login?return_to=%2Fstaticwebdev%2Fnextjs-hybrid-starter%2Fgenerate)

1. Name your repository **my-first-static-web-app**

1. Select **Create repository from template**.

## Create a static web app

Now that the repository is created, you can create a static web app from the Azure portal.

1. Go to the [Azure portal](https://portal.azure.com).

1. Select **Create a Resource**.

1. Search for **Static Web Apps**.

1. Select **Static Web Apps**.

1. Select **Create**.

In the _Basics_ section, begin by configuring your new app and linking it to a GitHub repository.

| Setting | Value |

|--|--|

| Subscription | Select your Azure subscription. |

| Resource Group | Select the **Create new** link, and enter **static-web-apps-test** in the textbox. |

| Name | Enter **my-first-static-web-app** in the textbox. |

| Plan type | Select **Free**. |

| Source | Select **GitHub** and sign in to GitHub if necessary. |

Select **Sign-in with GitHub** and authenticate with GitHub.

After you sign in with GitHub, enter the repository information.

| Setting | Value |

|--|--|

| Organization | Select your organization. |

| Repository| Select **my-first-web-static-app**. |

| Branch | Select **main**. |

> [!NOTE]

> If you don't see any repositories:

> - You may need to authorize Azure Static Web Apps in GitHub. Browse to your GitHub repository and go to **Settings > Applications > Authorized OAuth Apps**, select **Azure Static Web Apps**, and then select **Grant**.

> - You may need to authorize Azure Static Web Apps in your Azure DevOps organization. You must be an owner of the organization to grant the permissions. Request third-party application access via OAuth. For more information, see [Authorize access to REST APIs with OAuth 2.0](/azure/devops/integrate/get-started/authentication/oauth).

In the _Build Details_ section, add configuration details specific to your preferred front-end framework.

1. Select **Next.js** from the _Build Presets_ dropdown.

1. Keep the default value in the _App location_ box.

1. Leave the _Api location_ box empty.

1. Leave the _Output location_ box empty.

Select **Review + create**.

## View the website

There are two aspects to deploying a static app. The first creates the underlying Azure resources that make up your app. The second is a workflow that builds and publishes your application.

Before you can go to your new static site, the deployment build must first finish running.

The Static Web Apps Overview window displays a series of links that help you interact with your web app.

Selecting on the banner that says, Select here to check the status of your GitHub Actions runs takes you to the GitHub Actions running against your repository. Once you verify the deployment job is complete, then you can go to your website via the generated URL.

Once GitHub Actions workflow is complete, you can select the URL link to open the website in new tab.

## Set up your Next.js project locally to make changes

1. Clone the new repo to your machine. Make sure to replace <GITHUB_ACCOUNT_NAME> with your account name.

```bash

git clone http://github.com/<GITHUB_ACCOUNT_NAME>/my-first-static-web-app

```

1. Open the project in Visual Studio Code or your preferred code editor.

## Set up server side rendering

A managed backend is automatically available for every hybrid Next.js deployment in all plans. However, you can fine-tune performance and take more control of the backend by assigning a custom backend to your site. If you switch between a managed backend to a linked backend, your site experiences no downtime.

### Bring your own backend

You can improve performance and gain more control over the Next.js server side rendering when you bring your backend. Use the following steps to set up a custom backend for your site.

[!INCLUDE [Server side rendering](../../includes/static-web-apps/static-web-apps-nextjs-backends.md)]

## Add Server-Rendered data with a Server Component

To add server-rendered data in your Next.js project using the App Router, edit a Next.js component to add a server-side operation to render data in the component. By default, Next.js components are [Server Components](https://nextjs.org/docs/app/building-your-application/data-fetching/fetching-caching-and-revalidating) that can be server-rendered.

1. Open the `app/page.tsx` file and add an operation that sets the value of a server-side computed variable. Examples include fetching data or other server operations.

```ts

export default function Home() {

const timeOnServer = new Date().toLocaleTimeString('en-US');

return(

...

);

}

```

1. Import `unstable_noStore` from `next/cache` and call it within the `Home` component to ensure the route is dynamically rendered.

```ts

import { unstable_noStore as noStore } from 'next/cache';

export default function Home() {

noStore();

const timeOnServer = new Date().toLocaleTimeString('en-US');

return(

...

);

}

```

>[!NOTE]

>This example forces dynamic rendering of this component to demonstrate server-rendering of the server's current time. The App Router model of Next.js recommends caching individual data requests to optimize the performance of your Next.js app. Read more on [data fetching and caching in Next.js](https://nextjs.org/docs/app/building-your-application/data-fetching/fetching-caching-and-revalidating).

1. Update the `Home` component in _app/pages.tsx_ to render the server-side data.

```ts

import { unstable_noStore as noStore } from 'next/cache';

export default function Home() {

noStore();

const timeOnServer = new Date().toLocaleTimeString('en-US');

return(

<main className="flex min-h-screen flex-col items-center justify-between p-24">

<div>

This is a Next.js application hosted on Azure Static Web Apps with hybrid rendering. The time on the server is <strong>{timeOnServer}</strong>.

</div>

</main>

);

}

```

## Adding an API route

In addition to Server Components, Next.js provides [Route Handlers](https://nextjs.org/docs/app/building-your-application/routing/route-handlers) you can use to create API routes to your Next.js application. You can fetch these APIs in [Client Components](https://nextjs.org/docs/app/building-your-application/rendering/client-components).

Begin by adding an API route.

1. Create a new file at `app/api/currentTime/route.tsx`. This file holds the Route Handler for the new API endpoint.

1. Add a handler function to return data from the API.

```ts

import { NextResponse } from 'next/server';

export const dynamic = 'force-dynamic';

export async function GET() {

const currentTime = new Date().toLocaleTimeString('en-US');

return NextResponse.json({

message: `Hello from the API! The current time is ${currentTime}.`

});

}

```

1. Create a new file at `app/components/CurrentTimeFromAPI.tsx`. This component creates a container for the Client Component that fetches the API from the browser.

1. Add a client component that fetches the API in this file.

```ts

'use client';

import { useEffect, useState } from 'react';

export function CurrentTimeFromAPI(){

const [apiResponse, setApiResponse] = useState('');

const [loading, setLoading] = useState(true);

useEffect(() => {

fetch('/api/currentTime')

.then((res) => res.json())

.then((data) => {

setApiResponse(data.message);

setLoading(false);

});

},

[]);

return (

<div className='pt-4'>

The message from the API is: <strong>{apiResponse}</strong>

</div>

)

}

```

This Client Component fetches the API with a `useEffect` React hook to render the component after the load is complete. The `'use client'` directive identifies this element as a Client Component. For more information, see [Client Components](https://nextjs.org/docs/app/building-your-application/rendering/client-components).

1. Edit _app/page.tsx_ to import and render the `CurrentTimeFromAPI` Client Component.

```ts

import { unstable_noStore as noStore } from 'next/cache';

import { CurrentTimeFromAPI } from './components/CurrentTimeFromAPI';

export default function Home() {

noStore();

const timeOnServer = new Date().toLocaleTimeString('en-US');

return(

<main className="flex min-h-screen flex-col items-center justify-between p-24">

<div>

This is a Next.js application hosted on Azure Static Web Apps with hybrid rendering. The time on the server is <strong>{timeOnServer}</strong>.

</div>

<CurrentTimeFromAPI />

</main>

);

}

```

1. The result from the API route is displayed on the page.

## Configure the runtime version for Next.js

Certain Next.js versions require specific Node.js versions. To configure a specific Node version, you can set the `engines` property of your `package.json` file to designate a version.

```json

{

...

"engines": {

"node": "18.17.1"

}

}

```

## Set environment variables for Next.js

Next.js uses environment variables at build time and at request time, to support both static page generation and dynamic page generation with server-side rendering. Therefore, set environment variables both within the build and deploy task, and in the _Environment variables_ of your Azure Static Web Apps resource.

```yml

...

- name: Build And Deploy

id: builddeploy

uses: Azure/static-web-apps-deploy@v1

with:

azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN }}

repo_token: ${{ secrets.GITHUB_TOKEN }} # Used for GitHub integrations (i.e. PR comments)

action: "upload"

app_location: "/"

api_location: ""

output_location: ""

env:

DB_HOST: ${{ secrets.DB_HOST }}

DB_USER: ${{ secrets.DB_USER }}

DB_DATABASE: ${{ secrets.DB_DATABASE }}

DB_PASSWORD: ${{ secrets.DB_PASSWORD }}

DB_PORT: ${{ secrets.DB_PORT }}

...

```

## Enable standalone feature

When your application size exceeds 250 MB, the Next.js [Output File Tracing](https://nextjs.org/docs/advanced-features/output-file-tracing) feature helps optimize the app size and enhance performance.

Output File Tracing creates a compressed version of the whole application with necessary package dependencies. This package is built into a folder named _.next/standalone_. With this package, your app can deploy on its own without _node_modules_ dependencies.

In order to enable the `standalone` feature, add the following property to your `next.config.js`:

```js

module.exports ={

output:"standalone",

}

```

Next, configure the `build` command in the `package.json` file in order to copy static files to your standalone output.

```json

{

...

"scripts": {

...

"build": "next build && cp -r .next/static .next/standalone/.next/ && cp -r public .next/standalone/"

...

}

...

}

```

## Configure routing and middleware for deployment

You can configure your Next.js project handle of routes with custom redirects, rewrites, and middleware. These handlers are commonly used for authentication, personalization, routing, and internationalization. Custom handling affects the default routing of your Next.js site and the configuration must be compatible with hosting on Static Web Apps.

Static Web Apps validates that your Next.js site is successfully deployed by adding a page to your site at build time. The page is named `public/.swa/health.html`, and Static Web Apps verifies the successful startup and deployment of your site by navigating to `/.swa/health.html` and verifying a successful response. Middleware and custom routing, which includes redirects and rewrites, can affect the access of the `/.swa/health.html` path, which can prevent Static Web Apps' deployment validation. To configure middleware and routing for a successful deployment to Static Web Apps, follow these steps:

1. Exclude routes starting with `.swa` in your `middleware.ts` (or `.js`) file in your middleware configuration.

```js

export const config = {

matcher: [

/*

* Match all request paths except for the ones starting with:

* - .swa (Azure Static Web Apps)

*/

'/((?!.swa).*)',

],

}

```

1. Configure your redirects in `next.config.js` to exclude routes starting with `.swa`.

```js

module.exports = {

async redirects() {

return [

{

source: '/((?!.swa).*)<YOUR MATCHING RULE>',

destination: '<YOUR REDIRECT RULE>',

permanent: false,

},

]

},

};

```

1. Configure your rewrite rules in `next.config.js` to exclude routes starting with `.swa`.

```js

module.exports = {

async rewrites() {

return {

beforeFiles: [

{

source: '/((?!.swa).*)<YOUR MATCHING RULE>',

destination: '<YOUR REWRITE RULE>',

}

]

}

},

};

```

These code snippets exclude paths that start with `.swa` to stop your custom routing or middleware from processing these requests. These rules ensure that the paths resolve as expected during deployment validation.

## Enable logging for Next.js

Following best practices for Next.js server API troubleshooting, add logging to the API to catch these errors. Logging on Azure uses **Application Insights**. In order to preload this SDK, you need to create a custom startup script. To learn more:

* [Example preload script for Application Insights + Next.js](https://medium.com/microsoftazure/enabling-the-node-js-application-insights-sdk-in-next-js-746762d92507)

* [GitHub issue](https://github.com/microsoft/ApplicationInsights-node.js/issues/808)

* [Preloading with Next.js](https://jake.tl/notes/2021-04-04-nextjs-preload-hack)

## Clean up resources

[!INCLUDE [clean up](../../includes/static-web-apps/static-web-apps-tutorials-portal-clean-up.md)]

## Next steps

> [!div class="nextstepaction"]

> [Configure app settings](./application-settings.yml)


# Deploy Nuxtjs

# Deploy Nuxt 3 sites with universal rendering on Azure Static Web Apps

In this tutorial, you learn to deploy a [Nuxt 3](https://v3.nuxtjs.org/) application to [Azure Static Web Apps](overview.md). Nuxt 3 supports [universal (client-side and server-side) rendering](https://v3.nuxtjs.org/guide/concepts/rendering/#universal-rendering), including server and API routes. Without extra configuration, you can deploy Nuxt 3 apps with universal rendering to Azure Static Web Apps. When the app is built in the Static Web Apps GitHub Action or Azure Pipelines task, Nuxt 3 automatically converts it into static assets and an Azure Functions app that are compatible with Azure Static Web Apps.

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- A GitHub account. [Create an account for free](https://github.com/join).

- [Node.js](https://nodejs.org) 16 or later installed.

## Set up a Nuxt 3 app

You can set up a new Nuxt project using `npx nuxi init nuxt-app`. Instead of using a new project, this tutorial uses an existing repository set up to demonstrate how to deploy a Nuxt 3 site with universal rendering on Azure Static Web Apps.

1. Navigate to [http://github.com/staticwebdev/nuxt-3-starter/generate](https://github.com/login?return_to=/staticwebdev/nuxt-3-starter/generate).

1. Name the repository **nuxt-3-starter**.

1. Next, clone the new repo to your machine. Make sure to replace <YOUR_GITHUB_ACCOUNT_NAME> with your account name.

```bash

git clone http://github.com/<YOUR_GITHUB_ACCOUNT_NAME>/nuxt-3-starter

```

1. Navigate to the newly cloned Nuxt.js app:

```bash

cd nuxt-3-starter

```

1. Install dependencies:

```bash

npm install

```

1. Start Nuxt.js app in development:

```bash

npm run dev -- -o

```

Navigate to `http://localhost:3000` to open the app, where you should see the following website open in your preferred browser. Select the buttons to invoke server and API routes.

## Deploy your Nuxt 3 site

The following steps show how to create an Azure Static Web Apps resource and configure it to deploy your app from GitHub.

### Create an Azure Static Web Apps resource

1. Navigate to the [Azure portal](https://portal.azure.com).

1. Select **Create a Resource**.

1. Search for **Static Web Apps**.

1. Select **Static Web Apps**.

1. Select **Create**.

1. On the _Basics_ tab, enter the following values.

| Property | Value |

| --- | --- |

| _Subscription_ | Your Azure subscription name. |

| _Resource group_ | **my-nuxtjs-group**  |

| _Name_ | **my-nuxt3-app** |

| _Plan type_ | **Free** |

| _Region for Azure Functions API and staging environments_ | Select a region closest to you. |

| _Source_ | **GitHub** |

1. Select **Sign in with GitHub** and authenticate with GitHub.

1. Enter the following GitHub values.

| Property | Value |

| --- | --- |

| _Organization_ | Select your desired GitHub organization. |

| _Repository_ | Select the repository you created earlier. |

| _Branch_ | Select **main**. |

1. In the _Build Details_ section, select **Custom** from the _Build Presets_ drop-down and keep the default values.

1. In the _App location_, enter **/** in the box.

1. In the _Api location_, enter **.output/server** in the box.

1. In the _Output location_, enter **.output/public** in the box.

### Review and create

1. Select **Review + Create** to verify the details are all correct.

1. Select **Create** to start the creation of the static web app and provision a GitHub Actions for deployment.

1. Once the deployment completes, select **Go to resource**.

1. On the _Overview_ window, select the *URL* link to open your deployed application.

If the website does not immediately load, then the background GitHub Actions workflow is still running. Once the workflow is complete you can then refresh the browser to view your web app.

You can check the status of the Actions workflows by navigating to the Actions for your repository:

```url

https://github.com/<YOUR_GITHUB_USERNAME>/nuxt-3-starter/actions

```

### Synchronize changes

When you created the app, Azure Static Web Apps created a GitHub Actions workflow file in your repository. Return to the terminal and run the following command to pull the commit containing the new file.

```bash

git pull

```

Make changes to the app by updating the code and pushing it to GitHub. GitHub Actions automatically builds and deploys the app.

For more information, see the Azure Static Web Apps Nuxt 3 deployment preset [documentation](https://nitro.unjs.io/deploy/providers/azure#azure-static-web-apps).

> [!div class="nextstepaction"]

> [Set up a custom domain](custom-domain.md)


# Publish Vuepress

# Tutorial: Publish a VuePress site to Azure Static Web Apps

This article demonstrates how to create and deploy a [VuePress](https://vuepress.vuejs.org/) web application to [Azure Static Web Apps](overview.md). The final result is a new Azure Static Web Apps application with the associated GitHub Actions that give you control over how the app is built and published.

In this tutorial, you learn how to:

> [!div class="checklist"]

>

> - Create a VuePress app

> - Setup an Azure Static Web Apps

> - Deploy the VuePress app to Azure

## Prerequisites

- An Azure account with an active subscription. If you don't have one, you can [create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- A GitHub account. If you don't have one, you can [create an account for free](https://github.com/join).

- A Git setup installed. If you don't have one, you can [install Git](https://www.git-scm.com/downloads).

- [Node.js](https://nodejs.org) installed.

## Create a VuePress App

Create a VuePress app from the Command Line Interface (CLI):

1. Create a new folder for the VuePress app.

```bash

mkdir static-site

```

1. Add a _README.md_ file the folder.

```bash

echo '# Hello From VuePress' > README.md

```

1. Initialize the _package.json_ file.

```bash

npm init -y

```

1. Add VuePress as a `devDependency`.

```bash

npm install --save-dev vuepress

```

1. Open the _package.json_ file in a text editor and add a build command to the [`scripts`](https://docs.npmjs.com/cli/v11/commands/npm-run) section.

```json

...

"scripts": {

"build": "vuepress build"

}

...

```

1. Create a _.gitignore_ file to exclude the _node\_modules_ folder.

```bash

echo 'node_modules' > .gitignore

```

1. Initialize a Git repo.

```bash

git init

git add -A

git commit -m "initial commit"

```

## Push your application to GitHub

You need a repository on GitHub to connect to Azure Static Web Apps. The following steps show you how to create a repository for your site.

1. Create a blank GitHub repo (don't create a README) from [https://github.com/new](https://github.com/new) named **vuepress-static-app**.

1. Add the GitHub repository as a remote to your local repo. Make sure to add your GitHub username in place of the `<YOUR_USER_NAME>` placeholder in the following command.

```bash

git remote add origin https://github.com/<YOUR_USER_NAME>/vuepress-static-app

```

1. Push your local repo up to GitHub.

```bash

git push --set-upstream origin main

```

## Deploy your web app

The following steps show you how to create a new static site app and deploy it to a production environment.

### Create the application

1. Go to the [Azure portal](https://portal.azure.com)

1. Select **Create a Resource**

1. Search for **Static Web Apps**

1. Select **Static Web Apps**

1. Select **Create**

1. On the _Basics_ tab, enter the following values.

| Property | Value |

| --- | --- |

| _Subscription_ | Your Azure subscription name. |

| _Resource group_ | **my-vuepress-group**  |

| _Name_ | **vuepress-static-app** |

| _Plan type_ | **Free** |

| _Region for Azure Functions API and staging environments_ | Select a region closest to you. |

| _Source_ | **GitHub** |

1. Select **Sign in with GitHub** and authenticate with GitHub.

1. Enter the following GitHub values.

| Property | Value |

| --- | --- |

| _Organization_ | Select your desired GitHub organization. |

| _Repository_ | Select **vuepress-static-app**. |

| _Branch_ | Select **main**. |

> [!NOTE]

> If you don't see any repositories, you may need to authorize Azure Static Web Apps on GitHub.

> Browse to your GitHub repository and go to **Settings > Applications > Authorized OAuth Apps**, select **Azure Static Web Apps**, and then select **Grant**. For organization repositories, you must be an owner of the organization to grant the permissions.

1. In the _Build Details_ section, select **VuePress** from the _Build Presets_ drop-down and keep the default values.

### Review and create

1. Select **Review + Create** to verify the details are all correct.

2. Select **Create** to start the creation of the App Service Static Web App and provision a GitHub Actions for deployment.

3. Once the deployment completes, select **Go to resource**.

4. On the resource screen, select the _URL_ link to open your deployed application. You may need to wait a minute or two for the GitHub Actions to complete.

### Clean up resources

[!INCLUDE [cleanup-resource](../../includes/static-web-apps-cleanup-resource.md)]

## Next steps

> [!div class="nextstepaction"]

> [Add a custom domain](custom-domain.md)


# Configuration Overview

# Configuration overview

The following different concepts apply to configuring a static web app.

- [Application configuration](./configuration.md): Define rules in the `staticwebapp.config.json` file to control application behavior and features. Use this file to define route and security rules, custom headers, and networking settings.

- [Build configuration](./build-configuration.md): Define settings that control the build process.

- [Application settings](./application-settings.yml): Set application-level settings and environment variables that can be used by backend APIs.

## Example scenarios

| If you want to... | then... |

|---|---|

| Define routing rules | [Create rules in the staticwebapp.config.json file](./configuration.md) |

| Set which branch triggers builds | [Update the tracked branch name in the build configuration file](./build-configuration.md)  |

| Define which security roles have access to a route | [Secure routes with roles in the staticwebapp.config.json file](./configuration.md#securing-routes-with-roles) |

| Set which HTML file is served if a route doesn't match an actual file | [Define fallback route in the staticwebapp.config.json file](./configuration.md#fallback-routes) |

| Set global headers for HTTP requests | [Define global headers in the staticwebapp.config.json file](./configuration.md#global-headers)|

| Define a custom build command | [Set a custom build command value in the application configuration file](./build-configuration.md) |

| Set an environment variable for a frontend build | [Define an environment variable in the build configuration file](./build-configuration.md#environment-variables) |

| Set an environment variable for an API | [Set an application setting in the portal](./application-settings.yml) |

## Next steps

> [!div class="nextstepaction"]

> [Application configuration](configuration.md)


# Apis Overview

# Overview of API support in Azure Static Web Apps

Front end web applications often call back end APIs for data and services. Azure Static Web Apps provides built-in serverless API endpoints via integration with Azure services.

Key features of Azure Static Web Apps APIs include:

- **Integrated security** with direct access to user [authentication and role-based authorization](user-information.md) data.

- **Seamless routing** that makes the back-end `/api` route available to the front-end web app without requiring custom CORS rules.

## API options

The following Azure services can be integrated with Azure Static Web Apps:

| Service | Managed | Bring your own |

| --- | --- |

| [Azure Functions](apis-functions.md) | ✔ | ✔ |

| [Azure API Management](apis-api-management.md) |  | ✔ |

| [Azure App Service](apis-app-service.md) |  | ✔ |

| [Azure Container Apps](apis-container-apps.md) |  | ✔ |

- **Managed APIs**: By default, Azure Static Web Apps automatically integrates with Azure Functions as an API backend. You deploy an API with your static web app without managing a separate Azure Functions resource.

- **Bring your own APIs**: You can integrate your static web app with existing APIs hosted in Azure Functions, API Management, App Service, or Container Apps. You manage and deploy the API resources yourself.

> [!NOTE]

> Bring your own APIs is only available in the Azure Static Web Apps Standard plan. Built-in, managed Azure Functions APIs are available in all Azure Static Web Apps plans.

## <a name="constraints"></a>API constraints

The following constraints apply to all API backends:

- Each static web app environment can only be configured with one type of backend API at a time.

- The API route prefix must be `/api`.

- Route rules for APIs only support [redirects](configuration.md#define-routes) and [securing routes with roles](configuration.md#securing-routes-with-roles).

- Only HTTP requests are supported for APIs. WebSocket, for example, is not supported.

- The maximum duration of each API request 45 seconds.

- Network isolated backends are not supported.

The following constraints apply to Bring your own API backends:

- An application must be deployed to your static web app before requests to the `/api` route can be resolved.

- Bring your own API backends cannot be linked to a Static Web Apps pull request environment.

## Next steps

> [!div class="nextstepaction"]

> [Add an API](add-api.md)


# Review Publish Pull Requests

# Review pull requests in pre-production environments

This article shows you how to use pre-production environments to review changes to applications that are deployed with [Azure Static Web Apps](overview.md). A pre-production environment is a fully functional staged version of your application that includes changes not available in production.

> [!Note]

> Pull request environments are not automatically supported for Azure DevOps, but you can use [named environments](./named-environments.md) to set them up manually.

Azure Static Web Apps generates a YAML workflow in the repo. When a pull request is created against a branch that the workflow watches, the pre-production environment gets built. The pre-production environment stages the app, so you can review the changes before you push them to production. The lifecycle of a pre-production environment is tied to the pull request. Once the pull request is closed, the pre-production environment is automatically deleted.

You can do the following tasks within pre-production environments:

- Review visual changes between production and staging, like updates to content and layout

- Demonstrate the changes to your team

- Compare different versions of your application

- Validate changes using acceptance tests

- Perform sanity checks before you deploy to production

## Prerequisites

- An existing GitHub repo configured with Azure Static Web Apps. See [Building your first static app](getting-started.md) if you don't have one.

## Make a change

Make a change in your repo directly on GitHub, as shown in the following steps.

1. Go to your project's repo on GitHub, and then select **Branch**.

1. Enter a branch name and select **Create branch**.

1. Go to your _app_ folder and change some text content, like a title or paragraph. Select **Edit** to make the change in the file.

1. Select **Commit changes** when you're done.

## Create a pull request

Create a pull request to publish your update.

1. Open the **Pull request** tab of your project on GitHub.

1. Select **Compare & pull request**.

1. Optionally, enter details about your changes, and then select **Create pull request**.

Assign reviewers and add comments to discuss your changes, if needed.

Multiple pre-production environments can co-exist at the same time when you use Azure Static Web Apps. Each time you create a pull request against the watched branch, a staged version with your changes deploys to a distinct pre-production environment.

You can make multiple changes and push new commits to your branch. The pull request automatically updates to reflect all changes.

## Review changes

The [GitHub Actions](https://github.com/features/actions) deployment workflow runs and deploys your pull request changes to a pre-production environment.

Once the workflow completes building and deploying your app, the GitHub bot adds a comment to your pull request, which contains the URL of the pre-production environment.

1. Select the pre-production URL to see your staged changes.

The URL is composed like this: `https://<SUBDOMAIN-PULL_REQUEST_ID>.<AZURE_REGION>.azurestaticapps.net`. For a given pull request, the URL remains the same, even if you push new updates. The same pre-production environment also gets reused for the life of the pull request.

To automate the review process with end-to-end testing, the [GitHub Action for deploying Azure Static Web Apps](https://github.com/Azure/static-web-apps-deploy) has the `static_web_app_url` output variable.

You can reference this URL in the rest of your workflow to run your tests against the pre-production environment.

## Publish changes

Merge the pull request to publish to production.

1. Select **Merge pull request**.

Your changes get copied to the tracked branch (the "production" branch). Then, the deployment workflow starts on the tracked branch and the changes go live after    your application rebuilds.

1. Open your production URL to load the live version of the website and verify.

## Limitations

- Anyone can access the staged versions of your application via their URL, even if your GitHub repo is private.

> [!WARNING]

> Be careful with sensitive content, since anyone can access pre-production environments.

- The number of pre-production environments available for each app deployed with Static Web Apps depends your [hosting plan](plans.md). For example, with the [Free tier](https://azure.microsoft.com/pricing/details/devops/azure-devops-services/) you can have three pre-production environments along with the production environment.

- Pre-production environments aren't geo-distributed.

- Only GitHub Actions deployments support pre-production environments.

## Next steps

> [!div class="nextstepaction"]

> [Create branch preview environments](branch-environments.md)


# Build Configuration

# Build configuration for Azure Static Web Apps

The Azure Static Web Apps build configuration either uses GitHub Actions or Azure Pipelines. Each site has a YAML configuration file that controls how a site is built and deployed. This article explains the file's structure and options.

The following table lists the available configuration settings.

| Property | Description | Required |

|---|---|---|

| `app_location` | This folder contains the source code for your front-end application. The value is relative to the repository root in GitHub and the current working folder in Azure DevOps. When used with `skip_app_build: true`, this value is the app's build output location. | Yes |

| `api_location` | This folder that contains the source code for your API application. The value is relative to the repository root in GitHub and the current working folder in Azure DevOps. When used with `skip_api_build: true`, this value is the API's build output location. | No |

| `output_location` | If your web app runs a build step, the output location is the folder where the public files are generated. For most projects, the `output_location` is relative to the `app_location`. However, for .NET projects, the location is relative to the output folder. | No |

| `app_build_command` | For Node.js applications, you can define a custom command to build the static content application.<br><br>For example, to configure a production build for an Angular application create an npm script named `build-prod` to run `ng build --prod` and enter `npm run build-prod` as the custom command. If left blank, the workflow tries to run the `npm run build` or `npm run build:azure` commands. | No |

| `api_build_command` | For Node.js applications, you can define a custom command to build the Azure Functions API application. | No |

| `skip_app_build` | Set the value to `true` to skip building the front-end app. | No |

| `skip_api_build` | Set the value to `true` to skip building the API functions. | No |

| `cwd`<br />(Azure Pipelines only) | Absolute path to the working folder. Defaults to `$(System.DefaultWorkingDirectory)`. | No |

| `build_timeout_in_minutes` | Set this value to customize the build timeout. Defaults to `15`. | No |

With these settings, you can set up GitHub Actions or [Azure Pipelines](get-started-portal.md?pivots=azure-devops) to run continuous integration/continuous delivery (CI/CD) for your static web app.

## File name and location

The GitHub action generates the configuration file and is stored in the *.github/workflows* folder, named using the following format: `azure-static-web-apps-<RANDOM_NAME>.yml`.

By default, the configuration file is stored at the root of your repository with the name `azure-pipelines.yml`.

## Security

You can choose between two different deployment authorization policies to secure your build configuration. Static Web Apps supports either using an Azure deployment token (recommended), or a GitHub access token.

Use the following steps to set the deployment authorization policy in your app:

- **New apps**: When you create your static web app, on the *Deployment configuration* tab, make a selection for the *Deployment authorization policy*.

- **Existing apps**: To update an existing app, go to *Settings* > *Configuration* > *Deployment configuration*, and make a selection for the *Deployment authorization policy*.

## Build configuration

The following sample configuration monitors the repository for changes. As commits are pushed to the `main` branch, the application is built from the `app_location` folder and files in the `output_location` are served to the public web. Additionally, the application in the *api* folder is available under the site's `api` path.

```yaml

trigger:

- main

pool:

vmImage: ubuntu-latest

steps:

- checkout: self

submodules: true

- task: AzureStaticWebApp@0

inputs:

app_location: 'src' # App source code path relative to cwd

api_location: 'api' # Api source code path relative to cwd

output_location: 'public' # Built app content directory relative to app_location - optional

cwd: '$(System.DefaultWorkingDirectory)/myapp' # Working directory - optional

azure_static_web_apps_api_token: $(deployment_token)

```

In this configuration:

- The `main` branch is monitored for commits.

- The `app_location` points to the `src` folder that contains the source files for the web app. This value is relative to the working directory (`cwd`). To set it to the working directory, use `/`.

- The `api_location` points to the `api` folder that contains the Azure Functions application for the site's API endpoints. This value is relative to the working directory (`cwd`). To set it to the working directory, use `/`.

- The `output_location` points to the `public` folder that contains the final version of the app's source files. This value is relative to `app_location`. For .NET projects, the location is relative to the output folder.

- The `cwd` is an absolute path pointing to the working directory. It defaults to `$(System.DefaultWorkingDirectory)`.

- The `$(deployment_token)` variable points to the [generated Azure DevOps deployment token](./deployment-token-management.md).

> [!NOTE]

> `app_location` and `api_location` must be relative to the working directory (`cwd`) and they must be subdirectories under `cwd`.

# [Identity token](#tab/identity)

```yml

name: Azure Static Web Apps CI/CD

on:

push:

branches:

- main

- dev

pull_request:

types: [opened, synchronize, reopened, closed]

branches:

- main

jobs:

build_and_deploy_job:

if: github.event_name == 'push' || (github.event_name == 'pull_request' && github.event.action != 'closed')

runs-on: ubuntu-latest

name: Build and Deploy Job

permissions:

id-token: write

contents: read

steps:

- uses: actions/checkout@v3

with:

submodules: true

lfs: false

- name: Install OIDC Client from Core Package

run: npm install @actions/core@1.6.0 @actions/http-client

- name: Get Id Token

uses: actions/github-script@v6

id: idtoken

with:

script: |

const coredemo = require('@actions/core')

return await coredemo.getIDToken()

result-encoding: string

- name: Build And Deploy

id: builddeploy

uses: Azure/static-web-apps-deploy@v1

with:

azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN_GENTLE_WATER }}

action: "upload"

###### Repository/Build Configurations - These values can be configured to match your app requirements. ######

# For more information regarding Static Web App workflow configurations, please visit: https://aka.ms/swaworkflowconfig

app_location: "/" # App source code path

api_location: "" # Api source code path - optional

output_location: "dist/angular-basic" # Built app content directory - optional

production_branch: "dev"

github_id_token: ${{ steps.idtoken.outputs.result }}

###### End of Repository/Build Configurations ######

close_pull_request_job:

if: github.event_name == 'pull_request' && github.event.action == 'closed'

runs-on: ubuntu-latest

name: Close Pull Request Job

steps:

- name: Close Pull Request

id: closepullrequest

uses: Azure/static-web-apps-deploy@v1

with:

azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN_GENTLE_WATER_030D91C1E }}

action: "close"

```

# [Azure access token](#tab/aat)

```yml

name: Azure Static Web Apps CI/CD

on:

push:

branches:

- main

pull_request:

types: [opened, synchronize, reopened, closed]

branches:

- main

jobs:

build_and_deploy_job:

if: github.event_name == 'push' || (github.event_name == 'pull_request' && github.event.action != 'closed')

runs-on: ubuntu-latest

name: Build and Deploy Job

steps:

- uses: actions/checkout@v2

with:

submodules: true

- name: Build And Deploy

id: builddeploy

uses: Azure/static-web-apps-deploy@v1

with:

azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN }}

repo_token: ${{ secrets.GITHUB_TOKEN }} # Used for GitHub integrations (i.e. PR comments)

action: "upload"

###### Repository/Build Configurations ######

app_location: "src" # App source code path relative to repository root

api_location: "api" # Api source code path relative to repository root - optional

output_location: "public" # Built app content directory, relative to app_location - optional

###### End of Repository/Build Configurations ######

close_pull_request_job:

if: github.event_name == 'pull_request' && github.event.action == 'closed'

runs-on: ubuntu-latest

name: Close Pull Request Job

steps:

- name: Close Pull Request

id: closepullrequest

uses: Azure/static-web-apps-deploy@v1

with:

azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN }}

action: "close"

```

---

In this configuration:

- The `main` branch is monitored for commits.

- A GitHub Actions workflow is [triggered](https://help.github.com/actions/reference/events-that-trigger-workflows) when a pull request on the `main` branch is: opened, synchronized, reopened, or closed.

- The `build_and_deploy_job` executes when you push commits or open a pull request against the branch listed in the `on` property.

- The `app_location` points to the `src` folder that contains the source files for the web app. To set this value to the repository root, use `/`.

- The `api_location` points to the `api` folder that contains the Azure Functions application for the site's API endpoints. To set this value to the repository root, use `/`.

- The `output_location` points to the `public` folder that contains the final version of the app's source files. It's relative to `app_location`. For .NET projects, the location is relative to the publish output folder.

Don't change the values for `repo_token`, `action`, and `azure_static_web_apps_api_token` as they're set for you by Azure Static Web Apps.

The *Close Pull Request* job automatically closes the pull request that triggered the build and deployment. This optional job isn't required for the process to work.

When a pull request is opened, the Azure Static Web Apps GitHub Action builds and deploys the app to a staging environment. Afterward, the *Close Pull Request* job checks if the pull request is still open and closes it with a completion message.

This job helps keep your pull request workflow organized and prevents stale pull requests. By the runtime automatically closing the pull request, your repository stays up-to-date and your team is notified of the status.

The *Close Pull Request* job is part of the Azure Static Web Apps GitHub Actions workflow, closing the pull request after it's merged. The `Azure/static-web-apps-deploy` action deploys the app to Azure Static Web Apps, requiring the `azure_static_web_apps_api_token` for authentication.

## Custom build commands

For Node.js applications, you can take fine-grained control over what commands run during the app or API build process. The following example shows how to define build with values for `app_build_command` and `api_build_command`.

> [!NOTE]

> Currently, you can only define `app_build_command` and `api_build_command` for Node.js builds.

> To specify the Node.js version, use the [`engines`](https://docs.npmjs.com/cli/v8/configuring-npm/package-json#engines) field in the `package.json` file.

```yml

...

with:

azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN }}

repo_token: ${{ secrets.GITHUB_TOKEN }}

action: 'upload'

app_location: '/'

api_location: 'api'

output_location: 'dist'

app_build_command: 'npm run build-ui-prod'

api_build_command: 'npm run build-api-prod'

```

```yaml

...

inputs:

app_location: 'src'

api_location: 'api'

app_build_command: 'npm run build-ui-prod'

api_build_command: 'npm run build-api-prod'

output_location: 'public'

azure_static_web_apps_api_token: $(deployment_token)

```

## Skip building front-end app

If you need full control of the build for your front-end app, you can bypass the automatic build and deploy the app built in a previous step.

To skip building the front-end app:

- Set `app_location` to the location the files you want to deploy.

- Set `skip_app_build` to `true`.

- Set `output_location` to an empty string (`''`).

> [!NOTE]

> Make sure you have your `staticwebapp.config.json` file copied as well into the *output* directory.

```yml

...

with:

azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN }}

repo_token: ${{ secrets.GITHUB_TOKEN }}

action: 'upload'

app_location: 'src/dist'

api_location: 'api'

output_location: ''

skip_app_build: true

```

```yml

...

inputs:

app_location: 'src/dist'

api_location: 'api'

output_location: '' # Leave this empty

skip_app_build: true

azure_static_web_apps_api_token: $(deployment_token)

```

## Skip building the API

If you want to skip building the API, you can bypass the automatic build and deploy the API built in a previous step.

Steps to skip building the API:

- In the *staticwebapp.config.json* file, set `apiRuntime` to the correct runtime and version. Refer to [Configure Azure Static Web Apps](configuration.md#select-the-api-language-runtime-version) for the list of supported runtimes and versions.

```json

{

"platform": {

"apiRuntime": "node:16"

}

}

```

- Set `skip_api_build` to `true`.

- Set `api_location` to the folder containing the built API app to deploy. This path is relative to the repository root in GitHub Actions and `cwd` in Azure Pipelines.

```yml

...

with:

azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN }}

repo_token: ${{ secrets.GITHUB_TOKEN }}

action: 'upload'

app_location: "src" # App source code path relative to repository root

api_location: "api" # Api source code path relative to repository root - optional

output_location: "public" # Built app content directory, relative to app_location - optional

skip_api_build: true

```

```yml

...

inputs:

app_location: 'src'

api_location: 'api'

output_location: 'public'

skip_api_build: true

azure_static_web_apps_api_token: $(deployment_token)

```

## Extend build timeout

By default, the app and API builds are limited to 15 minutes. You can extend the build timeout by setting the `build_timeout_in_minutes` property.

```yaml

...

with:

azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN }}

repo_token: ${{ secrets.GITHUB_TOKEN }}

action: 'upload'

app_location: 'src'

api_location: 'api'

output_location: 'public'

build_timeout_in_minutes: 30

```

```yml

...

inputs:

app_location: 'src'

api_location: 'api'

output_location: 'public'

build_timeout_in_minutes: 30

azure_static_web_apps_api_token: $(deployment_token)

```

## Run workflow without deployment secrets

Sometimes you need your workflow to continue to process even when some secrets are missing. To configure your workflow to proceed without defined secrets, set the `SKIP_DEPLOY_ON_MISSING_SECRETS` environment variable to `true`.

When enabled, this feature allows the workflow to continue without deploying the site's content.

```yaml

...

with:

azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN }}

repo_token: ${{ secrets.GITHUB_TOKEN }}

action: 'upload'

app_location: 'src'

api_location: 'api'

output_location: 'public'

env:

SKIP_DEPLOY_ON_MISSING_SECRETS: true

```

```yaml

...

inputs:

app_location: 'src'

api_location: 'api'

output_location: 'public'

azure_static_web_apps_api_token: $(deployment_token)

env:

SKIP_DEPLOY_ON_MISSING_SECRETS: true

```

## Environment variables

You can set environment variables for your build via the `env` section of a job's configuration.

For more information about the environment variables used by Oryx, see [Oryx configuration](https://github.com/microsoft/Oryx/blob/main/doc/configuration.md).

```yaml

...

with:

azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN }}

repo_token: ${{ secrets.GITHUB_TOKEN }}

action: 'upload'

app_location: 'src'

api_location: 'api'

output_location: 'public'

env: # Add environment variables here

HUGO_VERSION: 0.58.0

```

```yml

...

inputs:

app_location: 'src'

api_location: 'api'

output_location: 'public'

azure_static_web_apps_api_token: $(deployment_token)

env: # Add environment variables here

HUGO_VERSION: 0.58.0

```

## Monorepo support

A monorepo is a repository that contains code for more than one application. By default, the workflow tracks all files in a repository, but you can adjust the configuration to target a single app.

To target a workflow file to a single app, you specify paths in the `push` and `pull_request` sections.

When you set up a monorepo, each static app configuration is scoped to only files for a single app. The different workflow files live side by side in the repository's _.github/workflows_ folder.

```files

├── .github

│   └── workflows

│       ├── azure-static-web-apps-purple-pond.yml

│       └── azure-static-web-apps-yellow-shoe.yml

│

├── app1  👉 controlled by: azure-static-web-apps-purple-pond.yml

├── app2  👉 controlled by: azure-static-web-apps-yellow-shoe.yml

│

├── api1  👉 controlled by: azure-static-web-apps-purple-pond.yml

├── api2  👉 controlled by: azure-static-web-apps-yellow-shoe.yml

│

└── README.md

```

The following example demonstrates how to add a `paths` node to the `push` and `pull_request` sections of a file named _azure-static-web-apps-purple-pond.yml_.

```yml

on:

push:

branches:

- main

paths:

- app1/**

- api1/**

- .github/workflows/azure-static-web-apps-purple-pond.yml

pull_request:

types: [opened, synchronize, reopened, closed]

branches:

- main

paths:

- app1/**

- api1/**

- .github/workflows/azure-static-web-apps-purple-pond.yml

```

In this example, only changes made to following files trigger a new build:

- Any files inside the _app1_ folder

- Any files inside the _api1_ folder

- Changes to the app's _azure-static-web-apps-purple-pond.yml_ workflow file

To support more than one application in a single repository, create a separate workflow file and associate it with different Azure Pipelines.

## Next steps

> [!div class="nextstepaction"]

> [Review pull requests in pre-production environments](review-publish-pull-requests.md)


# Publish Azure Resource Manager

# Tutorial: Publish Azure Static Web Apps using an ARM Template

This article demonstrates how to deploy [Azure Static Web Apps](./overview.md) using an [Azure Resource Manager template](../azure-resource-manager/templates/overview.md) (ARM template).

In this tutorial, you learn to:

> [!div class="checklist"]

> - Create an ARM Template for Azure Static Web Apps

> - Deploy the ARM Template to create an Azure Static Web App instance

## Prerequisites

- **Active Azure account:** If you don't have one, you can [create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- **GitHub Account:** If you don't have one, you can [create a GitHub Account for free](https://github.com)

- **Editor for ARM Templates:** Reviewing and editing templates requires a JSON editor. Visual Studio Code with the [Azure Resource Manager Tools extension](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) is well suited for editing ARM Templates. For instructions on how to install and configure Visual Studio Code, see [Quickstart: Create ARM templates with Visual Studio Code](../azure-resource-manager/templates/quickstart-create-templates-use-visual-studio-code.md).

- **Azure CLI or Azure PowerShell**: Deploying ARM templates requires a command line tool. For the installation instructions, see:

- [Install Azure CLI on Windows OS](/cli/azure/install-azure-cli-windows)

- [Install Azure CLI on Linux OS](/cli/azure/install-azure-cli-linux)

- [Install Azure CLI on macOS](/cli/azure/install-azure-cli-macos)

- [Install Azure PowerShell](/powershell/azure/install-azure-powershell)

## Create a GitHub personal access token

One of the parameters in the ARM template is `repositoryToken`, which allows the ARM deployment process to interact with the GitHub repo holding the static site source code.

1. From your GitHub Account Profile (in the upper right corner), select **Settings**.

1. Select **Developer Settings**.

1. Select **Personal Access Tokens**.

1. Select **Generate New Token**.

1. Provide a name for this token in the _Name_ field, for example *myfirstswadeployment*.

1. Select an _Expiration_ for the token, the default is 30 days.

1. Specify the following *scopes*: **repo, workflow, write:packages**

1. Select **Generate token**.

1. Copy the token value and paste it into a text editor for later use.

> [!IMPORTANT]

> Make sure you copy this token and store it somewhere safe. Consider storing this token in [Azure Key Vault](../azure-resource-manager/templates/template-tutorial-use-key-vault.md) and access it in your ARM Template.

## Create a GitHub repo

This article uses a GitHub template repository to make it easy for you to get started. The template features a starter app used to deploy using Azure Static Web Apps.

1. Go to the following location to create a new repository:

1. [https://github.com/staticwebdev/vanilla-basic/generate](https://github.com/login?return_to=/staticwebdev/vanilla-basic/generate)

1. Name your repository **myfirstswadeployment**

> [!NOTE]

> Azure Static Web Apps requires at least one HTML file to create a web app. The repository you create in this step includes a single _index.html_ file.

1. Select **Create repository**.

## Create the ARM Template

With the prerequisites in place, the next step is to define the ARM deployment template file.

1. Create a new folder to hold the ARM Templates.

1. Create a new file and name it **azuredeploy.json**.

1. Paste the following ARM template snippet into _azuredeploy.json_.

```json

{

"$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",

"contentVersion": "1.0.0.0",

"parameters": {

"name": {

"type": "string"

},

"location": {

"type": "string"

},

"sku": {

"type": "string"

},

"skucode": {

"type": "string"

},

"repositoryUrl": {

"type": "string"

},

"branch": {

"type": "string"

},

"repositoryToken": {

"type": "securestring"

},

"appLocation": {

"type": "string"

},

"apiLocation": {

"type": "string"

},

"appArtifactLocation": {

"type": "string"

},

"resourceTags": {

"type": "object"

},

"appSettings": {

"type": "object"

}

},

"resources": [

{

"apiVersion": "2021-01-15",

"name": "[parameters('name')]",

"type": "Microsoft.Web/staticSites",

"location": "[parameters('location')]",

"tags": "[parameters('resourceTags')]",

"properties": {

"repositoryUrl": "[parameters('repositoryUrl')]",

"branch": "[parameters('branch')]",

"repositoryToken": "[parameters('repositoryToken')]",

"buildProperties": {

"appLocation": "[parameters('appLocation')]",

"apiLocation": "[parameters('apiLocation')]",

"appArtifactLocation": "[parameters('appArtifactLocation')]"

}

},

"sku": {

"Tier": "[parameters('sku')]",

"Name": "[parameters('skuCode')]"

},

"resources":[

{

"apiVersion": "2021-01-15",

"name": "appsettings",

"type": "config",

"location": "[parameters('location')]",

"properties": "[parameters('appSettings')]",

"dependsOn": [

"[resourceId('Microsoft.Web/staticSites', parameters('name'))]"

]

}

]

}

]

}

```

1. Create a new file and name it **azuredeploy.parameters.json**.

1. Paste the following ARM template snippet into _azuredeploy.parameters.json_.

```json

{

"$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentParameters.json#",

"contentVersion": "1.0.0.0",

"parameters": {

"name": {

"value": "myfirstswadeployment"

},

"location": {

"value": "Central US"

},

"sku": {

"value": "Free"

},

"skucode": {

"value": "Free"

},

"repositoryUrl": {

"value": "https://github.com/<YOUR-GITHUB-USER-NAME>/<YOUR-GITHUB-REPOSITORY-NAME>"

},

"branch": {

"value": "main"

},

"repositoryToken": {

"value": "<YOUR-GITHUB-PAT>"

},

"appLocation": {

"value": "/"

},

"apiLocation": {

"value": ""

},

"appArtifactLocation": {

"value": "src"

},

"resourceTags": {

"value": {

"Environment": "Development",

"Project": "Testing SWA with ARM",

"ApplicationName": "myfirstswadeployment"

}

},

"appSettings": {

"value": {

"MY_APP_SETTING1": "value 1",

"MY_APP_SETTING2": "value 2"

}

}

}

}

```

1. Update the following parameters.

| Parameter | Expected value |

| --- | --- |

| `repositoryUrl` | Provide the URL to your Static Web Apps GitHub repository. |

| `repositoryToken` | Provide the GitHub PAT token. |

1. Save the updates before running the deployment in the next step.

## Running the deployment

You need either Azure CLI or Azure PowerShell to deploy the template.

### Sign in to Azure

To deploy a template, sign in to either the Azure CLI or Azure PowerShell.

# [Azure CLI](#tab/azure-cli)

```azurecli

az login

```

# [PowerShell](#tab/azure-powershell)

```azurepowershell

Connect-AzAccount

```

---

If you have multiple Azure subscriptions, select the subscription you want to use. Replace `<SUBSCRIPTION-ID>` with your subscription information:

# [Azure CLI](#tab/azure-cli)

```azurecli

az account set --subscription <SUBSCRIPTION-ID>

```

# [PowerShell](#tab/azure-powershell)

```azurepowershell

Set-AzContext <SUBSCRIPTION-ID>

```

---

## Create a resource group

When you deploy a template, you specify a resource group that contains related resources. Before running the deployment command, create the resource group with either Azure CLI or Azure PowerShell.

> [!NOTE]

> The CLI examples in this article are written for the Bash shell.

# [Azure CLI](#tab/azure-cli)

```azurecli

resourceGroupName="myfirstswadeployRG"

az group create \

--name $resourceGroupName \

--location "Central US"

```

# [PowerShell](#tab/azure-powershell)

```azurepowershell

$resourceGroupName = "myfirstswadeployRG"

New-AzResourceGroup `

-Name $resourceGroupName `

-Location "Central US"

```

---

## Deploy template

Use one of these deployment options to deploy the template.

# [Azure CLI](#tab/azure-cli)

```azurecli

az deployment group create \

--name DeployLocalTemplate \

--resource-group $resourceGroupName \

--template-file <PATH-TO-AZUREDEPLOY.JSON> \

--parameters <PATH-TO-AZUREDEPLOY.PARAMETERS.JSON> \

--verbose

```

To learn more about deploying templates using the Azure CLI, see [Deploy resources with ARM templates and Azure CLI](../azure-resource-manager/templates/deploy-cli.md).

# [PowerShell](#tab/azure-powershell)

```azurepowershell

$templateFile = Read-Host -Prompt "Enter the template file path and file name"

$templateparameterFile = Read-Host -Prompt "Enter the template parameter file path and file name"

New-AzResourceGroupDeployment `

-Name DeployLocalTemplate `

-ResourceGroupName $resourceGroupName `

-TemplateFile $templateFile `

-TemplateParameterFile $templateparameterfile `

-verbose

```

To learn more about deploying templates using Azure PowerShell, see [Deploy resources with ARM templates and Azure PowerShell](../azure-resource-manager/templates/deploy-powershell.md).

---

[!INCLUDE [view website](../../includes/static-web-apps-get-started-view-website.md)]

## Clean up resources

Clean up the resources you deployed by deleting the resource group.

1. From the Azure portal, select **Resource group** from the left menu.

2. Enter the resource group name in the **Filter by name** field.

3. Select the resource group name.

4. Select **Delete resource group** from the top menu.

## Next steps

> [!div class="nextstepaction"]

> [Configure your static web app](./configuration.md)


# Plans

# Azure Static Web Apps hosting plans

Azure Static Web Apps is available through two different plans, Free and Standard. See the [pricing page for Standard plan costs](https://azure.microsoft.com/pricing/details/app-service/static/). For information service level agreement details, see [Service Level Agreements (SLA) for Online Services](https://www.microsoft.com/licensing/docs/view/Service-Level-Agreements-SLA-for-Online-Services).

## Features

| Feature | Free plan <br> (For personal projects) | Standard plan <br> (For production apps) | Dedicated plan (Retired effective October 31st, 2025) |

| --- | --- | --- |---|

| Web hosting | ✔ | ✔ | ✔ |

| GitHub integration | ✔ | ✔ | ✔ |

| Azure DevOps integration | ✔ | ✔ | ✔ |

| Globally distributed static content | ✔ | ✔ | ✗ |

| Free, automatically renewing SSL certificates | ✔ | ✔ | ✔ |

| Staging environments | 3 per app | 10 per app | 20 per app |

| Max app size | 250 MB per app | 500 MB per app | 2 GB |

| Custom domains | 2 per app | 5 per app | 10 per app |

| APIs via Azure Functions | Managed | Managed or<br>[Bring your own Functions app](functions-bring-your-own.md) | Managed or<br>[Bring your own Functions app](functions-bring-your-own.md) |

| Authentication provider integration | [Preconfigured](authentication-authorization.yml)<br>(Service defined) | [Custom registrations](authentication-custom.md) | [Custom registrations](authentication-custom.md) |

| [Assign custom roles with a function](authentication-custom.md#manage-roles) | ✗ | ✔ | ✔ |

| Private endpoints | ✗ | ✔ | ✔ |

| [Service Level Agreement (SLA)](https://azure.microsoft.com/support/legal/sla/app-service-static/v1_0/) | None  | ✔ | ✔ |

## Selecting a plan

The following scenarios can help you decide if the Standard or Dedicated plan best fits your needs.

Select Standard when:

- Expected traffic volumes exceed bandwidth maximums.

- The existing Azure Functions app you want to use either has triggers and bindings beyond HTTP endpoints, or can't be converted to a managed Functions app.

- Security requirements that require a [custom provider registration](authentication-custom.md).

- The site's web assets total file size exceed the storage maximums.

- You require formal customer support.

- You require more than three [staging environments](review-publish-pull-requests.md).

See the [quotas guide](quotas.md) for limitation details.

## Changing plans

You can move between Free or Standard plans via the Azure portal.

1. Go to your Static Web Apps resource in the Azure portal.

1. Under the _Settings_ menu, select **Hosting plan**.

1. Select the hosting plan you want for your static web app.

1. Select **Save**.

**For Dedicated Plan deployments, follow the [Deploy your web app to Azure Static Web Apps](deploy-web-framework.md) guide to redeploy to a new Static Web App.**


# Deploy Web Framework

# Deploy your web app to Azure Static Web Apps

In this article, you create a new web app with the framework of your choice, run it locally, then deploy to Azure Static Web Apps.

## Prerequisites

To complete this tutorial, you need:

| Resource | Description |

|---|---|

| [Azure subscription][1] | If you don't have one, you can [create an account for free][1]. |

| [Node.js][2] | Install version 20.0 or later. |

| [Azure CLI][3] | Install version 2.6x or later. |

You also need a text editor. For work with Azure, [Visual Studio Code][4] is recommended.

You can run the app you create in this article on the platform of your choice including: Linux, macOS, Windows, or Windows Subsystem for Linux.

## Create your web app

1. Open a terminal window.

2. Select an appropriate directory for your code, then run the following commands.

```bash

npm create vite@latest swa-vanilla-demo -- --template=vanilla

cd swa-vanilla-demo

npm install

npm run dev

```

As you run these commands, the development server prints the URL of your website. Select the link to open it in your default browser.

![Screen shot of the generated vanilla web application.][img-vanilla-js]

2. Select an appropriate directory for your code, then run the following commands.

```bash

npx --package @angular/cli@latest ng new swa-angular-demo --ssr=false --defaults

cd swa-angular-demo

npm start

```

As you run these commands, the development server prints the URL of your website. Select the link to open it in your default browser.

![Screen shot of the generated angular web application.][img-angular]

2. Select an appropriate directory for your code, then run the following commands.

```bash

npm create vite@latest swa-react-demo -- --template react

cd swa-react-demo

npm install

npm run dev

```

As you run these commands, the development server prints the URL of your website. Select the link to open it in your default browser.

![Screen shot of the generated react web application.][img-react]

2. Select an appropriate directory for your code, then run the following commands.

```bash

npm create vite@latest swa-vue-demo -- --template vue

cd swa-vue-demo

npm install

npm run dev

```

As you run these commands, the development server prints the URL of your website. Select the link to open it in your default browser.

![Screen shot of the generated Vue web application.][img-vue]

3. Select <kbd>Cmd/Ctrl</kbd>+<kbd>C</kbd> to stop the development server.

[!INCLUDE [Create an Azure Static Web App](../../includes/static-web-apps/quickstart-direct-deploy-create.md)]

[!INCLUDE [Build your site for deployment](../../includes/static-web-apps/quickstart-direct-deploy-build.md)]

> [!WARNING]

> Angular v17 and later place the distributable files in a subdirectory of the output path that you can choose. The SWA CLI doesn't know the specific location of the directory. The following steps show you how to set this path correctly.

Locate the generated *index.html* file in your project in the *dist/swa-angular-demo/browser* folder.

1. Set the `SWA_CLI_OUTPUT_LOCATION` environment variable to the directory containing the *index.html* file:

# [bash](#tab/bash)

```bash

export SWA_CLI_OUTPUT_LOCATION="dist/swa-angular-demo/browser"

```

# [csh](#tab/csh)

```bash

setenv SWA_CLI_OUTPUT_LOCATION "dist/swa-angular-demo/browser"

```

# [PowerShell](#tab/pwsh)

```powershell

$env:SWA_CLI_OUTPUT_LOCATION="dist/swa-angular-demo/browser"

```

# [CMD](#tab/cmd)

```bash

set SWA_CLI_OUTPUT_LOCATION="dist/swa-angular-demo/browser"

```

---

## Deploy your site to Azure

Deploy your code to your static web app:

```bash

npx swa deploy --env production

```

It might take a few minutes to deploy the application. Once complete, the URL of your site is displayed.

![Screen shot of the deploy command.][img-deploy]

On most systems, you can select the URL of the site to open it in your default browser.

[!INCLUDE [Clean up resources](../../includes/static-web-apps/quickstart-direct-deploy-clean-up-resources.md)]

## Next steps

> [!div class="nextstepaction"]

> [Add authentication](./add-authentication.md)

## Related content

* [Authentication and authorization](./authentication-authorization.yml)

* [Database connections](./database-overview.md)

* [Custom Domains](./custom-domain.md)

* [Video series: Deploy websites to the cloud with Azure Static Web Apps](https://aka.ms/azure/beginnervideos/learn/swa)

[1]: https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn

[2]: https://nodejs.org/

[3]: /cli/azure/install-azure-cli

[4]: https://code.visualstudio.com

[img-deploy]: media/deploy-screenshot.png

[img-vanilla-js]: media/deploy-web-framework/vanilla-js-screenshot.png

[img-angular]: media/deploy-web-framework/angular-screenshot.png

[img-react]: media/deploy-web-framework/react-screenshot.png

[img-vue]: media/deploy-web-framework/vue-screenshot.png


# Get Started Portal

# Quickstart: Build your first static web app

Azure Static Web Apps publishes a website to a production environment by building apps from an Azure DevOps or GitHub repository. In this quickstart, you deploy a web application to Azure Static Web apps using the Azure portal.

## Prerequisites

- If you don't have an Azure subscription, [create a free trial account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- [GitHub](https://github.com) account

- If you don't have an Azure subscription, [create a free trial account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- [Azure DevOps](https://azure.microsoft.com/services/devops) organization

[!INCLUDE [create repository from template](../../includes/static-web-apps-get-started-create-repo.md)]

## Create a repository

This article uses an Azure DevOps repository to make it easy for you to get started. The repository features a starter app used to deploy using Azure Static Web Apps.

1. Sign in to Azure DevOps.

2. Select **New repository**.

3. In the *Create new project* window, expand **Advanced** menu and make the following selections:

| Setting | Value |

|--|--|

| Project | Enter **my-first-web-static-app**. |

| Visibility | Select **Private**. |

| Version control | Select **Git**.  |

| Work item process | Select the option that best suits your development methods. |

4. Select **Create**.

5. Select the **Repos** menu item.

6. Select the **Files** menu item.

7. Under the *Import repository* card, select **Import**.

8. Copy a repository URL for the framework of your choice, and paste it into the *Clone URL* box.

# [No Framework](#tab/vanilla-javascript)

[https://github.com/staticwebdev/vanilla-basic.git](https://github.com/staticwebdev/vanilla-basic.git)

# [Angular](#tab/angular)

[https://github.com/staticwebdev/angular-basic.git](https://github.com/staticwebdev/angular-basic.git)

# [Blazor](#tab/blazor)

[https://github.com/staticwebdev/blazor-basic.git](https://github.com/staticwebdev/blazor-basic.git)

# [React](#tab/react)

[https://github.com/staticwebdev/react-basic.git](https://github.com/staticwebdev/react-basic.git)

# [Vue](#tab/vue)

[https://github.com/staticwebdev/vue-basic.git](https://github.com/staticwebdev/vue-basic.git)

---

9. Select **Import** and wait for the import process to complete.

## Create a static web app

Now that the repository is created, you can create a static web app from the Azure portal.

1. Go to the [Azure portal](https://portal.azure.com).

1. Select **Create a Resource**.

1. Search for **Static Web Apps**.

1. Select **Static Web Apps**.

1. Select **Create**.

In the _Basics_ section, begin by configuring your new app and linking it to a GitHub repository.

| Setting | Value |

|--|--|

| Subscription | Select your Azure subscription. |

| Resource Group | Select the **Create new** link, and enter **static-web-apps-test** in the textbox. |

| Name | Enter **my-first-static-web-app** in the textbox. |

| Plan type | Select **Free**. |

| Source | Select **GitHub** and sign in to GitHub if necessary. |

If necessary sign in with GitHub, and enter the following repository information.

| Setting | Value |

|--|--|

| Organization | Select your organization. |

| Repository| Select **my-first-web-static-app**. |

| Branch | Select **main**. |

> [!NOTE]

> If you don't see a list of repositories:

>

> - You may need to authorize Azure Static Web Apps in GitHub. Browse to your GitHub profile and go to **Settings > Applications > Authorized OAuth Apps**, select **Azure Static Web Apps**, and then select **Grant**.

>

> - You may need to authorize Azure Static Web Apps in your Azure DevOps organization. You must be an owner of the organization to grant the permissions. Request third-party application access via OAuth. For more information, see [Authorize access to REST APIs with OAuth 2.0](/azure/devops/integrate/get-started/authentication/oauth).

In the _Basics_ section, begin by configuring your new app and linking it to an Azure DevOps repository.

| Setting | Value |

|--|--|

| Subscription | Select your Azure subscription. |

| Resource Group | Select the **Create new** link, and enter **static-web-apps-test** in the textbox. |

| Name | Enter **my-first-static-web-app** in the textbox. |

| Plan type | Select **Free**. |

| Azure Functions and staging details | Select a region closest to you. |

| Source | Select **Azure DevOps**. |

| Organization | Select your organization. |

| Project | Select your project. |

| Repository| Select **my-first-web-static-app**. |

| Branch | Select **main**. |

> [!NOTE]

> Make sure the branch you are using is not protected, and that you have sufficient permissions to issue a `push` command. To verify, browse to your DevOps repository and go to **Repos** -> **Branches** and select **More options**. Next, select your branch, and then **Branch policies** to ensure required policies aren't enabled.

In the _Build Details_ section, add configuration details specific to your preferred front-end framework.

# [No Framework](#tab/vanilla-javascript)

1. From the _Build Presets_ dropdown, select **Custom**.

1. In the _App location_ box, enter **./src**.

1. Leave the _Api location_ box empty.

1. In the _Output location_ box, enter **./src**.

# [Angular](#tab/angular)

1. From the _Build Presets_ dropdown, select **Angular**.

1. Keep the default value in the _App location_ box.

1. Leave the _Api location_ box empty.

1. In the _Output location_ box, enter **dist/angular-basic**.

# [Blazor](#tab/blazor)

1. From _Build Presets_ dropdown, select **Blazor**.

1. Keep the default value of **Client** in the _App location_ box.

1. Leave the _Api location_ box empty.

1. Keep the default value of **wwwroot** in the _Output location_ box.

# [React](#tab/react)

1. From the _Build Presets_ dropdown, select **React**.

1. Keep the default value in the _App location_ box.

1. Leave the _Api location_ box empty.

1. In the _Output location_ box, enter **build**.

# [Vue](#tab/vue)

1. From the _Build Presets_ dropdown, select **Vue.js**.

1. Keep the default value in the _App location_ box.

1. Leave the _Api location_ box empty.

1. Keep the default value in the _App artifact location_ box.

---

Select **Review + create**.

Select **Create**.

> [!NOTE]

> You can edit the [workflow file](build-configuration.md) to change these values after you create the app.

Select **Create**.

Select **Go to resource**.

## View the website

There are two aspects to deploying a static app. The first creates the underlying Azure resources that make up your app. The second is a workflow that builds and publishes your application.

Before you can go to your new static site, the deployment build must first finish running.

The Static Web Apps *Overview* window displays a series of links that help you interact with your web app.

1. Selecting on the banner that says, _Select here to check the status of your GitHub Actions runs_ takes you to the GitHub Actions running against your repository. Once you verify the deployment job is complete, then you can go to your website via the generated URL.

2. Once GitHub Actions workflow is complete, you can select the _URL_ link to open the website in new tab.

Once the  workflow is complete, you can select the _URL_ link to open the website in new tab.

## Clean up resources

If you're not going to continue to use this application, you can delete the Azure Static Web Apps instance through the following steps:

1. Open the [Azure portal](https://portal.azure.com).

1. Search for **my-first-web-static-app** from the top search bar.

1. Select the app name.

1. Select **Delete**.

1. Select **Yes** to confirm the delete action (this action may take a few moments to complete).

## Related content

* [Video series: Deploy websites to the cloud with Azure Static Web Apps](https://aka.ms/azure/beginnervideos/learn/swa)

## Next steps

> [!div class="nextstepaction"]

> [Add an API](add-api.md)


# Get Started Cli

# Quickstart: Building your first static site using the Azure CLI

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://go.microsoft.com/fwlink/?linkid=2286315)

Azure Static Web Apps publishes websites to production by building apps from a code repository.

In this quickstart, you deploy a web application to Azure Static Web apps using the Azure CLI.

## Prerequisites

- [GitHub](https://github.com) account.

- [Azure](https://portal.azure.com) account.

- If you don't have an Azure subscription, you can [create a free trial account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- [Azure CLI](/cli/azure/install-azure-cli) installed (version 2.29.0 or higher).

- [A Git setup](https://www.git-scm.com/downloads).

## Define environment variables

The first step in this quickstart is to define environment variables.

```bash

export RANDOM_ID="$(openssl rand -hex 3)"

export MY_RESOURCE_GROUP_NAME="myStaticWebAppResourceGroup$RANDOM_ID"

export REGION=EastUS2

export MY_STATIC_WEB_APP_NAME="myStaticWebApp$RANDOM_ID"

```

## Create a repository (optional)

(Optional) This article uses a GitHub template repository as another way to make it easy for you to get started. The template features a starter app to deploy to Azure Static Web Apps.

1. Navigate to the following location to create a new repository: https://github.com/staticwebdev/vanilla-basic/generate.

2. Name your repository `my-first-static-web-app`.

> [!NOTE]

> Azure Static Web Apps requires at least one HTML file to create a web app. The repository you create in this step includes a single `index.html` file.

3. Select **Create repository**.

## Deploy a Static Web App

Deploy the app as a static web app from the Azure CLI.

1. Create a resource group.

```bash

az group create \

--name $MY_RESOURCE_GROUP_NAME \

--location $REGION

```

Results:

```json

{

"id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/my-swa-group",

"location": "eastus2",

"managedBy": null,

"name": "my-swa-group",

"properties": {

"provisioningState": "Succeeded"

},

"tags": null,

"type": "Microsoft.Resources/resourceGroups"

}

```

2. Deploy a new static web app from your repository.

```bash

az staticwebapp create \

--name $MY_STATIC_WEB_APP_NAME \

--resource-group $MY_RESOURCE_GROUP_NAME \

--location $REGION

```

There are two aspects to deploying a static app. The first operation creates the underlying Azure resources that make up your app. The second is a workflow that builds and publishes your application.

Before you can go to your new static site, the deployment build must first finish running.

3. Return to your console window and run the following command to list the website's URL.

```bash

export MY_STATIC_WEB_APP_URL=$(az staticwebapp show --name  $MY_STATIC_WEB_APP_NAME --resource-group $MY_RESOURCE_GROUP_NAME --query "defaultHostname" -o tsv)

```

```bash

runtime="1 minute";

endtime=$(date -ud "$runtime" +%s);

while [[ $(date -u +%s) -le $endtime ]]; do

if curl -I -s $MY_STATIC_WEB_APP_URL > /dev/null ; then

curl -L -s $MY_STATIC_WEB_APP_URL 2> /dev/null | head -n 9

break

else

sleep 10

fi;

done

```

Results:

```HTML

<!DOCTYPE html>

<html lang=en>

<head>

<meta charset=utf-8 />

<meta name=viewport content="width=device-width, initial-scale=1.0" />

<meta http-equiv=X-UA-Compatible content="IE=edge" />

<title>Azure Static Web Apps - Welcome</title>

<link rel="shortcut icon" href=https://appservice.azureedge.net/images/static-apps/v3/favicon.svg type=image/x-icon />

<link rel=stylesheet href=https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap.min.css crossorigin=anonymous />

```

```bash

echo "You can now visit your web server at https://$MY_STATIC_WEB_APP_URL"

```

## Use a GitHub template

You've successfully deployed a static web app to Azure Static Web Apps using the Azure CLI. Now that you have a basic understanding of how to deploy a static web app, you can explore more advanced features and functionality of Azure Static Web Apps.

In case you want to use the GitHub template repository, follow these steps:

Go to https://github.com/login/device and enter the code you get from GitHub to activate and retrieve your GitHub personal access token.

1. Go to https://github.com/login/device.

2. Enter the user code as displayed your console's message.

3. Select `Continue`.

4. Select `Authorize AzureAppServiceCLI`.

### View the Website via Git

1. As you get the repository URL while running the script, copy the repository URL and paste it into your browser.

2. Select the `Actions` tab.

At this point, Azure is creating the resources to support your static web app. Wait until the icon next to the running workflow turns into a check mark with green background. This operation might take a few minutes to execute.

3. Once the success icon appears, the workflow is complete and you can return back to your console window.

4. Run the following command to query for your website's URL.

```bash

az staticwebapp show \

--name $MY_STATIC_WEB_APP_NAME \

--query "defaultHostname"

```

5. Copy the URL into your browser to go to your website.

## Clean up resources (optional)

If you're not going to continue to use this application, delete the resource group and the static web app using the [az group delete](/cli/azure/group#az-group-delete) command.

## Related content

* [Video series: Deploy websites to the cloud with Azure Static Web Apps](https://aka.ms/azure/beginnervideos/learn/swa)

## Next steps

> [!div class="nextstepaction"]

> [Add an API](add-api.md)


# Add Authentication

# Add authentication to your static site in Azure Static Web Apps

This article is part two in a series that show you how to deploy your first site to Azure Static Web Apps. Previously, you created and deployed a static site with the [web framework](./deploy-web-framework.md) of your choice.

In this article, you add authentication to your site and run the site locally before deploying to the cloud.

## Prerequisites

This tutorial continues from the previous tutorial, and has the same [prerequisites](deploy-web-framework.md#prerequisites).

## Authentication and authorization

Azure Static Web Apps makes it easy to use common authentication providers like Microsoft Entra and Google without writing security-related code.

> [!NOTE]

> You can optionally [register a custom provider and assign custom roles](./authentication-custom.md) for more fine-grained control when using backend APIs.

In this article, you configure your site to use Microsoft Entra ID for authentication.

## Add authentication

In the last article, you created a `staticwebapp.config.json` file. This file [controls many features](./configuration.md) for Azure Static Web Apps, including authentication.

1. Update the `staticwebapp.config.json` to match the following configuration.

```json

{

"navigationFallback": {

"rewrite": "/index.html"

},

"routes": [

{

"route": "/*",

"allowedRoles": [ "authenticated" ]

}

],

"responseOverrides": {

"401": {

"statusCode": 302,

"redirect": "/.auth/login/aad"

}

}

}

```

The `routes` section allows you to restrict access to named roles. There are two predefined roles: `authenticated` and `anonymous`. If the connected user doesn't have an allowed role, the server returns a "401 Unauthorized" response.

The values in the `responseOverrides` section configure your site so that instead of an unauthenticated user seeing a server error, their browser is redirected to the sign-in page instead.

1. Run the site locally.

To launch the site locally, run the [Static Web Apps CLI](https://azure.github.io/static-web-apps-cli) `start` command.

```bash

npx swa start

```

This command starts the Azure Static Web Apps emulator on `http://localhost:4280`.

This URL is shown in your terminal window after the service starts up.

1. Select the URL to go to the site.

Once you open the site in your browser, the local authentication sign in page is displayed.

![A screen shot of the local authentication sign in page.](./media/add-authentication/local-auth-page.png)

The local authentication sign in page provides an emulation of the real authentication experience without the need for external services. You can create a user ID and select which roles you'd like to apply to the user from this screen.

1. Enter a username, then select **Login**.

Once you authenticate, your site is displayed.

## Deploy the site to Azure

Deploy your site in the same way as you did in the last tutorial.

1. Build your site:

```bash

npx swa build

```

1. Deploy your site to the static web app:

```bash

npx swa deploy --app-name swa-demo-site

```

The URL for your site is displayed once the deployment is finished. Select the site URL to open the site in the browser. The standard Microsoft Entra ID sign in page is displayed:

![Screen shot of the Microsoft authentication sign in page.](./media/add-authentication/remote-auth-page.png)

Sign in with your Microsoft account.

[!INCLUDE [Clean up resources](../../includes/static-web-apps/quickstart-direct-deploy-clean-up-resources.md)]

## Related content

* [Authentication and authorization](./authentication-authorization.yml)

* [Custom authentication](./authentication-custom.md)


# Front End Frameworks

# Configure front-end frameworks and libraries with Azure Static Web Apps

Azure Static Web Apps requires that you have the appropriate configuration values in the [build configuration file](build-configuration.md) for your front-end framework or library.

## Configuration

The following table lists the settings for a series of frameworks and libraries<sup>1</sup>.

The intent of the table columns is explained by the following items:

- **Output location (App artifact location)**: Lists the value for `output_location`, which is the [folder for built static website files](build-configuration.md).

- **API artifact location (api location)**: Lists the value for `api_location`, which is the folder containing the built managed Azure Functions for frameworks that require server-side hosting.

- **Custom build command**: When the framework requires  a command different from `npm run build` or `npm run azure:build`, you can define a [custom build command](build-configuration.md#custom-build-commands).

> [!NOTE]

> Some web frameworks that feature server-side rendering and can be deployed to Azure Static Web Apps. This means your app is built into static assets along with Azure Functions. In the configuration file, the static assets are mapped to the *output location* and the Azure Functions files map to the *API artifact location*.

| Framework | Output location (App artifact location) | API artifact location | Custom build command |

|--|--|--|--|

| [Alpine.js](https://github.com/alpinejs/alpine/) | `/`  | n/a | n/a <sup>2</sup> |

| [Angular](https://angular.dev/) | `dist/<APP_NAME>/browser` |  n/a | n/a |

| [Astro](https://astro.build) | `dist` | n/a  | n/a |

| [Aurelia](https://aurelia.io/) | `dist` | n/a |  n/a |

| [Backbone.js](https://backbonejs.org/) | `/` | n/a | n/a |

| [Blazor (WASM)](https://dotnet.microsoft.com/apps/aspnet/web-apps/blazor) | `wwwroot` | `n/a` | n/a |

| [Ember](https://emberjs.com/) | `dist` | n/a | n/a |

| [Flutter](https://flutter.dev/) | `build/web` | n/a | `flutter build web` |

| [Framework7](https://framework7.io/) | `www` | n/a | `npm run build-prod` |

| [Glimmer](https://glimmerjs.com/) | `dist` | n/a | n/a |

| [HTML](https://developer.mozilla.org/docs/Web/HTML) | `/` | n/a | n/a |

| [Hugo](https://gohugo.io/) | `public` | n/a | n/a |

| [Hyperapp](https://github.com/jorgebucaran/hyperapp) | `/` | n/a | n/a |

| [JavaScript](https://developer.mozilla.org/docs/Web/javascript) | `/` | n/a | n/a |

| [jQuery](https://jquery.com/) | `/` | n/a | n/a |

| [KnockoutJS](https://knockoutjs.com/) | `dist` | n/a | n/a |

| [LitElement](https://lit-element.polymer-project.org/) | `/` | n/a | n/a |

| [Mithril](https://mithril.js.org/) | `/` | n/a | n/a |

| [Next.js](https://nextjs.org/) (Static HTML Export) | `out` | n/a | n/a |

| [Next.js](https://nextjs.org/) (Hybrid Rendering) | `/` | n/a | n/a |

| [Nuxt 2](https://v2.nuxt.com/) | `/` | n/a | n/a |

| [Nuxt 3](https://nuxt.com/) | `.output/public` | `.output/server` | n/a |

| [Preact](https://preactjs.com/) | `dist` | n/a | n/a |

| [React](https://reactjs.org/) | `build` | n/a | n/a |

| [RedwoodJS](https://redwoodjs.com/) | `web/dist` | n/a | `yarn rw build web` |

| [Solid](https://www.solidjs.com/) | `dist` | n/a | n/a |

| [Stencil](https://stenciljs.com/) | `www` | n/a |  n/a |

| [SvelteKit (static)](https://svelte.dev/) | `build` | n/a | n/a |

| [SvelteKit](https://kit.svelte.dev/) | `build/static` | `build/server` | n/a |

| [Three.js](https://threejs.org/) | `/` | n/a | n/a |

| [TypeScript](https://www.typescriptlang.org/) | `dist` | n/a | n/a |

| [Vue.js](https://vuejs.org/) | `dist` | n/a | n/a |

<sup>1</sup> The above table is not meant to be an exhaustive list of frameworks and libraries that work with Azure Static Web Apps.

<sup>2</sup> Not applicable

## Next steps

- [Build and workflow configuration](build-configuration.md)


# Deploy Angular

# Deploy an Angular app on Azure Static Web Apps

In this article, you learn to deploy an Angular application to Azure Static Web Apps using the Azure portal.

## Prerequisites

[!INCLUDE [prerequisites](../../includes/static-web-apps/static-web-apps-tutorials-portal-prerequisites.md)]

## Create a repository

This article uses a GitHub template repository to make it easy for you to get started. The template features a starter app to deploy to Azure Static Web Apps.

1. Navigate to the following location to create a new repository:

[https://github.com/staticwebdev/angular-basic/generate](https://github.com/login?return_to=%2Fstaticwebdev%2Fangular-basic%2Fgenerate)

1. Name your repository **my-first-static-web-app**

1. Select **Create repository from template**.

This article uses an Azure DevOps repository to make it easy for you to get started. The repository features a starter app used to deploy using Azure Static Web Apps.

1. Sign in to Azure DevOps.

1. Select **New repository**.

1. In the *Create new project* window, expand the **Advanced** menu, and make the following selections:

| Setting | Value |

|--|--|

| Project | Enter **my-first-web-static-app**. |

| Visibility | Select **Private**. |

| Version control | Select **Git**. |

| Work item process | Select the option that best suits your development methods. |

1. Select **Create**.

1. Select the **Repos** menu item.

1. Select the **Files** menu item.

1. Under the *Import repository* card, select **Import**.

1. Copy a repository URL for the framework of your choice, and paste it into the *Clone URL* box.

[https://github.com/staticwebdev/angular-basic.git](https://github.com/staticwebdev/angular-basic.git)

1. Select **Import** and wait for the import process to complete.

## Create a static web app

[!INCLUDE [create steps](../../includes/static-web-apps/static-web-apps-tutorials-portal-create.md)]

In the _Build Details_ section, add configuration details specific to your preferred front-end framework.

1. Select **Angular** from the _Build Presets_ dropdown.

1. Keep the default value in the _App location_ box.

1. Leave the _Api location_ box empty.

1. Type **dist/angular-basic** in the _Output location_ box.

> [!NOTE]

> If you are using these instructions with your own code and Angular 17 or above, the output location value needs to end with **/browser**.

Select **Review + create**.

> [!NOTE]

> You can edit the [workflow file](build-configuration.md) to change these values after you create the app.

Select **Create**.

Select **Go to resource**.

## View the website

[!INCLUDE [view website](../../includes/static-web-apps/static-web-apps-tutorials-portal-view-website.md)]

## Clean up resources

[!INCLUDE [clean up](../../includes/static-web-apps/static-web-apps-tutorials-portal-clean-up.md)]

## Next steps

> [!div class="nextstepaction"]

> [Add an API to your application](./add-api.md?tabs=angular)


# Deploy React

# Deploy a React app on Azure Static Web Apps

In this article, you learn to deploy a React application to Azure Static Web Apps using the Azure portal.

## Prerequisites

[!INCLUDE [prerequisites](../../includes/static-web-apps/static-web-apps-tutorials-portal-prerequisites.md)]

## Create a repository

This article uses a GitHub template repository to make it easy for you to get started. The template features a starter app to deploy to Azure Static Web Apps.

1. Navigate to the following location to create a new repository:

[https://github.com/staticwebdev/react-basic/generate](https://github.com/login?return_to=%2Fstaticwebdev%2Freact-basic%2Fgenerate)

1. Name your repository **my-first-static-web-app**.

1. Select **Create repository from template**.

This article uses an Azure DevOps repository to make it easy for you to get started. The repository features a starter app used to deploy using Azure Static Web Apps.

1. Sign in to Azure DevOps.

2. Select **New repository**.

3. In the *Create new project* window, expand the **Advanced** menu and make the following selections:

| Setting | Value |

|--|--|

| Project | Enter **my-first-web-static-app**. |

| Visibility | Select **Private**. |

| Version control | Select **Git**. |

| Work item process | Select the option that best suits your development methods. |

4. Select **Create**.

5. Select the **Repos** menu item.

6. Select the **Files** menu item.

7. Under the *Import repository* card, select **Import**.

8. Copy a repository URL for the framework of your choice, and paste it into the *Clone URL* box.

[https://github.com/staticwebdev/react-basic.git](https://github.com/staticwebdev/react-basic.git)

9. Select **Import** and wait for the import process to complete.

## Create a static web app

[!INCLUDE [create steps](../../includes/static-web-apps/static-web-apps-tutorials-portal-create.md)]

In the _Build Details_ section, add configuration details specific to your preferred front-end framework.

1. Select **React** from the _Build Presets_ dropdown.

1. Keep the default value in the _App location_ box.

1. Leave the _Api location_ box empty.

1. Type **build** in the _App artifact location_ box.

Select **Review + create**.

> [!NOTE]

> You can edit the [workflow file](build-configuration.md) to change these values after you create the app.

Select **Create**.

Select **Go to resource**.

## View the website

[!INCLUDE [view website](../../includes/static-web-apps/static-web-apps-tutorials-portal-view-website.md)]

## Clean up resources

[!INCLUDE [clean up](../../includes/static-web-apps/static-web-apps-tutorials-portal-clean-up.md)]

## Next steps

> [!div class="nextstepaction"]

> [Add an API to your application](./add-api.md?tabs=react)


# Nextjs

# Deploy Next.js websites on Azure Static Web Apps

Next.js support on Azure Static Web Apps can be categorized as two deployment models:

- **Hybrid**: Hybrid Next.js sites, which include support for all Next.js features such as the [App Router](https://nextjs.org/docs/app), the [Pages Router](https://nextjs.org/docs/pages) and [React Server Components](https://nextjs.org/docs/app/building-your-application/rendering/server-components)

- **Static**: Static Next.js sites, which use the [Static HTML Export](https://nextjs.org/docs/advanced-features/static-html-export) option of Next.js.

## Hybrid Next.js applications (preview)

Static Web Apps supports deploying hybrid Next.js websites. This enables support for all Next.js features, such as the [App Router](https://nextjs.org/docs/app) and [React Server Components](https://nextjs.org/docs/app/building-your-application/rendering/server-components).

Hybrid Next.js applications are hosted using the Static Web Apps globally distributed static content host and managed backend functions. Next.js backend functions are hosted on a dedicated App Service instance to ensure full feature compatibility.

With hybrid Next.js applications, pages and components can be dynamically rendered, statically rendered or incrementally rendered. Next.js automatically determines the best rendering and caching model based on your data fetching for optimal performance.

Key features that are available in the preview are:

- [App Router](https://nextjs.org/docs/app) and [Pages Router](https://nextjs.org/docs/pages)

- [React Server Components](https://nextjs.org/docs/app/building-your-application/rendering/server-components)

- [Hybrid rendering](https://nextjs.org/docs/app/building-your-application/rendering/server-components#server-rendering-strategies)

- [Route Handlers](https://nextjs.org/docs/app/building-your-application/routing/route-handlers)

- [Image optimization](https://nextjs.org/docs/app/guides/self-hosting#image-optimization)

- [Internationalization](https://nextjs.org/docs/advanced-features/i18n-routing)

- [Middleware](https://nextjs.org/docs/advanced-features/middleware)

- [Authentication](https://nextjs.org/docs/pages/building-your-application/authentication)

Follow the [deploy hybrid Next.js applications](deploy-nextjs-hybrid.md) tutorial to learn how to deploy a hybrid Next.js application to Azure.

[!INCLUDE [Unsupported Next.js features](../../includes/static-web-apps-nextjs-unsupported.md)]

## Server side rendering

[!INCLUDE [Server side rendering](../../includes/static-web-apps/static-web-apps-nextjs-backends.md)]

## Static HTML export

You can deploy a Next.js static site using the [static HTML export](https://nextjs.org/docs/advanced-features/static-html-export) feature of Next.js. This configuration generates static HTML files during the build, which are cached and reused for all requests. See the [supported features of Next.js static exports](https://nextjs.org/docs/pages/building-your-application/deploying/static-exports).

Static Next.js sites are hosted on the Azure Static Web Apps globally distributed network for optimal performance. Additionally, you can add [linked backends for your APIs](apis-overview.md).

To enable static export of a Next.js application, add `output: 'export'` to the nextConfig in `next.config.js`.

```

/** @type {import('next').NextConfig} */

const nextConfig = {

output: 'export',

// Optional: Change the output directory `out` -> `dist`

// distDir: 'dist',

}

module.exports = nextConfig

```

You must also specify the `output_location` in the GitHub Actions/Azure DevOps configuration. By default, this value is set to `out` as per Next.js defaults. If a custom output location is indicated in the Next.js configuration, the value provided for the build should match the one configured in Next.js' export.

If you're using custom build scripts, set `IS_STATIC_EXPORT` to `true` in the Static Web Apps task of the GitHub Actions/Azure DevOps YAML file.

The following example shows the GitHub Actions job that is enabled for static exports.

```yaml

- name: Build And Deploy

id: swa

uses: azure/static-web-apps-deploy@latest

with:

azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_TOKEN }}

repo_token: ${{ secrets.GITHUB_TOKEN }} # Used for GitHub integrations (i.e. PR comments)

action: "upload"

app_location: "/" # App source code path

api_location: "" # Api source code path - optional

output_location: "out" # Built app content directory - optional

env: # Add environment variables here

IS_STATIC_EXPORT: true

```

Follow the [deploy static-rendered Next.js websites](deploy-nextjs-static-export.md) tutorial to learn how to deploy a statically exported Next.js application to Azure.


# Deploy Vue

# Deploy a Vue app in Azure Static Web Apps

In this article, you learn to deploy a Vue application to Azure Static Web Apps using the Azure portal.

## Prerequisites

[!INCLUDE [prerequisites](../../includes/static-web-apps/static-web-apps-tutorials-portal-prerequisites.md)]

## Create a repository

This article uses a GitHub template repository to make it easy for you to get started. The template features a starter app to deploy to Azure Static Web Apps.

1. Navigate to the following location to create a new repository:

[https://github.com/staticwebdev/vue-basic/generate](https://github.com/login?return_to=%2Fstaticwebdev%2Fvue-basic%2Fgenerate)

1. Name your repository **my-first-static-web-app**

1. Select **Create repository from template**.

This article uses an Azure DevOps repository to make it easy for you to get started. The repository features a starter app used to deploy using Azure Static Web Apps.

1. Sign in to Azure DevOps.

2. Select **New repository**.

3. In the *Create new project* window, expand **Advanced** menu, and make the following selections:

| Setting | Value |

|--|--|

| Project | Enter **my-first-web-static-app**. |

| Visibility | Select **Private**. |

| Version control | Select **Git**. |

| Work item process | Select the option that best suits your development methods. |

4. Select **Create**.

5. Select the **Repos** menu item.

6. Select the **Files** menu item.

7. Under the *Import repository* card, select **Import**.

8. Copy a repository URL for the framework of your choice, and paste it into the *Clone URL* box.

[https://github.com/staticwebdev/vue-basic.git](https://github.com/staticwebdev/vue-basic.git)

9. Select **Import** and wait for the import process to complete.

## Create a static web app

[!INCLUDE [create steps](../../includes/static-web-apps/static-web-apps-tutorials-portal-create.md)]

In the _Build Details_ section, add configuration details specific to your preferred front-end framework.

1. Select **Vue.js** from the _Build Presets_ dropdown.

1. Keep the default value in the _App location_ box.

1. Leave the _Api location_ box empty.

1. Keep the default value in the _Output location_ box.

Select **Review + create**.

> [!NOTE]

> You can edit the [workflow file](build-configuration.md) to change these values after you create the app.

Select **Create**.

Select **Go to resource**.

## View the website

[!INCLUDE [view website](../../includes/static-web-apps/static-web-apps-tutorials-portal-view-website.md)]

## Clean up resources

[!INCLUDE [clean up](../../includes/static-web-apps/static-web-apps-tutorials-portal-clean-up.md)]

## Next steps

> [!div class="nextstepaction"]

> [Add an API to your application](./add-api.md?tabs=vue)


# Configuration

# Configure Azure Static Web Apps

You can define configuration for Azure Static Web Apps in the _staticwebapp.config.json_ file, which controls the following settings:

- [Routing](#routes)

- [Authentication](#authentication)

- [Authorization](#routes)

- [Fallback rules](#fallback-routes)

- [HTTP response overrides](#response-overrides)

- [Global HTTP header definitions](#global-headers)

- [Custom MIME types](#example-configuration-file)

- [Networking](#networking)

> [!NOTE]

> [_routes.json_](https://github.com/Azure/static-web-apps/wiki/routes.json-reference-(deprecated)) that was previously used to configure routing is deprecated. Use _staticwebapp.config.json_ as described in this article to configure routing and other settings for your static web app.

>

> This document describes how to configure Azure Static Web Apps, which is a standalone product and separate from the [static website hosting](../storage/blobs/storage-blob-static-website.md) feature of Azure Storage.

## File location

The recommended location for the _staticwebapp.config.json_ is in the folder set as the `app_location` in the [workflow file](./build-configuration.md). However, you can place the file in any subfolder within the folder set as the `app_location`. Additionally, if there's a build step, you must ensure that the build step outputs the file to the root of the output_location.

See the [example configuration](#example-configuration-file) file for details.

> [!IMPORTANT]

> The deprecated [_routes.json_ file](https://github.com/Azure/static-web-apps/wiki/routes.json-reference-(deprecated)) is ignored if a _staticwebapp.config.json_ exists.

## Routes

You can define rules for one or more routes in your static web app. Route rules allow you to restrict access to users in specific roles or perform actions such as redirect or rewrite. Routes are defined as an array of routing rules. See the [example configuration file](#example-configuration-file) for usage examples.

- Rules are defined in the `routes` array, even if you only have one route.

- Rules are evaluated in the order as they appear in the `routes` array.

- Rule evaluation stops at the first match. A match occurs when the `route` property and a value in the `methods` array (if specified) match the request. Each request can match at most one rule.

The routing concerns significantly overlap with authentication (identifying the user) and authorization (assigning abilities to the user) concepts. Make sure to read the [authentication and authorization](authentication-authorization.yml) guide along with this article.

### Define routes

Each rule is composed of a route pattern, along with one or more of the optional rule properties. Route rules are defined in the `routes` array. See the [example configuration file](#example-configuration-file) for usage examples.

> [!IMPORTANT]

> Only the `route` and `methods` (if specified) properties are used to determine whether a rule matches a request.

| Rule property | Required | Default value | Comment |

|--|--|--|--|

| `route` | Yes | n/a | The route pattern requested by the caller.<ul><li>[Wildcards](#wildcards) are supported at the end of route paths.<ul><li>For instance, the route _/admin\*_ matches any route beginning with _/admin_.</ul></ul> |

| `methods` | No | All methods | Defines an array of request methods that match a route. Available methods include: `GET`, `HEAD`, `POST`, `PUT`, `DELETE`, `CONNECT`, `OPTIONS`, `TRACE`, and `PATCH`. |

| `rewrite` | No | n/a | Defines the file or path returned from the request.<ul><li>Is mutually exclusive to a `redirect` rule.<li>Rewrite rules don't change the browser's location.<li>Values must be relative to the root of the app.</ul> |

| `redirect` | No | n/a | Defines the file or path redirect destination for a request.<ul><li>Is mutually exclusive to a `rewrite` rule.<li>Redirect rules change the browser's location.<li>Default response code is a [`302`](https://developer.mozilla.org/docs/Web/HTTP/Status/302) (temporary redirect), but you can override with a [`301`](https://developer.mozilla.org/docs/Web/HTTP/Status/301) (permanent redirect).</ul> |

| `statusCode` | No | `301` or `302` for redirects | The [HTTP status code](https://developer.mozilla.org/docs/Web/HTTP/Status) of the response. |

| `headers`<a id="route-headers"></a> | No | n/a | Set of [HTTP headers](https://developer.mozilla.org/docs/Web/HTTP/Headers) added to the response. <ul><li>Route-specific headers override [`globalHeaders`](#global-headers) when the route-specific header is the same as the global header is in the response.<li>To remove a header, set the value to an empty string.</ul> |

| `allowedRoles` | No | anonymous | Defines an array of role names required to access a route. <ul><li>Valid characters include `a-z`, `A-Z`, `0-9`, and `_`.<li>The built-in role, [`anonymous`](./authentication-authorization.yml), applies to all users.<li>The built-in role, [`authenticated`](./authentication-authorization.yml), applies to any logged-in user.<li>Users must belong to at least one role.<li>Roles are matched on an _OR_ basis.<ul><li>If a user is in any of the listed roles, then access is granted.</ul><li>Individual users are associated to roles through [invitations](authentication-authorization.yml).</ul> |

Each property has a specific purpose in the request/response pipeline.

| Purpose | Properties |

|--|--|

| Match routes | `route`, `methods` |

| Process after a rule is matched and authorized | `rewrite` (modifies request)<br><br>`redirect`, `headers`, `statusCode` (modifies response) |

| Authorize after a route is matched | `allowedRoles` |

### Specify route patterns

The `route` property can be an exact route or a wildcard pattern.

#### Exact route

To define an exact route, place the full path of the file in the `route` property.

```json

{

"route": "/profile/index.html",

"allowedRoles": ["authenticated"]

}

```

This rule matches requests for the file _/profile/index.html_. Because _index.html_ is the default file, the rule also matches requests for the folder (_/profile_ or _/profile/_).

> [!IMPORTANT]

> If you use a folder path (`/profile` or `/profile/`) in the `route` property, it won't match requests for the file _/profile/index.html_. When protecting a route that serves a file, always use the full path of the file such as `/profile/index.html`.

#### <a name="wildcards"></a>Wildcard pattern

Wildcard rules match all requests in a route pattern, and are only supported at the end of a path. See the [example configuration file](#example-configuration-file) for usage examples.

For instance, to implement routes for a calendar application, you can rewrite all URLs that fall under the _calendar_ route to serve a single file.

```json

{

"route": "/calendar*",

"rewrite": "/calendar.html"

}

```

The _calendar.html_ file can then use client-side routing to serve a different view for URL variations like `/calendar/january/1`, `/calendar/2020`, and `/calendar/overview`.

> [!NOTE]

> A route pattern of `/calendar/*` matches all requests under the _/calendar/_ path. However, it won't match requests for the paths _/calendar_ or _/calendar.html_. Use `/calendar*` to match all requests that begin with _/calendar_.

You can filter wildcard matches by file extension. For instance, if you wanted to add a rule that only matches HTML files in a given path you could create the following rule:

```json

{

"route": "/articles/*.html",

"headers": {

"Cache-Control": "public, max-age=604800, immutable"

}

}

```

To filter on multiple file extensions, you include the options in curly braces, as shown in this example:

```json

{

"route": "/images/thumbnails/*.{png,jpg,gif}",

"headers": {

"Cache-Control": "public, max-age=604800, immutable"

}

}

```

Common uses cases for wildcard routes include:

- Serving a specific file for an entire path pattern

- Enforcing authentication and authorization rules

- Implementing specialized caching rules

### <a name="securing-routes-with-roles"></a>Secure routes with roles

Routes are secured by adding one or more role names into a rule's `allowedRoles` array. See the [example configuration file](#example-configuration-file) for usage examples.

> [!IMPORTANT]

> Routing rules can only secure HTTP requests to routes that are served from Static Web Apps. Many front-end frameworks use client-side routing that modifies routes in the browser without issuing requests to Static Web Apps. Routing rules don't secure client-side routes. Clients should call [HTTP APIs](apis-overview.md) to retrieve sensitive data. Ensure APIs validate a [user's identity](user-information.md) before returning data.

By default, every user belongs to the built-in `anonymous` role, and all logged-in users are members of the `authenticated` role. Optionally, users are associated to custom roles via [invitations](./authentication-authorization.yml).

For instance, to restrict a route to only authenticated users, add the built-in `authenticated` role to the `allowedRoles` array.

```json

{

"route": "/profile*",

"allowedRoles": ["authenticated"]

}

```

You can create new roles as needed in the `allowedRoles` array. To restrict a route to only administrators, you could define your own role named `administrator`, in the `allowedRoles` array.

```json

{

"route": "/admin*",

"allowedRoles": ["administrator"]

}

```

- You have full control over role names; there's no list to which your roles must adhere.

- Individual users are associated to roles through [invitations](authentication-authorization.yml).

> [!IMPORTANT]

> When securing content, specify exact files when possible. If you have many files to secure, use wildcards after a shared prefix. For example: `/profile*` secures all possible routes that start with _/profile_, including _/profile_.

#### Restrict access to entire application

You often want to require authentication for every route in your application. To lock down your routes, add a rule that matches all routes and include the built-in `authenticated` role in the `allowedRoles` array.

The following example configuration blocks anonymous access and redirects all unauthenticated users to the Microsoft Entra sign-in page.

```json

{

"routes": [

{

"route": "/*",

"allowedRoles": ["authenticated"]

}

],

"responseOverrides": {

"401": {

"statusCode": 302,

"redirect": "/.auth/login/aad"

}

}

}

```

> [!NOTE]

> By default, all pre-configured identity providers are enabled. To block an authentication provider, see [Authentication and authorization](authentication-authorization.yml#block-an-authentication-provider).

## Fallback routes

Single Page Applications often rely on client-side routing. These client-side routing rules update the browser's window location without making requests back to the server. If you refresh the page, or go directly to URLs generated by client-side routing rules, a server-side fallback route is required to serve the appropriate HTML page. The fallback page is often designated as _index.html_ for your client-side app.

> [!NOTE]

> Route rules aren't applied on requests that trigger `navigationFallback`.

You can define a fallback rule by adding a `navigationFallback` section. The following example returns _/index.html_ for all static file requests that don't match a deployed file.

```json

{

"navigationFallback": {

"rewrite": "/index.html"

}

}

```

You can control which requests return the fallback file by defining a filter. In the following example, requests for certain routes in the _/images_ folder and all files in the _/css_ folder are excluded from returning the fallback file.

```json

{

"navigationFallback": {

"rewrite": "/index.html",

"exclude": ["/images/*.{png,jpg,gif}", "/css/*"]

}

}

```

For example, with the following directory structure, the above navigation fallback rule would result in the outcomes detailed in the following table.

```files

├── images

│   ├── logo.png

│   ├── headshot.jpg

│   └── screenshot.gif

│

├── css

│   └── global.css

│

├── about.html

└── index.html

```

| Requests to... | returns... | with the status... |

|--|--|--|

| _/about/_ | The _/index.html_ file. | `200` |

| _/images/logo.png_ | The image file. | `200` |

| _/images/icon.svg_ | The _/index.html_ file - since the _svg_ file extension isn't listed in the `/images/*.{png,jpg,gif}` filter. | `200` |

| _/images/unknown.png_ | File not found error. | `404` |

| _/css/unknown.css_ | File not found error. | `404` |

| _/css/global.css_ | The stylesheet file. | `200` |

| _/about.html_ | The HTML page. | `200` |

| Any other path outside the _/images_ or _/css_ folders that doesn't match the path to a deployed file. | The _/index.html_ file. | `200` |

> [!IMPORTANT]

> If you are migrating from the deprecated [_routes.json_](https://github.com/Azure/static-web-apps/wiki/routes.json-reference-(deprecated)) file, do not include the legacy fallback route (`"route": "/*"`) in the [routing rules](#routes).

## Global headers

The `globalHeaders` section provides a set of HTTP headers applied to each response, unless overridden by a [route header](#route-headers) rule, otherwise the union of both the headers from the route and the global headers is returned.

See the [example configuration file](#example-configuration-file) for usage examples.

To remove a header, set the value to an empty string (`""`).

Some common use cases for global headers include:

- Custom caching rules

- Security policies

- Encoding settings

- Cross-origin resource sharing ([CORS](https://developer.mozilla.org/docs/Web/HTTP/CORS)) configuration

The following example implements a custom CORS configuration.

```json

{

"globalHeaders": {

"Access-Control-Allow-Origin": "https://example.com",

"Access-Control-Allow-Methods": "POST, GET, OPTIONS"

}

}

```

> [!NOTE]

> Global headers do not affect API responses. Headers in API responses are preserved and returned to the client.

## Response overrides

The `responseOverrides` section provides an opportunity to define a custom response when the server would otherwise return an error code. See the [example configuration file](#example-configuration-file) for usage examples.

The following HTTP codes are available to override:

| Status Code | Meaning | Possible cause |

|--|--|--|

| [400](https://developer.mozilla.org/docs/Web/HTTP/Status/400) | Bad request | Invalid invitation link |

| [401](https://developer.mozilla.org/docs/Web/HTTP/Status/401) | Unauthorized | Request to restricted pages while unauthenticated |

| [403](https://developer.mozilla.org/docs/Web/HTTP/Status/403) | Forbidden | <ul><li>User is logged in but doesn't have the roles required to view the page.<li>User is logged in but the runtime can't get the user details from their identity claims.<li>There are too many users logged in to the site with custom roles, therefore the runtime can't sign in the user.</ul> |

| [404](https://developer.mozilla.org/docs/Web/HTTP/Status/404) | Not found | File not found |

The following example configuration demonstrates how to override an error code.

```json

{

"responseOverrides": {

"400": {

"rewrite": "/invalid-invitation-error.html"

},

"401": {

"statusCode": 302,

"redirect": "/login"

},

"403": {

"rewrite": "/custom-forbidden-page.html"

},

"404": {

"rewrite": "/custom-404.html"

}

}

}

```

## Platform

The `platform` section controls platform specific settings, such as the API language runtime version.

### Select the API language runtime version

[!INCLUDE [Languages and runtimes](../../includes/static-web-apps-languages-runtimes.md)]

## Networking

The `networking` section controls the network configuration of your static web app. To restrict access to your app, specify a list of allowed IP address blocks in `allowedIpRanges`. For more information about the number of allowed IP address blocks, see [Quotas in Azure Static Web Apps](../static-web-apps/quotas.md).

> [!NOTE]

> Networking configuration is only available in the Azure Static Web Apps Standard plan.

Define each IPv4 address block in Classless Inter-Domain Routing (CIDR) notation. To learn more about CIDR notation, see [Classless Inter-Domain Routing](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing). Each IPv4 address block can denote either a public or private address space. If you only want to allow access from a single IP Address, you can use the `/32` CIDR block.

```json

{

"networking": {

"allowedIpRanges": [

"10.0.0.0/24",

"100.0.0.0/32",

"192.168.100.0/22"

]

}

}

```

When one or more IP address blocks are specified, requests originating from IP addresses that don't match a value in `allowedIpRanges` are denied access.

In addition to IP address blocks, you can also specify [service tags](../virtual-network/service-tags-overview.md#discover-service-tags-by-using-downloadable-json-files) in the `allowedIpRanges` array to restrict traffic to certain Azure services.

```json

"networking": {

"allowedIpRanges": ["AzureFrontDoor.Backend"]

}

```

## Authentication

* [Default authentication providers](authentication-authorization.yml#set-up-sign-in) don't require settings in the configuration file.

* [Custom authentication providers](authentication-custom.md) use the `auth` section of the settings file.

For details on how to restrict routes to authenticated users, see [Securing routes with roles](#securing-routes-with-roles).

### Disable cache for authenticated paths

If you set up [manual integration with Azure Front Door](front-door-manual.md), you might want to disable caching for your secured routes. With [enterprise-grade edge](enterprise-edge.md) enabled, caching is already disabled for your secured routes.

To disable Azure Front Door caching for secured routes, add `"Cache-Control": "no-store"` to the route header definition.

For example:

```json

{

"route": "/members",

"allowedRoles": ["authenticated, members"],

"headers": {

"Cache-Control": "no-store"

}

}

```

## Forwarding gateway

The `forwardingGateway` section configures how a static web app is accessed from a forwarding gateway such as a Content Delivery Network (CDN) or Azure Front Door.

> [!NOTE]

> Forwarding gateway configuration is only available in the Azure Static Web Apps Standard plan.

### Allowed Forwarded Hosts

The `allowedForwardedHosts` list specifies which hostnames to accept in the [X-Forwarded-Host](https://developer.mozilla.org/docs/Web/HTTP/Headers/X-Forwarded-Host) header. If a matching domain is in the list, Static Web Apps uses the `X-Forwarded-Host` value when constructing redirect URLs, such as after a successful sign-in.

For Static Web Apps to function correctly behind a forwarding gateway, the request from the gateway must include the correct hostname in the `X-Forwarded-Host` header and the same hostname must be listed in `allowedForwardedHosts`.

```json

"forwardingGateway": {

"allowedForwardedHosts": [

"example.org",

"www.example.org",

"staging.example.org"

]

}

```

If the `X-Forwarded-Host` header doesn't match a value in the list, the requests still succeed, but the header isn't used in the response.

### Required headers

Required headers are HTTP headers that must be sent with each request to your site. One use of required headers is to deny access to a site unless all of the required headers are present in each request.

For example, the following configuration shows how you can add a unique identifier for [Azure Front Door](../frontdoor/front-door-overview.md) that limits access to your site from a specific Azure Front Door instance. See the [Configure Azure Front Door tutorial](front-door-manual.md) for full details.

```json

"forwardingGateway": {

"requiredHeaders": {

"X-Azure-FDID" : "692a448c-2b5d-4e4d-9fcc-2bc4a6e2335f"

}

}

```

- Key/value pairs can be any set of arbitrary strings

- Keys are case insensitive

- Values are case-sensitive

## Trailing slash

A trailing slash is the `/` at the end of a URL. Conventionally, a trailing slash URL refers to a directory on the web server, while a nontrailing slash indicates a file.

Search engines treat the two URLs separately, regardless of whether it's a file or a directory. When the same content is rendered at both of these URLs, your website serves duplicate content, which can negatively affect search engine optimization (SEO). When explicitly configured, Static Web Apps applies a set of URL normalization and redirect rules that help improve your website’s performance and SEO performance.

The following normalization and redirect rules apply for each of the available configurations:

### Always

When you're setting `trailingSlash` to `always`, all requests that don't include a trailing slash are redirected to a trailing slash URL. For example, `/contact` is redirected to `/contact/`.

```json

"trailingSlash": "always"

```

| Requests to... | returns... | with the status... | and path... |

|--|--|--|--|

| _/about_ | The _/about/index.html_ file | `301` | _/about/_ |

| _/about/_ | The _/about/index.html_ file | `200` | _/about/_ |

| _/about/index.html_ | The _/about/index.html_ file | `301` | _/about/_ |

| _/privacy.html_ | The _/privacy.html_ file | `301` | _/privacy/_ |

### Never

When setting `trailingSlash` to `never`, all requests ending in a trailing slash are redirected to a nontrailing slash URL. For example, `/contact/` is redirected to `/contact`.

```json

"trailingSlash": "never"

```

| Requests to... | returns... | with the status... | and path... |

|--|--|--|--|

| _/about_ | The _/about/index.html_ file | `200` | _/about_ |

| _/about/_ | The _/about/index.html_ file | `301` | _/about_ |

| _/about/index.html_ | The _/about/index.html_ file | `301` | _/about_ |

| _/privacy.html_ | The _/privacy.html_ file | `301` | _/privacy_ |

### Auto

When you set `trailingSlash` to `auto`, all requests to folders are redirected to a URL with a trailing slash. All requests to files are redirected to a nontrailing slash URL.

```json

"trailingSlash": "auto"

```

| Requests to... | returns... | with the status... | and path... |

|--|--|--|--|

| _/about_ | The _/about/index.html_ file | `301` | _/about/_ |

| _/about/_ | The _/about/index.html_ file | `200` | _/about/_ |

| _/about/index.html_ | The _/about/index.html_ file | `301` | _/about/_ |

| _/privacy.html_ | The _/privacy.html_ file | `301` | _/privacy_ |

For optimal website performance, configure a trailing slash strategy using one of the `always`, `never`, or `auto` modes.

By default, when the `trailingSlash` configuration is omitted, Static Web Apps applies the following rules:

| Requests to... | returns... | with the status... | and path... |

|--|--|--|--|

| _/about_ | The _/about/index.html_ file | `200` | _/about_ |

| _/about/_ | The _/about/index.html_ file | `200` | _/about/_ |

| _/about/index.html_ | The _/about/index.html_ file | `200` | _/about/index.html_ |

| _/privacy.html_ | The _/privacy.html_ file | `200` | _/privacy.html_ |

## Example configuration file

```json

{

"trailingSlash": "auto",

"routes": [

{

"route": "/profile*",

"allowedRoles": ["authenticated"]

},

{

"route": "/admin/index.html",

"allowedRoles": ["administrator"]

},

{

"route": "/images/*",

"headers": {

"cache-control": "must-revalidate, max-age=15770000"

}

},

{

"route": "/api/*",

"methods": ["GET"],

"allowedRoles": ["registeredusers"]

},

{

"route": "/api/*",

"methods": ["PUT", "POST", "PATCH", "DELETE"],

"allowedRoles": ["administrator"]

},

{

"route": "/api/*",

"allowedRoles": ["authenticated"]

},

{

"route": "/customers/contoso*",

"allowedRoles": ["administrator", "customers_contoso"]

},

{

"route": "/login",

"rewrite": "/.auth/login/github"

},

{

"route": "/.auth/login/x",

"statusCode": 404

},

{

"route": "/logout",

"redirect": "/.auth/logout"

},

{

"route": "/calendar*",

"rewrite": "/calendar.html"

},

{

"route": "/specials",

"redirect": "/deals",

"statusCode": 301

}

],

"navigationFallback": {

"rewrite": "index.html",

"exclude": ["/images/*.{png,jpg,gif}", "/css/*"]

},

"responseOverrides": {

"400": {

"rewrite": "/invalid-invitation-error.html"

},

"401": {

"redirect": "/login",

"statusCode": 302

},

"403": {

"rewrite": "/custom-forbidden-page.html"

},

"404": {

"rewrite": "/404.html"

}

},

"globalHeaders": {

"content-security-policy": "default-src https: 'unsafe-eval' 'unsafe-inline'; object-src 'none'"

},

"mimeTypes": {

".json": "text/json"

}

}

```

Based on the above configuration, review the following scenarios.

| Requests to... | results in... |

|--|--|

| _/profile_ | Authenticated users are served the _/profile/index.html_ file. Unauthenticated users are redirected to _/login_ by the `401` response override rule. |

| _/admin_, _/admin/_, or _/admin/index.html_ | Authenticated users in the _administrator_ role are served the _/admin/index.html_ file. Authenticated users not in the _administrator_ role are served a `403` error<sup>1</sup>. Unauthenticated users are redirected to _/login_ |

| _/images/logo.png_ | Serves the image with a custom cache rule where the max age is a little over 182 days (15,770,000 seconds). |

| _/api/admin_ | `GET` requests from authenticated users in the _registeredusers_ role are sent to the API. Authenticated users not in the _registeredusers_ role and unauthenticated users are served a `401` error.<br/><br/>`POST`, `PUT`, `PATCH`, and `DELETE` requests from authenticated users in the _administrator_ role are sent to the API. Authenticated users not in the _administrator_ role and unauthenticated users are served a `401` error. |

| _/customers/contoso_ | Authenticated users who belong to either the _administrator_ or _customers_contoso_ roles are served the _/customers/contoso/index.html_ file. Authenticated users not in the _administrator_ or _customers_contoso_ roles are served a `403` error<sup>1</sup>. Unauthenticated users are redirected to _/login_. |

| _/login_ | Unauthenticated users are challenged to authenticate with GitHub. |

| _/.auth/login/x | Since the route rule disables X authorization, a `404` error is returned. This error then falls back to serving _/index.html_ with a `200` status code. |

| _/logout_ | Users are logged out of any authentication provider. |

| _/calendar/2021/01_ | The browser is served the _/calendar.html_ file. |

| _/specials_ | The browser is permanently redirected to _/deals_. |

| _/data.json_ | The file served with the `text/json` MIME type. |

| _/about_, or any folder that matches client side routing patterns | The _/index.html_ file is served with a `200` status code. |

| An nonexistent file in the _/images/_ folder | A `404` error. |

<sup>1</sup> You can provide a custom error page by using a [response override rule](#response-overrides).

## Restrictions

The following restrictions exist for the _staticwebapp.config.json_ file.

- Max file size is 20 KB

- Max of 50 distinct roles

See the [Quotas article](quotas.md) for general restrictions and limitations.

## Next steps

> [!div class="nextstepaction"]

> [Set up authentication and authorization](authentication-authorization.yml)

## Related articles

- [Set application-level settings and environment variables used by backend APIs](application-settings.yml)

- [Define settings that control the build process](./build-configuration.md)


# Snippets

# Snippets in Azure Static Web Apps

Azure Static Web Apps allows you to inject custom code into the `head` or `body` elements at runtime. These pieces of code are known as *snippets*.

Snippets give you the flexibility to add code to every page in your site in a single place, all without modifying the core codebase.

Common use cases of snippets include:

- Analytics scripts

- Common scripts

- Global UI elements

> [!NOTE]

> Some front-end frameworks may overwrite your snippet code. Test your snippets before applying them to a production environment.

## Add a snippet

1. Go to your static web app in the Azure portal.

1. From the *Settings* menu, select **Snippets**.

1. Select the **Add** button.

1. Enter the following settings in the Snippets window:

| Setting | Value | Comments |

|---|---|---|

| Location | Select which HTML page element you want your code injected into. | |

| Name | Enter a snippet name. | |

| Insertion location | Select whether you want to **Prepend** or **Append** your code to the selected element. | *Prepend* means your code appears directly after the open tag of the element. *Append* means your code appears directly before the close tag of the element. |

| Environment | Select the environment(s) you want to target. | If you pick **Select environment**, then you can choose from different environments to target. |

1. Enter your code in the text box.

1. Select **OK** to close the window.

1. Select **Save** to commit your changes.

## Next steps

> [!div class="nextstepaction"]

> [Split traffic](./traffic-splitting.md)


# Custom Domain

# Custom domains with Azure Static Web Apps

> [!NOTE]

> Custom domain validation for Enterprise Grade Edge Static Web Apps now requires TXT token method - CNAME validation is no longer supported for new domains.

By default, Azure Static Web Apps provides an autogenerated domain name for your website, but you can point a custom domain to your site. Free SSL/TLS certificates are automatically created for the autogenerated domain name and any custom domains you may add.

When you map a custom domain to a static web app, you have a few options available, which include configuring subdomains and an apex domain.

The following table includes links to articles that demonstrate how to configure a custom domain based provider type. <sup>1</sup>

| Action | Using... | Using... |

|--|--|--|

| Set up a domain with the `www` subdomain | [Azure DNS](custom-domain-azure-dns.md) | [External provider](custom-domain-external.md) |

| Set up an apex domain | [Azure DNS](apex-domain-azure-dns.md) | [External provider](apex-domain-external.md) |

<sup>1</sup> Some registrars like GoDaddy don't support domain records that affect how you configure your apex domain. Consider using [Azure DNS](custom-domain-azure-dns.md) with these registrars to set up your apex domain.

> [!NOTE]

> Adding a custom domain to a [preview environment](preview-environments.md) is not supported. Unicode domains, including Punycode domains and the `xn--` prefix are also not supported.

## About domains

Setting up an apex domain is a common scenario to configure once your domain name is set up. Creating an apex domain is achieved by configuring an `ALIAS` or `ANAME` record or through `CNAME` flattening. Some domain registrars like GoDaddy and Squarespace (formerly Google) don't support these DNS records. If your domain registrar doesn't support all the DNS records you need, consider using [Azure DNS to configure your domain](custom-domain-azure-dns.md).

Alternatively, for domain registrars that don't support `ALIAS` records, `ANAME` records or `CNAME` flattening, you can configure an `A` record for your static web app. This configuration directs traffic to a single regional host of your static web app. Using `A` records isn't recommended as your application no longer benefits from global distribution, and this type of setup could affect application performance if your traffic is globally distributed.

> [!NOTE]

> `CNAME` record maps a domain name to another domain (or subdomain) whereas `A` record maps a domain name to an IP address. If the IP address changes, a `CNAME` entry is still valid, unlike `A` record. Let’s say you have WebApp1 and you would like users to access it from https://www.contoso.com. You can do it in two possible ways: you can create a `CNAME` record and map it to WebApp1.azurestaticapps.net. Alternatively, you can create an `A` record and map it to the IP address of WebApp1.

The following are terms you might encounter as you set up a custom domain.

* **Apex or root domains**: Given the domain `www.example.com`, the `www` prefix is known as the subdomain, while the remaining segment of `example.com` is referred to as the apex domain.

* **Domain registrar**: A registrar verifies the availability of a domain sells the rights to purchase a domain name.

* **DNS zone**: A Domain Name System (DNS) zone hosts the DNS records associated to a specific domain. There are various records available which direct traffic for different purposes. For example, the domain `example.com` may contain several DNS records. One record handles traffic for `mail.example.com` (for a mail server), and another `www.example.com` (for a website).

* **DNS hosting**: A DNS host maintains DNS servers that resolve a domain name to a specific IP address.

* **Name server**: A name server is responsible for storing the DNS records for a domain.

For custom domain verification to work with Static Web Apps, the DNS must be publicly resolvable. For automatic certificate renewal to work, the custom domain must resolve to the static web app over public internet. Automatic certificate renewal is supported even when you enable private endpoints. The purpose of a private endpoint for Static Web Apps is to block internet access to the site contents, but not to block internet DNS resolution to the site.

## Zero downtime migration

You may want to migrate a custom domain currently serving a production website to your static web app with zero downtime. DNS providers don't accept multiple records for the same name and host, so you can separately validate your ownership of the domain and route traffic to your web app.

1. Open your static web app in the Azure portal.

1. Add a **TXT record** for your custom domain (APEX or subdomain). Instead of entering the *Host* value as displayed, enter the *Host* in your DNS provider as follows:

* For APEX domains, enter `_dnsauth.www.<YOUR-DOMAIN.COM>`.

* For subdomains, enter `_dnsauth.<SUBDOMAIN>.<YOUR-DOMAIN.COM>`.

1. Once your domain is validated, you can migrate your traffic to your static web app by updating your `CNAME`, `ALIAS`, or `A` record to point to your [default host name](./apex-domain-external.md)

## Migrating domains between instances

Azure Static Web Apps only permit binding a unique domain to a single resource within a slice. Attempting to bind a domain already bound to another resource without first disassociating from the original resource will result in failure.

The slice your resource is placed in can be determined by inspecting the default URL assigned to it:

`<random-prefix>.<slice>.azurestaticapps.net`

For example, a Static Web App site with the default URL of `orange-pond-0a04b7203.2.azurestaticapps.net` has been placed in slice number 2.

If the static app you're migrating the domain from and to are both in the same slice you must either:

* Remove the domain from one instance, then add it to your new instance. This will result in some downtime.

* Delete and redeploy the new instance until the resulting resource is placed into a slice different from the source instance.

## Next steps

Use the following links for steps on how to set up your domain based on your provider.

* [Use Azure DNS](custom-domain-azure-dns.md)

* [Use an external DNS provider](custom-domain-external.md)


# Custom Domain Azure Dns

# Set up a custom domain with Azure DNS in Azure Static Web Apps

By default, Azure Static Web Apps provides an autogenerated domain name for your website, but you can point a custom domain to your site. Free SSL/TLS certificates are automatically created for the autogenerated domain name and any custom domains you may add.

Suppose you buy the domain `example.com` from a domain name registrar and then create a zone with the name `example.com` in Azure DNS. You want `www.example.com` to point to your Static Web Apps site.

- If you're using an apex domain (a domain without a subdomain, also known as a root domain), see [configuring a custom apex domain with Azure DNS](apex-domain-azure-dns.md).

- If you're using an external DNS provider, see [configuring a custom domain with external DNS](custom-domain-external.md) or [configuring a custom apex domain with external DNS](apex-domain-external.md).

## Prerequisites

- A domain purchased from a domain name registrar and hosted on Azure DNS. For details, see [Delegate your domain to Azure DNS](/azure/dns/dns-delegate-domain-azure-dns).

## Map the domain to your website

Now that your domain is hosted on Azure DNS, you can create a CNAME record for `www.<your domain>` to point to your Static Web App.

1. Sign in to the [Azure portal](https://portal.azure.com).

1. Enter the name of your static web app in the top search bar, or find the static web app in your resources.

1. Under **Settings**, select **Custom domains**.

1. Select **+ Add**, then select **Custom domain on Azure DNS**.

1. Enter the following values in the *Add custom domain on Azure DNS* window.

| Field name | Value |

| --- | --- |

| DNS zone | Select your domain name hosted on Azure DNS |

| Subdomain | **www** |

The *Full domain* is updated and should match the desired custom domain name.

1. Select **Add**

Static Web Apps makes the necessary adjustments to the DNS zone (including adding a CNAME), then validates the changes are available in the global DNS system.

> [!WARNING]

> If you receive the message *CNAME Record is invalid*, then check that your DNS zone lists the Microsoft DNS services with your DNS registrar.  If you have recently moved the domain to Azure DNS, you may need to wait for DNS propagation before adding the custom domain.

## Validate the custom domain

It may take some time for the DNS changes to propagate. The default time for Azure DNS is 1 hour.

Open a new browser and go to your domain (for example, `https://www.example.com`). Inspect the location to verify that your site is served securely using `https`.


# Apex Domain Azure Dns

# Set up an apex domain with Azure DNS in Azure Static Web Apps

Domain names without a subdomain are known as apex or root domains. For example, the domain `www.example.com` is the `www` subdomain joined with the `example.com` apex domain.

This guide demonstrates how to use `TXT` and `ALIAS` records to configure your apex domain in Azure DNS.

The following procedure requires you to copy settings from an Azure DNS zone you create and your existing static web app. Consider opening the Azure portal in two different windows to make it easier to switch between the two services.

> [!NOTE]

> Apex domain changes can take up to 72 hours to propagate.

## Validate domain ownership

1. Open the [Azure portal](https://portal.azure.com).

1. Go to your static web app.

1. Under *Settings*, select **Custom domains**.

1. Select **+ Add**, and then select **Custom Domain on Azure DNS** from the drop-down menu.

1. Select your apex domain name from the *DNS zone* drop-down.

If this list is empty, [create a public zone in Azure DNS](../dns/dns-getstarted-portal.md).

1. Select **Add**.

Wait as the DNS record and custom domain records are added for your static web app. It may take a minute or so to complete.

1. Select **Close**.

Observe the *Status* for the row of your apex domain. While this validation is running, the necessary CNAME or TXT and ALIAS records are created for you automatically. Once the validation is complete, your apex domain is publicly available.

Open a new browser tab and go to your apex domain. You should see your static web app in the browser. Also, inspect the location to verify that your site is served securely using `https`.

## Next steps

> [!div class="nextstepaction"]

> [Manage the default domain](custom-domain-default.md)


# Custom Domain External

# Set up a custom domain in Azure Static Web Apps

By default, Azure Static Web Apps provides an autogenerated domain name for your website, but you can point a custom domain to your site. Free SSL/TLS certificates automatically get created for the autogenerated domain name and any custom domains that you might add. This article shows how to configure your domain name with the `www` subdomain, using an external provider.

There are multiple methods of configuring a custom domain for use with Static Web Apps:

- If you're using an apex domain (a domain without a subdomain, also known as a root domain), see [configuring a custom apex domain on Static Web Apps](apex-domain-external.md).

- If you're using Azure DNS, see [configuring a custom domain with Azure DNS](custom-domain-azure-dns.md) or [configuring a custom apex domain with Azure DNS](apex-domain-azure-dns.md).

## Prerequisites

- You must be able to create a **CNAME** record on your DNS domain using the tools that your DNS service or domain registrar provides.

## Watch the video

> [!VIDEO https://learn.microsoft.com/Shows/5-Things/Configuring-a-custom-domain-with-Azure-Static-Web-Apps/player?format=ny]

## Get your static web app URL

1. Go to the [Azure portal](https://portal.azure.com).

1. Go to your static web app.

1. From the *Overview* window, copy the generated **URL** of your site and set it aside in a text editor for future use.

## Create a CNAME record on your domain registrar account

Domain registrars are services you can use to purchase and manage domain names. To find a domain registrar, see the [ICANN list of accredited registrars](https://www.icann.org/en/accredited-registrars).

1. Open a new browser tab and sign in to your domain registrar account.

1. Go to your domain name's DNS configuration settings.

1. Add a new `CNAME` record with the following values.

| Setting | Value |

|--|--|

| Type | `CNAME` |

| Host | Your subdomain, such as **www** |

| Value | Paste the domain name you set aside in the text editor. |

| TTL (if applicable) | Leave as default value. |

## Create a CNAME record in Azure Static Web Apps

1. Return to your static web app in the Azure portal.

1. Under *Settings*, select **Custom domains** > **+ Add**. Select **Custom domain on other DNS**.

1. Select **+ Add**.

1. In the *Enter domain* tab, enter your domain name prefixed with **www**, and then select **Next**.

For instance, if your domain name is `example.com`, enter `www.example.com`.

1. In the *Validate + add* tab, enter the following values.

| Setting | Value |

|---|---|

| Domain name | This value should match the domain name you entered in the previous step (with the `www` subdomain). |

| Hostname record type | Select **CNAME**. |

1. Select **Add**.

Azure validates that the CNAME record was created correctly and is available in the global DNS system.  Propagation depends on the time to live (TTL) for your domain and may take several days. If the validation fails, return to add the custom domain later.

1. When the update completes, open a new browser tab and go to your domain with the `www` subdomain.

You should see your static web app in the browser. Inspect the location to verify that your site is served securely using `https`.


# Apex Domain External

# Set up an apex domain in Azure Static Web Apps

Domain names without a subdomain are known as apex or root domains. For example, the domain `www.example.com` is the `www` subdomain joined with the `example.com` apex domain.

Some domain registrars (like Google and GoDaddy) don't allow you to point the apex domain to an existing URL. If your registrar doesn't support `ALIAS` or `ANAME` records, or doesn't allow `CNAME` flattening, consider the following options:

* Configure your domain with [Azure DNS](custom-domain.md)

* Forward the apex domain to the `www` subdomain

* Use an `A` record

Using an `A` record directs your traffic to a single regional host of your static web app. When enabled, your static web app no longer benefits from its global distribution, and this may affect your application performance. Consider using `ALIAS`, `ANAME` or `CNAME` record for APEX domains for the best performance.

This guide demonstrates three options for configuring an apex domain.

* Use the steps to [set up with an ALIAS record](#set-up-with-an-alias-record) if your domain registrar supports the `ALIAS` DNS record.

If your registrar doesn't support `ALIAS` records, but does support `ANAME` records or `CNAME` flattening, see their documentation for configuration settings.

* Use the steps in [forward to www subdomain](#forward-to-www-subdomain) if your domain registrar doesn't support the `ALIAS` DNS record.

* Use the steps to [set up with an A Record](#set-up-with-an-a-record) if the above options do not suit you. With an `A` record, your traffic is directed to a single Static Web Apps host, and your app no longer benefit from the performance improvements provided by global distribution.

> [!NOTE]

> `CNAME` record maps a domain name to another domain (or subdomain) whereas `A` record maps a domain name to an IP address. If the IP address changes, a `CNAME` entry is still valid, unlike `A` record.

> [!NOTE]

> Apex domain changes can take up to 72 hours to propagate.

## Set up with an ALIAS record

Before you create the `ALIAS` record, you first need to validate that you own the domain.

### Validate ownership

1. Open the [Azure portal](https://portal.azure.com).

1. Go to your static web app.

1. From the *Overview* window, copy the generated **URL** of your site and set it aside in a text editor for future use.

1. Under *Settings*, select **Custom domains**.

2. Select **+ Add**.

3. In the *Enter domain* tab, enter your apex domain name.

For instance, if your domain name is `example.com`, enter `example.com` into this box (without any subdomains).

4. Select **Next**.

5. In the *Validate + Configure* tab, enter the following values.

| Setting | Value |

|---|---|

| Domain name | This value should match the domain name you entered in the previous step. |

| Hostname record type | Select **TXT**. |

6. Select **Generate code**.

Wait as the code is generated. It make take a minute or so to complete.

7. Once the `TXT` record value is generated, **copy** (next to the generated value) the code to the clipboard.

8. Select **Close**.

9. Open a new browser tab and sign in to your domain registrar account.

10. Go to your domain name's DNS configuration settings.

11. Add a new `TXT` record with the following values.

| Setting | Value |

|--|--|

| Type | `TXT` |

| Host | Enter **@** |

| Value | Paste the generated code value you copied from the Azure portal. |

| TTL (if applicable) | Leave as default value. |

12. Save changes to your DNS record.

### Set up an ALIAS record

1. Return to your domain name's DNS configuration settings.

1. Add a new `ALIAS` record with the following values.

| Setting | Value |

|--|--|

| Type | `ALIAS` |

| Host | Enter **@** |

| Value | Paste the generated URL you copied from the Azure portal. Make sure to remove the `https://` prefix from your URL. |

| TTL (if applicable) | Leave as default value. |

1. Save changes to your DNS record.

Since DNS settings need to propagate, this process can take some time to complete.

1. Open a new browser tab and go to your apex domain.

After the DNS records are updated, you should see your static web app in the browser. Also, inspect the location to verify that your site is served securely using `https`.

## Forward to www subdomain

Each domain registrar has a different process for managing domain names. Once you sign in to your account with your registrar, look for domain forwarding options. Some registrars have this functionality listed under *DNS options*, while others have them associated with *Website options*.

Make sure as you set up forwarding that you only configure the apex domain to forward to the `www` subdomain.

See your registrar's documentation for details.

## Set up with an A record

Before you create the `A` record, you first need to validate that you own the domain.

### Validate ownership

1. Open the [Azure portal](https://portal.azure.com).

1. Go to your static web app.

1. From the *Overview* window in the top right corner of the *Essentials* section, select **JSON View**.

1. Copy the value of the **`stableInboundIP`** property and set it aside in a text editor for future use. This is the IP address of your regional Static Web Apps host.

1. Under Settings, select Custom domains.

1. Select **+ Add**.

1. In the *Enter domain* tab, enter your apex domain name.

For instance, if your domain name is `example.com`, enter `example.com` into this box (without any subdomains).

1. Select **Next**.

1. In the *Validate + Configure* tab, enter the following values.

| Setting | Value |

|---|---|

| Domain name | This value should match the domain name you entered in the previous step. |

| Hostname record type | Select **TXT**. |

1. Select **Generate code**.

Wait as the code is generated. It make take a minute or so to complete.

1. Once the `TXT` record value is generated, **copy** (next to the generated value) the code to the clipboard.

1. Select **Close**.

1. Open a new browser tab and sign in to your domain registrar account.

1. Go to your domain name's DNS configuration settings.

1. Add a new `TXT` record with the following values.

| Setting | Value |

|--|--|

| Type | `TXT` |

| Host | Enter **@** |

| Value | Paste the generated code value you copied from the Azure portal. |

| TTL (if applicable) | Leave as default value. |

1. Save changes to your DNS record.

### Set up an A record

1. Return to your domain name's DNS configuration settings.

1. Add a new `A` record with the following values.

| Setting | Value |

|--|--|

| Type | `A` |

| Host | Enter **@** |

| Value | Paste the **`stableInboundIP`** you copied from the Azure portal.  |

| TTL (if applicable) | Leave as default value. |

1. Save changes to your DNS record.

Since DNS settings need to propagate, this process can take some time to complete.

1. Open a new browser tab and go to your apex domain.

After the DNS records are updated, you should see your static web app in the browser. Also, inspect the location to verify that your site is served securely using `https`.

## Next steps

> [!div class="nextstepaction"]

> [Manage the default domain](custom-domain-default.md)


# Custom Domain Default

# Manage the default domain in Azure Static Web Apps

Your static web app can be accessed using its automatically generated domain and any custom domains that you've configured. Optionally, you can configure your app to redirect all traffic to a default domain.

## Set a default domain

When you designate a custom domain as your app's default domain, requests to other domains are automatically redirected to the default domain. Only one custom domain can be set as the default.

Follow the below steps to set a custom domain as default.

1. With your static web app opened in the Azure portal, select **Custom domains** in the menu.

1. Select the custom domain you want to configure as the default domain.

1. Select **Set default**.

1. After the operation completes, refresh the table to confirm your domain is marked as "default".

## Unset a default domain

To stop domains redirecting to a default domain, follow the below steps.

1. With your static web app opened in the Azure portal, select **Custom domains** in the menu.

1. Select the custom domain you configured as the default.

1. Select **Unset default**.

1. After the operation completes, refresh the table to confirm that no domains are marked as "default".

## Next steps

> [!div class="nextstepaction"]

> [Configure app settings](authentication-authorization.yml)


# Apis Functions

# API support in Azure Static Web Apps with Azure Functions

Front end web applications often call back-end APIs for data and services. By default, Azure Static Web Apps provides built-in serverless API endpoints via [Azure Functions](apis-functions.md).

Azure Functions APIs in Static Web Apps are available in two possible configurations depending on the [hosting plan](plans.md#features):

- **Managed functions**:  By default, the API of a static web app is an Azure Functions application managed and deployed by Azure Static Web Apps associated with some restrictions.

- **Bring your own functions**: Optionally, you can [provide an existing Azure Functions application](functions-bring-your-own.md) of any plan type, which includes all the features of Azure Functions. With this configuration, you're responsible to handle a separate deployment for the Functions app.

The following table contrasts the differences between using managed and existing functions.

| Feature | Managed Functions | Bring your own Functions |

|---|---|---|

| Access to Azure Functions [triggers and bindings](../azure-functions/functions-triggers-bindings.md#supported-bindings) | HTTP only | All |

| Supported Azure Functions [runtimes](../azure-functions/supported-languages.md#languages-by-runtime-version)<sup>1</sup> | See [supported languages and runtimes](languages-runtimes.md#api). | All |

| Supported Azure Functions [hosting plans](../azure-functions/functions-scale.md) | Consumption | Consumption<br>Premium<br>Dedicated |

| [Integrated security](user-information.md) with direct access to user authentication and role-based authorization data | ✔ | ✔ |

| [Routing integration](./configuration.md?#routes) that makes the `/api` route available to the web app securely without requiring custom CORS rules. | ✔ | ✔ |

| [Durable Functions](../durable-task/durable-functions/durable-functions-overview.md) programming model | ✕ | ✔ |

| [Managed identity](../app-service/overview-managed-identity.md) | ✕ | ✔ |

| [Azure App Service Authentication and Authorization](../app-service/configure-authentication-provider-aad.md) token management | ✕ | ✔ |

| API functions available outside Azure Static Web Apps | ✕ | ✔ |

| [Key Vault references](../app-service/app-service-key-vault-references.md) | ✕ | ✔ |

<sup>1</sup> To specify the runtime version in managed functions, add a configuration file to your frontend app and set the [`apiRuntime` property](configuration.md#platform). Support is subject to the [Azure Functions language runtime support policy](../azure-functions/language-support-policy.md).

[!INCLUDE [APIs overview](../../includes/static-web-apps-apis-overview.md)]

## Configuration

API endpoints are available to the web app through the `api` route.

| Managed functions | Bring your own functions |

|---|---|

| While the `/api` route is fixed, you have control over the source code folder location of the managed functions app. You can change this location by [editing the workflow YAML file](build-configuration.md) located in your repository's _.github/workflows_ folder. | Requests to the `/api` route are sent to your existing Azure Functions app. |

## Troubleshooting and logs

Logs are only available if you add [Application Insights](monitor.md).

| Managed functions | Bring your own functions |

|---|---|

| Turn on logging by enabling Application Insights on your static web app. | Turn on logging by enabling Application Insights on your Azure Functions app. |

## Constraints

In addition to the Static Web Apps API [constraints](apis-overview.md#constraints), the following restrictions are also applicable to Azure Functions APIs:

| Managed functions | Bring your own functions |

|---|---|

| <ul><li>Triggers and bindings are limited to [HTTP](../azure-functions/functions-bindings-http-webhook.md).</li><li>The Azure Functions app must either be in Node.js 12, Node.js 14, Node.js 16, Node.js 18, Node.js 20 (preview), .NET Core 3.1, .NET 6.0, .NET 7.0, .NET 8.0, Python 3.8, Python 3.9, or Python 3.10.</li><li>Some application settings are managed by the service, therefore the following prefixes are reserved by the runtime:<ul><li>*APPSETTING\_, AZUREBLOBSTORAGE\_, AZUREFILESSTORAGE\_, AZURE_FUNCTION\_, CONTAINER\_, DIAGNOSTICS\_, DOCKER\_, FUNCTIONS\_, IDENTITY\_, MACHINEKEY\_, MAINSITE\_, MSDEPLOY\_, SCMSITE\_, SCM\_, WEBSITES\_, WEBSITE\_, WEBSOCKET\_, AzureWeb*</li></ul></li><li>Some application tags are internally used by the service. Therefore, the following tags are reserved:<ul><li> *AccountId, EnvironmentId, FunctionAppId*.</li></ul></li></ul> | <ul><li>You're responsible to manage the Functions app deployment.</li></ul> |

## Next steps

> [!div class="nextstepaction"]

> [Add an API](add-api.md)


# Add Api

# Add an API to Azure Static Web Apps with Azure Functions

You can add serverless APIs to Azure Static Web Apps powered by Azure Functions. This article demonstrates how to add and deploy an API to an Azure Static Web Apps site.

> [!NOTE]

> The functions provided by default in Static Web Apps are pre-configured to provide secure API endpoints and only support HTTP-triggered functions. See [API support with Azure Functions](apis-functions.md) for information on how they differ from standalone Azure Functions apps.

## Prerequisites

- Azure account with an active subscription.

- If you don't have an account, you can [create one for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- [Visual Studio Code](https://code.visualstudio.com/).

- [Azure Static Web Apps extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurestaticwebapps) for Visual Studio Code.

- [Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions) for Visual Studio Code.

- [Node.js v18](https://nodejs.org/en/download) to run the frontend app and API.

> [!TIP]

> You can use the [nvm](https://github.com/nvm-sh/nvm/blob/master/README.md) tool to manage multiple versions of Node.js on your development system.

> On Windows, [NVM for Windows](https://github.com/coreybutler/nvm-windows/blob/master/README.md) can be installed via Winget.

## Create the static web app

Before adding an API, create and deploy a frontend application to Azure Static Web Apps by following the [Building your first static site with Azure Static Web Apps](getting-started.md) quickstart.

Once you have a frontend application deployed to Azure Static Web Apps, [clone your app repository](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository). For example, you can clone your repository using the `git` command line.

Before you run the following command, make sure to replace `<YOUR_GITHUB_USERNAME>` with your GitHub username.

```bash

git clone https://github.com/<YOUR_GITHUB_USERNAME>/my-first-static-web-app

```

In Visual Studio Code, open the root of your app's repository. The folder structure contains the source for your frontend app and the Static Web Apps GitHub workflow in _.github/workflows_ folder.

```Files

├── .github

│   └── workflows

│       └── azure-static-web-apps-<DEFAULT_HOSTNAME>.yml

│

└── (folders and files from your static web app)

```

## Create the API

You create an Azure Functions project for your static web app's API. By default, the Static Web Apps Visual Studio Code extension creates the project in a folder named _api_ at the root of your repository.

1. Press <kbd>F1</kbd> to open the Command Palette.

1. Select **Azure Static Web Apps: Create HTTP Function...**. If you're prompted to install the Azure Functions extension, install it and rerun this command.

1. When prompted, enter the following values:

| Prompt | Value |

| --- | --- |

| Select a language | **JavaScript** |

| Select a programming model | **V4** |

| Provide a function name | **message** |

> [!TIP]

> You can learn more about the differences between programming models in the [Azure Functions developer guide](/azure/azure-functions/functions-reference)

An Azure Functions project is generated with an HTTP-triggered function. Your app now has a project structure similar to the following example.

```Files

├── .github

│   └── workflows

│       └── azure-static-web-apps-<DEFAULT_HOSTNAME>.yml

│

├── api

│   ├── src

│   │   ├── functions

│   │   │   └── message.js

│   │   └── index.js

│   ├── .funcignore

│   ├── host.json

│   ├── local.settings.json

│   ├── package-lock.json

│   └── package.json

│

└── (...plus other folders and files from your static web app)

```

1. Next, change the `message` function to return a message to the frontend. Update the function in _src/functions/message.js_ with the following code.

```javascript

const { app } = require('@azure/functions');

app.http('message', {

methods: ['GET', 'POST'],

authLevel: 'anonymous',

handler: async (request, context) => {

return { body: JSON.stringify({ "text": `Hello, from the API!` }) };

}

});

```

> [!TIP]

> You can add more API functions by running the **Azure Static Web Apps: Create HTTP Function...** command again.

## Update the frontend app to call the API

Update your frontend app to call the API at `/api/message` and display the response message.

If you used the quickstarts to create the app, use the following instructions to apply the updates.

# [No Framework](#tab/vanilla-javascript)

Update the content of the _src/index.html_ file with the following code to fetch the text from the API function and display it on the screen.

```html

<!DOCTYPE html>

<html lang="en">

<head>

<meta charset="UTF-8">

<meta name="viewport" content="width=device-width, initial-scale=1.0">

<link rel="stylesheet" href="styles.css">

<title>Vanilla JavaScript App</title>

</head>

<body>

<main>

<h1>Vanilla JavaScript App</h1>

<p>Loading content from the API: <b id="name">...</b></p>

</main>

<script>

(async function() {

const { text } = await (await fetch(`/api/message`)).json();

document.querySelector('#name').textContent = text;

}());

</script>

</body>

</html>

```

# [Angular](#tab/angular)

1. Update the content of _src/app/app.module.ts_ with the following code to enable `HttpClient` in your app.

```typescript

import { BrowserModule } from "@angular/platform-browser";

import { NgModule } from "@angular/core";

import { HttpClientModule } from '@angular/common/http';

import { AppComponent } from "./app.component";

@NgModule({

declarations: [AppComponent],

imports: [BrowserModule, HttpClientModule],

bootstrap: [AppComponent]

})

export class AppModule {}

```

1. Update the content of _src/app/app.component.ts_ with the following code to fetch the text from the API function and display it on the screen.

```typescript

import { HttpClient } from '@angular/common/http';

import { Component } from '@angular/core';

@Component({

selector: 'app-root',

template: `<div>{{message}}</div>`,

})

export class AppComponent {

message = '';

constructor(private http: HttpClient) {

this.http.get('/api/message')

.subscribe((resp: any) => this.message = resp.text);

}

}

```

# [React](#tab/react)

Update the content of _src/App.js_ with the following code to fetch the text from the API function and display it on the screen.

```javascript

import React, { useState, useEffect } from 'react';

function App() {

const [data, setData] = useState('');

useEffect(() => {

(async function () {

const { text } = await (await fetch(`/api/message`)).json();

setData(text);

})();

});

return <div>{data}</div>;

}

export default App;

```

# [Vue](#tab/vue)

Update the content of _src/App.vue_ with the following code to fetch the text from the API function and display it on the screen.

```javascript

<template>

<div>{{ message }}</div>

</template>

<script>

export default {

name: "App",

data() {

return {

message: ""

};

},

async mounted() {

const { text } = await (await fetch("/api/message")).json();

this.message = text;

}

};

</script>

```

---

## Run the frontend and API locally

To run your frontend app and API together locally, Azure Static Web Apps provides a CLI that emulates the cloud environment. The CLI uses the Azure Functions Core Tools to run the API.

### Install command line tools

Ensure you have the necessary command line tools installed.

[!INCLUDE [Required version](includes/static-web-apps-cli-required-version.md)]

```bash

npm install -g @azure/static-web-apps-cli

```

> [!TIP]

> If you don't want to install the `swa` command line globally, you can use `npx swa` instead of `swa` in the following instructions.

### Build frontend app

If your app uses a framework, build the app to generate the output before running the Static Web Apps CLI.

# [No Framework](#tab/vanilla-javascript)

There's no need to build the app.

# [Angular](#tab/angular)

Install npm dependencies and build the app into the _dist/angular-basic_ folder.

```bash

npm install

npm run build --prod

```

# [React](#tab/react)

Install npm dependencies and build the app into the _build_ folder.

```bash

npm install

npm run build

```

# [Vue](#tab/vue)

Install npm dependencies and build the app into the _dist_ folder.

```bash

npm install

npm run build

```

---

### Run the application locally

Run the frontend app and API together by starting the app with the Static Web Apps CLI. Running the two parts of your application this way allows the CLI to serve your frontend's build output from a folder, and makes the API accessible to the running app.

1. In the root of your repository, start the Static Web Apps CLI with the `start` command. Adjust the arguments if your app has a different folder structure.

# [No Framework](#tab/vanilla-javascript)

Pass the current folder (`src`) and the API folder (`api`) to the CLI.

```bash

swa start src --api-location api

```

# [Angular](#tab/angular)

Pass the build output folder (`dist/angular-basic`) and the API folder (`api`) to the CLI.

```bash

swa start dist/angular-basic --api-location api

```

# [React](#tab/react)

Pass the build output folder (`build`) and the API folder (`api`) to the CLI.

```bash

swa start build --api-location api

```

# [Vue](#tab/vue)

Pass the build output folder (`dist`) and the API folder (`api`) to the CLI.

```bash

swa start dist --api-location api

```

---

1. Windows Firewall might prompt you to allow the Azure Functions runtime to access the Internet. Select **Allow**.

1. When the CLI processes start, access your app at `http://localhost:4280/`. Notice how the page calls the API and displays its output, `Hello from the API`.

1. To stop the CLI, type <kbd>Ctrl + C</kbd>.

## Add API location to workflow

Before you can deploy your app to Azure, update your repository's GitHub Actions workflow with the correct location of your API folder.

1. Open your workflow at _.github/workflows/azure-static-web-apps-\<DEFAULT-HOSTNAME>.yml_.

1. Search for the property `api_location` and set the value to `api`.

```yaml

###### Repository/Build Configurations - These values can be configured to match your app requirements. ######

# For more information regarding Static Web App workflow configurations, please visit: https://aka.ms/swaworkflowconfig

app_location: "src" # App source code path

api_location: "api" # Api source code path - optional

output_location: "" # Built app content directory - optional

###### End of Repository/Build Configurations ######

```

**Note**: The above values of `api_location`, `app_location`, `output_location` apply to apps without a framework. These values may vary depending on your framework.

1. Save the file.

## Deploy changes

To publish changes to your static web app in Azure, commit and push your code to the remote GitHub repository.

1. Press <kbd>F1</kbd> to open the Command Palette.

1. Select the **Git: Commit All** command.

1. When prompted for a commit message, enter **feat: add API** and commit all changes to your local git repository.

1. Press <kbd>F1</kbd> to open the Command Palette.

1. Select the **Git: push** command.

Your changes are pushed to the remote repository in GitHub, triggering the Static Web Apps GitHub Actions workflow to build and deploy your app.

1. Open your repository in GitHub to monitor the status of your workflow run.

1. When the workflow run completes, visit your static web app to view your changes.

## Next steps

> [!div class="nextstepaction"]

> [Configure app settings](./application-settings.yml)


# Functions Bring Your Own

# Bring your own functions to Azure Static Web Apps

Azure Static Web Apps provides API integration to allow you to build front end web applications that depend on backend APIs for data and services. The two API integration options are: managed functions and bring your own backends. For more information on the differences between these options, see the [overview](apis-functions.md).

This article demonstrates how to link an existing Azure Functions app to an Azure Static Web Apps resource.

> [!NOTE]

> The integration with Azure Functions requires the Static Web Apps Standard plan.

>

> Backend integration is not supported on Static Web Apps [pull request environments](review-publish-pull-requests.md).

## Prerequisites

To link a function app to your static web app, you need to have an existing Azure Functions resource and a static web app.

| Resource | Description |

|---|---|

| [Azure Functions](/azure/azure-functions/functions-get-started) | If you don't already have one, follow the steps in the [Getting started with Azure Functions](/azure/azure-functions/functions-get-started) guide. |

| [Existing static web app](getting-started.md) | If you don't already have one, follow the steps in the [getting started](getting-started.md) guide to create a *No Framework* static web app. |

## Example

Consider an existing Azure Functions app that exposes an endpoint via the following location.

```url

https://my-functions-app.azurewebsites.net/api/getProducts

```

Once linked, you can access that same endpoint through the `api` path from your static web app, as shown in this example URL.

```url

https://red-sea-123.azurestaticapps.net/api/getProducts

```

Both endpoint URLs point to the same function. The endpoint on the function app must have the `/api` prefix, since Static Web Apps matches requests made to `/api` and proxies the entire path to the linked resource.

## Link an existing Azure Functions app

### Remove managed functions from your Static Web Apps resource (if present)

Before you associate an existing Functions app, you first need to adjust the configuration of your static web app to remove managed functions if you have any.

1. Set `api_location` value to an empty string (`""`) in the [workflow configuration](./build-configuration.md) file.

### Link the Azure Functions app to the Static Web Apps resource

1. Open your Static Web Apps instance in the [Azure portal](https://portal.azure.com).

1. From the _Settings_ menu, select **APIs**.

1. From the _Production_ row, select **Link** to open the *Link new Backend* window.

Enter the following settings.

| Setting | Value |

|--|--|

| Backend resource type | Select **Function App**. |

| Subscription | Select your Azure subscription name. |

| Resource name | Select the Azure Functions app name. |

| Backend slot | Select the slot name for the Azure Function. |

1. Select **Link**.

The Azure Functions app is now mapped to the `/api` route of your static web app.

> [!IMPORTANT]

> Make sure to set the `api_location` value to an empty string (`""`) in the [workflow configuration](./build-configuration.md) file before you link an existing Functions application. Also, calls assume that the external function app retains the default `api` route prefix. Many apps remove this prefix in the *host.json*. Make sure the prefix is in place in the configuration, otherwise the call fails.

## Deployment

You're responsible for setting up a [deployment workflow](../azure-functions/functions-deployment-technologies.md) for your Azure Functions app.

## Unlink an Azure Functions app

### Unlink Functions app from Static Web Apps

To unlink a function app from a static web app, follow these steps:

1. In the Azure portal, go to the static web app.

1. Select **APIs** from the navigation menu.

1. Locate the environment that you want to unlink and select the function app name.

1. Select **Unlink**.

When the unlinking process is complete, requests to routes beginning with `/api` are no longer proxied to your Azure Functions app.

> [!NOTE]

> To prevent accidentally exposing your function app to anonymous traffic, the identity provider created by the linking process is not automatically deleted. You can delete the identity provider named *Azure Static Web Apps (Linked)* from the function app's authentication settings.

### Remove authentication from the Azure Functions resource

To enable your Azure Functions app to receive anonymous traffic, follow these steps to remove the identity provider:

1. In the Azure portal, navigate to the Azure Functions resource.

1. Select **Authentication** from the navigation menu.

1. From the list of **Identity providers**, delete the identity provider related to the Static Web Apps resource.

1. Select **Remove authentication** to remove authentication and allow anonymous traffic to your Azure Functions resource.

Your function app is now able to receive anonymous traffic.

## Security constraints

- **Authentication and authorization:** If authentication and authorization policies aren't already set up on your existing Functions app, then the static web app has exclusive access to the API. To make your Functions app accessible to other applications, add another identity provider or change the security settings to allow unauthenticated access.

> [!NOTE]

> If you enable authentication and authorization in your linked Functions app, it must use Azure App Service Authentication and authorization provider version 2.

- **Required public accessibility:** An existing Functions app needs to not apply the following security configurations.

- Restricting the IP address of the Functions app.

- Restricting traffic through private link or service endpoints.

- **Function access keys:** If your function requires an [access key](../azure-functions/security-concepts.md#function-access-keys), then you must provide the key with calls from the static app to the API.

## Restrictions

- Only one Azure Functions app is available to a single static web app.

- The `api_location` value in the [workflow configuration](./build-configuration.md) must be set to an empty string.

- Not supported in Static Web Apps pull request environments.

- While your Azure Functions app may respond to various triggers, the static web app can only access functions via HTTP endpoints.

## Next steps

> [!div class="nextstepaction"]

> [Add an API](add-api.md)


# Apis Api Management

# API support in Azure Static Web Apps with Azure API Management

[Azure API Management](../api-management/api-management-key-concepts.md) is a service that allows you to create a modern API gateway for existing back end services.

When you link your Azure API Management service to your static web app, any requests to your static web app with a route that starts with `/api` are proxied to the same route in the Azure API Management service.

An Azure API Management service can be linked to multiple static web apps at the same time. An API Management product is created for each linked static web app. Any APIs added to the product is available to the associated static web app.

All Azure API Management pricing tiers are available for use with Azure Static Web Apps.

[!INCLUDE [APIs overview](../../includes/static-web-apps-apis-overview.md)]

> [!NOTE]

> The integration with Azure API Management requires the Static Web Apps Standard plan.

>

> Backend integration is not supported on Static Web Apps [pull request environments](review-publish-pull-requests.md).

## Prerequisites

To link an API management instance to your static web app, you need to have an existing Azure API Management resource and a static web app.

| Resource | Description |

|---|---|

| [Azure API Management](/azure/api-management/get-started-create-service-instance) | If you don't already have one, follow the steps in the [Create a new Azure API Management service instance](/azure/api-management/get-started-create-service-instance) guide. |

| [Existing static web app](getting-started.md) | If you don't already have one, follow the steps in the [getting started](getting-started.md) guide to create a *No Framework* static web app. |

## Example

Consider an existing Azure API Management instance that exposes an endpoint via the following location.

```url

https://my-api-management-instance.azure-api.net/api/getProducts

```

Once linked, you can access that same endpoint through the `api` path from your static web app, as shown in this example URL.

```url

https://red-sea-123.azurestaticapps.net/api/getProducts

```

Both URLs point to the same API endpoint. The endpoint on the API Management instance must have the `/api` prefix, since Static Web Apps matches requests made to `/api` and proxies the entire path to the linked resource.

## Link an Azure API Management service

### Link the API Management instance to Static Web Apps

To link an Azure API Management service as the API backend for a static web app, follow these steps:

1. In the Azure portal, go to the static web app.

1. Select **APIs** from the navigation menu.

1. Locate the environment you want to link the API Management service to. Select **Link**.

1. In *Backend resource type*, select **API Management**.

1. In *Subscription*, select the subscription containing the Azure API Management service you want to link.

1. In *Resource name*, select the Azure API Management service.

1. Select **Link**.

> [!IMPORTANT]

> When the linking process is complete, requests to routes beginning with `/api` are proxied to your Azure API Management service. However, no APIs are exposed by default. See [Configure APIs to receive requests](#configure-apis-to-receive-requests) to configure an API Management product to allow the APIs you want to use.

### Configure APIs to receive requests

Azure API Management has a *products* feature that defines how APIs are surfaced. As part of the linking process, your API Management service is configured with a product named `Azure Static Web Apps - <STATIC_WEB_APP_AUTO_GENERATED_HOSTNAME> (Linked)`.

To make APIs available to your linked static web app, [add them to the product](../api-management/api-management-howto-add-products.md#add-apis-to-a-product).

1. Within the API Management instance in the portal, select the **Products** tab.

1. Select the `Azure Static Web Apps - <STATIC_WEB_APP_AUTO_GENERATED_HOSTNAME> (Linked)` product.

1. Select **+ Add API**.

1. Select the APIs you want to expose from your Static Web Apps, then select the **Select** link.

The linking process also automatically applies the following configuration to your API Management service:

* The product associated with the linked static web app is configured to require a subscription.

* An API Management subscription named `Generated for Static Web Apps resource with default hostname: <STATIC_WEB_APP_AUTO_GENERATED_HOSTNAME>` is created and scoped to the product with the same name.

* An inbound *validate-jwt* policy is added to the product to allow only requests that contain a valid access token from the linked static web app.

* The linked static web app is configured to include the subscription's primary key and a valid access token when proxying requests to the API Management service.

> [!IMPORTANT]

> Changing the *validate-jwt* policy or regenerating the subscription's primary key prevents your static web app from proxying requests to the API Management service. Do not modify or delete the subscription or product associated with your static web app while they are linked.

## Unlink an Azure API Management service

To unlink an Azure API Management service from a static web app, follow these steps:

1. In the Azure portal, go to the static web app.

1. Locate the environment that you want to unlink and select the API Management service name.

1. Select **Unlink**.

When the unlinking process is complete, requests to routes beginning with `/api/` are no longer proxied to your API Management service.

> [!NOTE]

> The API Management product and subscription associated with the linked static web app are not automatically deleted. You can delete them from the API Management service.

## Troubleshooting

If the APIs aren't associated to the API Management *product* created for the Static Web Apps resource, accessing a `/api` route in your static web app returns the following error from API management.

```json

{

"statusCode": 401,

"message": "Access denied due to invalid subscription key. Make sure to provide a valid key for an active subscription."

}

```

To resolve this error, configure the APIs you want to expose within your Static Web Apps to the product created for it, as detailed in the [Configure APIs to receive requests](#configure-apis-to-receive-requests) section.

## Next steps

> [!div class="nextstepaction"]

> [API overview](apis-overview.md)


# Apis App Service

# API support in Azure Static Web Apps with Azure App Service

[Azure App Service](../app-service/overview.md) is a managed platform for hosting web applications that execute code on servers. Azure App Service supports many runtimes and frameworks including Node.js, ASP.NET Core, PHP, Java, and Python.

When you link your Azure App Service web app to your static web app, any requests to your static web app with a route that starts with `/api` are proxied to the same route on the Azure App Service app.

By default, when an App Service app is linked to a static web app, the App Service app only accepts requests that are proxied through the linked static web app. An Azure App Service app can only be linked to a single static web app at a time.

All Azure App Service hosting plans are available for use with Azure Static Web Apps.

[!INCLUDE [APIs overview](../../includes/static-web-apps-apis-overview.md)]

> [!NOTE]

> The integration with Azure App Service requires the Static Web Apps Standard plan.

>

> Backend integration is not supported on Static Web Apps [pull request environments](review-publish-pull-requests.md).

## Prerequisites

To link an App Service to your static web app, you need to have an existing App Service resource and a static web app.

| Resource | Description |

|---|---|

| [Azure App Service](/azure/app-service/quickstart-nodejs) | If you don't already have one, follow the steps in the [Create a web app in Azure

](/azure/app-service/quickstart-nodejs) guide. |

| [Existing static web app](getting-started.md) | If you don't already have one, follow the steps in the [getting started](getting-started.md) guide to create a *No Framework* static web app. |

## Example

Consider an existing Azure App Service instance that exposes an endpoint via the following location.

```url

https://my-web-app.azurewebsites.net/api/getProducts

```

Once linked, you can access that same endpoint through the `api` path from your static web app, as shown in this example URL.

```url

https://red-sea-123.azurestaticapps.net/api/getProducts

```

Both URLs point to the same API endpoint. The endpoint on the App Service must have the `/api` prefix, since Static Web Apps matches requests made to `/api` and proxies the entire path to the linked resource.

## Link an Azure App Service Web App

To link a web app as the API backend for a static web app, follow these steps:

1. In the Azure portal, go to the static web app.

1. Select **APIs** from the navigation menu.

1. Locate the environment you want to link the API Management instance to. Select **Link**.

1. In *Backend resource type*, select **Web App**.

1. In *Subscription*, select the subscription containing the Azure App Service app you want to link.

1. In *Resource name*, select the Azure App Service app.

1. Select **Link**.

When the linking process is complete, requests to routes beginning with `/api` are proxied to the linked App Service app.

### Manage access to Azure App Service

Your App Service app is configured with an identity provider named `Azure Static Web Apps (Linked)` that permits only traffic that is proxied through the static web app. To make your App Service app accessible to other applications, update its authentication configuration to add another identity provider or change the security settings to allow unauthenticated access.

## Unlink an Azure App Service app

### Unlink App Service from Static Web Apps

To unlink a web app from a static web app, follow these steps:

1. In the Azure portal, go to the static web app.

1. Select **APIs** from the navigation menu.

1. Locate the environment that you want to unlink and select the web app name.

1. Select **Unlink**.

When the unlinking process is complete, requests to routes beginning with `/api` are no longer proxied to your App Service app.

> [!NOTE]

> To prevent accidentally exposing your App Service app to anonymous traffic, the identity provider created by the linking process is not automatically deleted. You can delete the identity provider named *Azure Static Web Apps (Linked)* from the App Service app's authentication settings.

### Remove authentication from the App Service resource

To enable your App Service resource to receive anonymous traffic, follow these steps to remove the identity provider:

1. In the Azure portal, navigate to the App Service resource.

1. Select **Authentication** from the navigation menu.

1. From the list of **Identity providers**, delete the identity provider related to the Static Web Apps resource.

1. Select **Remove authentication** to remove authentication and allow anonymous traffic to your App Service resource.

Your App Service resource is now able to receive anonymous traffic.

## Next steps

> [!div class="nextstepaction"]

> [API overview](apis-overview.md)


# Apis Container Apps

# API support in Azure Static Web Apps with Azure Container Apps

[Azure Container Apps](../container-apps/overview.md) is a managed platform for hosting serverless containers and microservices.

When you link your container app to your static web app, any requests to your static web app with a route that starts with `/api` are proxied to the same route on the container app.

By default, when a container app is linked to a static web app, the container app only accepts requests that are proxied through the linked static web app. A container app can be linked to a single static web app at a time.

[!INCLUDE [APIs overview](../../includes/static-web-apps-apis-overview.md)]

> [!NOTE]

> The integration with Azure Container Apps requires the Static Web Apps Standard plan.

>

> Backend integration is not supported on Static Web Apps [pull request environments](review-publish-pull-requests.md).

## Prerequisites

To link a container app to your static web app, you need to have an existing Container Apps resource and a static web app.

| Resource | Description |

|---|---|

| [Azure Container Apps](/azure/container-apps/quickstart-portal) | If you don't already have one, follow the steps in the [Deploy your first container app](/azure/container-apps/quickstart-portal) guide. |

| [Existing static web app](getting-started.md) | If you don't already have one, follow the steps in the [getting started](getting-started.md) guide to create a *No Framework* static web app. |

## Example

Consider an existing Azure Container App instance that exposes an endpoint via the following location.

```url

https://my-container-app.red-river-123.eastus2.azurecontainerapps.io/api/getProducts

```

Once linked, you can access that same endpoint through the `api` path from your static web app, as shown in this example URL.

```url

https://red-sea-123.azurestaticapps.net/api/getProducts

```

Both URLs point to the same API endpoint. The endpoint on the container app must have the `/api` prefix, since Static Web Apps matches requests made to `/api` and proxies the entire path to the linked resource.

## Link a container app

To link a container app as the API backend for a static web app, follow these steps:

1. In the Azure portal, go to the static web app.

1. Select **APIs** from the navigation menu.

1. Locate the environment you want to link the API Management instance to. Select **Link**.

1. In *Backend resource type*, select **Container App**.

1. In *Subscription*, select the subscription containing the container app you want to link.

1. In *Resource name*, select the container app.

1. Select **Link**.

When the linking process is complete, requests to routes beginning with `/api` are proxied to the linked container app.

### Manage access to the container app

Your container app is configured with an identity provider named `Azure Static Web Apps (Linked)` that permits only traffic that is proxied through the static web app. To make your container app accessible to other applications, update its authentication configuration to add another identity provider or change the security settings to allow unauthenticated access.

## Unlink a container app

To unlink a container app from a static web app, follow these steps:

1. In the Azure portal, go to the static web app.

1. Select **APIs** from the navigation menu.

1. Locate the environment that you want to unlink and select the container app name.

1. Select **Unlink**.

When the unlinking process is complete, requests to routes beginning with `/api` are no longer proxied to your container app.

> [!NOTE]

> To prevent accidentally exposing your container app to anonymous traffic, the identity provider created by the linking process is not automatically deleted. You can delete the identity provider named *Azure Static Web Apps (Linked)* from the container app's authentication settings.

### Remove authentication from the Container Apps resource

To enable your Container Apps resource to receive anonymous traffic, follow these steps to remove the identity provider:

1. In the Azure portal, navigate to the Container Apps resource.

1. Select **Authentication** from the navigation menu.

1. From the list of **Identity providers**, delete the identity provider related to the Static Web Apps resource.

1. Select **Remove authentication** to remove authentication and allow anonymous traffic to your Container Apps resource.

Your Container Apps resource is now able to receive anonymous traffic.

## Next steps

> [!div class="nextstepaction"]

> [API overview](apis-overview.md)


# Database Overview

# Connecting to a database with Azure Static Web Apps (preview)

> [!IMPORTANT]

> Retirement notice: Database Connections for Static Web Apps ends November 30, 2025. Migrate now to avoid disruption.

The Azure Static Web Apps database connection feature allows you to access a database from your static web app without writing custom server-side code.

Once you create a connection between your web application and database, you can manipulate data with full support for CRUD operations, built-in authorization, and relationships.

Based on the [Data API builder](/azure/data-api-builder), Azure Static Web Apps takes REST and GraphQL requests and converts them to database queries.

Features supported by database connections include:

| Feature | Description |

|---|---|

| **Integrated security** | Built-in integration with Azure Static Web Apps authentication and authorization security model. The same role-based security used to secure routes is available for API endpoints. |

| **Full CRUD-based operations**  | Refer to the tutorials for [Azure Cosmos DB](database-azure-cosmos-db.md), [Azure SQL](database-azure-sql.md), [MySQL](database-mysql.md), or [PostgreSQL](database-postgresql.md) for an example on how to manipulate data in your application. |

| **Supports SQL and NoSQL** | You can use relational and document databases as your application's database. |

| **Serverless architecture** | Connections scale from 0 to 1 worker (during preview). |

| **Database relationships** | Supported only via the GraphQL  endpoint. |

| **CLI support** | Develop locally with the [Static Web Apps CLI](https://github.com/Azure/static-web-apps-cli). Use the `--data-api-location` option to handle requests to data APIs in development just as they're handled in the cloud. |

## Supported databases

The following table shows support for different relational and NoSQL databases.

| Name | Type | Description | REST | GraphQL |

|---|---|---|---|---|

| [Azure Cosmos DB](/azure/cosmos-db/distributed-nosql) | Standard | Globally distributed database platform for both NoSQL and relational databases of any scale.<br><br>In addition to the [standard configuration](database-configuration.md), a [`gql` schema file](/azure/data-api-builder/get-started/get-started-azure-cosmos-db#add-book-schema-file) is required for GraphQL endpoints. | | ✔ |

| [Azure SQL](/azure/azure-sql/azure-sql-iaas-vs-paas-what-is-overview?view=azuresql&preserve-view=true) | Standard | Family of managed, secure, and intelligent products that use the SQL Server database engine in the Azure cloud. | ✔ | ✔ |

| [Azure Database for MySQL](/azure/mysql/single-server/overview#azure-database-for-mysql---flexible-server) | Flex |  Relational database service in the Microsoft cloud based on the MySQL Community Edition | ✔ | ✔ |

| [Azure Database for PostgreSQL](/azure/postgresql/flexible-server/) | Flex | Fully managed PostgreSQL database-as-a-service that handles mission-critical workloads with predictable performance and dynamic scalability. | ✔ | ✔ |

| [Azure Database for PostgreSQL (single)](/azure/postgresql/single-server/overview-single-server) | Single | Fully managed PostgreSQL database. | ✔ | ✔ |

You can use the following connection types for database access:

- Connection string

- User-assigned Managed Identity

- System-assigned Managed Identity

## Endpoint location

Access to data endpoints are available off the `/data-api` path.

The following table shows you how requests route to different parts of a static web app:

| Path | Description |

|---|---|

| `example.com/api/*` | [API functions](add-api.md) |

| `example.com/data-api/*` | Database connection endpoints that support REST and GraphQL requests. |

| `example.com/*` | Static content |

When you configure database connections on your website, you can configure the REST or GraphQL suffix of the `/data-api/*` route. The `/data-api` prefix is a convention of Static Web Apps and can't be changed.

## Configuration

There are two steps to configuring a database connection in Static Web Apps. You need to connect your database to your static web app in the Azure portal, and update your database connections configuration file.

See [Database connection configuration in Azure Static Web Apps](database-configuration.md) for more detail.

## Local development

The Azure Static Web Apps CLI (SWA CLI) includes support for working with database connections during local development.

The CLI activates the local `/data-api` endpoint, and proxies requests from port `4280` to the appropriate port for database access.

Here's an example command that starts the SWA CLI with a database connection:

```bash

swa start ./src --data-api-location swa-db-connections

```

This command starts the SWA CLI in the *src* directory. The `--data-api-location` option tells the CLI that a folder named *swa-db-connections* holds the *[staticwebapp.database.config.json](https://github.com/MicrosoftDocs/data-api-builder-docs/blob/main/data-api-builder/)* file.

> [!NOTE]

> In development, if you use a connection string to authenticate, use the `env()` function to read a connection string from an environment variable. The string passed in to the `env` function must be surrounded by quotes.

## Role-based security

When you define an entity in the *staticwebapp.database.config.json* file, you can specify a list of roles required to access an entity endpoint.

The following [configuration](database-configuration.md) fragment requires the *admin* role to access all actions (`create`, `read`, `update`, `delete`) on the *orders* entity.

```json

{

...

"entities": {

"Orders": {

"source": "dbo.Orders",

"permissions": [

{

"actions": ["*"],

"role": "admin"

}

]

}

}

...

}

```

When you make calls to an endpoint that requires a role, the following conditions are required:

1. The current user must be authenticated.

1. The current user must be a member of the required role.

1. The REST or GraphQL request must include a header with the key of `X-MS-API-ROLE` and a value of the role name matching what's listed in the entity configuration rules.

For instance, the following snippet shows how to pass the *admin* role in a request header.

```javascript

{

method: "POST",

headers: {

"Content-Type": "application/json",

"X-MS-API-ROLE": "admin"

},

body: JSON.stringify(requestPayload)

}

```

## Constraints

- Databases must be accessible by Azure's infrastructure.

- During public preview, database connections scale from 0 to 1 database worker.

## Next steps

> [!div class="nextstepaction"]

> [Configure your database](database-configuration.md)


# Database Configuration

# Database connection configuration in Azure Static Web Apps (preview)

Azure Static Web apps database connections work with various Azure databases.

As you connect a database to your static web app, you need to configure your database's firewall to accept network access from the Static Web Apps workers by allowing network access from Azure resources. Allowing specific Static Web Apps IP addresses isn't supported.

If you're using the Managed Identity authentication type, then you need to configure your static web app's Managed Identity profile to access your database.

Use this table for details about firewall and Managed Identity configuration for your database.

| Name | Type | Firewall | Managed Identity |

|---|---|---|---|

| [Azure Cosmos DB](/azure/cosmos-db/distributed-nosql) | Standard | [Configure firewall](/azure/cosmos-db/how-to-configure-firewall#configure-ip-policy) | [Configure Managed Identity](/azure/cosmos-db/managed-identity-based-authentication) |

| [Azure SQL](/azure/azure-sql/azure-sql-iaas-vs-paas-what-is-overview?view=azuresql&preserve-view=true) | Standard | [Configure firewall](/azure/azure-sql/database/firewall-configure?view=azuresql&preserve-view=true#connections-from-inside-azure) | [Configure Managed Identity](/azure/azure-sql/database/authentication-azure-ad-user-assigned-managed-identity?view=azuresql&preserve-view=true) |

| [Azure Database for MySQL](/azure/mysql/single-server/overview#azure-database-for-mysql---flexible-server) | Flex | [Configure firewall](/azure/mysql/flexible-server/concepts-networking-public#allow-all-azure-ip-addresses) | Not supported |

| [Azure Database for PostgreSQL](/azure/postgresql/flexible-server/) | Flex | [Configure firewall](/azure/postgresql/flexible-server/concepts-networking#allowing-all-azure-ip-addresses) | Not supported |

| [Azure Database for PostgreSQL (single)](/azure/postgresql/single-server/overview-single-server) | Single | [Configure firewall](/azure/postgresql/single-server/concepts-firewall-rules#connecting-from-azure) | [Configure Managed Identity](https://techcommunity.microsoft.com/t5/azure-database-for-postgresql/connect-from-function-app-with-managed-identity-to-azure/ba-p/1517032) |

## Configuration

You define the runtime behavior of the database connection in the `staticwebapp.database.config.json` file. Before you link a database to your static web app, you need to create this file within your repository. By convention, this file exists in the *swa-db-connections* folder at the root of your repository, but you can [relocate](#custom-configuration-folder) it if you wish.

The purpose of the configuration file is to:

- Map paths off the `/data-api` endpoint to your database tables or entities

- Expose REST or GraphQL endpoints (or both)

- Define entity security rules

- Control development configuration settings

If you're using Azure Cosmos DB with GraphQL, you also need to provide a [`gql` schema file](/azure/data-api-builder/get-started/get-started-azure-cosmos-db#add-book-schema-file).

> [!NOTE]

> Static Web Apps database connections requires a folder containing the configuration files.  This folder must contain the *staticwebapp.database.config.json* configuration file for all database types. For Cosmos DB for NoSQL databases, a *staticwebapp.database.schema.gql* schema file is also required.

>

> By convention, this folder is named *swa-db-connections* and placed at the root of the repository. This convention can be overridden with a [custom-configuration-folder](#custom-configuration-folder).

## Sample configuration file

The following sample configuration file shows you how to connect to an Azure SQL database and expose both REST and GraphQL endpoints. For full details on the configuration file and its supported features, refer to the [Data API Builder documentation](/azure/data-api-builder/configuration-file).

```json

{

"$schema": "https://github.com/Azure/data-api-builder/releases/latest/download/dab.draft.schema.json",

"data-source": {

"database-type": "mssql",

"options": {

"set-session-context": false

},

"connection-string": "@env('DATABASE_CONNECTION_STRING')"

},

"runtime": {

"rest": {

"enabled": true,

"path": "/rest"

},

"graphql": {

"allow-introspection": true,

"enabled": true,

"path": "/graphql"

},

"host": {

"mode": "production",

"cors": {

"origins": ["http://localhost:4280"],

"allow-credentials": false

},

"authentication": {

"provider": "StaticWebApps"

}

}

},

"entities": {

"Person": {

"source": "dbo.MyTestPersonTable",

"permissions": [

{

"actions": ["create", "read", "update", "delete"],

"role": "anonymous"

}

]

}

}

}

```

| Property | Description |

|---|---|

| `$schema` | The version of the [Database API builder](/azure/data-api-builder/) used by Azure Static Web Apps to interpret the configuration file. |

| `data-source` | Configuration settings specific to the target database. The `database-type` property accepts `mssql`, `postgresql`, `cosmosdb_nosql`, or `mysql`.<br><br>The connection string is overwritten upon deployment when a database is connected to your Static Web Apps resource. During local development, the connection string defined in the configuration file is what is used to connect to the database.  |

| `runtime` | Section that defines the exposed endpoints. The `rest` and `graphql` properties control the URL fragment used to access the respective API protocol. The `host` configuration section defines settings specific to your development environment. Make sure the `origins` array include your localhost address and port. The host.mode is overwritten to `production` when a database is connected to your Static Web Apps resource. |

| `entities` | Section that maps URL path to database entities and tables. The same [role-based authentication rules](configuration.md#authentication) used to secure paths also secure database entities and can be used to define permissions for each entity. The entities object also specifies the relationships between entities. |

### Generate configuration file

The [Static Web Apps CLI](https://github.com/Azure/static-web-apps-cli) allows you to generate a configuration file stub.

[!INCLUDE [Required version](includes/static-web-apps-cli-required-version.md)]

Use the `swa db init --database-type <YOUR_DATABASE_TYPE>` to generate a configuration file. By default, the CLI creates a new *staticwebapp.database.config.json* in a folder named *swa-db-connections*.

Supported database types include:

- `mssql`

- `postgresql`

- `cosmosdb_nosql`

- `mysql`

### Custom configuration folder

The default folder name for the *staticwebapp.database.config.json* file is *swa-db-connections*. If you'd like to use a different folder, you need to update your workflow file to tell the static web apps runtime where to find your configuration file. The `data_api_location` property allows you to define the location of your configuration folder.

> [!NOTE]

> Folder that holds the *staticwebapp.database.config.json* file must be at the root of your static web apps repository.

The following code shows you how to use a folder named *db-config* for the database configuration file.

```yml

app_location: "/src"

api_location: "api"

output_location: "/dist"

data_api_location: "db-config" # Folder holding the staticwebapp.database.config.json file

```

## Configure database connectivity

Azure Static Web Apps must have network access to your database for database connections to work. Additionally, to use an Azure database for local development, you need to configure your database to allow requests from your own IP address. The following are generic steps that apply to all databases. For specific steps for your database type, refer to the above links.

- Go to your database in the [Azure portal](https://portal.azure.com).

- Go to the Networking tab.

- Under the Firewall rules section, select **Add your client IPv4 address**. This step ensures that you can use this database for your local development.

- Select the **Allow Azure services and resources to access this server** checkbox. This step ensures that your deployed Static Web Apps resource can access your database.

- Select **Save**.

## Connect a database

Linking a database to your static web app establishes the production connection between your website and database when published to Azure.

1. Open your static web app in the Azure portal.

1. In the *Settings* section, select **Database connection**.

1. Under the *Production* section, select the **Link existing database** link.

1. In the *Link existing database* window, enter the following values:

| Property | Value |

|---|---|

| Database Type | Select your database type from the dropdown list. |

| Subscription | Select your Azure subscription from the dropdown list. |

| Resource Name | Select the database server name that has your desired database. |

| Database Name | Select the name of the database you want to link to your static web app. |

| Authentication Type | Select the connection type required to connect to your database. |

## Related content

Add a database to your static web app using one of the following databases:

- [Azure Cosmos DB](database-azure-cosmos-db.md)

- [Azure SQL](database-azure-sql.md)

- [MySQL](database-mysql.md)

- [PostgreSQL](database-postgresql.md)

Additionally, you can learn about how to use the [Data API builder](/azure/data-api-builder/how-to-deploy-static-web-app

) with Azure Static Web Apps.


# Database Azure Cosmos Db

# Tutorial: Add an Azure Cosmos DB database connection in Azure Static Web Apps (preview)

In this tutorial, you learn how to connect an Azure Cosmos DB for NoSQL database to your static web app. Once configured, you can make GraphQL requests to the built-in `/data-api` endpoint to manipulate data without having to write backend code.

For the sake of simplicity, this tutorial shows you how to use an Azure database for local development purposes, but you may also use a local database server for your local development needs.

> [!NOTE]

> This tutorial shows how to use Azure Cosmos DB for NoSQL. If you would like to use another database, refer to the [Azure SQL](database-azure-sql.md), [MySQL](database-mysql.md), or [PostgreSQL](database-postgresql.md) tutorials.

In this tutorial, you learn to:

> [!div class="checklist"]

> * Link a Azure Cosmos DB for NoSQL database to your static web app

> * Create, read, update, and delete data

## Prerequisites

To complete this tutorial, you need to have an existing Azure Cosmos DB for NoSQL database and static web app.

| Resource | Description |

|---|---|

| [Azure Cosmos DB for NoSQL Database](/azure/cosmos-db/nosql/quickstart-portal) | If you don't already have one, follow the steps in the [Create an Azure Cosmos DB database](/azure/cosmos-db/nosql/quickstart-portal) guide. |

| [Existing static web app](getting-started.md) | If you don't already have one, follow the steps in the [getting started](getting-started.md) guide to create a *No Framework* static web app. |

Begin by configuring your database to work with the Azure Static Web Apps database connection feature.

## Configure database connectivity

Azure Static Web Apps must have network access to your database for database connections to work. Additionally, to use an Azure database for local development, you need to configure your database to allow requests from your own IP address.

1. Go to your Azure Cosmos DB for NoSQL account in the [Azure portal](https://portal.azure.com).

1. Under the *Settings* section, select **Networking**.

1. Under the *Public access* section, select **All networks**. This action allows you to use the cloud database for local development, that your deployed Static Web Apps resource can access your database, and that you can query your database from the portal.

1. Select **Save**.

## Get database connection string for local development

To use your Azure database for local development, you need to retrieve the connection string of your database. You may skip this step if you plan to use a local database for development purposes.

1. Go to your Azure Cosmos DB for NoSQL account in the [Azure portal](https://portal.azure.com).

1. Under the *Settings* section, select **Keys**.

1. From the *PRIMARY CONNECTION STRING* box, copy the connection string and set it aside in a text editor.

## Create sample data

Create a sample table and seed it with sample data to match the tutorial.

1. On the left-hand navigation window, select **Data Explorer**.

1. Select **New Container**. Enter the Database ID as `Create new`, and enter `MyTestPersonDatabase` as value.

1. Enter the Container ID of `MyTestPersonContainer`.

1. Enter a partition key of `id` (this value is prefixed with `/`).

1. Select **OK**.

1. Select the *MyTestPersonContainer* container.

1. Select its *Items*.

1. Select **New Item** and enter the following value:

```

{

"id": "1",

"Name": "Sunny"

}

```

## Configure the static web app

The rest of this tutorial focuses on editing your static web app's source code to make use of database connections locally.

> [!IMPORTANT]

> The following steps assume you are working with the static web app created in the [getting started guide](getting-started.md). If you are using a different project, make sure to adjust the following git commands to match your branch names.

1. Switch to the `main` branch.

```bash

git checkout main

```

1. Synchronize your local version with what's on GitHub by using `git pull`.

```bash

git pull origin main

```

### Create the database configuration file

Next, create the configuration file that your static web app uses to interface with the database.

1. Open your terminal and create a new variable to hold your connection string. The specific syntax may vary depending on the shell type you're using.

# [Bash](#tab/bash)

```bash

export DATABASE_CONNECTION_STRING='<YOUR_CONNECTION_STRING>'

```

# [PowerShell](#tab/powershell)

```powershell

$env:DATABASE_CONNECTION_STRING='<YOUR_CONNECTION_STRING>'

```

---

Make sure to replace `<YOUR_CONNECTION_STRING>` with the connections string value you set aside in a text editor.

1. Use npm to install or update the Static Web Apps CLI. Select which command is best for your situation.

To install, use `npm install`.

# [Bash](#tab/bash)

```bash

npm install -g @azure/static-web-apps-cli

```

# [PowerShell](#tab/powershell)

```powershell

npm install -g @azure/static-web-apps-cli

```

---

To update, use `npm update`.

# [Bash](#tab/bash)

```bash

npm update

```

# [PowerShell](#tab/powershell)

```powershell

npm update

```

---

1. Use the `swa db init` command to generate a database configuration file.

# [Bash](#tab/bash)

```bash

swa db init --database-type cosmosdb_nosql --cosmosdb_nosql-database MyTestPersonDatabase

```

# [PowerShell](#tab/powershell)

```powershell

swa db init --database-type cosmosdb_nosql --cosmosdb_nosql-database MyTestPersonDatabase

```

---

The `init` command creates the *staticwebapp.database.config.json* file in the *swa-db-connections* folder.

1. Paste in this sample schema into the *staticwebapp.database.schema.gql* file you generated.

Since Cosmos DB for NoSQL is a schema agnostic database, Azure Static Web Apps database connections can't extract the schema of your database. The *staticwebapp.database.schema.gql* file allows you to specify the schema of your Cosmos DB for NoSQL database for Static Web Apps.

```gql

type Person @model {

id: ID

Name: String

}

```

1. Paste in this sample configuration into file *staticwebapp.database.config.json* you generated. Notice that Cosmos DB for NoSQL has more options in the `data-source` object to indicate the Cosmos DB database and the schema file needed for database connections to understand the schema of the database.

```json

{

"$schema": "https://github.com/Azure/data-api-builder/releases/latest/download/dab.draft.schema.json",

"data-source": {

"database-type": "cosmosdb_nosql",

"options": {

"database": "MyTestPersonDatabase",

"schema": "staticwebapp.database.schema.gql"

},

"connection-string": "@env('DATABASE_CONNECTION_STRING')"

},

"runtime": {

"graphql": {

"allow-introspection": true,

"enabled": true,

"path": "/graphql"

},

"host": {

"mode": "production",

"cors": {

"origins": ["http://localhost:4280"],

"allow-credentials": false

},

"authentication": {

"provider": "StaticWebApps"

}

}

},

"entities": {

"Person": {

"source": "MyTestPersonContainer",

"permissions": [

{

"actions": ["*"],

"role": "anonymous"

}

]

}

}

}

```

Before moving on to the next step, review the following table that explains different aspects of the configuration file. For full documentation on the configuration file and functionality such as relationships and policies for item-level security, refer to [Data API Builder documentation](/azure/data-api-builder/configuration-file).

| Feature | Explanation |

|---|---|

| **Database connection** | In development, the runtime reads the connection string from the value of the connection string in the configuration file. While you can specify your connection string directly in the configuration file, a best practice is to store connection strings in a local environment variable. You can refer to environment variable values in the configuration file via the `@env('DATABASE_CONNECTION_STRING')` notation. The value of the connection string gets overwritten by Static Web Apps for the deployed site with the information collected when you connect your database. |

| **API endpoint** | The GraphQL endpoint is available through `/data-api/graphql` as configured in this configuration file. You may configure the GraphQL path, but the `/data-api` prefix isn't configurable. |

| **API Security** | The `runtime.host.cors` settings allow you to define allowed origins that can make requests to the API. In this case, the configuration reflects a development environment and allowlists the *http://localhost:4280* location. |

| **Entity model** | Defines the entities exposed via routes as types in the GraphQL schema. In this case, the name *Person*, is the name exposed to the endpoint while `entities.<NAME>.source` is the database schema and table mapping. Notice how the API endpoint name doesn't need to be identical to the table name. |

| **Entity security** | Permissions rules listed in the `entity.<NAME>.permissions` array control the authorization settings for an entity. You can secure an entity with roles in the same way you [secure routes with roles](./configuration.md#securing-routes-with-roles).  |

> [!NOTE]

> The configuration file's `connection-string`, `host.mode`, and `graphql.allow-introspection` properties are overwritten when you deploy your site. Your connection string is overwritten with the authentication details collected when you connect your database to your Static Web Apps resource. The `host.mode` property is set to `production`, and the `graphql.allow-introspection` is set to `false`. These overrides provide consistency in your configuration files across your development and production workloads, while ensuring your Static Web Apps resource with database connections enabled is secure and production-ready.

With the static web app configured to connect to the database, you can now verify the connection.

### Update home page

Replace the markup between the `body` tags in the *index.html* file with the following HTML.

```html

<h1>Static Web Apps Database Connections</h1>

<blockquote>

Open the console in the browser developer tools to see the API responses.

</blockquote>

<div>

<button id="list" onclick="list()">List</button>

<button id="get" onclick="get()">Get</button>

<button id="update" onclick="update()">Update</button>

<button id="create" onclick="create()">Create</button>

<button id="delete" onclick="del()">Delete</button>

</div>

<script>

// add JavaScript here

</script>

```

## Start the application locally

Now you can run your website and manipulate data in the database directly.

[!INCLUDE [Required version](includes/static-web-apps-cli-required-version.md)]

1. Use npm to install or update the Static Web Apps CLI. Select which command is best for your situation.

To install, use `npm install`.

```bash

npm install -g @azure/static-web-apps-cli

```

To update, use `npm update`.

```bash

npm update

```

1. Start the static web app with the database configuration.

```bash

swa start ./src --data-api-location swa-db-connections

```

Now that the CLI is started, you can access your database via the endpoints as defined in the *staticwebapp.database.config.json* file.

The `http://localhost:4280/data-api/graphql` endpoint accepts GraphQL queries and mutations.

## Manipulate data

The following framework-agnostic commands demonstrate how to do full CRUD operations on your database.

The output for each function appears in the browser's console window.

Open the developer tools by pressing <kbd>CMD/CTRL</kbd> + <kbd>SHIFT</kbd> + <kbd>I</kbd> and select the **Console** tab.

### List all items

Add the following code between the `script` tags in *index.html*.

```javascript

async function list() {

const query = `

{

people {

items {

id

Name

}

}

}`;

const endpoint = "/data-api/graphql";

const response = await fetch(endpoint, {

method: "POST",

headers: { "Content-Type": "application/json" },

body: JSON.stringify({ query: query })

});

const result = await response.json();

console.table(result.data.people.items);

}

```

In this example:

* The GraphQL query selects the `Id` and `Name` fields from the database.

* The request passed to the server requires a payload where the `query` property holds the query definition.

* Data in the response payload is found in the `data.people.items` property.

Refresh the page and select the **List** button.

The browser's console window now displays a table that lists all the records in the database.

| id | Name |

|---|---|

| 1 | Sunny |

| 2 | Dheeraj |

Here's a screenshot of what it should look like in your browser.

### Get by ID

Add the following code between the `script` tags in *index.html*.

```javascript

async function get() {

const id = '1';

const gql = `

query getById($id: ID!) {

person_by_pk(id: $id) {

id

Name

}

}`;

const query = {

query: gql,

variables: {

id: id,

},

};

const endpoint = "/data-api/graphql";

const response = await fetch(endpoint, {

method: "POST",

headers: { "Content-Type": "application/json" },

body: JSON.stringify(query),

});

const result = await response.json();

console.table(result.data.person_by_pk);

}

```

In this example:

* The GraphQL query selects the `id` and `Name` fields from the database.

* The request passed to the server requires a payload where the `query` property holds the query definition.

* Data in the response payload is found in the `data.person_by_pk` property.

Refresh the page and select the **Get** button.

The browser's console window now displays a table listing the single record requested from the database.

| id | Name |

|---|---|

| 1 | Sunny |

### Update

Add the following code between the `script` tags in *index.html*.

```javascript

async function update() {

const id = '1';

const data = {

id: id,

Name: "Molly"

};

const gql = `

mutation update($id: ID!, $_partitionKeyValue: String!, $item: UpdatePersonInput!) {

updatePerson(id: $id, _partitionKeyValue: $_partitionKeyValue, item: $item) {

id

Name

}

}`;

const query = {

query: gql,

variables: {

id: id,

_partitionKeyValue: id,

item: data

}

};

const endpoint = "/data-api/graphql";

const res = await fetch(endpoint, {

method: "POST",

headers: { "Content-Type": "application/json" },

body: JSON.stringify(query)

});

const result = await res.json();

console.table(result.data.updatePerson);

}

```

In this example:

* The GraphQL query selects the `id` and `Name` fields from the database.

* The `query` object holds the GraphQL query in the `query` property.

* The argument values to the GraphQL function are passed in via the `query.variables` property.

* The request passed to the server requires a payload where the `query` property holds the query definition.

* Data in the response payload is found in the `data.updatePerson` property.

Refresh the page and select the **Update** button.

The browser's console window now displays a table showing the updated data.

| id | Name |

|---|---|

| 1 | Molly |

### Create

Add the following code between the `script` tags in *index.html*.

```javascript

async function create() {

const data = {

id: "3",

Name: "Pedro"

};

const gql = `

mutation create($item: CreatePersonInput!) {

createPerson(item: $item) {

id

Name

}

}`;

const query = {

query: gql,

variables: {

item: data

}

};

const endpoint = "/data-api/graphql";

const result = await fetch(endpoint, {

method: "POST",

headers: { "Content-Type": "application/json" },

body: JSON.stringify(query)

});

const response = await result.json();

console.table(response.data.createPerson);

}

```

In this example:

* The GraphQL query selects the `id` and `Name` fields from the database.

* The `query` object holds the GraphQL query in the `query` property.

* The argument values to the GraphQL function are passed in via the `query.variables` property.

* The request passed to the server requires a payload where the `query` property holds the query definition.

* Data in the response payload is found in the `data.updatePerson` property.

Refresh the page and select the **Create** button.

The browser's console window now displays a table showing the new record in the database.

| id | Name |

|---|---|

| 3 | Pedro |

### Delete

Add the following code between the `script` tags in *index.html*.

```javascript

async function del() {

const id = '3';

const gql = `

mutation del($id: ID!, $_partitionKeyValue: String!) {

deletePerson(id: $id, _partitionKeyValue: $_partitionKeyValue) {

id

}

}`;

const query = {

query: gql,

variables: {

id: id,

_partitionKeyValue: id

}

};

const endpoint = "/data-api/graphql";

const response = await fetch(endpoint, {

method: "POST",

headers: { "Content-Type": "application/json" },

body: JSON.stringify(query)

});

const result = await response.json();

console.log(`Record deleted: ${ JSON.stringify(result.data) }`);

}

```

In this example:

* The GraphQL query selects the `Id` field from the database.

* The `query` object holds the GraphQL query in the `query` property.

* The argument values to the GraphQL function are passed in via the `query.variables` property.

* The request passed to the server requires a payload where the `query` property holds the query definition.

* Data in the response payload is found in the `data.deletePerson` property.

Refresh the page and select the **Delete** button.

The browser's console window now displays a table showing the response from the delete request.

*Record deleted: 2*

Now that you've worked with your site locally, you can now deploy it to Azure.

## Deploy your site

To deploy this site to production, you just need to commit the configuration file and push your changes to the server.

1. Commit the configuration changes.

```bash

git commit -am "Add database configuration"

```

1. Push your changes to the server.

```bash

git push origin main

```

1. Wait for your web app to build.

1. Go to your static web app in the browser.

1. Select the **List** button to list all items.

The output should resemble what's shown in this screenshot.

## Connect the database to your static web app

Use the following steps to create a connection between the Static Web Apps instance of your site and your database.

1. Open your static web app in the Azure portal.

1. In the *Settings* section, select **Database connection**.

1. Under the *Production* section, select the **Link existing database** link.

1. In the *Link existing database* window, enter the following values:

| Property | Value |

|---|---|

| Database Type | Select your database type from the dropdown list. |

| Subscription | Select your Azure subscription from the dropdown list. |

| Database Name | Select the name of the database you want to link to your static web app. |

| Authentication Type | Select **Connection string**. |

1. Select **OK**.

## Verify that your database is connected to your Static Web Apps resource

Once you've connected your database to your static web app and the site is finished building, use the following steps to verify the database connection.

1. Open your static web app in the Azure portal.

1. In the *Essentials* section, select the **URL** of your Static Web Apps resource to navigate to your static web app.

1. Select the **List** button to list all items.

The output should resemble what's shown in this screenshot.

## Clean up resources

If you want to remove the resources created during this tutorial, you need to unlink the database and remove the sample data.

1. **Unlink database**: Open your static web app in the Azure portal. Under the *Settings* section, select **Database connection**. Next to the linked database, select **View details**. In the *Database connection details* window, select the **Unlink** button.

1. **Remove sample data**: In your database, delete the table named `MyTestPersonContainer`.

## Next steps

> [!div class="nextstepaction"]

> [Add an API](add-api.md)


# Database Azure Sql

# Tutorial: Add an Azure SQL database connection in Azure Static Web Apps (preview)

In this tutorial, you learn how to connect an Azure SQL database to your static web app. Once configured, you can make REST or GraphQL requests to the built-in `/data-api` endpoint to manipulate data without having to write backend code.

For the sake of simplicity, this tutorial shows you how to use an Azure database for local development purposes, but you may also use a local database server for your local development needs.

> [!NOTE]

> This tutorial shows how to use Azure SQL. If you would like to use another database, refer to the [Azure Cosmos DB](database-azure-cosmos-db.md), [MySQL](database-mysql.md), or [PostgreSQL](database-postgresql.md) tutorials.

In this tutorial, you learn to:

> [!div class="checklist"]

> * Link an Azure SQL database to your static web app

> * Create, read, update, and delete data

## Prerequisites

To complete this tutorial, you need to have an existing Azure SQL database and static web app.

| Resource | Description |

|---|---|

| [Azure SQL Database](/azure/azure-sql/database/single-database-create-quickstart) | If you don't already have one, follow the steps in the [create a single database](/azure/azure-sql/database/single-database-create-quickstart) guide. |

| [Existing static web app](getting-started.md) | If you don't already have one, follow the steps in the [getting started](getting-started.md) guide.  |

Begin by configuring your database to work with the Azure Static Web Apps database connection feature.

## Configure database connectivity

Azure Static Web Apps must have network access to your database for database connections to work. Additionally, to use an Azure database for local development, you need to configure your database to allow requests from your own IP address.

1. Go to your Azure SQL Server in the [Azure portal](https://portal.azure.com).

1. Under the *Security* section, select **Networking**.

1. Under the *Public access* tab, next to *Public network access*, select **Selected networks**.

1. Under the *Firewall rules* section, select the **Add your client IPv4 address** button. This step ensures you can use this database for your local development.

1. Under the *Exceptions* section, select the **Allow Azure services and resources to access this server** checkbox. This step ensures that your deployed Static Web Apps resource can access your database.

1. Select **Save**.

## Get database connection string for local development

To use your Azure database for local development, you need to retrieve the connection string of your database. You may skip this step if you plan to use a local database for development purposes.

1. Go to your Azure SQL Server in the [Azure portal](https://portal.azure.com).

1. Under the *Settings* section, select **SQL databases**.

1. Select the SQL database you created for this tutorial.

1. In the *Settings* section, select **Connection strings**

1. From the *ADO.NET (SQL authentication)* box, copy the connection string and set it aside in a text editor.

Make sure to replace the `{your_password}` placeholder in the connection string with your password.

## Create sample data

Create a sample table and seed it with sample data to match the tutorial.

1. On the left-hand navigation window, select **Query editor**.

1. Sign in to the server with your Entra ID account or the server's user name and password.

1. Run the following script to create a new table named `MyTestPersonTable`.

```sql

CREATE TABLE [dbo].[MyTestPersonTable] (

[Id] INT IDENTITY (1, 1) NOT NULL,

[Name] VARCHAR (25) NULL,

PRIMARY KEY (Id)

);

```

1. Run the following script to add data into the *MyTestPersonTable* table.

```sql

INSERT INTO [dbo].[MyTestPersonTable] (Name)

VALUES ('Sunny');

INSERT INTO [dbo].[MyTestPersonTable] (Name)

VALUES ('Dheeraj');

```

## Configure the static web app

The rest of this tutorial focuses on editing your static web app's source code to make use of database connections locally.

> [!IMPORTANT]

> The following steps assume you are working with the static web app created in the [getting started guide](getting-started.md). If you are using a different project, make sure to adjust the following git commands to match your branch names.

1. Switch to the `main` branch.

# [Bash](#tab/bash)

```bash

git checkout main

```

# [PowerShell](#tab/powershell)

```powershell

git checkout main

```

---

1. Synchronize your local version with what's on GitHub by using `git pull`.

# [Bash](#tab/bash)

```bash

git pull origin main

```

# [PowerShell](#tab/powershell)

```powershell

git pull origin main

```

---

### Create the database configuration file

Next, create the configuration file that your static web app uses to interface with the database.

1. Open your terminal and create a new variable to hold your connection string. The specific syntax may vary depending on the shell type you're using.

# [Bash](#tab/bash)

```bash

export DATABASE_CONNECTION_STRING='<YOUR_CONNECTION_STRING>'

```

# [PowerShell](#tab/powershell)

```powershell

$env:DATABASE_CONNECTION_STRING='<YOUR_CONNECTION_STRING>'

```

---

Make sure to replace `<YOUR_CONNECTION_STRING>` with the connections string value you set aside in a text editor.

1. Use npm to install or update the Static Web Apps CLI. Select which command is best for your situation.

To install, use `npm install`.

# [Bash](#tab/bash)

```bash

npm install -g @azure/static-web-apps-cli

```

# [PowerShell](#tab/powershell)

```powershell

npm install -g @azure/static-web-apps-cli

```

---

To update, use `npm update`.

# [Bash](#tab/bash)

```bash

npm update

```

# [PowerShell](#tab/powershell)

```powershell

npm update

```

---

1. Use the `swa db init` command to generate a database configuration file.

# [Bash](#tab/bash)

```bash

swa db init --database-type mssql

```

# [PowerShell](#tab/powershell)

```powershell

swa db init --database-type mssql

```

---

The `init` command creates the *staticwebapp.database.config.json* file in the *swa-db-connections* folder.

1. Paste in this sample into file *staticwebapp.database.config.json* you generated.

```json

{

"$schema": "https://github.com/Azure/data-api-builder/releases/latest/download/dab.draft.schema.json",

"data-source": {

"database-type": "mssql",

"options": {

"set-session-context": false

},

"connection-string": "@env('DATABASE_CONNECTION_STRING')"

},

"runtime": {

"rest": {

"enabled": true,

"path": "/rest"

},

"graphql": {

"allow-introspection": true,

"enabled": true,

"path": "/graphql"

},

"host": {

"mode": "production",

"cors": {

"origins": ["http://localhost:4280"],

"allow-credentials": false

},

"authentication": {

"provider": "StaticWebApps"

}

}

},

"entities": {

"Person": {

"source": "dbo.MyTestPersonTable",

"permissions": [

{

"actions": ["*"],

"role": "anonymous"

}

]

}

}

}

```

Before moving on to the next step, review the following table that explains different aspects of the configuration file. For full documentation on the configuration file and functionality such as relationships and policies for item-level security, refer to [Data API Builder documentation](/azure/data-api-builder/configuration-file).

| Feature | Explanation |

|---|---|

| **Database connection** | In development, the runtime reads the connection string from the value of the connection string in the configuration file. While you can specify your connection string directly in the configuration file, a best practice is to store connection strings in a local environment variable. You can refer to environment variable values in the configuration file via the `@env('DATABASE_CONNECTION_STRING')` notation. The value of the connection string gets overwritten by Static Web Apps for the deployed site with the information collected when you connect your database. |

| **API endpoint** | The REST endpoint is available via `/data-api/rest` while the GraphQL endpoint is available through `/data-api/graphql` as configured in this configuration file. You may configure the REST and GraphQL paths, but the `/data-api` prefix isn't configurable. |

| **API Security** | The `runtime.host.cors` settings allow you to define allowed origins that can make requests to the API. In this case, the configuration reflects a development environment and allowlists the *http://localhost:4280* location. |

| **Entity model** | Defines the entities exposed via routes in the REST API, or as types in the GraphQL schema. In this case, the name *Person*, is the name exposed to the endpoint while `entities.<NAME>.source` is the database schema and table mapping. Notice how the API endpoint name doesn't need to be identical to the table name. |

| **Entity security** | Permissions rules listed in the `entity.<NAME>.permissions` array control the authorization settings for an entity. You can secure an entity with roles in the same way you [secure routes with roles](./configuration.md#securing-routes-with-roles).  |

> [!NOTE]

> The configuration file's `connection-string`, `host.mode`, and `graphql.allow-introspection` properties are overwritten when you deploy your site. Your connection string is overwritten with the authentication details collected when you connect your database to your Static Web Apps resource. The `host.mode` property is set to `production`, and the `graphql.allow-introspection` is set to `false`. These overrides provide consistency in your configuration files across your development and production workloads, while ensuring your Static Web Apps resource with database connections enabled is secure and production-ready.

With the static web app configured to connect to the database, you can now verify the connection.

[!INCLUDE [Database connection  - client code](../../includes/static-web-apps-database-connection-client-code.md)]

## Connect the database to your static web app

Use the following steps to create a connection between the Static Web Apps instance of your site and your database.

1. Open your static web app in the Azure portal.

1. In the *Settings* section, select **Database connection**.

1. Under the *Production* section, select the **Link existing database** link.

1. In the *Link existing database* window, enter the following values:

| Property | Value |

|---|---|

| Database Type | Select your database type from the dropdown list. |

| Subscription | Select your Azure subscription from the dropdown list. |

| Resource Group | Select or create a resource group for your database. |

| Resource Name | Select the database server name that has your desired database. |

| Database Name | Select the name of the database you want to link to your static web app. |

| Authentication Type | Select **Connection string**, and enter the Azure SQL user name and password. |

1. Select **OK**.

## Verify that your database is connected to your Static Web Apps resource

Once you've connected your database to your static web app and the site is finished building, use the following steps to verify the database connection.

1. Open your static web app in the Azure portal.

1. In the *Essentials* section, select the **URL** of your Static Web Apps resource to navigate to your static web app.

1. Select the **List** button to list all items.

The output should resemble what's shown in this screenshot.

## Clean up resources

If you want to remove the resources created during this tutorial, you need to unlink the database and remove the sample data.

1. **Unlink database**: Open your static web app in the Azure portal. Under the *Settings* section, select **Database connection**. Next to the linked database, select **View details**. In the *Database connection details* window, select the **Unlink** button.

1. **Remove sample data**: In your database, delete the table named `MyTestPersonTable`.

## Next steps

> [!div class="nextstepaction"]

> [Add an API](add-api.md)


# Database Mysql

# Tutorial: Add a MySQL database connection in Azure Static Web Apps (preview)

In this tutorial, you learn how to connect an Azure Database for MySQL Flexible Server database to your static web app. Once configured, you can make REST or GraphQL requests to the built-in `/data-api` endpoint to manipulate data without having to write backend code.

For the sake of simplicity, this tutorial shows you how to use an Azure database for local development purposes, but you may also use a local database server for your local development needs.

> [!NOTE]

> This tutorial shows how to use Azure Database for MySQL Flexible Server. If you would like to use another database, refer to the [Azure Cosmos DB](database-azure-cosmos-db.md), [Azure SQL](database-azure-sql.md), or [PostgreSQL](database-postgresql.md) tutorials.

In this tutorial, you learn to:

> [!div class="checklist"]

> * Link an Azure Database for MySQL database to your static web app

> * Create, read, update, and delete data

## Prerequisites

To complete this tutorial, you need to have an existing Azure Database for MySQL database and static web app. Additionally, you need to install Visual Studio Code.

| Resource | Description |

|---|---|

| [Azure Database for MySQL Flexible Server](/azure/mysql/flexible-server/quickstart-create-server-portal) | If you need to create a database, follow the steps in the [create an Azure Database for MySQL Flexible Server](/azure/mysql/flexible-server/quickstart-create-server-portal) guide. If you plan to use a connection string authentication for your web app, ensure that you create your database with MySQL authentication. You can change this setting later if you want to use managed identity later on. |

| [Existing static web app](getting-started.md) | If you don't already have one, follow the steps in the [getting started](getting-started.md) guide to create a *No Framework* static web app.  |

| [Visual Studio Code, with the MySQL Shell extension](https://marketplace.visualstudio.com/items?itemName=Oracle.mysql-shell-for-vs-code) | If you don't already have Visual Studio Code installed, follow the guide to install [Visual Studio Code, with the MySQL Shell extension](https://marketplace.visualstudio.com/items?itemName=Oracle.mysql-shell-for-vs-code). Alternatively, you may use any other tool to query your MySQL database, such as MySQL Workbench. |

Begin by configuring your database to work with the Azure Static Web Apps database connection feature.

## Configure database connectivity

Azure Static Web Apps must have network access to your database for database connections to work. Additionally, to use an Azure database for local development, you need to configure your database to allow requests from your own IP address.

1. Go to your Azure Database for MySQL Server Flexible Server in the [Azure portal](https://portal.azure.com).

1. Under the *Settings* section, select **Networking**.

1. Under the *Firewall rules* section, select the **Add your current client IP address** button. This step ensures that you can use this database for your local development.

1. Under the *Firewall rules* section, select the **Allow public access from any Azure service within Azure to this server** checkbox. This step ensures that your deployed Static Web Apps resource can access your database.

1. Select **Save**.

## Get database connection string for local development

To use your Azure database for local development, you need to retrieve the connection string of your database. You may skip this step if you plan to use a local database for development purposes.

1. Go to your Azure Database for MySQL Server Flexible Server in the [Azure portal](https://portal.azure.com).

1. Under the *Settings* section, select **Connect**.

1. In the *Connect from your app* section, select the ADO.NET connection string and set it aside in a text editor.

1. Replace the `{your_password}` placeholder in the connection string with your password.

1. Replace the `{your_database}` placeholder with the database name `MyTestPersonDatabase`. You'll create the `MyTestPersonDatabase` in the coming steps.

1. Delete the *SslMode* and the *SslCa* sections of the connection string as these require extra steps and are intended for production purposes.

## Create sample data

Create a sample table and seed it with sample data to match the tutorial. Here, you can use [Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=Oracle.mysql-shell-for-vs-code), but you may use MySQL Workbench or any other tool.

1. In Visual Studio Code with the MySQL Shell extension, create a connection to your Azure MySQL Flexible Server.

1. Right-click your server, and create a new database. Enter `MyTestPersonDatabase` as the database name, and select the charset to be `utf8mb4` and the collation of `utf8mb4_0900_ai_ci`.

1. Right-click your server and select **Refresh**.

1. Right-click your `MyTestPersonDatabase` database and select **New Query**. Run the following script to create a new table named `MyTestPersonTable`.

```sql

CREATE TABLE MyTestPersonTable (

Id INT AUTO_INCREMENT NOT NULL,

Name VARCHAR(25) NULL,

PRIMARY KEY (Id)

);

```

1. Run the following script to add data into the `MyTestPersonTable` table.

```sql

INSERT INTO MyTestPersonTable (Name)

VALUES ('Sunny');

INSERT INTO MyTestPersonTable (Name)

VALUES ('Dheeraj');

```

1. Right-click your `MyTestPersonTable` table and select **Select Top 1000** to verify there's data in your database.

## Configure the static web app

The rest this tutorial focuses on editing your static web app's source code to make use of database connections locally.

> [!IMPORTANT]

> The following steps assume you are working with the static web app created in the [getting started guide](getting-started.md). If you are using a different project, make sure to adjust the following git commands to match your branch names.

1. Switch to the `main` branch.

# [Bash](#tab/bash)

```bash

git checkout main

```

# [PowerShell](#tab/powershell)

```powershell

git checkout main

```

---

1. Synchronize your local version with what's on GitHub by using `git pull`.

# [Bash](#tab/bash)

```bash

git pull origin main

```

# [PowerShell](#tab/powershell)

```powershell

git pull origin main

```

---

### Create the database configuration file

Next, create the configuration file that your static web app uses to interface with the database.

1. Open your terminal and create a new variable to hold your connection string. The specific syntax may vary depending on the shell type you're using.

# [Bash](#tab/bash)

```bash

export DATABASE_CONNECTION_STRING='<YOUR_CONNECTION_STRING>'

```

# [PowerShell](#tab/powershell)

```powershell

$env:DATABASE_CONNECTION_STRING='<YOUR_CONNECTION_STRING>'

```

---

Make sure to replace `<YOUR_CONNECTION_STRING>` with the connections string value you set aside in a text editor.

1. Use npm to install or update the Static Web Apps CLI. Select which command is best for your situation.

To install, use `npm install`.

# [Bash](#tab/bash)

```bash

npm install -g @azure/static-web-apps-cli

```

# [PowerShell](#tab/powershell)

```powershell

npm install -g @azure/static-web-apps-cli

```

---

To update, use `npm update`.

# [Bash](#tab/bash)

```bash

npm update

```

# [PowerShell](#tab/powershell)

```powershell

npm update

```

---

1. Use the `swa db init` command to generate a database configuration file.

# [Bash](#tab/bash)

```bash

swa db init --database-type mysql

```

# [PowerShell](#tab/powershell)

```powershell

swa db init --database-type mysql

```

---

The `init` command creates the *staticwebapp.database.config.json* file in the *swa-db-connections* folder.

1. Paste in this sample into file *staticwebapp.database.config.json* you generated.

```json

{

"$schema": "https://github.com/Azure/data-api-builder/releases/latest/download/dab.draft.schema.json",

"data-source": {

"database-type": "mysql",

"options": {

"set-session-context": false

},

"connection-string": "@env('DATABASE_CONNECTION_STRING')"

},

"runtime": {

"rest": {

"enabled": true,

"path": "/rest"

},

"graphql": {

"allow-introspection": true,

"enabled": true,

"path": "/graphql"

},

"host": {

"mode": "production",

"cors": {

"origins": ["http://localhost:4280"],

"allow-credentials": false

},

"authentication": {

"provider": "StaticWebApps"

}

}

},

"entities": {

"Person": {

"source": "MyTestPersonTable",

"permissions": [

{

"actions": ["*"],

"role": "anonymous"

}

]

}

}

}

```

Before moving on to the next step, review the following table that explains different aspects of the configuration file. For full documentation on the configuration file, refer to [Data API Builder documentation](/azure/data-api-builder/configuration-file).

| Feature | Explanation |

|---|---|

| **Database connection** | In development, the runtime reads the connection string from the value of the connection string in the configuration file. While you can specify your connection string directly in the configuration file, a best practice is to store connection strings in a local environment variable. You can refer to environment variable values in the configuration file via the `@env('DATABASE_CONNECTION_STRING')` notation. The value of the connection string gets overwritten by Static Web Apps for the deployed site with the information collected when you connect your database. |

| **API endpoint** | The REST endpoint is available via `/data-api/rest` while the GraphQL endpoint is available through `/data-api/graphql` as configured in this configuration file. You may configure the REST and GraphQL paths, but the `/data-api` prefix isn't configurable. |

| **API Security** | The `runtime.host.cors` settings allow you to define allowed origins that can make requests to the API. In this case, the configuration reflects a development environment and allowlists the *http://localhost:4280* location. |

| **Entity model** | Defines the entities exposed via routes in the REST API, or as types in the GraphQL schema. In this case, the name *Person*, is the name exposed to the endpoint while `entities.<NAME>.source` is the database schema and table mapping. Notice how the API endpoint name doesn't need to be identical to the table name. |

| **Entity security** | Permissions rules listed in the `entity.<NAME>.permissions` array control the authorization settings for an entity. You can secure an entity with roles in the same way you [secure routes with roles](./configuration.md#securing-routes-with-roles).  |

> [!NOTE]

> The configuration file's `connection-string`, `host.mode`, and `graphql.allow-introspection` properties are overwritten when you deploy your site. Your connection string is overwritten with the authentication details collected when you connect your database to your Static Web Apps resource. The `host.mode` property is set to `production`, and the `graphql.allow-introspection` is set to `false`. These overrides provide consistency in your configuration files across your development and production workloads, while ensuring your Static Web Apps resource with database connections enabled is secure and production-ready.

With the static web app configured to connect to the database, you can now verify the connection.

[!INCLUDE [Database connection  - client code](../../includes/static-web-apps-database-connection-client-code.md)]

## Connect the database to your static web app

Use the following steps to create a connection between the Static Web Apps instance of your site and your database.

1. Open your static web app in the Azure portal.

1. In the *Settings* section, select **Database connection**.

1. Under the *Production* section, select the **Link existing database** link.

1. In the *Link existing database* window, enter the following values:

| Property | Value |

|---|---|

| Database Type | Select your database type from the dropdown list. |

| Subscription | Select your Azure subscription from the dropdown list. |

| Resource Name | Select the database server name that has your desired database. |

| Database Name | Select the name of the database you want to link to your static web app. |

| Authentication Type | Select **Connection string**, and enter the MySQL user name and password. |

1. Select **OK**.

## Verify that your database is connected to your Static Web Apps resource

Once you've connected your database to your static web app and the site is finished building, use the following steps to verify the database connection.

1. Open your static web app in the Azure portal.

1. In the *Essentials* section, select the **URL** of your Static Web Apps resource to navigate to your static web app.

1. Select the **List** button to list all items.

The output should resemble what's shown in this screenshot.

## Clean up resources

If you want to remove the resources created during this tutorial, you need to unlink the database and remove the sample data.

1. **Unlink database**: Open your static web app in the Azure portal. Under the *Settings* section, select **Database connection**. Next to the linked database, select **View details**. In the *Database connection details* window, select the **Unlink** button.

1. **Remove sample data**: In your database, delete the table named `MyTestPersonTable`.

## Next steps

> [!div class="nextstepaction"]

> [Add an API](add-api.md)


# Database Postgresql

# Tutorial: Add a PostgreSQL database connection in Azure Static Web Apps (preview)

In this tutorial, you learn how to connect an Azure Database for PostgreSQL Single Server or Flexible Server database to your static web app. Once configured, you can make REST or GraphQL requests to the built-in `/data-api` endpoint to manipulate data without having to write backend code.

For the sake of simplicity, this tutorial shows you how to use an Azure database for local development purposes, but you may also use a local database server for your local development needs.

> [!NOTE]

> This tutorial shows how to use Azure Database for PostgreSQL Flexible Server or Single Server. If you would like to use another database, refer to the [Azure Cosmos DB](database-azure-cosmos-db.md), [Azure SQL](database-azure-sql.md), or [MySQL](database-mysql.md) tutorials.

In this tutorial, you learn to:

> [!div class="checklist"]

> * Link an Azure Database for PostgreSQL Flexible Server or Single Server database to your static web app

> * Create, read, update, and delete data

## Prerequisites

To complete this tutorial, you need to have an existing Azure Database for PostgreSQL Flexible Server or Single Server and static web app. Additionally, you need to install Visual Studio Code.

| Resource | Description |

|---|---|

| [Azure Database for PostgreSQL Flexible Server](/azure/postgresql/flexible-server/quickstart-create-server-portal) or [Azure Database for PostgreSQL Single Server Database](/azure/postgresql/single-server/quickstart-create-server-database-portal) | If you don't already have one, follow the steps in the [create an Azure Database for PostgreSQL Flexible Server database](/azure/postgresql/flexible-server/quickstart-create-server-portal) guide, or in the [create an Azure Database for PostgreSQL Single Server database](/azure/postgresql/single-server/quickstart-create-server-database-portal) guide. If you plan to use a connection string authentication for Static Web Apps' database connections, ensure that you create your Azure Database for PostgreSQL Server with PostgreSQL authentication. You can change this value if you want to use managed identity later on. |

| [Existing static web app](getting-started.md) | If you don't already have one, follow the steps in the [getting started](getting-started.md) guide to create a *No Framework* static web app. |

| [Visual Studio Code, with the PostgreSQL extension](/azure-data-studio/quickstart-postgres) | If you don't already have Visual Studio Code installed, follow the guide to install [Visual Studio Code, with the PostgreSQL extension](/azure/postgresql/developer/vs-code-extension/vs-code-connect). Alternatively, you may use any other tool to query your PostgreSQL database, such as PgAdmin. |

Begin by configuring your database to work with the Azure Static Web Apps database connection feature.

## Configure database connectivity

Azure Static Web Apps must have network access to your database for database connections to work. Additionally, to use an Azure database for local development, you need to configure your database to allow requests from your own IP address.

1. Go to your Azure Database for PostgreSQL Server in the [Azure portal](https://portal.azure.com).

1. If you're using Azure Database for PostgreSQL Flexible Server, under the *Settings* section, select **Networking**. If you're using Azure Database for PostgreSQL Single Server, under the *Settings* section, select **Connection security**.

1. Under the *Firewall rules* section, select the **Add your current client IP address** button. This step ensures that you can use this database for your local development.

1. Under the *Firewall rules* section, select the **Allow public access from any Azure service within Azure to this server** checkbox. If you're using Azure Database for PostgreSQL Single Server, this toggle is labeled **Allow access to Azure services**. This step ensures that your deployed Static Web Apps resource can access your database.

1. Select **Save**.

## Get database connection string for local development

To use your Azure database for local development, you need to retrieve the connection string of your database. You may skip this step if you plan to use a local database for development purposes.

1. Go to your Azure Database for PostgreSQL Server in the [Azure portal](https://portal.azure.com).

1. Under the *Settings* section, select **Connection strings**.

1. From the *ADO.NET* box, copy the connection string and set it aside in a text editor.

1. Replace the `{your_password}` placeholder in the connection string with your password.

1. Replace the `{your_database}` placeholder with the database name `MyTestPersonDatabase`. You'll create the `MyTestPersonDatabase` in the coming steps.

1. Append `Trust Server Certificate=True;` to the connection string to use this connection string for local development.

## Create sample data

Create a sample table and seed it with sample data to match the tutorial. This tutorial uses [Visual Studio Code](/azure/postgresql/developer/vs-code-extension/vs-code-connect), but you may use PgAdmin or any other tool.

1. In Visual Studio Code, [create a connection to your Azure Database for PostgreSQL Server](/azure/postgresql/developer/vs-code-extension/vs-code-connect)

1. Right-click your server, and select **New Query**. Run the following querying to create a database named `MyTestPersonDatabase`.

```sql

CREATE DATABASE "MyTestPersonDatabase";

```

1. Right-click your server, and select **Refresh**.

1. Right-click your `MyTestPersonDatabase` and select **New Query**. Run the following query to create a new table named `MyTestPersonTable`.

```sql

CREATE TABLE "MyTestPersonTable" (

"Id" SERIAL PRIMARY KEY,

"Name" VARCHAR(25) NULL

);

```

1. Run the following queries to add data into the *MyTestPersonTable* table.

```sql

INSERT INTO "MyTestPersonTable" ("Name")

VALUES ('Sunny');

INSERT INTO "MyTestPersonTable" ("Name")

VALUES ('Dheeraj');

```

## Configure the static web app

The rest this tutorial focuses on editing your static web app's source code to make use of database connections locally.

> [!IMPORTANT]

> The following steps assume you are working with the static web app created in the [getting started guide](getting-started.md). If you are using a different project, make sure to adjust the following git commands to match your branch names.

1. Switch to the `main` branch.

# [Bash](#tab/bash)

```bash

git checkout main

```

# [PowerShell](#tab/powershell)

```powershell

git checkout main

```

---

1. Synchronize your local version with what's on GitHub by using `git pull`.

# [Bash](#tab/bash)

```bash

git pull origin main

```

# [PowerShell](#tab/powershell)

```powershell

git pull origin main

```

---

### Create the database configuration file

Next, create the configuration file that your static web app uses to interface with the database.

1. Open your terminal and create a new variable to hold your connection string. The specific syntax may vary depending on the shell type you're using.

# [Bash](#tab/bash)

```bash

export DATABASE_CONNECTION_STRING='<YOUR_CONNECTION_STRING>'

```

# [PowerShell](#tab/powershell)

```powershell

$env:DATABASE_CONNECTION_STRING='<YOUR_CONNECTION_STRING>'

```

---

Make sure to replace `<YOUR_CONNECTION_STRING>` with the connections string value you set aside in a text editor.

1. Use npm to install or update the Static Web Apps CLI. Select which command is best for your situation.

To install, use `npm install`.

```bash

npm install -g @azure/static-web-apps-cli

```

```powershell

npm install -g @azure/static-web-apps-cli

```

To update, use `npm update`.

```bash

npm update

```

```powershell

npm update

```

1. Use the `swa db init` command to generate a database configuration file.

# [Bash](#tab/bash)

```bash

swa db init --database-type postgresql

```

# [PowerShell](#tab/powershell)

```powershell

swa db init --database-type postgresql

```

---

The `init` command creates the *staticwebapp.database.config.json* file in the *swa-db-connections* folder.

1. Paste in this sample into file *staticwebapp.database.config.json* you generated.

```json

{

"$schema": "https://github.com/Azure/data-api-builder/releases/latest/download/dab.draft.schema.json",

"data-source": {

"database-type": "postgresql",

"options": {

"set-session-context": false

},

"connection-string": "@env('DATABASE_CONNECTION_STRING')"

},

"runtime": {

"rest": {

"enabled": true,

"path": "/rest"

},

"graphql": {

"allow-introspection": true,

"enabled": true,

"path": "/graphql"

},

"host": {

"mode": "production",

"cors": {

"origins": ["http://localhost:4280"],

"allow-credentials": false

},

"authentication": {

"provider": "StaticWebApps"

}

}

},

"entities": {

"Person": {

"source": "MyTestPersonTable",

"permissions": [

{

"actions": ["*"],

"role": "anonymous"

}

]

}

}

}

```

Before moving on to the next step, review the following table that explains different aspects of the configuration file. For full documentation on the configuration file and functionality such as relationships and policies for item-level security, refer to [Data API Builder documentation](/azure/data-api-builder/configuration-file).

| Feature | Explanation |

|---|---|

| **Database connection** | In development, the runtime reads the connection string from the value of the connection string in the configuration file. While you can specify your connection string directly in the configuration file, a best practice is to store connection strings in a local environment variable. You can refer to environment variable values in the configuration file via the `@env('DATABASE_CONNECTION_STRING')` notation. The value of the connection string gets overwritten by Static Web Apps for the deployed site with the information collected when you connect your database. |

| **API endpoint** | The REST endpoint is available via `/data-api/rest` while the GraphQL endpoint is available through `/data-api/graphql` as configured in this configuration file. You may configure the REST and GraphQL paths, but the `/data-api` prefix isn't configurable. |

| **API Security** | The `runtime.host.cors` settings allow you to define allowed origins that can make requests to the API. In this case, the configuration reflects a development environment and allowlists the *http://localhost:4280* location. |

| **Entity model** | Defines the entities exposed via routes in the REST API, or as types in the GraphQL schema. In this case, the name *Person*, is the name exposed to the endpoint while `entities.<NAME>.source` is the database schema and table mapping. Notice how the API endpoint name doesn't need to be identical to the table name. |

| **Entity security** | Permissions rules listed in the `entity.<NAME>.permissions` array control the authorization settings for an entity. You can secure an entity with roles in the same way you [secure routes with roles](./configuration.md#securing-routes-with-roles).  |

> [!NOTE]

> The configuration file's `connection-string`, `host.mode`, and `graphql.allow-introspection` properties are overwritten when you deploy your site. Your connection string is overwritten with the authentication details collected when you connect your database to your Static Web Apps resource. The `host.mode` property is set to `production`, and the `graphql.allow-introspection` is set to `false`. These overrides provide consistency in your configuration files across your development and production workloads, while ensuring your Static Web Apps resource with database connections enabled is secure and production-ready.

With the static web app configured to connect to the database, you can now verify the connection.

[!INCLUDE [Database connection  - client code](../../includes/static-web-apps-database-connection-client-code.md)]

## Connect the database to your static web app

Use the following steps to create a connection between the Static Web Apps instance of your site and your database.

1. Open your static web app in the Azure portal.

1. In the *Settings* section, select **Database connection**.

1. Under the *Production* section, select the **Link existing database** link.

1. In the *Link existing database* window, enter the following values:

| Property | Value |

|---|---|

| Database Type | Select your database type from the dropdown list. |

| Subscription | Select your Azure subscription from the dropdown list. |

| Resource Name | Select the database server name that has your desired database. |

| Database Name | Select the name of the database you want to link to your static web app. |

| Authentication Type | Select **Connection string**, and enter the PostgreSQL user name and password. For PostgreSQL Single Server, don't include the `@servername` suffix. |

1. Select **OK**.

## Verify that your database is connected to your Static Web Apps resource

Once you've connected your database to your static web app and the site is finished building, use the following steps to verify the database connection.

1. Open your static web app in the Azure portal.

1. In the *Essentials* section, select the **URL** of your Static Web Apps resource to navigate to your static web app.

1. Select the **List** button to list all items.

The output should resemble what's shown in this screenshot.

## Clean up resources

If you want to remove the resources created during this tutorial, you need to unlink the database and remove the sample data.

1. **Unlink database**: Open your static web app in the Azure portal. Under the *Settings* section, select **Database connection**. Next to the linked database, select **View details**. In the *Database connection details* window, select the **Unlink** button.

1. **Remove sample data**: In your database, delete the table named `MyTestPersonTable`.

## Next steps

> [!div class="nextstepaction"]

> [Add an API](add-api.md)


# Add Mongoose

# Access data in Azure Cosmos DB using Mongoose with Azure Static Web Apps

[Mongoose](https://mongoosejs.com/) is the most popular ODM (Object Document Mapping) client for Node.js. Mongoose allows you to design a data structure and enforce validation, and provides all the tooling necessary to interact with databases that support the MongoDB API. [Cosmos DB](/azure/cosmos-db/mongodb-introduction) supports the necessary MongoDB APIs and is available as a back-end server option on Azure.

## Prerequisites

- An [Azure account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). If you don’t have an Azure subscription, create a [free trial account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- A [GitHub account](https://github.com/join).

- A [Cosmos DB serverless](/azure/cosmos-db/serverless) account. With a serverless account, you only pay for the resources as they're used and avoid needing to create a full infrastructure.

## 1. Create a Cosmos DB serverless database

Complete the following steps to create a Cosmos serverless DB.

1. Sign in to the [Azure portal](https://portal.azure.com).

2. Select **Create a resource**.

3. Enter *Azure Cosmos DB* in the search box.

4. Select **Azure Cosmos DB**.

5. Select **Create**.

6. If prompted, under **Azure Cosmos DB API for MongoDB** select **Create**.

7. Configure your Azure Cosmos DB Account with the following information:

- Subscription: Choose the subscription you wish to use

- Resource: Select **Create new**, and set the name to **aswa-mongoose**

- Account name: A unique value is required

- Location: **West US 2**

- Capacity mode: **Serverless (preview)**

- Version: **4.0**

8. Select **Review + create**.

9. Select **Create**.

The creation process takes a few minutes. We'll come back to the database to gather the connection string after we [create a static web app](#2-create-a-static-web-app).

## 2. Create a static web app

This tutorial uses a GitHub template repository to help you create your application.

1. Go to the [starter template](https://github.com/login?return_to=/staticwebdev/mongoose-starter/generate).

2. Choose the **owner** (if using an organization other than your main account).

3. Name your repository **aswa-mongoose-tutorial**.

4. Select **Create repository from template**.

5. Return to the [Azure portal](https://portal.azure.com).

6. Select **Create a resource**.

7. Enter **static web app** in the search box.

8. Select **Static Web App**.

9. Select **Create**.

10. Configure your Azure Static Web App with the following information:

- Subscription: Choose the same subscription as before

- Resource group: Select **aswa-mongoose**

- Name: **aswa-mongoose-tutorial**

- Region: **West US 2**

- Select **Sign in with GitHub**

- Select **Authorize** if prompted to allow Azure Static Web Apps to create the GitHub Action to enable deployment

- Organization: Your GitHub account name

- Repository: **aswa-mongoose-tutorial**

- Branch: **main**

- Build presets: Choose **React**

- App location: **/**

- Api location: **api**

- Output location: **build**

11. Select **Review and create**.

12. Select **Create**.

13. The creation process takes a few moments; select **Go to resource** once the static web app is provisioned.

## 3. Configure database connection string

To allow the web app to communicate with the database, the database connection string is stored as an [application setting](application-settings.yml). Setting values are accessible in Node.js using the `process.env` object.

1. Select **Home** in the upper left corner of the Azure portal (or go back to [https://portal.azure.com](https://portal.azure.com)).

2. Select **Resource groups**.

3. Select **aswa-mongoose**.

4. Select the name of your database account - it has a type of **Azure Cosmos DB API for Mongo DB**.

5. Under **Settings** select **Connection String**.

6. Copy the connection string listed under **PRIMARY CONNECTION STRING**.

7. In the breadcrumbs, select **aswa-mongoose**.

8. Select **aswa-mongoose-tutorial** to return to the website instance.

9. Under **Settings** select **Configuration**.

10. Select **Add** and create a new Application Setting with the following values:

- Name: **AZURE_COSMOS_CONNECTION_STRING**

- Value: \<Paste the connection string you copied earlier\>

11. Select **OK**.

12. Select **Add** and create a new Application Setting with the following values for name of the database:

- Name: **AZURE_COSMOS_DATABASE_NAME**

- Value: **todo**

13. Select **OK**.

14. Select **Save**.

## 4. Go to your site

You can now explore the static web app.

1. In the Azure portal, select **Overview**.

2. Select the URL displayed in the upper right.

1. It looks similar to `https://calm-pond-05fcdb.azurestaticapps.net`.

3. Select **Please login to see your list of tasks**.

4. Select **Grant consent** to access the application.

5. Create a new list by entering a name into the textbox labeled **create new list** and selecting **Save**.

6. Create a new task by typing in a title in the textbox labeled **create new item** and selecting **Save**.

7. Confirm the task is displayed (it may take a moment).

8. Mark the task as complete by **selecting the check**; the task moves to the **Done items** section of the page.

9. **Refresh the page** to confirm a database is being used.

## Clean up resources

If you're not going to continue to use this application, delete

the resource group with the following steps:

1. Return to the [Azure portal](https://portal.azure.com).

2. Select **Resource groups**.

3. Select **aswa-mongoose**.

4. Select **Delete resource group**.

5. Enter **aswa-mongoose** into the textbox.

6. Select **Delete**.

## Next steps

Advance to the next article to learn how to configure local development...

> [!div class="nextstepaction"]

> [Set up local development](./local-development.md)


# User Information

# Accessing user information in Azure Static Web Apps

Azure Static Web Apps provides authentication-related user information via a [direct-access endpoint](#direct-access-endpoint) and to [API functions](#api-functions).

Many user interfaces rely heavily on user authentication data. The direct-access endpoint is a utility API that exposes user information without having to implement a custom function. Beyond convenience, the direct-access endpoint isn't subject to cold start delays that are associated with serverless architecture.

This article shows you how to read user information from a deployed application. If you want to read emulated user information during local development, see [Authorization and authentication emulation](./local-development.md#authorization-and-authentication-emulation).

## Client principal data

Client principal data object exposes user-identifiable information to your app. The following properties are featured in the client principal object:

| Property | Description |

|---|---|

| `identityProvider` | The name of the [identity provider](authentication-authorization.yml). |

| `userId`| An Azure Static Web Apps-specific unique identifier for the user. <ul><li>The value is unique on a per-app basis. For instance, the same user returns a different `userId` value on a different Static Web Apps resource.<li>The value persists for the lifetime of a user. If you delete and add the same user back to the app, a new `userId` is generated.</ul> |

| `userDetails` | Username or email address of the user. Some providers return the [user's email address](authentication-authorization.yml), while others send the [user handle](authentication-authorization.yml). |

| `userRoles` | An array of the [user's assigned roles](authentication-authorization.yml). |

| `claims` | An array of claims returned by your [custom authentication provider](authentication-custom.md). Only accessible in the direct-access endpoint. |

The following example is a sample client principal object:

```json

{

"identityProvider": "github",

"userId": "abcd12345abcd012345abcdef0123450",

"userDetails": "username",

"userRoles": ["anonymous", "authenticated"],

"claims": [{

"typ": "name",

"val": "Azure Static Web Apps"

}]

}

```

## Direct-access endpoint

You can send a `GET` request to the `/.auth/me` route and receive direct access to the client principal data. When the state of your view relies on authorization data, use this approach for the best performance.

For logged-in users, the response contains a client principal JSON object. Requests from unauthenticated users returns `null`.

Using the [fetch](https://developer.mozilla.org/docs/Web/API/Fetch_API/Using_Fetch)<sup>1</sup> API, you can access the client principal data using the following syntax.

```javascript

async function getUserInfo() {

const response = await fetch('/.auth/me');

const payload = await response.json();

const { clientPrincipal } = payload;

return clientPrincipal;

}

(async () => {

console.log(await getUserInfo());

})();

```

## API functions

The API functions available in Static Web Apps via the Azure Functions backend have access to the same user information as a client application, with the exception of the `claims` array. While the API does receive user-identifiable information, it does not perform its own checks if the user is authenticated or if they match a required role. Access control rules are defined in the [`staticwebapp.config.json`](configuration.md#routes) file.

# [JavaScript](#tab/javascript)

Client principal data is passed to API functions in the `x-ms-client-principal` request header. The client principal data is sent as a [Base64](https://www.wikipedia.org/wiki/Base64)-encoded string containing a serialized JSON object.

The following example function shows how to read and return user information.

```javascript

module.exports = async function (context, req) {

const header = req.headers.get('x-ms-client-principal');

const encoded = Buffer.from(header, 'base64');

const decoded = encoded.toString('ascii');

context.res = {

body: {

clientPrincipal: JSON.parse(decoded),

},

};

};

```

Assuming the above function is named `user`, you can use the [fetch](https://developer.mozilla.org/docs/Web/API/Fetch_API/Using_Fetch)<sup>1</sup> browser API to access the API's response using the following syntax.

```javascript

async function getUser() {

const response = await fetch('/api/user');

const payload = await response.json();

const { clientPrincipal } = payload;

return clientPrincipal;

}

console.log(await getUser());

```

# [C#](#tab/csharp)

In a C# function, the user information is available from the `x-ms-client-principal` header which your app can deserialize into a `ClaimsPrincipal` object, or your own custom type. The following code demonstrates how to unpack the header into an intermediary type, `ClientPrincipal`, which is then turned into a `ClaimsPrincipal` instance.

```csharp

using System;

using System.Collections.Generic;

using System.Linq;

using System.Security.Claims;

using System.Text;

using System.Text.Json;

using Microsoft.AspNetCore.Http;

public static class StaticWebAppsAuth

{

private class ClientPrincipal

{

public string IdentityProvider { get; set; }

public string UserId { get; set; }

public string UserDetails { get; set; }

public IEnumerable<string> UserRoles { get; set; }

}

public static ClaimsPrincipal Parse(HttpRequest req)

{

var principal = new ClientPrincipal();

if (req.Headers.TryGetValue("x-ms-client-principal", out var header))

{

var data = header[0];

var decoded = Convert.FromBase64String(data);

var json = Encoding.UTF8.GetString(decoded);

principal = JsonSerializer.Deserialize<ClientPrincipal>(json, new JsonSerializerOptions { PropertyNameCaseInsensitive = true });

}

principal.UserRoles = principal.UserRoles?.Except(new string[] { "anonymous" }, StringComparer.CurrentCultureIgnoreCase);

if (!principal.UserRoles?.Any() ?? true)

{

return new ClaimsPrincipal();

}

var identity = new ClaimsIdentity(principal.IdentityProvider);

identity.AddClaim(new Claim(ClaimTypes.NameIdentifier, principal.UserId));

identity.AddClaim(new Claim(ClaimTypes.Name, principal.UserDetails));

identity.AddClaims(principal.UserRoles.Select(r => new Claim(ClaimTypes.Role, r)));

return new ClaimsPrincipal(identity);

}

}

```

---

When a user is logged in, the `x-ms-client-principal` header is added to the requests for user information via the Static Web Apps edge nodes.

> [!NOTE]

> The `x-ms-client-principal` header accessible in the API function does not contain the `claims` array.

<sup>1</sup> The [fetch](https://caniuse.com/#feat=fetch) API and [await](https://caniuse.com/#feat=mdn-javascript_operators_await) operator aren't supported in Internet Explorer.

## Next steps

> [!div class="nextstepaction"]

> [Configure app settings](application-settings.yml)


# Authentication Custom

# Custom authentication in Azure Static Web Apps

Azure Static Web Apps provides [managed authentication](authentication-authorization.yml) that uses provider registrations managed by Azure. To enable more flexibility over the registration, you can override the defaults with a custom registration.

- Custom authentication also allows you to [configure custom providers](./authentication-custom.md?tabs=openid-connect#configure-a-custom-identity-provider) that support [OpenID Connect](https://openid.net/connect/). This configuration allows the registration of multiple external providers.

- Using any custom registrations disables all preconfigured providers.

> [!NOTE]

> Custom authentication is only available in the Azure Static Web Apps Standard plan.

## Configure a custom identity provider

Custom identity providers are configured in the `auth` section of the [configuration file](configuration.md).

To avoid putting secrets in source control, the configuration looks into [application settings](application-settings.yml#configure-application-settings) for a matching name in the configuration file. You might also choose to store your secrets in [Azure Key Vault](./key-vault-secrets.md).

# [Microsoft Entra ID](#tab/aad)

To create the registration, begin by creating the following [application settings](application-settings.yml#configure-application-settings):

| Setting Name | Value |

| --- | --- |

| `AZURE_CLIENT_ID` | The Application (client) ID for the Microsoft Entra app registration. |

| `AZURE_CLIENT_SECRET_APP_SETTING_NAME` | The name of the application setting that holds the client secret for the Microsoft Entra app registration. |

Next, use the following sample to configure the provider in the [configuration file](configuration.md).

Microsoft Entra providers are available in two different versions. Version 1 explicitly defines the `userDetailsClaim`, which allows the payload to return user information. By contrast, version 2 returns user information by default, and is designated by `v2.0` in the `openIdIssuer` URL.

<a name='azure-active-directory-version-1'></a>

### Microsoft Entra Version 1

```json

{

"auth": {

"identityProviders": {

"azureActiveDirectory": {

"userDetailsClaim": "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name",

"registration": {

"openIdIssuer": "https://login.microsoftonline.com/<TENANT_ID>",

"clientIdSettingName": "AZURE_CLIENT_ID",

"clientSecretSettingName": "AZURE_CLIENT_SECRET_APP_SETTING_NAME"

}

}

}

}

}

```

Make sure to replace `<TENANT_ID>` with your Microsoft Entra tenant ID.

<a name='azure-active-directory-version-2'></a>

### Microsoft Entra Version 2

```json

{

"auth": {

"identityProviders": {

"azureActiveDirectory": {

"registration": {

"openIdIssuer": "https://login.microsoftonline.com/<TENANT_ID>/v2.0",

"clientIdSettingName": "AZURE_CLIENT_ID",

"clientSecretSettingName": "AZURE_CLIENT_SECRET_APP_SETTING_NAME"

}

}

}

}

}

```

Make sure to replace `<TENANT_ID>` with your Microsoft Entra tenant ID.

For more information on how to configure Microsoft Entra ID, see the [App Service Authentication/Authorization documentation](../app-service/configure-authentication-provider-aad.md#-option-2-use-an-existing-registration-created-separately) on using an existing registration.

To configure which accounts can sign in, see [Modify the accounts supported by an application](../active-directory/develop/howto-modify-supported-accounts.md) and [Restrict your Microsoft Entra app to a set of users in a Microsoft Entra tenant](../active-directory/develop/howto-restrict-your-app-to-a-set-of-users.md).

> [!NOTE]

> While the configuration section for Microsoft Entra ID is `azureActiveDirectory`, the platform aliases this to `aad` in the URL's for login, logout and purging user information. Refer to the [authentication and authorization](authentication-authorization.yml) section for more information.

### Custom certificate

Use the following steps to add a custom certificate to your Microsoft Entra ID app registration.

1. If it isn't already, upload your certificate to a Microsoft Key Vault.

1. Add a managed identity on your Static Web App.

For user assigned managed identities, set `keyVaultReferenceIdentity` property on your static site object to the `resourceId` of the user assigned managed identity.

Skip this step if your managed identity is system assigned.

1. Grant the managed identity the following access policies:

- *Secrets*: **Get/List**

- *Certificates*: **Get/List**

1. Update the auth config section of the `azureActiveDirectory` configuration section with a `clientSecretCertificateKeyVaultReference` value as shown in the following example:

```json

{

"auth": {

"rolesSource": "/api/GetRoles",

"identityProviders": {

"azureActiveDirectory": {

"userDetailsClaim": "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress",

"registration": {

"openIdIssuer": "https://login.microsoftonline.com/common/v2.0",

"clientIdSettingName": "AZURE_CLIENT_ID",

"clientSecretCertificateKeyVaultReference": "@Microsoft.KeyVault(SecretUri=https://<KEY_VAULT_NAME>.azure.net/certificates/<CERTIFICATE_NAME>/<CERTIFICATE_VERSION_ID>)",

"clientSecretCertificateThumbprint": "*"

}

}

}

}

}

```

Make sure to replace your values in for the placeholders surrounded by `<>`.

In the secret URI, specify the key vault name and certificate name. If you want to pin to a version, include the certificate version, otherwise omit the version to allow the runtime to select the newest version of the certificate.

Set `clientSecretCertificateThumbprint` equal to `*` to always pull the latest version of the certificates thumbprint.

# [Apple](#tab/apple)

To create the registration, begin by creating the following [application settings](application-settings.yml):

| Setting Name | Value |

| --- | --- |

| `APPLE_CLIENT_ID` | The Apple client ID. |

| `APPLE_CLIENT_SECRET_APP_SETTING_NAME` | The name of the application setting that holds the Apple client secret. |

Next, use the following sample to configure the provider in the [configuration file](configuration.md).

```json

{

"auth": {

"identityProviders": {

"apple": {

"registration": {

"clientIdSettingName": "APPLE_CLIENT_ID",

"clientSecretSettingName": "APPLE_CLIENT_SECRET_APP_SETTING_NAME"

}

}

}

}

}

```

For more information on how to configure Apple as an authentication provider, see the [App Service Authentication/Authorization documentation](../app-service/configure-authentication-provider-apple.md).

# [Facebook](#tab/facebook)

To create the registration, begin by creating the following [application settings](application-settings.yml):

| Setting Name | Value |

| --- | --- |

| `FACEBOOK_APP_ID` | The Facebook application ID. |

| `FACEBOOK_APP_SECRET_APP_SETTING_NAME` | The name of the application setting that holds the Facebook application secret. |

Next, use the following sample to configure the provider in the [configuration file](configuration.md).

```json

{

"auth": {

"identityProviders": {

"facebook": {

"registration": {

"appIdSettingName": "FACEBOOK_APP_ID",

"appSecretSettingName": "FACEBOOK_APP_SECRET_APP_SETTING_NAME"

}

}

}

}

}

```

For more information on how to configure Facebook as an authentication provider, see the [App Service Authentication/Authorization documentation](../app-service/configure-authentication-provider-facebook.md).

# [GitHub](#tab/github)

To create the registration, begin by creating the following [application settings](application-settings.yml):

| Setting Name | Value |

| --- | --- |

| `GITHUB_CLIENT_ID` | The GitHub client ID. |

| `GITHUB_CLIENT_SECRET_APP_SETTING_NAME` | The name of the application setting that holds the GitHub client secret. |

Next, use the following sample to configure the provider in the [configuration file](configuration.md).

```json

{

"auth": {

"identityProviders": {

"github": {

"registration": {

"clientIdSettingName": "GITHUB_CLIENT_ID",

"clientSecretSettingName": "GITHUB_CLIENT_SECRET_APP_SETTING_NAME"

}

}

}

}

}

```

# [Google](#tab/google)

To create the registration, begin by creating the following [application settings](application-settings.yml):

| Setting Name | Value |

| --- | --- |

| `GOOGLE_CLIENT_ID` | The Google client ID. |

| `GOOGLE_CLIENT_SECRET_APP_SETTING_NAME` | The name of the application setting that holds the Google client secret. |

Next, use the following sample to configure the provider in the [configuration file](configuration.md).

```json

{

"auth": {

"identityProviders": {

"google": {

"registration": {

"clientIdSettingName": "GOOGLE_CLIENT_ID",

"clientSecretSettingName": "GOOGLE_CLIENT_SECRET_APP_SETTING_NAME"

}

}

}

}

}

```

For more information on how to configure Google as an authentication provider, see the [App Service Authentication/Authorization documentation](../app-service/configure-authentication-provider-google.md).

# [X](#tab/x)

To create the registration, begin by creating the following [application settings](application-settings.yml):

| Setting Name | Value |

| --- | --- |

| `X_CONSUMER_KEY` | The X consumer key. |

| `X_CONSUMER_SECRET_APP_SETTING_NAME` | The name of the application setting that holds the X consumer secret. |

Next, use the following sample to configure the provider in the [configuration file](configuration.md).

```json

{

"auth": {

"identityProviders": {

"twitter": {

"registration": {

"consumerKeySettingName": "X_CONSUMER_KEY",

"consumerSecretSettingName": "X_CONSUMER_SECRET_APP_SETTING_NAME"

}

}

}

}

}

```

For more information on how to configure X as an authentication provider, see the [App Service Authentication/Authorization documentation](../app-service/configure-authentication-provider-twitter.md).

# [OpenID Connect](#tab/openid-connect)

You can configure Azure Static Web Apps to use a custom authentication provider that adheres to the [OpenID Connect (OIDC) specification](https://openid.net/connect/). The following steps are required to use a custom OIDC provider.

- One or more OIDC providers are allowed.

- Each provider must have a unique name in the configuration.

- Only one provider can serve as the default redirect target.

### Register your application with the identity provider

You're required to register your application's details with an identity provider. Check with the provider regarding the steps needed to generate a **client ID** and **client secret** for your application.

Once the application is registered with the identity provider, create the following application secrets in the [application settings](application-settings.yml) of the Static Web App:

| Setting Name | Value |

| --- | --- |

| `MY_PROVIDER_CLIENT_ID` | The client ID generated by the authentication provider for your static web app. |

| `MY_PROVIDER_CLIENT_SECRET_APP_SETTING_NAME` | The  name of the application setting that holds the client secret generated by the authentication provider's custom registration for your static web app. |

If you register other providers, each one needs an associated client ID and client secret store in application settings.

> [!IMPORTANT]

> Application secrets are sensitive security credentials. Do not share this secret with anyone, distribute it within a client application, or check into source control.

Once you have the registration credentials, use the following steps to create a custom registration.

1. You need the OpenID Connect metadata for the provider. This information is often exposed via a [configuration metadata document](https://openid.net/specs/openid-connect-discovery-1_0.html#ProviderConfig), which is the provider's _Issuer URL_ suffixed with `/.well-known/openid-configuration`. Gather this configuration URL.

1. Add an `auth` section of the [configuration file](configuration.md) with a configuration block for the OIDC providers, and your provider definition.

```json

{

"auth": {

"identityProviders": {

"customOpenIdConnectProviders": {

"myProvider": {

"registration": {

"clientIdSettingName": "MY_PROVIDER_CLIENT_ID",

"clientCredential": {

"clientSecretSettingName": "MY_PROVIDER_CLIENT_SECRET_APP_SETTING_NAME"

},

"openIdConnectConfiguration": {

"wellKnownOpenIdConfiguration": "https://<PROVIDER_ISSUER_URL>/.well-known/openid-configuration"

}

},

"login": {

"nameClaimType": "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name",

"scopes": [],

"loginParameterNames": []

}

}

}

}

}

}

```

- The provider name, `myProvider` in this example, is the unique identifier used by Azure Static Web Apps.

- Make sure to replace `<PROVIDER_ISSUER_URL>` with the path to the _Issuer URL_ of the provider.

- The `login` object allows you to provide values for: custom scopes, log in parameters, or custom claims.

---

## Authentication callbacks

Identity providers require a redirect URL to complete the login or logout request. Most providers require that you add the callback URLs to an allowlist. The following endpoints are available as redirect destinations.

| Type   | URL pattern                                                 |

| ------ | ----------------------------------------------------------- |

| Login  | `https://<YOUR_SITE>/.auth/login/<PROVIDER_NAME_IN_CONFIG>/callback`  |

| Logout | `https://<YOUR_SITE>/.auth/logout/<PROVIDER_NAME_IN_CONFIG>/callback` |

If you're using Microsoft Entra ID, use `aad` as the value for the `<PROVIDER_NAME_IN_CONFIG>` placeholder.

> [!Note]

> These URLs are provided by Azure Static Web Apps to receive the response from the authentication provider, you don't need to create pages at these routes.

## Login, logout, and user details

To use a custom identity provider, use the following URL patterns.

| Action             | Pattern                                  |

| ------------------ | ---------------------------------------- |

| Login              | `/.auth/login/<PROVIDER_NAME_IN_CONFIG>` |

| Logout             | `/.auth/logout`                          |

| User details       | `/.auth/me`                              |

| Purge user details | `/.auth/purge/<PROVIDER_NAME_IN_CONFIG>` |

If you're using Microsoft Entra ID, use `aad` as the value for the `<PROVIDER_NAME_IN_CONFIG>` placeholder.

## Manage roles

Every user who accesses a static web app belongs to one or more roles. There are two built-in roles that users can belong to:

- **anonymous**: All users automatically belong to the _anonymous_ role.

- **authenticated**: All users who are signed in belong to the _authenticated_ role.

Beyond the built-in roles, you can assign custom roles to users, and reference them in the _staticwebapp.config.json_ file.

# [Invitations](#tab/invitations)

### Add a user to a role

To add a user to a role, you generate invitations that allow you to associate users to specific roles. Roles are defined and maintained in the _staticwebapp.config.json_ file.

<a name="invitations" id="invitations"></a>

#### Create an invitation

Invitations are specific to individual authorization-providers, so consider the needs of your app as you select which providers to support. Some providers expose a user's email address, while others only provide the site's username.

<a name="provider-user-details" id="provider-user-details"></a>

| Authorization provider | Exposes |

| ---------------------- | ---------------- |

| Microsoft Entra ID | email address    |

| GitHub                 | username         |

| X                | username         |

Use the following steps to create an invitation.

1. Go to a Static Web Apps resource in the [Azure portal](https://portal.azure.com).

2. Under _Settings_, select **Role Management**.

3. Select **Invite**.

4. Select an _Authorization provider_ from the list of options.

5. Add either the username or email address of the recipient in the _Invitee details_ box.

- For GitHub and X, enter the username. For all others, enter the recipient's email address.

6. Select the domain of your static site from the _Domain_ drop-down menu.

- The domain you select is the domain that appears in the invitation. If you have a custom domain associated with your site, choose the custom domain.

7. Add a comma-separated list of role names in the _Role_ box.

8. Enter the maximum number of hours you want the invitation to remain valid.

- The maximum possible limit is 168 hours, which is seven days.

9. Select **Generate**.

10. Copy the link from the _Invite link_ box.

11. Email the invitation link to the user that you're granting access to.

When the user selects the link in the invitation, they're prompted to sign in with their corresponding account. Once successfully signed in, the user is associated with the selected roles.

> [!CAUTION]

> Make sure your route rules don't conflict with your selected authentication providers. Blocking a provider with a route rule prevents users from accepting invitations.

### Update role assignments

1. Go to a Static Web Apps resource in the [Azure portal](https://portal.azure.com).

1. Under _Settings_, select **Role Management**.

2. Select the user in the list.

3. Edit the list of roles in the _Role_ box.

4. Select **Update**.

### Remove user

1. Go to a Static Web Apps resource in the [Azure portal](https://portal.azure.com).

1. Under _Settings_, select **Role Management**.

1. Locate the user in the list.

1. Check the checkbox on the user's row.

2. Select **Delete**.

As you remove a user, keep in mind the following items:

- Removing a user invalidates their permissions.

- Worldwide propagation might take a few minutes.

- If the user is added back to the app, the [`userId` changes](user-information.md).

# [Function (preview)](#tab/function)

Instead of using the built-in invitations system, you can use a serverless function to programmatically assign roles to users when they sign in.

To assign custom roles in a function, you can define an API function that is automatically called after each time a user successfully authenticates with an identity provider. The function is passed the user's information from the provider. It must return a list of custom roles that are assigned to the user.

Example uses of this function include:

- Query a database to determine which roles a user should be assigned

- Call the [Microsoft Graph API](https://developer.microsoft.com/graph) to determine a user's roles based on their Active Directory group membership

- Determine a user's roles based on claims returned by the identity provider

> [!NOTE]

> The ability to assign roles via a function is only available when [custom authentication](authentication-custom.md) is configured.

>

> When this feature is enabled, any roles assigned via the built-in invitations system are ignored.

### Configure a function for assigning roles

To configure Static Web Apps to use an API function as the role assignment function, add a `rolesSource` property to the `auth` section of your app's [configuration file](configuration.md). The value of the `rolesSource` property is the path to the API function.

```json

{

"auth": {

"rolesSource": "/api/GetRoles",

"identityProviders": {

// ...

}

}

}

```

> [!NOTE]

> Once configured, the role assignment function can no longer be accessed by external HTTP requests.

### Create a function for assigning roles

After you define the `rolesSource` property in your app's configuration, add an [API function](apis-functions.md) in your static web app at the specified path. You can use a managed function app or [bring your own function app](functions-bring-your-own.md).

Each time a user successfully authenticates with an identity provider, the POST method calls the specified function. The function passes a JSON object in the request body that contains the user's information from the provider. For some identity providers, the user information also includes an `accessToken` that the function can use to make API calls using the user's identity.

See the following example payload from Microsoft Entra ID:

```json

{

"identityProvider": "aad",

"userId": "00aa00aa-bb11-cc22-dd33-44ee44ee44ee",

"userDetails": "ellen@contoso.com",

"claims": [

{

"typ": "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress",

"val": "ellen@contoso.com"

},

{

"typ": "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname",

"val": "Contoso"

},

{

"typ": "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname",

"val": "Ellen"

},

{

"typ": "name",

"val": "Ellen Contoso"

},

{

"typ": "http://schemas.microsoft.com/identity/claims/objectidentifier",

"val": "7da753ff-1c8e-4b5e-affe-d89e5a57fe2f"

},

{

"typ": "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier",

"val": "00aa00aa-bb11-cc22-dd33-44ee44ee44ee"

},

{

"typ": "http://schemas.microsoft.com/identity/claims/tenantid",

"val": "3856f5f5-4bae-464a-9044-b72dc2dcde26"

},

{

"typ": "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name",

"val": "ellen@contoso.com"

},

{

"typ": "ver",

"val": "1.0"

}

],

"accessToken": "eyJ0eXAiOiJKV..."

}

```

The function can use the user's information to determine which roles to assign to the user. It must return an HTTP 200 response with a JSON body containing a list of custom role names to assign to the user.

For example, to assign the user to the `Reader` and `Contributor` roles, return the following response:

```json

{

"roles": [

"Reader",

"Contributor"

]

}

```

If you don't want to assign any other roles to the user, return an empty `roles` array.

To learn more, see [Tutorial: Assign custom roles with a function and Microsoft Graph](assign-roles-microsoft-graph.md).

---

## Next steps

> [!div class="nextstepaction"]

> [Set user roles programmatically](./assign-roles-microsoft-graph.md)


# Private Endpoint

# Configure private endpoint in Azure Static Web Apps

You can use a private endpoint (also called private link) to restrict access to your static web app so that it is only accessible from your private network.

## How it works

An Azure Virtual Network (VNet) is a network just like you might have in a traditional data center, but resources within the VNet talk to each other securely on the Microsoft backbone network.

Configuring Static Web Apps with a private endpoint allows you to use a private IP address from your VNet. Once this link is created, your static web app is integrated into your VNet. As a result, your static web app is no longer available to the public internet, and is only accessible from machines within your Azure VNet.

> [!NOTE]

> Placing your application behind a private endpoint means your app is only available in the region where your VNet is located. As a result, your application is no longer available across multiple points of presence.

If your app has a private endpoint enabled, the server responds with a `403` status code if the request comes from a public IP address. This behavior applies to both the production environment as well as any staging environments. The only way to reach the app is to use the private endpoint deployed within your VNet.

The default DNS resolution of the static web app still exists and routes to a public IP address. The private endpoint exposes 2 IP Addresses within your VNet, one for the production environment and one for any staging environments. To ensure your client is able to reach the app correctly, make sure your client resolves the hostname of the app to the appropriate IP address of the private endpoint. This is required for the default hostname as well as any custom domains configured for the static web app. This resolution is done automatically if you select a private DNS zone when creating the private endpoint (see example below) and is the recommended solution.

If you are connecting from on-prem or do not wish to use a private DNS zone, manually configure the DNS records for your application so that requests are routed to the appropriate IP address of the private endpoint. You can find more information on private endpoint DNS resolution [here](../private-link/private-endpoint-dns.md).

> [!NOTE]

> Private endpoints restrict the incoming traffic going to the website to a specific virtual network. They do not apply to deployments of new site assets.

## Prerequisites

- An Azure account with an active subscription.

- [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- An [Azure VNet](../virtual-network/quick-create-portal.md).

- An application deployed with [Azure Static Web Apps](./get-started-portal.md) that uses the Standard hosting plan.

## Create a private endpoint

In this section, you create a private endpoint for your static web app.

> [!IMPORTANT]

> Your static web app must be deployed on the Standard hosting plan to use Private endpoints. You can change the hosting plan from the **Hosting Plan** option in the side menu.

1. In the portal, open your static web app.

2. Select the **Private Endpoints** option from the side menu.

3. Select **Add**.

4. In the "Add Private Endpoint" dialog, enter this information:

| Setting                         | Value                         |

| ------------------------------- | ----------------------------- |

| Name                            | Enter **myPrivateEndpoint**.  |

| Subscription                    | Select your subscription.     |

| Virtual Network                 | Select your virtual network.  |

| Subnet                          | Select your subnet.           |

| Integrate with private DNS zone | Leave the default of **Yes**. |

5. Select **Ok**.

> [!NOTE]

> The name of the private DNS zone depends upon the default domain name suffix of the static web app. For example, if the default domain suffix of the app is `3.azurestaticapps.net`, the name of the private DNS zone is `privatelink.3.azurestaticapps.net`. When a new static web app is created, the default domain suffix might be different from the default domain suffix(es) of previous static web apps. If you are using an automated deployment process to create the private DNS zone, you can use the `DefaultHostname` property in your app to programmatically extract the domain suffix. The `DefaultHostname` property value resembles `<STATIC_WEB_APP_DEFAULT_DOMAIN_PREFIX>.<PARTITION_ID>.azurestaticapps.net` or `STATIC_WEB_APP_DEFAULT_DOMAIN_PREFIX.azurestaticapps.net`. The default domain suffix resembles `<PARTITION_ID>.azurestaticapps.net` or `azurestaticapps.net`.

## Testing your private endpoint

Since your application is no longer publicly available, the only way to access it is from inside of your virtual network. To test, set up a virtual machine inside of your virtual network and go to your site.

## Next steps

> [!div class="nextstepaction"]

> [Learn more about private endpoints](../private-link/private-endpoint-overview.md)


# Key Vault Secrets

# Secure authentication secrets in Azure Key Vault for Azure Static Web Apps

When configuring custom authentication providers, you may want to store connection secrets in Azure Key Vault. This article demonstrates how to use a managed identity to grant Azure Static Web Apps access to Key Vault for custom authentication secrets.

> [!NOTE]

> Azure Serverless Functions do not support direct Key Vault integration. If you require Key Vault integration with your managed Function app, you will need to implement Key Vault access into your app's code.

Security secrets require the following items to be in place.

- Create a system-assigned identity in your static web app.

- Grant the identity access to a Key Vault secret.

- Reference the Key Vault secret from the Static Web Apps application settings.

This article demonstrates how to set up each of these items in production for [bring your own functions applications](./functions-bring-your-own.md).

Key Vault integration is not available for:

- [Staging versions of your static web app](./review-publish-pull-requests.md). Key Vault integration is only supported in the production environment.

- [Static web apps using managed functions](./apis-functions.md).

> [!NOTE]

> Using managed identity is only available in the Azure Static Web Apps Standard plan.

## Prerequisites

- Existing Azure Static Web Apps site using [bring your own functions](./functions-bring-your-own.md).

- Existing Key Vault resource with a secret value.

## Create identity

1. Open your static web apps in the Azure portal.

1. Under _Settings_, select **Identity**.

1. Select the **System assigned** tab.

2. Under the _Status_ label, select **On**.

3. Select **Save**.

4. When the confirmation dialog appears, select **Yes**.

You can now add an access policy to allow your static web app to read Key Vault secrets.

## Add a Key Vault access policy

1. Open your Key Vault resource in the Azure portal.

1. Under the _Settings_ menu, select **Access policies**.

1. Select the link, **Add Access Policy**.

1. From the _Secret permissions_ drop down, select **Get**.

1. Next to the _Select principal_ label, select the **None selected** link.

1. In search box, search for your static web app name.

1. Select the list item that matches your application name.

2. Select **Select**.

3. Select **Add**.

4. Select **Save**.

The access policy is now saved to Key Vault. Next, access the secret's URI to use when associating your static web app to the Key Vault resource.

1. Under the _Settings_ menu, select **Secrets**.

1. Select your desired secret from the list.

1. Select your desired secret version from the list.

2. Select **copy** at end of _Secret Identifier_ text box to copy the secret URI value to the clipboard.

3. Paste this value into a text editor for later use.

## Add application setting

1. Open your Static Web Apps site in the Azure portal.

1. Under the _Settings_ menu, select **Configuration**.

1. Under the _Application settings_ section, select **Add**.

1. Enter a name in the text box for the _Name_ field.

1. Determine the secret value in text box for the _Value_ field.

The secret value is a composite of a few different values. The following template shows how the final string is built.

```text

@Microsoft.KeyVault(SecretUri=<YOUR_KEY_VAULT_SECRET_URI>)

```

For example, a final string would look like the following sample:

```

@Microsoft.KeyVault(SecretUri=https://myvault.vault.azure.net/secrets/mysecret/)

```

Alternatively:

```

@Microsoft.KeyVault(VaultName=myvault;SecretName=mysecret)

```

Use the following steps to build the full secret value.

1. Copy the template from above and paste it into a text editor.

1. Replace `<YOUR_KEY_VAULT_SECRET_URI>` with the Key Vault URI value you set aside earlier.

1. Copy the new full string value.

1. Paste the value into the text box for the _Value_ field.

1. Select **OK**.

1. Select **Save** at the top of the _Application settings_ toolbar.

Now when your custom authentication configuration references your newly created application setting, the value is extracted from Azure Key Vault using your static web app's identity.

## Next Steps

> [!div class="nextstepaction"]

> [Custom authentication](./authentication-custom.md)


# Password Protection

# Configure password protection (preview)

You can use a password to protect your app's pre-production environments or all environments. Scenarios when password protection is useful include:

- Limiting access to your static web app to people who have the password

- Protecting your static web app's staging environments

Password protection is a lightweight feature that offers a limited level of security. To secure your app using an identity provider, use the integrated [Static Web Apps authentication](authentication-authorization.yml). You can also restrict access to your app using [IP restrictions](configuration.md#networking) or a [private endpoint](private-endpoint.md).

## Prerequisites

An existing static web app in the Standard plan.

## Enable password protection

1. Open your static web app in the Azure portal.

1. Under *Settings* menu, select **Configuration**.

1. Select the **General settings** tab.

1. In the *Password protection* section, select **Protect staging environments only** to protect only your app's pre-production environments or select **Protect both production and staging environments** to protect all environments.

1. Enter a password in **Visitor password**. Passwords must be at least eight characters long and contain a capital letter, a lowercase letter, a number, and a symbol.

1. Enter the same password in **Confirm visitor password**.

2. Select **Save**.

When visitors first go to a protected environment, they're prompted to enter the password before they can view the site.

## Next steps

> [!div class="nextstepaction"]

> [Authentication and authorization](./authentication-authorization.yml)


# Assign Roles Microsoft Graph

# Tutorial: Assign custom roles with a function and Microsoft Graph (preview)

This article demonstrates how to use a function to query [Microsoft Graph](https://developer.microsoft.com/graph) and assign custom roles to a user based on their Entra ID group membership.

In this tutorial, you learn to:

- Deploy a static web app.

- Create a Microsoft Entra app registration.

- Set up custom authentication with Microsoft Entra ID.

- Configure a [serverless function](authentication-custom.md#manage-roles) that queries the user's Entra ID group membership and returns a list of custom roles.

> [!NOTE]

> This tutorial requires you to [use a function to assign roles](authentication-custom.md#manage-roles). Function-based role management is currently in preview. The permission level required to complete this tutorial is "User.Read.All".

There's a function named *GetRoles* in the app's API. This function uses the user's access token to query Entra ID from Microsoft Graph. If the user is a member of any groups defined in the app, then the corresponding custom roles are mapped to the user.

## Prerequisites

| Requirement | Comments |

|---|---|

| Active Azure account | If you don't have one, you can [create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). |

| Microsoft Entra permissions | You must have sufficient permissions to create a Microsoft Entra application. |

## Create a GitHub repository

1. Generate a repository based on the roles function template. Go to the following location to create a new repository.

[https://github.com/staticwebdev/roles-function/generate](https://github.com/login?return_to=/staticwebdev/roles-function/generate)

1. Name your repository **my-custom-roles-app**.

1. Select **Create repository from template**.

## Deploy the static web app to Azure

1. In a new browser window, open the [Azure portal](https://portal.azure.com).

1. From the top left corner, select **Create a resource**.

1. In the search box, type **static web apps**.

1. Select **Static Web Apps**.

1. Select **Create**.

1. Configure your static web app with the following information:

| Setting | Value | Notes |

|---|---|---|

| Subscription | Select your Azure subscription. | |

| Resource group | Create a new group named **my-custom-roles-app-group**. | |

| Name | **my-custom-roles-app**  | |

| Plan type | **Standard** | Customizing authentication and assigning roles using a function require the *Standard* plan. |

| Region for API | Select the region closest to you. |

1. In the *Deployment details* section:

| Setting | Value |

|---|---|

| Source | Select **GitHub**. |

| Organization | Select the organization where you generated the repository. |

| Repository | Select **my-custom-roles-app**. |

| Branch | Select **main**. |

1. In the _Build Details_ section, add the configuration details for this app.

| Setting | Value | Notes |

|---|---|---|

| Build presets | Select **Custom**. | |

| App location | Enter **/frontend**. | This folder contains the front end application. |

| API location | **/api** | Folder in the repository containing the API functions. |

| Output location | Leave blank. | This app has no build output. |

1. Select **Review + create**.

1. Select **Create** initiate the first deployment.

1. Once the process is complete, select **Go to resource** to open your new static web app.

1. In the overview section, locate your application's **URL**. Copy this value into a text editor to use in upcoming steps to set up Entra authentication.

<a name='create-an-azure-active-directory-application'></a>

## Create a Microsoft Entra application

1. In the Azure portal, search for and go to *Microsoft Entra ID*.

1. From the *Manage* menu, select **App registrations**.

1. Select **New registration** to open the *Register an application* window. Enter the following values:

| Setting | Value | Notes |

|---|---|---|

| Name | Enter **MyStaticWebApp**. | |

| Supported account types | Select **Accounts in this organizational directory only**. ||

| Redirect URI | Select **Web** and enter the Microsoft Entra [authentication callback](authentication-custom.md#authentication-callbacks) URL of your static web app. Replace `<YOUR_SITE_URL>` in `<YOUR_SITE_URL>/.auth/login/aad/callback` with the URL of your static web app. | This URL is what you  copied to a text editor in an earlier step. |

1. Select **Register**.

1. After the app registration is created, copy the **Application (client) ID** and **Directory (tenant) ID** in the *Essentials* section to a text editor.

You need these values to configure Entra ID authentication in your static web app.

### Enable ID tokens

1. From the app registration settings, select **Authentication** under *Manage*.

1. In the *Implicit grant and hybrid flows* section, select **ID tokens (used for implicit and hybrid flows)**.

The Static Web Apps runtime requires this configuration to authenticate your users.

1. Select **Save**.

### Create a client secret

1. In the app registration settings, select **Certificates & secrets** under *Manage*.

1. In the *Client secrets* section, select **New client secret**.

1. For the *Description* field, enter **MyStaticWebApp**.

1. For the *Expires* field, leave the default value of _6 months_.

> [!NOTE]

> You must rotate the secret before the expiration date by generating a new secret and updating your app with its value.

1. Select **Add**.

1. Copy the **Value** of the client secret you created to a text editor.

You need this value to configure Entra ID authentication in your static web app.

## Configure Entra ID authentication

1. In a browser, open the GitHub repository containing the static web app you deployed.

Go to the app's configuration file at *frontend/staticwebapp.config.json*. This file contains the following section:

```json

"auth": {

"rolesSource": "/api/GetRoles",

"identityProviders": {

"azureActiveDirectory": {

"userDetailsClaim": "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name",

"registration": {

"openIdIssuer": "https://login.microsoftonline.com/<YOUR_ENTRA_TENANT_ID>",

"clientIdSettingName": "ENTRA_CLIENT_ID",

"clientSecretSettingName": "ENTRA_CLIENT_SECRET"

},

"login": {

"loginParameters": [

"resource=https://graph.microsoft.com"

]

}

}

}

},

```

This configuration is made up of the following settings:

| Properties | Description |

|---|---|

| `rolesSource` | The URL where the login process gets a list of available roles. For the sample application the URL is `/api/GetRoles`. |

| `userDetailsClaim` | The URL of the schema used to validate the login request. |

| `openIdIssuer` | The Microsoft Entra login route, appended with your tenant ID. |

| `clientIdSettingName` | Your Microsoft Entra client ID. |

| `clientSecretSettingName` | Your Microsoft Entra client secret value. |

| `loginParameters` | To obtain an access token for Microsoft Graph, the `loginParameters` field must be configured with `resource=https://graph.microsoft.com`. |

1. Select **Edit** to update the file.

1. Update the *openIdIssuer* value of `https://login.microsoftonline.com/<YOUR_ENTRA_TENANT_ID>` by replacing `<YOUR_ENTRA_TENANT_ID>` with the directory (tenant) ID of your Microsoft Entra ID.

1. Select **Commit changes...**.

1. Enter a commit message, and select **Commit changes**.

Committing these changes initiates a GitHub Actions run to update the static web app.

1. Go to your static web app resource in the Azure portal.

1. Select **Configuration** in the menu bar.

1. In the *Application settings* section, add the following settings:

| Name | Value |

|---|---|

| `ENTRA_CLIENT_ID` | Your Entra ID application (client) ID. |

| `ENTRA_CLIENT_SECRET` | Your Entra application client secret value. |

1. Select **Save**.

## Create roles

1. Open you Entra ID app registration in the Azure portal.

1. Under *Manage*, select **App roles**.

1. Select **Create app role** and enter the following values:

| Setting | Value |

|---|---|

| Display name | Enter **admin**. |

| Allowed member types | Select **Users/Groups**. |

| Value | Enter **admin**. |

| Description | Enter **Administrator**. |

1. Check the box for **Do you want to enable this app role?**

1. Select **Apply**.

1. Now repeat the same process for a role named **reader**.

1. Copy the *ID* values for each role and set them aside in a text editor.

## Verify custom roles

The sample application contains an API function (*api/GetRoles/index.js*) that queries Microsoft Graph to determine if a user is in a predefined group.

Based on the user's group memberships, the function assigns custom roles to the user. The application is configured to restrict certain routes based on these custom roles.

1. In your GitHub repository, go to the *GetRoles* function located at *api/GetRoles/index.js*.

Near the top, there's a `roleGroupMappings` object that maps custom user roles to Microsoft Entra groups.

1. Select **Edit**.

1. Update the object with group IDs from your Microsoft Entra tenant.

For instance, if you have groups with IDs `6b0b2fff-53e9-4cff-914f-dd97a13bfbd6` and `b6059db5-9cef-4b27-9434-bb793aa31805`, you would update the object to:

```js

const roleGroupMappings = {

'admin': '6b0b2fff-53e9-4cff-914f-dd97a13bfbd6',

'reader': 'b6059db5-9cef-4b27-9434-bb793aa31805'

};

```

The *GetRoles* function is called whenever a user is successfully authenticated with Microsoft Entra ID. The function uses the user's access token to query their Entra group membership from Microsoft Graph. If the user is a member of any groups defined in the `roleGroupMappings` object, then the corresponding custom roles are returned.

In the above example, if a user is a member of the Entra ID group with ID `b6059db5-9cef-4b27-9434-bb793aa31805`, they're granted the `reader` role.

1. Select **Commit changes...**.

1. Add a commit message and select **Commit changes**.

Making these changes initiates a build in to update the static web app.

1. When the deployment is complete, you can verify your changes by navigating to the app's URL.

1. Sign in to your static web app using Microsoft Entra ID.

1. When you're logged in, the sample app displays the list of roles that you're assigned based on your identity's Entra ID group membership.

Depending on these roles, you're permitted or prohibited to access some of the routes in the app.

> [!NOTE]

> Some queries against Microsoft Graph return multiple pages of data. When more than one query request is required, Microsoft Graph returns an `@odata.nextLink` property in the response which contains a URL to the next page of results. For more information, see [Paging Microsoft Graph data in your app](/graph/paging)

## Clean up resources

Clean up the resources you deployed by deleting the resource group.

1. From the Azure portal, select **Resource group** from the left menu.

1. Enter the resource group name in the **Filter by name** field.

1. Select the resource group name you used in this tutorial.

1. Select **Delete resource group** from the top menu.

## Next steps

> [!div class="nextstepaction"]

> [Authentication and authorization](./authentication-authorization.yml)


# Local Development

# Set up local development for Azure Static Web Apps

When published to the cloud, an Azure Static Web Apps site links together many services that work together as if they're the same application. These services include:

- The static web app

- Azure Functions API

- Authentication and authorization services

- Routing and configuration services

These services must communicate with each other, and Azure Static Web Apps handles this integration for you in the cloud.

However, when you run your application locally these services aren't automatically tied together.

To provide a similar experience as to what you get in Azure, the [Azure Static Web Apps CLI](https://github.com/Azure/static-web-apps-cli) provides the following services:

- A local static site server

- A proxy to the front-end framework development server

- A proxy to your API endpoints - available through Azure Functions Core Tools

- A mock authentication and authorization server

- Local routes and configuration settings enforcement

> [!NOTE]

> Often sites built with a front-end framework require a proxy configuration setting to correctly handle requests under the `api` route. When using the Azure Static Web Apps CLI the proxy location value is `/api`, and without the CLI the value is `http://localhost:7071/api`.

[!INCLUDE [Local development overview](../../includes/static-web-apps-local-dev-overview.md)]

The following article details the steps for running a node-based application, but the process is the same for any language or environment.

## Prerequisites

- **Existing Azure Static Web Apps site**: If you don't have one, begin with the [vanilla-api](https://github.com/staticwebdev/vanilla-api/generate?return_to=/staticwebdev/vanilla-api/generate) starter app.

- **[Node.js](https://nodejs.org) with npm**: Run the [Node.js LTS](https://nodejs.org) version, which includes access to [npm](https://www.npmjs.com/).

- **[Visual Studio Code](https://code.visualstudio.com/)**: Used for debugging the API application, but not required for the CLI.

## Get started

Open a terminal to the root folder of your existing Azure Static Web Apps site.

1. Install the CLI.

```console

npm install -D @azure/static-web-apps-cli

```

> [!TIP]

> If you want to install the SWA CLI globally, use `-g` in place of `-D`. It is highly recommended, however, to install SWA as a development dependency.

1. Build your app if required by your application.

Run `npm run build`, or the equivalent command for your project.

1. Initialize the repository for the CLI.

```console

swa init

```

Answer the questions posed by the CLI to verify your configuration settings are correct.

1. Start the CLI.

```console

swa start

```

1. Go to `http://localhost:4280` to view the app in the browser.

### Other ways to start the CLI

| Description | Command | Comments |

|--|--|--|

| Serve a specific folder | `swa start ./<OUTPUT_FOLDER_NAME>` | Replace `<OUTPUT_FOLDER_NAME>` with the name of your output folder. |

| Use a running framework development server | `swa start http://localhost:3000` | This command works when you have an instance of your application running under port `3000`. Update the port number if your configuration is different. |

| Start a Functions app in a folder | `swa start ./<OUTPUT_FOLDER_NAME> --api-location ./api` | Replace `<OUTPUT_FOLDER_NAME>` with the name of your output folder. This command expects your application's API to have files in the `api` folder. Update this value if your configuration is different. |

| Use a running Functions app | `swa start ./<OUTPUT_FOLDER_NAME> --api-location http://localhost:7071` | Replace `<OUTPUT_FOLDER_NAME>` with the name of your output folder. This command expects your Azure Functions application to be available through port `7071`. Update the port number if your configuration is different. |

## Authorization and authentication emulation

The Static Web Apps CLI emulates the [security flow](./authentication-authorization.yml) implemented in Azure. When a user logs in, you can define a fake identity profile returned to the app.

For instance, when you try to go to `/.auth/login/github`, a page is returned that allows you to define an identity profile.

> [!NOTE]

> The emulator works with any security provider, not just GitHub.

The emulator provides a page allowing you to provide the following [client principal](./user-information.md#client-principal-data) values:

| Value | Description |

| --- | --- |

| **Username** | The account name associated with the security provider. This value appears as the `userDetails` property in the client principal and is autogenerated if you don't provide a value. |

| **User ID** | Value autogenerated by the CLI.  |

| **Roles** | A list of role names, where each name is on a new line.  |

| **Claims** | A list of [user claims](user-information.md#client-principal-data), where each name is on a new line.  |

Once logged in:

- You can use the `/.auth/me` endpoint, or a function endpoint to retrieve the user's [client principal](./user-information.md).

- Navigating to `/.auth/logout` clears the client principal and signs out the mock user.

## Debugging

There are two debugging contexts in a static web app. The first is for the static content site, and the second is for API functions. Local debugging is possible by allowing the Static Web Apps CLI to use development servers for one or both of these contexts.

The following steps show you a common scenario that uses development servers for both debugging contexts.

1. Start the static site development server. This command is specific to the front-end framework you're using, but often comes in the form of commands like `npm run build`, `npm start`, or `npm run dev`.

1. Open the API application folder in Visual Studio Code and start a debugging session.

1. Start the Static Web Apps CLI using the following command.

```console

swa start http://localhost:<DEV-SERVER-PORT-NUMBER> --appDevserverUrl http://localhost:7071

```

Replace `<DEV_SERVER_PORT_NUMBER>` with the development server's port number.

The following screenshots show the terminals for a typical debugging scenario:

The static content site is running via `npm run dev`.

The Azure Functions API application is running a debug session in Visual Studio Code.

The Static Web Apps CLI is launched using both development servers.

Now requests that go through port `4280` are routed to either the static content development server, or the API debugging session.

For more information on different debugging scenarios, with guidance on how to customize ports and server addresses, see the [Azure Static Web Apps CLI repository](https://github.com/Azure/static-web-apps-cli).

### Sample debugging configuration

Visual Studio Code uses a file to enable debugging sessions in the editor. If Visual Studio Code doesn't generate a *launch.json* file for you, you can place the following configuration in *.vscode/launch.json*.

```json

{

"version": "0.2.0",

"configurations": [

{

"name": "Attach to Node Functions",

"type": "node",

"request": "attach",

"port": 9229,

"preLaunchTask": "func: host start"

}

]

}

```

## Next steps

> [!div class="nextstepaction"]

> [Configure your application](configuration.md)


# Static Web Apps Cli Overview

# Azure Static Web Apps CLI overview

[!INCLUDE [Required version](includes/static-web-apps-cli-required-version.md)]

Azure Static Web Apps websites are hosted in the cloud and often connect together a collection of cloud services. During development, and any time you need to run your app locally, you need tools to mimic how your app runs in the cloud.

The Static Web Apps CLI (SWA CLI) includes a series of local services that approximate how your app would run on Azure, but instead they run exclusively on your machine.

The Azure Static Web Apps CLI provides the following services:

- A local static site server

- A proxy to the front-end framework development server

- A proxy to your API endpoints - available through Azure Functions Core Tools

- A mock authentication and authorization server

- Local routes and configuration settings enforcement

[!INCLUDE [Local development overview](../../includes/static-web-apps-local-dev-overview.md)]

## Get started

Get started working with the Static Web Apps CLI with the following resources.

| Resource | Description |

|---|---|

| [Install the Static Web Apps CLI (SWA CLI)](static-web-apps-cli-install.md) | Install the Azure Static Web Apps CLI to your machine. |

| [Configure your environment](static-web-apps-cli-configuration.md) | Set up how your application reads configuration information. |

| [Start the website emulator](static-web-apps-cli-emulator.md) | Start the service to locally serve your website. |

| [Start the local API server](static-web-apps-cli-api-server.md) | Start the service to locally serve your API endpoints. |

| [Deploy to Azure](static-web-apps-cli-deploy.md) | Deploy your application to production on Azure. |

> [!NOTE]

> Often sites built with a front-end framework require a proxy configuration setting to correctly handle requests under the `api` route. When using the Azure Static Web Apps CLI the proxy location value is `/api`, and without the CLI the value is `http://localhost:7071/api`.

## Next steps

> [!div class="nextstepaction"]

> [Install the CII](static-web-apps-cli-install.md)


# Static Web Apps Cli Install

# Install the Static Web Apps CLI (SWA CLI)

[!INCLUDE [Required version](includes/static-web-apps-cli-required-version.md)]

You have different options available to install the Azure Static Web Apps CLI. The Azure Static Web Apps CLI requires that you have [Node.js](https://nodejs.org/) installed locally. By default, Node.js comes with the Node Package Manager (npm), though you may opt to use other package managers such as [Yarn](https://yarnpkg.com/) or [pnpm](https://pnpm.io/).

| Resource | Command |

|---|---|

| [`npm`](https://docs.npmjs.com/cli/v6/commands/npm-install) | `npm install -g @azure/static-web-apps-cli` |

| [`yarn`](https://classic.yarnpkg.com/lang/en/docs/cli/install/) | `yarn add @azure/static-web-apps-cli` |

| [`pnpm`](https://pnpm.io/cli/install) | `pnpm install -g @azure/static-web-apps-cli` |

> [!NOTE]

> SWA CLI only supports Node versions 16 and below.

## Validate install

Installing the package makes the `swa` command available on your machine. You can verify the installation is successful by requesting the CLI version.

```bash

swa --version

# When installed, the version number is printed out

```

## Usage

To begin using the CLI, you can run the `swa` command alone and follow the interactive prompts.

The SWA CLI interactive prompts help guide you through the different options important as you develop your web app.

Run the `swa` command to begin setting up your application.

```bash

swa

```

The `swa` command generates a configuration file, builds your project, and gives you the option to deploy to Azure.

For details on all the SWA CLI commands, see the [CLI reference](static-web-apps-cli.md).

## Using npx

You can run any Static Web Apps CLI commands directly using npx. For example:

```bash

npx @azure/static-web-apps-cli --version

```

Alternatively, you can start the emulator via the `start` command:

```bash

npx @azure/static-web-apps-cli start

```

## Next steps

> [!div class="nextstepaction"]

> [Start the emulator](static-web-apps-cli-emulator.md)


# Static Web Apps Cli Emulator

# Start the Static Web Apps CLI emulator

[!INCLUDE [Required version](includes/static-web-apps-cli-required-version.md)]

Static Web Apps is a cloud-based platform that hosts and runs your web apps. When you run your app locally, you need special tools to help you approximate how your app would run in the cloud.

The Static Web Apps CLI (SWA CLI) includes an emulator that mimics how your app would run on Azure, but instead runs exclusively on your machine.

The `swa start` command launches the emulator with default settings. By default, the emulator uses port `4280`.

For more information about individual commands, see the [CLI reference](/azure/static-web-apps/static-web-apps-cli#swa-start).

## Serve static files from your filesystem

The SWA CLI allows you to directly serve your static content from your filesystem with no other required tools. You can either serve the static content from your current directory or a specific folder.

| Serve from... | Command | Notes |

|---|---|---|

| Current folder | `swa start` | By default, the CLI starts and serves static content (HTML, image, script, and CSS files) from the current working directory. |

| Specific folder | `swa start ./my-dist` | You can override the behavior to start the emulator with a different static assets folder.  |

## Use development server

As you develop your app's front-end, you might want to use the framework's default development server. Using a framework's server allows you to take advantage of benefits like live reload and hot module replacement (HMR).

For example, Angular developers often use `ng serve` or `npm start` to run the development server.

You can set up the Static Web Apps SWA CLI to proxy requests to the dev server, which gives you the benefits of both your framework's CLI while simultaneously working with Static Web Apps CLI.

There are two steps to using a framework's dev server along with the SWA CLI:

1. Start your framework's local dev server as usual. Make sure to note the URL (including the port) used by the framework.

1. Start the SWA CLI in a new terminal, passing in the dev server URL.

```bash

swa start <DEV_SERVER_URL>

```

> [!NOTE]

> Make sure to replace the `<DEV_SERVER_URL>` placeholder with your own value.

### Launch dev server

You can simplify your workflow further by having the SWA CLI launch the dev server for you.

You can pass a custom command to the `--run` parameter to the `swa start` command.

```bash

swa start <DEV_SERVER_URL> --run <DEV_SERVER_LAUNCH_COMMAND>

```

Here's some examples of starting the emulator with a few different frameworks:

| Framework | Command |

|---|---|

| React | `swa start http://localhost:3000 --run "npm start"` |

| Blazor | `swa start http://localhost:5000 --run "dotnet watch run"` |

| Jekyll | `swa start http://localhost:4000 --run "jekyll serve"` |

You can also use the `--run` parameter if you want to run a custom script as you launch the dev server.

```bash

swa start http://localhost:4200 --run "./startup.sh"

```

Using the above command, you can access the application with the emulated services from `http://localhost:4280`

## Next steps

> [!div class="nextstepaction"]

> [Start the API server](static-web-apps-cli-api-server.md)


# Static Web Apps Cli Api Server

# Start the API server with the Azure Static Web App CLI

[!INCLUDE [Required version](includes/static-web-apps-cli-required-version.md)]

In Azure Static Web Apps, you can use the [integrated managed Functions](/azure/static-web-apps/apis-functions) to add API endpoints to your application. You can run an Azure Functions app locally using [Azure Functions core tools CLI](/azure/azure-functions/functions-run-local). The core tools CLI gives you the opportunity to run and debug your API endpoints locally.

You can start the core tools manually or automatically.

## Manual start

To use the SWA CLI emulator alongside the API server:

1. Start API server using the Azure Functions core tools CLI or the [Visual Studio Code Extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions).

Copy the URL of the local API server, once the core tools are running.

```bash

func host start

```

1. In a separate terminal, start the SWA CLI using the `--api-devserver-url` option to pass it the local API Server URI.

For example:

```bash

swa start ./my-dist --api-devserver-url http://localhost:7071

```

## Automatic start

To set up an automatic start, you first need to have an Azure Functions application project located in an `api` folder in your local development environment.

1. Launch the API server alongside the SWA emulator

```bash

swa start ./my-dist --api-location ./api

```

1. Combine the launch with usage of a running dev server

```bash

swa start http://localhost:3000 --api-location ./api

```

## Next steps

> [!div class="nextstepaction"]

> [Deploy to Azure](static-web-apps-cli-deploy.md)


# Static Web Apps Cli Deploy

# Deploy a static web app with Azure Static Web Apps CLI

[!INCLUDE [Required version](includes/static-web-apps-cli-required-version.md)]

The Azure Static Web Apps CLI (SWA CLI) features the `deploy` command to deploy the current project to Azure Static Web Apps.

Common deployment scenarios include:

- A front-end app without an API

- A front-end app with an API

- Blazor apps

## Deployment token

The SWA CLI supports deploying using a deployment token to enable setups in CI/CD environments.

You can get a deployment token from:

- **Azure portal**: **Home → Static Web App → Your Instance → Overview → Manage deployment token**

- **Azure CLI**: Using the `secrets list` command:

```azstatic-cli

az staticwebapp secrets list --name <APPLICATION_NAME> --query "properties.apiKey"

```

- **Azure Static Web Apps CLI**: Using the `deploy` command:

```azstatic-cli

swa deploy --print-token

```

You can then use the token value with the `--deployment-token <TOKEN>` or you can create an environment variable called `SWA_CLI_DEPLOYMENT_TOKEN` and set it to the deployment token.

> [!IMPORTANT]

> Don't store deployment tokens in a public repository.

## Deploy a front-end app without an API

You can deploy a front-end application without an API to Azure Static Web Apps. If your front-end application requires a build step, run `swa build` or refer to your application build instructions.

Select the option that best suits your needs to configure your deployment

- **Option 1:** From build folder you would like to deploy, run the deploy command:

```azstatic-cli

cd build/

swa deploy

```

> [!NOTE]

> The *build* folder must contain the static content of your app to be deployed.

- **Option 2:** You can also deploy a specific folder:

1. If your front-end application requires a build step, run `swa build` or refer to your application build instructions.

2. Deploy your app:

```azstatic-cli

swa deploy ./my-dist

```

## Deploy a front-end app with an API

Use the following steps to deploy an application that has API endpoints.

1. If your front-end application requires a build step, run `swa build` or refer to your application build instructions.

1. Ensure the API language runtime version in the *staticwebapp.config.json* file is set correctly, for example:

```json

{

"platform": {

"apiRuntime": "node:16"

}

}

```

> [!NOTE]

> If your project doesn't have the *staticwebapp.config.json* file, add one under your `outputLocation` folder.

1. Deploy your app:

```azstatic-cli

swa deploy ./my-dist --api-location ./api

```

### Deploy a Blazor app

You can deploy a Blazor app using the following steps.

1. Build your Blazor app in **Release** mode:

```azstatic-cli

dotnet publish -c Release -o bin/publish

```

1. From the root of your project, run the deploy command:

```azstatic-cli

swa deploy ./bin/publish/wwwroot --api-location ./Api

```

## Deploy using a configuration file

> [!NOTE]

> The path for `outputLocation` must be relative to the `appLocation`.

If you're using a [`swa-cli.config.json`](./static-web-apps-cli-configuration.md) configuration file in your project with a single configuration entry, then you can deploy your application by running the following steps.

For reference, an example of a single configuration entry looks like the following code snippet.

```json

{

"configurations": {

"my-app": {

"appLocation": "./",

"apiLocation": "api",

"outputLocation": "frontend",

"start": {

"outputLocation": "frontend"

},

"deploy": {

"outputLocation": "frontend"

}

}

}

}

```

1. If your front-end application requires a build step, run `swa build` or refer to your application build instructions.

2. Deploy your app.

```azstatic-cli

swa deploy

```

If you have multiple configuration entries, you can provide the entry ID to specify which one to use:

```azstatic-cli

swa deploy my-otherapp

```

## Options

The following are options you can use with `swa deploy`:

- `-a, --app-location <path>`: the folder containing the source code of the front-end application (default: "`.`")

- `-i, --api-location <path>`: the folder containing the source code of the API application

- `-O, --output-location <path>`: the folder containing the built source of the front-end application. The path is relative to `--app-location` (default: "`.`")

- `-w, --swa-config-location <swaConfigLocation>`: the directory where the staticwebapp.config.json file is located

- `-d, --deployment-token <secret>`: the secret token used to authenticate with the Static Web Apps

- `-dr, --dry-run`: simulate a deploy process without actually running it (default: `false`)

- `-pt, --print-token`: print the deployment token (default: `false`)

- `--env [environment]`: the type of deployment environment where to deploy the project (default: "`preview`")

- `-S, --subscription-id <subscriptionId>`: Azure subscription ID used by this project (default: `process.env.AZURE_SUBSCRIPTION_ID`)

- `-R, --resource-group <resourceGroupName>`: Azure resource group used by this project

- `-T, --tenant-id <tenantId>`: Azure tenant ID (default: `process.env.AZURE_TENANT_ID`)

- `-C, --client-id <clientId>`: Azure client ID

- `-CS, --client-secret <clientSecret>`: Azure client secret

- `-n, --app-name <appName>`: Azure Static Web App application name

- `-cc, --clear-credentials`: clear persisted credentials before sign in (default: `false`)

- `-u, --use-keychain`: enable using the operating system native keychain for persistent credentials (default: `true`)

- `-nu, --no-use-keychain`: disable using the operating system native keychain

- `-h, --help`: display help for command

## Usage

Deploy using a deployment token.

```azstatic-cli

swa deploy ./dist/ --api-location ./api/ --deployment-token <TOKEN>

```

Deploy using a deployment token from the environment variables.

```azstatic-cli

SWA_CLI_DEPLOYMENT_TOKEN=123 swa deploy ./dist/ --api-location ./api/

```

Deploy using `swa-cli.config.json` file

```azstatic-cli

swa deploy

swa deploy myconfig

```

Print the deployment token.

```azstatic-cli

swa deploy --print-token

```

Deploy to a specific environment.

```azstatic-cli

swa deploy --env production

```

## Next steps

> [!div class="nextstepaction"]

> [Configure your deployment](static-web-apps-cli-configuration.md)


# Static Web Apps Cli Configuration

# Configure the Azure Static Web Apps CLI

[!INCLUDE [Required version](includes/static-web-apps-cli-required-version.md)]

The Azure Static Web Apps (SWA) CLI gets configuration information for your static web app in one of two ways:

- CLI options (passed in at runtime)

- A CLI configuration file named *swa-cli.config.json*

> [!NOTE]

> By default, the SWA CLI looks for a configuration file named *swa-cli.config.json* in the current directory.

The configuration file can contain multiple configurations, each identified by a unique configuration name.

- If only a single configuration is present in the *swa-cli.config.json* file, `swa start` uses it by default.

- If options are loaded from a config file, then command line options are ignored.

## Example configuration file

The following code snippet shows the configuration file's shape.

```json

{

"configurations": {

"app": {

"appDevserverUrl": "http://localhost:3000",

"apiLocation": "api",

"run": "npm run start",

"swaConfigLocation": "./my-app-source"

}

}

}

```

When you only have one configuration section, as shown by this example, then the `swa start` command automatically uses these values.

## Initialize a configuration file

You can initialize your configuration file with the `swa init` command. If you run the command against an existing project, then `swa init` tries to guess the configuration settings for you.

By default, the process creates these settings in a *swa-cli.config.json* in the current working directory of your project. This directory is the default file name and location used by `swa` when searching for project configuration values.

```azstatic-cli

swa --config <PATH>

```

If the file contains only one named configuration, then that configuration is used by default. If multiple configurations are defined, then you pass the desired configuration name in as an option.

```azstatic-cli

swa --<CONFIG_NAME>

```

When the configuration file option is used, the settings are stored in JSON format. Once created, you can manually edit the file to update settings or use `swa init` to make updates.

## View configuration

The Static Webs CLI provides a `--print-config` option so you can review your current configuration.

Here's an example of what that output looks like when run on a new project with default settings.

```azstatic-cli

swa --print-config

Options:

- port: 4280

- host: localhost

- apiPort: 7071

- appLocation: .

- apiLocation: <undefined>

- outputLocation: .

- swaConfigLocation: <undefined>

- ssl: false

- sslCert: <undefined>

- sslKey: <undefined>

- appBuildCommand: <undefined>

- apiBuildCommand: <undefined>

- run: <undefined>

- verbose: log

- serverTimeout: 60

- open: false

- githubActionWorkflowLocation: <undefined>

- env: preview

- appName: <undefined>

- dryRun: false

- subscriptionId: <undefined>

- resourceGroupName: <undefined>

- tenantId: <undefined>

- clientId: <undefined>

- clientSecret: <undefined>

- useKeychain: true

- clearCredentials: false

- config: swa-cli.config.json

- printConfig: true

```

Running `swa --print-config` provide's the current configuration defaults.

> [!NOTE]

> If the project has not yet defined a configuration file, this automatically triggers the `swa init` workflow to help you create one.

## Validate configuration

You can validate the *swa-cli.config.json* file against the following schema: https://aka.ms/azure/static-web-apps-cli/schema


# Static Web Apps Cli

# Azure Static Web Apps CLI reference

The reference of Azure Static Web Apps CLI commands.

## Commands

| Command | Description | Type | Status |

|---|---|---|---|

| [swa login](#swa-login) | Log in to Azure. | SWA Core | GA |

| [swa init](#swa-init) | Configures a new Azure Static Web Apps project. | SWA Core | GA |

| [swa build](#swa-build) | Builds the application. If you have a Node.js application, it installs dependencies first. | SWA Core | GA |

| [swa start](#swa-start) | Start the Azure Static Web Apps emulator from a directory or bind to a running dev server. | SWA Core | GA |

| [swa deploy](#swa-deploy) | Deploy the current project to Azure Static Web Apps. | SWA Core | GA |

| [swa db](#swa-db) | Generate and edit your Static Web Apps database connections configuration. | SWA Core | GA |

## Global Parameters

| Parameter | Summary |

|---|---|

| --version, -v | Display the version number. |

| --verbose, --V [level] | Enable verbose output. Level values include `silly`, `info`, `log` (default), and `silent`. |

| --config, -c [path] | Path to the swa-cli.config.json file. |

| --config-name, -cn | Configuration used by the CLI. |

| --print-config, -g | Print all resolved options. Default is `false`. |

| --help, -h | Show context-sensitive help. |

## swa login

Log in to Azure.

Authenticate with Azure to get a deployment token for Azure Static Web Apps, using the `swa deploy` command.

### Syntax

```azstatic-cli

swa login

[--subscription-id]

[--resource-group]

[--tenant-id]

[--client-id]

[--client-secret]

[--app-name]

[--clear-credentials]

[--use-keychain]

[--no-use-keychain]

```

### Examples

#### Example 1: Interactive log in to Azure

```azstatic-cli

swa login

```

### Parameters

___`--subscription-id, -S`___

Azure subscription ID used by this project. The default is `process.env.AZURE_SUBSCRIPTION_ID`.

___`--resource-group, -R`___

Name of resource group. You can configure the default group using `az configure --defaults group=<name>`.

___`--tenant-id, -T`___

Azure tenant ID. The default is `process.env.AZURE_TENANT_ID`.

___`--client-id, -C`___

Azure client ID.

___`--client-secret, -CS`___

Azure client secret.

___`--app-name, -n`___

Azure Static Web Apps app name.

___`--clear-credentials -cc`___

Clear persisted credentials before login. The default is `false`.

___`--use-keychain, -u`___

Use the operating system native keychain for persistent credentials. The default is `true`.

___`--no-use-keychain, -nu`___

Disable use of the operating system native keychain.

___[Global Parameters](#global-parameters)___

## swa init

Configures a new Azure Static Web Apps project.

Configures a new Azure Static Web Apps project with the Static Web Apps CLI. Interactive mode prompts you for a configuration name, detects your project settings and the frameworks used. Once complete, a new static web app is created and a `swa-cli.config.json` file is generated in the current directory.

You can run `swa init` multiple times to create different configurations for your project. You may want to do this if you're working on a monorepo and want to configure different projects.

The generated configuration file is used in every command you run with the Static Web Apps CLI. If you have multiple named configurations, you can use the positional argument or `--config-name` option to specify which configuration you want to use.

The following is an example configuration generated by the `init` command:

```json

{

"$schema": "https://aka.ms/azure/static-web-apps-cli/schema",

"configurations": {

"myApp": {

"appLocation": ".",

"apiLocation": "api",

"outputLocation": "dist",

"appBuildCommand": "npm run build",

"apiBuildCommand": "npm run build --if-present",

"run": "npm run dev",

"appDevserverUrl": "http://localhost:8080"

}

}

}

```

### Syntax

```azstatic-cli

swa init

[--yes]

```

### Examples

#### Example 1: Create a new configuration interactively.

```azstatic-cli

swa init

```

#### Example 2: Create a new configuration using default values for all options.

```azstatic-cli

swa init --yes

```

#### Example 3: Initialize the project using the configuration named "myApp" from the swa-cli.config.json file.

```azstatic-cli

swa init --config-name myApp

```

### Parameters

___`--yes, -y`___

Answers "yes" to all prompts, which disables interactive mode. Default is `false`.

___[Global Parameters](#global-parameters)___

## swa build

Builds the application. If you have a Node.js application, it installs dependencies first.

Common use cases include: Installing dependencies for the front-end app and API and running the build commands for both, only building the front-end or API project if the other doesn't have a build step.

### Syntax

```azstatic-cli

swa build

[--app-location]

[--api-location]

[--output-location]

[--app-build-command]

[--api-build-command]

[--auto]

```

### Examples

#### Example 1: Build the app, and optionally install dependencies.

```azstatic-cli

swa build

```

#### Example 2: Detect how to build your app and run build commands after installing dependencies.

```azstatic-cli

swa build --auto

```

#### Example 3: Install dependencies for the front-end application.

```azstatic-cli

swa build --app-location ./client

```

#### Example 4: Use the configuration named `myApp` in *swa-cli.config.json* to build your front-end application.

```azstatic-cli

swa build myApp

```

### Parameters

___`--app-location, -a`___

The folder containing the source code of the front-end application. Default is `.`.

___`--api-location, -i`___

The folder containing the source code of the API application.

___`--output-location, -O`___

The folder containing the built source of the front-end application. This path is relative to `--app-location`. Default is `.`.

___`--app-build-command, -A`___

Builds the front-end application.

___`--api-build-command, -I`___

Builds the API application.

___`--auto`___

Automatically detects how to build your front-end and API applications. Default is `false`.

___[Global Parameters](#global-parameters)___

## swa start

Start the Azure Static Web Apps emulator from a directory or bind to a running dev server.

### Serve from a folder

By default, the CLI starts and serves any static content from the current working directory `./`:

```azstatic-cli

swa start

```

If the artifact folder of your static app is under a different folder (for example, `./my-dist`), then run the CLI and provide that folder:

```azstatic-cli

swa start ./my-dist

```

### Serve from a dev server

When developing your front-end app locally, it's often useful to use the dev server that comes with your front end framework's CLI. Using the framework CLI allows you to use built-in features like "livereload" and HMR (hot module replacement).

To use SWA CLI with your local dev server, follow these two steps:

1. Start your local dev server as usual. For example, if you are using Angular: `ng serve` (or `npm start`).

1. In a separate terminal, run `swa start` with the URI provided by the dev server, in the following format:

```azstatic-cli

swa start http://<APP_DEV_SERVER_HOST>:<APP_DEV_SERVER_PORT>

```

Here is a list of the default ports and commands used by some popular dev servers:

| Tool | Port | Command |

|--|--|--|

| [Angular](https://angular.io/cli) | `4200` | `swa start http://localhost:4200` |

| [Blazor WebAssembly](https://dotnet.microsoft.com/apps/aspnet/web-apps/blazor) | `5000` | `swa start http://localhost:5000` |

| [Gatsby](https://www.gatsbyjs.com/docs/reference/gatsby-cli/) | `8000` | `swa start http://localhost:8000` |

| [Hugo](https://gohugo.io/commands/hugo_server/) | `1313` | `swa start http://localhost:1313` |

| [Next.js](https://nextjs.org/) | `3000` | `swa start http://localhost:3000` |

| [React (Create React App)](https://reactjs.org/docs/create-a-new-react-app.html) | `3000` | `swa start http://localhost:3000` |

| [Svelte (sirv-cli)](https://github.com/lukeed/sirv/tree/master/packages/sirv-cli/) | `5000` | `swa start http://localhost:5000` |

| [Vue](https://github.com/vuejs/create-vue) | `3000` | `swa start http://localhost:3000` |

Instead of starting a dev server separately, you can provide the startup command to the CLI.

```azstatic-cli

# npm start script (React)

swa start http://localhost:3000 --run "npm start"

# dotnet watch (Blazor)

swa start http://localhost:5000 --run "dotnet watch run"

# Jekyll

swa start http://localhost:4000 --run "jekyll serve"

# custom script

swa start http://localhost:4200 --run "./startup.sh"

```

Then access the application with the emulated services from `http://localhost:4280`

### Serve both the front-end app and API

If your project includes API functions, the CLI checks if the Azure Functions Core Tools are installed and available. If not, the CLI downloads and install the right version of the Azure Functions Core Tools.

#### Start the API server automatically

Run the CLI and provide the folder that contains the API backend (a valid Azure Functions App project):

```azstatic-cli

# static content plus an API

swa start ./my-dist --api-location ./api

# front-end dev server plus an API

swa start http://localhost:3000 --api-location ./api

```

#### Start API server manually

When developing your backend locally, sometimes it's useful to run Azure Functions Core Tools separately to serve your API. This allows you to use built-in features like debugging and rich editor support.

To use the CLI with your local API backend dev server, follow these two steps:

1. Start your API using Azure Functions Core Tools: `func host start` or start debugging in VS Code.

2. In a separate terminal, run the SWA CLI with the `--api-location` flag and the URI of the local API server, in the following format:

```azstatic-cli

swa start ./my-dist --api-location http://localhost:7071

```

#### Database connections

To start your application with a [database connection](database-overview.md), use the `--data-api-location` parameter and point to the folder containing the _staticwebapp.database.config.json_ file.

```azstatic-cli

swa start ./src --data-api-location swa-db-connections

```

### Syntax

```azstatic-cli

swa start

```

### Examples

#### Example 1: Start the application with defaults.

```azstatic-cli

swa start

```

#### Example 2: Start the application with a front end dev server.

```azstatic-cli

swa start http://<APP_DEV_SERVER_HOST>:<APP_DEV_SERVER_PORT>

```

#### Example 3: Start the application with a front end and back end dev server.

```azstatic-cli

swa start http://<APP_DEV_SERVER_HOST>:<APP_DEV_SERVER_PORT> --api-location http://localhost:7071

```

### Parameters

___`--app-location, -a <PATH>`___

The folder containing the source code of the front end application. Default is `.`.

___`--api-location, -i <PATH>`___

The folder containing the source code of the API application.

___`--output-location, -O <PATH>`___

The folder containing the built source of the front end application. The path is relative to `--app-location`. Default is `.`.

___`--data-api-location`___

The folder containing the *staticwebapp.database.config.json* file.

___`--app-devserver-url, -D <URL>`___

Connect to the app dev server at this URL instead of using output location.

___`--api-devserver-url, -is <URL>`___

Connect to the API server at this URL instead of using output location.

___`--api-port, -j <API_PORT>`___

The API server port passed to `func start`. Default is 7071.

___`--host, -q <HOST>`___

The host address used for the CLI dev server. Default is `localhost`.

___`--port, -p <PORT>`___

The port value to use for the CLI dev server. Default `4280`.

___`--ssl, -s`___

Serve the front end application and API over HTTPS. Default is `false`.

___`--ssl-cert, -e <SSL_CERT_LOCATION>`___

The SSL certificate (.crt) used when enabling HTTPS.

___`--ssl-key, -k <SSL_KEY_LOCATION>`___

The SSL key (.key) used when enabling HTTPS.

___`--run, -r <STARTUP_SCRIPT>`___

Location of a custom shell command or script file to run at startup.

___`--devserver-timeout, -t <TIME>`___

The amount of time to wait (in seconds) when connecting to a front end application's dev server or an API server. Default is 60.

___`--swa-config-location, -w <SWA_CONFIG_FILE_LOCATION>`___

The directory location of the `staticwebapp.config.json` file.

___`--open, -o`___

Open the browser to the dev server. Default is false.

___`--func-args, -f <FUNCTION_ARGUMENTS>`___

Pass additional arguments to the `func start` command.

___[Global Parameters](#global-parameters)___

## swa deploy

Deploy the current project to Azure Static Web Apps.

Common use cases include:

1. Deploy a front end app without an API

1. Deploy a front end app with an API

1. Deploy a Blazor app

### Deployment token

The SWA CLI supports deploying using a deployment token. This is often useful when deploying from a CI/CD environment. You can get a deployment token either from:

- The [Azure portal](https://portal.azure.com/): **Home → Static Web App → Your Instance → Overview → Manage deployment token**

- If you are using the [Azure CLI](https://aka.ms/azcli), you can get the deployment token of your project using the following command:

```azstatic-cli

az staticwebapp secrets list --name <APPLICATION_NAME> --query "properties.apiKey"

```

- If you are using the Azure Static Web Apps CLI, you can use the following command:

```azstatic-cli

swa deploy --print-token

```

You can then use that value with the `--deployment-token <TOKEN>` or you can create an environment variable called `SWA_CLI_DEPLOYMENT_TOKEN` and set it to the deployment token.

> [!IMPORTANT]

> Don't store the deployment token in a public repository. This value must remain a secret.

### Deploy a front end app without an API

You can deploy a front end application without an API to Azure Static Web Apps by running the following steps:

1. If your front-end application requires a build step, run `swa build` or refer to your application build instructions.

**Option 1:** From build folder you would like to deploy, run the deploy command:

```azstatic-cli

cd build/

swa deploy

```

> [!NOTE]

> The `build` folder must contain the static content of your app that you want to deploy.

**Option 2:** You can also deploy a specific folder:

1. If your front end application requires a build step, run `swa build` or refer to your application build instructions.

2. Deploy your app:

```azstatic-cli

swa deploy ./my-dist

```

### Deploy a front-end app with an API

To deploy both the front end app and an API to Azure Static Web Apps, use the following steps:

1. If your front end application requires a build step, run `swa build` or refer to your application build instructions.

2. Make sure the API language runtime version in the `staticwebapp.config.json` file is set correctly, for example:

```json

{

"platform": {

"apiRuntime": "node:16"

}

}

```

> [!NOTE]

> If your project doesn't have any `staticwebapp.config.json` file, add one under your `outputLocation` folder.

3. Deploy your app:

```azstatic-cli

swa deploy ./my-dist --api-location ./api

```

### Deploy a Blazor app

To deploy a Blazor app with an optional API to Azure Static Web Apps, use the following steps:

1. Build your Blazor app in **Release** mode:

```azstatic-cli

dotnet publish -c Release -o bin/publish

```

2. From the root of your project, run the `deploy` command:

```azstatic-cli

swa deploy ./bin/publish/wwwroot --api-location ./Api

```

### Deploy using the `swa-cli.config.json`

> [!NOTE]

> The path for `outputLocation` must be relative to the `appLocation`.

If you are using a `swa-cli.config.json` configuration file in your project and have a single configuration entry, use a configuration like this:

```json

{

"configurations": {

"my-app": {

"appLocation": "./",

"apiLocation": "api",

"outputLocation": "frontend",

"start": {

"outputLocation": "frontend"

},

"deploy": {

"outputLocation": "frontend"

}

}

}

}

```

Then you can deploy your application by running the following steps:

1. If your front-end application requires a build step, run `swa build` or refer to your application build instructions.

2. Deploy your app:

```azstatic-cli

swa deploy

```

If you have multiple configuration entries, you can provide the entry ID to specify which one to use:

```azstatic-cli

swa deploy my-otherapp

```

### Syntax

```azstatic-cli

swa deploy

[--yes]

```

### Examples

#### Example 1: Deploy using a deployment token.

```azstatic-cli

swa deploy ./dist/ --api-location ./api/ --deployment-token <TOKEN>

```

#### Example 2: Deploy using a deployment token from the environment variables

```azstatic-cli

SWA_CLI_DEPLOYMENT_TOKEN=123 swa deploy ./dist/ --api-location ./api/

```

#### Example 3: Deploy using `swa-cli.config.json` file

```azstatic-cli

swa deploy

swa deploy myconfig

```

#### Example 4: Print the deployment token

```azstatic-cli

swa deploy --print-token

```

#### Example 5: Deploy to a specific environment

```azstatic-cli

swa deploy --env production

```

___[Global Parameters](#global-parameters)___

## swa db

Generate and edit your Static Web Apps database connections configuration.

Use `swa db init` to generate a sample _swa-db-connections_ folder, along with a `staticwebapp.database.config.json` configuration file. If you are using a Cosmos DB for NoSQL database, this also generates a sample `staticwebapp.database.schema.gql` schema file.

### Syntax

```azstatic-cli

swa db init --database-type <DATABASE_TYPE>

```

### Examples

#### Example 1: Generate a sample database connection configuration folder for an Azure SQL database.

```azstatic-cli

swa db init --database-type mssql

```

### Parameters

___`--database-type, -t <DATABASE_TYPE>`___

(Required) The type of the database you want to connect (mssql, postgresql, cosmosdb_nosql, mysql).

___`--folder-name, -f <FOLDER_NAME>`___

A folder name to override the convention database connection configuration folder name (ensure that you update your CI/CD workflow files accordingly). The default value is `swa-db-connections`.

___`---connection-string, -cs <CONNECTION_STRING>`___

The connection string of the database you want to connect.

___`--cosmosdb_nosql-database, -nd <COSMOSDB_NOSQL_DATABASE>`___

The database of your Cosmos DB account you want to connect (only needed if using `cosmosdb_nosql` database type).

___`--cosmosdb_nosql-container, -nc <COSMOSDB_NOSQL_CONTAINER>`___

The container of your Cosmos DB account you want to connect.

___`--help, -h`___

Display help for command.

___[Global Parameters](#global-parameters)___


# Traffic Splitting

# Traffic Splitting in Azure Static Web Apps (preview)

Traffic splitting allows you to divert a percentage of traffic to different [branch environments](./branch-environments.md).

Traffic splitting is only available on the [Standard hosting plan](plans.md).

> [!NOTE]

> Traffic splitting does not work with private endpoint or enterprise-grade edge.

## Split traffic

Before you can split traffic between branches, you first need to have open pull requests to create separate environments.

To split traffic among different environments, use the following steps:

1. Open your static web app in the Azure portal.

1. From the *Settings* section, select **Environments**.

1. Select the **Traffic splitting** tab.

1. Select the **Add** button to create a new row in the traffic mapping table.

1. From the dropdown, select name of the pull request you want to target.

1. Enter the percentage amount of traffic you want to allocate among the different environments.

Adjust the values in each of the input boxes in the *Traffic* column so the total equals 100%.

1. Select **Save** to commit your changes.

## Disable traffic splitting

To disable traffic splitting, select the **Traffic splitting** to open the settings window.

Remove all nonproduction environments from the list and save your changes.

## Next steps

> [!div class="nextstepaction"]

> [Use preview environments](preview-environments.md)


# Enterprise Edge

# Enterprise-grade edge

Use Azure Static Web Apps enterprise-grade edge to enable faster page loads, enhance security, and optimize reliability for your global applications. Enterprise edge combines the capabilities of Azure Static Web Apps, Azure Front Door, and Azure Content Delivery Network (CDN) into a single secure cloud CDN platform.

Key features of Azure Static Web Apps enterprise-grade edge include:

* Global presence in 118+ [edge locations](../frontdoor/edge-locations-by-region.md) across 100 metro cities.

* Caching assets at the [edge](../frontdoor/front-door-caching.md).

* Proactive protection against [Distributed Denial of Service (DDoS) attacks](../frontdoor/front-door-ddos.md).

* Native support of end-to-end IPv6 connectivity and [HTTP/2 protocol](../frontdoor/front-door-http2.md).

* Optimized file compression.

## Caching

When enterprise-grade edge is enabled for your static web app, you benefit from caching at various levels.

* **CDN**: Caching content on edge locations as physically close to users a possible to reduce latency.

* **DNS**: Caching DNS records for faster lookups.

* **Browser**: Files are stored in the browser and returned for identical requests.

For further control, you can also create [custom cache control headers](configuration.md) for your static web app.

## Configuration types

You can enable enterprise-grade edge powered by Azure Front Door via a managed experience through the Azure portal, or you [can set it up manually](front-door-manual.md?pivots=swa-afd-manual-afd).

A managed experience provides:

* Zero configuration changes

* No downtime

* Automatically managed SSL certifications and custom domains

A manual setup gives you full control over the CDN configuration including the chance to:

* Limit traffic origin by origin

* Add a web application firewall

* Use more advanced features of Azure Front Door

## Enable enterprise-grade edge

### Prerequisites

* [Custom domain](./custom-domain.md) configured for your static web app with a time to live (TTL) set to less than 48 hrs.

* An application deployed with [Azure Static Web Apps](./get-started-portal.md) that uses the Standard hosting plan.

# [Azure portal](#tab/azure-portal)

1. Go to your static web app in the Azure portal.

1. Select **Enterprise-grade edge** from the menu.

1. Check the box labeled **Enable enterprise-grade edge**.

1. Select **Save**.

1. Select **OK** to confirm the save.

Enabling this feature incurs extra costs.

# [Azure CLI](#tab/azure-cli)

```azurecli

az extension add --name enterprise-edge

az staticwebapp enterprise-edge enable --name my-static-webapp --resource-group my-resource-group

```

---

## Considerations

- Deleting a custom domain mapped to your account can take up to 48 hours to propagate.

## Limitations

- Private Endpoint can't be used with enterprise-grade edge.

## Next steps

> [!div class="nextstepaction"]

> [Application configuration](configuration.md)


# Front Door Manual

# Tutorial: Configure a CDN for Azure Static Web Apps

By adding [Azure Front Door](../frontdoor/front-door-overview.md) as the CDN for your static web app, you benefit from a secure entry point for fast delivery of your web applications.

With Static Web Apps, you have two options to integrate with Azure Front Door. You can add Azure Front Door to your static web app by enabling enterprise-grade edge, a managed integration of Azure Front Door with Static Web Apps. Alternatively, you can configure an Azure Front Door resource manually in front of your static web app.

Consider the advantages below to determine which option best suits your needs.

**Enterprise-grade edge provides:**

* Zero configuration changes

* No downtime

* Automatically managed SSL certifications and custom domains

**A manual Azure Front Door setup gives you full control over the CDN configuration including the chance to:**

* Limit traffic origin by origin

* Add a web application firewall (WAF)

* Route across multiple applications

* Use more advanced features of Azure Front Door

In this tutorial, you learn to add Azure Front Door to your static web app.

### Prerequisites

* Registered `Microsoft.Cdn` [resource provider](/azure/azure-resource-manager/management/resource-providers-and-types).

* [Custom domain](./custom-domain.md) configured for your static web app with a time to live (TTL) set to less than 48 hrs.

* An application deployed with [Azure Static Web Apps](./get-started-portal.md) that uses the Standard hosting plan.

### Enable enterprise-grade edge on the Static Web Apps resource

# [Azure portal](#tab/azure-portal)

1. Go to your static web app in the Azure portal.

1. Select **Enterprise-grade edge** in the left menu.

1. Check the box labeled **Enable enterprise-grade edge**.

1. Select **Save**.

1. Select **OK** to confirm the save.

Enabling this feature incurs extra costs.

# [Azure CLI](#tab/azure-cli)

```azurecli

az extension add -n enterprise-edge

az staticwebapp enterprise-edge enable -n my-static-webapp -g my-resource-group

```

### Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)

- An Azure Static Web Apps site. [Build your first static web app](get-started-portal.md)

- Azure Static Web Apps Standard and Azure Front Door Standard / Premium plans. For more information, see [Static Web Apps pricing](https://azure.microsoft.com/pricing/details/app-service/static/)

- Consider using [enterprise-grade edge](enterprise-edge.md) for faster page loads, enhanced security, and optimized reliability for global applications.

### Create an Azure Front Door

1. Sign in to the [Azure portal](https://portal.azure.com).

2. From the home page or the Azure menu, select **+ Create a resource**. Search for *Front Door and CDN profiles*, and then select **Create** > **Front Door and CDN profiles**.

3. On the Compare offerings page, select **Quick create**, and then select **Continue to create a Front Door**.

4. On the **Create a Front Door profile** page, enter or select the following settings.

| Setting | Value |

|---|---|

| Subscription | Select your Azure subscription. |

| Resource group | Enter a resource group name. This name is often the same group name used by your static web app. |

| Resource group location | If you create a new resource group, enter the location nearest you. |

| Name | Enter **my-static-web-app-front-door**. |

| Tier | Select **Standard**. |

| Endpoint name | Enter a unique name for your Front Door host. |

| Origin type | Select **Static Web App**. |

| Origin host name | Select the host name of your static web app from the dropdown.  |

| Caching | Check the **Enable caching** checkbox. |

| Query string caching behavior | Select **Use Query String** |

| Compression | Select **Enable compression** |

| WAF policy | Select **Create new** or select an existing Web Application Firewall policy from the dropdown if you want to enable this feature. |

> [!NOTE]

> When you create an Azure Front Door profile, you must select an origin from the same subscription the Front Door is created in.

5. Select **Review + create**, and then select **Create**. The creation process may take a few minutes to complete.

6. When  deployment completes, select **Go to resource**.

7. [Add a condition](#add-a-condition).

### Disable cache for auth workflow

> [!NOTE]

> The cache expiration, cache key query string and origin group override actions are deprecated. These actions can still work normally, but your rule set can't change. Replace these overrides with new route configuration override actions before changing your rule set.

Add the following settings to disable Front Door's caching policies from trying to cache authentication and authorization-related pages.

#### Add a condition

1. From your Front Door, under *Settings*, select **Rule set**.

2. Select **Add**.

3. In the *Rule set name* textbox, enter **Security**.

4. In the *Rule name* textbox, enter **NoCacheAuthRequests**.

5. Select **Add a condition**.

6. Select **Request path**.

7. Select the *Operator* drop-down, and then **Begins With**.

8. Select the **Edit** link above the *Value* textbox.

9. Enter `/.auth` in the textbox, and then select **Update**.

10. Select no options from the *String transform* dropdown.

#### Add an action

1. Select the **Add an action** dropdown.

2. Select **Route configuration override**.

3. Select **Disabled** in the *Caching* dropdown.

4. Select **Save**.

#### Associate rule to an endpoint

Now that the rule is created, apply the rule to a Front Door endpoint.

1. From your Front Door, select **Rule set**, and then the **Unassociated** link.

2. Select the endpoint name to which you want to apply the caching rule, and then select **Next**.

3. Select **Associate**.

### Copy Front Door ID

Use the following steps to copy the Front Door instance's unique identifier.

1. From your Front Door, select the **Overview** link on the left-hand navigation.

1. Copy the value labeled **Front Door ID** and paste it into a file for later use.

### Update static web app configuration

To complete the integration with Front Door, you need to update the application configuration file to do the following functions:

- Restrict traffic to your site only through Front Door

- Restrict traffic to your site only from your Front Door instance

- Define which domains can access your site

- Disable caching for secured routes

Open the [staticwebapp.config.json](configuration.md) file for your site and make the following changes.

1. Restrict traffic to only use Front Door by adding the following section to the configuration file:

```json

"networking": {

"allowedIpRanges": ["AzureFrontDoor.Backend"]

}

```

1. To define which Azure Front Door instances and domains can access your site, add the `forwardingGateway` section.

```json

"forwardingGateway": {

"requiredHeaders": {

"X-Azure-FDID" : "<YOUR-FRONT-DOOR-ID>"

},

"allowedForwardedHosts": [

"my-sitename.azurefd.net"

]

}

```

First, configure your app to only allow traffic from your Front Door instance. In every backend request, Front Door automatically adds an `X-Azure-FDID` header that contains your Front Door instance ID. By configuring your static web app to require this header, it restricts traffic exclusively to your Front Door instance. In the `forwardingGateway` section in your configuration file, add the `requiredHeaders` section and define the `X-Azure-FDID` header. Replace `<YOUR-FRONT-DOOR-ID>` with the *Front Door ID* you set aside earlier.

Next, add the Azure Front Door hostname (not the Azure Static Web Apps hostname) into the `allowedForwardedHosts` array. If you have custom domains configured in your Front Door instance, also include them in this list.

In this example, replace `my-sitename.azurefd.net` with the Azure Front Door hostname for your site.

2. For all secured routes in your app, disable Azure Front Door caching by adding `"Cache-Control": "no-store"` to the route header definition.

```json

{

...

"routes": [

{

"route": "/members",

"allowedRoles": ["authenticated", "members"],

"headers": {

"Cache-Control": "no-store"

}

}

]

...

}

```

With this configuration, your site is no longer available via the generated `*.azurestaticapps.net` hostname, but exclusively through the hostnames configured in your Front Door instance.

### Considerations

- **Custom domains**: Now that Front Door is managing your site, you no longer use the Azure Static Web Apps custom domain feature. Azure Front Door has a separate process for adding a custom domain. Refer to [Add a custom domain to your Front Door](../frontdoor/front-door-custom-domain.md). When you add a custom domain to Front Door, you'll need to update your static web app configuration file to include it in the `allowedForwardedHosts` list.

- **Traffic statistics**: By default, Azure Front Door configures [health probes](../frontdoor/front-door-health-probes.md) that may affect your traffic statistics. You may want to edit the default values for the [health probes](../frontdoor/front-door-health-probes.md).

- **Serving old versions**: When you deploy updates to existing files in your static web app, Azure Front Door may continue to serve older versions of your files until their [time-to-live](https://wikipedia.org/wiki/Time_to_live) expires. [Purge the Azure Front Door cache](../frontdoor/front-door-caching.md#cache-purge) for the affected paths to ensure the latest files are served.

## Clean up resources

If you no longer want to use the resources created in this tutorial, delete the Azure Static Web Apps and Azure Front Door instances.

## Next steps

> [!div class="nextstepaction"]

> [Add an API](apis-overview.md)


# External Providers

# Set up Azure Static Web Apps to deploy to external providers

Azure Static Web Apps supports a series of built-in providers to help you publish your website. If you would like to use a provider beyond the out-of-the-box options, use the following guide to build and deploy your static web app.

> [!NOTE]

> You can also follow the steps specific to [Bitbucket](bitbucket.md) and [GitLab](gitlab.md).

## Create a static web app

When you create a new static web app from the Azure portal, you can select the source location of your web app.

1. Under *Deployment details*, select **Other** to use a custom source control provider.

Once the static web app is ready, then go to the *Overview* section.

1. From the *Overview* section, select the **Manage deployment token** button.

1. Copy the deployment token and paste it into a text editor so you can set up your CI/CD pipeline.

## Set up a CI/CD pipeline

When you set up your CI/CD pipeline, you need to create two jobs. The first job builds your static web app and the second deploys the app.

### Build

The purpose of the build job is to build the web application into a production-ready state. Set up your build job to run the commands necessary to build and package your web application to make it ready for deployment.

The build process needs to build the static web app and the APIs in the `api` folder, if they exist.

Build commands are specific to the technology you use. See the documentation for libraries or frameworks used in your application for details.

### Deploy

Create a job to deploy the production-ready files and folders to the empty Static Web App. Your job must include the static web app's deployment token to authenticate with Azure.

Deployment commands are specific to the technology you use. See the documentation for your source control provider for details.

## Next steps

> [!div class="nextstepaction"]

> [Build your first static app](getting-started.md)


# Deployment Token Management

# Reset deployment tokens in Azure Static Web Apps

When you create a new Azure Static Web Apps site, Azure generates a token used to identify the application during deployment. During provisioning, this token is stored as a secret in the GitHub repository. This article explains how to use and manage this token.

Normally, you don't need to worry about the deployment token, but the following are some reasons you might need to retrieve or reset the token.

* **Token compromise**: Reset your token if it is exposed to an outside party.

* **Deploying from a separate GitHub repository**: If you are manually deploying from a separate GitHub repository, then you need to set the deployment token in the new repository.

## Prerequisites

- An existing GitHub repository configured with Azure Static Web Apps.

- See [Building your first static app](getting-started.md) if you don't have one.

## Reset a deployment token

1. Select **Manage deployment token** on the _Overview_ page of your Azure Static Web Apps site.

2. Select **Reset token**.

3. After displaying a new token in the _Deployment token_ field, copy the token by selecting **Copy to clipboard**.

## Update a secret in the GitHub repository

To keep automated deployment running, after resetting a token you need to set the new value in the corresponding GitHub repository.

1. Go to your project's repository on GitHub, and select the **Settings** tab.

1. Under the *Security* section, select **Actions**.

1. Find a secret generated during Static Web App provisioning named _AZURE_STATIC_WEB_APPS_API_TOKEN_... in the _Repository secrets_ section.

> [!NOTE]

> If you created the Azure Static Web Apps site against multiple branches of this repository, you see multiple _AZURE_STATIC_WEB_APPS_API_TOKEN_... secrets in this list. Select the correct one by matching the file name listed in the _Edit workflow_ field on the _Overview_ tab of the Static Web Apps site.

1. Select pen icon button to update the value.

1. **Paste the value** of the deployment token to the _Value_ field.

1. Select **Update secret**.

## Next steps

> [!div class="nextstepaction"]

> [Publish from a static site generator](publish-gatsby.md)


# Publish Bicep

# Deploy Azure Static Web Apps with Bicep

You can use a Bicep file to create an instance of Azure Static Web Apps. Bicep provides a declarative syntax to define and create Azure resources, which can be automated and repeated for consistency.

The steps in this article show you how to use Bicep to create a resource group and a Static Web Apps instance. After your static web app is created you still need to deploy your code using the typical methods of GitHub Actions, or using Azure Pipelines.

You can use Bicep along with Azure Verified Modules (AVM) to deploy your static web apps.

## Verified modules

The Bicep examples in this article use [Azure Verified Modules (AVM)](https://azure.github.io/Azure-Verified-Modules/) when possible and [Bicep](/azure/azure-resource-manager/bicep/) when AVM isn't available. AVM modules are recognizable because they reference modules that include `avm/res`, such as `br/public:avm/res/web/static-site:0.3.0`.

Using a verified module allows you to use opinionated managed Bicep code maintained by professional engineers fluent in Bicep. Since verified modules require support and dedicated attention, sometimes a module you need might not be available. If an AVM isn't available, you can code your [Bicep files](/azure/templates/) by hand.

## Prerequisites

- [Bicep tools](../azure-resource-manager/Bicep/install.md): Learn how to install Bicep tools.

- [Visual Studio Code extension for Bicep](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-bicep): An optional extension that creates resources for you by running your Bicep file.

## Create a static web app resource

The following code creates a new resource group and a Static Web Apps resource and then outputs the default host name and static web app name.

Create a file named `main.bicep` file and paste in the following code.

Before you run this code, make sure to replace the `<REGION_NAME>` placeholder with your region name.

```Bicep

targetScope = 'subscription'

param location string ='<REGION_NAME>'

@description('String to make resource names unique')

var resourceToken = uniqueString(subscription().subscriptionId, location)

@description('Create a resource group')

resource rg 'Microsoft.Resources/resourceGroups@2024-03-01' = {

name: 'rg-swa-app-${resourceToken}'

location: location

}

@description('Create a static web app')

module swa 'br/public:avm/res/web/static-site:0.3.0' = {

name: 'client'

scope: rg

params: {

name: 'swa-${resourceToken}'

location: location

sku: 'Free'

}

}

@description('Output the default hostname')

output endpoint string = swa.outputs.defaultHostname

@description('Output the static web app name')

output staticWebAppName string = swa.outputs.name

```

This code:

- Scopes the action to the current Azure subscription.

- Generates a unique string to ensure the static web app name is globally unique.

- Creates a new resource group.

- Creates a new Static Web Apps instance using the free tier.

- Outputs the web app's URL.

- Outputs the static web app name.

After you execute this file, save the values of the output variables to a text editor.

See the next section if you want to link an existing Azure Functions app to your static web app.

## Link a Functions app

The code in the previous section demonstrates how to create a static web app using the free tier. If you want to link a managed backend to your static web app, you need to change to the [Standard hosting plan](/azure/static-web-apps/plans).

To link your Functions app to your static web app, you need the `resourceId` of your Functions App. You can get this value from the Azure portal, or you can use the following command to return your Functions app `resourceId`.

```azurecli

az functionapp show -n <FUNCTION-APP-NAME> -g <RESOURCE-GROUP-NAME> --query id --output tsv

```

Create a file named `config.bicep` file and paste in the following code.

Before you run this code, make sure to replace the placeholders surrounded by `<>` with your values.

```Bicep

targetScope = 'resourceGroup'

param location string = '<REGION_NAME>'

param staticWebAppName string = '<STATIC_WEB_APP_NAME>'

param functionsAppResourceId = '<FUNCTIONS_APP_RESOURCE_ID>'

@description('Get reference to the static web app')

resource staticWebApp 'Microsoft.Web/staticSites@2023-12-01' existing = {

name: staticWebAppName

}

@description('Link backend to static web app')

resource linkedStaticWebAppBackend 'Microsoft.Web/staticSites/linkedBackends@2023-12-01' = {

parent: staticWebApp

name: 'linkedBackend'

properties: {

backendResourceId: functionsAppResourceId

region: location

}

}

```

This code:

- Scopes the action to the Azure resource group.

- Gets access to the existing static web app by name.

- Links the static web app to a Functions app using the Functions app `resourceId`.

## Deployment

Now that your Azure Static Web Apps instance is created, you can deploy your source code to the static web app with one of the following tools:

- [Azure Developer CLI (Recommended)](/azure/developer/azure-developer-cli)

- [Static Web Apps CLI](https://github.com/Azure/static-web-apps-cli)

- [GitHub Actions](https://docs.github.com/actions)

- [Azure Pipelines](/azure/devops/pipelines/overview-azure)

- **Local development environment**: Use [Azure Developer CLI](/azure/developer/azure-developer-cli) to deploy from your local machine. When running locally, you define your deployment in an `azure.yml` file. This file includes hooks that plug into the resource creation process at any point. These extensibility points help you during deployment, especially when different parts of your app need to know about each other at build time.

- **Production environment**: The ability to deploy from a GitHub Actions workflow file is a built-in feature when you create your static web app. Once the file is in your repository, you can edit the file as needed. Deployment from [other source code providers](external-providers.md) is also supported.

To learn more from a full end-to-end application that includes resource creation and application deployment, see [Serverless AI Chat with RAG using LangChain.js](https://github.com/Azure-Samples/serverless-chat-langchainjs).

## Faster deployments with the Azure Developer CLI

Azure Developer CLI (`azd`) uses Bicep files along with deployment configurations to create your application. Since version 1.4, `azd` checks the Bicep against cloud resources to determine if the underlying infrastructure as code (IaC) state requires updates. If the state remains unchanged, creation and configuration are skipped. To learn more about this performance improvement, see [azd provision is now faster when there are no infrastructure changes](

https://devblogs.microsoft.com/azure-sdk/azure-developer-cli-azd-october-2023-release/#azd-provision-is-now-faster-when-there-are-no-infrastructure-changes

).

## Related content

- [Awesome AZD](https://azure.github.io/awesome-azd/?tags=swa)

- [Public Bicep Registry](https://github.com/Azure/bicep-registry-modules)

- [Azure Developer CLI](/azure/developer/azure-developer-cli)

- [Static Web Apps CLI](https://github.com/Azure/static-web-apps-cli)

- [GitHub Actions](https://docs.github.com/actions)


# Bitbucket

# Tutorial: Deploy Bitbucket repositories on Azure Static Web Apps

Azure Static Web Apps has flexible deployment options that allow to work with various providers. In this tutorial, you deploy a web application hosted in Bitbucket to Azure Static Web Apps using a Linux virtual machine.

> [!NOTE]

> The Static Web Apps pipeline task currently only works on Linux machines.

In this tutorial, you learn to:

> [!div class="checklist"]

> * Import a repository to Bitbucket

> * Create a static web app

> * Configure the Bitbucket repo to deploy to Azure Static Web Apps

## Prerequisites

- [Bitbucket](https://bitbucket.org) account

- Ensure you have enabled [two-step verification](https://bitbucket.org/account/settings/two-step-verification/manage)

- [Azure](https://portal.azure.com) account

- If you don't have an Azure subscription, [create a free trial account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Create a repository

This article uses a GitHub repository as the source to import code into a Bitbucket repository.

1. Sign in to [Bitbucket](https://bitbucket.org).

1. Go to [https://bitbucket.org/repo/import](https://bitbucket.org/repo/import) to begin the import process.

1. Under the *Old repository* label, in the *URL* box, enter the repository URL for your choice of framework.

# [No Framework](#tab/vanilla-javascript)

[https://github.com/staticwebdev/vanilla-basic.git](https://github.com/staticwebdev/vanilla-basic.git)

# [Angular](#tab/angular)

[https://github.com/staticwebdev/angular-basic.git](https://github.com/staticwebdev/angular-basic.git)

# [Blazor](#tab/blazor)

[https://github.com/staticwebdev/blazor-basic.git](https://github.com/staticwebdev/blazor-basic.git)

# [React](#tab/react)

[https://github.com/staticwebdev/react-basic.git](https://github.com/staticwebdev/react-basic.git)

# [Vue](#tab/vue)

[https://github.com/staticwebdev/vue-basic.git](https://github.com/staticwebdev/vue-basic.git)

---

1. Next to the *Project* label, select **Create new project**.

1. Enter **MyStaticWebApp**.

1. Select **Import repository** and wait a moment while the website creates your repository.

### Set main branch

From time to time the template repository have more than one branch. Use the following steps to ensure Bitbucket maps the *main* tag to the main branch in the repository.

1. Select **Repository settings**.

1. Expand the **Advanced** section.

1. Under the *Main branch* label, ensure **main** is selected in the drop down.

1. If you made a change, select **Save changes**.

1. Select **Back**.

## Create a static web app

Now that the repository is created, you can create a static web app from the Azure portal.

1. Go to the [Azure portal](https://portal.azure.com).

1. Select **Create a Resource**.

1. Search for **Static Web Apps**.

1. Select **Static Web Apps**.

1. Select **Create**.

1. In the _Basics_ section, begin by configuring your new app.

| Setting | Value |

|--|--|

| Azure subscription | Select your Azure subscription. |

| Resource Group | Select the **Create new** link and enter **static-web-apps-bitbucket**. |

| Name | Enter **my-first-static-web-app**. |

| Plan type | Select **Free**. |

| Region for Azure Functions API and staging environments | Select the region closest to you. |

| Source | Select **Other**. |

1. Select **Review + create**.

1. Select **Create**.

1. Select **Go to resource**.

1. Select **Manage deployment token**.

1. Copy the deployment token value and set it aside in an editor for later use.

1. Select **Close** on the *Manage deployment token* window.

## Create the pipeline task in Bitbucket

1. Go to the repository in Bitbucket.

1. Select the **Source** menu item.

1. Ensure the **main** branch is selected in the branch drop down.

1. Select **Pipelines**.

1. Select text link **Create your first pipeline**.

1. On the *Starter pipeline* card, select **Select**.

1. Enter the following YAML into the configuration file.

# [No Framework](#tab/vanilla-javascript)

```yml

pipelines:

branches:

main:

- step:

name: Deploy to test

deployment: test

script:

- chown -R 165536:165536 $BITBUCKET_CLONE_DIR

- pipe: microsoft/azure-static-web-apps-deploy:main

variables:

APP_LOCATION: '$BITBUCKET_CLONE_DIR/src'

OUTPUT_LOCATION: '$BITBUCKET_CLONE_DIR/src'

API_TOKEN: $deployment_token

```

# [Angular](#tab/angular)

```yml

pipelines:

branches:

main:

- step:

name: Deploy to test

deployment: test

script:

- chown -R 165536:165536 $BITBUCKET_CLONE_DIR

- pipe: microsoft/azure-static-web-apps-deploy:main

variables:

APP_LOCATION: '$BITBUCKET_CLONE_DIR'

OUTPUT_LOCATION: '$BITBUCKET_CLONE_DIR/dist/angular-basic'

API_TOKEN: $deployment_token

```

> [!NOTE]

> If you are using these instructions with your own code and Angular 17 or above, the output location value needs to end with **/browser**.

# [Blazor](#tab/blazor)

```yml

pipelines:

branches:

main:

- step:

name: Deploy to test

deployment: test

script:

- chown -R 165536:165536 $BITBUCKET_CLONE_DIR

- pipe: microsoft/azure-static-web-apps-deploy:main

variables:

APP_LOCATION: '$BITBUCKET_CLONE_DIR/Client'

OUTPUT_LOCATION: 'wwwroot'

API_TOKEN: $deployment_token

```

# [React](#tab/react)

```yml

pipelines:

branches:

main:

- step:

name: Deploy to test

deployment: test

script:

- chown -R 165536:165536 $BITBUCKET_CLONE_DIR

- pipe: microsoft/azure-static-web-apps-deploy:main

variables:

APP_LOCATION: '$BITBUCKET_CLONE_DIR'

OUTPUT_LOCATION: '$BITBUCKET_CLONE_DIR/build'

API_TOKEN: $deployment_token

```

# [Vue](#tab/vue)

```yml

pipelines:

branches:

main:

- step:

name: Deploy to test

deployment: test

script:

- chown -R 165536:165536 $BITBUCKET_CLONE_DIR

- pipe: microsoft/azure-static-web-apps-deploy:main

variables:

APP_LOCATION: '$BITBUCKET_CLONE_DIR'

OUTPUT_LOCATION: '$BITBUCKET_CLONE_DIR/dist'

API_TOKEN: $deployment_token

```

---

> [!NOTE]

> In this example the value for `pipe` is set to `microsoft/azure-static-web-apps-deploy:main`. Replace `main` with your desired branch name if you want your pipeline to work with a different branch.

The following configuration properties are used in the configuration file for your static web app.

The `$BITBUCKET_CLONE_DIR` variable maps to the repository's root folder location during the build process.

| Property | Description | Example | Required |

|--|--|--|--|

| `app_location` | Location of your application code. | Enter `/` if your application source code is at the root of the repository, or `/app` if your application code is in a directory named `app`. | Yes |

| `api_location` | Location of your Azure Functions code. | Enter `/api` if your api code is in a folder named `api`. If no Azure Functions app is detected in the folder, the build doesn't fail, the workflow assumes you don't want an API. | No |

| `output_location` | Location of the build output directory relative to the `app_location`. | If your application source code is located at `/app`, and the build script outputs files to the `/app/build` folder, then set `build` as the `output_location` value. | No |

Next, define value for the `API_TOKEN` variable.

1. Select **Add variables**.

1. In the *Name* box, enter **deployment_token**, which matches the name in the workflow.

1. In the *Value* box, paste in the deployment token value you set aside in a previous step.

1. Check the **Secured** checkbox.

2. Select **Add**.

3. Select **Commit file** and return to your pipelines tab.

Wait a moment on the *Pipelines* window and you'll see your deployment status appear. Once the deployment is finished running, you can view the website in your browser.

## View the website

There are two aspects to deploying a static app. The first step creates the underlying Azure resources that make up your app. The second is a Bitbucket workflow that builds and publishes your application.

Before you can go to your new static site, the deployment build must first finish running.

The Static Web Apps overview window displays a series of links that help you interact with your web app.

1. Return to your static web app in the Azure portal.

1. Go to the **Overview** window.

2. Select the link under the *URL* label. Your website loads in a new tab.

## Clean up resources

If you're not going to continue to use this application, you can delete the Azure Static Web Apps instance and all the associated services by removing the resource group.

1. Select the **static-web-apps-bitbucket** resource group from the *Overview* section.

2. Select **Delete resource group** at the top of the resource group *Overview*.

3. Enter the resource group name **static-web-apps-bitbucket** in the *Are you sure you want to delete "static-web-apps-bitbucket"?* confirmation dialog.

4. Select **Delete**.

The process to delete the resource group may take a few minutes to complete.

## Next steps

> [!div class="nextstepaction"]

> [Add an API](add-api.md)


# Gitlab

# Tutorial: Deploy GitLab repositories on Azure Static Web Apps

Azure Static Web Apps has flexible deployment options that allow to work with various providers. In this article, you deploy a web application hosted in GitLab to Azure Static Web Apps.

In this tutorial, you learn to:

> [!div class="checklist"]

> * Import a repository to GitLab

> * Create a static web app

> * Configure the GitLab repo to deploy to Azure Static Web Apps

## Prerequisites

- [GitLab](https://gitlab.com) account

- [Azure](https://portal.azure.com) account

- If you don't have an Azure subscription, [create a free trial account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Create a repository

This article uses a GitHub repository as the source to import code into a GitLab repository.

1. Sign in to your GitLab account and go to [https://gitlab.com/projects/new#import_project](https://gitlab.com/projects/new#import_project)

2. Select **Repo by URL**.

3. In the *Git repository URL* box, enter the repository URL for your choice of framework.

# [No Framework](#tab/vanilla-javascript)

[https://github.com/staticwebdev/vanilla-basic.git](https://github.com/staticwebdev/vanilla-basic.git)

# [Angular](#tab/angular)

[https://github.com/staticwebdev/angular-basic.git](https://github.com/staticwebdev/angular-basic.git)

# [Blazor](#tab/blazor)

[https://github.com/staticwebdev/blazor-basic.git](https://github.com/staticwebdev/blazor-basic.git)

# [React](#tab/react)

[https://github.com/staticwebdev/react-basic.git](https://github.com/staticwebdev/react-basic.git)

# [Vue](#tab/vue)

[https://github.com/staticwebdev/vue-basic.git](https://github.com/staticwebdev/vue-basic.git)

---

4. In the *Project slug* box, enter **my-first-static-web-app**.

5. Select **Create project** and wait a moment while your repository is set up.

## Create a static web app

Now that the repository is created, you can create a static web app from the Azure portal.

1. Go to the [Azure portal](https://portal.azure.com).

1. Select **Create a Resource**.

1. Search for **Static Web Apps**.

1. Select **Static Web Apps**.

1. Select **Create**.

1. In the _Basics_ section, begin by configuring your new app.

| Setting | Value |

|--|--|

| Azure subscription | Select your Azure subscription. |

| Resource Group | Select the **Create new** link and enter **static-web-apps-gitlab**. |

| Name | Enter **my-first-static-web-app**. |

| Plan type | Select **Free**. |

| Source | Select **Other**. |

1. Select **Review + create**.

1. Select **Create**.

1. Select **Go to resource**.

1. Select **Manage deployment token**.

1. Copy the deployment token value and set it aside in an editor for later use.

1. Select **Close** on the *Manage deployment token* window.

## Create the pipeline task in GitLab

Now that you have your deployment token, you add a workflow task responsible for building and deploying your site as you make changes.

### Add deployment token

When going through the following steps, make sure that you select `*` for the environments section. It may appear the default value is `all`, but you need to select the dropdown and manually choose `*`.

1. Go to the repository in GitLab.

1. Select **Settings**.

1. Select **CI/CD**.

1. Next to the *Variables* section, select **Expand**.

1. Select **Add variable**.

1. In the *Key* box, enter **DEPLOYMENT_TOKEN**.

1. In the *Value* box, paste in the deployment token value you set aside in a previous step.

1. Select **Add variable**.

### Add file

1. Return to your repository's main screen in GitLab.

1. Select the **Edit** button and choose, **Web IDE**.

1. Ensure the *main* branch is selected in the branch drop down.

1. Create a new file named `.gitlab-ci.yml` at the root of the repository. (Make sure the file extension is `.yml`.)

1. Enter the following YAML into the file.

# [No Framework](#tab/vanilla-javascript)

```yml

variables:

API_TOKEN: $DEPLOYMENT_TOKEN

APP_PATH: '$CI_PROJECT_DIR/src'

deploy:

stage: deploy

image: registry.gitlab.com/static-web-apps/azure-static-web-apps-deploy

script:

- echo "App deployed successfully."

```

# [Angular](#tab/angular)

```yml

variables:

API_TOKEN: $DEPLOYMENT_TOKEN

APP_PATH: '$CI_PROJECT_DIR/src'

OUTPUT_PATH: '$CI_PROJECT_DIR/dist/angular-basic'

deploy:

stage: deploy

image: registry.gitlab.com/static-web-apps/azure-static-web-apps-deploy

script:

- echo "App deployed successfully."

```

# [Blazor](#tab/blazor)

```yml

variables:

API_TOKEN: $DEPLOYMENT_TOKEN

APP_PATH: '$CI_PROJECT_DIR/Client'

OUTPUT_PATH: 'wwwroot'

deploy:

stage: deploy

image: registry.gitlab.com/static-web-apps/azure-static-web-apps-deploy

script:

- echo "App deployed successfully."

```

# [React](#tab/react)

```yml

variables:

API_TOKEN: $DEPLOYMENT_TOKEN

APP_PATH: '$CI_PROJECT_DIR'

OUTPUT_PATH: '$CI_PROJECT_DIR/build'

deploy:

stage: deploy

image: registry.gitlab.com/static-web-apps/azure-static-web-apps-deploy

script:

- echo "App deployed successfully."

```

# [Vue](#tab/vue)

```yml

variables:

API_TOKEN: $DEPLOYMENT_TOKEN

APP_PATH: '$CI_PROJECT_DIR'

OUTPUT_PATH: '$CI_PROJECT_DIR/dist'

deploy:

stage: deploy

image: registry.gitlab.com/static-web-apps/azure-static-web-apps-deploy

script:

- echo "App deployed successfully."

```

---

The following configuration properties are used in the *.gitlab-ci.yml* file to configure your static web app.

The `$CI_PROJECT_DIR` variable maps to the repository's root folder location during the build process.

| Property | Description | Example | Required |

|--|--|--|--|

| `APP_PATH` | Location of your application code. | Enter `$CI_PROJECT_DIR/` if your application source code is at the root of the repository, or `$CI_PROJECT_DIR/app` if your application code is in a folder named `app`. | Yes |

| `API_PATH` | Location of your Azure Functions code. | Enter `$CI_PROJECT_DIR/api` if your app code is in a folder named `api`. | No |

| `OUTPUT_PATH` | Location of the build output folder relative to the `APP_PATH`. | If your application source code is located at `$CI_PROJECT_DIR/app`, and the build script outputs files to the `$CI_PROJECT_DIR/app/build` folder, then set `$CI_PROJECT_DIR/app/build` as the `OUTPUT_PATH` value. | No |

| `API_TOKEN` | API token for deployment. | `API_TOKEN: $DEPLOYMENT_TOKEN` | Yes |

1. **Commit changes** to the main branch and close the web IDE.

1. Return to your site and select the **Settings** > **CI/CD** > **General Pipelines** menu items to view the progress of your deployment.

Once the deployment is complete, you can view your website.

## View the website

There are two aspects to deploying a static app. The first step creates the underlying Azure resources that make up your app. The second is a GitLab workflow that builds and publishes your application.

Before you can go to your new static site, the deployment build must first finish running.

The Static Web Apps overview window displays a series of links that help you interact with your web app.

1. Return to your static web app in the Azure portal.

1. Go to the **Overview** window.

1. Select the link under the *URL* label. Your website loads in a new tab.

## Clean up resources

If you're not going to continue to use this application, you can delete the Azure Static Web Apps instance and all the associated services by removing the resource group.

1. Select the **static-web-apps-gitlab** resource group from the *Overview* section.

1. Select **Delete resource group** at the top of the resource group *Overview*.

1. Enter the resource group name **static-web-apps-gitlab** in the *Are you sure you want to delete "static-web-apps-gitlab"?* confirmation dialog.

1. Select **Delete**.

The process to delete the resource group may take a few minutes to complete.

## Next steps

> [!div class="nextstepaction"]

> [Add an API](add-api.md)


# Preview Environments

# Preview environments in Azure Static Web Apps

By default, when you deploy a site to Azure Static Web Apps [each pull request deploys a preview version of your site available through a temporary URL](review-publish-pull-requests.md). This version of the site allows you to review changes before merging pull requests. Once the pull request (PR) is closed, the temporary environment disappears.

Beyond PR-driven temporary environments, you can enable preview environments that feature stable locations. The URLs for preview environments take on the following form:

```text

<DEFAULT_HOST_NAME>-<BRANCH_OR_ENVIRONMENT_NAME>.<LOCATION>.azurestaticapps.net

```

### Limitations

- Custom domains do not work with preview environments.

- Pre-production environments aren't geo-distributed.

## Deployment types

The following deployment types are available in Azure Static Web Apps.

- **Production**: Changes to production branches are deployed into the production environment. Your custom domain points to this environment, and content served from this location is indexed by search engines.

- [**Pull requests**](review-publish-pull-requests.md): Pull requests against your production branch deploy to a temporary environment that disappears after the pull request is closed. The URL for this environment includes the PR number as a suffix. For example, if you make your first PR, the preview location looks something like `<DEFAULT_HOST_NAME>-1.<LOCATION>.azurestaticapps.net`.

- [**Branch**](branch-environments.md): You can optionally configure your site to deploy every change made to branches that aren't a production branch. This preview deployment is published at a stable URL that includes the branch name. For example, if the branch is named `dev`, then the environment is available at a location like `<DEFAULT_HOST_NAME>-dev.<LOCATION>.azurestaticapps.net`. You can delete a branch environment in the portal via the *Environments* tab of your static web app.

- [**Named environment**](named-environments.md): You can configure your pipeline to deploy all changes to a named environment. This preview deployment is published at a stable URL that includes the environment name. For example, if the deployment environment is named `release`, then the environment is available at a location like `<DEFAULT_HOST_NAME>-release.<LOCATION>.azurestaticapps.net`.

> [!NOTE]

> Valid characters for environment names are `0-9`,`a-z`, and `A-Z`. The maximum character string limit allowed is 16.

## Next Steps

> [!div class="nextstepaction"]

> [Review pull requests in pre-production environments](./review-publish-pull-requests.md)


# Branch Environments

# Create branch preview environments in Azure Static Web Apps

You can configure your site to deploy every change made to branches that aren't a production branch. This preview deployment is published at a stable URL that includes the branch name. For example, if the branch is named `dev`, then the environment is available at a location like `<DEFAULT_HOST_NAME>-dev.<LOCATION>.azurestaticapps.net`. You can delete a branch environment in the portal via the *Environments* tab of your static web app.

## Configuration

To enable stable URL environments, make the following changes to your [configuration.yml file](build-configuration.md?tabs=github-actions).

- Set the `production_branch` input to your production branch name on the `static-web-apps-deploy` job in GitHub action or on the AzureStaticWebApp task. This action ensures changes to your production branch are deployed to the production environment, while changes to other branches are deployed to a preview environment.

- List the branches you want to deploy to preview environments in the trigger array in your workflow configuration so that changes to those branches also trigger the GitHub Actions or Azure Pipelines deployment.

- Set this array to `**` for GitHub Actions or `*` for Azure Pipelines if you want to track all branches.

## Example

The following example demonstrates how to enable branch preview environments.

# [GitHub Actions](#tab/github-actions)

```yml

name: Azure Static Web Apps CI/CD

on:

push:

branches:

- main

- dev

- staging

pull_request:

types: [opened, synchronize, reopened, closed]

branches:

- main

jobs:

build_and_deploy_job:

...

name: Build and Deploy Job

steps:

- uses: actions/checkout@v2

with:

submodules: true

- name: Build And Deploy

id: builddeploy

uses: Azure/static-web-apps-deploy@v1

with:

...

production_branch: "main"

```

# [Azure Pipelines](#tab/azure-devops)

```yml

trigger:

- main

- dev

- staging

pool:

vmImage: ubuntu-latest

steps:

- checkout: self

submodules: true

- task: AzureStaticWebApp@0

inputs:

...

production_branch: 'main'

```

---

> [!NOTE]

> The `...` denotes code skipped for clarity.

In this example, the preview environments are defined for the `dev` and `staging` branches. Each branch is deployed to a separate preview environment.

## Next steps

> [!div class="nextstepaction"]

> [Create named preview environments](./named-environments.md)


# Named Environments

# Create named preview environments in Azure Static Web Apps

You can configure your site to deploy every change to a named environment. This preview deployment is published at a stable URL that includes the environment name. For example, if the environment is named `release`, then the preview is available at a location like `<DEFAULT_HOST_NAME>-release.<LOCATION>.azurestaticapps.net`.

## Configuration

To enable stable URL environments with named deployment environment, make the following changes to your build configuration file.

- Set the `deployment_environment` input to a specific name on the `static-web-apps-deploy` job in GitHub action or on the AzureStaticWebApp task. This ensures all changes to your tracked branches are deployed to the named preview environment.

- List the branches you want to deploy to preview environments in the trigger array in your workflow configuration so that changes to those branches also trigger the GitHub Actions or Azure Pipelines deployment.

- Set this array to `**` for GitHub Actions or `*` for Azure Pipelines if you want to track all branches.

## Example

The following example demonstrates how to enable branch preview environments.

# [GitHub Actions](#tab/github-actions)

```yml

name: Azure Static Web Apps CI/CD

on:

push:

branches:

- "**"

pull_request:

types: [opened, synchronize, reopened, closed]

branches:

- main

jobs:

build_and_deploy_job:

...

name: Build and Deploy Job

steps:

- uses: actions/checkout@v2

with:

submodules: true

- name: Build And Deploy

id: builddeploy

uses: Azure/static-web-apps-deploy@v1

with:

...

deployment_environment: "release"

```

# [Azure Pipelines](#tab/azure-devops)

```yml

trigger:

- "*"

pool:

vmImage: ubuntu-latest

steps:

- checkout: self

submodules: true

- task: AzureStaticWebApp@0

inputs:

...

deployment_environment: "release"

```

---

> [!NOTE]

> The `...` denotes code skipped for clarity.

In this example, changes to all branches get deployed to the `release` named preview environment.

## Next Steps

> [!div class="nextstepaction"]

> [Review pull requests in pre-production environments](./review-publish-pull-requests.md)


# Monitor

# Monitor Azure Static Web Apps

Enable [Application Insights](/azure/azure-monitor/app/app-insights-overview) to monitor API  requests, failures, and tracing information.

> [!IMPORTANT]

> Application Insights has an [independent pricing model](https://azure.microsoft.com/pricing/details/monitor) from Azure Static Web Apps.

> [!NOTE]

> Using Application Insights with Azure Static Web Apps requires an application with an [API](./add-api.md).

## Add monitoring

Use the following steps to add Application Insights monitoring to your static web app.

1. Open the Static Web Apps instance in the Azure portal.

1. Select **Application Insights** from the menu.

1. Select **Yes** next to _Enable Application Insights_.

1. Select **Save**.

Once you create the Application Insights instance, it creates an associated application setting in the Azure Static Web Apps instance used to link the services together.

> [!NOTE]

> If you want to track how the different features of your web app are used end-to-end client side, you can insert trace calls in your JavaScript code. For more information, see [Application Insights for webpages](/azure/azure-monitor/app/javascript?tabs=snippet).

## Access data

1. From the _Overview_ window in your static web app, select the link next to the _Resource group_.

1. From the list, select the Application Insights instance prefixed with the same name as your static web app.

The following table highlights a few locations in the portal you can use to inspect aspects of your application's API endpoints.

> [!NOTE]

> For more information on Application Insights usage, see the [App insights overview](/azure/azure-monitor/app/app-insights-overview).

| Type | Menu location | Description |

|--- | --- | --- |

| [Failures](/azure/azure-monitor/app/asp-net-exceptions) | _Investigate > Failures_ | Review failed requests. |

| [Server requests](/azure/azure-monitor/app/tutorial-performance) | _Investigate > Performance_ | Review individual API requests.  |

| [Logs](/azure/azure-monitor/app/search-and-transaction-diagnostics?tabs=transaction-search) | _Monitoring > Logs_ | Interact with an editor to query transaction logs. |

| [Metrics](/azure/azure-monitor/essentials/app-insights-metrics) | _Monitoring > Metrics_ | Interact with a designer to create custom charts using various metrics. |

### Traces

Using the following steps to view traces in your application.

1. Select **Logs** under _Monitoring_.

1. Hover your mouse over any card in the _Queries_ window.

2. Select **Load Editor**.

3. Replace the generated query with the word `traces`.

4. Select **Run**.

## Limit logging

In some cases, you may want to limit logging while still capturing details on errors and warnings. You can do so by making the following changes to your _host.json_ file of the Azure Functions app.

```json

{

"version": "2.0",

"logging": {

"applicationInsights": {

"samplingSettings": {

"isEnabled": true

},

"enableDependencyTracking": false

},

"logLevels": {

"default": "Warning"

}

}

}

```

## Next steps

> [!div class="nextstepaction"]

> [Set up authentication and authorization](authentication-authorization.yml)


# Metrics

# Supported metrics for managed Functions in Azure Static Web Apps

Azure Static Web Apps collects a series of metrics when you add a managed API to your application.

To view metrics on your app, open your static web app in the Azure portal and select **Monitoring**. In the *Monitoring* query window, you have access to metrics that report activity of your application.

## Supported metrics

The following metrics are tracked for your application:

| Name | Description |

|---|---|

| `BytesSent` | The number of outgoing bytes. |

| `CdnPercentageOf4XX` | Percentage of requests that result in `400` series server responses. |

| `CdnPercentageOf5XX` | Percentage of requests that result in `500` series server responses. |

| `CdnRequestCount` | Number of requests that make it to the site when enterprise grade edge is enabled. |

| `CdnResponseSize` | Size of CDN responses in bytes. |

| `CdnTotalLatency` | Time, measured in milliseconds, representing the CDN latency. |

| `DataApiErrors` | Number of errors produced from API calls. |

| `DataApiHits` | Number of hit to API endpoints. |

| `FunctionErrors` | Number of errors encounter by managed API functions and linked backend functions. |

| `FunctionHits` | Number of hits to managed API functions and linked backend functions. |

| `SiteErrors` | Number of errors encountered by the website. |

| `SiteHits` | Number of hits to the website. |

## Related content

* [Monitoring in Azure Static Web Apps](./monitor.md)


# Languages Runtimes

# Supported languages and runtimes in Azure Static Web Apps

Azure Static Web Apps features two different places where runtime and language versions are important, on the front end and for the API.

| Runtime type | Description |

|--|--|

| [Front end](#front-end) | The version responsible for running the website's build steps that build the front end application. |

| [API](#api) | The version and runtime of Azure Functions used in your web application. |

## Front end

You can specify the version used to build the front end of your static web app. Configuring a non-default version is often only necessary if you need to target older versions.

You can specify the runtime version that builds the front end of your static web app in the _package.json_ file in the `engines` section of the file.

```json

{

...

"engines": {

"node": ">=14.0.0"

}

}

```

## API

The underlying support for APIs in Azure Static Web Apps is provided by Azure Functions. Refer to the [Azure Functions supported languages and runtimes](../azure-functions/supported-languages.md) for details.

The following versions are supported for managed functions in Static Web Apps. If your application requires a version not listed, consider [bringing your own functions](./functions-bring-your-own.md) to your app.

[!INCLUDE [Languages and runtimes](../../includes/static-web-apps-languages-runtimes.md)]

## Re-enabling proxies in v4.x

Azure Functions supports [re-enabling proxies in v4.x](../azure-functions/legacy-proxies.md#re-enable-proxies-in-functions-v4x). To enable proxy support in managed functions for your static web app, set `SWA_ENABLE_PROXIES_MANAGED_FUNCTIONS` to `true` in your application settings.

> [!NOTE]

> While proxies are supported in v4.x, consider using Azure API Management integration with your managed function apps, so your app isn't reliant on proxies.

## Deprecations

> [!NOTE]

> Now that Azure Functions v3 is retired, Static Web Apps uses Azure Functions v4 for API runtime support for Python 3.8. Redeploy your app to enable this change. While not recommended, you can revert back to v3 by setting the environment variable `USEV3_FOR_PYTHON38` to `true`.

The following runtimes are deprecated in Azure Static Web Apps. For more information about changing your runtime, see [Specify API language runtime version in Azure Static Web Apps](https://azure.microsoft.com/updates/generally-available-specify-api-language-runtime-version-in-azure-static-web-apps/) and [Migrate apps from Azure Functions version 3.x to version 4.x](../azure-functions/migrate-version-3-version-4.md).

- .NET Core 3.1

- Node.js 12.x


# Troubleshooting

# Troubleshooting deployment and runtime errors

This article features step-by-step guides to troubleshooting deployment and other issues for your static web app.

## Retrieve deployment error messages

The Azure Static Web Apps deployment workflow uses the Node.js [Oryx build process](https://github.com/microsoft/Oryx/blob/master/doc/runtimes/nodejs.md#build) that automatically runs the following commands:

```bash

npm install

npm run build # if specified in package.json

npm run build:azure # if specified in package.json

```

Any errors raised by this process are logged in the GitHub workflow run. To view the logs generated by build action, use the following steps.

1. Go to the GitHub repository for your static web app.

1. Select **Actions**.

> [!NOTE]

> Any failed workflow runs display with a red *X* rather than a green check mark.

1. Select the link for the workflow run you wish to validate.

1. Select **Build and Deploy Job** to open the details of the deployment.

1. Select **Build And Deploy** to display the log.

![Screenshot of the deployment log for a static web app](./media/troubleshooting/build-deploy-log.png)

5. Review the logs and any error messages.

> [!NOTE]

> Some warning error messages may display in red, such as notes about *.oryx_prod_node_modules* and *workspace*. These are part of the normal deployment process.

If any packages fail to install or other issues are raised, the original error messages are available here.

### Confirm folder configuration

Azure Static Web Apps needs to know which folders to use to host your application. This configuration is confirmed by the build process at the end of the workflow. Any errors are logged during the validation steps.

If you see one of the following error messages in the error log, it's an indication the folder configuration for your workflow is incorrect.

| Error message | Description |

| --- | --- |

|App Directory Location: '/*folder*' is invalid. Couldn't detect this directory. | Verify your workflow reflects your repository structure. |

| The app build failed to produce artifact folder: '*folder*'. | Ensure the `folder` property is configured correctly in your workflow file. |

| Either no API directory was specified, or the specified directory wasn't found. | Azure Functions isn't created, as the workflow doesn't define a value for the `api` folder. |

There are three folder locations specified in the workflow. Ensure these settings match both your project and any tools that transform your source code before deployment.

| Configuration setting | Description |

| --- | --- |

| `app_location` | The root location of the source code to be deployed. This setting is typically */* or the location of the JavaScript and HTML for your project. |

| `output_location` | Name of the folder created by any build process from a bundler such as webpack. This folder both needs to be created by the build process, and a subdirectory under the `app_location` |

| `api_location` |The root location of your Azure Functions application hosted by Azure Static Web Apps. This points to the root folder of all Azure Functions for your project, typically *api*. |

> [!NOTE]

> Error messages generated by an incorrect `api_location` configuration may still build successfully, as Azure Static Web Apps doesn't require serverless code.

## Review server errors

Use [Application Insights](/azure/azure-monitor/app/app-insights-overview) to find runtime error messages. If you don't already have an instance created, refer to [Monitoring Azure Static Web Apps](monitor.md). Application Insights logs the full error message and stack trace generated by each error.

> [!NOTE]

> You can only view error messages that are generated after Application Insights is installed.

1. Inside the Azure portal, open the **Resource Group** associated with your static web app.

1. Select the Application Insights instance, which has the same name as your static web app (if created using the previous steps).

1. Under *Investigate*, select **Failures**.

1. Go down to *Drill into* on the right.

1. Under *Drill into*, a button displays the number of recently failed operations.

![Screenshot of the failures screen](./media/troubleshooting/app-insights-errors.png)

1. Select **x Operations** to open a panel displaying the recent failed operations.

![Screenshot of the operations screen](./media/troubleshooting/app-insights-operations.png)

1. Explore an error by selecting one from the list.

![Screenshot of the error details screen](./media/troubleshooting/app-insights-details.png)

## Environment variables

Many web applications use environment variables for storing sensitive or environment-specific settings. Azure Static Web Apps supports environment variables through Application Settings.

Application Settings are key/value pairs that set environment variables for your application. Variables are available to your application using the same syntax typical for accessing environment variables.

When deploying, double check any environment variables are set as Application Settings.

1. Open your static web app in the Azure portal.

1. Select **Configuration**. The *Configuration* screen displays the list of all Application Settings.

![Screenshot of the Configuration screen on a static web app](media/troubleshooting/app-settings.png)

Use the following steps to add a new variable.

1. Select **Add**.

1. Set the **Name**.

1. Set the **Value**.

1. Select **OK**.

1. Select **Save**.

## Review diagnostic reports

The [diagnose and solve](diagnostics-overview.md) feature can guide you through steps to troubleshoot problems.


# Quotas

# Quotas in Azure Static Web Apps

Subscription limits:

| Feature                             | Free plan   | Standard plan | Dedicated plan (Preview) |

|-------------------------------------|-------------|---------------|--------------------------|

| Included bandwidth (per month)      | 100 GB      | 100 GB        | 100 GB                   |

| Overage bandwidth                   | Unavailable | $0.20 per GB  | $0.20 per GB             |

| Apps                                | 10          | 100           | 1                        |

If you need more apps on the Standard plan, contact Azure Support.

App limits:

| Feature                             | Free plan   | Standard plan | Dedicated plan (Preview) |

|-------------------------------------|-------------|---------------|--------------------------|

| [Preview environments][3]           | 3           | 10            | 10                       |

| Total storage (all environments)    | 500 MB      | 2 GB          | 2 GB                     |

| Storage (single environment)        | 250 MB      | 500 MB        | 500 MB                   |

| File count                          | 15,000      | 15,000        | 15,000                   |

| [Custom domains][1]                 | 2           | 6             | 6                        |

| [Private endpoint][4]               | Unavailable | 1             | 1                        |

| Allowed IP range restrictions       | Unavailable | 25            | 25                       |

| [Authorization (custom roles)][2]   |             |               |                          |

| &nbsp;&nbsp;&nbsp;&nbsp;via invitations | 25 | 25 | 25 |

| &nbsp;&nbsp;&nbsp;&nbsp;via serverless functions | Unavailable | Unlimited | Unlimited |

| Request Size Limit                  | 30 MB       | 30 MB         | 30 MB                    |

## GitHub storage

GitHub Actions and Packages use GitHub Storage, which has its own set of quotas. When you create an Azure Static Web Apps site, GitHub stores the artifacts for your site even after deployment.

See the following resources for more detail:

- [Managing Actions storage space](https://github.community/t5/GitHub-Actions/Managing-Actions-storage-space/td-p/38944)

- [About billing for GitHub Actions](https://help.github.com/github/setting-up-and-managing-billing-and-payments-on-github/about-billing-for-github-actions#about-billing-for-github-actions)

- [Managing your spending limit for GitHub Actions](https://help.github.com/github/setting-up-and-managing-billing-and-payments-on-github/managing-your-spending-limit-for-github-actions)

## Next steps

- [Azure Static Web Apps overview](overview.md)

[1]: custom-domain.md

[2]: authentication-custom.md#manage-roles

[3]: preview-environments.md

[4]: private-endpoint.md


# Static Web Apps Cli Required Version

> [!IMPORTANT]

> To improve the security of deployments from the [Static Web Apps CLI](https://www.npmjs.com/package/@azure/static-web-apps-cli), a breaking change was introduced that requires you to upgrade to the latest version (2.0.2) of the Static Web Apps CLI by Jan. 15th, 2025.


# Diagnostics Overview

# Azure Static Web Apps diagnostics overview

If you encounter issues with your Azure Static Web Apps instance,  the diagnose and solve feature can guide you through steps to troubleshoot problems.

Diagnostics for your static web app are accessible directly from the Azure portal, with no configuration required.

Although these diagnostics are most helpful for issues that have occurred in the last 24 hours, all the diagnostic data remains available for analysis.

## Categories

You have access to diagnostic data in these categories:

| Category | Description | Examples |

|--|--|--|

| Availability and performance | Health and performance data | Service uptime, site hits, platform health |

| Configuration and Management | Application configuration data | Configuration of Static Web Apps features, custom authentication information |

| Content Deployment | Content deployment data | Deployments |

## View diagnostics

1. From the [Azure portal](https://portal.azure.com), go to your static web app.

1. Select **Diagnose and solve problems**.

From the diagnostics window you can filter diagnostic categories, or select one from the list.

## Reports

Selecting a detector reveals a series of visualization for the diagnostic data. The following screenshot is an example of the availability and performance report.

## Next steps

> [!div class="nextstepaction"]

> [Troubleshooting deployment and runtime errors](troubleshooting.md)
