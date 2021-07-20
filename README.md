Java Function App Using Http triggers and output bindings to send data to CosmosDB

Pre-requisites:

In order to use these examples, you will need:
	1. An active Azure Account (get a free trial account here).
	2. Java SDK 1.8+ installed.
	3. Maven.
	4. Some knowledge of Java and Git.
	5. Azure CLI installed.
	6. Visual Studio Code to modify the source code to suit your own needs. VS Code is optional; you can use any supported IDE. If using Visual Studio Code, please ensure to install the Azure Functions extension.
	7. An HTTP client, such as Postman for testing the GET and POST calls in HTTP-triggered functions.

Parameters to be modified/added in order to connect to ComosDB:

Fetch the value of connections string from the "Keys" under your cosmosdb resource from the azure portal. This string would be something like this: 
     
     "AccountEndpoint=https://yourcosmosdb.documents.azure.com:443/;AccountKey=Aabcd….;"

Add the above fetched CosmosDB connection String to your local.settings.json file under the field "AzureCosmosDBConnection". It would be defined as-

      "AzureCosmosDBConnection":"AccountEndpoint=https://yourcosmosdb.documents.azure.com:443/;AccountKey=Aabcd….;"

You also need to provide the values of name,databaseName, collectionName here      
             
https://github.com/Astha0710/JavaFnCosmosOutputBindings/blob/8c382564aa592427a039c9bc7f4211926c0d5647/src/main/java/com/function/Function.java#L33

name="any name",  databaseName: "cosmosdb name", collectionName: " name of container in your db"


Build and run the code locally:
     
     mvn clean package
     mvn azure-functions:run
     
     
Browse to the app:

Once your functions project is deployed, you can test if everything is working by going to the following URL with your browser or Postman:

Here, we are passing the value of parameter desc in the request header, this will be sent along with the randomly generated ID to the CosmosDB in the JSON document format.
     
     http://localhost:7071/api/WriteOneDocOutputBinding?desc=NewEntry
