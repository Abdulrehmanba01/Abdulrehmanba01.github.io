# For .NET
  
## Getting Started
  
### Description

The ICG underwriting API will give merchants the ability to submit their applications for managing and tracking their progress. They are able to carry out a variety of tasks with this API, including keeping track of prospect documents, Dropbox files, PDFs, integrations, logs, messages, scroes, tax, and balance plaid transactions. By sending API calls using this API, users may quickly access and control their merchant application.

#### API Client Configuration Parameters: 
  
|Parameter       | Type      |Description|
|----------------|-----------|-------------------------------------------------------|
|`Timeout`         |`TimeSpan`   |Http client timeout. Default: `TimeSpan.FromSeconds(100)`|   
|`authorization`   | `String`    |API Access token provided by the Auth API after User authentication|
  
  
The API client configuration looks like this:
```markdown 
 ICGAPIUnderwriting.Standard.ICGAPIUnderwritingClient client = new ICGAPIUnderwriting.Standard.ICGAPIUnderwritingClient.Builder().Build();
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
## Prospect Document 
### Prospect Document Post
#### Description

This API call will be made in order to send the document for electronic signature. It just needs one parameter, which is the prospect document id. To do this, the API Client will create an instance of the class `ProspectDocumentController` and use the method `ProspectDocumentPostAsync`.


```markdown
ProspectDocumentController prospectDocumentController = client.ProspectDocumentController;
```

```markdown
 ProspectDocumentPostAsync(int prospectId)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
