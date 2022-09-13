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
     
In order to send document for sign digitally, this API call will be executed that requires one parameter which is the prospect document id. 

```markdown
int prospectId = 118;
try
{
    object result = await prospectDocumentController.ProspectDocumentPostAsync(prospectId);
}
catch (ApiException e){};
```
This endpoint requires [Authentication](https://developers.icheckdev.com/UW/#/net-standard-library/getting-started/how-to-get-started)

In order to use ICG's APIs, all the applications needs to be authenticated first using Auth API through valid credentails including username and password. When user get authenticated successfully, the system will provide the token that user can utilize for making secure API calls. 


The paramters are listed below that are used to authenticate the user for a specific application:
|Parameter| Type |Description|
|---------|------|-----------|
| username |String| It can be username or email address|
|password|String|It is the password in encrypted form|
|client_id|String|It is the audience id unique for each application|
|grant_type|String|It is the grant mode which is password|

#### Response 

The response for authentication will be a token that is valid for some seconds only.

#### Response body

```markdown 
{
   "access_token": "{access_token_value}",
   "token_type": "bearer",
   "expires_in": 89399
}
```

You can make API calls by including the token in each header request which is:

```markdown 
   authorization: Bearer {access_token_value}
```

 

#### Class-Object
```markdown
try
{
    Dictionary<string, string> result = await accountController.AccountMySettingsAsync();
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "accountController" object fails to produce the accurate result that were anticipated to be returned. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 


#### Parameters Detail  
This API call did not take any parameters.



#### Responses 

For viewing the response body, you need to download the text file. 

#### Response body-Text File
```markdown 
{
  "Message": "Authorization has been denied for this request."
}
```

#### Verify Process Configuration

![19](https://user-images.githubusercontent.com/110983629/187513032-35b406d7-7a46-41da-9de8-79b252cdbb56.png)

You must confirm that the client configuration for the My Account setting procedure contains the single authorization token that must be inserted in order to get verified successfully. The authorization token will be accessible after the user authentication through the Auth API.



#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

    
 ##### 'ResponseType' Object Parameters
There are no parameters available for the response request.  
  
```markdown
   Task<Dictionary<string, string>>
```
  
  

