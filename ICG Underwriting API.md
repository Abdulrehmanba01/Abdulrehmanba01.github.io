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





















