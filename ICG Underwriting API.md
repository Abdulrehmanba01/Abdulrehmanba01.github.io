# For .NET
  
## Getting Started
  
### Description

The ICG underwriting API will give merchants the ability to submit their applications for managing and tracking their progress. They are able to carry out a variety of tasks with this API, including keeping track of prospect documents, Dropbox files, PDFs, integrations, logs, messages, scroes, tax, and balance plaid transactions. By sending API calls using this API, users may quickly access and control their merchant application.

  
#### Building
  
This API requires you to install 
  
  ```markdown 
  Newtonsoft Json.NET NuGet 
  ``` 
  
package. If you have enabled the **automatic NuGet package restore** then all the dependencies will get installed automatically. Therefore, you will need internet access for build.

**Steps to Proceed:**
  
1. Open the solution (ICGAPIUnderwriting.sln) file
2. Invoke the build process using 
  
  ```markdown 
  Ctrl + Shift + B 
  ``` 
  
  shortcut key or using the Build menu.
  
3. The build process generates a portable class library, which can be used like a normal class library. The generated library is compatible with 
  
     I) Windows Forms
  
    II) Windows RT
  
    III) Windows Phone 8
  
    IV) Silverlight 5 
  
     V) Xamarin iOS 
  
    VI) Xamarin Android and Mono
  
More information on how to use can be found at the **MSDN Portable Class Libraries documentation** 
  
#### Installation
  
You need to do some installation before you can use the **ICGAPIUnderwriting.Standard** library in a new project.
  
 1. Create new project: Right click on the current solution from the solution explorer and choose 
  > Add -> New Project
    
![19](https://user-images.githubusercontent.com/110983629/187217207-72aba7dd-9ef8-4832-82be-73cde9735dc8.png)

 2. Next, 
  > Choose Console Application, provide **TestConsoleProject** as the project name and click OK.
  
 ![20](https://user-images.githubusercontent.com/110983629/187217949-c08ed6d5-f8a8-4c30-b48f-3c5bae8a4c20.png)

 3. Set as Startup Project
  
 The new console project is the entry point for the eventual execution. This requires us to set the **TestConsoleProject** as the start-up project. To do this, 
  
  > right-click on the `TestConsoleProject` and choose `Set as StartUp Project` form the context menu.
  
 ![21](https://user-images.githubusercontent.com/110983629/187218304-67953c9b-a76b-452c-a77b-612cfa968118.png)

  4. Add reference of the library project
  
  In order to use the Tester library in the new project, first we must add a project reference to the TestConsoleProject. First, 
  
  > right click on the `References`node in the solution explorer and click `Add Reference`.
  
 ![22](https://user-images.githubusercontent.com/110983629/187218682-edfe46e9-0581-44af-b7ca-89b40bb1db40.png)

 > Next, a window will be displayed where we must set the `checkbox` on `Tester.Tests` and click `OK`. 
 By doing this, we have added a reference of the `Tester.Tests` project into the new `TestConsoleProject`.
  
 ![23](https://user-images.githubusercontent.com/110983629/187219056-c52818fc-b1e6-486a-b6a0-74ea5c592f78.png)
  
4. Write a Sample code
  
Once the `TestConsoleProject` is created, a file named `Program.cs` will be visible in the solution explorer with an empty `Main` method. This is the entry point for the execution of the entire solution. Here, you can add code to initialize the client library and acquire the instance of a Controller class. Sample code to initialize the client library and using Controller methods is given in the subsequent sections.
  
  
 ![24](https://user-images.githubusercontent.com/110983629/187219422-f2d8ab42-2cad-4025-8182-6a9bef3b67a4.png)

  
   
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
|Task<Models.ICGBusinessEntitiesProspectCompletionInformation>|[Task<Models.ICGBusinessEntitiesProspectCompletionInformation>](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-business-entities-prospect-completion-information)|



 




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
|Task<Models.ICGBusinessEntitiesProspectIntegrationResult>|[Task<Models.ICGBusinessEntitiesProspectIntegrationResult>](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-business-entities-prospect-integration-result)|
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
|Task<Models.ICGBusinessEntitiesProspectIntegrationResult>|[Task<Models.ICGBusinessEntitiesProspectIntegrationResult>](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-business-entities-prospect-integration-result)|
|Models.ICGModelsUnderwritingProspect|[Models.ICGModelsUnderwritingProspect](https://developers.icheckdev.com/UW/#/net-standard-library/models/structures/icg-models-underwriting-prospect)|





















