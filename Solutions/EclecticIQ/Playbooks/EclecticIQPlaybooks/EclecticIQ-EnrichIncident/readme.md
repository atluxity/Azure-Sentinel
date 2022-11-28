# ElasticSearch-EnrichIncident Playbook
 ## Summary
 When a new Azure Sentinel incident is created, this playbook gets triggered and performs below actions
 1. For each Entity (Accounts, Host, IP Address, FileHash, URL) available in Sentinel incident, it performs lookup for a match in EclecticIQ
 2. If it finds the match, this playbook adds a rich comment to the incident with all the collected information
    ![Comment example](./images/CommentElasticSearch_EnrichIncident.png)



![Playbook Designer view](./images/EnrichIndicentElasticSearchWorkflow.png)<br>

### Prerequisites 
1. EclecticIQ Custom Connector needs to be deployed prior to the deployment of this playbook under the same subscription.
2. API key. To get API Key, find the instructions here https://developers.eclecticiq.com/docs/authenticate#generate-api-token.

### Deployment instructions 
1. Deploy the playbook by clicking on "Deploy to Azure" button. This will take you to deplyoing an ARM Template wizard.
[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FAzure-Sentinel%2Fmaster%2FSolutions%EclecticIQ%2FPlaybooks%2FEclecticIQPlaybooks%EclecticIQ-EnrichIncident%2Fazuredeploy.json)
[![Deploy to Azure Gov](https://aka.ms/deploytoazuregovbutton)](https://portal.azure.us/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FAzure-Sentinel%2Fmaster%2FSolutions%2FEclecticIQ%2FPlaybooks%2FEclecticIQPlaybooks%EclecticIQ-EnrichIncident%2Fazuredeploy.json)

2. Fill in the required paramteres:
    * Playbook Name: Enter the playbook name here (Ex: EclecticIQ-EnrichIncident)
    * Custom Connector Name: Enter the EclecticIQ Custom connector name here (Ex: EclecticIQCustomConnector)
    
### Post-Deployment instructions 
#### a. Authorize connections
Once deployment is complete, you will need to authorize each connection.
1.	Click the Azure Sentinel connection resource
2.	Click edit API connection
3.	Click Authorize
4.	Sign in
5.	Click Save
6.	Repeat steps for EclecticIQ Api  Connection (For authorizing the EclecticIQ API connection, API Key needs to be provided)
#### b. Configurations in Sentinel
1. In Azure sentinel analytical rules should be configured to trigger an incident with risky user account or host or URL or FileHash or IP Address. 
2. Configure the automation rules to trigger this playbook

