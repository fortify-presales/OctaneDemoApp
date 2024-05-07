[![Build Status](https://dev.azure.com/fortify-presales/OctaneDemoApp/_apis/build/status%2Ffortify-presales.OctaneDemoApp?branchName=main)](https://dev.azure.com/fortify-presales/OctaneDemoApp/_build/latest?definitionId=13&branchName=main)

# Octane Demo App

This is a simple Java Web application that can be used for the demonstration of application
security testing tools such as those provided by [Fortify by OpenText](https://www.microfocus.com/en-us/cyberres/application-security). It also includes pipeline integrations
to [ALM Octane/ValueEdge by OpenText](https://www.opentext.com/products/alm-octane).
It is a cut down "search" results/details page from a larger sample application [IWA-Java](https://github.com/fortify/IWA-Java) and is kept deliberately 
small for demos.

Run Application (locally)
-------------------------

You can the run the application locally using the following:

```
gradlew bootRun
```

The application should then be available at the URL `http://localhost:8088`. If it fails to start,
make sure you have no other applications running on port 8088. There are only a few features that are
functional in this version of the app:

- you can type in some keywords in the search box, e.g. "alphadex" to filter results
- you can click on any search result to navigate to a details page
- you can download a datasheet PDF from a details page
- you can subscribe to the newsletter by entering an email address in the input field of the footer
- you can login/logout (user credentials are: admin@localhost.com/password or user1@localhost.com/password)

These have been "enabled" because they all have potential security issues that can be found by Fortify.

Deploy Application (Azure)
--------------------------

If you want to run the application in the cloud you can deploy it to Microsoft Azure along with its required
infrastructure by using the Azure DevOps CLI and the Gradle build script. In order to deploy to Azure you will need
to create a `.env` file in the root directory with contents similar to the following:

```
AZURE_SUBSCRIPTION_ID=17d2722b-256e-47e5-84b8-5b01f509a42c
AZURE_RESOURCE_GROUP=fortifydemorg
AZURE_APP_NAME=fortifydemoapp
AZURE_REGION=eastus
```

Then you can run the following commands:

```
az login [--tenant XXXX]
az group create --name [YOUR_INITIALS]-fortifydemorg --location eastus
gradlew azureWebAppDeploy
```

Replace `eastus` with your own desired region and make sure in the `.env` file you have
set `AZURE_APP_NAME` to a unique value.

You can navigate to your [Azure portal](https://portal.azure.com/#home) to see the built infrastructure and to
the deployed web application using the URL output shown from the `azureWebAppDeploy task`.

Remove Application and Infrastructure
-------------------------------------

To clean up all the resources you can execute the following (from a Windows command prompt):

```
az group delete --name [YOUR_INITIALS]-fortifydemorg
```

---

Kevin A. Lee (kadraman) - klee2@opentext.com
