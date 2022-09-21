
# For .NET
  
## Getting Started
  
### Description 
ICG Process API endpoints include all the methods that are needed to process transactions using the different processors based on the merchant configuration. These procedures include invoices, transactions, merchants, portals, settlements, Reconciliation etc. 


#### API Client Configuration Parameters: 
  
|Parameter       | Type      |Description|
|----------------|-----------|-------------------------------------------------------|
|`Timeout`         |`TimeSpan`   |Http client timeout. Default: `TimeSpan.FromSeconds(100)`|   
|`authorization`   | `String`    |API Access token provided by the Auth API after User authentication|
  
  
The API client configuration looks like this:
```markdown  
ICGAPIProcess.Standard.ICGAPIProcessClient client = new ICGAPIProcess.Standard.ICGAPIProcessClient.Builder().Build();
```
   
#### Authorization 
This API uses the 
```markdown 
  Custom Header Signature 
```
The following table describe the list of configured parameters for retries through the  HttpClientConfiguration in the API Client.
  
#### API Client Configuration Parameters: 
  
|Parameter            | Type               |Description|
|---------------------|--------------------|--------------------------------------------------------------------------------------------------------------------|
|`Timeout`            |`TimeSpan`          |	Http client timeout.Default: `100`                                                                                   |   
|`NumberOfRetries`    |`int`                 | Number of times the request is retried. Default: `0`                                                                 |
|`BackoffFactor`      |`int`                 |Exponential backoff factor for duration between retry calls. Default: `2`                                             |
|`RetryInterval       |`double`              |The time interval between the endpoint calls.Default: `1`                                                             |
|`MaximumRetryWaitTime` |`TimeSpan`          |The maximum retry wait time. Default: `0`                                                                             |
|`StatusCodesToRetry`   |`IList\<int\>`           |List of Http status codes to invoke retry. Default: `408, 413, 429, 500, 502, 503, 504, 521, 522, 524, 408, 413, 429, 500, 502, 503, 504, 521, 522, 524`|
|`RequestMethodsToRetry` |`IList\<HttpMethod\>`   |List of Http request methods to invoke retry. Default: `"GET", "PUT", "GET", "PUT"`|
  

## API Endpoints
## Invoices
### Process Pay Invoice
#### Description
 
This API call will be made in order to process the transaction. The user will pay for the invoice by submitting his personal details and payment method details. To accomplish that, the API Client will create an instance of the class `InvoicesController` and invoking the method `ProcessPayInvoiceAsync`.


```markdown
   InvoicesController invoicesController = client.InvoicesController;
```

```markdown
  ProcessPayInvoiceAsync(
    int id,
    Models.ICGAPIProcessWebAPIModelsTransactionsProcessRequest request)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
int id = 112;
var request = new ICGAPIProcessWebAPIModelsTransactionsProcessRequest();
request.Amount = 131.88;
request.Type = TypeEnum.V;

