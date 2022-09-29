
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
The response of this endpoint service request contains the `Task<bool>` object that returns value whether the job get executed or not.
 
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
 






## API Endpoints
## Tokens 
### Tokens Save Credit Card Token
#### Description
 
This API endpoint will allow the user to save the credit card token. For successfully saving credit card token, you need to follow the constraints that are applied on the token, address, zipcode, cardnumber etc. To accomplish that, the API Client will create an instance of the class `TokensController` for invoking the method `TokensSaveCreditCardTokenAsync`.


```markdown 
    TokensController tokensController = client.TokensController;
```

```markdown
  TokensSaveCreditCardTokenAsync(
    Models.ICGBusinessEntitiesCreditCardTokens model)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
var model = new ICGBusinessEntitiesCreditCardTokens();
model.SiteId = "SiteId8";
model.Number = "Number8";
model.Name = "Name8";
try
{
    string result = await tokensController.TokensSaveCreditCardTokenAsync(model);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "tokensController" object fails to save the credit card token that was anticipated to be returned. The model object of `ICGBusinessEntitiesCreditCardTokens` type will be passed as parameter to the method `TokensSaveCreditCardTokenAsync`. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail   
This endpoint requires only one parameter which is **model** object that further contains the Id (int type), SiteId (string type), Token (string type), Number (string type), Name (string type), ExpDate (int type), Display (string type), Address (string type), ZipCode (string type), and CardInfo (string type). From all of these parameters, the SiteId, Number, Name are required for the user to enter for saving the credit card token. 

The class name of **model** object is
```markdown
  ICGBusinessEntitiesCreditCardTokens
```

#### model object parameters

![13](https://user-images.githubusercontent.com/110983629/191744592-f6a67ae8-2be6-4fa4-907d-e8f6c94b2652.png)


#### Explorer 

|Name|Description|
|-----|-----------|
|model|[Models.ICGBusinessEntitiesCreditCardTokens](https://developers.icheckdev.com/Process/#/net-standard-library/models/structures/icg-business-entities-credit-card-tokens)
 
#### Responses 
The response of this endpoint service request contains the `Task<string>` object that returns value for saving token.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
 
#### Errors
  
Here is the list of errors that the API might throw.
  
|HTTP Status Code|Error Description| Exception Class|
|------|-----|----------|
|400|Bad Request|`ApiException`|
 

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, the 400 code in the 4xx range indicate an error that failed given the information provided (e.g., bad request etc.) 




### Tokens Update Credit Card Token
#### Description
This API endpoint will allow the user to update the credit card token. For successfully editing credit card token, you need to follow the constraints that are applied on the token, address, zipcode, cardnumber etc. To accomplish that, the API Client will create an instance of the class `TokensController` for invoking the method `TokensUpdateCreditCardTokenAsync`.

```markdown
   TokensUpdateCreditCardTokenAsync(
    Models.ICGBusinessEntitiesCreditCardTokens model)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
var model = new ICGBusinessEntitiesCreditCardTokens();
model.SiteId = "SiteId8";
model.Number = "Number8";
model.Name = "Name8";

