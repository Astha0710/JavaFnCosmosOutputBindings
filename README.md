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

	• Fetch the value of connections string from the "Keys" under your cosmosdb resource from the azure portal. This string would be something like this: 
"AccountEndpoint=https://yourcosmosdb.documents.azure.com:443/;AccountKey=Aabcd….;"

	• Add the above fetched CosmosDB connection String to your local.settings.json file under the field "AzureCosmosDBConnection". It would be defined as-

"AzureCosmosDBConnection":"AccountEndpoint=https://yourcosmosdb.documents.azure.com:443/;AccountKey=Aabcd….;"

	• You also need to provide the values of  parameters  <a href="https://github.com/Astha0710/JavaFnCosmosOutputBindings/blob/80f6c0afe952af2af8d6b0d443dd699fad0d476f/src/main/java/com/function/Function.java#L33">here</a>
	name="any name",  databaseName: "cosmosdb name", collectionName: " name of container in your db"


Build and run the code locally:
     
     mvn clean package
     mvn azure-functions:run
     
     
Browse to the app:

Once your functions project is deployed, you can test if everything is working by going to the following URL with your browser or Postman:

Here, we are passing the value of parameter desc in the request header, this will be sent along with the randomly generated ID to the CosmosDB in the JSON document format.
     
     http://localhost:7071/api/WriteOneDocOutputBinding?desc=NewEntry![image](https://user-images.githubusercontent.com/43231180/126320344-3da03210-97c6-4bdd-99ca-ad99e34f40a0.png)

