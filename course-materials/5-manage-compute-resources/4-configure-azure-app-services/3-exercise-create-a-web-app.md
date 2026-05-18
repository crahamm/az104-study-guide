Exercise - Create a web app in the Azure portal
===============================================

Choose your development language: Node.js

In this unit, you use the Azure portal to create a web app.

Create a web app
----------------

Sign in to the [Azure portal](https://portal.azure.com/) using your Azure account.

1.  On the Azure portal menu, or from the **Home** page, select **Create a resource**. Everything you create on Azure is a resource. The **Create a resource** pane appears.

    Here, you can search for the resource you want to create, or select one of the popular resources that people create in the Azure portal.

2.  In the **Create a resource** menu, select **Web**.

3.  Select **Web App**. If you don't see it, in the search box, search for and select **Web App**. The **Create Web App** pane appears.

4.  On the **Basics** tab, enter the following values for each setting.

    Expand table

    | Setting | Value | Details |
    | --- |  --- |  --- |
    | **Project Details** |  |  |
    | --- |  --- |  --- |
    | Subscription | Select your Azure subscription | The web app you're creating must belong to a resource group. Here, you select the Azure subscription to which the resource group belongs. |
    | Resource Group | Select **Create new**and enter a name like **myResourceGroup** | The resource group to which the web app belongs. All Azure resources must belong to a resource group. |
    | **Instance Details** |  |  |
    | Name | *Enter a name* | The name of your web app. This name becomes part of the app's URL: *appname*\-*hash*.*region*.azurewebsites.net. |
    | Publish | Code | The method you want to use to publish your application. When publishing an application as code, you also must configure **Runtime stack** to prepare App Service resources to run your app. |
    | Runtime stack | Node 20 LTS | The platform on which you want your application to run. Your choice might affect whether you have a choice of operating system; for some runtime stacks, App Service supports only one operating system. |
    | Operating System | Linux | The operating system used on the virtual servers to run your app. |
    | Region | East US | The geographical region from which your app is hosted. |
    | **Pricing plans** |  |  |
    | Linux Plan | Accept default | The name of the App Service plan that powers your app. By default, the wizard creates a new plan in the same region as the web app. |
    | Pricing plan | Free F1 | The pricing tier of the service plan being created. The pricing plan determines the performance characteristics of the virtual servers that power your app and the features to which it has access. Select **Free F1** in the drop-down. |

    ![Screenshot showing web app creation details.](https://learn.microsoft.com/en-us/training/modules/host-a-web-app-with-azure-app-service/media/3-create-web-app-node.png)

5.  Leave any other settings as default. Select **Review + Create** to go to the review pane, and then select **Create**. The portal shows the deployment pane, where you can view the status of your deployment.

> **Note:** It can take a moment for deployment to complete.

Preview your web app
--------------------

1.  When deployment is complete, select **Go to resource**. The portal shows the App Service Overview pane for your web app.

    ![Screenshot showing the App Service pane with the URL link of the overview section highlighted.](https://learn.microsoft.com/en-us/training/modules/host-a-web-app-with-azure-app-service/media/3-web-app-home.png)

2.  To preview your web app's default content, select the URL under **Default domain** at the top right. The placeholder page that loads indicates that your web app is up and running and is ready to receive deployment of your app's code.

![Screenshot showing your App Service in a browser.](https://learn.microsoft.com/en-us/training/modules/host-a-web-app-with-azure-app-service/media/3-web-app-online-node.png)

Leave the browser tab with the new app's placeholder page open. You'll come back to it after your app is deployed.