int prospectId = 118;
try
{
    object result = await prospectDocumentController.ProspectDocumentPostAsync(prospectId);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectDocumentController" object fails to send document for sign that was anticipated to be returned. The prospect id will be passed as a parameter to the `ProspectDocumentPostAsync` method. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail   
This API call uses an int-type prospect id as the only mandatory parameter. The prospoct document id is a unique for each prospect document. This ID will be used to access a specific document in order to send it for signing.


![1](https://user-images.githubusercontent.com/110983629/189973237-2a1f4ea2-b964-41b6-898b-de3aa8f4182a.png)


#### Responses 

For viewing the response body, you need to download the text file. 

#### Response body-Text File
```markdown 
{
  "Message": "Authorization has been denied for this request."
}
```

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|*/*; charset=utf-8|

    
 ##### 'ResponseType' Object Parameters 
 The Response of this API request returns `Task<object>` that indicate the document is sent for sign or not.
  
  







### Prospect Document Check Status
#### Description

This API call will be made in order to verify that the document is signed. It just needs one parameter, which is the prospect document id. To do this, the API Client will create an instance of the class `ProspectDocumentController` for invoking the `ProspectDocumentCheckStatusAsync` method.
 

```markdown
 ProspectDocumentCheckStatusAsync(int prospectId)
```
This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
int prospectId = 118;
try
{
    object result = await prospectDocumentController.ProspectDocumentCheckStatusAsync(prospectId);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectDocumentController" object fails to verify the document is signed that was anticipated to be returned. The prospect id will be passed as a parameter to the `ProspectDocumentPostAsync` method. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail   
This API call uses an int-type prospect id as the only mandatory parameter. The prospoct document id is a unique for each prospect document. This ID will be used to access a specific document in order to verified the signed document.

 
![2](https://user-images.githubusercontent.com/110983629/189976765-40ae42f2-eb71-4be7-9a23-02dd5c802891.png)


#### Responses 

For viewing the response body, you need to download the text file. 

#### Response body-Text File
```markdown 
{
  "Message": "Authorization has been denied for this request."
}
```

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|*/*; charset=utf-8|

    
 ##### 'ResponseType' Object Parameters 
 The Response of this API request returns `Task<object>` that indicate the signed document is verified or not.
  
  


### Prospect Document Send Reminder
#### Description

This API call will be made in order to send reminder to the user who has to signed the document. It just needs one parameter, which is the prospect document id. To do this, the API Client will create an instance of the class `ProspectDocumentController` for invoking the `ProspectDocumentSendReminderAsync` method.
 

```markdown
 ProspectDocumentSendReminderAsync(
    int prospectId)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
int prospectId = 118;

try
{
    object result = await prospectDocumentController.ProspectDocumentSendReminderAsync(prospectId);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectDocumentController" object fails to send reminder that was anticipated to be returned. The prospect id will be passed as a parameter to the `ProspectDocumentSendReminderAsync` method. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail   
This API call uses an int-type prospect id as the only mandatory parameter. The prospoct document id is a unique for each prospect document. This ID will be used to access a specific document in order to verified the signed document.

 ![3](https://user-images.githubusercontent.com/110983629/189979572-df8b4620-4fb7-4852-9063-1061d7c59c5d.png)


#### Responses 

For viewing the response body, you need to download the text file. 

#### Response body-Text File
```markdown 
{
  "Message": "Authorization has been denied for this request."
}
```

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|*/*; charset=utf-8|

    
 ##### 'ResponseType' Object Parameters 
 The Response of this API request returns `Task<object>` that indicate the reminder is sent or not.
  







### Prospect Document Get Generate PDF
#### Description

This endpoint service request will allow you to get the document PDF which is generated by the ICG. This process call just need one parameter, which is the prospect document id. To do this, the API Client will create an instance of the class `ProspectDocumentController` for invoking the `ProspectDocumentGetGeneratePDFAsync` method.
 

```markdown
  ProspectDocumentGetGeneratePDFAsync(int prospectId)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started)

#### Class-Object
```markdown
int prospectId = 118;
try
{
    object result = await prospectDocumentController.ProspectDocumentGetGeneratePDFAsync(prospectId);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectDocumentController" object fails to retrieve the document PDF that was anticipated to be returned. The prospect id will be passed as a parameter to the `ProspectDocumentGetGeneratePDFAsync` method. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail   
This API call uses an int-type prospect id as the only mandatory parameter. The prospoct document id is a unique for each prospect document. This ID will be used to access a specific document in order to verified the signed document.

 ![3](https://user-images.githubusercontent.com/110983629/189979572-df8b4620-4fb7-4852-9063-1061d7c59c5d.png)


#### Responses 

For viewing the response body, you need to download the text file. 

#### Response body-Text File
```markdown 
{
  "Message": "Authorization has been denied for this request."
}
```

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|*/*; charset=utf-8|

    
 ##### 'ResponseType' Object Parameters 
 The Response of this API request returns `Task<object>` that indicate the document PDF generated get retrieved or not.
  






## API Endpoints
## Prospect Dropbox Files
### Prospect Dropbox Files Get Prospect Dropbox Files
#### Description
With the use of this service endpoint, merchants can retrieve prospect Dropbox files. These files will provide a description of each file for the current prospect, including filename, fileId, size, etc.
The 'ProspectDropboxFilesGetProspectDropboxFilesAsync' method of the 'ProspectDropboxFilesController' class will be called by the API client for this process in order to retrieve the files description.


```markdown
 ProspectDropboxFilesGetProspectDropboxFilesAsync(
    int prospectId)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int prospectId = 118;
try
{
    ICGBusinessEntitiesProspectDropboxFile result = await prospectDropboxFilesController.ProspectDropboxFilesGetProspectDropboxFilesAsync(prospectId);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectDropboxFilesController" object fails to retrieve the current prospect files description that was anticipated to be returned. The prospect id will be passed as a parameter to the `ProspectDropboxFilesGetProspectDropboxFilesAsync`. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.


#### Parameters Detail   
The parameters of this endpoint service includes **prospectId** (int Type) which is unique identifier for each prospect. It is required for the user enter the prospect id for retrieving the description of all files
  
![4](https://user-images.githubusercontent.com/110983629/189987344-6b51409b-133e-4929-9e75-cd2c542d6d50.png)

  

#### Responses 

The response of this endpoint service request contains the `Task<Models.ICGBusinessEntitiesProspectDropboxFile>` object. The class name of this object is 

```markdown
 ICGBusinessEntitiesProspectDropboxFile
``` 

#### Response body-JSON  
```markdown
 {
  "Id": null,
  "ProspectId": null,
  "FileTypeId": null,
  "FileSubtypeId": null,
  "FileName": null,
  "FileId": null,
  "AddedBy": null,
  "AddedUTCDate": null,
  "AddedMethod": null,
  "ServerModifiedDate": null,
  "Comment": null,
  "Size": null
}      
```

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

    
##### 'Task<Models.ICGBusinessEntitiesProspectDropboxFile>' Object Parameters

![5](https://user-images.githubusercontent.com/110983629/189988133-447c0f25-2389-4b1f-b005-74aa318e6d24.png)

 
  
#### Explorer 

|Names|Description|
|-----|-----------|
|Task<Models.ICGBusinessEntitiesProspectDropboxFile>|[Task<Models.ICGBusinessEntitiesProspectDropboxFile>](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-business-entities-prospect-dropbox-file)
 






### Prospect Dropbox Files Delete Prospect Dropbox Files
#### Description
With the use of this service endpoint, merchants can delete a file from the prospect Dropbox files. The user will not able to access the removed file anymore. 
The 'ProspectDropboxFilesDeleteProspectDropboxFilesAsync' method of the 'ProspectDropboxFilesController' class will be called by the API client for this process in order to delete the file.


```markdown
 ProspectDropboxFilesDeleteProspectDropboxFilesAsync(
    int prospectId,
    Models.ICGBusinessEntitiesProspectDropboxFileDeleteRequest model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int prospectId = 118;
var model = new ICGBusinessEntitiesProspectDropboxFileDeleteRequest();

try
{
    object result = await prospectDropboxFilesController.ProspectDropboxFilesDeleteProspectDropboxFilesAsync(prospectId, model);
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectDropboxFilesController" object fails to delete the file that was anticipated to be returned. The prospect id and model object will be passed as parameters to the `ProspectDropboxFilesDeleteProspectDropboxFilesAsync`. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.


#### Parameters Detail   
The parameters of this endpoint service request requires two parameters which are **prospectId** (int type) and **model** object. The model object will further contains the information (such as file id and file name) of the file that is intended to be delete. 
  
![6](https://user-images.githubusercontent.com/110983629/189991408-781bf818-f366-48d7-92b4-bc9c70f2e076.png)


The class name of the **model** object is 
```markdown
ICGBusinessEntitiesProspectDropboxFileDeleteRequest
```

#### model object parameters

![7](https://user-images.githubusercontent.com/110983629/189991859-8c18547b-e163-409a-8da2-f55276affc82.png)


    
#### Explorer 

|Names|Description|
|-----|-----------|
|model (required)|[Models.ICGBusinessEntitiesProspectDropboxFileDeleteRequest](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-business-entities-prospect-dropbox-file-delete-request)|

#### Responses 

The response of this endpoint service request contains the `Task<object>` that will determine whether the file get deleted or not.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|









### Prospect Dropbox Files Upload
#### Description
With the use of this service endpoint, User can upload a file in the Dropbox as well as also a row will be inserted into the database for uploading file into the dropbox.  
The 'ProspectDropboxFilesUploadAsync' method of the 'ProspectDropboxFilesController' class will be called by the API client for this process in order to upload the file and inserting row in the database.


```markdown
 ProspectDropboxFilesUploadAsync(
    int prospectId,
    int typeId,
    int subtypeId)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int prospectId = 118;
int typeId = 190;
int subtypeId = 220;

try
{
    object result = await prospectDropboxFilesController.ProspectDropboxFilesUploadAsync(prospectId, typeId, subtypeId);
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectDropboxFilesController" object fails to upload a file that was anticipated to be returned. The prospectId, typeId and subtypeId will be passed as parameters to the `ProspectDropboxFilesUploadAsync` method for uploading file into the specific prospect. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail   
The parameters of this endpoint service request requires three parameters which are **prospectId** (int type), **typeId** (int type), and **subtypeId** (int type). The prospectid is unique for each prospect, typeId is unique for each file type Id and subtypeId can be zero if the uploading file does not have any sub type.
  
![8](https://user-images.githubusercontent.com/110983629/189995473-9a5da728-c816-43ee-989d-89b8f9626001.png)

  
#### Responses 

The response of this endpoint service request contains the `Task<object>` that will determine whether the file get uploaded in the dropbox or not.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|







### Prospect Dropbox Files Get Dropbox File
#### Description
With the use of this service endpoint, User can retrieve a file from the Dropbox that you have uploaded before in the dropbox by entering the prospect id and file id.
The 'ProspectDropboxFilesGetDropboxFileAsync' method of the 'ProspectDropboxFilesController' class will be called by the API client for this process in order to get the file.


```markdown
  ProspectDropboxFilesGetDropboxFileAsync(
    int prospectId,
    string fileId)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int prospectId = 118;
string fileId = "fileId6";

try
{
    object result = await prospectDropboxFilesController.ProspectDropboxFilesGetDropboxFileAsync(prospectId, fileId);
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectDropboxFilesController" object fails to retrieve a file that was anticipated to be returned. The prospectId, fileId will be passed as parameters to the `ProspectDropboxFilesGetDropboxFileAsync` method for getting file of the specific prospect type. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail   
The parameters of this endpoint service request requires two parameters which are **prospectId** (int type), and **fileId** (int type). The prospectid is unique for each prospect, fileid is unique for each file uploaded into the dropbox.
   
   
![9](https://user-images.githubusercontent.com/110983629/189997593-61948d75-f14a-4087-abc2-e946e9a32e80.png)

  
#### Responses 

The response of this endpoint service request contains the `Task<object>` that will determine whether the file get retrieved from the dropbox or not.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|










### Prospect Dropbox Files Get Dropbox File Show Inline
#### Description 
By supplying the prospect id and file id at this service endpoint, the user can get a file from Dropbox that they have previously put there. The user will see the file inline so that he may readily access the data that is written in it.
The 'ProspectDropboxFilesGetDropboxFileShowInlineAsync' method of the 'ProspectDropboxFilesController' class will be called by the API client for this process in order to get the file.


```markdown
  ProspectDropboxFilesGetDropboxFileShowInlineAsync(
    int prospectId,
    string fileId)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int prospectId = 118;
string fileId = "fileId6";

try
{
    object result = await prospectDropboxFilesController.ProspectDropboxFilesGetDropboxFileShowInlineAsync(prospectId, fileId);
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectDropboxFilesController" object fails to retrieve a file that was anticipated to be returned. The prospectId, fileId will be passed as parameters to the `ProspectDropboxFilesGetDropboxFileAsync` method for getting file of the specific prospect type. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 

#### Parameters Detail   
The parameters of this endpoint service request requires two parameters which are **prospectId** (int type), and **fileId** (int type). The prospectid is unique for each prospect, fileid is unique for each file uploaded into the dropbox.
   
![10](https://user-images.githubusercontent.com/110983629/189999222-82b240a7-6e0e-4dae-a783-1e4f189aca09.png)

  
#### Responses 

The response of this endpoint service request contains the `Task<object>` that will determine whether the file get retrieved from the dropbox or not.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|







### Prospect Dropbox Files Update Comment
#### Description
With the use of this service endpoint, users can update the comment of a file that is accessed from Dropbox files by entering the fileId, and prospect id.
The 'ProspectDropboxFilesUpdateCommentAsync' method of the 'ProspectDropboxFilesController' class will be called by the API client for this process in order to delete the file.


```markdown
 ProspectDropboxFilesUpdateCommentAsync(
    int prospectId,
    string fileId,
    Models.ICGBusinessEntitiesProspectDropboxFileComment commentData)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int prospectId = 118;
string fileId = "fileId6";
var commentData = new ICGBusinessEntitiesProspectDropboxFileComment();

try
{
    object result = await prospectDropboxFilesController.ProspectDropboxFilesUpdateCommentAsync(prospectId, fileId, commentData);
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectDropboxFilesController" object fails to update the comment on file that was anticipated to be returned. The prospect id, fileid and model object will be passed as parameters to the `ProspectDropboxFilesUpdateCommentAsync`. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.


#### Parameters Detail   
The parameters of this endpoint service request requires three parameters which are **prospectId** (int type), **fileId** (String type), and **commentData** object. The commentData object will further contains the comment that user has edited on the file.
  
  
![11](https://user-images.githubusercontent.com/110983629/190001092-98865aee-7661-4833-ba31-d7fb0a1605e8.png)


The class name of the **commentData** object is 
```markdown
 ICGBusinessEntitiesProspectDropboxFileComment
```

#### commentData object parameters
 
![12](https://user-images.githubusercontent.com/110983629/190001280-b6652be2-e478-4530-92d6-2d1796caa097.png)

 
    
#### Explorer 

|Names|Description|
|-----|-----------|
|commentData (required)|[Models.ICGBusinessEntitiesProspectDropboxFileComment](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-business-entities-prospect-dropbox-file-comment)|

#### Responses 

The response of this endpoint service request contains the `Task<object>` that will determine whether the comment on file get updated or not.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|







## API Endpoints
## Prospect Extras
### Prospect Extras Get Parameters
#### Description
This service endpoint will allow the user to retrieve all the parameters, master tables, static things used by the prospect that comes from the database. For this purpose, an instance of `ProspectExtrasController` class is created by the API client for invoking the `ProspectExtrasGetParametersAsync` method.

```markdown
ProspectExtrasController prospectExtrasController = client.ProspectExtrasController;
```

```markdown
  ProspectExtrasGetParametersAsync()
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
try
{
    ICGBusinessEntitiesProspectParameters result = await prospectExtrasController.ProspectExtrasGetParametersAsync();
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectExtrasController" object fails to retrieve prospect extras that was anticipated to be returned. These extras will include the all the parameters, master tables, static things used by the prospect. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.


#### Parameters Detail   
This endpoint does not take any parameter.


#### Responses 

The response of this endpoint service request contains the `Task<Models.ICGBusinessEntitiesProspectParameters>` that will provide all the parameters to the user that are associated with the prospect.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|


The class name of the **Task<Models.ICGBusinessEntitiesProspectParameters>** object is 
```markdown
  ICGBusinessEntitiesProspectParameters
```

#### ICGBusinessEntitiesProspectParameters object parameters
 
![13](https://user-images.githubusercontent.com/110983629/190173660-807e4496-a61c-4c24-975b-82fe84306bfb.png)

####  Isos Class name and object parameters

![14](https://user-images.githubusercontent.com/110983629/190174185-13cea1d6-7092-4d56-9241-60accb8113de.png)


#### SalesReps Class name and object parameters


![15](https://user-images.githubusercontent.com/110983629/190174222-c5709f19-4076-49aa-aced-5158d5a557a6.png)


    
#### Explorer 

|Names|Description|
|-----|-----------|
|Task<Models.ICGBusinessEntitiesProspectParameters>|[Task<Models.ICGBusinessEntitiesProspectParameters>](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-business-entities-prospect-parameters)|






### Prospect Extras Update Status
#### Description
This service endpoint will allow the user to update the status of the prospect by entering the prospect id which is unique for each prospect. For this purpose, an instance of `ProspectExtrasController` class is created by the API client for invoking the `ProspectExtrasUpdateStatusAsync` method.

```markdown
 ProspectExtrasUpdateStatusAsync(
    int prospectId,
    Models.ICGBusinessEntitiesProspectStatusUpdateRequest statusUpdate)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int prospectId = 118;
var statusUpdate = new ICGBusinessEntitiesProspectStatusUpdateRequest();

try
{
    ICGBusinessEntitiesProspectStatusUpdateResponse result = await prospectExtrasController.ProspectExtrasUpdateStatusAsync(prospectId, statusUpdate);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectExtrasController" object fails to update the prospect status that was anticipated to be returned. The statusUpdate is the object of `ICGBusinessEntitiesProspectStatusUpdateRequest` type and prospectId will be passed as parameters to the `ProspectExtrasUpdateStatusAsync` method. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.


#### Parameters Detail   
The parameters of this endpoint includes the **prospectId** (int type), **statusUpdate** object. The statusUpdate object further contains the ProspectStatusId (int type) and Message (String type). 

![16](https://user-images.githubusercontent.com/110983629/190181736-38015d24-0b00-4041-9c69-14729d5272a7.png)

The class name of statusUpdate object

```markdown
ICGBusinessEntitiesProspectStatusUpdateRequest
```

#### statusUpdate Object Parameters  
![17](https://user-images.githubusercontent.com/110983629/190182514-bd12ce33-6eec-4d39-8059-ca2776ec756a.png)



#### Responses 

The response of this endpoint service request contains the `Task<Models.ICGBusinessEntitiesProspectStatusUpdateResponse>` that will update the status of the prospect.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|


The class name of the **Task<Models.ICGBusinessEntitiesProspectStatusUpdateResponse>** object is 
```markdown
   ICGBusinessEntitiesProspectStatusUpdateResponse
```

#### Task<Models.ICGBusinessEntitiesProspectStatusUpdateResponse> object parameters
 
![18](https://user-images.githubusercontent.com/110983629/190183476-5ab23c9d-16bb-435d-9475-7b5a12c5c564.png)


    
#### Explorer 

|Names|Description|
|-----|-----------|
|Task<Models.ICGBusinessEntitiesProspectStatusUpdateResponse>|[Task<Models.ICGBusinessEntitiesProspectStatusUpdateResponse>](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-business-entities-prospect-status-update-response)|











### Prospect Extras Get Prospect Summary
#### Description
This service endpoint will allow the user to retrieve the prospect summary of a prospect by entering the prospect id which is unique for each prospect. For this purpose, an instance of `ProspectExtrasController` class is created by the API client for invoking the `ProspectExtrasGetProspectSummaryAsync` method.

```markdown
 ProspectExtrasGetProspectSummaryAsync(
    int prospectId)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int prospectId = 118;
try
{
    ICGBusinessEntitiesProspectSalesRep result = await prospectExtrasController.ProspectExtrasGetProspectSummaryAsync(prospectId);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectExtrasController" object fails to retrieve summary of the prospect that was anticipated to be returned. The prospectId will be passed as a parameter to the `ProspectExtrasGetProspectSummaryAsync` method. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.


#### Parameters Detail    

The parameters of this endpoint includes the **prospectId** (int type) that is required for the prospect to enter for retrieving the prospect summary.

![19](https://user-images.githubusercontent.com/110983629/190188642-23c2371a-09ec-488c-bdd6-bd87d8a19ad6.png)

 
#### Responses 

The response of this endpoint service request contains the `Task<Models.ICGBusinessEntitiesProspectSalesRep>` that will return the summary of the prospect whose id is entered.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|


The class name of the **Task<Models.ICGBusinessEntitiesProspectSalesRep>** object is 
```markdown
    ICGBusinessEntitiesProspectSalesRep
```

#### Task<Models.ICGBusinessEntitiesProspectSalesRep> object parameters
  
![20](https://user-images.githubusercontent.com/110983629/190189664-fe81cef1-8688-4e49-8488-25907e5828c0.png)

  
#### Explorer 

|Names|Description|
|-----|-----------|
|Task<Models.ICGBusinessEntitiesProspectSalesRep>|[Task<Models.ICGBusinessEntitiesProspectSalesRep>](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-business-entities-prospect-sales-rep)|












## API Endpoints
## Prospect Generate Pdf
### Prospect Generate Pdf Generate Pdf File
#### Description
This service endpoint will allow the user to generate the PDF file for the prospect. For this purpose, an instance of `ProspectGeneratePdfController` class is created by the API client for invoking the `ProspectGeneratePdfGeneratePdfFileAsync` method.

```markdown
 ProspectGeneratePdfController prospectGeneratePdfController = client.ProspectGeneratePdfController;
```

```markdown
  ProspectGeneratePdfGeneratePdfFileAsync(
    int id)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int id = 112;
try
{
    object result = await prospectGeneratePdfController.ProspectGeneratePdfGeneratePdfFileAsync(id);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectGeneratePdfController" object fails to generate the PDF file for prospect that was anticipated to be returned. The id will be passed as parameter to `ProspectGeneratePdfGeneratePdfFileAsync` method for generating the PDF file. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.


#### Parameters Detail   
This endpoint requires only one parameter which is id for generating the PDF file of the prospect.


#### Responses 

The response of this endpoint service request contains the `Task<object>` that will indicate whether the PDF file get generated or not.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|







## API Endpoints
## Prospect Integration
### Prospect Integration Get Prospect Percentage of Completion
#### Description
This service endpoint will allow the user to retrieve the Percentage of completion and Missing fields for the prospect.In order to do that, an instance of `ProspectIntegrationController` class is created by the API client for invoking the `ProspectIntegrationGetProspectPercentageOfCompletionAsync` method.

```markdown
  ProspectIntegrationController prospectIntegrationController = client.ProspectIntegrationController;
```

If permission FEATURE_MERCHANTS_NEW is assign to user going to get percentage including new features fields. 

```markdown
   ProspectIntegrationGetProspectPercentageOfCompletionAsync(
    int prospectId)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int prospectId = 118;
try
{
    ICGBusinessEntitiesProspectCompletionInformation result = await prospectIntegrationController.ProspectIntegrationGetProspectPercentageOfCompletionAsync(prospectId);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectIntegrationController" object fails to retrieve percentage of completion and missing fields for prospect that was anticipated to be returned. The id will be passed as parameter to `ProspectIntegrationGetProspectPercentageOfCompletionAsync` method for getting the data of missing fields. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.


#### Parameters Detail    

The parameters of this endpoint includes the **prospectId** (int type) that is required for the prospect to enter for retrieving the percentage of completion along with the missing fields.
 
![21](https://user-images.githubusercontent.com/110983629/190408707-000bda82-023b-46f3-a17d-03074ae3f950.png)

  
#### Responses 

The response of this endpoint service request contains the `Task<Models.ICGBusinessEntitiesProspectCompletionInformation>` that will returns the completion percentage with the missing fields of the specific prospect.


#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

#### Response Body
```markdown
{
  "IsUpdated": null,
  "PercentageOfCompletionMissingFields": null,
  "PercentageOfCompletionMissingFiles": null,
  "Id": null,
  "MerchantName": null,
  "FieldsPercentageOfCompletion": null,
  "FilesPercentageOfCompletion": null
}
```
  

The class name of the **Task<Models.ICGBusinessEntitiesProspectCompletionInformation>** object is 
```markdown
     ICGBusinessEntitiesProspectCompletionInformation
```

#### Task<Models.ICGBusinessEntitiesProspectCompletionInformation> object parameters
  
![22](https://user-images.githubusercontent.com/110983629/190409346-a8a658e4-27e3-414d-8d59-a1b7fcc381c2.png)
  
#### Explorer 

|Names|Description|
|-----|-----------|
|Response Type|[Task<Models.ICGBusinessEntitiesProspectCompletionInformation>](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-business-entities-prospect-completion-information)|



 




### Prospect Integration Submit Elavon
#### Description 

This service endpoint will allow the user to initiates the processing to Elavon by entering the prospect id which is unique for each prospect. For this purpose, an instance of `ProspectIntegrationController` class is created by the API client for invoking the `ProspectIntegrationSubmitElavonAsync` method.


```markdown
    ProspectIntegrationSubmitElavonAsync(
    int prospectId)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int prospectId = 118;
try
{
    ICGBusinessEntitiesProspectIntegrationResult result = await prospectIntegrationController.ProspectIntegrationSubmitElavonAsync(prospectId);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectIntegrationController" object fails to initiate the process to Elavon for prospect that was anticipated to be returned. The prospectId will be passed as parameter to `ProspectIntegrationSubmitElavonAsync` method for starting the Elavon process. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.


#### Parameters Detail    

The parameter of this endpoint includes the **prospectId** (int type) that is required for accessing the specific prospect to start the elavon process. 
 
![21](https://user-images.githubusercontent.com/110983629/190408707-000bda82-023b-46f3-a17d-03074ae3f950.png)

  
#### Responses 

The response of this endpoint service request contains the `Task<Models.ICGBusinessEntitiesProspectIntegrationResult>` that will returns the data of elavon processing. 


#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

#### Response Body
```markdown
{
  "Success": null,
  "ErrorMessage": null,
  "NewSubmition": null,
  "Prospect": null
}
```
  

The class name of the **Task<Models.ICGBusinessEntitiesProspectIntegrationResult>** object is 
```markdown
     ICGBusinessEntitiesProspectIntegrationResult
```

#### Task<Models.ICGBusinessEntitiesProspectIntegrationResult> object parameters
  
![23](https://user-images.githubusercontent.com/110983629/190412848-4ba5cf25-8166-40ad-8469-8e838db8f02d.png)


#### Explorer 

|Names|Description|
|-----|-----------|
|Response Type|[Task<Models.ICGBusinessEntitiesProspectIntegrationResult>](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-business-entities-prospect-integration-result)|
|Models.ICGModelsUnderwritingProspect|[Models.ICGModelsUnderwritingProspect](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-models-underwriting-prospect)|









### Prospect Integration Submit Admin Console
#### Description 
This service endpoint will allow the user to submit the prospect to the admin console. In order to submit the prospect, it will be accessed through the prospect id which is a unique identifier for the prospect. An instance of `ProspectIntegrationController` class is created by the API client for invoking the `ProspectIntegrationSubmitAdminConsoleAsync` method.


```markdown
   ProspectIntegrationSubmitAdminConsoleAsync(
    int prospectId)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int prospectId = 118;
try
{
    ICGBusinessEntitiesProspectIntegrationResult result = await prospectIntegrationController.ProspectIntegrationSubmitAdminConsoleAsync(prospectId);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectIntegrationController" object fails to submit the prospect to the admin console that was anticipated to be returned. The prospectId will be passed as parameter to `ProspectIntegrationSubmitAdminConsoleAsync` method for submitting the specific prospect. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.


#### Parameters Detail    

The parameter of this endpoint includes the **prospectId** (int type) that is required for accessing the specific prospect to submit it to admin. 
 
![21](https://user-images.githubusercontent.com/110983629/190408707-000bda82-023b-46f3-a17d-03074ae3f950.png)

  
#### Responses 

The response of this endpoint service request contains the `Task<Models.ICGBusinessEntitiesProspectIntegrationResult>` that will returns the prospect data which is submitting to admin. 


#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

#### Response Body
```markdown
 {
  "Success": null,
  "ErrorMessage": null,
  "NewSubmition": null,
  "Prospect": null
}
```
  
The class name of the **Task<Models.ICGBusinessEntitiesProspectIntegrationResult>** object is 
```markdown
    ICGBusinessEntitiesProspectIntegrationResult
```

#### Task<Models.ICGBusinessEntitiesProspectIntegrationResult> object parameters

![24](https://user-images.githubusercontent.com/110983629/190418160-e9753a27-a632-4083-90d2-7c55c8df919f.png)

   

#### Explorer 

|Names|Description|
|-----|-----------|
|Response Type|[Task<Models.ICGBusinessEntitiesProspectIntegrationResult>](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-business-entities-prospect-integration-result)|
|Models.ICGModelsUnderwritingProspect|[Models.ICGModelsUnderwritingProspect](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-models-underwriting-prospect)|






### Prospect Integration Update Prospect Merchant Id
#### Description 
This service endpoint will allow the user to update prospect merchant id after doing integration with the Administration Service Console (ASC). In order to update the merchant id, prospect will be accessed through the prospect id which is a unique identifier for each prospect. An instance of `ProspectIntegrationController` class is created by the API client for invoking the `ProspectIntegrationUpdateProspectMerchantIdAsync` method.


```markdown 
ProspectIntegrationUpdateProspectMerchantIdAsync(
    int prospectId,
    int merchantId,
    string merchantCode)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int prospectId = 118;
int merchantId = 72;
string merchantCode = "merchantCode6";
try
{
    ICGBusinessEntitiesProspectIntegrationResult result = await prospectIntegrationController.ProspectIntegrationUpdateProspectMerchantIdAsync(prospectId, merchantId, merchantCode);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectIntegrationController" object fails to update the merchant id that was anticipated to be returned. The prospectId, merchantId and merchantCode will be passed as parameters to `ProspectIntegrationUpdateProspectMerchantIdAsync` method for updating the merchant id of the specific merchant associated with the specific prospect. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.


#### Parameters Detail    

The parameter of this endpoint includes the **prospectId** (int type), **merchantId** (int type), **merchantCode** (String type) that are required to enter for accessing the specific prospect of the specific merchant.
  
![25](https://user-images.githubusercontent.com/110983629/190424550-a9502449-4929-4582-97ad-f31bed5f22ee.png)

  
#### Responses 

The response of this endpoint service request contains the `Task<Models.ICGBusinessEntitiesProspectIntegrationResult>` that will returns the results along with prospect data for which the merchant id is updated.


#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

#### Response Body
```markdown
 {
  "Success": null,
  "ErrorMessage": null,
  "NewSubmition": null,
  "Prospect": null
}
```
  
The class name of the **Task<Models.ICGBusinessEntitiesProspectIntegrationResult>** object is 
```markdown
     ICGBusinessEntitiesProspectIntegrationResult
```

#### Task<Models.ICGBusinessEntitiesProspectIntegrationResult> object parameters
 
![26](https://user-images.githubusercontent.com/110983629/190425524-1b66c1da-95e1-4e47-8c6e-41f5da3ba580.png)

   

#### Explorer 

|Names|Description|
|-----|-----------|
|Response Type|[Task<Models.ICGBusinessEntitiesProspectIntegrationResult>](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-business-entities-prospect-integration-result)|
|Prospect object in Response|[Models.ICGModelsUnderwritingProspect](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-models-underwriting-prospect)|





### Prospect Integration Get Prospectby Merchant Id
#### Description  
By providing the merchant id, the user will be able to obtain the prospect's data from this service endpoint. Each merchant is uniquely identified by their merchant id, which may be used to determine which merchant is associated with which prospect. The API client creates an instance of the "ProspectIntegrationController" class using the "ProspectIntegrationGetProspectbyMerchantIdAsync" method.

```markdown 
 ProspectIntegrationGetProspectbyMerchantIdAsync(
    int merchantId)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int merchantId = 72;
try
{
    ICGBusinessEntitiesProspect result = await prospectIntegrationController.ProspectIntegrationGetProspectbyMerchantIdAsync(merchantId);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectIntegrationController" object fails to retrieve the prospect details that was anticipated to be returned. The merchantId will be passed as parameter to `ProspectIntegrationGetProspectbyMerchantIdAsync` method for getting the specific prospects of the merchant. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.


#### Parameters Detail    

The parameter of this endpoint includes the **merchantId** (int type) that is required to enter for accessing the specific prospect of the specific merchant.
   
![27](https://user-images.githubusercontent.com/110983629/190431882-eb4f17e1-a920-4ecb-8d81-0285f802fbe8.png)

  
#### Responses 

The response of this endpoint service request contains the `Task<Models.ICGBusinessEntitiesProspect>` that will returns the prospect details for which the merchant id is provided.


#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

#### Response Body
```markdown
 {
  "PrincipalOwners": null,
  "Users": null,
  "ContactsEmailNoticeList": null,
  "Ach": null,
  "CC": null,
  "ProcessorCode": null,
  "ProspectProducts": null,
  "ProspectProductValues": null,
  "ProspectSettings": null,
  "ProspectCampaigns": null,
  "ProspectIntermediaryBusinessOwnerships": null,
  "CustomFields": null,
  "CustomPaymentPortals": null,
  "ProspectAdobeDocuments": null,
  "CallbackFunction": null,
  "Id": null,
  "ProspectTypeId": null,
  "ProspectStatusId": null,
  "IsACH": null,
  "IsCC": null,
  "FeeModelId": null,
  "MerchantName": null,
  "Iso": null,
  "ReferalPartner": null,
  "SalesRepName": null,
  "SalesRepEmail": null,
  "SalesRepCode": null,
  "NotesForUnderwriting": null,
  "DbaName": null,
  "LegalBusinessName": null,
  "FederalTaxId": null,
  "SicCode": null,
  "NaicsCode": null,
  "BusinessAddress1": null,
  "BusinessAddress2": null,
  "City": null,
  "State": null,
  "ZipCode": null,
  "MonthEstablished": null,
  "YearEstablished": null,
  "StateOrganization": null,
  "BusinessPhoneNumber": null,
  "CustomerServicePhoneNumber": null,
  "MerchantWebsiteURL": null,
  "NoMerchantWebsiteURL": null,
  "TypeBusiness": null,
  "DetailedInfoPayment": null,
  "TypeOwnershipsId": null,
  "TaxClassificationsId": null,
  "TaxClassificationsTypeId": null,
  "HadAdminHearing": null,
  "AdminHearingReson": null,
  "ContactFirstName": null,
  "ContactLastName": null,
  "ContactTitle": null,
  "ContactEmail": null,
  "ContactPhone": null,
  "ContactExtension": null,
  "AREmail": null,
  "POAEmail": null,
  "TechnicalContactEmail": null,
  "TechnicalContactName": null,
  "IsBusinessContactPreferred": null,
  "BusinessContactEmail": null,
  "BusinessContactName": null,
  "IsOwnerOfficerContactPreferred": null,
  "OwnerOfficerContactEmail": null,
  "OwnerOfficerContactName": null,
  "FeeScheduleGatewaySetupFee": null,
  "FeeScheduleGatewayMonthlyFee": null,
  "HasFeeScheduleCustomPaymentPortal": null,
  "FeeScheduleCustomPaymentPortal": null,
  "HasFeeScheduleICGInvoicing": null,
  "FeeScheduleICGInvoicing": null,
  "HasFeeScheduleQuickBooksPlugin": null,
  "FeeScheduleQuickBooksPlugin": null,
  "HasFeeScheduleQuickBooksOnline": null,
  "FeeScheduleQuickBooksOnline": null,
  "HasFeeScheduleWooCommercePlugin": null,
  "FeeScheduleWooCommercePlugin": null,
  "HasFeeScheduleIVRFee": null,
  "FeeScheduleIVRFee": null,
  "HasFeeScheduleSMSProcessingFee": null,
  "FeeScheduleSMSProcessingFee": null,
  "HasFeeScheduleMagtekUSBSwiper": null,
  "FeeScheduleMagtekUSBSwiper": null,
  "HasFeeScheduleMobileSwiper": null,
  "FeeScheduleMobileSwiper": null,
  "HasLockboxProcessingFeesStandard": null,
  "LockboxProcessingFeesStandard": null,
  "HasLockboxProcessingFeesLarge": null,
  "LockboxProcessingFeesLarge": null,
  "IsIcgVerify": null,
  "IcgVerifyVerificationFee": null,
  "IcgVerifyEstimatedNVerificationsPerMonth": null,
  "IcgVerifyPurposeOfUsingVerificationServices": null,
  "IsIcgVerifyTypeServiceAPIAccess": null,
  "IsIcgVerifyTypeServiceManuallyRunning": null,
  "IcgVerifyBillingOptionsId": null,
  "SettlementAccountBank": null,
  "SettlementAccountRouting": null,
  "SettlementAccountNumber": null,
  "SettlementAccountType": null,
  "IsBillingAccountSameAsSettlement": null,
  "BillingAccountBank": null,
  "BillingAccountRouting": null,
  "BillingAccountNumber": null,
  "BillingAccountType": null,
  "PaymentModelSettlementAccountBank": null,
  "PaymentModelSettlementAccountRouting": null,
  "PaymentModelSettlementAccountNumber": null,
  "IsPaymentModelBillingAccountSameAsSettlement": null,
  "PaymentModelBillingAccountBank": null,
  "PaymentModelBillingAccountRouting": null,
  "PaymentModelBillingAccountNumber": null,
  "PaymentPortalTypeId": null,
  "IsICGInvoicing": null,
  "MerchantPaymentURL": null,
  "ContactRequirementPortalName": null,
  "ContactRequirementPortalPhone": null,
  "PaymentPortalNotes": null,
  "CreatedUtcDate": null,
  "CreatedUser": null,
  "CurrentLoggedUser": null,
  "CurrentUser": null,
  "CurrentAdmin": null,
  "ElavonIntegrationApplicationId": null,
  "ElavonIntegrationMerchantNumber": null,
  "PercentageCompletionFields": null,
  "PercentageCompletionFiles": null,
  "CanIntegrateWithElavon": null,
  "AdminConsoleMerchantCode": null,
  "AdminConsoleMerchantPaymentFeeCode": null,
  "AdminConsoleMerchantId": null,
  "RelationshipManager": null,
  "RecurringOption": null,
  "RecurringFrequency": null,
  "AchConvenienceFee": null,
  "IsAchConvenienceFeeTypeFlat": null,
  "IsAchConvenienceFeeTypePercentage": null,
  "AchConvenienceFeeAmount": null,
  "CreditDebitCardConvenienceFeeOption": null,
  "IsCreditDebitCardConvenienceFeeFlat": null,
  "IsCreditDebitCardConvenienceFeePercentage": null,
  "CreditDebitCardConvenienceFeeAmount": null,
  "AnnualReviewStatus": null,
  "HasPlaidMerchantToken": null,
  "IsAuthVerify": null,
  "AccountBalanceVerify": null,
  "IdentityVerify": null,
  "WixWebSiteFee": null,
  "HasWixWebSiteFee": null,
  "HasInvoicingOptions": null,
  "FeeInvoicingOptions": null,
  "HasEmailInvoicing": null,
  "FeeEmailInvoicing": null,
  "HasSmsInvoicing": null,
  "FeeSmsInvoicing": null,
  "HasFeeScheduleSMSNotify": null,
  "FeeScheduleSMSNotify": null,
  "HasIcgProcessPaymentToken": null,
  "IcgProcessPaymentToken": null,
  "AssignUserId": null
}
```
  
The class name of the **Task<Models.ICGBusinessEntitiesProspect>** object is 
```markdown
      ICGBusinessEntitiesProspect
```

#### Task<Models.ICGBusinessEntitiesProspect> object parameters
 
![28](https://user-images.githubusercontent.com/110983629/190434100-efa19965-e600-43a7-9f08-3ac07b70d214.png)

 

#### Explorer 

|Names|Description|
|-----|-----------|
|Response Type|[Task<Models.ICGBusinessEntitiesProspect>](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-business-entities-prospect)| 








## API Endpoints
## Prospect Logs
### Prospect Logs Get Prospect Logs
#### Description
This service endpoint will allow the user to retrieve prospect logs by entering the prospect id which is a unique identifier for each prospect. For this purpose, an instance of `ProspectLogsController` class is created by the API client for invoking the `ProspectLogsGetProspectLogsAsync` method.

```markdown
 ProspectLogsController prospectLogsController = client.ProspectLogsController;
```

```markdown
  ProspectLogsGetProspectLogsAsync(
    int prospectId)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int prospectId = 118;
try
{
    ICGBusinessEntitiesProspectLog result = await prospectLogsController.ProspectLogsGetProspectLogsAsync(prospectId);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectLogsController" object fails to retrieve prospect logs that was anticipated to be returned. The prospectId will be passed as parameter to `ProspectLogsGetProspectLogsAsync` method for getting the specific logs. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.


#### Parameters Detail    
This endpoint requires only one parameter which is **prospectId** (int type) for retrieving the prospect logs details.

![34](https://user-images.githubusercontent.com/110983629/190437098-d52ecccf-06b8-4386-adf4-e3fc9db21655.png)


#### Responses 

The response of this endpoint service request contains the `Task<Models.ICGBusinessEntitiesProspectLog>` that will returns the prospect logs to the user.

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|



#### Response Body
```markdown
 {
  "Id": null,
  "ProspectId": null,
  "UtcDate": null,
  "UserName": null,
  "ProspectStatusId": null,
  "ProspectStatus": null,
  "ProspectLogTypeId": null,
  "ProspectLogType": null,
  "Message": null
}
```
  
The class name of the **Task<Models.ICGBusinessEntitiesProspectLog>** object is 
```markdown
      ICGBusinessEntitiesProspectLog
```

#### Task<Models.ICGBusinessEntitiesProspectIntegrationResult> object parameters
 
![35](https://user-images.githubusercontent.com/110983629/190442796-4e435695-88d1-4fff-a8ad-ef506144ff7b.png)


#### Explorer 

|Names|Description|
|-----|-----------|
|Response Type|[Task<Models.ICGBusinessEntitiesProspectIntegrationResult> ](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-business-entities-prospect-log)|
 






## API Endpoints
## Prospect Messages
### Prospect Messages Get Prospect Messages
#### Description
This service endpoint will allow the user to retrieve the messages that are sent for the prospect. You can access them by entering the prospect id which is a unique identifier for each prospect. For this purpose, an instance of `ProspectMessagesController` class is created by the API client for invoking the `ProspectMessagesGetProspectMessagesAsync` method.

```markdown
 ProspectMessagesController prospectMessagesController = client.ProspectMessagesController;
```

```markdown
   ProspectMessagesGetProspectMessagesAsync(
    int prospectId)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int prospectId = 118;
try
{
    ICGBusinessEntitiesProspectMessageSent result = await prospectMessagesController.ProspectMessagesGetProspectMessagesAsync(prospectId);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectMessagesController" object fails to retrieve messages of the prospect that was anticipated to be returned. The prospectId will be passed as parameter to `ProspectMessagesGetProspectMessagesAsync` method for getting the messages of the specific prospect. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.


#### Parameters Detail     
This endpoint requires only one parameter which is **prospectId** (int type) for retrieving the messages of the prospect.

![36](https://user-images.githubusercontent.com/110983629/190445193-037f2977-3443-47fb-9477-90bd640d30dc.png)


#### Responses 

The response of this endpoint service request contains the `Task<Models.ICGBusinessEntitiesProspectMessageSent>` that will returns the messages details to the user.

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|



#### Response Body
```markdown
 {
  "Id": null,
  "SentDate": null,
  "ProspectId": null,
  "FromUserName": null,
  "ToUserName": null,
  "Message": null
}
```
  
The class name of the **Task<Models.ICGBusinessEntitiesProspectMessageSent>** object is 
```markdown
       ICGBusinessEntitiesProspectMessageSent
```

#### Task<Models.ICGBusinessEntitiesProspectMessageSent> object parameters
 
![37](https://user-images.githubusercontent.com/110983629/190445583-a50d53f7-f5af-48fb-8ecd-4429392dd433.png)


#### Explorer 

|Names|Description|
|-----|-----------|
|Response Type|[Task<Models.ICGBusinessEntitiesProspectMessageSent>](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-business-entities-prospect-message-sent)|
 









### Prospect Messages Post
#### Description
This service endpoint will allow the user to send a message to the user. This message will also get saved when user send a message. For this purpose, an instance of `ProspectMessagesController` class is created by the API client for invoking the `ProspectMessagesPostAsync` method.

```markdown
  ProspectMessagesPostAsync(
    int prospectId,
    Models.ICGBusinessEntitiesProspectMessage message)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int prospectId = 118;
var message = new ICGBusinessEntitiesProspectMessage();

try
{
    ICGBusinessEntitiesProspectMessage result = await prospectMessagesController.ProspectMessagesPostAsync(prospectId, message);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectMessagesController" object fails to send a message that was anticipated to be returned. The prospectId and message will be passed as parameters to `ProspectMessagesPostAsync` method for sending a message which is associated with the specific prospect. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.


#### Parameters Detail     
This endpoint requires only two parameters which are **prospectId** (int type) and **message** object for sending and saving the message of the prospect.
 
![38](https://user-images.githubusercontent.com/110983629/190448195-38b2d7cc-48c4-4c9d-af19-eaf88db3677b.png)

The class name of the **message** object is

```markdown
ICGBusinessEntitiesProspectMessage
```


#### message object parameters

![39](https://user-images.githubusercontent.com/110983629/190448764-0381559f-b579-41d2-9cdf-b0d4fc0d8e59.png)



#### Responses 

The response of this endpoint service request contains the `Task<Models.ICGBusinessEntitiesProspectMessage>` that will returns the message which is sent and saved.

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|



#### Response Body
```markdown
 {
  "ProspectId": null,
  "FromUserName": null,
  "ToUserName": null,
  "Message": null
}
```
  
The class name of the **Task<Models.ICGBusinessEntitiesProspectMessage>** object is 
```markdown
      ICGBusinessEntitiesProspectMessage
```

#### Task<Models.ICGBusinessEntitiesProspectMessage>object parameters
  
![40](https://user-images.githubusercontent.com/110983629/190449551-755856f3-5a56-4afb-acac-6495aeb299ff.png)



### Prospect Messages Get Prospect Users
#### Description
This service endpoint will provide facility to retrieve all users that are associated with a prospect by accessing them through the prospect id. For this purpose, an instance of `ProspectMessagesController` class is created by the API client for invoking the `ProspectMessagesGetProspectUsersAsync` method.

```markdown
  ProspectMessagesGetProspectUsersAsync(
    int prospectId)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int prospectId = 118;
try
{
    ICGBusinessEntitiesProspectUser result = await prospectMessagesController.ProspectMessagesGetProspectUsersAsync(prospectId);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectMessagesController" object fails to retrieve all users that was anticipated to be returned. The prospectId will be passed as parameter to `ProspectMessagesGetProspectUsersAsync` method for accessing specific users which are associated with the specific prospect. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.


#### Parameters Detail      
This endpoint requires only one parameter which is **prospectId** (int type) for retrieving all users.
   
![41](https://user-images.githubusercontent.com/110983629/190452907-f836b076-a93e-4f7c-ac89-8f346312563d.png)
 

#### Responses 

The response of this endpoint service request contains the `Task<Models.ICGBusinessEntitiesProspectUser>` that will returns the users who are associated with the prospect.

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|



#### Response Body
```markdown
 {
  "Id": null,
  "ProspectId": null,
  "UserName": null
}
```
  
The class name of the **Task<Models.ICGBusinessEntitiesProspectUser>** object is 
```markdown
  ICGBusinessEntitiesProspectUser
```

#### Task<Models.ICGBusinessEntitiesProspectUser> object parameters
   
![42](https://user-images.githubusercontent.com/110983629/190453598-50145b52-e8d9-48b2-998e-ec76014a282d.png)





## API Endpoints
## Prospect Ofac Search
### Prospect Ofac Search Search Ofac
#### Description
This service endpoint will allow the user to search Ofac for prospect by entering the prospect id. In accordance with US foreign policy and national security objectives, the Office of Foreign Assets Control ("OFAC") of the US Department of the Treasury administers and enforces economic and trade sanctions against specific foreign nations and regimes, terrorists, global drug traffickers, individuals involved in the proliferation of WMD, as well as other threats to US national security, foreign policy, or economy. Through this Ofac, we review the merchant's background.
You can retrieve results by entering the prospect id which is a unique identifier for each prospect. For this purpose, an instance of `ProspectOfacSearchController` class is created by the API client for invoking the `ProspectOfacSearchSearchOfacAsync` method.

```markdown
  ProspectOfacSearchController prospectOfacSearchController = client.ProspectOfacSearchController;
```

```markdown
 ProspectOfacSearchSearchOfacAsync(
    int prospectId)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int prospectId = 118;
try
{
    object result = await prospectOfacSearchController.ProspectOfacSearchSearchOfacAsync(prospectId);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectOfacSearchController" object fails to get search results of Ofac that was anticipated to be returned. The prospectId will be passed as parameter to `ProspectOfacSearchSearchOfacAsync` method for getting the respective Ofac of the specific prospect. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.


#### Parameters Detail     
This endpoint requires only one parameter which is **prospectId** (int type) for retrieving the Ofac detail.

![36](https://user-images.githubusercontent.com/110983629/190445193-037f2977-3443-47fb-9477-90bd640d30dc.png)


#### Responses 

The response of this endpoint service request contains the `Task<object>` that will returns the Ofac details to the user.

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|


 




### Prospect Ofac Search Get Ofac Result
#### Description
This service endpoint will allow the user to get Ofac result by entering the prospect id for merchants. You can retrieve results by entering the prospect id which is a unique identifier for each prospect. For this purpose, an instance of `ProspectOfacSearchController` class is created by the API client for invoking the `ProspectOfacSearchGetOfacResultAsync` method.

```markdown
  ProspectOfacSearchGetOfacResultAsync(
    int prospectId)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int prospectId = 118;
try
{
    object result = await prospectOfacSearchController.ProspectOfacSearchGetOfacResultAsync(prospectId);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectOfacSearchController" object fails to get Ofac result that was anticipated to be returned. The prospectId will be passed as parameter to `ProspectOfacSearchSearchOfacAsync` method for getting the respective Ofac result of the specific prospect. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.


#### Parameters Detail     
This endpoint requires only one parameter which is **prospectId** (int type) for retrieving the Ofac result.

![36](https://user-images.githubusercontent.com/110983629/190445193-037f2977-3443-47fb-9477-90bd640d30dc.png)


#### Responses 

The response of this endpoint service request contains the `Task<object>` that will returns the Ofac results to the user.

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|






### Prospect Ofac Search Add Ofac Search Result
#### Description 
To track and monitor the list of merchants whose Ofac search results are recorded, the user will be able to add Ofac search results using this API endpoint. Its main objective is to look into and evaluate the merchant's record. The API client creates an instance of the "ProspectOfacSearchController" class for this purpose and calls the "ProspectOfacSearchAddOfacSearchResultAsync" function.

```markdown
 ProspectOfacSearchAddOfacSearchResultAsync(
    int prospectId,
    string name,
    int minScore,
    DateTime requestDate,
    int searchTypeId,
    int? principalOwnerId = null)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int prospectId = 118;
string name = "name0";
int minScore = 242;
DateTime requestDate = DateTime.Parse("2016-03-13T12:52:32.123Z");
int searchTypeId = 36;
try
{
    ICGBusinessEntitiesProspectOfacSearchResult result = await prospectOfacSearchController.ProspectOfacSearchAddOfacSearchResultAsync(prospectId, name, minScore, requestDate, searchTypeId, null);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectOfacSearchController" object fails to add Ofac search result that was anticipated to be returned. The prospectId, name, minScore, date and search type will be passed as parameters to `ProspectOfacSearchAddOfacSearchResultAsync` method for adding Ofac search result of the specific prospect. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.


#### Parameters Detail  
This endpoint requires six parameters which includes **prospectId** (int type), **name** (String Type), **minScore** (int type), **requestDate** (DateTime type), **searchTypeId** (int type), and **principalOwnerId** (int type). Where the principalOwnerId is optional to add for adding the Ofac search results.
 
![43](https://user-images.githubusercontent.com/110983629/190645281-adc5600f-24ab-45ba-b8c2-cb391b90af67.png)

 
#### Responses 

The response of this endpoint service request contains the `Task<Models.ICGBusinessEntitiesProspectOfacSearchResult>` that will returns the Ofac search results added into the system. 

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|


#### Response Body
```markdown
 {
  "Id": null,
  "ProspectId": null,
  "ProspectOfacSearchTypeId": null,
  "PrincipalOwnerId": null,
  "UserName": null,
  "RequestDate": null,
  "RequestBody": null,
  "ResponseBody": null,
  "HasRecordFound": null,
  "ProspectOfacResultList": null
}
```
  
The class name of the **Task<Models.ICGBusinessEntitiesProspectOfacSearchResult>** object is 
```markdown
    ICGBusinessEntitiesProspectOfacSearchResult  
```

#### Task<Models.ICGBusinessEntitiesProspectOfacSearchResult> object parameters
  
![44](https://user-images.githubusercontent.com/110983629/190645844-6c77e64b-9817-476f-8db2-a159e855df39.png)

  
#### ProspectOfacResultList object class name and parameters
    
![45](https://user-images.githubusercontent.com/110983629/190646144-4aab9d66-0de2-4ba3-b441-49f2c69b2760.png)
  

#### Explorer 

|Names|Description|
|-----|-----------|
|Response Type|[Task<Models.ICGBusinessEntitiesProspectOfacSearchResult>](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-business-entities-prospect-ofac-search-result)|
 


## API Endpoints
## Prospect Plaid Email
### Prospect Plaid Get Prospect Emails for Plaid Email
#### Description 
This service endpoint will allow the user to retrieve the data in order to create the Plaid Registration Email. Through this, you can get prospect emails for plaid emails which enables you to connect your financial accounts securely with the apps you want to use frequently. For this purpose, an instance of `ProspectPlaidEmailController` class is created by the API client for calling the `ProspectPlaidGetProspectEmailsForPlaidEmailAsync` method.

```markdown
   ProspectPlaidEmailController prospectPlaidEmailController = client.ProspectPlaidEmailController;
```

```markdown
  ProspectPlaidGetProspectEmailsForPlaidEmailAsync(
    int prospectId)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int prospectId = 118;
try
{
    object result = await prospectPlaidEmailController.ProspectPlaidGetProspectEmailsForPlaidEmailAsync(prospectId);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectPlaidEmailController" object fails to get prospect emails that was anticipated to be returned. The prospectId will be passed as parameter to `ProspectPlaidGetProspectEmailsForPlaidEmailAsync` method for getting all the email of the respective prospect. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes. 
 

#### Parameters Detail     
This endpoint requires only one parameter which is **prospectId** (int type) for retrieving the prospect emails.
 
![46](https://user-images.githubusercontent.com/110983629/190649723-96690664-02fd-4043-ab2f-f54ae3d87364.png)
 

#### Responses 

The response of this endpoint service request contains the `Task<object>` that will returns the prospect emails data to create plaid email.

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|



### Prospect Plaid Send Prospect Plaid Email
#### Description 
This service endpoint will allow the user to send prospect pliad emails to the users who got registered for plaid emails. Through this, you can process to save and send the plaid emails with the Url. For this purpose, an instance of `ProspectPlaidEmailController` class is created by the API client for calling the `ProspectPlaidSendProspectPlaidEmailAsync` method.

```markdown
   ProspectPlaidSendProspectPlaidEmailAsync(
    int prospectId,
    Models.ICGBusinessEntitiesProspectPlaidRegistrationEmailToSend email)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int prospectId = 118;
var email = new ICGBusinessEntitiesProspectPlaidRegistrationEmailToSend();

try
{
    object result = await prospectPlaidEmailController.ProspectPlaidSendProspectPlaidEmailAsync(prospectId, email);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectPlaidEmailController" object fails to send prospect plaid emails that was anticipated to be returned. The **email** object is created which is of `ICGBusinessEntitiesProspectPlaidRegistrationEmailToSend` type and passed as parameter to `ProspectPlaidSendProspectPlaidEmailAsync` method along with the prospect id in order to send pliad emails. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes. 
 

#### Parameters Detail     
This endpoint requires two parameter which includes **prospectId** (int type) and **email** object that further contains the list of recipient's emails for sending plaid emails.
  
![47](https://user-images.githubusercontent.com/110983629/190653383-b5affb29-ab82-469e-8197-f577ee9a7dc3.png)

The class name of **email** object is 
```markdown
   ICGBusinessEntitiesProspectPlaidRegistrationEmailToSend
```


#### email object parameters

![48](https://user-images.githubusercontent.com/110983629/190653677-3fd6b3c1-04a9-448c-b8d3-71e219ba74a8.png)

#### Responses 

The response of this endpoint service request contains the `Task<object>` that will returns the value for sent prospect plaid emails.

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|






### Prospect Plaid Validate Email Token
#### Description 
This service endpoint will allow the user to validate the email token that is used for sending the plaid emails. It is an anonymous method that verifies if the token is valid or not. To acquire that, an instance of `ProspectPlaidEmailController` class is created by the API client for calling the `ProspectPlaidValidateEmailTokenAsync` method.

```markdown
   ProspectPlaidValidateEmailTokenAsync(
    Models.ICGAPIUnderwritingWebAPIModelsPlaidEmailTokenVerification verificationToken)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
var verificationToken = new ICGAPIUnderwritingWebAPIModelsPlaidEmailTokenVerification();
try
{
    object result = await prospectPlaidEmailController.ProspectPlaidValidateEmailTokenAsync(verificationToken);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectPlaidEmailController" object fails to validate the email token that was anticipated to be returned. The **verificationToken** object is created which is of `ICGAPIUnderwritingWebAPIModelsPlaidEmailTokenVerification` type and passed as parameter to `ProspectPlaidValidateEmailTokenAsync` method in order to verify plaid email token. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes. 
 

#### Parameters Detail     
This endpoint requires only one parameter which is **verificationToken** object that further contains the token of string type.
  
![49](https://user-images.githubusercontent.com/110983629/190657668-3dedfb41-956f-46c5-8bd2-f010b4b5060e.png)

 
The class name of **verificationToken** object is 
```markdown
   ICGAPIUnderwritingWebAPIModelsPlaidEmailTokenVerification
```
 
#### Responses 

The response of this endpoint service request contains the `Task<object>` that will returns the value whether the email token get verified or not.

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|







### Prospect Plaid Create Link Token
#### Description 
This service endpoint will allow the user to create the link token for plaid. It is an anonymous method that enables you to securely connect financial accounts with the apps. To acquire that, an instance of `ProspectPlaidEmailController` class is created by the API client for calling the `ProspectPlaidCreateLinkTokenAsync` method.

```markdown
   ProspectPlaidCreateLinkTokenAsync(
    Models.ICGAPIUnderwritingWebAPIModelsPlaidCreateLinkToken data)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
var data = new ICGAPIUnderwritingWebAPIModelsPlaidCreateLinkToken();
try
{
    object result = await prospectPlaidEmailController.ProspectPlaidCreateLinkTokenAsync(data);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectPlaidEmailController" object fails to create link token that was anticipated to be returned. The **data** object is created which is of `ICGAPIUnderwritingWebAPIModelsPlaidCreateLinkToken` type and passed as parameter to `ProspectPlaidCreateLinkTokenAsync` method in order to create token anonymously. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes. 
 

#### Parameters Detail     
This endpoint requires only one parameter which is **data** object that further contains the user id of string type.
  
  
![50](https://user-images.githubusercontent.com/110983629/190661835-86998aab-76da-439e-ad75-d06638431863.png)

 
The class name of **data** object is 
```markdown
    ICGAPIUnderwritingWebAPIModelsPlaidCreateLinkToken
```
 
#### Responses 

The response of this endpoint service request contains the `Task<object>` that will returns the value whether the token link created or not.

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|






### Prospect Plaid Public Token Exchange
#### Description 
This service endpoint will allow the user to exchange the link token for plaid. It is an anonymous method that helps you to securely connect financial accounts with the apps. To acquire that, an instance of `ProspectPlaidEmailController` class is created by the API client for calling the `ProspectPlaidPublicTokenExchangeAsync` method.

```markdown 
ProspectPlaidPublicTokenExchangeAsync(
    Models.ICGEntitiesPlaidPublicTokenExchange data)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
var data = new ICGEntitiesPlaidPublicTokenExchange();
try
{
    object result = await prospectPlaidEmailController.ProspectPlaidPublicTokenExchangeAsync(data);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectPlaidEmailController" object fails to exchange link token that was anticipated to be returned. The **data** object is created which is of `ICGEntitiesPlaidPublicTokenExchange` type and passed as parameter to `ProspectPlaidPublicTokenExchangeAsync` method in order to successfully exchange token anonymously. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes. 
 

#### Parameters Detail     
This endpoint requires only one parameter which is **data** object that further contains the EmailToken, PublicToken, AccountId, AccountMask, AccountName, 
AccountSubType, AccountType, IntitutionId, InstitutionName, and LinkSessionId where all of these are of string type.
   
![51](https://user-images.githubusercontent.com/110983629/190665189-2404e074-6f75-4931-93d6-c05c4f8defff.png)

 
The class name of **data** object is 
```markdown
     ICGEntitiesPlaidPublicTokenExchange
```
 
#### Explorer 

|Names|Description|
|-----|-----------|
|data|[Models.ICGEntitiesPlaidPublicTokenExchange](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-entities-plaid-public-token-exchange)|
  
 
 
#### Responses 

The response of this endpoint service request contains the `Task<object>` that will returns the value whether the token link get exchanged or not.

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|









## API Endpoints
## Prospect Scores
### Prospect Scores Get Prospect Scores 
#### Description 
This service endpoint will allow the user to retrieve prospect scores details including prospect categories and scores categories by entering the prospect id. To acquire that, an instance of `ProspectScoresController` class is created by the API client for calling the `ProspectScoresGetProspectScoresAsync` method.


```markdown 
 ProspectScoresController prospectScoresController = client.ProspectScoresController;
```

```markdown 
 ProspectScoresGetProspectScoresAsync(int prospectId)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int prospectId = 118;
try
{
    ICGBusinessEntitiesProspectScoresCategories result = await prospectScoresController.ProspectScoresGetProspectScoresAsync(prospectId);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectScoresController" object fails to get prospect scores that was anticipated to be returned. The prospect id will be passed as parameter to `ProspectScoresGetProspectScoresAsync` method in order to successfully retrieve scores of the specific prospect. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  
 

#### Parameters Detail      
This endpoint requires only one parameter **prospectId** which is unique for each prospect for getting scores details.

![52](https://user-images.githubusercontent.com/110983629/190669605-92ff8676-6918-4f30-9cc3-73f7d360436f.png)

 
#### Responses 
The response of this endpoint service request contains the `Task<Models.ICGBusinessEntitiesProspectScoresCategories>` that further contains **ProspectScoreCategories** and **ScoreCategories** objects.

The class name of the **Task<Models.ICGBusinessEntitiesProspectScoresCategories>** object is
```markdown
   ICGBusinessEntitiesProspectScoresCategories
```

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|


#### Response Body
```markdown
 {
  "ProspectScoreCategories": null,
  "ScoreCategories": null
}
```


#### Explorer 

|Names|Description|
|-----|-----------|
|Response Type|[Task<Models.ICGBusinessEntitiesProspectScoresCategories>](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-business-entities-prospect-scores-categories)|

  



### Prospect Scores Set Prospect Score
#### Description 
This service endpoint will allow the user to set prospect score value by accessing the specific score category of the prospect through the prospect id and score category id. To acquire that, an instance of `ProspectScoresController` class is created by the API client for calling the `ProspectScoresSetProspectScoreAsync` method.
 
```markdown 
 ProspectScoresGetProspectScoresAsync(int prospectId)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int prospectId = 118;
int scoreCategoryId = 16;
var score = new ICGBusinessEntitiesProspectScoreCategory();

try
{
    ICGBusinessEntitiesProspectScoreCategory result = await prospectScoresController.ProspectScoresSetProspectScoreAsync(prospectId, scoreCategoryId, score);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectScoresController" object fails to set prospect scores that was anticipated to be returned. The prospect id and score category id will be passed as parameter to `ProspectScoresSetProspectScoreAsync` method in order to successfully define the score of the specific prospect. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  
 

#### Parameters Detail      
 
This endpoint requires three parameters which includes **prospectId** (int type), **scoreCategoryId** (int type) and **score** object. The score object further contains the Id, prospectId, ScoreCategoryId and Score parameters of int type. And it is essential to add all parameter's value for defining the score of the specific category of prospect.
 
![53](https://user-images.githubusercontent.com/110983629/190675211-07e6a541-abaf-4f49-b3ad-ead9f3c93211.png)

#### Score object class name and parameters

![54](https://user-images.githubusercontent.com/110983629/190675475-17ec6ca6-51f6-419b-aed9-3d3c75f82ca7.png)


 
#### Responses 
The response of this endpoint service request contains the `Task<Models.ICGBusinessEntitiesProspectScoreCategory>` that returns the value which is defind for the score. 


The class name of the **Task<Models.ICGBusinessEntitiesProspectScoreCategory>** object is
```markdown
    ICGBusinessEntitiesProspectScoreCategory
```

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|


#### Response Body
```markdown
 {
  "Id": null,
  "ProspectId": null,
  "ScoreCategoryId": null,
  "Score": null
}
```


#### Explorer 

|Names|Description|
|-----|-----------|
|Response Type|[Task<Models.ICGBusinessEntitiesProspectScoreCategory>](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-business-entities-prospect-score-category)|






### Prospect Scores Get Prospect Score Comments
#### Description 
This service endpoint will allow the user to retrieve the prospect Scores Category comments by accessing the specific score category of the prospect through the prospect id and score category id. To acquire that, an instance of `ProspectScoresController` class is created by the API client for calling the `ProspectScoresGetProspectScoreCommentsAsync` method.
 
```markdown 
 ProspectScoresGetProspectScoreCommentsAsync(
    int prospectId,
    int scoreCategoryId)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int prospectId = 118;
int scoreCategoryId = 16;
try
{
    ICGBusinessEntitiesProspectScoreCategoryComment result = await prospectScoresController.ProspectScoresGetProspectScoreCommentsAsync(prospectId, scoreCategoryId);
}
catch (ApiException e){};
 
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectScoresController" object fails to retrieve the comments that was anticipated to be returned. The prospect id and score category id will be passed as parameter to `ProspectScoresGetProspectScoreCommentsAsync` method in order to successfully retrieve the comments of the specific prospect score category. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  
 

#### Parameters Detail      
 
This endpoint requires two parameters which includes **prospectId** (int type), **scoreCategoryId** (int type) for accessing the comments of the score category of specific prospect.
 
![55](https://user-images.githubusercontent.com/110983629/190679328-5ea02c0b-d462-4a5d-8841-d85c5bbc938b.png)
 
 
#### Responses 
The response of this endpoint service request contains the `Task<Models.ICGBusinessEntitiesProspectScoreCategoryComment>` that returns the detail of the comments.


The class name of the **Task<Models.ICGBusinessEntitiesProspectScoreCategoryComment>** object is
```markdown
     ICGBusinessEntitiesProspectScoreCategoryComment
```

![56](https://user-images.githubusercontent.com/110983629/190680343-edb9031d-531a-47a1-a150-2fc6927afd5f.png)


#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|


#### Response Body
```markdown
 {
  "Id": null,
  "ProspectScoreCategoryId": null,
  "UserName": null,
  "Comment": null,
  "CreationUTCDate": null
}
```

#### Explorer 

|Names|Description|
|-----|-----------|
|Response Type|[Task<Models.ICGBusinessEntitiesProspectScoreCategoryComment>](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-business-entities-prospect-score-category-comment)|






### Prospect Scores Create Prospect Score Comment
#### Description 
This service endpoint will allow the user to create the prospect Scores Category comment by accessing the specific score category of the prospect through the prospect id and score category id. To acquire that, an instance of `ProspectScoresController` class is created by the API client for calling the `ProspectScoresCreateProspectScoreCommentAsync` method.
 
```markdown 
 ProspectScoresCreateProspectScoreCommentAsync(
    int prospectId,
    int scoreCategoryId,
    Models.ICGBusinessEntitiesProspectScoreCategoryComment comment)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int prospectId = 118;
int scoreCategoryId = 16;
var comment = new ICGBusinessEntitiesProspectScoreCategoryComment();

try
{
    ICGBusinessEntitiesProspectScoreCategoryComment result = await prospectScoresController.ProspectScoresCreateProspectScoreCommentAsync(prospectId, scoreCategoryId, comment);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectScoresController" object fails to add new comment for the prospect score category that was anticipated to be returned. The prospect id, score category id and comment object will be passed as parameter to `ProspectScoresCreateProspectScoreCommentAsync` method in order to successfully retrieve the comments of the specific prospect score category. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  
 

#### Parameters Detail      
 
This endpoint requires three required parameters which includes **prospectId** (int type), **scoreCategoryId** (int type) and **comment** object. The comment object further contains the id, ProspectScoreCategoryId, UserName, Comment, and CreationUTCDate in order to add new comment for the score category of specific prospect.
  
![57](https://user-images.githubusercontent.com/110983629/190684826-ecd1c680-aedf-40f6-8f39-247e31500991.png)


The class name of **comment** object is

```markdown
   ICGBusinessEntitiesProspectScoreCategoryComment
```

#### comment object parameters

![58](https://user-images.githubusercontent.com/110983629/190685150-64e047de-9bb0-4be4-8f1e-2c0e3da3c92b.png)

  
  
#### Responses 
The response of this endpoint service request contains the `Task<Models.ICGBusinessEntitiesProspectScoreCategoryComment>` that returns the detail of comment which needs to be added for the prospect score category.


The class name of the **Task<Models.ICGBusinessEntitiesProspectScoreCategoryComment>** object is
```markdown
    ICGBusinessEntitiesProspectScoreCategoryComment
```
 

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|


#### Response Body
```markdown
 {
  "Id": null,
  "ProspectScoreCategoryId": null,
  "UserName": null,
  "Comment": null,
  "CreationUTCDate": null
}
```

#### Explorer 

|Names|Description|
|-----|-----------|
|Response Type|[Task<Models.ICGBusinessEntitiesProspectScoreCategoryComment>](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-business-entities-prospect-score-category-comment)|










### Prospect Scores Run Score Manual Tools
#### Description 
This service endpoint will allow the user to run the score manual tools which select the categories for all the users. To acquire that, an instance of `ProspectScoresController` class is created by the API client for calling the `ProspectScoresRunScoreManualToolsAsync` method.
 
```markdown 
  ProspectScoresRunScoreManualToolsAsync(
    int prospectId,
    Models.ICGBusinessEntitiesProspectScoreRunToolsRequest categories)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int prospectId = 118;
var categories = new ICGBusinessEntitiesProspectScoreRunToolsRequest();
categories.ScoreCategoryIds = new List<int>();
categories.ScoreCategoryIds.Add(41);
categories.ScoreCategoryIds.Add(42);
try
{
    ICGBusinessEntitiesProspectScoreCategoryComment result = await prospectScoresController.ProspectScoresRunScoreManualToolsAsync(prospectId, categories);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectScoresController" object fails to add score categories for the prospect that was anticipated to be returned. The **categories** object is created which will be of `ICGBusinessEntitiesProspectScoreRunToolsRequest` type. And passed as parameter to `ProspectScoresRunScoreManualToolsAsync` method in order to insert the score categories to run the tools. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  
 

#### Parameters Detail      
 
This endpoint includes two required parameters that are **prospectId** (int type), **categories** object. The categories object further contains the list of categories along with the user id in order to run the tools. The respective prospect whose id is entered should be on status in review.
 
![59](https://user-images.githubusercontent.com/110983629/190847623-734c4473-7a86-4ef7-8a77-298bfa0adfa9.png)


The class name of **categories** object is

```markdown
    ICGBusinessEntitiesProspectScoreRunToolsRequest
```

#### categories object parameters
 
 ![60](https://user-images.githubusercontent.com/110983629/190847657-551d80ae-1a54-49f8-8f55-15f28076333d.png)

   
#### Responses 
The response of this endpoint service request contains the `Task<Models.ICGBusinessEntitiesProspectScoreCategoryComment>` that returns the detail of categories along with the user id which needs to be save for the running the tools.

The class name of the **Task<Models.ICGBusinessEntitiesProspectScoreCategoryComment>** object is
```markdown
     ICGBusinessEntitiesProspectScoreCategoryComment
```
 

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|


#### Response Body
```markdown
 {
  "Id": null,
  "ProspectScoreCategoryId": null,
  "UserName": null,
  "Comment": null,
  "CreationUTCDate": null
}
```

#### Explorer 

|Names|Description|
|-----|-----------|
|Response Type|[Task<Models.ICGBusinessEntitiesProspectScoreCategoryComment>](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-business-entities-prospect-score-category-comment)|







## API Endpoints
## Prospect Scores Average Bank Balance
### Prospect Scores Average Bank Balance Get Prospect Average Bank Balance Score
#### Description 
This service endpoint will allow the user to retrieve the average bank balance score for the automatic or manual set of scores by entering the prospect id. To acquire that, an instance of `ProspectScoresAverageBankBalanceController` class is created by the API client for calling the `ProspectScoresAverageBankBalanceGetProspectAverageBankBalanceScoreAsync` method.


```markdown  
   ProspectScoresAverageBankBalanceController prospectScoresAverageBankBalanceController = client.ProspectScoresAverageBankBalanceController;
```

```markdown 
  ProspectScoresAverageBankBalanceGetProspectAverageBankBalanceScoreAsync(
    int prospectId)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int prospectId = 118;
try
{
    object result = await prospectScoresAverageBankBalanceController.ProspectScoresAverageBankBalanceGetProspectAverageBankBalanceScoreAsync(prospectId);
}
catch (ApiException e){};
 
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectScoresAverageBankBalanceController" object fails to get average bank balance scores that was anticipated to be returned. The prospect id will be passed as parameter to `ProspectScoresAverageBankBalanceGetProspectAverageBankBalanceScoreAsync` method in order to successfully retrieve bank balance score values of the specific prospect. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  
 

#### Parameters Detail      
This endpoint requires only one parameter **prospectId** which is unique for each prospect for getting avergae bank balance scores details.


![61](https://user-images.githubusercontent.com/110983629/190848507-b608be2d-a9f7-4cf0-b4a1-35af9a9aadda.png)

 
#### Responses 
The response of this endpoint service request contains the `Task<object>` that returns the values for average bank balance score that are added automatically or manually. 

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|




### Prospect Scores Average Bank Balance Recalculate Prospect Score Average Bank Balance
#### Description 
This service endpoint will allow the user to recalculate the average bank balance score by entering the prospect id in order to get the new score. To acquire that, an instance of `ProspectScoresAverageBankBalanceController` class is created by the API client for calling the `ProspectScoresAverageBankBalanceRecalculateProspectScoreAverageBankBalanceAsync` method.


```markdown 
 ProspectScoresAverageBankBalanceRecalculateProspectScoreAverageBankBalanceAsync(
    int prospectId)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int prospectId = 118;
try
{
    ICGBusinessEntitiesProspectScoreTaxIdQuery result = await prospectScoresAverageBankBalanceController.ProspectScoresAverageBankBalanceRecalculateProspectScoreAverageBankBalanceAsync(prospectId);
}
catch (ApiException e){};
 
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectScoresAverageBankBalanceController" object fails to recalculate average bank balance scores that was anticipated to be returned. The prospect id will be passed as parameter to `ProspectScoresAverageBankBalanceRecalculateProspectScoreAverageBankBalanceAsync` method in order to successfully retrieve bank balance score values which are recalculated. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  
 

#### Parameters Detail      
This endpoint requires only one parameter **prospectId** which is unique for each prospect for getting avergae bank balance scores detail which is recalculated by the system.

![62](https://user-images.githubusercontent.com/110983629/190849533-95966ee2-5e81-4f6f-8735-c2c0c1a0a70a.png)

 
#### Responses 
The response of this endpoint service request contains the `Task<Models.ICGBusinessEntitiesProspectScoreTaxIdQuery>` that returns the values for average bank balance score in order to review the recalculated scores. 

The class name of the **Task<Models.ICGBusinessEntitiesProspectScoreTaxIdQuery>** object is
```markdown
   ICGBusinessEntitiesProspectScoreTaxIdQuery
```


![63](https://user-images.githubusercontent.com/110983629/190849679-b9662e5e-d9aa-46a1-b680-b9541869bb24.png)


#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|


#### Response Body
```markdown
{
  "ProspectScoreCategory": null,
  "ProspectScoreTaxIdQueryValidation": null,
  "ProspectScoreTaxIdQueryScores": null,
  "Id": null,
  "ProspectScoreCategoryId": null,
  "ScoreTaxIdQueryResultId": null,
  "Tin": null,
  "LegalName": null,
  "Street1": null,
  "Street2": null,
  "City": null,
  "State": null,
  "ZipCode": null,
  "UserName": null,
  "CreatedUtcDate": null
}
```

#### Explorer 

|Names|Description|
|-----|-----------|
|Response Type|[Task<Models.ICGBusinessEntitiesProspectScoreTaxIdQuery>](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-business-entities-prospect-score-tax-id-query)|








### Prospect Scores Average Bank Balance Save Manual Prospect Score Average Bank Balance
#### Description 
This service endpoint will allow the user to save Manual Prospect Score by entering the tax id in order to update the bank balance average score. To acquire that, an instance of `ProspectScoresAverageBankBalanceController` class is created by the API client for calling the `ProspectScoresAverageBankBalanceSaveManualProspectScoreAverageBankBalanceAsync` method.


```markdown 
 ProspectScoresAverageBankBalanceSaveManualProspectScoreAverageBankBalanceAsync(
    int prospectId,
    Models.ICGBusinessEntitiesProspectScoreAverageBankBalanceResultManualUpdate scoreManualUpdate)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int prospectId = 118;
var scoreManualUpdate = new ICGBusinessEntitiesProspectScoreAverageBankBalanceResultManualUpdate();
try
{
    ICGBusinessEntitiesProspectScoreAverageBankBalanceResult result = await prospectScoresAverageBankBalanceController.ProspectScoresAverageBankBalanceSaveManualProspectScoreAverageBankBalanceAsync(prospectId, scoreManualUpdate);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectScoresAverageBankBalanceController" object fails to update average bank balance score that was anticipated to be returned. The prospect id and scoreManualUpdate object will be passed as parameters to `ProspectScoresAverageBankBalanceSaveManualProspectScoreAverageBankBalanceAsync` method to update the score manually. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  
 

#### Parameters Detail       
This endpoint requires two parameters **prospectId** (int type) and **scoreManualUpdate**  object. The scoreManualUpdate will further contain score and comment for updating the score manually of the specific prospect. 
 
 
![64](https://user-images.githubusercontent.com/110983629/190850262-2af88981-e241-4353-ac97-cc352294b33b.png)

The class name of the **scoreManualUpdate** object is
```markdown
ICGBusinessEntitiesProspectScoreAverageBankBalanceResultManualUpdate
```
 
 #### scoreManualUpdate parameters

 ![65](https://user-images.githubusercontent.com/110983629/190850335-0a7347aa-78fb-41dc-b0e7-d06f130e9fb3.png)

#### Explorer 

|Names|Description|
|-----|-----------|
|scoreManualUpdate|[Models.ICGBusinessEntitiesProspectScoreAverageBankBalanceResultManualUpdate](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-business-entities-prospect-score-average-bank-balance-result-manual-update)|

 
#### Responses 
The response of this endpoint service request contains the `Task<Models.ICGBusinessEntitiesProspectScoreAverageBankBalanceResult>` that returns the values for manually updating prospect score.

The class name of the **Task<Models.ICGBusinessEntitiesProspectScoreAverageBankBalanceResult>** object is
```markdown
    ICGBusinessEntitiesProspectScoreAverageBankBalanceResult
``` 
 

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|


#### Response Body
```markdown
 {
  "ProspectScoreCategory": null,
  "PlaidRequqest": null,
  "ProspectScoreAverageBankBalanceResultValues": null,
  "Id": null,
  "ProspectScoreCategoryId": null,
  "Score": null,
  "RequestedMaxSingle": null,
  "AverageBankAccountBalance": null,
  "PercentageBalanceToRequestedMaxSingle": null,
  "HasPlaidMerchantToken": null,
  "HasRunPlaidService": null
}
```

#### Explorer 

|Names|Description|
|-----|-----------|
|Response Type|[Task<Models.ICGBusinessEntitiesProspectScoreAverageBankBalanceResult>](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-business-entities-prospect-score-average-bank-balance-result)|





### Prospect Scores Average Bank Balance Save Manual Prospect Score Average Bank Balance Values
#### Description 
This service endpoint will allow the user to save Manual Prospect Score for the specific tax id in order to update the bank balance average score. To acquire that, an instance of `ProspectScoresAverageBankBalanceController` class is created by the API client for calling the `ProspectScoresAverageBankBalanceSaveManualProspectScoreAverageBankBalanceValuesAsync` method.


```markdown  
ProspectScoresAverageBankBalanceSaveManualProspectScoreAverageBankBalanceValuesAsync(
    int prospectId,
    Models.ICGBusinessEntitiesProspectScoreAverageBankBalanceResultValuesManualUpdate bankBalancesManualUpdate)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int prospectId = 118;
var bankBalancesManualUpdate = new ICGBusinessEntitiesProspectScoreAverageBankBalanceResultValuesManualUpdate();
try
{
    ICGBusinessEntitiesProspectScoreAverageBankBalanceResult result = await prospectScoresAverageBankBalanceController.ProspectScoresAverageBankBalanceSaveManualProspectScoreAverageBankBalanceValuesAsync(prospectId, bankBalancesManualUpdate);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectScoresAverageBankBalanceController" object fails to update average bank balance score that was anticipated to be returned. The prospect id and bankBalancesManualUpdate object will be passed as parameters to `ProspectScoresAverageBankBalanceSaveManualProspectScoreAverageBankBalanceValuesAsync` method to update the score. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  
 

#### Parameters Detail       
This endpoint requires two parameters **prospectId** (int type) and **bankBalancesManualUpdate**  object. The bankBalancesManualUpdate will further contain comment and ProspectScoreAverageBankBalanceResultValues object. The **ProspectScoreAverageBankBalanceResultValues** object includes the list of average bank balance result values.
 
![66](https://user-images.githubusercontent.com/110983629/190852368-dd4e839b-4f7a-436f-b53d-ad0b59f3aadb.png)

   
The class name of the **bankBalancesManualUpdate** object is
```markdown
 ICGBusinessEntitiesProspectScoreAverageBankBalanceResultValuesManualUpdate
```
 
 ####  bankBalancesManualUpdate parameters 
 
 ![67](https://user-images.githubusercontent.com/110983629/190852409-735a5292-56c0-4ac5-ad65-9ac92cba93e5.png)


####  ProspectScoreAverageBankBalanceResultValues object class name and parameters 

![68](https://user-images.githubusercontent.com/110983629/190852480-e9764687-a285-42e9-84a8-d23ee05821a7.png)


#### Explorer 

|Names|Description|
|-----|-----------|
|bankBalancesManualUpdate|[Models.ICGBusinessEntitiesProspectScoreAverageBankBalanceResultValuesManualUpdate](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-business-entities-prospect-score-average-bank-balance-result-values-manual-update)|

 
#### Responses 
The response of this endpoint service request contains the `Task<Models.ICGBusinessEntitiesProspectScoreAverageBankBalanceResult>` that returns the values for updating prospect average bank balance values.

The class name of the **Task<Models.ICGBusinessEntitiesProspectScoreAverageBankBalanceResult>** object is
```markdown
     ICGBusinessEntitiesProspectScoreAverageBankBalanceResult
``` 

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|


#### Response Body
```markdown
 {
  "ProspectScoreCategory": null,
  "PlaidRequqest": null,
  "ProspectScoreAverageBankBalanceResultValues": null,
  "Id": null,
  "ProspectScoreCategoryId": null,
  "Score": null,
  "RequestedMaxSingle": null,
  "AverageBankAccountBalance": null,
  "PercentageBalanceToRequestedMaxSingle": null,
  "HasPlaidMerchantToken": null,
  "HasRunPlaidService": null
}
```

#### Explorer 

|Names|Description|
|-----|-----------|
|Response Type|[Task<Models.ICGBusinessEntitiesProspectScoreAverageBankBalanceResult>](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-business-entities-prospect-score-average-bank-balance-result)|








## API Endpoints
## Prospect Scores Business Types
### Prospect Scores Business Type Get Prospect Business Type Score
#### Description 
This service endpoint will allow the user to retrieve the Business Type Score values for the automatic set of score for a prospect by entering the prospect id. To acquire that, an instance of `ProspectScoresBusinessTypesController` class is created by the API client for calling the `ProspectScoresBusinessTypeGetProspectBusinessTypeScoreAsync` method.


```markdown  
   ProspectScoresBusinessTypesController prospectScoresBusinessTypesController = client.ProspectScoresBusinessTypesController;
```

```markdown 
   ProspectScoresBusinessTypeGetProspectBusinessTypeScoreAsync(
    int prospectId)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int prospectId = 118;
try
{
    object result = await prospectScoresBusinessTypesController.ProspectScoresBusinessTypeGetProspectBusinessTypeScoreAsync(prospectId);
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectScoresBusinessTypesController" object fails to retrieve business type scores that was anticipated to be returned. The prospect id will be passed as parameter to `ProspectScoresBusinessTypeGetProspectBusinessTypeScoreAsync` method in order to successfully retrieve business type score values of the specific prospect. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  
 

#### Parameters Detail      
This endpoint requires only one parameter **prospectId** which is unique for each prospect in order to get automatic set of score values. 
 
![69](https://user-images.githubusercontent.com/110983629/190853161-de6647f4-fa8e-435b-b473-3e1302dbcbb8.png)

 
#### Responses 
The response of this endpoint service request contains the `Task<object>` that returns the values for set of scores of business type.

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|








### Prospect Scores Business Type Set Prospect Score Business Type
#### Description  
This service endpoint will allow the user to update a business type score by accessing it through the prospect id which is a unique identifier for the prospect. You can update the business type score only if it is restricted. To acquire that, an instance of `ProspectScoresBusinessTypesController` class is created by the API client for calling the `ProspectScoresBusinessTypeSetProspectScoreBusinessTypeAsync` method.

```markdown 
    ProspectScoresBusinessTypeSetProspectScoreBusinessTypeAsync(
    int prospectId,
    Models.ICGBusinessEntitiesProspectScoreCategory score)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int prospectId = 118;
var score = new ICGBusinessEntitiesProspectScoreCategory();
try
{
    ICGBusinessEntitiesProspectScoreCategory result = await prospectScoresBusinessTypesController.ProspectScoresBusinessTypeSetProspectScoreBusinessTypeAsync(prospectId, score);
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectScoresBusinessTypesController" object fails to update business type score that was anticipated to be returned. The prospect id and score object will be passed as parameter to `ProspectScoresBusinessTypeSetProspectScoreBusinessTypeAsync` method in order to successfully update business type score values of the specific prospect. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  
 

#### Parameters Detail      
This endpoint requires two parameters **prospectId** (int type) and **score** object which further contains Id, ProspectId, ScoreCategoryId, and Score of int type. 
  
![70](https://user-images.githubusercontent.com/110983629/190853791-6cf09595-b88c-4b24-bf52-7575f411c0a9.png)


The score object class name is
```markdown
     ICGBusinessEntitiesProspectScoreCategory
```


#### score object parameters

![71](https://user-images.githubusercontent.com/110983629/190853837-095e3820-63c7-42e2-912f-cbf42c4811f0.png)

 
#### Responses 
The response of this endpoint service request contains the `Task<Models.ICGBusinessEntitiesProspectScoreCategory>` that returns the values for set of scores of business type that gets updated.

The class name of the Task<Models.ICGBusinessEntitiesProspectScoreCategory> object is
```markdown
   ICGBusinessEntitiesProspectScoreCategory
```

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|


#### Response Body
```markdown
{
  "Id": null,
  "ProspectId": null,
  "ScoreCategoryId": null,
  "Score": null
}
```

#### Explorer 

|Names|Description|
|-----|-----------|
|Response Type|[Task<Models.ICGBusinessEntitiesProspectScoreCategory>](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-business-entities-prospect-score-category)|







### Prospect Scores Business Type Recalculate Prospect Score Business Type
#### Description  
This service endpoint will allow the user to recalculate prospect business type score by accessing it through the prospect id which is a unique identifier for the prospect. To acquire that, an instance of `ProspectScoresBusinessTypesController` class is created by the API client for calling the `ProspectScoresBusinessTypeRecalculateProspectScoreBusinessTypeAsync` method.

```markdown 
  ProspectScoresBusinessTypeRecalculateProspectScoreBusinessTypeAsync(
    int prospectId)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int prospectId = 118;
try
{
    ICGBusinessEntitiesProspectScoreCategory result = await prospectScoresBusinessTypesController.ProspectScoresBusinessTypeRecalculateProspectScoreBusinessTypeAsync(prospectId);
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectScoresBusinessTypesController" object fails to recalculate business type score that was anticipated to be returned. The prospect id and score object will be passed as parameter to `ProspectScoresBusinessTypeRecalculateProspectScoreBusinessTypeAsync` method in order to successfully provide business type score values of the specific prospect. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  
 

#### Parameters Detail      
This endpoint requires one parameter **prospectId** (int type) for recalculating scores.
   
![72](https://user-images.githubusercontent.com/110983629/190854533-54051a75-6049-4712-966b-a0c9a0ee1d44.png)

 
 
#### Responses 
The response of this endpoint service request contains the `Task<Models.ICGBusinessEntitiesProspectScoreCategory>` that returns the values for set of scores of business type that gets recalculated.

The class name of the Task<Models.ICGBusinessEntitiesProspectScoreCategory> object is
```markdown
    ICGBusinessEntitiesProspectScoreCategory
```

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|


#### Response Body
```markdown
 {
  "Id": null,
  "ProspectId": null,
  "ScoreCategoryId": null,
  "Score": null
}
```

#### Explorer 

|Names|Description|
|-----|-----------|
|Response Type|[Task<Models.ICGBusinessEntitiesProspectScoreCategory>](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-business-entities-prospect-score-category)|







### Prospect Scores Business Type Get Score Business Type Codes
#### Description  
This service endpoint will allow the user to retrieve the list of Descriptors that match the list of Code Pairs sent. To acquire that, an instance of `ProspectScoresBusinessTypesController` class is created by the API client for calling the `ProspectScoresBusinessTypeGetScoreBusinessTypeCodesAsync` method.

```markdown 
 ProspectScoresBusinessTypeGetScoreBusinessTypeCodesAsync(
    int scoreBusinessTypeCodeId)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int scoreBusinessTypeCodeId = 186;
try
{
    object result = await prospectScoresBusinessTypesController.ProspectScoresBusinessTypeGetScoreBusinessTypeCodesAsync(scoreBusinessTypeCodeId);
}
catch (ApiException e){};
```
If the "prospectScoresBusinessTypesController" object is unable to obtain the expected list of descriptors, it will be included in the try and catch block to handle any exceptions that may occur. In order to effectively return a list of descriptors that match with the code pairs, the scoreBusinessTypeCodeId will be supplied as a parameter to the 'ProspectScoresBusinessTypeGetScoreBusinessTypeCodesAsync' method. To avoid unhandled exceptions, user error, or application crashes, the try catch block will handle any exceptions that are thrown. 
 

#### Parameters Detail      
This endpoint requires one parameter **ScoreBusinessTypeCodeId** (int type) for showing the list of code pairs.
    
![73](https://user-images.githubusercontent.com/110983629/190999581-95c0ab03-b264-40ec-add8-4189bb977f8a.png)

 
#### Responses 
The response of this endpoint service request contains the `Task<object>` that returns the values for set of code pairs which are matched with the descriptors. 

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

 



### Prospect Scores Business Type Update Code Descriptor
#### Description   
This service endpoint will allow the user to update the code pair/descriptor from a given ProspectScoreBusinessTypeValue. As there are many code pairs, prospectScoreBusinessTypeValueId will be used which is a unique identifier for the prospect score business type values.
To acquire that, an instance of `ProspectScoresBusinessTypesController` class is created by the API client for calling the `ProspectScoresBusinessTypeUpdateCodeDescriptorAsync` method.

```markdown 
  ProspectScoresBusinessTypeUpdateCodeDescriptorAsync(
    int prospectScoreBusinessTypeValueId,
    Models.ICGBusinessEntitiesProspectScoreBusinessTypeValue prospectScoreBusinessTypeValue)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int prospectScoreBusinessTypeValueId = 0;
var prospectScoreBusinessTypeValue = new ICGBusinessEntitiesProspectScoreBusinessTypeValue();
try
{
    ICGBusinessEntitiesProspectScoreBusinessTypeValue result = await prospectScoresBusinessTypesController.ProspectScoresBusinessTypeUpdateCodeDescriptorAsync(prospectScoreBusinessTypeValueId, prospectScoreBusinessTypeValue);
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectScoresBusinessTypesController" object fails to update the code pairs that was anticipated to be returned. The prospectScoreBusinessTypeValueId and  prospectScoreBusinessTypeValue object will be passed as parameters to `ProspectScoresBusinessTypeUpdateCodeDescriptorAsync` method in order to successfully update business type score values of the specific prospect. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  
 

#### Parameters Detail      
This endpoint requires two parameters **prospectScoreBusinessTypeValueId** (int type) and **prospectScoreBusinessTypeValue** object that further contains the **ProspectScoreCategory** object, **ScoreBusinessTypeCodeDescriptor** object, Id (int type), **ProspectScoreCategoryId** (int type), **ScoreBusinessTypeCodeDescriptorId** (int type), **BusinessTypeValueResultId** (int type), **Score** (int type), **CreatedUtcDate** (DateTime type), **UserName** (string type).
  
![74](https://user-images.githubusercontent.com/110983629/191002122-57ec8056-86fd-4960-995f-89af5fbf353e.png)


#### prospectScoreBusinessTypeValue object parameters

![75](https://user-images.githubusercontent.com/110983629/191002343-e0422b40-7659-48b1-8454-2e9229330010.png)

The class name of prospectScoreBusinessTypeValue object is 

```markdown
   ICGBusinessEntitiesProspectScoreBusinessTypeValue
```

#### ProspectScoreCategory object class name and parameters
 
![76](https://user-images.githubusercontent.com/110983629/191002561-b5250986-3846-4242-ad3c-3a8ccb78e81a.png)

 
 
#### ScoreBusinessTypeCodeDescriptor object class name and parameters

![77](https://user-images.githubusercontent.com/110983629/191002694-e254835c-2c1c-4626-bed9-1d2b0055c731.png)


 
#### Responses 
The response of this endpoint service request contains the `Task<Models.ICGBusinessEntitiesProspectScoreBusinessTypeValue>` that returns the values for set of code pairs/descriptors of business type that gets updated.

The class name of the Task<Models.ICGBusinessEntitiesProspectScoreBusinessTypeValue> object is
```markdown
     ICGBusinessEntitiesProspectScoreBusinessTypeValue
```

![78](https://user-images.githubusercontent.com/110983629/191003204-b3d23e35-bc08-4b8e-b895-49942d85d62c.png)


#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|


#### Response Body
```markdown
 {
  "ProspectScoreCategory": null,
  "ScoreBusinessTypeCodeDescriptor": null,
  "Id": null,
  "ProspectScoreCategoryId": null,
  "ScoreBusinessTypeCodeDescriptorId": null,
  "BusinessTypeValueResultId": null,
  "Score": null,
  "CreatedUtcDate": null,
  "UserName": null
}
```

#### Explorer 

|Names|Description|
|-----|-----------|
|Response Type|[Task<Models.ICGBusinessEntitiesProspectScoreBusinessTypeValue>](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-business-entities-prospect-score-business-type-value)|






### Prospect Scores Business Type Add Descriptor to Code Pair
#### Description   
This service endpoint will allow the user to add a descriptor to the code pair. As there are many code pairs associated with the descriptors, ScoreBusinessTypeDescriptorId will be used which is a unique identifier for the descriptor business type values.
To acquire that, an instance of `ProspectScoresBusinessTypesController` class is created by the API client for calling the `ProspectScoresBusinessTypeAddDescriptorToCodePairAsync` method.

```markdown 
  ProspectScoresBusinessTypeAddDescriptorToCodePairAsync(
    Models.ICGBusinessEntitiesScoreBusinessTypeCodeDescriptor scoreBusinessTypeCodeDescriptor)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
var scoreBusinessTypeCodeDescriptor = new ICGBusinessEntitiesScoreBusinessTypeCodeDescriptor();
try
{
    object result = await prospectScoresBusinessTypesController.ProspectScoresBusinessTypeAddDescriptorToCodePairAsync(scoreBusinessTypeCodeDescriptor);
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectScoresBusinessTypesController" object fails to add descriptor to the code pair that was anticipated to be returned. The scoreBusinessTypeCodeDescriptor object will be passed as parameter to `ProspectScoresBusinessTypeAddDescriptorToCodePairAsync` method in order to successfully add descriptor. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  
 

#### Parameters Detail      
This endpoint requires one parameter which is **scoreBusinessTypeCodeDescriptor** object that further contains the **ScoreBusinessTypeCode** object, **ScoreBusinessTypeDescriptor** object, Id (int type), **ScoreBusinessTypeCodeId** (int type), and **ScoreBusinessTypeDescriptorId** (int type).
   
#### scoreBusinessTypeCodeDescriptor object parameters
 
![79](https://user-images.githubusercontent.com/110983629/191005827-6d562f6e-7f44-499b-9c0b-835ce5a2b742.png)

The class name of scoreBusinessTypeCodeDescriptor object is 

```markdown
    ICGBusinessEntitiesScoreBusinessTypeCodeDescriptor
```

#### ScoreBusinessTypeCode object class name and parameters
  
 ![80](https://user-images.githubusercontent.com/110983629/191006028-155847fc-ec0c-483f-ad4e-89bea236bbee.png)

 
#### ScoreBusinessTypeDescriptor object class name and parameters
 
![81](https://user-images.githubusercontent.com/110983629/191006082-aeae26af-7b8d-48df-9658-f2d9d50f8679.png)


 
#### Responses 
The response of this endpoint service request contains the `Task<object>` that returns the descriptor value which is added for the code pair. 

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

 

## API Endpoints
## Prospect Scores Equifax Owner Credit
### Prospect Scores Equifax Owner Credit Get Score Equifax Owner Credit Response
#### Description 
This service endpoint will allow the user to retrieve the list of owners that may contain the equifax score. This is due to the fact that there may be an owner that does not had equifax score. To acquire all the owners list, an instance of `ProspectScoresEquifaxOwnerCreditController` class is created by the API client for calling the `ProspectScoresEquifaxOwnerCreditGetScoreEquifaxOwnerCreditResponseAsync` method.


```markdown  
   ProspectScoresEquifaxOwnerCreditController prospectScoresEquifaxOwnerCreditController = client.ProspectScoresEquifaxOwnerCreditController;
```

```markdown  
  ProspectScoresEquifaxOwnerCreditGetScoreEquifaxOwnerCreditResponseAsync(
    int prospectId)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int prospectId = 118;
try
{
    object result = await prospectScoresEquifaxOwnerCreditController.ProspectScoresEquifaxOwnerCreditGetScoreEquifaxOwnerCreditResponseAsync(prospectId);
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectScoresEquifaxOwnerCreditController" object fails to retrieve owners list that was anticipated to be returned. The prospect id will be passed as parameter to `ProspectScoresEquifaxOwnerCreditGetScoreEquifaxOwnerCreditResponseAsync` method in order to successfully retrieve owners list of the specific prospect. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  
 

#### Parameters Detail      
This endpoint requires only one parameter **prospectId** which is unique for each prospect in order to get the list of owners that may be an equifax credit owner or not.
 
![82](https://user-images.githubusercontent.com/110983629/191008754-edc1ceb1-e652-444f-8d6c-9b98384c8c71.png)

 
#### Responses 
The response of this endpoint service request contains the `Task<object>` that returns the values for equifax credit owner.

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|







### Prospect Scores Equifax Owner Credit Save Score Equifax Owner Credit Response
#### Description 
This service endpoint will allow the user to save Equifax owner credit score by accessing the prospect through the prospect id. To acquire that, an instance of `ProspectScoresEquifaxOwnerCreditController` class is created by the API client for calling the `ProspectScoresEquifaxOwnerCreditSaveScoreEquifaxOwnerCreditResponseAsync` method.

```markdown  
  ProspectScoresEquifaxOwnerCreditSaveScoreEquifaxOwnerCreditResponseAsync(
    int prospectId,
    Models.ICGBusinessEntitiesProspectScoreEquifaxOwnerCreditResponse response)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int prospectId = 118;
var response = new ICGBusinessEntitiesProspectScoreEquifaxOwnerCreditResponse();
try
{
    ICGBusinessEntitiesProspectScoreEquifaxOwnerCreditResponse result = await prospectScoresEquifaxOwnerCreditController.ProspectScoresEquifaxOwnerCreditSaveScoreEquifaxOwnerCreditResponseAsync(prospectId, response);
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectScoresEquifaxOwnerCreditController" object fails to save equifax owner score that was anticipated to be returned. The prospect id and response object will be passed as parameters to `ProspectScoresEquifaxOwnerCreditSaveScoreEquifaxOwnerCreditResponseAsync` method in order to successfully save owner details of the specific prospect. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  
 

#### Parameters Detail      
This endpoint requires two parameters **prospectId** which is unique for each prospect and **response** object that further contains model, owner, ResponseValidator, ProspectDropboxFile objects, and Id (int type), UserId (int type), ResponseJsonBody (string type), CreateUtcDate (DateTime type), ModelId (int type), OwnerId (int type), ICGScore (int type), Recalculate (bool type), ProspectDropboxFileId (string type), ReportPDFLink (string type).
 
 
![83](https://user-images.githubusercontent.com/110983629/191011411-8df23c9c-fab3-4789-9e35-5621a40e19c2.png)

The class name of **response** object is
```markdown
   ICGBusinessEntitiesProspectScoreEquifaxOwnerCreditResponse
```

#### response object parameters

![84](https://user-images.githubusercontent.com/110983629/191011593-0f39af52-9f4d-4983-9dd6-f11570072e13.png)

 
 
 #### Explorer 

|Names|Description|
|-----|-----------|
|response|[Models.ICGBusinessEntitiesProspectScoreEquifaxOwnerCreditResponse](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-business-entities-prospect-score-equifax-owner-credit-response)|


 
#### Responses 
The response of this endpoint service request contains the `Task<Models.ICGBusinessEntitiesProspectScoreEquifaxOwnerCreditResponse>` that returns the value for saving Score Equifax Owner Credit Response details.

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

#### Response Body
```markdown
{
  "Model": null,
  "Owner": null,
  "ResponseValidator": null,
  "ProspectDropboxFile": null,
  "Id": null,
  "UserId": null,
  "ResponseJsonBody": null,
  "CreateUtcDate": null,
  "ModelId": null,
  "OwnerId": null,
  "ICGScore": null,
  "Recalculate": null,
  "ProspectDropboxFileId": null,
  "ReportPDFLink": null
}
```
The class name of **Task<Models.ICGBusinessEntitiesProspectScoreEquifaxOwnerCreditResponse>** object is
```markdown
    ICGBusinessEntitiesProspectScoreEquifaxOwnerCreditResponse
```

 #### Explorer 

|Names|Description|
|-----|-----------|
|response type|[Task<Models.ICGBusinessEntitiesProspectScoreEquifaxOwnerCreditResponse>](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-business-entities-prospect-score-equifax-owner-credit-response)|







### Prospect Scores Equifax Owner Credit Set All Score Equifax Owner Credit Response
#### Description 
This service endpoint will allow the user to calculate score for all the equifax owners credit by accessing the prospect through the prospect id. To acquire that, an instance of `ProspectScoresEquifaxOwnerCreditController` class is created by the API client for calling the `ProspectScoresEquifaxOwnerCreditSetAllScoreEquifaxOwnerCreditResponseAsync` method.

```markdown  
  ProspectScoresEquifaxOwnerCreditSetAllScoreEquifaxOwnerCreditResponseAsync(
    int prospectId)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int prospectId = 118;
try
{
    ICGBusinessEntitiesProspectScoreCategory result = await prospectScoresEquifaxOwnerCreditController.ProspectScoresEquifaxOwnerCreditSetAllScoreEquifaxOwnerCreditResponseAsync(prospectId);
}
catch (ApiException e){};
``` 

It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectScoresEquifaxOwnerCreditController" object fails to calculate equifax owner score that was anticipated to be returned. The prospect id will be passed as parameter to `ProspectScoresEquifaxOwnerCreditSetAllScoreEquifaxOwnerCreditResponseAsync` method in order to successfully and accurately calculate score of the specific prospect. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.   
 

#### Parameters Detail      
This endpoint requires only one parameter **prospectId** which is unique for each prospect for calculating the equifax owner credit score.
  
![85](https://user-images.githubusercontent.com/110983629/191017276-34eaa71c-469b-40d2-95d0-195559d19e6b.png)

 
#### Responses 
The response of this endpoint service request contains the `Task<Models.ICGBusinessEntitiesProspectScoreCategory>` that returns the value for the list of owners for calculating Score Equifax Owner Credit Response.

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

#### Response Body
```markdown
{
  "Id": null,
  "ProspectId": null,
  "ScoreCategoryId": null,
  "Score": null
} 
```
The class name of **Task<Models.ICGBusinessEntitiesProspectScoreCategory>** object is
```markdown
     ICGBusinessEntitiesProspectScoreCategory
```

 #### Explorer 

|Names|Description|
|-----|-----------|
|response type|[Task<Models.ICGBusinessEntitiesProspectScoreCategory>](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-business-entities-prospect-score-category)|






### Prospect Scores Equifax Owner Credit Get Score Equifax Owner Credit Response S Sn Control
#### Description 
This service endpoint will allow the user to retrieve the list of owners credit by accessing the prospect through the prospect id. The owner list may contain equifax score but it is not required. To acquire that, an instance of `ProspectScoresEquifaxOwnerCreditController` class is created by the API client for calling the `ProspectScoresEquifaxOwnerCreditSetAllScoreEquifaxOwnerCreditResponseAsync` method.

```markdown  
  ProspectScoresEquifaxOwnerCreditGetScoreEquifaxOwnerCreditResponseSSnControlAsync(
    int prospectId,
    Models.ICGBusinessEntitiesProspectPrincipalOwner owner)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int prospectId = 118;
var owner = new ICGBusinessEntitiesProspectPrincipalOwner();
try
{
    object result = await prospectScoresEquifaxOwnerCreditController.ProspectScoresEquifaxOwnerCreditGetScoreEquifaxOwnerCreditResponseSSnControlAsync(prospectId, owner);
}
catch (ApiException e){};
``` 

It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectScoresEquifaxOwnerCreditController" object fails to retrieve owner list that was anticipated to be returned. The prospect id and owner object will be passed as parameters to `ProspectScoresEquifaxOwnerCreditGetScoreEquifaxOwnerCreditResponseSSnControlAsync` method in order to successfully get owners list of the specific prospect. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.   
 

#### Parameters Detail      
This endpoint requires two parameters **prospectId** which is unique for each prospect and **owner** object that further contains Id (int type), ProspectId (int type), Title (string type), FirstName (string type), MiddleName (string type), LastName (string type), PercentageOfOwnership (double type), Ssn (string type), HomeAddress1 (string type), HomeAddress2 (string type), City (string type), State (string type), ZipCode (string type), DateOfBirth (DateTime type), Phone (string type), Email (string type), NameofBusiness (string type), Edited (bool type). 
   
![86](https://user-images.githubusercontent.com/110983629/191046312-f669024f-8775-42de-b25d-9b807e536e0a.png)

The class name of **owner** object is

```markdown
   ICGBusinessEntitiesProspectPrincipalOwner
```

#### owner object parameters

![87](https://user-images.githubusercontent.com/110983629/191046760-9167f33c-11fa-4e85-8955-de240a132b00.png)


 #### Explorer 

|Names|Description|
|-----|-----------|
|owner|[Models.ICGBusinessEntitiesProspectPrincipalOwner](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-business-entities-prospect-principal-owner)|



#### Responses 
The response of this endpoint service request contains the `Task<object>` that returns the value for the list of owners of the specific prospect.

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

 






### Prospect Scores Equifax Owner Credit Get Score Equifax Owner Credit PDF Response
#### Description 
This service endpoint will allow the user to retrieve the owner details in form of the PDF by accessing the prospect through the prospect id. The owner may contain equifax score but it is not required. To acquire that, an instance of `ProspectScoresEquifaxOwnerCreditController` class is created by the API client for calling the `ProspectScoresEquifaxOwnerCreditGetScoreEquifaxOwnerCreditPDFResponseAsync` method.

```markdown  
  ProspectScoresEquifaxOwnerCreditGetScoreEquifaxOwnerCreditPDFResponseAsync(
    int prospectId,
    Models.ICGBusinessEntitiesProspectPrincipalOwner owner)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int prospectId = 118;
var owner = new ICGBusinessEntitiesProspectPrincipalOwner();
try
{
    object result = await prospectScoresEquifaxOwnerCreditController.ProspectScoresEquifaxOwnerCreditGetScoreEquifaxOwnerCreditPDFResponseAsync(prospectId, owner);
}
catch (ApiException e){};
``` 

It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectScoresEquifaxOwnerCreditController" object fails to retrieve PDF for owner detail that was anticipated to be returned. The prospect id and owner object will be passed as parameters to `ProspectScoresEquifaxOwnerCreditGetScoreEquifaxOwnerCreditPDFResponseAsync` method in order to successfully get owner details of the specific prospect. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.   
 

#### Parameters Detail      
This endpoint requires two parameters **prospectId** which is unique for each prospect and **owner** object that further contains Id (int type), ProspectId (int type), Title (string type), FirstName (string type), MiddleName (string type), LastName (string type), PercentageOfOwnership (double type), Ssn (string type), HomeAddress1 (string type), HomeAddress2 (string type), City (string type), State (string type), ZipCode (string type), DateOfBirth (DateTime type), Phone (string type), Email (string type), NameofBusiness (string type), Edited (bool type). 
   
![86](https://user-images.githubusercontent.com/110983629/191046312-f669024f-8775-42de-b25d-9b807e536e0a.png)

The class name of **owner** object is

```markdown
   ICGBusinessEntitiesProspectPrincipalOwner
```

#### owner object parameters

![87](https://user-images.githubusercontent.com/110983629/191046760-9167f33c-11fa-4e85-8955-de240a132b00.png)


 #### Explorer 

|Names|Description|
|-----|-----------|
|owner|[Models.ICGBusinessEntitiesProspectPrincipalOwner](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-business-entities-prospect-principal-owner)|



#### Responses 
The response of this endpoint service request contains the `Task<object>` that returns the PDF for the owner of the specific prospect.

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|







### Prospect Scores Equifax Owner Credit Upload PDF to Drop Box
#### Description 
This service endpoint will allow the user to upload PDF to the drop box by accessing the report through the prospect id. The report will contain credit owner report data. The owner may contain equifax score but it is not required. To acquire that, an instance of `ProspectScoresEquifaxOwnerCreditController` class is created by the API client for calling the `ProspectScoresEquifaxOwnerCreditUploadPDFToDropBoxAsync` method.

```markdown  
  ProspectScoresEquifaxOwnerCreditUploadPDFToDropBoxAsync(
    int prospectId,
    Models.ICGBusinessEntitiesProspectScoreEquifaxOwnerCreditResponse response)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int prospectId = 118;
var response = new ICGBusinessEntitiesProspectScoreEquifaxOwnerCreditResponse();
try
{
    object result = await prospectScoresEquifaxOwnerCreditController.ProspectScoresEquifaxOwnerCreditUploadPDFToDropBoxAsync(prospectId, response);
}
catch (ApiException e){};
``` 

It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectScoresEquifaxOwnerCreditController" object fails to upload PDF that was anticipated to be returned. The prospect id and owner object will be passed as parameters to `ProspectScoresEquifaxOwnerCreditUploadPDFToDropBoxAsync` method in order to successfully upload owner details of the specific prospect. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.   
 

#### Parameters Detail      
This endpoint requires two parameters **prospectId** which is unique for each prospect and **response** object that further contains model, owner, ResponseValidator, ProspectDropboxFile, objects along with Id (int type), UserId (int type), ResponseJsonBody (string type), CreateUtcDate (DateTime type), ModelId (int type), OwnerId (int type), ICGScore (int type), Recalculate (bool type), ProspectDropboxFileId (string type), ReportPDFLink (string type).
 
 ![88](https://user-images.githubusercontent.com/110983629/191054893-382b117e-f13f-42ec-9f47-a0f076699241.png)

 
The class name of **response** object is

```markdown
    ICGBusinessEntitiesProspectScoreEquifaxOwnerCreditResponse
```

#### response object parameters
 
![89](https://user-images.githubusercontent.com/110983629/191055144-b46d3d2f-fedd-47ea-8864-6b31aa0c0e8f.png)

#### Explorer 

|Names|Description|
|-----|-----------|
|response|[Models.ICGBusinessEntitiesProspectScoreEquifaxOwnerCreditResponse](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-business-entities-prospect-score-equifax-owner-credit-response)|


#### Responses 
The response of this endpoint service request contains the `Task<object>` that returns the value for uploading PDF for the owner on the drop box.

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|





## API Endpoints
## Prospect Scores Tax Id
### Prospect Scores Tax Id Get Prospect Tax Id Score
#### Description 
This service endpoint will allow the user to retrieve the Tax Id Score values for the automatic set of score for a prospect by entering the prospect id which is unique for each prospect. For this purpose, an instance of `ProspectScoresTaxIdController` class is created by the API client for calling the `ProspectScoresTaxIdGetProspectTaxIdScoreAsync` method.


```markdown  
   ProspectScoresTaxIdController prospectScoresTaxIdController = client.ProspectScoresTaxIdController;
```

```markdown  
 ProspectScoresTaxIdGetProspectTaxIdScoreAsync(
    int prospectId)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int prospectId = 118;
try
{
    object result = await prospectScoresTaxIdController.ProspectScoresTaxIdGetProspectTaxIdScoreAsync(prospectId);
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectScoresTaxIdController" object fails to retrieve tax id score values that was anticipated to be returned. The prospect id will be passed as parameter to `ProspectScoresTaxIdGetProspectTaxIdScoreAsync` method in order to successfully retrieve score values for the automatic set of score of the specific prospect. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  
 

#### Parameters Detail      
This endpoint requires only one parameter **prospectId** which is unique for each prospect in order to get the  tax id score values.
 
![82](https://user-images.githubusercontent.com/110983629/191008754-edc1ceb1-e652-444f-8d6c-9b98384c8c71.png)

 
#### Responses 
The response of this endpoint service request contains the `Task<object>` that returns the values for score values.

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|






### Prospect Scores Tax Id Recalculate Prospect Score Tax Id
#### Description 
This service endpoint will allow the user to recalculate the score for Tax Id and get the new score values for a prospect by entering the prospect id which is unique for each prospect. For this purpose, an instance of `ProspectScoresTaxIdController` class is created by the API client for calling the `ProspectScoresTaxIdRecalculateProspectScoreTaxIdAsync` method.


```markdown  
 ProspectScoresTaxIdRecalculateProspectScoreTaxIdAsync(
    int prospectId)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int prospectId = 118;
try
{
    ICGBusinessEntitiesProspectScoreTaxIdQuery result = await prospectScoresTaxIdController.ProspectScoresTaxIdRecalculateProspectScoreTaxIdAsync(prospectId);
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectScoresTaxIdController" object fails to recalculate tax id score values that was anticipated to be returned. The prospect id will be passed as parameter to `ProspectScoresTaxIdRecalculateProspectScoreTaxIdAsync` method in order to successfully retrieve score values for the automatic set of score of the specific prospect. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  
 

#### Parameters Detail      
This endpoint requires only one parameter **prospectId** which is unique for each prospect in order to recalculate the score for tax id.
  
![90](https://user-images.githubusercontent.com/110983629/191237237-8b9570f2-02cf-46a2-a00c-d51170b9b76c.png)

 
#### Responses 
The response of this endpoint service request contains the `Task<Models.ICGBusinessEntitiesProspectScoreTaxIdQuery>` that returns the values for recalculated score values.

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

#### Response Body
```markdown
 {
  "ProspectScoreCategory": null,
  "ProspectScoreTaxIdQueryValidation": null,
  "ProspectScoreTaxIdQueryScores": null,
  "Id": null,
  "ProspectScoreCategoryId": null,
  "ScoreTaxIdQueryResultId": null,
  "Tin": null,
  "LegalName": null,
  "Street1": null,
  "Street2": null,
  "City": null,
  "State": null,
  "ZipCode": null,
  "UserName": null,
  "CreatedUtcDate": null
}
```
The class name of **Task<Models.ICGBusinessEntitiesProspectScoreTaxIdQuery>** object is
```markdown
     ICGBusinessEntitiesProspectScoreTaxIdQuery
```

#### Task<Models.ICGBusinessEntitiesProspectScoreTaxIdQuery> Parameters  

![91](https://user-images.githubusercontent.com/110983629/191238093-f298c86e-c4a0-4a40-af3d-789c64393f72.png)


#### Explorer 

|Names|Description|
|-----|-----------|
|response type|[Task<Models.ICGBusinessEntitiesProspectScoreTaxIdQuery>](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-business-entities-prospect-score-tax-id-query)|





### Prospect Scores Tax Id Save Manual Prospect Score Tax Id
#### Description 
This service endpoint will allow the user to update the score manually for Tax Id and get the new score values for a prospect by entering the prospect id which is unique for each prospect. For this purpose, an instance of `ProspectScoresTaxIdController` class is created by the API client for calling the `ProspectScoresTaxIdSaveManualProspectScoreTaxIdAsync` method.


```markdown  
 ProspectScoresTaxIdSaveManualProspectScoreTaxIdAsync(
    int prospectId,
    Models.ICGBusinessEntitiesProspectScoreTaxIdQueryScore score)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int prospectId = 118;
var score = new ICGBusinessEntitiesProspectScoreTaxIdQueryScore();

try
{
    ICGBusinessEntitiesProspectScoreTaxIdQueryScore result = await prospectScoresTaxIdController.ProspectScoresTaxIdSaveManualProspectScoreTaxIdAsync(prospectId, score);
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectScoresTaxIdController" object fails to update score for the tax id that was anticipated to be returned. The prospect id and updated score will be passed as parameters to `ProspectScoresTaxIdSaveManualProspectScoreTaxIdAsync` method in order to successfully update score values manually. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  
 

#### Parameters Detail      
This endpoint requires two parameters **prospectId** (int type) which is unique for each prospect and **score** object for updating score data that includes Id (int type), ProspectScoreTaxIdQueryId (int type), Score (int type), IsAutomaticScore (bool type), Comment (string type), UserName (string type), CreatedUtcDate (DateTime type). 
   
   
 ![92](https://user-images.githubusercontent.com/110983629/191240924-edc14116-9010-4d46-b7b6-02aa75779bd9.png)

The class name of score object is 
```markdown
    ICGBusinessEntitiesProspectScoreTaxIdQueryScore
```


#### score object parameters

![93](https://user-images.githubusercontent.com/110983629/191241406-f2c84432-f0cc-41d5-b205-950a749df8aa.png)


#### Responses 
The response of this endpoint service request contains the `Task<Models.ICGBusinessEntitiesProspectScoreTaxIdQueryScore>` that returns the values for update score data.

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

#### Response Body
```markdown
 {
  "Id": null,
  "ProspectScoreTaxIdQueryId": null,
  "Score": null,
  "IsAutomaticScore": null,
  "Comment": null,
  "UserName": null,
  "CreatedUtcDate": null
}
```
The class name of **Task<Models.ICGBusinessEntitiesProspectScoreTaxIdQueryScore>** object is
```markdown
      ICGBusinessEntitiesProspectScoreTaxIdQueryScore
```
 

#### Explorer 

|Names|Description|
|-----|-----------|
|response type|[Task<Models.ICGBusinessEntitiesProspectScoreTaxIdQueryScore>](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-business-entities-prospect-score-tax-id-query-score)|





## API Endpoints
## Prospects Scores Average Bank Balances Plaid Transaction 
### O Data Prospects Scores Average Bank Balances Plaid Transaction
#### Description 
This service endpoint will allow the user to retrieve the single item from ProspectsScoresAverageBankBalancesPlaidTransaction so that you can get information about the plaid transaction of average bank balances. For this purpose, an instance of `ProspectsScoresAverageBankBalancesPlaidTransactionController` class is created by the API client for calling the `ODataProspectsScoresAverageBankBalancesPlaidTransactionAsync` method.


```markdown  
   ProspectsScoresAverageBankBalancesPlaidTransactionController prospectsScoresAverageBankBalancesPlaidTransactionController = client.ProspectsScoresAverageBankBalancesPlaidTransactionController;
```

```markdown  
 ODataProspectsScoresAverageBankBalancesPlaidTransactionAsync(
    int key)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int key = 120;
try
{
    await prospectsScoresAverageBankBalancesPlaidTransactionController.ODataProspectsScoresAverageBankBalancesPlaidTransactionAsync(key);
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectsScoresAverageBankBalancesPlaidTransactionController" object fails to retrieve single item that was anticipated to be returned. The key will be passed as parameter to `ODataProspectsScoresAverageBankBalancesPlaidTransactionAsync` method in order to successfully retrieve plaid transaction of the specific prospect. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  
 

#### Parameters Detail      
This endpoint requires only one parameter **key** (int type) which is unique for each plaid transaction of avergae bank balance score.
  
![94](https://user-images.githubusercontent.com/110983629/191245102-71669990-69e7-49ed-a24b-4ea869dce22d.png)

  
#### Responses 
The response of this endpoint service request contains the `Task` that returns the item for Prospect Scores Average Bank Balances Plaid Transaction.

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|







## API Endpoints
## Prospect Status
### O Data Prospect Status
#### Description 
This service endpoint will allow the user to retrieve the statuses of the prospects so that you can get information about the prospect data with respect to the statuses. For this purpose, an instance of `ProspectStatusController` class is created by the API client for calling the `ODataProspectStatusAsync` method.


```markdown  
   ProspectStatusController prospectStatusController = client.ProspectStatusController;
```

```markdown  
   ODataProspectStatusAsync()
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
try
{
    await prospectStatusController.ODataProspectStatusAsync();
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectStatusController" object fails to retrieve prospect statuses that was anticipated to be returned. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  
 

#### Parameters Detail      
This endpoint does not require any parameter.
  
#### Responses 
The response of this endpoint service request contains the `Task` that returns the prospect statuses for each Prospect.

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|







## API Endpoints
## Prospect Entities
### O Data Prospect Entities
#### Description 
This service endpoint will allow the user to retrieve all the data of the prospect which is present in the prospect entities so that you can get information about the prospect data without applying any filter. For this purpose, an instance of `ProspectEntitiesController` class is created by the API client for calling the `ODataProspectEntitiesAsync` method.


```markdown   
   ProspectEntitiesController prospectEntitiesController = client.ProspectEntitiesController;
```

```markdown  
   ODataProspectEntitiesAsync()
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
try
{
    await prospectEntitiesController.ODataProspectEntitiesAsync();
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectEntitiesController" object fails to retrieve prospect data that was anticipated to be returned. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  
 

#### Parameters Detail      
This endpoint does not require any parameter.
  
#### Responses 
The response of this endpoint service request contains the `Task` that returns the prospect data for each Prospect entity.

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|









## API Endpoints
## Prospects
### O Data Prospects
#### Description 
This service endpoint will allow the user to retrieve all the items of the prospect which is present in the prospect so that you can get information about the prospect data without applying any filter. For this purpose, an instance of `ProspectsController` class is created by the API client for calling the `ODataProspectsAsync()` method.


```markdown    
   ProspectsController prospectsController = client.ProspectsController;
```

```markdown  
   ODataProspectsAsync()
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
try
{
    List<ICGBusinessEntitiesProspect> result = await prospectsController.ODataProspectsAsync();
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectsController" object fails to retrieve prospect data that was anticipated to be returned. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  
 

#### Parameters Detail      
This endpoint does not require any parameter.
  
#### Responses 
The response of this endpoint service request contains the `Task<List<Models.ICGBusinessEntitiesProspect>>` that returns the prospect data for each Prospect.

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|


#### Response Body -JSON
```markdown
   {
  "PrincipalOwners": null,
  "Users": null,
  "ContactsEmailNoticeList": null,
  "Ach": null,
  "CC": null,
  "ProcessorCode": null,
  "ProspectProducts": null,
  "ProspectProductValues": null,
  "ProspectSettings": null,
  "ProspectCampaigns": null,
  "ProspectIntermediaryBusinessOwnerships": null,
  "CustomFields": null,
  "CustomPaymentPortals": null,
  "ProspectAdobeDocuments": null,
  "CallbackFunction": null,
  "Id": null,
  "ProspectTypeId": null,
  "ProspectStatusId": null,
  "IsACH": null,
  "IsCC": null,
  "FeeModelId": null,
  "MerchantName": null,
  "Iso": null,
  "ReferalPartner": null,
  "SalesRepName": null,
  "SalesRepEmail": null,
  "SalesRepCode": null,
  "NotesForUnderwriting": null,
  "DbaName": null,
  "LegalBusinessName": null,
  "FederalTaxId": null,
  "SicCode": null,
  "NaicsCode": null,
  "BusinessAddress1": null,
  "BusinessAddress2": null,
  "City": null,
  "State": null,
  "ZipCode": null,
  "MonthEstablished": null,
  "YearEstablished": null,
  "StateOrganization": null,
  "BusinessPhoneNumber": null,
  "CustomerServicePhoneNumber": null,
  "MerchantWebsiteURL": null,
  "NoMerchantWebsiteURL": null,
  "TypeBusiness": null,
  "DetailedInfoPayment": null,
  "TypeOwnershipsId": null,
  "TaxClassificationsId": null,
  "TaxClassificationsTypeId": null,
  "HadAdminHearing": null,
  "AdminHearingReson": null,
  "ContactFirstName": null,
  "ContactLastName": null,
  "ContactTitle": null,
  "ContactEmail": null,
  "ContactPhone": null,
  "ContactExtension": null,
  "AREmail": null,
  "POAEmail": null,
  "TechnicalContactEmail": null,
  "TechnicalContactName": null,
  "IsBusinessContactPreferred": null,
  "BusinessContactEmail": null,
  "BusinessContactName": null,
  "IsOwnerOfficerContactPreferred": null,
  "OwnerOfficerContactEmail": null,
  "OwnerOfficerContactName": null,
  "FeeScheduleGatewaySetupFee": null,
  "FeeScheduleGatewayMonthlyFee": null,
  "HasFeeScheduleCustomPaymentPortal": null,
  "FeeScheduleCustomPaymentPortal": null,
  "HasFeeScheduleICGInvoicing": null,
  "FeeScheduleICGInvoicing": null,
  "HasFeeScheduleQuickBooksPlugin": null,
  "FeeScheduleQuickBooksPlugin": null,
  "HasFeeScheduleQuickBooksOnline": null,
  "FeeScheduleQuickBooksOnline": null,
  "HasFeeScheduleWooCommercePlugin": null,
  "FeeScheduleWooCommercePlugin": null,
  "HasFeeScheduleIVRFee": null,
  "FeeScheduleIVRFee": null,
  "HasFeeScheduleSMSProcessingFee": null,
  "FeeScheduleSMSProcessingFee": null,
  "HasFeeScheduleMagtekUSBSwiper": null,
  "FeeScheduleMagtekUSBSwiper": null,
  "HasFeeScheduleMobileSwiper": null,
  "FeeScheduleMobileSwiper": null,
  "HasLockboxProcessingFeesStandard": null,
  "LockboxProcessingFeesStandard": null,
  "HasLockboxProcessingFeesLarge": null,
  "LockboxProcessingFeesLarge": null,
  "IsIcgVerify": null,
  "IcgVerifyVerificationFee": null,
  "IcgVerifyEstimatedNVerificationsPerMonth": null,
  "IcgVerifyPurposeOfUsingVerificationServices": null,
  "IsIcgVerifyTypeServiceAPIAccess": null,
  "IsIcgVerifyTypeServiceManuallyRunning": null,
  "IcgVerifyBillingOptionsId": null,
  "SettlementAccountBank": null,
  "SettlementAccountRouting": null,
  "SettlementAccountNumber": null,
  "SettlementAccountType": null,
  "IsBillingAccountSameAsSettlement": null,
  "BillingAccountBank": null,
  "BillingAccountRouting": null,
  "BillingAccountNumber": null,
  "BillingAccountType": null,
  "PaymentModelSettlementAccountBank": null,
  "PaymentModelSettlementAccountRouting": null,
  "PaymentModelSettlementAccountNumber": null,
  "IsPaymentModelBillingAccountSameAsSettlement": null,
  "PaymentModelBillingAccountBank": null,
  "PaymentModelBillingAccountRouting": null,
  "PaymentModelBillingAccountNumber": null,
  "PaymentPortalTypeId": null,
  "IsICGInvoicing": null,
  "MerchantPaymentURL": null,
  "ContactRequirementPortalName": null,
  "ContactRequirementPortalPhone": null,
  "PaymentPortalNotes": null,
  "CreatedUtcDate": null,
  "CreatedUser": null,
  "CurrentLoggedUser": null,
  "CurrentUser": null,
  "CurrentAdmin": null,
  "ElavonIntegrationApplicationId": null,
  "ElavonIntegrationMerchantNumber": null,
  "PercentageCompletionFields": null,
  "PercentageCompletionFiles": null,
  "CanIntegrateWithElavon": null,
  "AdminConsoleMerchantCode": null,
  "AdminConsoleMerchantPaymentFeeCode": null,
  "AdminConsoleMerchantId": null,
  "RelationshipManager": null,
  "RecurringOption": null,
  "RecurringFrequency": null,
  "AchConvenienceFee": null,
  "IsAchConvenienceFeeTypeFlat": null,
  "IsAchConvenienceFeeTypePercentage": null,
  "AchConvenienceFeeAmount": null,
  "CreditDebitCardConvenienceFeeOption": null,
  "IsCreditDebitCardConvenienceFeeFlat": null,
  "IsCreditDebitCardConvenienceFeePercentage": null,
  "CreditDebitCardConvenienceFeeAmount": null,
  "AnnualReviewStatus": null,
  "HasPlaidMerchantToken": null,
  "IsAuthVerify": null,
  "AccountBalanceVerify": null,
  "IdentityVerify": null,
  "WixWebSiteFee": null,
  "HasWixWebSiteFee": null,
  "HasInvoicingOptions": null,
  "FeeInvoicingOptions": null,
  "HasEmailInvoicing": null,
  "FeeEmailInvoicing": null,
  "HasSmsInvoicing": null,
  "FeeSmsInvoicing": null,
  "HasFeeScheduleSMSNotify": null,
  "FeeScheduleSMSNotify": null,
  "HasIcgProcessPaymentToken": null,
  "IcgProcessPaymentToken": null,
  "AssignUserId": null
}
```
The class name of Task<List<Models.ICGBusinessEntitiesProspect>> is
```markdown
  ICGBusinessEntitiesProspect
```


#### Explorer 

|Names|Description|
|-----|-----------|
|response type|[Task<List<Models.ICGBusinessEntitiesProspect>>](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-business-entities-prospect)|




### O Data Prospects 1
#### Description 
This service endpoint will allow the user to add a new prospect by adding all its details so that you can employ it in performing operations on merchants. For this purpose, an instance of `ProspectsController` class is created by the API client for calling the `ODataProspectsAsync()` method.

```markdown  
  ODataProspects1Async(
    Models.ICGBusinessEntitiesProspect prospect)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
var prospect = new ICGBusinessEntitiesProspect();
try
{
    ICGBusinessEntitiesProspect result = await prospectsController.ODataProspects1Async(prospect);
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectsController" object fails to add prospect data that was anticipated to be returned. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  
 

#### Parameters Detail      
This endpoint requires one parameter which is **prospect** object that further contains the PrincipalOwners, Users, ContactsEmailNoticeList etc along with many other attributes. See the explorer for more information:

#### Explorer 

|Names|Description|
|-----|-----------|
|prospect|[Models.ICGBusinessEntitiesProspect](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-business-entities-prospect)|

  
#### Responses 
The response of this endpoint service request contains the `Task<Models.ICGBusinessEntitiesProspect>` that returns the prospect data which is added for creating the prospect.

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|


#### Response Body -JSON
```markdown
  {
  "PrincipalOwners": null,
  "Users": null,
  "ContactsEmailNoticeList": null,
  "Ach": null,
  "CC": null,
  "ProcessorCode": null,
  "ProspectProducts": null,
  "ProspectProductValues": null,
  "ProspectSettings": null,
  "ProspectCampaigns": null,
  "ProspectIntermediaryBusinessOwnerships": null,
  "CustomFields": null,
  "CustomPaymentPortals": null,
  "ProspectAdobeDocuments": null,
  "CallbackFunction": null,
  "Id": null,
  "ProspectTypeId": null,
  "ProspectStatusId": null,
  "IsACH": null,
  "IsCC": null,
  "FeeModelId": null,
  "MerchantName": null,
  "Iso": null,
  "ReferalPartner": null,
  "SalesRepName": null,
  "SalesRepEmail": null,
  "SalesRepCode": null,
  "NotesForUnderwriting": null,
  "DbaName": null,
  "LegalBusinessName": null,
  "FederalTaxId": null,
  "SicCode": null,
  "NaicsCode": null,
  "BusinessAddress1": null,
  "BusinessAddress2": null,
  "City": null,
  "State": null,
  "ZipCode": null,
  "MonthEstablished": null,
  "YearEstablished": null,
  "StateOrganization": null,
  "BusinessPhoneNumber": null,
  "CustomerServicePhoneNumber": null,
  "MerchantWebsiteURL": null,
  "NoMerchantWebsiteURL": null,
  "TypeBusiness": null,
  "DetailedInfoPayment": null,
  "TypeOwnershipsId": null,
  "TaxClassificationsId": null,
  "TaxClassificationsTypeId": null,
  "HadAdminHearing": null,
  "AdminHearingReson": null,
  "ContactFirstName": null,
  "ContactLastName": null,
  "ContactTitle": null,
  "ContactEmail": null,
  "ContactPhone": null,
  "ContactExtension": null,
  "AREmail": null,
  "POAEmail": null,
  "TechnicalContactEmail": null,
  "TechnicalContactName": null,
  "IsBusinessContactPreferred": null,
  "BusinessContactEmail": null,
  "BusinessContactName": null,
  "IsOwnerOfficerContactPreferred": null,
  "OwnerOfficerContactEmail": null,
  "OwnerOfficerContactName": null,
  "FeeScheduleGatewaySetupFee": null,
  "FeeScheduleGatewayMonthlyFee": null,
  "HasFeeScheduleCustomPaymentPortal": null,
  "FeeScheduleCustomPaymentPortal": null,
  "HasFeeScheduleICGInvoicing": null,
  "FeeScheduleICGInvoicing": null,
  "HasFeeScheduleQuickBooksPlugin": null,
  "FeeScheduleQuickBooksPlugin": null,
  "HasFeeScheduleQuickBooksOnline": null,
  "FeeScheduleQuickBooksOnline": null,
  "HasFeeScheduleWooCommercePlugin": null,
  "FeeScheduleWooCommercePlugin": null,
  "HasFeeScheduleIVRFee": null,
  "FeeScheduleIVRFee": null,
  "HasFeeScheduleSMSProcessingFee": null,
  "FeeScheduleSMSProcessingFee": null,
  "HasFeeScheduleMagtekUSBSwiper": null,
  "FeeScheduleMagtekUSBSwiper": null,
  "HasFeeScheduleMobileSwiper": null,
  "FeeScheduleMobileSwiper": null,
  "HasLockboxProcessingFeesStandard": null,
  "LockboxProcessingFeesStandard": null,
  "HasLockboxProcessingFeesLarge": null,
  "LockboxProcessingFeesLarge": null,
  "IsIcgVerify": null,
  "IcgVerifyVerificationFee": null,
  "IcgVerifyEstimatedNVerificationsPerMonth": null,
  "IcgVerifyPurposeOfUsingVerificationServices": null,
  "IsIcgVerifyTypeServiceAPIAccess": null,
  "IsIcgVerifyTypeServiceManuallyRunning": null,
  "IcgVerifyBillingOptionsId": null,
  "SettlementAccountBank": null,
  "SettlementAccountRouting": null,
  "SettlementAccountNumber": null,
  "SettlementAccountType": null,
  "IsBillingAccountSameAsSettlement": null,
  "BillingAccountBank": null,
  "BillingAccountRouting": null,
  "BillingAccountNumber": null,
  "BillingAccountType": null,
  "PaymentModelSettlementAccountBank": null,
  "PaymentModelSettlementAccountRouting": null,
  "PaymentModelSettlementAccountNumber": null,
  "IsPaymentModelBillingAccountSameAsSettlement": null,
  "PaymentModelBillingAccountBank": null,
  "PaymentModelBillingAccountRouting": null,
  "PaymentModelBillingAccountNumber": null,
  "PaymentPortalTypeId": null,
  "IsICGInvoicing": null,
  "MerchantPaymentURL": null,
  "ContactRequirementPortalName": null,
  "ContactRequirementPortalPhone": null,
  "PaymentPortalNotes": null,
  "CreatedUtcDate": null,
  "CreatedUser": null,
  "CurrentLoggedUser": null,
  "CurrentUser": null,
  "CurrentAdmin": null,
  "ElavonIntegrationApplicationId": null,
  "ElavonIntegrationMerchantNumber": null,
  "PercentageCompletionFields": null,
  "PercentageCompletionFiles": null,
  "CanIntegrateWithElavon": null,
  "AdminConsoleMerchantCode": null,
  "AdminConsoleMerchantPaymentFeeCode": null,
  "AdminConsoleMerchantId": null,
  "RelationshipManager": null,
  "RecurringOption": null,
  "RecurringFrequency": null,
  "AchConvenienceFee": null,
  "IsAchConvenienceFeeTypeFlat": null,
  "IsAchConvenienceFeeTypePercentage": null,
  "AchConvenienceFeeAmount": null,
  "CreditDebitCardConvenienceFeeOption": null,
  "IsCreditDebitCardConvenienceFeeFlat": null,
  "IsCreditDebitCardConvenienceFeePercentage": null,
  "CreditDebitCardConvenienceFeeAmount": null,
  "AnnualReviewStatus": null,
  "HasPlaidMerchantToken": null,
  "IsAuthVerify": null,
  "AccountBalanceVerify": null,
  "IdentityVerify": null,
  "WixWebSiteFee": null,
  "HasWixWebSiteFee": null,
  "HasInvoicingOptions": null,
  "FeeInvoicingOptions": null,
  "HasEmailInvoicing": null,
  "FeeEmailInvoicing": null,
  "HasSmsInvoicing": null,
  "FeeSmsInvoicing": null,
  "HasFeeScheduleSMSNotify": null,
  "FeeScheduleSMSNotify": null,
  "HasIcgProcessPaymentToken": null,
  "IcgProcessPaymentToken": null,
  "AssignUserId": null
}
```

The class name of **Task<Models.ICGBusinessEntitiesProspect>** is
```markdown
   ICGBusinessEntitiesProspect
```

#### Explorer 

|Names|Description|
|-----|-----------|
|response type|[Task<Models.ICGBusinessEntitiesProspect>](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-business-entities-prospect)|








### O Data Prospects 2
#### Description 
This service endpoint will allow the user to  retrieve single item from the prospect in order to take informed decisions based on the one single item of the prospect. For this purpose, an instance of `ProspectsController` class is created by the API client for calling the `ODataProspects2Async` method.

```markdown  
  ODataProspects2Async(
    int key)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int key = 120;
try
{
    ICGBusinessEntitiesProspect result = await prospectsController.ODataProspects2Async(key);
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectsController" object fails to retrieve one prospect item that was anticipated to be returned. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  
 

#### Parameters Detail      
This endpoint requires one parameter which is **key** (int type). It is actually the prospect id which is a unique identifier for prospect.


![95](https://user-images.githubusercontent.com/110983629/191270742-cfb60c47-76f8-45d6-9485-0501fc9dfdb7.png)
 
 
#### Responses 
The response of this endpoint service request contains the `Task<Models.ICGBusinessEntitiesProspect>` that returns the one item/instance of prospect.

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|


#### Response Body -JSON
```markdown
{
  "PrincipalOwners": null,
  "Users": null,
  "ContactsEmailNoticeList": null,
  "Ach": null,
  "CC": null,
  "ProcessorCode": null,
  "ProspectProducts": null,
  "ProspectProductValues": null,
  "ProspectSettings": null,
  "ProspectCampaigns": null,
  "ProspectIntermediaryBusinessOwnerships": null,
  "CustomFields": null,
  "CustomPaymentPortals": null,
  "ProspectAdobeDocuments": null,
  "CallbackFunction": null,
  "Id": null,
  "ProspectTypeId": null,
  "ProspectStatusId": null,
  "IsACH": null,
  "IsCC": null,
  "FeeModelId": null,
  "MerchantName": null,
  "Iso": null,
  "ReferalPartner": null,
  "SalesRepName": null,
  "SalesRepEmail": null,
  "SalesRepCode": null,
  "NotesForUnderwriting": null,
  "DbaName": null,
  "LegalBusinessName": null,
  "FederalTaxId": null,
  "SicCode": null,
  "NaicsCode": null,
  "BusinessAddress1": null,
  "BusinessAddress2": null,
  "City": null,
  "State": null,
  "ZipCode": null,
  "MonthEstablished": null,
  "YearEstablished": null,
  "StateOrganization": null,
  "BusinessPhoneNumber": null,
  "CustomerServicePhoneNumber": null,
  "MerchantWebsiteURL": null,
  "NoMerchantWebsiteURL": null,
  "TypeBusiness": null,
  "DetailedInfoPayment": null,
  "TypeOwnershipsId": null,
  "TaxClassificationsId": null,
  "TaxClassificationsTypeId": null,
  "HadAdminHearing": null,
  "AdminHearingReson": null,
  "ContactFirstName": null,
  "ContactLastName": null,
  "ContactTitle": null,
  "ContactEmail": null,
  "ContactPhone": null,
  "ContactExtension": null,
  "AREmail": null,
  "POAEmail": null,
  "TechnicalContactEmail": null,
  "TechnicalContactName": null,
  "IsBusinessContactPreferred": null,
  "BusinessContactEmail": null,
  "BusinessContactName": null,
  "IsOwnerOfficerContactPreferred": null,
  "OwnerOfficerContactEmail": null,
  "OwnerOfficerContactName": null,
  "FeeScheduleGatewaySetupFee": null,
  "FeeScheduleGatewayMonthlyFee": null,
  "HasFeeScheduleCustomPaymentPortal": null,
  "FeeScheduleCustomPaymentPortal": null,
  "HasFeeScheduleICGInvoicing": null,
  "FeeScheduleICGInvoicing": null,
  "HasFeeScheduleQuickBooksPlugin": null,
  "FeeScheduleQuickBooksPlugin": null,
  "HasFeeScheduleQuickBooksOnline": null,
  "FeeScheduleQuickBooksOnline": null,
  "HasFeeScheduleWooCommercePlugin": null,
  "FeeScheduleWooCommercePlugin": null,
  "HasFeeScheduleIVRFee": null,
  "FeeScheduleIVRFee": null,
  "HasFeeScheduleSMSProcessingFee": null,
  "FeeScheduleSMSProcessingFee": null,
  "HasFeeScheduleMagtekUSBSwiper": null,
  "FeeScheduleMagtekUSBSwiper": null,
  "HasFeeScheduleMobileSwiper": null,
  "FeeScheduleMobileSwiper": null,
  "HasLockboxProcessingFeesStandard": null,
  "LockboxProcessingFeesStandard": null,
  "HasLockboxProcessingFeesLarge": null,
  "LockboxProcessingFeesLarge": null,
  "IsIcgVerify": null,
  "IcgVerifyVerificationFee": null,
  "IcgVerifyEstimatedNVerificationsPerMonth": null,
  "IcgVerifyPurposeOfUsingVerificationServices": null,
  "IsIcgVerifyTypeServiceAPIAccess": null,
  "IsIcgVerifyTypeServiceManuallyRunning": null,
  "IcgVerifyBillingOptionsId": null,
  "SettlementAccountBank": null,
  "SettlementAccountRouting": null,
  "SettlementAccountNumber": null,
  "SettlementAccountType": null,
  "IsBillingAccountSameAsSettlement": null,
  "BillingAccountBank": null,
  "BillingAccountRouting": null,
  "BillingAccountNumber": null,
  "BillingAccountType": null,
  "PaymentModelSettlementAccountBank": null,
  "PaymentModelSettlementAccountRouting": null,
  "PaymentModelSettlementAccountNumber": null,
  "IsPaymentModelBillingAccountSameAsSettlement": null,
  "PaymentModelBillingAccountBank": null,
  "PaymentModelBillingAccountRouting": null,
  "PaymentModelBillingAccountNumber": null,
  "PaymentPortalTypeId": null,
  "IsICGInvoicing": null,
  "MerchantPaymentURL": null,
  "ContactRequirementPortalName": null,
  "ContactRequirementPortalPhone": null,
  "PaymentPortalNotes": null,
  "CreatedUtcDate": null,
  "CreatedUser": null,
  "CurrentLoggedUser": null,
  "CurrentUser": null,
  "CurrentAdmin": null,
  "ElavonIntegrationApplicationId": null,
  "ElavonIntegrationMerchantNumber": null,
  "PercentageCompletionFields": null,
  "PercentageCompletionFiles": null,
  "CanIntegrateWithElavon": null,
  "AdminConsoleMerchantCode": null,
  "AdminConsoleMerchantPaymentFeeCode": null,
  "AdminConsoleMerchantId": null,
  "RelationshipManager": null,
  "RecurringOption": null,
  "RecurringFrequency": null,
  "AchConvenienceFee": null,
  "IsAchConvenienceFeeTypeFlat": null,
  "IsAchConvenienceFeeTypePercentage": null,
  "AchConvenienceFeeAmount": null,
  "CreditDebitCardConvenienceFeeOption": null,
  "IsCreditDebitCardConvenienceFeeFlat": null,
  "IsCreditDebitCardConvenienceFeePercentage": null,
  "CreditDebitCardConvenienceFeeAmount": null,
  "AnnualReviewStatus": null,
  "HasPlaidMerchantToken": null,
  "IsAuthVerify": null,
  "AccountBalanceVerify": null,
  "IdentityVerify": null,
  "WixWebSiteFee": null,
  "HasWixWebSiteFee": null,
  "HasInvoicingOptions": null,
  "FeeInvoicingOptions": null,
  "HasEmailInvoicing": null,
  "FeeEmailInvoicing": null,
  "HasSmsInvoicing": null,
  "FeeSmsInvoicing": null,
  "HasFeeScheduleSMSNotify": null,
  "FeeScheduleSMSNotify": null,
  "HasIcgProcessPaymentToken": null,
  "IcgProcessPaymentToken": null,
  "AssignUserId": null
}
```

The class name of **Task<Models.ICGBusinessEntitiesProspect>** is
```markdown
   ICGBusinessEntitiesProspect
```

#### Explorer 

|Names|Description|
|-----|-----------|
|response type|[Task<Models.ICGBusinessEntitiesProspect>](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-business-entities-prospect)|







### O Data Prospects 3
#### Description 
This service endpoint will allow the user to update single item from the prospect in order to add latest prospect information in the system. For this purpose, an instance of `ProspectsController` class is created by the API client for calling the `ODataProspects3Async` method.

```markdown  
   ODataProspects3Async(
    int key,
    Models.ICGBusinessEntitiesProspect prospect)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int key = 120;
var prospect = new ICGBusinessEntitiesProspect();
try
{
    await prospectsController.ODataProspects3Async(key, prospect);
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectsController" object fails to update one prospect item that was anticipated to be returned. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  
 

#### Parameters Detail       
This endpoint requires two parameters which are **key** (int type) and **prospect** object. The key is actually the prospect id which is a unique identifier for prospect. And the **prospect** object further contains the attributes/parameters for the prospect instance that needs to be updated. 

![96](https://user-images.githubusercontent.com/110983629/191277898-f9218b65-b8d1-48ab-99ab-1d1def54b034.png)

The class name for the prospect object is
```markdown
    ICGBusinessEntitiesProspect
```

 
#### Explorer 

|Names|Description|
|-----|-----------|
|prospect object|[Models.ICGBusinessEntitiesProspect](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-business-entities-prospect)|


 
#### Responses 
The response of this endpoint service request contains the `Task` that returns the one item/instance of prospect which get updated by the user.

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

 





### O Data Prospects 4
#### Description 
This service endpoint will allow the user to delete single item from the prospect in order to remove prospect information from the system. For this purpose, an instance of `ProspectsController` class is created by the API client for calling the `ODataProspects4Async` method.

```markdown  
   ODataProspects4Async(
    int key,
    int message)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started) 

#### Class-Object
```markdown
int key = 120;
int message = 16;
try
{
    await prospectsController.ODataProspects4Async(key, message);
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "prospectsController" object fails to delete one prospect item that was anticipated to be returned. And try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  
 

#### Parameters Detail       
This endpoint requires two parameters which are **key** (int type) and **message** (int type). The key and message both are actually the prospect id which is a unique identifier for prospect.  
 
 
![97](https://user-images.githubusercontent.com/110983629/191281108-2ce2cd37-5d72-4c92-83b5-d84df9bd94fb.png)

 
#### Responses 
The response of this endpoint service request contains the `Task` that returns the one item/instance of prospect which get deleted by the user.

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

 




























































































































































