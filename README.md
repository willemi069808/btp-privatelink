# Private Link Approuter

Sample NodeJS application to proxy requests over the BTP Private Link service.
This sample application uses Azure Blob Storage as sample hyperscaler service which needs to be consumed via the private link connection.

More info:
- https://help.sap.com/docs/private-link/private-link1/azure-storage-account
- https://blogs.sap.com/2022/06/03/extend-your-business-processes-with-the-new-sap-private-link-service/
- https://github.com/SAP-samples/btp-private-link-approuter/tree/main/azure-blob-approuter-cloud-integration

## Azure Configuration
1. Create an Azure Storage account
2. Create a Container and upload a test file
3. (optional) In the Networking tab of the Azure Storage account, set the 'Public network access' to Disabled, and Save
4. Copy the Azure Storage account Resource ID for later use
5. Generate a Shared Access Signature (SAS token) having at least [Blob, Container + Object, Read + List] permissions on the Storage Account

## Approuter Configuration
1. Enter the Resource ID in the [private-link.json](private-link.json) file
3. Deploy this application via `mbt build` and `cf deploy`
4. _**DURING**_ the deployment, approve the activation of the private link on Azure: Navigate to the Azure Storage account > Networking > Private endpoint connections and approve
5. Create a BTP Destination (PrivateLink_AzureBlob) and use the hostname mentioned in the BTP Private Link Service binding as URL, using the Private Link proxy type

## Test the application
In a browser, call the approuter URL followed with:
- `/PrivateLink_AzureBlob/<your_container_name>/restype=container&comp=list&<your_SAS_token>` to see the list of sample files
- `/PrivateLink_AzureBlob/<your_container_name>/<your_file_name>?<your_SAS_token>` to see your sample file
