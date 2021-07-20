# Java Function App Using Http triggers and output bindings to send data to CosmosDB

## Pre-requisites:

In order to use these examples, you will need:

1. An active Azure Account.
2. Java SDK 1.8+ installed.
3. Maven.
5. Azure CLI installed.
6. Visual Studio Code to modify the source code to suit your own needs. VS Code is optional; you can use any supported IDE. If using Visual Studio Code, please ensure to install the Azure Functions extension.
7. An HTTP client, such as Postman for testing the GET and POST calls in HTTP-triggered functions.

## Parameters to be modified/added in order to connect to ComosDB:

Fetch the value of connections string from the "Keys" under your cosmosdb resource from the azure portal. This string would be something like this: 
     
     "AccountEndpoint=https://yourcosmosdb.documents.azure.com:443/;AccountKey=Aabcd….;"

Add the above fetched CosmosDB connection String to your local.settings.json file under the field "AzureCosmosDBConnection". It would be defined as-

      "AzureCosmosDBConnection":"AccountEndpoint=https://yourcosmosdb.documents.azure.com:443/;AccountKey=Aabcd….;"

You also need to provide the values of name,databaseName, collectionName here      
             
https://github.com/Astha0710/JavaFnCosmosOutputBindings/blob/8c382564aa592427a039c9bc7f4211926c0d5647/src/main/java/com/function/Function.java#L33

name="any name",  databaseName: "cosmosdb name", collectionName: " name of container in your db"


##Build and run the code locally:
     
     mvn clean package
     mvn azure-functions:run
     
     
## Browse to the app:

Once your functions project is deployed, you can test if everything is working by going to the following URL with your browser or Postman:

Here, we are passing the value of parameter desc in the request header, this will be sent along with the randomly generated ID to the CosmosDB in the JSON document format.
     
     http://localhost:7071/api/WriteOneDocOutputBinding?desc=NewEntry
     
     
## Deploy to azure :

Set your subscription in az-cli using the below command:

      az account set --subscription "My Demos"
      
Deploy to azure using the below command:

      mvn azure-functions:deploy
      
Once the application is deployed, add the below setting under the Configuration -> Application settings section of your function app from azure portal

Name=AzureCosmosDBConnection and Value=AccountEndpoint=https://yourcosmosdb.documents.azure.com:443/;AccountKey=Aabcd….

      
Browse to the app using the similar url for your app and pass any value under desc here we have passed "ResponseFromAzure":

     https://<Yourfunctionappname>.azurewebsites.net/api/WriteOneDocOutputBinding?desc=ResponseFromAzure

## Follow below steps to deploy to a pre-created function app:

In the pom.xml file modify the following:

Provide the name of your pre-created function app here: https://github.com/Astha0710/JavaFnCosmosOutputBindings/blob/cf6a3899f1e19572f31e2e914f5ac1eff23d28ba/pom.xml#L17


Provide the name of the resource group in which your app is created here https://github.com/Astha0710/JavaFnCosmosOutputBindings/blob/cf6a3899f1e19572f31e2e914f5ac1eff23d28ba/pom.xml#L63

Provide the name of the App Service Plan containing your app here: https://github.com/Astha0710/JavaFnCosmosOutputBindings/blob/cf6a3899f1e19572f31e2e914f5ac1eff23d28ba/pom.xml#L65


Provide the Region in which your application is created in here: https://github.com/Astha0710/JavaFnCosmosOutputBindings/blob/cf6a3899f1e19572f31e2e914f5ac1eff23d28ba/pom.xml#L68

Provide the OS that your application is using here: https://github.com/Astha0710/JavaFnCosmosOutputBindings/blob/cf6a3899f1e19572f31e2e914f5ac1eff23d28ba/pom.xml#L77

You can also modify other parameters based on your requirement through the pom.xml file.

Once all the changes are made, follow the Deploy to azure steps as given above.
