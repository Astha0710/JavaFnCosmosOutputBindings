# JavaFnCosmosOutputBindings

Add your CosmosDB connection String in the local.settings.json file.

Build and run the code:
     
     mvn clean package
     mvn azure-functions:run
     
     
Browse to the app:
     
     http://localhost:7071/api/WriteOneDocOutputBinding?desc=NewEntry
