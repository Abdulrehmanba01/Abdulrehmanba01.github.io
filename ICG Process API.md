
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
 
