try
{
    ICGTransactionsModelsResponsesProcessResponse result = await invoicesController.ProcessPayInvoiceAsync(id, request);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "invoicesController" object fails to process a transaction that was anticipated to be returned. The invoice id, payment amount and payment method type in the request object will be passed as a parameters to the `ProcessPayInvoiceAsync` method. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail   
This API call requires **id** (int type), **request** object as the mandatory parameters to process the transaction successfully. The id is the invoice number which is unique for each invoice. The request object will contain further parameters includes Amount (double type), Laneid (string type), CashBackAmount (double type),  metadata (string type), deviceSerialNumber (string type) along with Type, Description (string type), Invoices, Customer, Method, and IMetadata objects. The required parameter for the request object are transaction type and transaction amount.
 
 ![1  invoice ](https://user-images.githubusercontent.com/110983629/191497035-613e2de6-066e-4813-88a8-79cc4af601b3.png)

The class name of **request** object is
```markdown 
    ICGAPIProcessWebAPIModelsTransactionsProcessRequest
```

#### Request object parameters

![2](https://user-images.githubusercontent.com/110983629/191497464-010882ea-a216-43e9-a62d-fd3f722bce16.png)

#### Explorer 

|Name|Description|
|-----|-----------|
|request object|[Models.ICGAPIProcessWebAPIModelsTransactionsProcessRequest](https://developers.icheckdev.com/Process/#/net-standard-library/models/structures/icg-api-process-web-api-models-transactions-process-request)


#### Responses 
The response of this endpoint service request contains the `Task<Models.ICGTransactionsModelsResponsesProcessResponse>` object. The class name of this object is 

```markdown
  ICGTransactionsModelsResponsesProcessResponse
``` 

#### Response body-JSON  
```markdown
 {
  "TransactionAmount": null,
  "TransactionDate": null,
  "RawRequest": null,
  "RawResponse": null,
  "Status": null,
  "StatusMessage": null,
  "ConfirmationCode": null,
  "ApprovalCode": null,
  "CvcResponse": null,
  "AvsResponse": null,
  "CardDisplay": null,
  "CardType": null,
  "Arpc": null,
  "ErrorData": null,
  "IssuerScript": null,
  "IssuerScript2": null,
  "ApplicationId": null,
  "ReferenceNumber": null,
  "ExtraData": null,
  "TransactionId": null
}    
```

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

    
##### 'Task<Models.ICGTransactionsModelsResponsesProcessResponse>' Object Parameters
 
![3](https://user-images.githubusercontent.com/110983629/191502279-7a75b9da-d6dc-4f4b-84f1-3495dbef9f4e.png)

  
#### Explorer 

|Name|Description|
|-----|-----------|
|Response type|[Task<Models.ICGTransactionsModelsResponsesProcessResponse>](https://developers.icheckdev.com/Process/#/net-standard-library/models/structures/icg-transactions-models-responses-process-response)
 


#### Errors
  
Here is the list of errors that the API might throw.
  
|HTTP Status Code|Error Description| Exception Class|
|------|-----|----------|
|400|Bad Request|`ApiException`|
 

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, the 400 code in the 4xx range indicate an error that failed given the information provided (e.g., bad request etc.) 
 
  




  
## API Endpoints
## Merchants
### Merchants Activate Merchant
#### Description
 
This API endpoint will allow the user to activate merchant for executing the transactions. In order to activate merchant, the merchant code which is a unique identifier will be employed. To accomplish that, the API Client will create an instance of the class `MerchantsController` and invoking the method `MerchantsActivateMerchantAsync`.


```markdown
  MerchantsController merchantsController = client.MerchantsController;
```

```markdown
  MerchantsActivateMerchantAsync(
    string code)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
string code = "code8";
try
{
    string result = await merchantsController.MerchantsActivateMerchantAsync(code);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "merchantsController" object fails to activate merchant that was anticipated to be returned. The merchant code will be passed as a parameter to the `MerchantsActivateMerchantAsync` method. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail   
This API call requires **code** (string type) as the mandatory parameter to activate the merchant for processing his transactions successfully. 

![4](https://user-images.githubusercontent.com/110983629/191505904-70e9b921-d52a-4f99-aacd-c7ffbab6657d.png)

#### Responses 
The response of this endpoint service request contains the `Task<string>` object that returns the value for activating the merchant account for transactions.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
 





### Merchants Is Merchant Ready
#### Description
 
This API endpoint will allow the user to verify that the merchant is ready for making transactions or not. In order to verify specific merchant, the merchant code which is a unique identifier will be employed. To accomplish that, the API Client will create an instance of the class `MerchantsController` and invoking the method `MerchantsIsMerchantReadyAsync`.

```markdown
 MerchantsIsMerchantReadyAsync(
    string code)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
string code = "code8";
try
{
    ICGTransactionsModelsResponsesMerchantReadyResponse result = await merchantsController.MerchantsIsMerchantReadyAsync(code);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "merchantsController" object fails to verify merchant that was anticipated to be returned. The merchant code will be passed as a parameter to the `MerchantsIsMerchantReadyAsync` method. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail    
This API call requires **code** (string type) as the mandatory parameter to verify the merchant for processing his transactions successfully. It is the pre-requisite for making transaction successfully.

![4](https://user-images.githubusercontent.com/110983629/191505904-70e9b921-d52a-4f99-aacd-c7ffbab6657d.png)

#### Responses 
The response of this endpoint service request contains the `Task<Models.ICGTransactionsModelsResponsesMerchantReadyResponse>` object that returns the value for verifying the merchant account for transactions.

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
 

#### Response body-JSON
```markdown
{
  "Ready": null,
  "Message": null
}
```
The class name of **Task<Models.ICGTransactionsModelsResponsesMerchantReadyResponse>** object is
```markdown
   ICGTransactionsModelsResponsesMerchantReadyResponse
```

#### Task<Models.ICGTransactionsModelsResponsesMerchantReadyResponse> object parameters

![5](https://user-images.githubusercontent.com/110983629/191512079-ba8916bc-f1a2-4a53-a6b6-aae11ad12abe.png)


#### Explorer 

|Name|Description|
|-----|-----------|
|Response type|[Task<Models.ICGTransactionsModelsResponsesMerchantReadyResponse>](https://developers.icheckdev.com/Process/#/net-standard-library/models/structures/icg-transactions-models-responses-merchant-ready-response)
 


#### Errors
  
Here is the list of errors that the API might throw.
  
|HTTP Status Code|Error Description| Exception Class|
|------|-----|----------|
|400|Bad Request|`ApiException`|
 

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, the 400 code in the 4xx range indicate an error that failed given the information provided (e.g., bad request etc.) 







### Merchants Merchant Provisioning
#### Description
 
This API endpoint will allow the user to retrieve the data about merchant provisioning. To accomplish that, the API Client will create an instance of the class `MerchantsController` for invoking the method `MerchantsMerchantProvisioningAsync`.

```markdown
  MerchantsMerchantProvisioningAsync()
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
try
{
    List<ICGDataEntitiesMerchantsProvisioning> result = await merchantsController.MerchantsMerchantProvisioningAsync();
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "merchantsController" object fails to get the merchant provisions that was anticipated to be returned. There will be no parameter passed to the `MerchantsIsMerchantReadyAsync` method call. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail    
This endpoint does not require any parameter.

#### Responses 
The response of this endpoint service request contains the `Task<List<Models.ICGDataEntitiesMerchantsProvisioning>>` object that returns the value for merchant provisioning.

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
 

#### Response body-JSON
```markdown
 {
  "id": null,
  "data": "data0",
  "created": null
}
```
The class name of **Task<List<Models.ICGDataEntitiesMerchantsProvisioning>>** object is
```markdown
    ICGDataEntitiesMerchantsProvisioning
```

#### Task<List<Models.ICGDataEntitiesMerchantsProvisioning>> object parameters
 
 ![6](https://user-images.githubusercontent.com/110983629/191519323-035a7632-39b4-43ea-809d-1180257d7e41.png)


#### Explorer 

|Name|Description|
|-----|-----------|
|Response type|[Task<List<Models.ICGDataEntitiesMerchantsProvisioning>>](https://developers.icheckdev.com/Process/#/net-standard-library/models/structures/icg-data-entities-merchants-provisioning)
 


#### Errors
  
Here is the list of errors that the API might throw.
  
|HTTP Status Code|Error Description| Exception Class|
|------|-----|----------|
|400|Bad Request|`ApiException`|
 

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, the 400 code in the 4xx range indicate an error that failed given the information provided (e.g., bad request etc.) 






### Merchants Merchant Provisioning 1
#### Description
 
This API endpoint will allow the user to retrieve the data about merchant provisioning by entering the content details. To accomplish that, the API Client will create an instance of the class `MerchantsController` for invoking the method `MerchantsMerchantProvisioning1Async`.

```markdown
   MerchantsMerchantProvisioning1Async(
    object content)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
object content = ApiHelper.JsonDeserialize<Object>("{\"key1\":\"val1\",\"key2\":\"val2\"}");
try
{
    ICGDataEntitiesMerchantsProvisioning result = await merchantsController.MerchantsMerchantProvisioning1Async(content);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "merchantsController" object fails to get the merchant provisions that was anticipated to be returned. The content object will be passed as parameter to the `MerchantsMerchantProvisioning1Async` method. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail    
This endpoint requires **content** object that further contains the key, value pair for merchant Provisioning.

#### content object

![7](https://user-images.githubusercontent.com/110983629/191522041-744942fd-35cc-4682-b428-b680454a444f.png)



#### Responses 
The response of this endpoint service request contains the `Task<Models.ICGDataEntitiesMerchantsProvisioning>` object that returns the value for merchant provisioning.

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
 

#### Response body-JSON
```markdown
 {
  "id": null,
  "data": "data0",
  "created": null
}
```
The class name of **Task<Models.ICGDataEntitiesMerchantsProvisioning>** object is
```markdown
     ICGDataEntitiesMerchantsProvisioning
```

#### Task<Models.ICGDataEntitiesMerchantsProvisioning> object parameters
  
![8](https://user-images.githubusercontent.com/110983629/191522828-3b6cadea-3223-494f-b69c-552a0b76e64f.png)


#### Explorer 

|Name|Description|
|-----|-----------|
|Response type|[Task<Models.ICGDataEntitiesMerchantsProvisioning>](https://developers.icheckdev.com/Process/#/net-standard-library/models/structures/icg-data-entities-merchants-provisioning)
 


#### Errors
  
Here is the list of errors that the API might throw.
  
|HTTP Status Code|Error Description| Exception Class|
|------|-----|----------|
|400|Bad Request|`ApiException`|
 

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, the 400 code in the 4xx range indicate an error that failed given the information provided (e.g., bad request etc.) 








### Merchants Merchant Provisioning 2
#### Description
 
This API endpoint will allow the user to retrieve the data about merchant provisioning by entering the name and filter details. To accomplish that, the API Client will create an instance of the class `MerchantsController` for invoking the method `MerchantsMerchantProvisioning2Async`.

```markdown
    MerchantsMerchantProvisioning2Async(
    string filter,
    string name)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
string filter = "filter4";
string name = "name0";
try
{
    List<ICGDataEntitiesMerchantsProvisioning> result = await merchantsController.MerchantsMerchantProvisioning2Async(filter, name);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "merchantsController" object fails to get the merchant provisions that was anticipated to be returned. The filter and name will be passed as parameter to the `MerchantsMerchantProvisioning2Async` method. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail     
This endpoint requires **filter** (string type) and **name** (string type)  where the name will be the used for retrieving the merchant Provisioning. and filter will used for retrieving the specific merchant provision details. 

![9](https://user-images.githubusercontent.com/110983629/191525718-261da011-12b2-47df-a1e4-d95c158e26ac.png)



#### Responses 
The response of this endpoint service request contains the `Task<List<Models.ICGDataEntitiesMerchantsProvisioning>>` object that returns the value for merchant provisioning.

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
 

#### Response body-JSON
```markdown
 {
  "id": null,
  "data": "data0",
  "created": null
}
```
The class name of **Task<List<Models.ICGDataEntitiesMerchantsProvisioning>>** object is
```markdown
     ICGDataEntitiesMerchantsProvisioning
```

#### Task<Models.ICGDataEntitiesMerchantsProvisioning> object parameters
  
![8](https://user-images.githubusercontent.com/110983629/191522828-3b6cadea-3223-494f-b69c-552a0b76e64f.png)


#### Explorer 

|Name|Description|
|-----|-----------|
|Response type|[Task<Models.ICGDataEntitiesMerchantsProvisioning>](https://developers.icheckdev.com/Process/#/net-standard-library/models/structures/icg-data-entities-merchants-provisioning)
 

#### Errors
  
Here is the list of errors that the API might throw.
  
|HTTP Status Code|Error Description| Exception Class|
|------|-----|----------|
|400|Bad Request|`ApiException`|
 

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, the 400 code in the 4xx range indicate an error that failed given the information provided (e.g., bad request etc.) 





## API Endpoints
## Portal
### Portal Portal 
#### Description
 
This API endpoint will allow the user to retrieve the documentation generated by the system that consist of the static files.  These static files are ready to be deployed. To accomplish that, the API Client will create an instance of the class `PortalController` for invoking the method `PortalPortalAsync`.


```markdown
 PortalController portalController = client.PortalController;
```

```markdown
   PortalPortalAsync()
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
try
{
    object result = await portalController.PortalPortalAsync();
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "portalController" object fails to returns the documentation files that was anticipated to be returned. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail   
This endpoint does not require any parameter.

#### Responses 
The response of this endpoint service request contains the `Task<object>` object that returns the data for portal static files that needs to be deployed.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
 







## API Endpoints
## Settlements 
### Settlements Detail Update Settlement Detail 
#### Description
 
This API endpoint will allow the user to update the settlement details through the Processor Settlement identifier which is unique for each settlement. To accomplish that, the API Client will create an instance of the class `SettlementsController` for invoking the method `SettlementsDetailUpdateSettlementDetailAsync`.


```markdown
  SettlementsController settlementsController = client.SettlementsController;
```

```markdown
   SettlementsDetailUpdateSettlementDetailAsync(int id)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
int id = 112;
try
{
    bool? result = await settlementsController.SettlementsDetailUpdateSettlementDetailAsync(id);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "settlementsController" object fails to update settlements that was anticipated to be returned. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail   
This endpoint requires only one parameter which is **id** (int type) that is Processor Settlement identifier for updating the settlement. 

![10](https://user-images.githubusercontent.com/110983629/191534379-a2068234-0cec-4e38-bc7f-b04e0f6c4089.png)

 
#### Responses 
The response of this endpoint service request contains the `Task<bool>` object that returns value whether the settlement get updated or not.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
 





## API Endpoints
## Settlements Reports Groups  
### Settlements Detail Run Job Now
#### Description
 
This API endpoint will allow the user to run job now through the groupid. To accomplish that, the API Client will create an instance of the class `SettlementsReportsGroupsController` for invoking the method `SettlementsDetailRunJobNowAsync`.


```markdown
 SettlementsReportsGroupsController settlementsReportsGroupsController = client.SettlementsReportsGroupsController;
```

```markdown
 SettlementsDetailRunJobNowAsync(
    int groupid)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
int groupid = 40;
try
{
    bool? result = await settlementsReportsGroupsController.SettlementsDetailRunJobNowAsync(groupid);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "settlementsReportsGroupsController" object fails to run job that was anticipated to be returned. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail   
This endpoint requires only one parameter which is **groupid** (int type) that is mandatory for executing the job properly.
 
 ![11](https://user-images.githubusercontent.com/110983629/191537088-0718d0da-60bc-4159-a1eb-4848070fd453.png)

 
#### Responses 
The response of this endpoint service request contains the `Task<bool>` object that returns value whether the the job get executed or not.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
 



### O Data Settlements Reports Groups
#### Description
 
This API endpoint will allow the user to retrieve all items from the settlement report group. To accomplish that, the API Client will create an instance of the class `SettlementsReportsGroupsController` for invoking the method `ODataSettlementsReportsGroupsAsync`.
 

```markdown
  ODataSettlementsReportsGroupsAsync()
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
try
{
    await settlementsReportsGroupsController.ODataSettlementsReportsGroupsAsync();
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "settlementsReportsGroupsController" object fails to retrieve settlement data that was anticipated to be returned. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail   
This endpoint does not take any parameter.

 
#### Responses 
The response of this endpoint service request contains the `Task` object that returns data for the settlement reports.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
 



### O Data Settlements Reports Groups 1
#### Description
 
This API endpoint will allow the user to retrieve one item from the settlement report group by entering the unique settlement report group id. To accomplish that, the API Client will create an instance of the class `SettlementsReportsGroupsController` for invoking the method `ODataSettlementsReportsGroups1Async`.
 

```markdown
   ODataSettlementsReportsGroups1Async(
    int key)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
int key = 120;
try
{
    await settlementsReportsGroupsController.ODataSettlementsReportsGroups1Async(key);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "settlementsReportsGroupsController" object fails to retrieve settlement data that was anticipated to be returned. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail    
This endpoint requires only one parameter **key** (int type) for retrieving one instance of the settlement report group.

![12](https://user-images.githubusercontent.com/110983629/191541044-17981a59-2ce0-4ceb-bed2-659a60179541.png)

 
#### Responses 
The response of this endpoint service request contains the `Task` object that returns data for the one settlement report.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
 























