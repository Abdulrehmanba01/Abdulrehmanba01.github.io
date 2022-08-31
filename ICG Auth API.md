# For .NET
  
## Getting Started
  
### Description

The ICG Auth API of the iCheckGateway facilitate its users to carry out different operations in their account after getting authenticated and authorized for the account. The users can organize their account setting, profile, permissions, enable/disable App TFA etc., managing their applications permissions, deletion and renewals, audience, permissions, users, portals and roles.
 
  
#### Building
  
This API requires you to install 
  
  ```markdown 
  Newtonsoft Json.NET NuGet 
  ``` 
  
package. If you have enabled the **automatic NuGet package restore** then all the dependencies will get installed automatically. Therefore, you will need internet access for build.

**Steps to Proceed:**
  
1. Open the solution (ICGAPIAuth.sln) file
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
  
You need to do some installation before you can use the **ICGAPIAuth.Standard** library in a new project.
  
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
|`authorization`   | `String`    |                                                       |
  
  
The API client configuration looks like this:
```markdown 
 ICGAPIAuth.Standard.ICGAPIAuthClient client = new ICGAPIAuth.Standard.ICGAPIAuthClient.Builder().Build();
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
## Account
### Account My Settings
#### Description
     
In order to access the account settings, this API call will be executed where no parameters are passed through this API call. 

For this API call, an instance of `AccountController` class will be accessed from the API client.
 
```markdown
  AccountController accountController = client.AccountController;
```
This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
try
{
    Dictionary<string, string> result = await accountController.AccountMySettingsAsync();
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "accountController" object fails to produce the accurate result that were anticipated to be returned. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.
 


#### API object Parameters
This API call did not take any parameters.



#### Responses 

For viewing the response body, you need to download the text file. 

#### Response body-Text File
{
  "Message": "Authorization has been denied for this request."
}

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
  
  


## API Endpoints
## Account
### Account My Settings 2
#### Description
     
This service endpoint provides customers the ability to submit the current user account setting details. Through this process, you can update your current account setting where each user account setting is identified by the unique User Id.  
 
For this process, an instance of `AccountController` class will be accessed from the API client that will pass the user account setting details to the `AccountMySettings2Async` method in order to update it.
 
 
```markdown
AccountMySettings2Async(Models.UserSettingModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
var model = new UserSettingModel();
model.Key = "Key6";

try
{
    UserSettingModel result = await accountController.AccountMySettings2Async(model);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "accountController" object fails to put the user's account current state to the system that was anticipated to be returned. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.

 

#### API object Parameters
This endpoint will contain the `model` object as a parameter that further contains the **key**, **MValue**, **Description**, **Level**, **Enabled**, **DataType**, **UserId** parameters. The **Key** is the required parameter that is of _String_Type. The MValue, Description, DataType, UserId and Level are also of _String_Type. Only the **Enabled** parameter is of Boolean Type.

#### Model Object Parameters 
![1  bankaccount_setting](https://user-images.githubusercontent.com/110983629/187688776-20e7f944-11e1-43e5-a88f-83cf75bf1858.png)



#### Explorer 

|Names|Description|
|-----|-----------|
|Model(required)|[Models.UserSettingModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/user-setting-model)
 


#### Responses 

The response of this endpoint service request contains the "ResponseType" object. The class name of the ResposneType object is 

```markdown
UserSettingModel
``` 

#### Response body-JSON  
```markdown
   {
  "Key": "Key4",
  "Value": null,
  "Description": null,
  "Level": null,
  "Enabled": null,
  "DataType": null,
  "UserId": null
}
```

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

    
##### 'ResponseType' Object Parameters
The following list describe the parameters of the response type object:
1. **Key:** The key will be of String_Type that is unique for the model object.
2. **MValue:**  The mvalue will be of String_Type that contains merchant information. 
3. **Description:** It will be of _string_ type which will acknowledge user about the API response in form of text information. 
4. **Level:** It will be of _string_ type that contains user account level information.
5. **Enabled:** It will be of Boolean type that can be true of false based on user account setting.
6. **DataType:** It will be of String_Type that contains the user account setting details.
7. **UserId:** It will be of String_Type that is distinct for each user account.


### Account My Settings 1
#### Description
     
This service endpoint provides customers the ability to submit the current user account setting details. Through this process, you can add user's current account setting where each user account setting is identified by the unique User Id.  
 
For this process, an instance of `AccountController` class will be accessed from the API client that will pass the user account setting details to the `AccountMySettings1Async` method in order to update it.
 
 
```markdown
 AccountMySettings1Async(Models.UserSettingModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
var model = new UserSettingModel();
model.Key = "Key6";

try
{
    UserSettingModel result = await accountController.AccountMySettings1Async(model);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "accountController" object fails to add the user's account current state to the system that was anticipated to be returned. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.


#### API object Parameters
This endpoint will contain the `model` object as a parameter that further contains the **key**, **MValue**, **Description**, **Level**, **Enabled**, **DataType**, **UserId** parameters. The **Key** is the required parameter that is of _String_Type. The MValue, Description, DataType, UserId and Level are also of _String_Type. Only the **Enabled** parameter is of Boolean Type.

#### Model Object Parameters 
![1  bankaccount_setting](https://user-images.githubusercontent.com/110983629/187688776-20e7f944-11e1-43e5-a88f-83cf75bf1858.png)



#### Explorer 

|Names|Description|
|-----|-----------|
|Model(required)|[Models.UserSettingModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/user-setting-model)
 


#### Responses 

The response of this endpoint service request contains the "ResponseType" object. The class name of the ResposneType object is 

```markdown 
UserSettingModel
``` 

#### Response body-JSON  
```markdown
   {
  "Key": "Key4",
  "Value": null,
  "Description": null,
  "Level": null,
  "Enabled": null,
  "DataType": null,
  "UserId": null
}
```

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

    
##### 'ResponseType' Object Parameters
The following list describe the parameters of the response type object:
1. **Key:** The key will be of String_Type that is unique for the model object.
2. **MValue:**  The mvalue will be of String_Type that contains merchant information. 
3. **Description:** It will be of _string_ type which will acknowledge user about the API response in form of text information. 
4. **Level:** It will be of _string_ type that contains user account level information.
5. **Enabled:** It will be of Boolean type that can be true of false based on user account setting.
6. **DataType:** It will be of String_Type that contains the user account setting details.
7. **UserId:** It will be of String_Type that is distinct for each user account.

  
  









