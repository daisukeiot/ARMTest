https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fdaisukeiot%2FARMTest%2Fmaster%2Fiothubtest1.json

https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fdaisukeiot%2FARMTest%2Fmaster%2Ffunctions.json

https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fdaisukeiot%2FARMTest%2Fmaster%2Fazuredeploy.json

https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fdaisukeiot%2FARMTest%2Fmaster%2FResourceGroup.json


https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fdaisukeiot%2FARMTest%2Fv0.3%2Fazuredeploy.json

https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fdaisukeiot%2FARMTest%2Fmaster%2Fazuredeploy-dev.json

https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fdaisukeiot%2FARMTest%2Fmaster%2Fauzredeploy-advanced.json

https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fdaisukeiot%2FARMTest%2Fmaster%2Fazuredeploy-adt.json

https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fdaisukeiot%2FARMTest%2Fmaster%2Fazuredeploy-v0.4.json


ADT Functions App

az functionapp config appsettings set -g IoT-PnP-Demo -n Functions-hzdlc --settings "ADT_SERVICE_URL=https://IoT-PnP-Demo.api.wcus.digitaltwins.azure.net"
az functionapp identity assign -g IoT-PnP-Demo -n Functions-hzdlc
az dt role-assignment create --dt-name IoT-PnP-Demo --assignee "<principal-ID>" --role "Azure Digital Twins Owner (Preview)"

az eventgrid topic create -g IoT-PnP-Demo --name DigitalTwinToFunctionsTopic -l westcentralus
az dt endpoint create eventgrid --dt-name IoT-PnP-Demo --eventgrid-resource-group IoT-PnP-Demo --eventgrid-topic DigitalTwinToFunctionsTopic --endpoint-name adteventgridep
az dt route create --dt-name IoT-PnP-Demo --endpoint-name adteventgridep --route-name adteventgridroute

Map
az eventgrid topic create -g IoT-PnP-Demo --name DigitalTwinToMapFunctionsTopic -l westcentralus
az dt endpoint create eventgrid --endpoint-name adtmapeventgridep --eventgrid-resource-group IoT-PnP-Demo --eventgrid-topic DigitalTwinToMapFunctionsTopic -n IoT-PnP-Demo
az dt route create -n IoT-PnP-Demo --endpoint-name adtmapeventgridep --route-name adtmapeventgridroute --filter "type = 'Microsoft.DigitalTwins.Twin.Update'"
az functionapp config appsettings set --settings "map-subscription-key=d4Oj6DNMCCJ2iDY6cBHMr9Llqirefg67qOiBeIVNzTc" -g IoT-PnP-Demo -n Functions-hzdlc 
az functionapp config appsettings set --settings "statesetID=5f1589fd-b97e-aeaa-a651-4599d7487818" -g IoT-PnP-Demo -n Functions-hzdlc 


https://stackoverflow.com/questions/47360529/how-to-use-listkeys-function-in-an-arm-template-with-event-hub