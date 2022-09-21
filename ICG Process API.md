
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

|Names|Description|
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

|Names|Description|
|-----|-----------|
|Response type|[Task<Models.ICGTransactionsModelsResponsesProcessResponse>](https://developers.icheckdev.com/Process/#/net-standard-library/models/structures/icg-transactions-models-responses-process-response)
 




