try
{
    string result = await tokensController.TokensUpdateCreditCardTokenAsync(model);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "tokensController" object fails to update the credit card token that was anticipated to be returned. The model object of `ICGBusinessEntitiesCreditCardTokens` type will be passed as parameter to the method `TokensSaveCreditCardTokenAsync`. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail   
This endpoint requires only one parameter which is **model** object that further contains the Id (int type), SiteId (string type), Token (string type), Number (string type), Name (string type), ExpDate (int type), Display (string type), Address (string type), ZipCode (string type), and CardInfo (string type). From all of these parameters, the SiteId, Number, Name are required for the user to enter for updating the credit card token. 

The class name of **model** object is
```markdown
   ICGBusinessEntitiesCreditCardTokens
```

#### model object parameters

![13](https://user-images.githubusercontent.com/110983629/191744592-f6a67ae8-2be6-4fa4-907d-e8f6c94b2652.png)


#### Explorer 

|Name|Description|
|-----|-----------|
|model|[Models.ICGBusinessEntitiesCreditCardTokens](https://developers.icheckdev.com/Process/#/net-standard-library/models/structures/icg-business-entities-credit-card-tokens)
 
#### Responses 
The response of this endpoint service request contains the `Task<string>` object that returns value for updating token details.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
 
#### Errors
  
Here is the list of errors that the API might throw.
  
|HTTP Status Code|Error Description| Exception Class|
|------|-----|----------|
|400|Bad Request|`ApiException`|
 

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, the 400 code in the 4xx range indicate an error that failed given the information provided (e.g., bad request etc.) 




### Tokens Delete Credit Card Token
#### Description
This API endpoint will allow the user to delete the credit card token. For successfully deleting credit card token, you need to provide the merchant's site identifier and credit card token. To accomplish that, the API Client will create an instance of the class `TokensController` for invoking the method `TokensDeleteCreditCardTokenAsync`.

```markdown 
   TokensDeleteCreditCardTokenAsync(
    string siteId,
    string token)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
string siteId = "siteId8";
string token = "token6";
try
{
    string result = await tokensController.TokensDeleteCreditCardTokenAsync(siteId, token);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "tokensController" object fails to delete the credit card token that was anticipated to be returned. The siteId and token will be passed as parameters to the method `TokensDeleteCreditCardTokenAsync`. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail   
This endpoint requires two parameters which are **siteId** (string type) and **token** (string type). The siteId will be the merchant's site id whose credit card token need to be deleted. 
 
![14](https://user-images.githubusercontent.com/110983629/191760246-e5efafc4-ccbb-4e54-a1b7-0cb9a61898b2.png)

 
#### Responses 
The response of this endpoint service request contains the `Task<string>` object that returns value for deleting the merchant's credit card token.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
 
#### Errors
  
Here is the list of errors that the API might throw.
  
|HTTP Status Code|Error Description| Exception Class|
|------|-----|----------|
|400|Bad Request|`ApiException`|
 

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, the 400 code in the 4xx range indicate an error that failed given the information provided (e.g., bad request etc.) 






### Tokens Get Credit Card Token
#### Description
This API endpoint will allow the user to retrieve the credit card token details of a merchant by accessing it through the merchant's site identifier and credit card token. To accomplish that, the API Client will create an instance of the class `TokensController` for invoking the method `TokensGetCreditCardTokenAsync`.

```markdown 
   TokensGetCreditCardTokenAsync(
    string siteId,
    string token)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
string siteId = "siteId8";
string token = "token6";

try
{
    ICGBusinessEntitiesCreditCardTokens result = await tokensController.TokensGetCreditCardTokenAsync(siteId, token);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "tokensController" object fails to retrieve the credit card token details that was anticipated to be returned. The siteId and token will be passed as parameters to the method `TokensGetCreditCardTokenAsync`. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail   
This endpoint requires two parameters which are **siteId** (string type) and **token** (string type). The siteId will be the merchant's site id whose credit card token details need to be retrieved. 
  
![15](https://user-images.githubusercontent.com/110983629/191762772-d37456b0-bb40-410d-96d0-5f15856fef4f.png)

 
#### Responses 
The response of this endpoint service request contains the `Task<Models.ICGBusinessEntitiesCreditCardTokens>` object that returns detail of merchant credit card token. 
 

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

#### Response Body-JSON
```markdown
{
  "Id": null,
  "SiteId": "SiteId0",
  "Token": null,
  "Number": "Number0",
  "Name": "Name0",
  "ExpDate": null,
  "Display": null,
  "Address": null,
  "ZipCode": null,
  "CardInfo": null
}
``` 
The class name of Task<Models.ICGBusinessEntitiesCreditCardTokens> is
```markdown
   ICGBusinessEntitiesCreditCardTokens
```


#### Task<Models.ICGBusinessEntitiesCreditCardTokens> object parameters

![16](https://user-images.githubusercontent.com/110983629/191764742-e36ae96e-ec44-4a1f-824e-9f952a35e886.png)
 
 
#### Errors
  
Here is the list of errors that the API might throw.
  
|HTTP Status Code|Error Description| Exception Class|
|------|-----|----------|
|400|Bad Request|`ApiException`|
 

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, the 400 code in the 4xx range indicate an error that failed given the information provided (e.g., bad request etc.) 







### Tokens Get Credit Card Token List
#### Description
This API endpoint will allow the user to retrieve the credit card token list of a merchant by accessing it through the merchant's site identifier. To accomplish that, the API Client will create an instance of the class `TokensController` for invoking the method `TokensGetCreditCardTokenListAsync`.

```markdown 
   TokensGetCreditCardTokenListAsync(
    string siteId)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
string siteId = "siteId8";
try
{
    List<ICGBusinessEntitiesCreditCardTokens> result = await tokensController.TokensGetCreditCardTokenListAsync(siteId);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "tokensController" object fails to retrieve the credit card token list that was anticipated to be returned. The siteId will be passed as parameter to the method `TokensGetCreditCardTokenAsync`. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail   
This endpoint requires only one parameter which is **siteId** (string type). The siteId will be the merchant's site id whose credit card token list need to be retrieved. 
  
![17](https://user-images.githubusercontent.com/110983629/191771741-0098e22d-daee-452d-9c4d-7b4578d05f47.png)

  
#### Responses 
The response of this endpoint service request contains the **Task<List<Models.ICGBusinessEntitiesCreditCardTokens>>** object that returns list of merchant credit card token. 
 

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

#### Response Body-JSON
```markdown
 {
  "Id": null,
  "SiteId": "SiteId0",
  "Token": null,
  "Number": "Number0",
  "Name": "Name0",
  "ExpDate": null,
  "Display": null,
  "Address": null,
  "ZipCode": null,
  "CardInfo": null
}
```

The class name of Task<List<Models.ICGBusinessEntitiesCreditCardTokens>> is
```markdown
   ICGBusinessEntitiesCreditCardTokens
```


#### Task<List<Models.ICGBusinessEntitiesCreditCardTokens>> object parameters
 
![18](https://user-images.githubusercontent.com/110983629/191772677-11b74d34-1a73-4d43-938c-ba81e4576998.png)

 
#### Errors
  
Here is the list of errors that the API might throw.
  
|HTTP Status Code|Error Description| Exception Class|
|------|-----|----------|
|400|Bad Request|`ApiException`|
 

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, the 400 code in the 4xx range indicate an error that failed given the information provided (e.g., bad request etc.) 








### Tokens Get All Credit Card Token Listby Date
#### Description
This API endpoint will allow the user to retrieve the credit card token list of the merchants accessing them by entering the start date and end date. To accomplish that, the API Client will create an instance of the class `TokensController` for invoking the method `TokensGetAllCreditCardTokenListbyDateAsync`.

```markdown 
   TokensGetAllCreditCardTokenListbyDateAsync(
    string siteId,
    DateTime start,
    DateTime end)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
string siteId = "siteId8";
DateTime start = DateTime.Parse("2016-03-13T12:52:32.123Z");
DateTime end = DateTime.Parse("2016-03-13T12:52:32.123Z");

try
{
    List<ICGBusinessEntitiesCreditCardTokens> result = await tokensController.TokensGetAllCreditCardTokenListbyDateAsync(siteId, start, end);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "tokensController" object fails to retrieve the specific credit card token list that was anticipated to be returned. The siteId, start and end will be passed as parameters to the method `TokensGetAllCreditCardTokenListbyDateAsync`. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail   
This endpoint requires three parameters which are **siteId** (string type), **start** (DateTime type) and **end** (DateTime type). The siteId will be the merchant's site id whose credit card token list need to be retrieved, and the start and end are two dates through which the token get employed by the merchant.
   
![19](https://user-images.githubusercontent.com/110983629/191963902-d88f9542-316b-4d45-b46a-d7ec74f04510.png)

  
#### Responses 
The response of this endpoint service request contains the **Task<List<Models.ICGBusinessEntitiesCreditCardTokens>>** object that returns list of merchant credit card token list for the specified dates.
 

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

#### Response Body-JSON
```markdown
 {
  "Id": null,
  "SiteId": "SiteId0",
  "Token": null,
  "Number": "Number0",
  "Name": "Name0",
  "ExpDate": null,
  "Display": null,
  "Address": null,
  "ZipCode": null,
  "CardInfo": null
}
```

The class name of Task<List<Models.ICGBusinessEntitiesCreditCardTokens>> is
```markdown
    ICGBusinessEntitiesCreditCardTokens
```


#### Task<List<Models.ICGBusinessEntitiesCreditCardTokens>> object parameters
  
![20](https://user-images.githubusercontent.com/110983629/191964443-16519201-c6b5-41ad-810c-f423ad18f363.png)
  
 
#### Errors
  
Here is the list of errors that the API might throw.
  
|HTTP Status Code|Error Description| Exception Class|
|------|-----|----------|
|400|Bad Request|`ApiException`|
 

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, the 400 code in the 4xx range indicate an error that failed given the information provided (e.g., bad request etc.) 




### Tokens Save Check Token
#### Description
 
This API endpoint will allow the user to save the check token. For successfully saving check token, you need to follow the constraints that are applied on the token, Authorization, Account, AccounType etc. To accomplish that, the API Client will create an instance of the class `TokensController` for invoking the method `TokensSaveCheckTokenAsync`.

```markdown
  TokensSaveCheckTokenAsync(
    Models.ICGBusinessEntitiesCheckTokens model)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
var model = new ICGBusinessEntitiesCheckTokens();
model.SiteId = "SiteId8";
model.Account = "Account6";
model.AccountType = "AccountType2";
model.Routing = "Routing8";

try
{
    string result = await tokensController.TokensSaveCheckTokenAsync(model);
}
catch (ApiException e){}; 
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "tokensController" object fails to save the check token that was anticipated to be returned. The model object of `ICGBusinessEntitiesCheckTokens` type will be passed as parameter to the method `TokensSaveCheckTokenAsync`. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail   
This endpoint requires one parameter which is **model** object that further contains the Id (int type), SiteId (string type), Token (string type), Authorization (string type), Account (string type), AccountType (int type), Routing (string type), and Display (string type). From all of these parameters, the SiteId, Account, AccountType and Routing are required for the user to enter for saving the check token. 

The class name of **model** object is
```markdown
   ICGBusinessEntitiesCheckTokens
```

#### model object parameters

![21](https://user-images.githubusercontent.com/110983629/191967757-542b0837-3046-4c72-a75c-231af81eb016.png)

#### Explorer 

|Name|Description|
|-----|-----------|
|model|[Models.ICGBusinessEntitiesCheckTokens](https://developers.icheckdev.com/Process/#/net-standard-library/models/structures/icg-business-entities-check-tokens)
 
#### Responses 
The response of this endpoint service request contains the `Task<string>` object that returns value for saving check token.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
 
#### Errors
  
Here is the list of errors that the API might throw.
  
|HTTP Status Code|Error Description| Exception Class|
|------|-----|----------|
|400|Bad Request|`ApiException`|
 

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, the 400 code in the 4xx range indicate an error that failed given the information provided (e.g., bad request etc.) 




### Tokens Update Check Token
#### Description
This API endpoint will allow the user to update the check token. For successfully editing check token, you need to follow the constraints that are applied on the token, Authorization, Account, AccounType etc. To accomplish that, the API Client will create an instance of the class `TokensController` for invoking the method `TokensUpdateCheckTokenAsync`.

```markdown
   TokensUpdateCheckTokenAsync(
    Models.ICGBusinessEntitiesCheckTokens model)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
var model = new ICGBusinessEntitiesCheckTokens();
model.SiteId = "SiteId8";
model.Account = "Account6";
model.AccountType = "AccountType2";
model.Routing = "Routing8";

try
{
    string result = await tokensController.TokensUpdateCheckTokenAsync(model);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "tokensController" object fails to update the check token that was anticipated to be returned. The model object of `ICGBusinessEntitiesCheckTokens` type will be passed as parameter to the method `TokensUpdateCheckTokenAsync`. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail   
This endpoint requires only one parameter which is **model** object that further contains the Id (int type), SiteId (string type), Token (string type), Authorization (string type), Account (string type), AccountType (int type), Routing (string type), and Display (string type). From all of these parameters, the SiteId, Account, AccountType, and Routing are required for the user to enter for updating the check token. 

The class name of **model** object is
```markdown
   ICGBusinessEntitiesCheckTokens
```

#### model object parameters
 
![22](https://user-images.githubusercontent.com/110983629/191976200-020c9ee8-2cd2-492d-9554-2ae0523d0de1.png)

 
#### Explorer 

|Name|Description|
|-----|-----------|
|model|[Models.ICGBusinessEntitiesCheckTokens](https://developers.icheckdev.com/Process/#/net-standard-library/models/structures/icg-business-entities-check-tokens)
 
#### Responses 
The response of this endpoint service request contains the `Task<string>` object that returns value for updating check token details.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
 
#### Errors
  
Here is the list of errors that the API might throw.
  
|HTTP Status Code|Error Description| Exception Class|
|------|-----|----------|
|400|Bad Request|`ApiException`|
 

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, the 400 code in the 4xx range indicate an error that failed given the information provided (e.g., bad request etc.) 





### Tokens Delete Check Token
#### Description
This API endpoint will allow the user to delete the check token. For successfully deleting check token, you need to provide the merchant's site identifier and specific check token. To accomplish that, the API Client will create an instance of the class `TokensController` for invoking the method `TokensDeleteCheckTokenAsync`.

```markdown 
    TokensDeleteCheckTokenAsync(
    string siteId,
    string token)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
string siteId = "siteId8";
string token = "token6";
try
{
    string result = await tokensController.TokensDeleteCheckTokenAsync(siteId, token);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "tokensController" object fails to delete the check token that was anticipated to be returned. The siteId and token will be passed as parameters to the method `TokensDeleteCheckTokenAsync`. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail   
This endpoint requires two parameters which are **siteId** (string type) and **token** (string type). The siteId will be the merchant's site id whose check need to be deleted. 
  
![23](https://user-images.githubusercontent.com/110983629/191978150-4559302c-553d-46c0-a819-b2fae0c3afd1.png)

   
#### Responses 
The response of this endpoint service request contains the `Task<string>` object that returns value for deleting the merchant's specific check token.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
 
#### Errors
  
Here is the list of errors that the API might throw.
  
|HTTP Status Code|Error Description| Exception Class|
|------|-----|----------|
|400|Bad Request|`ApiException`|
 

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, the 400 code in the 4xx range indicate an error that failed given the information provided (e.g., bad request etc.) 



### Tokens Get Check Token
#### Description
This API endpoint will allow the user to retrieve the check token details of a merchant by accessing it through the merchant's site identifier and check token. To accomplish that, the API Client will create an instance of the class `TokensController` for invoking the method `TokensGetCheckTokenAsync`.

```markdown 
    TokensGetCheckTokenAsync(
    string siteId,
    string token)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
string siteId = "siteId8";
string token = "token6";
try
{
    ICGBusinessEntitiesCheckTokens result = await tokensController.TokensGetCheckTokenAsync(siteId, token);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "tokensController" object fails to retrieve the check token details that was anticipated to be returned. The siteId and token will be passed as parameters to the method `TokensGetCheckTokenAsync`. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail   
This endpoint requires two parameters which are **siteId** (string type) and **token** (string type). The siteId will be the merchant's site id whose check token details need to be retrieved. 
   
![24](https://user-images.githubusercontent.com/110983629/191980596-63fbb165-5a43-446f-9615-7769e5fa0a50.png)

 
#### Responses 
The response of this endpoint service request contains the `Task<Models.ICGBusinessEntitiesCheckTokens>` object that returns detail of merchant check token. 
 

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

#### Response Body-JSON
```markdown
 {
  "Id": null,
  "SiteId": "SiteId0",
  "Token": null,
  "Authorization": null,
  "Account": "Account8",
  "AccountType": "AccountType0",
  "Routing": "Routing6",
  "Display": null
}
``` 
The class name of Task<Models.ICGBusinessEntitiesCheckTokens> is
```markdown
    ICGBusinessEntitiesCheckTokens
```


#### Task<Models.ICGBusinessEntitiesCheckTokens> object parameters
 
![25](https://user-images.githubusercontent.com/110983629/191981155-520c9a5f-0131-4e7a-95b4-3dec622f58f2.png)

 
#### Errors
  
Here is the list of errors that the API might throw.
  
|HTTP Status Code|Error Description| Exception Class|
|------|-----|----------|
|400|Bad Request|`ApiException`|
 

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, the 400 code in the 4xx range indicate an error that failed given the information provided (e.g., bad request etc.) 






### Tokens Get Check Token List
#### Description
This API endpoint will allow the user to retrieve the check token list of a merchant by accessing it through the merchant's site identifier. To accomplish that, the API Client will create an instance of the class `TokensController` for invoking the method `TokensGetCheckTokenListAsync`.

```markdown 
   TokensGetCheckTokenListAsync(
    string siteId)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
string siteId = "siteId8";
try
{
    List<ICGBusinessEntitiesCheckTokens> result = await tokensController.TokensGetCheckTokenListAsync(siteId);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "tokensController" object fails to retrieve the check token list that was anticipated to be returned. The siteId will be passed as parameter to the method `TokensGetCheckTokenListAsync`. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail   
This endpoint requires only one parameter which is **siteId** (string type). The siteId will be the merchant's site id whose check token list need to be retrieved. 
  
![26](https://user-images.githubusercontent.com/110983629/191984337-ab21368c-230a-4fa5-a510-4636407f234e.png)

  
#### Responses 
The response of this endpoint service request contains the **Task<List<Models.ICGBusinessEntitiesCheckTokens>>** object that returns list of merchant check tokens. 
 

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

#### Response Body-JSON
```markdown
 {
  "Id": null,
  "SiteId": "SiteId0",
  "Token": null,
  "Authorization": null,
  "Account": "Account8",
  "AccountType": "AccountType0",
  "Routing": "Routing6",
  "Display": null
}
```

The class name of Task<List<Models.ICGBusinessEntitiesCheckTokens>> is
```markdown
    ICGBusinessEntitiesCheckTokens
```


#### Task<List<Models.ICGBusinessEntitiesCheckTokens>> object parameters
  
![27](https://user-images.githubusercontent.com/110983629/191984935-9874fc69-b4cd-4e42-b22c-9cb1481e4031.png)

  
 
#### Errors
  
Here is the list of errors that the API might throw.
  
|HTTP Status Code|Error Description| Exception Class|
|------|-----|----------|
|400|Bad Request|`ApiException`|
 

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, the 400 code in the 4xx range indicate an error that failed given the information provided (e.g., bad request etc.) 




### Tokens Tokenize PAN Only
#### Description
  
This API endpoint will allow the user to save the tokenize PAN of the Merchant. For successfully saving tokenize PAN, the merchant's site ID needs to provided along with the account details. To accomplish that, the API Client will create an instance of the class `TokensController` for invoking the method `TokensTokenizePANOnlyAsync`.

```markdown 
    TokensTokenizePANOnlyAsync(
    Models.ICGBusinessEntitiesPanTokens model)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
var model = new ICGBusinessEntitiesPanTokens();
try
{
    string result = await tokensController.TokensTokenizePANOnlyAsync(model);
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "tokensController" object fails to save the Tokenize PAN that was anticipated to be returned. The model object of `ICGBusinessEntitiesPanTokens` type will be passed as parameter to the method `TokensTokenizePANOnlyAsync`. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail   
This endpoint requires one parameter which is **model** object that further contains the Id (int type), SiteId (string type), Token (string type), Pan (string type), and PanDisplay (string type). Token will be of Minimum Length: 0, Maximum Length: 32, Pan will be of Minimum Length: 13, Maximum Length: 20 and PanDisplay will be of Minimum Length: 0, Maximum Length: 25. 

The class name of **model** object is
```markdown
  ICGBusinessEntitiesPanTokens    
```

#### model object parameters

![28](https://user-images.githubusercontent.com/110983629/192091777-4a5bff89-bbd6-4086-8db2-b1d1532548f6.png)

  
#### Explorer 

|Name|Description|
|-----|-----------|
|model|[Models.ICGBusinessEntitiesPanTokens](https://developers.icheckdev.com/Process/#/net-standard-library/models/structures/icg-business-entities-pan-tokens)
 
#### Responses 
The response of this endpoint service request contains the `Task<string>` object that returns value for saving tokenize PAN.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
 
#### Errors
  
Here is the list of errors that the API might throw.
  
|HTTP Status Code|Error Description| Exception Class|
|------|-----|----------|
|400|Bad Request|`ApiException`|
 

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, the 400 code in the 4xx range indicate an error that failed given the information provided (e.g., bad request etc.) 








### Tokens Validate PAN Token Bin
#### Description
  
This API endpoint will allow the user to validate a PAN Token Bin of the Merchant. For successfully verifying the PAN bin, the merchant's site ID needs to provided. To accomplish that, the API Client will create an instance of the class `TokensController` for invoking the method `TokensValidatePANTokenBinAsync`.

```markdown 
    TokensValidatePANTokenBinAsync(
    string siteID,
    string token)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
string siteID = "siteID6";
string token = "token6";
try
{
    ICGBusinessEntitiesPanTokens result = await tokensController.TokensValidatePANTokenBinAsync(siteID, token);
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "tokensController" object fails to validate PAN token bin that was anticipated to be returned. The siteID and token will be passed as parameters to the method `TokensValidatePANTokenBinAsync` for specifically validating a PAN bin of the merchant. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail   
This endpoint requires two parameters which are **siteID** (string type) and **token** (string type). The siteID will be merchant's site identifier and token is actually the merchant's PAN. 

![29](https://user-images.githubusercontent.com/110983629/192092994-001949f6-25d1-497e-ad2b-dc3a4b46518a.png)

 
#### Responses 
The response of this endpoint service request contains the `Task<Models.ICGBusinessEntitiesPanTokens>` object that returns value for validating merchant's PAN.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

#### Response Body-JSON
```markdown
 {
  "Id": null,
  "SiteId": null,
  "Token": null,
  "Pan": null,
  "PanDisplay": null
 }
```

The class name of response type Task<Models.ICGBusinessEntitiesPanTokens> is
```markdown
  ICGBusinessEntitiesPanTokens
```

#### Task<Models.ICGBusinessEntitiesPanTokens> object parameter

![30](https://user-images.githubusercontent.com/110983629/192093283-b3791e29-47d7-4881-9912-0ae300a8f6f6.png)

#### Explorer 

|Name|Description|
|-----|-----------|
|model|[Task<Models.ICGBusinessEntitiesPanTokens>](https://developers.icheckdev.com/Process/#/net-standard-library/models/structures/icg-business-entities-pan-tokens)
 

#### Errors
  
Here is the list of errors that the API might throw.
  
|HTTP Status Code|Error Description| Exception Class|
|------|-----|----------|
|400|Bad Request|`ApiException`|
 

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, the 400 code in the 4xx range indicate an error that failed given the information provided (e.g., bad request etc.) 



### Tokenize DDA Only
#### Description
  
This API endpoint will allow the user to save the tokenize DDA (demand deposit amount) of the Merchant. It is an easy way to securely make payments online. For successfully saving tokenize DDA, the merchant's site ID needs to provided along with the account details. To accomplish that, the API Client will create an instance of the class `TokensController` for invoking the method `TokensTokenizeDDAOnlyAsync`.

```markdown  
   TokensTokenizeDDAOnlyAsync(
    Models.ICGBusinessEntitiesDdaTokens model)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
var model = new ICGBusinessEntitiesDdaTokens();
try
{
    string result = await tokensController.TokensTokenizeDDAOnlyAsync(model);
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "tokensController" object fails to save the Tokenize DDA that was anticipated to be returned. The model object of `ICGBusinessEntitiesDdaTokens` type will be passed as parameter to the method `TokensTokenizeDDAOnlyAsync`. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail   
This endpoint requires one parameter which is **model** object that further contains the Id (int type), SiteId (string type), Token (string type), Acc (string type), and AccDisplay (string type). The token length will be minimum: 0, maximum: 32, Acc length will be minimum: 3, maximum: 17, and AccDisplay length will be minimum: 0, maximum: 25. 
 

The class name of **model** object is
```markdown
   ICGBusinessEntitiesDdaTokens    
```

#### model object parameters
 
![31](https://user-images.githubusercontent.com/110983629/192094105-76a2e770-f02d-4d08-891d-b1ffbbdb42d2.png)

 
#### Explorer 

|Name|Description|
|-----|-----------|
|model|[Models.ICGBusinessEntitiesDdaTokens](https://developers.icheckdev.com/Process/#/net-standard-library/models/structures/icg-business-entities-dda-tokens)
 
#### Responses 
The response of this endpoint service request contains the `Task<string>` object that returns value for saving tokenize DDA details of merchant.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
 
#### Errors
  
Here is the list of errors that the API might throw.
  
|HTTP Status Code|Error Description| Exception Class|
|------|-----|----------|
|400|Bad Request|`ApiException`|
 

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, the 400 code in the 4xx range indicate an error that failed given the information provided (e.g., bad request etc.) 







### Tokens Get Expired Credit Card Tokens
#### Description
This API endpoint will allow the user to retrieve the expired credit card token details of a merchant by accessing it through the merchant's site identifier. To accomplish that, the API Client will create an instance of the class `TokensController` for invoking the method `TokensGetExpiredCreditCardTokensAsync`.

```markdown 
 TokensGetExpiredCreditCardTokensAsync(
    string siteId)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
string siteId = "siteId8";
try
{
    List<ICGBusinessEntitiesExpiredCreditCardTokens> result = await tokensController.TokensGetExpiredCreditCardTokensAsync(siteId);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "tokensController" object fails to retrieve the expired credit card token details that was anticipated to be returned. The siteId of the merchant will be passed as parameter to the method `TokensGetExpiredCreditCardTokensAsync`. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail   
This endpoint requires one parameter which is merchant's site identifier **siteId** (string type) for specifically accessing the expired credit card details whose site id is entered.

![32](https://user-images.githubusercontent.com/110983629/192095394-8cf6c7b3-beca-42ce-bf55-1e1ab7ffabdd.png)

 
#### Responses 
The response of this endpoint service request contains the `Task<List<Models.ICGBusinessEntitiesExpiredCreditCardTokens>>` object that returns detail of merchant expired credit card token. 
 

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

#### Response Body-JSON
```markdown
 {
  "Id": null,
  "MerchantId": null,
  "SiteId": null,
  "CustomerId": null,
  "CustomerCardId": null,
  "CreditCardTokenId": null,
  "Token": null,
  "Name": null,
  "ExpDate": null,
  "Display": null,
  "Date": null
}
``` 
The class name of Task<List<Models.ICGBusinessEntitiesExpiredCreditCardTokens>> is
```markdown
    ICGBusinessEntitiesExpiredCreditCardTokens
```


#### Task<List<Models.ICGBusinessEntitiesExpiredCreditCardTokens>> object parameters

![33](https://user-images.githubusercontent.com/110983629/192095478-fad8df42-61db-4726-97a1-2756fd9294b6.png)

 
#### Errors
  
Here is the list of errors that the API might throw.
  
|HTTP Status Code|Error Description| Exception Class|
|------|-----|----------|
|400|Bad Request|`ApiException`|
 

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, the 400 code in the 4xx range indicate an error that failed given the information provided (e.g., bad request etc.) 




### Tokens Get All Expired Credit Card Tokens
#### Description 
This API endpoint will allow the user to retrieve the list of all expired credit card tokens of the merchants in order to get information of how many tokens get expired. To accomplish that, the API Client will create an instance of the class `TokensController` for invoking the method `TokensGetAllExpiredCreditCardTokensAsync`.

```markdown 
  TokensGetAllExpiredCreditCardTokensAsync()
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
try
{
    List<ICGBusinessEntitiesExpiredCreditCardTokens> result = await tokensController.TokensGetAllExpiredCreditCardTokensAsync();
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "tokensController" object fails to retrieve the expired credit card token list that was anticipated to be returned. No parameter is needed for calling the method `TokensGetAllExpiredCreditCardTokensAsync`. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail   
This endpoint does not take any parameters.  
  
#### Responses 
The response of this endpoint service request contains the **Task<List<Models.ICGBusinessEntitiesExpiredCreditCardTokens>>** object that returns list of all expired merchant's credit card token. 
 

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

#### Response Body-JSON
```markdown
 {
  "Id": null,
  "MerchantId": null,
  "SiteId": null,
  "CustomerId": null,
  "CustomerCardId": null,
  "CreditCardTokenId": null,
  "Token": null,
  "Name": null,
  "ExpDate": null,
  "Display": null,
  "Date": null
}
```

The class name of Task<List<Models.ICGBusinessEntitiesExpiredCreditCardTokens>> is
```markdown
    ICGBusinessEntitiesExpiredCreditCardTokens
```


####  Task<List<Models.ICGBusinessEntitiesExpiredCreditCardTokens>> object parameters
  
![34](https://user-images.githubusercontent.com/110983629/192096269-1e5881f5-978b-4512-afc8-309ef3fa629a.png)

 
#### Errors
  
Here is the list of errors that the API might throw.
  
|HTTP Status Code|Error Description| Exception Class|
|------|-----|----------|
|400|Bad Request|`ApiException`|
 

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, the 400 code in the 4xx range indicate an error that failed given the information provided (e.g., bad request etc.) 




## API Endpoints
## Transactions  
### Process Process Batch
#### Description
This API endpoint will allow the user to process payment request in Batch which means that many of the payments requests get processed by using this process call. For successfully processing payments in bulk, you need to provide the payment details such as transaction amount, type, Metadata etc. To accomplish that, the API Client will create an instance of the class `TransactionsController` for invoking the method `ProcessProcessBatchAsync`.  

```markdown 
    TransactionsController transactionsController = client.TransactionsController; 
```

```markdown 
  ProcessProcessBatchAsync(
    List<Models.ICGAPIProcessWebAPIModelsTransactionsProcessRequest> requests)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
var requests = new List<ICGAPIProcessWebAPIModelsTransactionsProcessRequest>();
var requests0 = new ICGAPIProcessWebAPIModelsTransactionsProcessRequest();
requests0.Amount = 207.86;
requests0.Type = TypeEnum.D;
requests.Add(requests0);
try
{
    List<ICGTransactionsModelsResponsesProcessResponse> result = await transactionsController.ProcessProcessBatchAsync(requests);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "transactionsController" object fails to process bulk payments that was anticipated to be returned. The list of requests of `ICGAPIProcessWebAPIModelsTransactionsProcessRequest` type will be passed as parameter to the method `ProcessProcessBatchAsync`. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail    
This endpoint requires **request** object that further includes Amount (double type), Laneid (string type), CashBackAmount (double type), description (string type), Metadata (string type), DeviceSerialNumber (string type) parameters along with the type, Invoices, customer, method, Imetadata objects. From all of these parameters, Transaction amount, transaction type that can be debit/sales or credit/refund are mandatory to process the payment request.


The class name of **request** object is
```markdown
   ICGAPIProcessWebAPIModelsTransactionsProcessRequest
```

#### request object parameters

![35](https://user-images.githubusercontent.com/110983629/192098751-3cb4b57e-fa53-4254-8d5b-173c7e8baf31.png)


#### Explorer 

|Name|Description|
|-----|-----------|
|request|[List<Models.ICGAPIProcessWebAPIModelsTransactionsProcessRequest>](https://developers.icheckdev.com/Process/#/net-standard-library/models/structures/icg-api-process-web-api-models-transactions-process-request)
 
#### Responses 
The response of this endpoint service request contains the `Task<List<Models.ICGTransactionsModelsResponsesProcessResponse>>` object that returns value for processing payment.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
 
#### Response Body-JSON 
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

#### Explorer 

|Name|Description|
|-----|-----------|
|response type|[Task<List<Models.ICGTransactionsModelsResponsesProcessResponse>>](https://developers.icheckdev.com/Process/#/net-standard-library/models/structures/icg-transactions-models-responses-process-response)

 
#### Errors
  
Here is the list of errors that the API might throw.
  
|HTTP Status Code|Error Description| Exception Class|
|------|-----|----------|
|400|Bad Request|`ApiException`|
 

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, the 400 code in the 4xx range indicate an error that failed given the information provided (e.g., bad request etc.) 





### Process Process Batch Async
#### Description
This API endpoint will allow the user to process payment request in Batch which means that many of the payments requests get processed by using this process call. For successfully processing payments in bulk, you need to provide the payment details such as transaction amount, type, Metadata etc. To accomplish that, the API Client will create an instance of the class `TransactionsController` for invoking the method `ProcessProcessBatchAsyncAsync`.  

```markdown 
  ProcessProcessBatchAsyncAsync(
    List<Models.ICGAPIProcessWebAPIModelsTransactionsProcessRequest> requests)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
var requests = new List<ICGAPIProcessWebAPIModelsTransactionsProcessRequest>();
var requests0 = new ICGAPIProcessWebAPIModelsTransactionsProcessRequest();
requests0.Amount = 207.86;
requests0.Type = TypeEnum.D;
requests.Add(requests0);
try
{
    string result = await transactionsController.ProcessProcessBatchAsyncAsync(requests);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "transactionsController" object fails to process bulk payments that was anticipated to be returned. The list of requests of `ICGAPIProcessWebAPIModelsTransactionsProcessRequest` type will be passed as parameter to the method `ProcessProcessBatchAsyncAsync`. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail    
This endpoint requires **request** object that further includes Amount (double type), Laneid (string type), CashBackAmount (double type), description (string type), Metadata (string type), DeviceSerialNumber (string type) parameters along with the type, Invoices, customer, method, Imetadata objects. From all of these parameters, Transaction amount, transaction type that can be debit/sales or credit/refund are mandatory to process the payment request.


The class name of **request** object is
```markdown
   ICGAPIProcessWebAPIModelsTransactionsProcessRequest
```

#### request object parameters

![35](https://user-images.githubusercontent.com/110983629/192098751-3cb4b57e-fa53-4254-8d5b-173c7e8baf31.png)


#### Explorer 

|Name|Description|
|-----|-----------|
|request|[List<Models.ICGAPIProcessWebAPIModelsTransactionsProcessRequest>](https://developers.icheckdev.com/Process/#/net-standard-library/models/structures/icg-api-process-web-api-models-transactions-process-request)
 
#### Responses 
The response of this endpoint service request contains the `Task<string>` object that returns value for processing payment.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
 
  
#### Errors
  
Here is the list of errors that the API might throw.
  
|HTTP Status Code|Error Description| Exception Class|
|------|-----|----------|
|400|Bad Request|`ApiException`|
 

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, the 400 code in the 4xx range indicate an error that failed given the information provided (e.g., bad request etc.) 
 



### Process Process Batch Status
#### Description
This API endpoint will allow the user to retrieve the status of previously created Batch payment in which many of the payment requests get processed by once. For successfully getting status of bulk payments, you need to provide the unique batch id. To accomplish that, the API Client will create an instance of the class `TransactionsController` for invoking the method `ProcessProcessBatchStatusAsync`.  

```markdown 
    ProcessProcessBatchStatusAsync(
    string batchId)
```
 
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
string batchId = "batchId2";
try
{
    ICGAPIProcessWebAPIModelsTransactionsBatchProcessModel result = await transactionsController.ProcessProcessBatchStatusAsync(batchId);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "transactionsController" object fails to retrieve bulk payment status that was anticipated to be returned. The batchid will be passed as parameter to the method `ProcessProcessBatchStatusAsync`. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail    
This endpoint requires only one parameter which is **batchId** (String type). It is unique for each batch payment done by the user previously.
 
![36](https://user-images.githubusercontent.com/110983629/192291494-9b5c7df9-53aa-452b-aa1b-5b7d1aebc43a.png)

 
#### Responses 
The response of this endpoint service request contains the `Task<Models.ICGAPIProcessWebAPIModelsTransactionsBatchProcessModel>` object that returns status value for processing payment.

The class name of the Task<Models.ICGAPIProcessWebAPIModelsTransactionsBatchProcessModel> object is
```markdown
   ICGAPIProcessWebAPIModelsTransactionsBatchProcessModel
```

![37](https://user-images.githubusercontent.com/110983629/192292189-4e88a604-47e4-4bb4-b81d-9ec14696d79c.png)

 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
 
#### Response Body-JSON 
```markdown
 {
  "BatchId": null,
  "TotalTransactions": null,
  "TotalSales": null,
  "TotalRefunds": null,
  "ProcessedTransactions": null,
  "ApprovedTransactions": null,
  "DeclinedTransactions": null,
  "StartDatetime": null,
  "EndDatetime": null,
  "ElapsedTime": null,
  "RemainingTime": null,
  "Responses": null,
  "Transactions": null
}
``` 

#### Explorer 

|Name|Description|
|-----|-----------|
|response type|[Task<Models.ICGAPIProcessWebAPIModelsTransactionsBatchProcessModel>](https://developers.icheckdev.com/Process/#/net-standard-library/models/structures/icg-api-process-web-api-models-transactions-batch-process-model)

 
#### Errors
  
Here is the list of errors that the API might throw.
  
|HTTP Status Code|Error Description| Exception Class|
|------|-----|----------|
|400|Bad Request|`ApiException`|
 

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, the 400 code in the 4xx range indicate an error that failed given the information provided (e.g., bad request etc.) 



### Process Process 
#### Description 
This API endpoint will allow the user to process payment request by providing DDA token of the merchant account along with the bank routing number. For successfully processing payment, you need to provide the payment details such as transaction amount, type, Metadata etc. To accomplish that, the API Client will create an instance of the class `TransactionsController` for invoking the method `ProcessProcessAsync`.
  
```markdown 
   ProcessProcessAsync(
    Models.ICGAPIProcessWebAPIModelsTransactionsProcessRequest request)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
var request = new ICGAPIProcessWebAPIModelsTransactionsProcessRequest();
request.Amount = 131.88;
request.Type = TypeEnum.V;

try
{
    ICGTransactionsModelsResponsesProcessResponse result = await transactionsController.ProcessProcessAsync(request);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "transactionsController" object fails to process payment that was anticipated to be returned. The request object of `ICGAPIProcessWebAPIModelsTransactionsProcessRequest` type will be passed as parameter to the method `ProcessProcessAsync`. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail    
This endpoint requires **request** object that further includes Amount (double type), Laneid (string type), CashBackAmount (double type), description (string type), Metadata (string type), DeviceSerialNumber (string type) parameters along with the type, Invoices, customer, method, Imetadata objects. From all of these parameters, Transaction amount, transaction type that can be debit/sales or credit/refund are mandatory to process the payment request.


The class name of **request** object is
```markdown
    ICGAPIProcessWebAPIModelsTransactionsProcessRequest
```

#### request object parameters

![35](https://user-images.githubusercontent.com/110983629/192098751-3cb4b57e-fa53-4254-8d5b-173c7e8baf31.png)


#### Explorer 

|Name|Description|
|-----|-----------|
|request|[Models.ICGAPIProcessWebAPIModelsTransactionsProcessRequest](https://developers.icheckdev.com/Process/#/net-standard-library/models/structures/icg-api-process-web-api-models-transactions-process-request)
 
#### Responses 
The response of this endpoint service request contains the `Task<Models.ICGTransactionsModelsResponsesProcessResponse>` object that returns value for processing payment of a merchant.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
 
#### Response Body-JSON 
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

#### Explorer 

|Name|Description|
|-----|-----------|
|response type|[Task<Models.ICGTransactionsModelsResponsesProcessResponse>](https://developers.icheckdev.com/Process/#/net-standard-library/models/structures/icg-transactions-models-responses-process-response)

 
#### Errors
  
Here is the list of errors that the API might throw.
  
|HTTP Status Code|Error Description| Exception Class|
|------|-----|----------|
|400|Bad Request|`ApiException`|
 

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, the 400 code in the 4xx range indicate an error that failed given the information provided (e.g., bad request etc.) 






### Process Process Dcc  
#### Description 
This API endpoint will allow the user to process Dcc transaction by providing process request id. Through the Dcc transaction, the merchants can make payments through eligible cards to pay in the base currency of the card. For successfully processing Dcc payment, you need to provide the payment details such as transaction amount, type, Metadata etc. To accomplish that, the API Client will create an instance of the class `TransactionsController` for invoking the method `ProcessProcessDccAsync`.
  
```markdown 
    ProcessProcessDccAsync(
    string id,
    bool cancelDcc)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
string id = "id0";
bool cancelDcc = false;

try
{
    ICGTransactionsModelsResponsesProcessResponse result = await transactionsController.ProcessProcessDccAsync(id, cancelDcc);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "transactionsController" object fails to process Dcc payment that was anticipated to be returned. The id and cancelDcc will be passed as parameters to the method `ProcessProcessDccAsync`. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail    
This endpoint requires **id** (string type) and **cancelDcc** (bool type) as a required parameters where the id is the process request id unique for each request and cancelDcc is the bool value that cancelling the Dcc payment processing.

![38](https://user-images.githubusercontent.com/110983629/192302472-74fa55c3-e6fc-4a05-a7df-b74f36f57178.png)

#### Responses 
The response of this endpoint service request contains the `Task<Models.ICGTransactionsModelsResponsesProcessResponse>` object that returns value for processing Dcc payment of a merchant.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
 
#### Response Body-JSON 
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

#### Explorer 

|Name|Description|
|-----|-----------|
|response type|[Task<Models.ICGTransactionsModelsResponsesProcessResponse>](https://developers.icheckdev.com/Process/#/net-standard-library/models/structures/icg-transactions-models-responses-process-response)

 
#### Errors
  
Here is the list of errors that the API might throw.
  
|HTTP Status Code|Error Description| Exception Class|
|------|-----|----------|
|400|Bad Request|`ApiException`|
 

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, the 400 code in the 4xx range indicate an error that failed given the information provided (e.g., bad request etc.) 







###  Process Reversal
#### Description 
This API endpoint will allow the user to reverse the process of making transaction by providing confirmation code and transaction amount. The merchant will receive the confirmation code for reversing the transaction that will expire after sometime. To accomplish that, the API Client will create an instance of the class `TransactionsController` for invoking the method `ProcessReversalAsync`.
  
```markdown 
   ProcessReversalAsync(
    string confirmationCode,
    double amount)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
string confirmationCode = "confirmationCode6";
double amount = 56.78;
try
{
    ICGTransactionsModelsResponsesProcessResponse result = await transactionsController.ProcessReversalAsync(confirmationCode, amount);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "transactionsController" object fails to process a reverse transaction that was anticipated to be returned. The confirmationCode and amount will be passed as parameters to the method `ProcessReversalAsync`. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail    
This endpoint requires **confirmationCode** (string type) and **amount** (double type) as a required parameters where the confirmation code is authenticate the user for reverse payment processing and amount is the transaction amount that need to be reversed.
 
![39](https://user-images.githubusercontent.com/110983629/192309009-ac6f14a7-aaed-4af8-ba2a-fb6d0aaddf51.png)

 
#### Responses 
The response of this endpoint service request contains the `Task<Models.ICGTransactionsModelsResponsesProcessResponse>` object that returns value for processing reverse payment of a merchant.

The class name of Task<Models.ICGTransactionsModelsResponsesProcessResponse> is
```markdown
   ICGTransactionsModelsResponsesProcessResponse
```

#### Task<Models.ICGTransactionsModelsResponsesProcessResponse> object parameters

![40](https://user-images.githubusercontent.com/110983629/192312146-38a5f24e-6340-477c-b62d-4275c09c097a.png)


 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
 
#### Response Body-JSON 
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

#### Explorer 

|Name|Description|
|-----|-----------|
|response type|[Task<Models.ICGTransactionsModelsResponsesProcessResponse>](https://developers.icheckdev.com/Process/#/net-standard-library/models/structures/icg-transactions-models-responses-process-response)

 
#### Errors
  
Here is the list of errors that the API might throw.
  
|HTTP Status Code|Error Description| Exception Class|
|------|-----|----------|
|400|Bad Request|`ApiException`|
 

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, the 400 code in the 4xx range indicate an error that failed given the information provided (e.g., bad request etc.) 






### Process Dcc Refusal
#### Description 
This API endpoint will make the merchant's payment refusal if there may be an issue found such as incorrect personal details (customer details), or any Suspected fraud. The merchant will receive the confirmation code for refusing the transaction that will expire after sometime. To accomplish that, the API Client will create an instance of the class `TransactionsController` for invoking the method `ProcessDccRefusalAsync`.
  
```markdown 
   ProcessDccRefusalAsync(
    string confirmationCode)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
string confirmationCode = "confirmationCode6";
try
{
    ICGTransactionsModelsResponsesProcessResponse result = await transactionsController.ProcessDccRefusalAsync(confirmationCode);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "transactionsController" object fails to refuse Dcc transaction that was anticipated to be returned. The confirmationCode will be passed as parameter to the method `ProcessDccRefusalAsync`. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail    
This endpoint requires **confirmationCode** (string type) as a required parameter where the confirmation code is used to authenticate the user for Refusal Dcc payment processing.
 
![41](https://user-images.githubusercontent.com/110983629/192315948-49acf5e3-4bc7-401f-8231-54e47986c540.png)
  
 
#### Responses 
The response of this endpoint service request contains the `Task<Models.ICGTransactionsModelsResponsesProcessResponse>` object that returns value for processing Refusal payment of a merchant.

The class name of Task<Models.ICGTransactionsModelsResponsesProcessResponse> is
```markdown
    ICGTransactionsModelsResponsesProcessResponse
```

#### Task<Models.ICGTransactionsModelsResponsesProcessResponse> object parameters
 
![42](https://user-images.githubusercontent.com/110983629/192316443-d5f6564e-0cde-4efe-8ed2-969d996c0ece.png)

 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
 
#### Response Body-JSON 
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

#### Explorer 

|Name|Description|
|-----|-----------|
|response type|[Task<Models.ICGTransactionsModelsResponsesProcessResponse>](https://developers.icheckdev.com/Process/#/net-standard-library/models/structures/icg-transactions-models-responses-process-response)

 
#### Errors
  
Here is the list of errors that the API might throw.
  
|HTTP Status Code|Error Description| Exception Class|
|------|-----|----------|
|400|Bad Request|`ApiException`|
 

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, the 400 code in the 4xx range indicate an error that failed given the information provided (e.g., bad request etc.) 






### Process Force
#### Description 
By submitting the approval code and confirmation code, the user can force a transaction using this API endpoint. A forced transaction is a sort of offline transaction that can avoid the authorization tokenization procedure that usually goes along with normal transactions. The API Client will do this by creating an instance of the class "TransactionsController" and calling the function "ProcessForceAsync" on it. 
 
```markdown 
  ProcessForceAsync(
    string confirmationCode,
    string approvalCode)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
string confirmationCode = "confirmationCode6";
string approvalCode = "approvalCode0";

try
{
    ICGTransactionsModelsResponsesForceResponse result = await transactionsController.ProcessForceAsync(confirmationCode, approvalCode);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "transactionsController" object fails to process force transaction that was anticipated to be returned. The confirmationCode and approvalcode will be passed as parameters to the method `ProcessForceAsync` for making force payment. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail     
This endpoint requires **confirmationCode** (string type) and **approvalCode** (string type) as a required parameters where the confirmation code is used to authenticate the user and approval code for making transaction successful.
  
![43](https://user-images.githubusercontent.com/110983629/192319262-9ff077f5-9c4d-43a3-8397-5a71be00ad43.png)


#### Responses 
The response of this endpoint service request contains the `Task<Models.ICGTransactionsModelsResponsesForceResponse>` object that returns value for processing force payment of a merchant.

The class name of Task<Models.ICGTransactionsModelsResponsesForceResponse> is
```markdown
  ICGTransactionsModelsResponsesForceResponse
```

#### Task<Models.ICGTransactionsModelsResponsesForceResponse> object parameters
  
![44](https://user-images.githubusercontent.com/110983629/192319854-b4babfc4-19b2-427f-a704-daad3f0c18d6.png)

 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
 
#### Response Body-JSON 
```markdown
 {
  "RawRequest": null,
  "RawResponse": null,
  "TransactionAmount": null,
  "TransactionDate": null,
  "Status": null,
  "StatusMessage": null,
  "ErrorData": null
}
``` 

#### Explorer 

|Name|Description|
|-----|-----------|
|response type|[Task<Models.ICGTransactionsModelsResponsesForceResponse>](https://developers.icheckdev.com/Process/#/net-standard-library/models/structures/icg-transactions-models-responses-force-response)

 
#### Errors
  
Here is the list of errors that the API might throw.
  
|HTTP Status Code|Error Description| Exception Class|
|------|-----|----------|
|400|Bad Request|`ApiException`|
 

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, the 400 code in the 4xx range indicate an error that failed given the information provided (e.g., bad request etc.) 






### Process Re Auth
#### Description 
This endpoint will allow the user to reauth the transaction of the merchant through the confirmation code and transaction amount. The reauth is a process where a new authorization can be performed using the same credit/debit card as a previous transaction. The API Client will do this by creating an instance of the class "TransactionsController" and calling the function "ProcessReAuthAsync" on it. 
 
```markdown 
 ProcessReAuthAsync(
    string confirmationCode,
    double amount)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
string confirmationCode = "confirmationCode6";
double amount = 56.78;
try
{
    ICGTransactionsModelsResponsesProcessResponse result = await transactionsController.ProcessReAuthAsync(confirmationCode, amount);
}
catch (ApiException e){};
``` 
It will be included in the try and catch block to deal with any exceptions that could arise if the "transactionsController" object fails to reauth the transaction that was anticipated to be returned. The confirmationCode and transaction amount will be passed as parameters to the method `ProcessReAuthAsync` for making payment using the transaction model which is used for previously one. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail     
This endpoint requires **confirmationCode** (string type) and **amount** (double type) as a required parameters where the confirmation code is used to authenticate the user and transaction amount that needs to be submitted.
  
![45](https://user-images.githubusercontent.com/110983629/192324516-8ce0d9ca-ae7b-4133-bc3b-bb3b05007d51.png)


#### Responses 
The response of this endpoint service request contains the `Task<Models.ICGTransactionsModelsResponsesProcessResponse>` object that returns value for processing reauth payment of a merchant.

The class name of Task<Models.ICGTransactionsModelsResponsesProcessResponse> is
```markdown
   ICGTransactionsModelsResponsesProcessResponse
```

#### Task<Models.ICGTransactionsModelsResponsesProcessResponse> object parameters
   
![46](https://user-images.githubusercontent.com/110983629/192325123-72343d30-ee02-42dd-b8fc-62cdf8c15ad2.png)

 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
 
#### Response Body-JSON 
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

#### Explorer 

|Name|Description|
|-----|-----------|
|response type|[Task<Models.ICGTransactionsModelsResponsesProcessResponse>](https://developers.icheckdev.com/Process/#/net-standard-library/models/structures/icg-transactions-models-responses-process-response)

 
#### Errors
  
Here is the list of errors that the API might throw.
  
|HTTP Status Code|Error Description| Exception Class|
|------|-----|----------|
|400|Bad Request|`ApiException`|
 

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, the 400 code in the 4xx range indicate an error that failed given the information provided (e.g., bad request etc.) 




### Process Capture
#### Description 
This endpoint will allow the user to capture the transaction of the merchant by entering the confirmation code, transaction amount, and tip. The API Client will do this by creating an instance of the class "TransactionsController" and calling the function "ProcessCaptureAsync" on it. 
 
```markdown 
 ProcessCaptureAsync(
    string confirmationCode,
    double amount,
    double tip)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
string confirmationCode = "confirmationCode6";
double amount = 56.78;
double tip = 171.08;

try
{
    ICGTransactionsModelsResponsesCaptureResponse result = await transactionsController.ProcessCaptureAsync(confirmationCode, amount, tip);
}
catch (ApiException e){};
``` 
It will be included in the try and catch block to deal with any exceptions that could arise if the "transactionsController" object fails to capture the transaction that was anticipated to be returned. The confirmationCode, amount and tip will be passed as parameters to the method `ProcessCaptureAsync` for making payment. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail     
This endpoint requires **confirmationCode** (string type), **amount** (double type) and **tip** (double type) as a required parameters where the confirmation code is used to authenticate the user and transaction amount that needs to be submitted and tip is the amount that you wished to submit with the actual payment amount.
  
![47](https://user-images.githubusercontent.com/110983629/192514123-54fd3953-8bfd-4cd0-9ab8-39485094cbc5.png)


#### Responses 
The response of this endpoint service request contains the `Task<Models.ICGTransactionsModelsResponsesCaptureResponse>` object that returns value for capturing payment of a merchant.

The class name of Task<Models.ICGTransactionsModelsResponsesCaptureResponse> is
```markdown
    ICGTransactionsModelsResponsesCaptureResponse
```

####  Task<Models.ICGTransactionsModelsResponsesCaptureResponse> object parameters
    
![48](https://user-images.githubusercontent.com/110983629/192514662-298744f4-f786-4081-8581-ce3f9d27c56d.png)

 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
 
#### Response Body-JSON 
```markdown
  {
  "RawRequest": null,
  "RawResponse": null,
  "TransactionAmount": null,
  "TransactionDate": null,
  "Status": null,
  "StatusMessage": null,
  "ErrorData": null,
  "ApprovalCode": null,
  "ReferenceNumber": null,
  "ConfirmationCode": null
}
``` 

#### Explorer 

|Name|Description|
|-----|-----------|
|response type|[Task<Models.ICGTransactionsModelsResponsesCaptureResponse>](https://developers.icheckdev.com/Process/#/net-standard-library/models/structures/icg-transactions-models-responses-capture-response)

 
#### Errors
  
Here is the list of errors that the API might throw.
  
|HTTP Status Code|Error Description| Exception Class|
|------|-----|----------|
|400|Bad Request|`ApiException`|
 

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, the 400 code in the 4xx range indicate an error that failed given the information provided (e.g., bad request etc.) 








### Process Void
#### Description 
This endpoint will give the user the ability to cancel a merchant transaction before it is processed through the merchant's debit or credit card account. When a transaction is cancelled, it briefly appears on the merchant's account as a pending transaction while the procedure is being finished.
The API Client will do this by creating an instance of the class "TransactionsController" and calling the function "ProcessVoidAsync" on it. 
 
```markdown 
 ProcessVoidAsync(
    string confirmationCode,
    double amount)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
string confirmationCode = "confirmationCode6";
double amount = 56.78;
try
{
    ICGTransactionsModelsResponsesVoidResponse result = await transactionsController.ProcessVoidAsync(confirmationCode, amount);
}
catch (ApiException e){};
```  
It will be included in the try and catch block to deal with any exceptions that could arise if the "transactionsController" object fails to void a transaction that was anticipated to be returned. The confirmationCode, and amount will be passed as parameters to the method `ProcessVoidAsync` for making transaction nullified. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail     
This endpoint requires **confirmationCode** (string type), and **amount** (double type) as a required parameters where the confirmation code is used to authenticate the user and amount is the transaction amount that needs to be submitted.
   
![49](https://user-images.githubusercontent.com/110983629/192519717-f8166173-2efe-4d54-8f5c-23571fc41f64.png)
   

#### Responses 
The response of this endpoint service request contains the `Task<Models.ICGTransactionsModelsResponsesVoidResponse>` object that returns value for making payment void of a merchant.

The class name of Task<Models.ICGTransactionsModelsResponsesVoidResponse> is
```markdown
     ICGTransactionsModelsResponsesVoidResponse
```

#### Task<Models.ICGTransactionsModelsResponsesVoidResponse> object parameters

![50](https://user-images.githubusercontent.com/110983629/192520028-ccc4556d-5e1c-4037-b7fc-11bb182047b3.png)

     
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
 
#### Response Body-JSON 
```markdown
 {
  "RawRequest": null,
  "RawResponse": null,
  "TransactionAmount": null,
  "TransactionDate": null,
  "Status": null,
  "StatusMessage": null,
  "ErrorData": null
}
``` 

#### Explorer 

|Name|Description|
|-----|-----------|
|response type|[Task<Models.ICGTransactionsModelsResponsesVoidResponse>](https://developers.icheckdev.com/Process/#/net-standard-library/models/structures/icg-transactions-models-responses-void-response)

 
#### Errors
  
Here is the list of errors that the API might throw.
  
|HTTP Status Code|Error Description| Exception Class|
|------|-----|----------|
|400|Bad Request|`ApiException`|
 

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, the 400 code in the 4xx range indicate an error that failed given the information provided (e.g., bad request etc.) 




### Process Refund
#### Description 
By providing the transaction's confirmation code and the amount, the user will be able to cancel a merchant transaction using this service. The merchant's bank account receives the money back. It is typical for the merchant to face a slight delay as the bank may need a few days to deposit the refunded payments. 
 
The API Client will do this by creating an instance of the class "TransactionsController" and calling the function "ProcessRefundAsync" on it. 
 
```markdown 
 ProcessRefundAsync(
    string confirmationCode,
    double amount)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
string confirmationCode = "confirmationCode6";
double amount = 56.78;

try
{
    ICGTransactionsModelsResponsesRefundResponse result = await transactionsController.ProcessRefundAsync(confirmationCode, amount);
}
catch (ApiException e){};
```  
It will be included in the try and catch block to deal with any exceptions that could arise if the "transactionsController" object fails to refund a transaction that was anticipated to be returned. The confirmationCode, and amount will be passed as parameters to the method `ProcessRefundAsync` for making transaction refunded. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail     
This endpoint requires **confirmationCode** (string type), and **amount** (double type) as a required parameters where the confirmation code is used to authenticate the user for a unique transaction and amount is the transaction amount that needs to be submitted. 

![51](https://user-images.githubusercontent.com/110983629/192525254-1a937d53-bfdc-4c52-8870-f8b8c70e4dc2.png)


#### Responses 
The response of this endpoint service request contains the `Task<Models.ICGTransactionsModelsResponsesRefundResponse>` object that returns value for refunding payment of a merchant.

The class name of Task<Models.ICGTransactionsModelsResponsesRefundResponse> is
```markdown
    ICGTransactionsModelsResponsesRefundResponse  
```

#### Task<Models.ICGTransactionsModelsResponsesRefundResponse> object parameters
 
![52](https://user-images.githubusercontent.com/110983629/192525528-d1bc0bfb-2f38-4ae9-8432-3423b59325a2.png)

 
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
 
#### Response Body-JSON 
```markdown
 {
  "RawRequest": null,
  "RawResponse": null,
  "TransactionAmount": null,
  "TransactionDate": null,
  "Status": null,
  "StatusMessage": null,
  "ConfirmationCode": null,
  "ApprovalCode": null,
  "CvcResponse": null,
  "AvsResponse": null,
  "ReferenceNumber": null,
  "ErrorData": null
}
``` 

#### Explorer 

|Name|Description|
|-----|-----------|
|response type|[Task<Models.ICGTransactionsModelsResponsesRefundResponse>](https://developers.icheckdev.com/Process/#/net-standard-library/models/structures/icg-transactions-models-responses-refund-response)

 
#### Errors
  
Here is the list of errors that the API might throw.
  
|HTTP Status Code|Error Description| Exception Class|
|------|-----|----------|
|400|Bad Request|`ApiException`|
 

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, the 400 code in the 4xx range indicate an error that failed given the information provided (e.g., bad request etc.) 



### Transaction Scheduled Process Scheduled
#### Description  
The user can schedule upcoming one-time, recurring, and instalment transactions using this API endpoint. Future payments that are scheduled to occur just once are known as one-time payments. The transactions that are planned for a specified, repeating time interval in the future are known as recurring transactions. You must submit payment information, including the transaction amount, type, metadata, etc., in order for the payment to be processed successfully. This will be done by the API Client calling the method "TransactionScheduledProcessScheduledAsync" by creating an instance of the class "TransactionsController".
  
```markdown 
    TransactionScheduledProcessScheduledAsync(
    Models.ICGTransactionsModelsRequestsProcessScheduleRequest request)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
var request = new ICGTransactionsModelsRequestsProcessScheduleRequest();
request.Amount = 131.88;
request.Type = Type3Enum.V;
try
{
    string result = await transactionsController.TransactionScheduledProcessScheduledAsync(request);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "transactionsController" object fails to schedule payment that was anticipated to be returned. The request object of `ICGTransactionsModelsRequestsProcessScheduleRequest` type will be passed as parameter to the method `TransactionScheduledProcessScheduledAsync`. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail    
This endpoint requires **request** object that further includes TransactionScheduledId (int type), Amount (double type), Laneid (string type), CashBackAmount (double type), description (string type), Metadata (string type), DeviceSerialNumber (string type) parameters along with the type, Invoices, customer, method, Imetadata objects. From all of these parameters, Transaction amount, transaction type that can be debit/sales or credit/refund are mandatory to process the payment request.


The class name of **request** object is
```markdown
   ICGTransactionsModelsRequestsProcessScheduleRequest
```

#### request object parameters

![53](https://user-images.githubusercontent.com/110983629/192531176-963dbc89-4208-4b5e-be9f-d802d2dc317e.png)

 
#### Explorer 

|Name|Description|
|-----|-----------|
|request|[Models.ICGTransactionsModelsRequestsProcessScheduleRequest](https://developers.icheckdev.com/Process/#/net-standard-library/models/structures/icg-transactions-models-requests-process-schedule-request)
 
#### Responses 
The response of this endpoint service request contains the `Task<string>` object that returns value for scheduling payment of a merchant.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
 
  
#### Errors
  
Here is the list of errors that the API might throw.
  
|HTTP Status Code|Error Description| Exception Class|
|------|-----|----------|
|400|Bad Request|`ApiException`|
 

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, the 400 code in the 4xx range indicate an error that failed given the information provided (e.g., bad request etc.) 



### Transaction Scheduled Update Transaction Scheduled Status
#### Description  
The user can update the schedule transaction status that can be an upcoming one-time, recurring, and instalment transactions using this API endpoint. Future payments that are scheduled to occur just once are known as one-time payments. The transactions that are planned for a specified, repeating time interval in the future are known as recurring transactions. This will be done by the API Client calling the method "TransactionScheduledUpdateTransactionScheduledStatusAsync" by creating an instance of the class "TransactionsController".
  
```markdown 
    TransactionScheduledUpdateTransactionScheduledStatusAsync(
    int transactionScheduledId,
    int status)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
int transactionScheduledId = 4;
int status = 204;

try
{
    int? result = await transactionsController.TransactionScheduledUpdateTransactionScheduledStatusAsync(transactionScheduledId, status);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "transactionsController" object fails to update the status of scheduled payment that was anticipated to be returned. The transactionScheduledId, status will be passed as parameters to the method `TransactionScheduledUpdateTransactionScheduledStatusAsync`. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail     
This endpoint requires **transactionScheduledId** (int type), and **status** (int type). The transactionScheduledId will be unique identifier for each transaction which is scheduled. The status can be Scheduled, Processing, Processed, Declined, Cancelled, and Error for a payment transaction. You can change the status value for by accessing it through transactionScheduledId through this endpoint.

![54](https://user-images.githubusercontent.com/110983629/192538725-54964af9-6234-4894-9982-ce80bfff6385.png)

 
#### Responses 
The response of this endpoint service request contains the `Task<int>` object that returns value for changing transaction status of a merchant.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
 
  
#### Errors
  
Here is the list of errors that the API might throw.
  
|HTTP Status Code|Error Description| Exception Class|
|------|-----|----------|
|400|Bad Request|`ApiException`|
|404|Not Found|`ApiException`|
 

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, the 400 code in the 4xx range indicate an error that failed given the information provided (e.g., bad request, not found etc.) 






### Transaction Scheduled Update Process Scheduled
#### Description  
The user can update the schedule transaction details that can be an upcoming one-time, recurring, and instalment transactions using this API endpoint. Future payments that are scheduled to occur just once are known as one-time payments. The transactions that are planned for a specified, repeating time interval in the future are known as recurring transactions. This will be done by the API Client calling the method "TransactionScheduledUpdateProcessScheduledAsync" by creating an instance of the class "TransactionsController".
  
```markdown 
    TransactionScheduledUpdateProcessScheduledAsync(
    Models.ICGTransactionsModelsRequestsProcessScheduleRequest request)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
var request = new ICGTransactionsModelsRequestsProcessScheduleRequest();
request.Amount = 131.88;
request.Type = Type3Enum.V;
try
{
    string result = await transactionsController.TransactionScheduledUpdateProcessScheduledAsync(request);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "transactionsController" object fails to update the payment that was anticipated to be returned. The request object which will be of `ICGTransactionsModelsRequestsProcessScheduleRequest` type will be passed as parameter to the method `TransactionScheduledUpdateProcessScheduledAsync`. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail     
This endpoint requires **request** object that will process the scheduled request of making payment.This **request** object will further contains the TransactionScheduledId (int type), Amount (double type), Laneid (string type), CashBackAmount (double type), description (string type), Metadata (string type), DeviceSerialNumber (string type) along with the type, Invoices, customer, method, Imetadata objects. From all of these parameters, Transaction amount, transaction type that can be debit/sales or credit/refund are mandatory to process the payment request for updating.


The class name of **request** object is
```markdown
   ICGTransactionsModelsRequestsProcessScheduleRequest
```

#### request object parameters

![53](https://user-images.githubusercontent.com/110983629/192531176-963dbc89-4208-4b5e-be9f-d802d2dc317e.png)

 
#### Explorer 

|Name|Description|
|-----|-----------|
|request|[Models.ICGTransactionsModelsRequestsProcessScheduleRequest](https://developers.icheckdev.com/Process/#/net-standard-library/models/structures/icg-transactions-models-requests-process-schedule-request)
  
 
#### Responses 
The response of this endpoint service request contains the `Task<string>` object that returns value for updating scheduled transaction details of a merchant.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
 
  
#### Errors
  
Here is the list of errors that the API might throw.
  
|HTTP Status Code|Error Description| Exception Class|
|------|-----|----------|
|400|Bad Request|`ApiException`|
 

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, the 400 code in the 4xx range indicate an error that failed given the information provided (e.g., bad request etc.) 




### Transaction Scheduled Get Transaction Scheduled
#### Description  
This endpoint service request will provide the facility to the user to retrieve all scheduled transactions by method type that is defined for the each scheduled payment. The payment method can be card or a check for preforming the transaction. This will be done by the API Client calling the method "TransactionScheduledGetTransactionScheduledAsync" by creating an instance of the class "TransactionsController".
  
```markdown 
    TransactionScheduledGetTransactionScheduledAsync(
    string methodType)TransactionScheduledGetTransactionScheduledAsync(
    string methodType)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
string methodType = "methodType0";
try
{
    List<ICGBusinessEntitiesTransactionsScheduled> result = await transactionsController.TransactionScheduledGetTransactionScheduledAsync(methodType);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "transactionsController" object fails to retrieve all the scheduled payment that was anticipated to be returned. The methodType will be passed as parameter to the method `TransactionScheduledGetTransactionScheduledAsync`. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail     
This endpoint requires **methodType** (string type) which can be a card or check for retrieving all the payments scheduled for sending in future.  

![55](https://user-images.githubusercontent.com/110983629/192558029-f8680bca-24d3-43a7-b1e0-61153c7b1790.png)


#### Responses  
The response of this endpoint service request contains the `Task<List<Models.ICGBusinessEntitiesTransactionsScheduled>>` object that returns value for retrieving all transactions scheduled previously.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
 
#### Response Body-JSON  
```markdown
{
  "Id": null,
  "MerchantId": null,
  "ProcessorId": null,
  "CustomerId": null,
  "BillingTypeId": null,
  "BillingType": null,
  "StartDate": null,
  "LastBilled": null,
  "NextBill": null,
  "ScheduleTypeId": null,
  "NumberofPayments": null,
  "RemainingPayments": null,
  "StatusId": null,
  "Status": null,
  "InvoiceNumber": null,
  "FromIp": null,
  "Description": null,
  "TransactionType": null,
  "Amount": null,
  "Authorization": null,
  "Creation": null,
  "Modification": null,
  "TransactionsScheduledCard": null,
  "TransactionsScheduledCheck": null,
  "TransactionsScheduledCustomer": null,
  "TransactionsScheduledCustomerAddress": null
}
```
  
 The class name of Task<List<Models.ICGBusinessEntitiesTransactionsScheduled>> object is
 ```markdown
    ICGBusinessEntitiesTransactionsScheduled
 ```
 
#### Explorer 

|Name|Description|
|-----|-----------|
|Respose type|[Task<List<Models.ICGBusinessEntitiesTransactionsScheduled>>](https://developers.icheckdev.com/Process/#/net-standard-library/models/structures/icg-business-entities-transactions-scheduled)


#### Errors
  
Here is the list of errors that the API might throw.
  
|HTTP Status Code|Error Description| Exception Class|
|------|-----|----------|
|400|Bad Request|`ApiException`|
|404|Not Found|`ApiException`|
 

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, the 400 code in the 4xx range indicate an error that failed given the information provided (e.g., bad request, not found etc.) 







### Transaction Scheduled Get Transaction Scheduled by Id
#### Description  
This endpoint service request will provide the facility to the user to retrieve the scheduled transaction by entering the id which is unique identifier for each scheduled transaction. This will be done by the API Client calling the method "TransactionScheduledGetTransactionScheduledByIdAsync" by creating an instance of the class "TransactionsController".
  
```markdown 
    TransactionScheduledGetTransactionScheduledByIdAsync(int id)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
int id = 112;
try
{
    ICGBusinessEntitiesTransactionsScheduled result = await transactionsController.TransactionScheduledGetTransactionScheduledByIdAsync(id);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "transactionsController" object fails to retrieve the scheduled payment that was anticipated to be returned. The id will be passed as parameter to the method `TransactionScheduledGetTransactionScheduledAsync` in order to access one unique scheduled payment. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes. 
 

#### Parameters Detail      
This endpoint requires **id** (int type) which is a unique scheduled transaction identifier for retrieving the payment details.
 
![56](https://user-images.githubusercontent.com/110983629/192564213-30c0bc88-c578-4276-bc39-1f719f0d19fe.png)


#### Responses  
The response of this endpoint service request contains the `Task<Models.ICGBusinessEntitiesTransactionsScheduled>` object that returns details of the transaction which is scheduled.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
 
#### Response Body-JSON  
```markdown
 {
  "Id": null,
  "MerchantId": null,
  "ProcessorId": null,
  "CustomerId": null,
  "BillingTypeId": null,
  "BillingType": null,
  "StartDate": null,
  "LastBilled": null,
  "NextBill": null,
  "ScheduleTypeId": null,
  "NumberofPayments": null,
  "RemainingPayments": null,
  "StatusId": null,
  "Status": null,
  "InvoiceNumber": null,
  "FromIp": null,
  "Description": null,
  "TransactionType": null,
  "Amount": null,
  "Authorization": null,
  "Creation": null,
  "Modification": null,
  "TransactionsScheduledCard": null,
  "TransactionsScheduledCheck": null,
  "TransactionsScheduledCustomer": null,
  "TransactionsScheduledCustomerAddress": null
}
```
  
 The class name of Task<Models.ICGBusinessEntitiesTransactionsScheduled> object is
 ```markdown
     ICGBusinessEntitiesTransactionsScheduled
 ```
 
#### Explorer 

|Name|Description|
|-----|-----------|
|Respose type|[Task<Models.ICGBusinessEntitiesTransactionsScheduled>](https://developers.icheckdev.com/Process/#/net-standard-library/models/structures/icg-business-entities-transactions-scheduled)


#### Errors
  
Here is the list of errors that the API might throw.
  
|HTTP Status Code|Error Description| Exception Class|
|------|-----|----------|
|400|Bad Request|`ApiException`|
|404|Not Found|`ApiException`|
 

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, the 400 code in the 4xx range indicate an error that failed given the information provided (e.g., bad request, not found etc.) 








### Transaction Scheduled Delete Scheduled Card Transaction
#### Description   
This endpoint service request will provide the facility to the user to delete a scheduled transaction by entering the id which is unique identifier for each scheduled transaction. You can delete a card transaction which has been scheduled before. This will be done by the API Client calling the method "TransactionScheduledDeleteScheduledCardTransactionAsync" by creating an instance of the class "TransactionsController".
  
```markdown 
     TransactionScheduledDeleteScheduledCardTransactionAsync(
    int id)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
int id = 112;
try
{
    string result = await transactionsController.TransactionScheduledDeleteScheduledCardTransactionAsync(id);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "transactionsController" object fails to delete the scheduled card transaction that was anticipated to be returned. The id will be passed as parameter to the method `TransactionScheduledDeleteScheduledCardTransactionAsync` in order to access one unique scheduled payment. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes. 
 

#### Parameters Detail      
This endpoint requires **id** (int type) which is a unique scheduled transaction identifier for removing the scheduled payment details.
 
![56](https://user-images.githubusercontent.com/110983629/192564213-30c0bc88-c578-4276-bc39-1f719f0d19fe.png)


#### Responses  
The response of this endpoint service request contains the  `Task<string>` object that returns the value for successfully deleting the scheduled card transaction.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
 
  
#### Errors
  
Here is the list of errors that the API might throw.
  
|HTTP Status Code|Error Description| Exception Class|
|------|-----|----------|
|400|Bad Request|`ApiException`|
 

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, the 400 code in the 4xx range indicate an error that failed given the information provided (e.g., bad request etc.) 






### Transaction Scheduled Delete Scheduled Check Transaction
#### Description   
This endpoint service request will provide the facility to the user to delete a scheduled transaction by entering the id which is unique identifier for each scheduled transaction. You can delete a check transaction which has been scheduled before by the user. This will be done by the API Client calling the method "TransactionScheduledDeleteScheduledCheckTransactionAsync" by creating an instance of the class "TransactionsController".
  
```markdown 
    TransactionScheduledDeleteScheduledCheckTransactionAsync(
    int id)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
int id = 112;
try
{
    string result = await transactionsController.TransactionScheduledDeleteScheduledCheckTransactionAsync(id);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "transactionsController" object fails to delete the scheduled check transaction that was anticipated to be returned. The id will be passed as parameter to the method `TransactionScheduledDeleteScheduledCheckTransactionAsync` in order to access one unique scheduled payment. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes. 
 

#### Parameters Detail      
This endpoint requires **id** (int type) which is a unique scheduled transaction identifier for removing the scheduled check payment details.
  
![57](https://user-images.githubusercontent.com/110983629/192804565-6f9edb08-d2f5-4e4f-a5d7-89bfbcc95f26.png)



#### Responses  
The response of this endpoint service request contains the  `Task<string>` object that returns the value for successfully deleting the scheduled check transaction.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
 
  
#### Errors
  
Here is the list of errors that the API might throw.
  
|HTTP Status Code|Error Description| Exception Class|
|------|-----|----------|
|400|Bad Request|`ApiException`|
 

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, the 400 code in the 4xx range indicate an error that failed given the information provided (e.g., bad request etc.) 




### Transaction Scheduled Get Expiring Scheduled Transactions
#### Description  
This endpoint service request will provide the facility to the user to retrieve all expired scheduled transactions by merchant's site identifier. The merchant's site identifier will be distinct that is used to get merchant's expired transactions. This will be done by the API Client calling the method "TransactionScheduledGetExpiringScheduledTransactionsAsync" by creating an instance of the class "TransactionsController".
  
```markdown 
   TransactionScheduledGetExpiringScheduledTransactionsAsync(
    string siteId,
    DateTime start,
    DateTime end)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/Process/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
string siteId = "siteId8";
DateTime start = DateTime.Parse("2016-03-13T12:52:32.123Z");
DateTime end = DateTime.Parse("2016-03-13T12:52:32.123Z");

try
{
    List<ICGBusinessEntitiesExpiringTransactionsScheduled> result = await transactionsController.TransactionScheduledGetExpiringScheduledTransactionsAsync(siteId, start, end);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "transactionsController" object fails to retrieve all the expired scheduled payments that was anticipated to be returned. The start and end date will be passed as parameters to the method `TransactionScheduledGetExpiringScheduledTransactionsAsync`. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail      

This endpoint requires **siteId** (string type), **start** (DateTime type), and **end** (DateTime type) parameters. The siteId is the merchant's site identifier for retrieving all the expired scheduled transactions of the merchant. 

![58](https://user-images.githubusercontent.com/110983629/193024457-ee05586f-83ba-4cbc-8b45-7cd876a24c3c.png)



#### Responses  
The response of this endpoint service request contains the `Task<List<Models.ICGBusinessEntitiesExpiringTransactionsScheduled>>` object that returns detail of all expired transactions scheduled previously of the merchant.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
 
#### Response Body-JSON  
```markdown
 {
  "CustomerId": null,
  "CompanyName": null,
  "TransactionsScheduledId": null,
  "Token": null,
  "Number": null,
  "Name": null,
  "ExpDate": null,
  "Display": null,
  "Address": null,
  "ZipCode": null,
  "EntryMode": null,
  "PaymentType": null,
  "CardInfo": null
}
```
  
 The class name of Task<List<Models.ICGBusinessEntitiesExpiringTransactionsScheduled>> object is
 ```markdown
     ICGBusinessEntitiesExpiringTransactionsScheduled
 ```
 
#### Explorer 

|Name|Description|
|-----|-----------|
|Respose type|[Task<List<Models.ICGBusinessEntitiesExpiringTransactionsScheduled>>](https://developers.icheckdev.com/Process/#/net-standard-library/models/structures/icg-business-entities-expiring-transactions-scheduled)


#### Errors
  
Here is the list of errors that the API might throw.
  
|HTTP Status Code|Error Description| Exception Class|
|------|-----|----------|
|400|Bad Request|`ApiException`|
|404|Not Found|`ApiException`|
 

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, the 400 code in the 4xx range indicate an error that failed given the information provided (e.g., bad request, not found etc.) 


























