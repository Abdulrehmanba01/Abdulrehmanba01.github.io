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

 

#### Parameters Detail  
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
 
For this process, an instance of `AccountController` class will be accessed from the API client that will pass the user account setting details to the `AccountMySettings1Async` method in order to submit it.
 
 
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


#### Parameters Detail  
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

  
  
### Account My Settings Delete
#### Description
     
This service endpoint provides customers the ability to delete the account settings by providing the key as a parameter to this process call. The key will be unique for each customer's account setting that will point towards only one account of the customer.
 
For this process, an instance of `AccountController` class will be accessed from the API client that will pass the user account setting key to the `AccountMySettingsDeleteAsync` method in order to submit it.
 
 
```markdown
 AccountMySettingsDeleteAsync(string key)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
string key = "key0";
try
{
    object result = await accountController.AccountMySettingsDeleteAsync(key);
}
catch (ApiException e){};
```


It will be included in the try and catch block to deal with any exceptions that could arise if the "accountController" object fails to delete the user's account settings that was anticipated to be returned. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.


#### Parameters Detail  
The API parameter for this service endpoint is **Key** (String_Type). It is the required parameter to add for deleting the user's account setting. 
 
![2](https://user-images.githubusercontent.com/110983629/187703187-50dab53f-35a6-4917-92da-9125c28d66b0.png)


#### Responses 

The response of this endpoint service request contains the Task<object>. 

```markdown 
Task<object>
``` 

#### Response headers-JSON
  
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

     
  
### Account My Settings 3
#### Description
  
This service endpoint provides customer the ability to retrieve his account details that has been created previously. This process call will recevie the **Key**
as a required parameter. The key will be unique for each customer's account setting that will point towards only one account of the customer.
 
For this process, an instance of `AccountController` class will be accessed from the API client that will pass the **key** to the `AccountMySettings3Async` method in order to get all details of the user's account.
 
 
```markdown
 AccountMySettings3Async(string key)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
 string key = "key0";
 try
 {
    string result = await accountController.AccountMySettings3Async(key);
 }
 catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "accountController" object fails to get the user's account settings detail that was anticipated to be returned. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.


#### Parameters Detail  
  
The API parameter for this service endpoint is **Key** (String_Type). It is the required parameter to add for retrieving the user's account setting. 
  
 ![3](https://user-images.githubusercontent.com/110983629/187707105-9cd07b2b-d485-489e-90d7-51cfbafbfbe8.png)

  

#### Responses 

The response of this endpoint service request contains the Task<object>. 

```markdown 
Task<object>
``` 

#### Response headers-JSON
  
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|





### Account My Profile
#### Description
     
This service endpoint will reterive current user details in order to keep track of the user in the system. This API request does not take any parameter. 
For this process, an instance of `AccountController` class will be accessed from the API client in order to call `AccountMyProfileAsync()` method to get user details.
 
```markdown
 AccountMyProfileAsync()
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
 
try
{
    UserReturnModel result = await accountController.AccountMyProfileAsync();
}
catch (ApiException e){};
  
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "accountController" object fails to get user current information from the system that was anticipated to be returned. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.


#### Parameters Detail  
This endpoint does not contain any parameter.


#### Responses 

The response of this endpoint service request contains the "ResponseType" object. The class name of the ResponseType object is 

```markdown 
UserReturnModel
``` 

#### Response body-JSON  
```markdown 
{
  "Url": null,
  "Id": null,
  "UserName": null,
  "FullName": null,
  "FirstName": null,
  "LastName": null,
  "Email": null,
  "MobilePhone": null,
  "HomePhone": null,
  "OfficePhone": null,
  "PostalCode": null,
  "EmailConfirmed": null,
  "Lockout": null,
  "Level": null,
  "Address": null,
  "Address2": null,
  "City": null,
  "State": null,
  "Country": null,
  "JoinDate": null,
  "Roles": null,
  "Settings": null,
  "PasswordExpDate": null,
  "CustomDaysToExpired": null,
  "TwoFactorEnabled": null,
  "IsPasswordCreated": null
}

```

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

    
##### 'ResponseType' Object Parameters
The following table describe the parameters of the response type object:
  
|Names|Description|
|-----|-----------| 
|Url|URL of String Type|
|ID|Id of String Type|
|UserName|User Name of String Type|
|FullName|Full Name of user of String Type|
|FirstName|First Name of String Type|
|LastName|Last Name of String Type|
|Email|Email of String Type|
|MobilePhone|Phone Number of String Type|
|HomePhone|Home Phone of String Type|  
|OfficePhone|Office Phone of String Type|
|PostalCode|Postal Code of String Type|
|EmailConfirmed|bool value|
|Lockout|bool value|
|Level|int value|
|Address|Address of String Type|
|Address2|Address2 of String Type|
|City|City of String Type|
|State|State of String Type|
|Country|Country of String Type|
|JoinDate|Join Date of DateTime Type|
|Roles|Roles of List<String> Type|
|Settings|Dictionary<string, string>|
|PasswordExpDate|Password Expiration date of DateTime Type|
|CustomDaysToExpired|Int Type that allow to set a custom policy for days to expired|
|TwoFactorEnable|TwoFactorEnabled of Bool Type|
|IsPasswordCreated|IsPasswordCreated of bool type|
  
  

#### Explorer 

|Names|Description|
|-----|-----------|
|ResponseType|[Task<Models.UserReturnModel>](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/user-return-model)|
 
 
### Account My Profile 1
#### Description
     
This service endpoint will update the current user details in order to store the latest information of the user in the system. This API contains the **"Model"** object as a parameter that is a required one. For this process, an instance of `AccountController` class will be accessed from the API client in order to call `AccountMyProfile1Async()` method to update the user details.
 
```markdown
 AccountMyProfile1Async(Models.ModifyUserProfileBindingModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
var model = new ModifyUserProfileBindingModel();
model.FirstName = "FirstName2";
model.LastName = "LastName2";

try
{
    UserReturnModel result = await accountController.AccountMyProfile1Async(model);
}
catch (ApiException e){};
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "accountController" object fails to update user information that was anticipated to be returned. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes. The model will be passed as a parameter to the `AccountMyProfile1Async()` method.
The FirstName and LastName are two required parameters of the `model` object. 


#### Model object Parameters 
  
  ![4](https://user-images.githubusercontent.com/110983629/187724681-40a8659b-5246-4dbd-b3f6-bb670bafc37e.png)
 ![5](https://user-images.githubusercontent.com/110983629/187724707-44c466d9-a81d-40a9-b622-9563b3dcaab2.png)



#### Responses 

The response of this endpoint service request contains the "ResponseType" object. The class name of the ResponseType object is 

```markdown 
UserReturnModel
``` 

#### Response body-JSON  
```markdown 
{
  "Url": null,
  "Id": null,
  "UserName": null,
  "FullName": null,
  "FirstName": null,
  "LastName": null,
  "Email": null,
  "MobilePhone": null,
  "HomePhone": null,
  "OfficePhone": null,
  "PostalCode": null,
  "EmailConfirmed": null,
  "Lockout": null,
  "Level": null,
  "Address": null,
  "Address2": null,
  "City": null,
  "State": null,
  "Country": null,
  "JoinDate": null,
  "Roles": null,
  "Settings": null,
  "PasswordExpDate": null,
  "CustomDaysToExpired": null,
  "TwoFactorEnabled": null,
  "IsPasswordCreated": null
}
```

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

    
##### 'ResponseType' Object Parameters
The following table describe the parameters of the response type object:
  
|Names|Description|
|-----|-----------| 
|Url|URL of String Type|
|ID|Id of String Type|
|UserName|User Name of String Type|
|FullName|Full Name of user of String Type|
|FirstName|First Name of String Type|
|LastName|Last Name of String Type|
|Email|Email of String Type|
|MobilePhone|Phone Number of String Type|
|HomePhone|Home Phone of String Type|  
|OfficePhone|Office Phone of String Type|
|PostalCode|Postal Code of String Type|
|EmailConfirmed|bool value|
|Lockout|bool value|
|Level|int value|
|Address|Address of String Type|
|Address2|Address2 of String Type|
|City|City of String Type|
|State|State of String Type|
|Country|Country of String Type|
|JoinDate|Join Date of DateTime Type|
|Roles|Roles of List<String> Type|
|Settings|Dictionary<string, string>|
|PasswordExpDate|Password Expiration date of DateTime Type|
|CustomDaysToExpired|Int Type that allow to set a custom policy for days to expired|
|TwoFactorEnable|TwoFactorEnabled of Bool Type|
|IsPasswordCreated|IsPasswordCreated of bool type|
  
  

#### Explorer 

|Names|Description|
|-----|-----------|
|ResponseType|[Task<Models.UserReturnModel>](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/user-return-model)|
 
 

### Account My Permissions
#### Description
In order to track user authenticated privileges across their account, this service endpoint will obtain the most recent user permissions. For the purpose of retrieving the actual user account permissions, this endpoint will use the 'AccountMyPermissionsAsync' function. The 'AccountMyPermissionsAsync()' function will be called by the API client by accessing an instance of the 'AccountController' class.
  
 
```markdown
   AccountMyPermissionsAsync()
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
try
{
    List<string> result = await accountController.AccountMyPermissionsAsync();
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "accountController" object fails to retrieve current user account permissions that was anticipated to be returned. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
This endpoint does not take any parameters.  
  

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|  
 

#### Response
##### 'ResponseType' Object Parameters 
The response of this endpoint service request contains the "ResponseType" object. The `Task<List<string>>` is the parameter that will return the list of the strings of current user permissions. 

 
 

### Account Enable App TFA
#### Description
This service endpoint will make the Google Authenticator app available for the user account, enabling two-factor authentication to increase account security. The 'AccountEnableAppTFAAsync()' function will be applied throughout this procedure to enable the Google Authenticator app for the user's account. The API client will obtain an instance of the 'AccountController' class and invoke the 'AccountEnableAppTFAAsync()' function.
  
 
```markdown
    AccountEnableAppTFAAsync()
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
try
{
    List<string> result = await accountController.AccountEnableAppTFAAsync();
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "accountController" object fails to enable the Google authenticator app for the user account that was anticipated to be returned. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

  
#### Parameters Detail  
This endpoint does not take any parameters.  
  

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|  
 

#### Response
##### 'ResponseType' Object Parameters   
The response of this endpoint service request contains the "ResponseType" object. The `Task<List<string>>` is the parameter that will return the list of the strings for enabling 2 factor authentication.



### Account Enable TFA
#### Description
  
For secure access to the application, this service endpoint enables two-factor authentication for user accounts. The 'AccountEnableTFAAsync()' method has been used for this process, and it will take a model object as a parameter to allow access to the relevant user account in order to verify users through the Google Authenticator App. 
An instance of `AccountController` class will be accessed from the API client. The parameters of the model get initialized in order verify the users through the AccountEnableTFAAsync method.
 
 
```markdown
 AccountEnableTFAAsync(Models.TfaAuthenticatorModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
var model = new TfaAuthenticatorModel();
model.Code = "Code2";
model.SecretKey = "SecretKey8";
model.Type = "Type2";
model.Audiences = new List<int>();
model.Audiences.Add(178);

try
{
    List<string> result = await accountController.AccountEnableTFAAsync(model);
}
catch (ApiException e){};
```
The model object's attributes will be declared and initialized first and then the model object will be passed to the `AccountEnableTFAAsync()`method as a parameter. It will be included in the try and catch block to deal with any exceptions that could arise if the "accountController" object fails to verify the users OTPs that was anticipated to be returned. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.


#### Parameters Detail  
  
This endpoint will contain the `model` object as a parameter that further contains the **Code**, **SecertKey**, **Type**, **Audiences** parameters where the Code, SecretKey and Type are the required parameters of String_Type. The Audiences is the list of integers to define the number of users whose 2 factor authentication process is enabled.  

#### Model Object Parameters 
  
![6](https://user-images.githubusercontent.com/110983629/187924670-790b62ea-78b7-446f-8354-5d6eee87748c.png)

 
The class name of the `model` object is
  
```markdown 
  TfaAuthenticatorModel
```  
  
#### Explorer 

|Names|Description|
|-----|-----------|
|Model(required)|[Models.TfaAuthenticatorModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/tfa-authenticator-model)
 


#### Responses 

The response of this endpoint service request contains the "ResponseType" object that contains the `Task<List<string>>` as a parameter. It will return the list of strings for the users who has enabled the TFA (Two factor Authentication). 


#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

 
  
  
### Account Disable TFA
#### Description
This service endpoint will disable the two factor authentication for the user accounts. The API client will obtain an instance of the 'AccountController' class and invoke the 'AccountDisableTFAAsync()` method in order to disable the TFA.  
  
 
```markdown
    AccountDisableTFAAsync()
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
try
{
    List<string> result = await accountController.AccountDisableTFAAsync();
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "accountController" object fails to disable the two factor authentication process for the user account that was anticipated to be returned. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

  
#### Parameters 
This endpoint does not take any parameters.  
  

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|  
 

#### Response
##### 'ResponseType' Object Parameters   
The response of this endpoint service request contains the "ResponseType" object. The `Task<List<string>>` is the parameter that will return the list of the strings for disabling 2 factor authentication.


 
  
### Account Confirm Email
#### Description
The user will have the option to confirm his account via email using this service endpoint. The user must confirm his account by email that he provides during the sign up process. It is the most effective technique to confirm and authenticate a person using his email address. The API client for this procedure accesses an instance of the 'AccountController' class and calls the 'AccountConfirmEmailAsync' method.  
 
 
```markdown
   AccountConfirmEmailAsync(
    string userId = null,
    string code = null,
    string callbackurl = null)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
try
{
    object result = await accountController.AccountConfirmEmailAsync(null, null, null);
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "accountController" object fails to confirm user's email address that was anticipated to be returned. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail   
This endpoint will contain the three parameters that includes user id, hash code, callbackurl. All of these three parameters are of String_Type and code and user id are required to enter for this process call. 
  
![7](https://user-images.githubusercontent.com/110983629/187933225-55fa524b-e8b7-4ead-ac89-47a2f3021aee.png)

  

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|  
 

#### Response
##### 'ResponseType' Object Parameters 
The response of this endpoint service request contains the "ResponseType" object. The `Task<object>` is the parameter that will return whether the user has confirmed his account by email or not.

  
### Account Confirm Email Set Password
#### Description  
  
The user will have the facility to confirm his account via email using this service endpoint. The user must confirm his account by email that he provides during the registeration process of the application. It is the most effective technique to confirm and authenticate a person using his email address. The API client for this process accesses an instance of the 'AccountController' class and calls the 'AccountConfirmEmailSetPasswordAsync' method.  
 
 
```markdown
   AccountConfirmEmailSetPasswordAsync(
    string userId = null,
    string code = null,
    string callbackurl = null)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
try
{
    object result = await accountController.AccountConfirmEmailSetPasswordAsync(null, null, null);
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "accountController" object fails to confirm user's email address set password that was anticipated to be returned. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
This endpoint will contain the three parameters that includes userId, code (hash code), callbackurl. All of these three parameters are of String_Type and code and user id are required to enter for this process call. 
  
  
![8](https://user-images.githubusercontent.com/110983629/187936383-08c2ebe6-d212-42b9-a0ef-f006afb330db.png)

  

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|  
 

#### Response
##### 'ResponseType' Object Parameters 
The response of this endpoint service request contains the "ResponseType" object. The `Task<object>` is the parameter that will return whether the user has confirmed his account by email or not to set password.

 
 
  
  
### Account Confirm Change Email 
#### Description  
    
The user will have the facility to confirm his account via email using this service endpoint when he wants to change his email address. The user must confirm his account by email that he provides during the registeration process of the application, but when he wants to change the email address. This changed email address should also be confirmed through the email. It is the most effective technique to confirm and authenticate a person using his email address. The API client for this process accesses an instance of the 'AccountController' class and calls the 'AccountConfirmChangeEmailAsync' method.  
 
 
```markdown
   AccountConfirmChangeEmailAsync(
    string userId = null,
    string code = null,
    string preToken = null,
    string callbackurl = null)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
try
{
    object result = await accountController.AccountConfirmChangeEmailAsync(null, null, null, null);
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "accountController" object fails to confirm user's changed email address that was anticipated to be returned. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
This endpoint will contain the four parameters that includes userId, code (hash code), preToken, callbackurl. All of these four parameters are of String_Type and code and user id are required to enter for this process call. 
  
![9](https://user-images.githubusercontent.com/110983629/187940304-a9c853b1-f60d-47f6-8049-a32d23f62d39.png)
  

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|  
 

#### Response
##### 'ResponseType' Object Parameters 
The response of this endpoint service request contains the "ResponseType" object. The `Task<object>` is the parameter that will return whether the user has confirmed his account by changed email or not.

 

  
### Account Confirm Change Password 
#### Description  
Through this service endpoint, the user will have the ability to change his account password. The necessity or potential for the user to update their account password to make their account more safe against malicious assaults may arise after creating an account in the application. It is the best technique for using a fresh password to authenticate a user. The 'AccountConfirmChangePasswordAsync' function is called by the API client for this procedure on an instance of the 'AccountController' class.
 
 
```markdown
   AccountConfirmChangePasswordAsync(
    string userId = null,
    string code = null,
    string preToken = null,
    string newPassword = null)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
try
{
    object result = await accountController.AccountConfirmChangePasswordAsync(null, null, null, null);
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "accountController" object fails to change user account password that was anticipated to be returned. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail   
This endpoint will contain the four parameters that includes userId, code, preToken, and newPassword. All of these four parameters are of String_Type. The code is used to validate the user, preToken is the hash code sent to the user and the newPassword is the new password that user set out for his account.  
 
![10](https://user-images.githubusercontent.com/110983629/187946577-d2c83884-f596-46d1-900d-142c67d99b30.png)


#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|  
 

#### Response
##### 'ResponseType' Object Parameters 
The response of this endpoint service request contains the "ResponseType" object. The `Task<object>` is the parameter that will return whether the user's account password has been changed or not.
 
  
  
### Account Forgot User Name 
#### Description  

This service endpoint will allow the user to recover his account if he forgot his username. In order to recover the user's account, his email address will be used for verifying the user and allow him to access his account. For this purpose, the 'AccountForgotUserNameAsync' method is called by the API client for this process on an instance of the 'AccountController' class.       
   
 
```markdown
   AccountForgotUserNameAsync(string email)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
 string email = "email6";
try
{
    object result = await accountController.AccountForgotUserNameAsync(email);
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "accountController" object fails to acess user account through the email that was anticipated to be returned. The email will be passed as a parameter to the method `AccountForgotUserNameAsync`. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
This endpoint will contain the only one parameters which is email address of the user who forgot his user name. The email address will be of String_Type and it is required to enter in order to recover the user's account securely. 
 
![11](https://user-images.githubusercontent.com/110983629/187952042-fcd4f852-c291-4d6e-b791-bd0a0c34b9bf.png)



#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|  
 

#### Response
##### 'ResponseType' Object Parameters 
The response of this endpoint service request contains the "ResponseType" object. The `Task<object>` is the parameter that will return whether the user's account get recovered through the email or not.
 
### Account Forgot Password
#### Description  

This service endpoint will allow the user to recover the password by sending email to the user's email address. When the user forgot his account password, the system will be able to recover it by sending email to the user's email address. The user must have to provide the user name and email address in order to recover his account password. For this purpose, the 'AccountForgotPasswordAsync' method is called by the API client for this process on an instance of the 'AccountController' class.       
 
```markdown
    AccountForgotPasswordAsync(
    string userName,
    string email,
    string urlCallback,
    string audienceId)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
string userName = "userName2";
string email = "email6";
string urlCallback = "urlCallback8";
string audienceId = "audienceId8";

try
{
    object result = await accountController.AccountForgotPasswordAsync(userName, email, urlCallback, audienceId);
}
catch (ApiException e){};
```
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "accountController" object fails to recover the user's account password that was anticipated to be returned. The user's email address and user name will be passed as a parameter to the method `AccountForgotPasswordAsync`. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
This endpoint will contain the four parameters which include the userName, email, urlCallback, and audienceId. These four parameters are required to enter for recovering the user's account password in a secured manner. All of these parameters are of String_Type.   
  
 
![12](https://user-images.githubusercontent.com/110983629/187960953-c058067e-9aae-440c-bebb-fa781e1a715c.png)



#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|  
 

#### Response
##### 'ResponseType' Object Parameters 
The response of this endpoint service request contains the "ResponseType" object. The `Task<object>` is the parameter that will return whether the user's account password get recovered by sending email or not.
   
  
### Account Change Email
#### Description  

The user can update his account email by entering his old and new email addresses to this service endpoint. It's possible that the user wished to alter his account's email address so he could get notifications at the new address. To add a new email address to his account, the user must first submit his previous email address. The API client calls the 'AccountChangeEmailAsync' method on an instance of the 'AccountController' class in order to do this.
          
 
```markdown
    AccountChangeEmailAsync(Models.ChangeEmailBindingModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
var model = new ChangeEmailBindingModel();
model.OldEmail = "OldEmail6";
model.NewEmail = "NewEmail8";
model.ConfirmEmail = "ConfirmEmail4";

try
{
    object result = await accountController.AccountChangeEmailAsync(model);
}
catch (ApiException e){};
```
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "accountController" object fails to change user's account email address that was anticipated to be returned. The `model` used to declare and initialize the user's old email address, new email address and confirmed new email address. The model will be passed to `AccountChangeEmailAsync` method. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Object `Model` Parameters 
  
The model object will contain the four parameters which include the OldEmail, NewEmail, ConfirmEmail, and CallBackUrl. These four parameters are required to enter for changing the user's account email except the CallBackUrl. All of these parameters are of String_Type where the NewEmail will have a contraint on the lenght (min-0 & max-100). 
  
 ![1](https://user-images.githubusercontent.com/110983629/188124519-73bde4f3-5160-4887-b75e-156114d0274d.png)

The class name of the `Model` object is 
 ```markdown
  ChangeEmailBindingModel
  ```

 
#### Explorer 

|Names|Description|
|-----|-----------|
|model(required)|[Models.ChangeEmailBindingModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/change-email-binding-model)
 


#### Responses 
 
##### 'ResponseType' Object Parameters 
The response of this endpoint service request contains the "ResponseType" object. The `Task<object>` is the parameter that will return whether the user's email address is changed or not.
   
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|     
  
  
  
 
### Account Login API
#### Description  
The user will be able to log into the application using the API key owing to this service endpoint. The API key itself serves as the user's identity, hence it must be distinct, random, and impenetrable in order to do so. Alphanumeric and special characters must be used when generating API keys. The API key serves as an identification code or authentication token when logging into the system. The 'AccountLoginApiAsync' method on an instance of the 'AccountController' class is invoked by the API client in order to do this.  
 
```markdown
    AccountLoginApiAsync(
    string appid,
    string apikey,
    string audienceid)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
string appid = "appid6";
string apikey = "apikey6";
string audienceid = "audienceid2";

try
{
    object result = await accountController.AccountLoginApiAsync(appid, apikey, audienceid);
}
catch (ApiException e){};
```
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "accountController" object fails to login through the API key that was anticipated to be returned. The appid, apikey and audienceid are the variables that get declared and initialize and then passed to the `AccountLoginApiAsync` method. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
The parameters of this endpoint are appid, apikey and audienceid where all of them are required to enter for logging in through the API key. All of these parameters are of String_Type.  
  
![2](https://user-images.githubusercontent.com/110983629/188129177-9096ef6f-ad00-4b8a-b2f2-2746ab2d7e04.png)


#### Responses 
 
##### 'ResponseType' Object Parameters 
The response of this endpoint service request contains the "ResponseType" object. The `Task<object>` is the parameter that will return the value whether the user get logged in through API key or not.
   
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|     
  
   
  
### Account Login Tfa
#### Description  
This service endpoint will enable two-factor authentication, requiring the user to input a one-time pin (OTP) that is only valid for a shorter amount of time while logging in to the system. An instance of the "AccountController" class is used for this by calling the "AccountLoginTfaAsync" function. By eliminating malicious assaults, it makes using the system to log in more secure.
 
```markdown
   AccountLoginTfaAsync(
    string preToken,
    string code,
    string audienceId = null)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
string preToken = "preToken2";
string code = "code8";

try
{
    object result = await accountController.AccountLoginTfaAsync(preToken, code, null);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "accountController" object fails to login through the OTP that was anticipated to be returned. The preToken and code are declared and initialize and then passed to the `AccountLoginTfaAsync` method. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
The parameters of this endpoint are preToken, code and audienceid where all of them are required to enter except audienceid for logging in. All of these parameters are of String_Type. The pretoken is the token for session id and code is the code (OTP) that is sent to the user through mobile number or through the email.
  
 ![3](https://user-images.githubusercontent.com/110983629/188132917-9ab790e9-7af1-44f3-8bf5-a70def9b2269.png)


#### Responses 
 
##### 'ResponseType' Object Parameters 
The response of this endpoint service request contains the "ResponseType" object. The `Task<object>` is the parameter that will return the value whether the user logged in through the valid TFA or not.
   
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|     
  
  
  
  
  
### Account Change Password
#### Description  
By using this service endpoint, the user can change his account password by submitting his previous password. If users have used the same password for several accounts on other platforms, there is a high risk of hacking and other harmful attempts. In order to successfully and securely update the user's account password, the API client calls the 'AccountChangePasswordAsync' method on an instance of the 'AccountController' class.  
          
 
```markdown
 AccountChangePasswordAsync(Models.ChangePasswordBindingModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
var model = new ChangePasswordBindingModel();
model.OldPassword = "OldPassword4";
model.NewPassword = "NewPassword2";
model.ConfirmPassword = "ConfirmPassword0";

try
{
    object result = await accountController.AccountChangePasswordAsync(model);
}
catch (ApiException e){};
```
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "accountController" object fails to change user's account password that was anticipated to be returned. The `model` used to declare and initialize the user's old password, new password and confirmed password. The model will be passed to `AccountChangePasswordAsync` method. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Object `Model` Parameters 
  
The model object will contain the three parameters which include the OldPassword, NewPassword, and ConfirmPassword. These three parameters are required to enter for changing the user's account password. All of these parameters are of String_Type where the NewPassword will have a contraint on the lenght (min-8 & max-128). 
  
![4](https://user-images.githubusercontent.com/110983629/188139823-ec7c54c4-a157-4e9c-8358-214781393dd0.png)

 

The class name of the `Model` object is 
 ```markdown
  ChangePasswordBindingModel
  ```

 
#### Explorer 

|Names|Description|
|-----|-----------|
|model(required)|[Models.ChangePasswordBindingModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/change-password-binding-model)
 


#### Responses 
 
##### 'ResponseType' Object Parameters 
The response of this endpoint service request contains the "ResponseType" object. The `Task<object>` is the parameter that will return whether the user's account password is changed or not.
   
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|     
  
  
  


### Account Register User
#### Description 
This service endpoint will provide the facility to the user to get registered in the system anonymously. The user will have to enter the registration details such as email, first name, last name etc. in order to get registered in the system successfully for utilizing platform's provided services. For this purpose, the `AccountRegisterUserAsync` method is called to create user account on in instance of `AccountController` class from the API client. 
   
 
```markdown
 AccountRegisterUserAsync(Models.CreateUserBindingModelAnonymous createUserModel)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
var createUserModel = new CreateUserBindingModelAnonymous();
createUserModel.Email = "Email8";
createUserModel.Username = "Username4";
createUserModel.FirstName = "FirstName8";
createUserModel.LastName = "LastName8";
createUserModel.Password = "Password6";
createUserModel.ConfirmPassword = "ConfirmPassword4";

try
{
    UserReturnModel result = await accountController.AccountRegisterUserAsync(createUserModel);
}
catch (ApiException e){};  
  
```
It will be included in the try and catch block to deal with any exceptions that could arise if the "accountController" object fails to register a user that was anticipated to be returned. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.


#### Parameters Detail  
The parameter of this endpoint service contains **createUserModel** as a required object. It further contains the Email, Username, FirstName, LastName, Password, ConfirmPassword, Recaptchakey, MobilePhone, HomePhone, OfficePhone, PostalCode, Address, Address2, City, State, Country, CallBackUrl, AudienceId, Level parameters. Whereas, the **UserSettings**, **Roles**, and **Permissions** objects are further contains parameters. In all of these parameters, the Email, Username, FirstName, LastName, Password, ConfirmPassword and UserSettings are required ones. 
  

The class name of the **createUserModel** is
```markdown
  CreateUserBindingModelAnonymous
```  
  
#### createUserModel object Parameters
  
![5](https://user-images.githubusercontent.com/110983629/188149707-d4207f75-f48d-464f-8593-bddcf2c38235.png)

![6](https://user-images.githubusercontent.com/110983629/188149741-e883e4dd-1d66-4e33-826f-1f31cb47bd81.png)

  
#### UserSettings object class name and Parameters   
  
![7](https://user-images.githubusercontent.com/110983629/188154817-2e3a29bf-ab3a-4d9b-b101-624283bc96ac.png)

#### Roles object class name and Parameters   
  
![8](https://user-images.githubusercontent.com/110983629/188154893-0e8f5100-4ce5-4832-90cb-8262c9d61bed.png)


#### Permissions object class name and Parameters     
  
![9](https://user-images.githubusercontent.com/110983629/188154938-64a5d381-2dc4-481c-9e98-b16b1b3fe571.png)

  
#### Explorer 

|Names|Description|
|-----|-----------|
|createUserModel (required)|[Models.CreateUserBindingModelAnonymous](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/create-user-binding-model-anonymous)| 
  
  
#### Responses 

The response of this endpoint service request contains the "ResponseType" object. The class name of the ResponseType object is 

```markdown 
 UserReturnModel
``` 
 
#### Response body-JSON  
```markdown 
{
  "Url": null,
  "Id": null,
  "UserName": null,
  "FullName": null,
  "FirstName": null,
  "LastName": null,
  "Email": null,
  "MobilePhone": null,
  "HomePhone": null,
  "OfficePhone": null,
  "PostalCode": null,
  "EmailConfirmed": null,
  "Lockout": null,
  "Level": null,
  "Address": null,
  "Address2": null,
  "City": null,
  "State": null,
  "Country": null,
  "JoinDate": null,
  "Roles": null,
  "Settings": null,
  "PasswordExpDate": null,
  "CustomDaysToExpired": null,
  "TwoFactorEnabled": null,
  "IsPasswordCreated": null
}
```

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

    
##### 'ResponseType' Object Parameters
The following table describe the parameters of the response type object:
  
|Names|Description|
|-----|-----------| 
|Url|URL of String Type|
|ID|Id of String Type|
|UserName|User Name of String Type|
|FullName|Full Name of user of String Type|
|FirstName|First Name of String Type|
|LastName|Last Name of String Type|
|Email|Email of String Type|
|MobilePhone|Phone Number of String Type|
|HomePhone|Home Phone of String Type|  
|OfficePhone|Office Phone of String Type|
|PostalCode|Postal Code of String Type|
|EmailConfirmed|bool value|
|Lockout|bool value|
|Level|int value|
|Address|Address of String Type|
|Address2|Address2 of String Type|
|City|City of String Type|
|State|State of String Type|
|Country|Country of String Type|
|JoinDate|Join Date of DateTime Type|
|Roles|Roles of List<String> Type|
|Settings|Dictionary<string, string>|
|PasswordExpDate|Password Expiration date of DateTime Type|
|CustomDaysToExpired|Int Type that allow to set a custom policy for days to expired|
|TwoFactorEnable|TwoFactorEnabled of Bool Type|
|IsPasswordCreated|IsPasswordCreated of bool type|
  
  

#### Explorer 

|Names|Description|
|-----|-----------|
|ResponseType|[Task<Models.UserReturnModel>](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/user-return-model)|
 
  
 
  
  
### Account Re Send Confirmation Email
#### Description  
The user will be able to resend the account confirmation email using this service endpoint. There is a chance that a network issue will prevent the user from receiving the confirmation email. The user can thus resend the account confirmation email using this service. The 'AccountController' class instance calls the 'AccountReSendConfirmationEmailAsync' function in order to do this. 
          
 
```markdown
 AccountReSendConfirmationEmailAsync(string userId,string audienceId)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
string userId = "userId0";
string audienceId = "audienceId8";

try
{
    object result = await accountController.AccountReSendConfirmationEmailAsync(userId, audienceId);
}
catch (ApiException e){};
```
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "accountController" object fails to resend confirmation email to the user that was anticipated to be returned. The user id and audience id are passed as a parameter to the `AccountReSendConfirmationEmailAsync` method. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
The userId and audienceId parameters for this API request are included. Both of them must be entered in order to process the request, and they are both of the String Type.
  
 
 ![10](https://user-images.githubusercontent.com/110983629/188165226-15843895-a9f0-4318-beae-0f28a0ab94ae.png)

 
#### Responses 
 
##### 'ResponseType' Object Parameters 
The response of this endpoint service request contains the "ResponseType" object. The `Task<object>` is the parameter that will return value whether the confirmation email is resent or not.
   
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|     
  
   
  
  
### Account Send Register Email
#### Description  
This service endpoint will send register email to the user who has created his account in the application. When the user enter his detail to get registered in the platform, he will receive the registration email. Through this process call, the registration email will be send to the respective user. For this purpose, the `AccountSendRegisterEmailAsync` method is called by creating in an instance of 'AccountController' class. 
   
 
```markdown
  AccountSendRegisterEmailAsync(string registerId)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
string registerId = "registerId4";

try
{
    object result = await accountController.AccountSendRegisterEmailAsync(registerId);
}
catch (ApiException e){};
```
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "accountController" object fails to send registration email to the user that was anticipated to be returned. In order to send the email, the register id will be used as a parameter that will be passed to the `AccountSendRegisterEmailAsync` method. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail   
The registerId is the required parameter of String_Type for making this process call successful to send registration email.  
  
![11](https://user-images.githubusercontent.com/110983629/188168338-2c9e4a73-f5aa-43bc-9ab4-2c5c01637564.png)

 
  
#### Responses 
 
##### 'ResponseType' Object Parameters 
The response of this endpoint service request contains the "ResponseType" object. The `Task<object>` is the parameter that will return value whether the register email is sent to the user or not.
   
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|     
  
  
  
  
### Users Login
#### Description  
The user can log into the system using this service endpoint by entering their username, password, and grant type as valid credentials. Valid credentials must be entered in order to safely access the user's account and to authenticate and authorise the user. In order to do this, an instance of the AccountController class is created from the API client, and the 'UsersLoginAsync' method is invoked. 
  
 
```markdown
   UsersLoginAsync(
    string username,
    string password,
    string grantType,
    string clientId = "f1fa7fff-92e4-4133-8d10-36868c4987ad")
  
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
string username = "nanosassa";
string password = "$RFVvfr4$RFVvfr4";
string grantType = "password";
string clientId = "f1fa7fff-92e4-4133-8d10-36868c4987ad";

try
{
    dynamic result = await accountController.UsersLoginAsync(username, password, grantType, clientId);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "accountController" object fails to login the user into his account that was anticipated to be returned. In order to login, the username, password, grant type and clientId will be used as a parameters that will be passed to the `UsersLoginAsync` method. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
There are four parameters for logging into the system in which username, password and grant type are required ones. The username can be the email address of the user, password will be the account password of the user, grantType will also be the password of the user. The clientid will be the audience id that is `"f1fa7fff-92e4-4133-8d10-36868c4987ad"` by default.    
   
![12](https://user-images.githubusercontent.com/110983629/188172744-7308deea-7c26-4208-824a-a6c5133f5831.png)
 
  
#### Responses 
 
##### 'ResponseType' Object Parameters 
The response of this endpoint service request contains the "ResponseType" object. The `Task<dynamic>` is the parameter that will return value whether the user logged into the system or not.
   
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|     
   
  
## API Endpoints
## Applications
### Applications Get
#### Description
This service endpoint will allow the user to get all applications details. For this purpose, the `ApplicationsGetAsync` method is called by creating an instance of ApplicationsController class which is accessed from the API client. 
  
```markdown  
ApplicationsController applicationsController = client.ApplicationsController;  
```   
  
```markdown
  ApplicationsGetAsync()
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
 try
{
    List<ApplicationReturnModel> result = await applicationsController.ApplicationsGetAsync();
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "ApplicationsController" object fails to get all applications details that was anticipated to be returned. In order to get applications, `ApplicationsGetAsync` method is used that does not take any parameter. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
This service endpoint does not take any parameter.   
   
 
#### Responses  

The response of this endpoint service request contains the `Task<List<Models.ApplicationReturnModel>>` object. The class name of the ResponseType object is 

```markdown 
 ApplicationReturnModel
``` 
 
#### Response body-JSON  
```markdown 
{
  "Id": null,
  "Description": null,
  "AudienceId": null,
  "AppId": null,
  "ApiKey": null,
  "ExpirationDate": null,
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
The following table describe the parameters of the response type object:
  
|Names|Description|
|-----|-----------| 
|Id|Id of int Type|
|Description|Description of String Type|
|AudienceId|AudienceId of String Type|
|AppId|Application id of String Type|
|ApiKey|App Key of String Type|
|ExpirationDate|Expiration date of DateTime|
|UserId|UserId of String Type|
 
#### Explorer 

|Names|Description|
|-----|-----------|
|ResponseType|[Task<List<Models.ApplicationReturnModel>>](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/application-return-model)|
 
  
### Applications Post
#### Description
This service endpoint will allow the user to create an application by adding its details. For this purpose, the `ApplicationsPostAsync` method is called by creating an instance of ApplicationsController class which is accessed from the API client. 
  
```markdown
  ApplicationsPostAsync(Models.CreateApplicationBindingModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
var model = new CreateApplicationBindingModel();
model.Description = "Description4";

try
{
    ApplicationReturnModel result = await applicationsController.ApplicationsPostAsync(model);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "ApplicationsController" object fails to create an application that was anticipated to be returned. In order to create application, model object is created which will be of `CreateApplicationBindingModel` type and description will be defined for the model. The `model` will be passed as a parameter to the `ApplicationsPostAsync` method in order to create an application. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
The **application model** object is the required parameter to enter that includes description(String_type), Id (int type), AppId (String type), ApiKey  (String type), ExpirationDate (DateTime type), and PermissionsAssigned object. The description parameter is required that cannot be null. The minimum length for the description is 2 and maximum length is 256.    

The class name of the application model is   
  
```markdown 
 CreateApplicationBindingModel
```   
  
  
#### Application model Object Parameters
  
![13](https://user-images.githubusercontent.com/110983629/188262165-26fd057d-5b3f-474a-904d-65804fbd1ebc.png)

  
The class name of the PermissionsAssigned object is   
  
```markdown 
  PermissionsBindingModel
```   
    
  
#### PermissionsAssigned Object Parameters  
  
![14](https://user-images.githubusercontent.com/110983629/188262175-db378b62-68a1-4ffa-bf16-01208be52243.png)

  
#### Explorer 

|Names|Description|
|-----|-----------|
|model (required)|[Models.CreateApplicationBindingModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/create-application-binding-model)|
  
 
#### Responses  

The response of this endpoint service request contains the `Task<Models.ApplicationReturnModel>` object. The class name of the ResponseType object is 

```markdown 
  ApplicationReturnModel
``` 
 
#### Response body-JSON  
```markdown 
 {
  "Id": null,
  "Description": null,
  "AudienceId": null,
  "AppId": null,
  "ApiKey": null,
  "ExpirationDate": null,
  "UserId": null
}
```

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

    
##### `Task<Models.ApplicationReturnModel>` Object Parameters

![15](https://user-images.githubusercontent.com/110983629/188262409-523dfbe2-15cf-4def-b018-90d3182e5124.png)

 
#### Explorer 

|Names|Description|
|-----|-----------|
|ResponseType|[Task<Models.ApplicationReturnModel>](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/application-return-model)|
 
  
 
  

### Applications Get 1
#### Description 
  
This service endpoint will allow the user to retrieve an application through its description. For this purpose, the `ApplicationsGet1Async` method is called by creating an instance of ApplicationsController class which is accessed from the API client. 
  
```markdown
  ApplicationsGet1Async(string description)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
string description = "description0";
try
{
    ApplicationReturnModel result = await applicationsController.ApplicationsGet1Async(description);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "ApplicationsController" object fails to retrieve application that was anticipated to be returned. In order to get application details, description of the application will be used as a parameter that will be passed to the `ApplicationsGet1Async` method. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

  
#### Parameters Detail  
The **Description** is the required parameter to enter for retrieving the specific application. It will be of String_type.   
  
![16](https://user-images.githubusercontent.com/110983629/188263209-9bc712b4-bc17-43ea-a079-5b80e1237deb.png)
 
#### Responses  

The response of this endpoint service request contains the `Task<Models.ApplicationReturnModel>` object. The class name of the Response object is 

```markdown 
 ApplicationReturnModel
``` 
 
#### Response body-JSON  
```markdown 
{
  "Id": null,
  "Description": null,
  "AudienceId": null,
  "AppId": null,
  "ApiKey": null,
  "ExpirationDate": null,
  "UserId": null
}
```

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

    
##### `Task<Models.ApplicationReturnModel>` Object Parameters

![17](https://user-images.githubusercontent.com/110983629/188263317-cac4da2f-7753-4a89-98f9-d19238cb17c7.png)

 
#### Explorer 

|Names|Description|
|-----|-----------|
|ResponseType|[Task<Models.ApplicationReturnModel>](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/application-return-model)|
    
  
  
  
### Applications Put
#### Description
    
This service endpoint will allow the user to update an application by editing its details. For this purpose, the `ApplicationsPutAsync` method is called by creating an instance of ApplicationsController class which is accessed from the API client. 
  
```markdown 
  ApplicationsPutAsync(
    string description,
    Models.CreateApplicationBindingModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
string description = "description0";
var model = new CreateApplicationBindingModel();
model.Description = "Description4";

try
{
    ApplicationReturnModel result = await applicationsController.ApplicationsPutAsync(description, model);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "ApplicationsController" object fails to update an application detail that was anticipated to be returned. In order to update an application, model object is created which will be of `CreateApplicationBindingModel` type and description of the updating application will be added in the model's description. The `model` will be passed as a parameter to the `ApplicationsPutAsync` method in order to update an application. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
The **model** object is the required parameter to enter that includes description(String_type), Id (int type), AppId (String type), ApiKey  (String type), ExpirationDate (DateTime type), and PermissionsAssigned object. The description parameter is required that cannot be null. The minimum length for the description is 2 and maximum length is 256. One other parameter for updating the application is the **description** that is the application name.   
  
  
![20](https://user-images.githubusercontent.com/110983629/188263898-f0fd54c0-c4c9-4b73-84eb-a45574ddc52a.png)

  

The class name of the application model which is also known as model is   
  
```markdown 
 CreateApplicationBindingModel
```   
  
  
#### Application model Object Parameters
 
![18](https://user-images.githubusercontent.com/110983629/188263792-48f7c7f5-0b11-49cb-81c4-7d7abb4968d6.png)

  
The class name of the PermissionsAssigned object is   
  
```markdown 
  PermissionsBindingModel
```      
  
#### PermissionsAssigned Object Parameters  
  
![19](https://user-images.githubusercontent.com/110983629/188263823-11264d8a-720a-4412-b64f-92b34372bf36.png)

  
#### Explorer 

|Names|Description|
|-----|-----------|
|model (required)|[Models.CreateApplicationBindingModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/create-application-binding-model)|
  
 
#### Responses  

The response of this endpoint service request contains the `Task<Models.ApplicationReturnModel>` object. The class name of the ResponseType object is 

```markdown 
  ApplicationReturnModel
``` 
 
#### Response body-JSON  
```markdown 
 {
  "Id": null,
  "Description": null,
  "AudienceId": null,
  "AppId": null,
  "ApiKey": null,
  "ExpirationDate": null,
  "UserId": null
}
```

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

    
##### `Task<Models.ApplicationReturnModel>` Object Parameters

![21](https://user-images.githubusercontent.com/110983629/188263998-b7241a70-ca7f-44a9-98af-de4154aa910d.png)

 
#### Explorer 

|Names|Description|
|-----|-----------|
|ResponseType|[Task<Models.ApplicationReturnModel>](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/application-return-model)|
 
  
 
  
 
### Applications Delete
#### Description
    
This service endpoint will allow the user to delete an application by accessing it through application name. For this purpose, the `ApplicationsDeleteAsync` method is called by creating an instance of ApplicationsController class which is accessed from the API client. 
  
```markdown 
  ApplicationsDeleteAsync(string description)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
string description = "description0";
try
{
    string result = await applicationsController.ApplicationsDeleteAsync(description);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "ApplicationsController" object fails to delete an application that was anticipated to be returned. In order to delete an application, description of the application will be used that is passed as a parameter to the `ApplicationsDeleteAsync` method. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
The **description** is the only required parameter used for deleting an application. It is basically the application id that is significantly associated to one application. 
  
![22](https://user-images.githubusercontent.com/110983629/188266381-551169cb-493a-4ff5-a3b2-812c602ffa21.png)


#### Responses  

The response of this endpoint service request contains the `Task<string>` object. It returns the value whether the application is deleted or not.  
  
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

   
### Applications Effective Permissions Get
#### Description

This service endpoint will allow the user to retrieve the application's permissions by entering the application name. For this purpose, the `ApplicationsEffectivePermissionsGetAsync` method is called by creating an instance of ApplicationsController class which is accessed from the API client.   
 
```markdown 
  ApplicationsEffectivePermissionsGetAsync(string appId)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
string appId = "appId6";
try
{
    List<ReturnEffecivePermissionV2> result = await applicationsController.ApplicationsEffectivePermissionsGetAsync(appId);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "ApplicationsController" object fails to retrieve an application's permissions that was anticipated to be returned. In order to get an application permissions, the appid will be used as a parameters that will be passed to the `ApplicationsEffectivePermissionsGetAsync` method.This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
The **appId** is the only required parameter for retrieving the specific permissions of the application. It will be of String_type.   
   
![23](https://user-images.githubusercontent.com/110983629/188266784-5e1b07c9-3122-4df8-8a7f-19887fbca38d.png)

 
#### Responses  

The response of this endpoint service request contains the `Task<List<Models.ReturnEffecivePermissionV2>>` object. It will be the list of permissions that are associated with the applications.
  
The class name of the `Task<List<Models.ReturnEffecivePermissionV2>>`  
```markdown 
  ReturnEffecivePermissionV2
``` 
 
#### Response body-JSON  
```markdown 
{
  "Permissions": null,
  "AudienceId": null
}
```

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

    
##### `Task<List<Models.ReturnEffecivePermissionV2>>` Object Parameters

![24](https://user-images.githubusercontent.com/110983629/188266892-1af9ea56-dc1a-4582-94c0-e08babcc724d.png)

#### Explorer 

|Names|Description|
|-----|-----------|
|ResponseType|[Task<List<Models.ReturnEffecivePermissionV2>>](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/return-effecive-permission-v2)|
 
  
### Applications Permissions Get
#### Description

This service endpoint will allow the user to retrieve the application's permissions direclty which are assigned by role name.  For this purpose, the `ApplicationsPermissionsGetAsync` method is called by creating an instance of ApplicationsController class which is accessed from the API client.   
 
```markdown  
  ApplicationsPermissionsGetAsync(string appid)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
string appid = "appid6";
try
{
    List<ReturnEffecivePermissionV2> result = await applicationsController.ApplicationsPermissionsGetAsync(appid);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "ApplicationsController" object fails to retrieve an application's permissions (which are assigned by role name) that was anticipated to be returned. In order to get an application permissions, the appid will be used as a parameters that will be passed to the `ApplicationsEffectivePermissionsGetAsync` method.This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
The **appId** is the only required parameter for retrieving the specific permissions assigned by the role name of the application. It will be of String_type.   
   
 
![25](https://user-images.githubusercontent.com/110983629/188267489-3781cc67-3996-48a1-a602-c70c7bcac05c.png)

 
#### Responses  

The response of this endpoint service request contains the `Task<List<Models.ReturnEffecivePermissionV2>>` object. It will be the list of permissions that are associated with the applications and also assigned by role name.
  
The class name of the `Task<List<Models.ReturnEffecivePermissionV2>>`  
```markdown 
  ReturnEffecivePermissionV2
``` 
 
#### Response body-JSON  
```markdown 
{
  "Permissions": null,
  "AudienceId": null
}
```

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

    
##### `Task<List<Models.ReturnEffecivePermissionV2>>` Object Parameters 

![26](https://user-images.githubusercontent.com/110983629/188267590-4980d536-13a6-482e-b984-daae632eabe4.png)

  

#### Explorer 

|Names|Description|
|-----|-----------|
|ResponseType|[Task<List<Models.ReturnEffecivePermissionV2>>](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/return-effecive-permission-v2)|
 
 
  
### Applications Permissions Post
#### Description 

This service endpoint will allow the user to assign permissions to the role of the application. In order to assign permissions, the role name will be used for significantly defining to which role that specific permissions is assigned. For this purpose, the `ApplicationsPermissionsPostAsync` method is called by creating an instance of ApplicationsController class which is accessed from the API client.  
  
```markdown 
  ApplicationsPermissionsPostAsync(
    string appid,
    Models.AssignPermisionRoleModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
string appid = "appid6";
var model = new AssignPermisionRoleModel();

try
{
    string result = await applicationsController.ApplicationsPermissionsPostAsync(appid, model);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "ApplicationsController" object fails to assign permissions to the specific role by role name that was anticipated to be returned. In order to assign permissions, model object and appid parameters will be passed to the `ApplicationsPermissionsPostAsync` method. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
The **model** object and **appid** are the two required parameters of this endpoint service call. Where the appid is the role name of String_type and model contains permissions object and TargetAudienceId. The audience id is optional to add which is of String_type.  
  
  
![27](https://user-images.githubusercontent.com/110983629/188268416-201853cc-ab74-4432-a60d-a4fb7e60b246.png)


The class name of the model object is
  
```markdown 
 AssignPermisionRoleModel
```   
  
#### model Object Parameters
 
![28](https://user-images.githubusercontent.com/110983629/188268480-453ad34e-162d-4298-ae53-c98cb8d4a1fa.png)

  
The class name of the Permissions object is   
  
```markdown 
  PermissionsBindingModel
```      
  
#### Permissions Object Parameters  

![29](https://user-images.githubusercontent.com/110983629/188268537-9be26796-d59f-4d17-bdcb-0678b0a7199b.png)

  
#### Explorer 

|Names|Description|
|-----|-----------|
|appid|Role name of String Type|  
|model (required)|[Models.AssignPermisionRoleModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/assign-permision-role-model)|
  
 
#### Responses  

The response of this endpoint service request contains the `Task<string>` object that will return the value whether the permissions are assigned or not to the respective role name.  
 

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

  
  
### Applications Renew
#### Description
    
This service endpoint will allow the user to renew an application by employing the application id. In order to do that the `ApplicationsRenewAsync` method is called by creating an instance of ApplicationsController class which is accessed from the API client. 
  
```markdown 
  ApplicationsRenewAsync(string appid)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/api-endpoints/applications/applications-renew)

#### Class-Object
```markdown
string appid = "appid6";

try
{
    ApplicationReturnModel result = await applicationsController.ApplicationsRenewAsync(appid);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "ApplicationsController" object fails to renew an application that was anticipated to be returned. In order to renew the application, the application id will be passed as a parameter to the `ApplicationsRenewAsync` method in order to renew the specific application. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
The **appid** parameter (String_type) is the only required parameter for renewing an application.  
  
![30](https://user-images.githubusercontent.com/110983629/188269178-fdf95074-b297-4108-b423-422ebfbc9b10.png)

#### Responses  

The response of this endpoint service request contains the `Task<Models.ApplicationReturnModel>` object that returns the application that is get renewed. 
 
#### Response body-JSON  
```markdown 
 {
  "Id": null,
  "Description": null,
  "AudienceId": null,
  "AppId": null,
  "ApiKey": null,
  "ExpirationDate": null,
  "UserId": null
}
```

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

The class name of the  response object "Task<Models.ApplicationReturnModel>" is
  
 ```markdown  
  ApplicationReturnModel
 ```
  
##### `Task<Models.ApplicationReturnModel>` Object Parameters
  
![31](https://user-images.githubusercontent.com/110983629/188269366-e5d8024e-b7f1-4322-98c3-b777a15fdc99.png)

 
  
#### Explorer 

|Names|Description|
|-----|-----------|
|ResponseType|[Task<Models.ApplicationReturnModel>](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/application-return-model)|
 

  
### Applications Permissions Delete
#### Description 
The user will be able to remove all the permissions connected to the role name using this service endpoint. The role name will be used to significantly access the roles whose permissions need to be deleted in order to eliminate permissions. For this purpose, the `ApplicationsPermissionsDeleteAsync` method is called by creating an instance of ApplicationsController class which is accessed from the API client. 
  
```markdown 
   ApplicationsPermissionsDeleteAsync(
    string appId,
    Models.DropPermisionRoleModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
string appId = "appId6";
var model = new DropPermisionRoleModel();
model.Permissions = new List<string>();
model.Permissions.Add("Permissions6");
model.Permissions.Add("Permissions7");

try
{
    string result = await applicationsController.ApplicationsPermissionsDeleteAsync(appId, model);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "ApplicationsController" object fails to delete permissions (that are associated with the specific role) which was anticipated to be returned. In order to delete permissions, the model object has been created that will be of `DropPermisionRoleModel` type. And all the permissions that needs to be removed will be added into the model object. The `ApplicationsPermissionsDeleteAsync` method will be executed to delete all those permissions from the specific application which is accessed through the appId. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
The **model** object and **appid** are the two required parameters of this endpoint service call. Where the appid is the role name of String_type and model contains permissions object which is of String_type.  The permissions object is actually the list of permissions that needs to be deleted.
  
  
![32](https://user-images.githubusercontent.com/110983629/188270057-855f35ef-5fba-4eda-a1a5-47c9985e2d6d.png)


The class name of the model object is
  
```markdown 
  DropPermisionRoleModel
```   
  
#### model Object Parameters

![33](https://user-images.githubusercontent.com/110983629/188270093-8ba2f2f9-071c-46e4-bb1c-258866d78cf4.png)
  
#### Explorer 

|Names|Description|
|-----|-----------|
|appid|Role name of String Type|  
|model (required)|[Models.DropPermisionRoleModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/drop-permision-role-model)|
  
 
#### Responses  

The response of this endpoint service request contains the `Task<string>` object that will return the value whether the permissions are deleted or not to the respective role name of the application.  
 

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

  
     
  
## API Endpoints
## Audiences 
### Audiences Get
#### Description
This service endpoint will allow the user to retrieve all the audiences that are active. For this purpose, the `AudiencesGetAsync` method is called by creating an instance of `AudiencesController` class which is accessed from the API client. 
  
```markdown  
 AudiencesController audiencesController = client.AudiencesController;
```   
  
```markdown
  AudiencesGetAsync()
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
try
{
    Audience result = await audiencesController.AudiencesGetAsync();
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "audiencesController" object fails to get all active audiences that was anticipated to be returned. In order to get audiences, `AudiencesGetAsync` method is used that does not take any parameter. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
This service endpoint does not take any parameter.   
   
 
#### Responses  

The response of this endpoint service request contains the `Task<Models.Audience>` object. The class name of the ResponseType object is 

```markdown 
  Audience
``` 
 
#### Response body-JSON  
```markdown 
  {
  "Id": null,
  "Description": null,
  "AudienceId": null,
  "SecretKey": null
} 
```

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

    
##### 'ResponseType' Object Parameters
The following table describe the parameters of the response type object:
  
|Names|Description|
|-----|-----------| 
|Id|Id of int Type|
|Description|Description of String Type|
|AudienceId|AudienceId of String Type|
|SecertKey|SecertKey of String Type|
 
 
#### Explorer 

|Names|Description|
|-----|-----------|
|ResponseType|[Task<Models.Audience>](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/audience)]

  
  
### Audiences Post
#### Description
This service endpoint will allow the user to create an audience by adding its details. For this purpose, the `AudiencesPostAsync` method is called by creating an instance of audiencesController class which is accessed from the API client. 
  
```markdown
  AudiencesPostAsync(Models.CreateAudienceBindingModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
var model = new CreateAudienceBindingModel();
model.Description = "Description4";

try
{
    Audience result = await audiencesController.AudiencesPostAsync(model);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "audiencesController" object fails to create an audience that was anticipated to be returned. In order to create audience, model object is created which will be of `CreateAudienceBindingModel` type and description will be defined for the model. The `model` will be passed as a parameter to the `AudiencesPostAsync` method in order to create an audience. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
The **model** object is required parameter to enter that includes Description(String_type), Roles (List of Strings), Permissions (List of Strings), Settings object, UsersDefaultSettings object, AudienceId (String type), and SecretKey (String type). The parameters of **model** object that are required to enter for creating audience includes Description, Settings, UserDefaultSettings. 

The class name of the model is   
  
```markdown 
  CreateAudienceBindingModel
```   
  
  
#### model Object Parameters
   
![34](https://user-images.githubusercontent.com/110983629/188271650-72bb5a86-a635-48f1-9ad0-22abe872310d.png)

  
####  Audience Settings class name and Object Parameters  

![35](https://user-images.githubusercontent.com/110983629/188271709-682d9cac-702f-4c26-b20f-b2f228c7729b.png)



####  User Default Settings class name and Object Parameters    
  
![36](https://user-images.githubusercontent.com/110983629/188271794-80157746-97c9-49ce-af7c-ca8a67abd1c6.png)

  
 ####  Audience class name and Object Parameters    
  
 ![37](https://user-images.githubusercontent.com/110983629/188271863-5cd05480-079e-4d89-ba60-dfea4ab56e1e.png)

  
#### Explorer 

|Names|Description|
|-----|-----------|
|model (required)|[Models.CreateAudienceBindingModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/create-audience-binding-model)|
  
 
#### Responses  

The response of this endpoint service request contains the `Task<Models.Audience>` object. The class name of the ResponseType object is 

```markdown 
   Audience
``` 
 
#### Response body-JSON  
```markdown 
  {
  "Id": null,
  "Description": null,
  "AudienceId": null,
  "SecretKey": null
}
```

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

    
##### `Task<Models.Audience>` Object Parameters

![38](https://user-images.githubusercontent.com/110983629/188271948-3a347a7e-8d7a-43da-be7d-f65b62e0f825.png)

  
#### Explorer 

|Names|Description|
|-----|-----------|
|ResponseType|[Task<Models.Audience>](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/audience)|
 
  

  
  
### Audiences Get 1
#### Description
This service endpoint will allow the user to retrieve an audience by entering audience id. For this purpose, the `AudiencesGet1Async` method is called by creating an instance of audiencesController class which is accessed from the API client. 
  
```markdown
 AudiencesGet1Async(string id)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
string id = "id0";
try
{
    Audience result = await audiencesController.AudiencesGet1Async(id);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "audiencesController" object fails to retrieve an audience that was anticipated to be returned. In order to get an audience detail, the audience id is passed as a parameter to the method `AudiencesGet1Async` so that only the audience whose id is passed will be retrieved in result. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
There is only one required parameter which is **id** that is associated with only one instance of audience. The user must need to enter the audience id for receiving the detail of the specific audience.  

![39](https://user-images.githubusercontent.com/110983629/188448981-b8ebdb07-c31a-410e-91d4-3a4c676c528c.png)
 
 
#### Responses  

The response of this endpoint service request contains the `Task<Models.Audience>` object. The class name of the ResponseType object is 

```markdown 
   Audience
``` 
 
#### Response body-JSON  
```markdown 
 {
  "Id": null,
  "Description": null,
  "AudienceId": null,
  "SecretKey": null
}
```

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

    
##### `Task<Models.Audience>` Object Parameters  
    
![40](https://user-images.githubusercontent.com/110983629/188449508-c863c9e4-78e1-4d1c-9c4c-8b0dd1afc6e6.png)

  
#### Explorer 

|Names|Description|
|-----|-----------|
|ResponseType|[Task<Models.Audience>](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/audience)|
 
 
  
  
  
### Audiences Put
#### Description
This service endpoint will allow the user to update an audience by adding its details. For this purpose, the `AudiencesPutAsync` method is called by creating an instance of audiencesController class which is accessed from the API client. 
  
```markdown
 AudiencesPutAsync(
    string id,
    Models.UpdateAudienceBindingModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
string id = "id0";
var model = new UpdateAudienceBindingModel();
model.Description = "Description4";

try
{
    Audience result = await audiencesController.AudiencesPutAsync(id, model);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "audiencesController" object fails to update an audience that was anticipated to be returned. In order to edit audience details, model object is created which will be of `UpdateAudienceBindingModel` type and description will be defined for the model. The `model`and audience id will be passed as a parameter to the `AudiencesPutAsync` method in order to update an audience. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
The **model** object is required parameter to enter that includes Description(String_type), Roles (List of Strings), Permissions (List of Strings), Settings object, UsersDefaultSettings object, AudienceId (String type), and SecretKey (String type). The parameters of **model** object that are required to enter for updating audience are **Description**, **Settings**, **UserDefaultSettings**. The id of audience is also passed as a separate parameter to this service endpoint for indicating which audience detail needs to be updated. 

The class name of the model is   
  
```markdown 
 UpdateAudienceBindingModel
```   
  
#### model Object Parameters 
  
![41](https://user-images.githubusercontent.com/110983629/188451966-2301f2bf-06c9-4a56-8198-905c718ca91e.png)
 
  
####  Audience Settings class name and Object Parameters  

![42](https://user-images.githubusercontent.com/110983629/188452272-f424c83c-4dc2-42a3-9578-17da4a015945.png)


####  User Default Settings class name and Object Parameters    
  
![43](https://user-images.githubusercontent.com/110983629/188452439-fe748e6c-e8f8-48ed-bb72-53d8fde8e851.png)

  
 ####  Audience class name and Object Parameters    

![44](https://user-images.githubusercontent.com/110983629/188452589-04bf9f6d-02ba-4560-a3ce-2f26043cd934.png)

 
  
#### Explorer 

|Names|Description|
|-----|-----------|
|model (required)|[Models.UpdateAudienceBindingModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/update-audience-binding-model)|
  
 
#### Responses  

The response of this endpoint service request contains the `Task<Models.Audience>` object. The class name of the ResponseType object is 

```markdown 
   Audience
``` 
 
#### Response body-JSON  
```markdown 
  {
  "Id": null,
  "Description": null,
  "AudienceId": null,
  "SecretKey": null
}
```

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

    
##### `Task<Models.Audience>` Object Parameters

![45](https://user-images.githubusercontent.com/110983629/188453174-b9595957-56df-4865-8f4a-4a27832dfbe3.png)
  
  
#### Explorer 

|Names|Description|
|-----|-----------|
|ResponseType|[Task<Models.Audience>](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/audience)|
 
  

  
### Audiences Delete
#### Description
This service endpoint will allow the user to delete an audience by entering audience id. For this purpose, the `AudiencesDeleteAsync` method is called by creating an instance of audiencesController class which is accessed from the API client. 
  
```markdown
  AudiencesDeleteAsync(string id)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown 
string id = "id0";
try
{
    string result = await audiencesController.AudiencesDeleteAsync(id);
}
catch (ApiException e){};
  
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "audiencesController" object fails to delete an audience that was anticipated to be returned. In order to remove an audience, the audience id is passed as a parameter to the method `AudiencesDeleteAsync` so that only the audience whose id is passed will be deleted in result. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
There is only one required parameter which is **id** that is associated with only one instance of audience. The user must need to enter the audience id for deleting the detail of the specific audience.   
  
![46](https://user-images.githubusercontent.com/110983629/188455410-7f03e977-b1be-442e-8719-7fa8907ab98b.png)

 
#### Responses  

The response of this endpoint service request contains the `Task<string>` object that will returns the value whether the respective audience is deleted or not.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

  
  
  
  
  
### Audiences Find
#### Description
This service endpoint will allow the user to retrieve an audience by entering audience description. For this purpose, the `AudiencesFindAsync` method is called by creating an instance of audiencesController class which is accessed from the API client. 
  
```markdown
  AudiencesFindAsync(string description)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
string description = "description0";
try
{
    Audience result = await audiencesController.AudiencesFindAsync(description);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "audiencesController" object fails to retrieve an audience details that was anticipated to be returned. In order to get an audience detail, the audience description is passed as a parameter to the method `AudiencesFindAsync` so that only the audience whose description is passed will be retrieved in result. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
There is only one required parameter which is **description** that is associated with only one instance of audience. The user must need to enter the audience description for receiving the detail of the specific audience.  
 
![47](https://user-images.githubusercontent.com/110983629/188457053-4d341165-a547-4bab-890f-625e9fc76172.png)

 
#### Responses  

The response of this endpoint service request contains the `Task<Models.Audience>` object. The class name of the ResponseType object is 

```markdown 
   Audience
``` 
 
#### Response body-JSON  
```markdown 
 {
  "Id": null,
  "Description": null,
  "AudienceId": null,
  "SecretKey": null
}
```

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

    
##### `Task<Models.Audience>` Object Parameters  
    
![40](https://user-images.githubusercontent.com/110983629/188449508-c863c9e4-78e1-4d1c-9c4c-8b0dd1afc6e6.png)

  
#### Explorer 

|Names|Description|
|-----|-----------|
|ResponseType|[Task<Models.Audience>](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/audience)|
 

 
### Audiences Default Settings Get
#### Description
This service endpoint will allow the user to retrieve the audiences default settings that will be automatically added to each new Audience when it is created. For this purpose, the `AudiencesDefaultSettingsGetAsync` method is called by creating an instance of audiencesController class which is accessed from the API client. 
  
```markdown
  AudiencesDefaultSettingsGetAsync()
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
try
{
    List<AudienceDefaultSetting> result = await audiencesController.AudiencesDefaultSettingsGetAsync();
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "audiencesController" object fails to retrieve the audiences default settings details that was anticipated to be returned. The list of audiences settings will get returned against this endpoint request. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail   
This endpoint does not take any parameter to process and retrieve the audiences default settings 
 
#### Responses  

The response of this endpoint service request contains the `Task<List<Models.AudienceDefaultSetting>>` object. The class name of the ResponseType object is 

```markdown 
  AudienceDefaultSetting
``` 
 
#### Response body-JSON  
```markdown 
 {
  "Key": null,
  "Value": null,
  "Description": null,
  "Level": null,
  "Enabled": false,
  "DataType": "DataType4"
} 
```

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

    
##### `Task<List<Models.AudienceDefaultSetting>>` Object Parameters  
     
![48](https://user-images.githubusercontent.com/110983629/188459594-2ed4c7d7-9e18-420f-b6a0-9bb4b15fd3f2.png)

  
#### Explorer 

|Names|Description|
|-----|-----------|
|ResponseType|[Task<List<Models.AudienceDefaultSetting>>](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/audience-default-setting)|
 
   
  
  
### Audiences Default Settings Put
#### Description
This service endpoint will allow the user to assign Default Settings that will be automatically added to each new Audience. For this purpose, the `AudiencesDefaultSettingsPutAsync` method is called by creating an instance of audiencesController class which is accessed from the API client. 
  
```markdown
 AudiencesDefaultSettingsPutAsync(Models.UpdateAudienceDefaultSettingBindingModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
var model = new UpdateAudienceDefaultSettingBindingModel();
try
{
    object result = await audiencesController.AudiencesDefaultSettingsPutAsync(model);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "audiencesController" object fails to assign default settings to the audiences that was anticipated to be returned. In order to assign default settings, model object is created which will be of `UpdateAudienceDefaultSettingBindingModel` type and will be passed as a parameter to the `AudiencesDefaultSettingsPutAsync` method in order to update an default settigns for each audience. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
The **model** object is the required parameter to enter that contains **audiencesDefaultSettings** object and **reset** parameters. The reset parameter will be of bool type for indicating whether the Audiences Default Settings should be reset or not.  
  
The class name of the model is   
  
```markdown 
  UpdateAudienceDefaultSettingBindingModel
```   
  
#### model Object Parameters 

![49](https://user-images.githubusercontent.com/110983629/188462227-e091dd74-2308-4b23-aefa-f5f8e894396e.png)

    
#### AudiencesDefaultSettings class name and Object Parameters  

![50](https://user-images.githubusercontent.com/110983629/188462471-937063de-1bb1-463c-a8f2-50e3af662f6e.png)
   
#### Explorer 

|Names|Description|
|-----|-----------|
|model (required)|[Models.UpdateAudienceDefaultSettingBindingModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/update-audience-default-setting-binding-model)|
  
 
#### Responses  

The response of this endpoint service request contains the `Task<object>` object that will indicate whether the audiences default setting is updated or not.
  

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

   
  
  
### Audiences Default Settings Post
#### Description
This service endpoint will allow the user to assign Default Settings that will be automatically added to each new Audience. For this purpose, the `AudiencesDefaultSettingsPostAsync` method is called by creating an instance of audiencesController class which is accessed from the API client. 
  
```markdown
AudiencesDefaultSettingsPostAsync(
    Models.AudienceDefaultSettingBindingModel model) 
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
var model = new AudienceDefaultSettingBindingModel();
model.Key = "Key6";
model.MValue = "Value0";

try
{
    object result = await audiencesController.AudiencesDefaultSettingsPostAsync(model);
}
catch (ApiException e){};
  
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "audiencesController" object fails to assign default settings to the audiences that was anticipated to be returned. In order to assign default settings, model object is created which will be of `AudienceDefaultSettingBindingModel` type and will be passed as a parameter to the `AudiencesDefaultSettingsPostAsync` method in order to add an default settigns for each audience. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
The **model** object is the required parameter to enter that contains Key (String_Type), MValue (String_Type), Description (String_Type), Level (String_Type), Enabled (bool), DataType (String_Type), Propagate (bool). The key. MValue are the required parameters for adding the default settings of the audiences. 
  
The class name of the model is   
  
```markdown 
   AudienceDefaultSettingBindingModel
```   
  
#### model Object Parameters 

![51](https://user-images.githubusercontent.com/110983629/188465544-77fddc7d-ecfc-42d9-be3a-fbe31b630467.png)

 
#### Explorer 

|Names|Description|
|-----|-----------|
|model (required)|[Models.AudienceDefaultSettingBindingModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/audience-default-setting-binding-model)|
  
 
#### Responses  

The response of this endpoint service request contains the `Task<object>` object that will indicate whether the audiences default setting is added or not.
  

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

 

  
  
  
    
### Audiences Default Settings Delete
#### Description
This service endpoint will allow the user to delete Default Settings that will be automatically added to each new Audience. Through this process, all the default settings will get removed. For this purpose, the `AudiencesDefaultSettingsDeleteAsync` method is called by creating an instance of audiencesController class which is accessed from the API client. 
  
```markdown
 AudiencesDefaultSettingsDeleteAsync(Models.AudienceDefaultSettingRemoveModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown[
var model = new AudienceDefaultSettingRemoveModel();
model.Key = "Key6";

try
{
    object result = await audiencesController.AudiencesDefaultSettingsDeleteAsync(model);
}
catch (ApiException e){};
  
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "audiencesController" object fails to delete default settings of the audiences that was anticipated to be returned. In order to remove default settings, model object is created which will be of `AudienceDefaultSettingRemoveModel` type and will be passed as a parameter to the `AudiencesDefaultSettingsDeleteAsync` method in order to remove the default settigns for each audience. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
The **model** object is the required parameter to enter that contains Key (String_Type), and Propagate (bool) parameters. The key is the required parameter for removing the default settings of the audiences. And the Propagate will specify whether this setting will be applied to all the audiences or not.
  
The class name of the model is   
  
```markdown 
   AudienceDefaultSettingRemoveModel
```   
  
#### model Object Parameters 

![52](https://user-images.githubusercontent.com/110983629/188467833-f8596a87-bd74-4d17-af68-08fde7b4945c.png)

 
#### Explorer 

|Names|Description|
|-----|-----------|
|model (required)|[Models.AudienceDefaultSettingRemoveModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/audience-default-setting-remove-model)|
  
 
#### Responses  

The response of this endpoint service request contains the `Task<object>` object that will indicate whether the audiences default setting is successfully deleted or not.
  

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|


  
  
  
  
  
    
### Audiences Settings Get
#### Description 
This service endpoint will allow the user to retrieve Settings of the audience by adding the audience id so that only the specific settings of an audience can be accessed. Through this process, all the default settings will get removed. For this purpose, the `AudiencesSettingsGetAsync` method is called by creating an instance of audiencesController class which is accessed from the API client. 
  
```markdown
 AudiencesSettingsGetAsync(string id)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
string id = "id0";
try
{
    object result = await audiencesController.AudiencesSettingsGetAsync(id);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "audiencesController" object fails to retrieve settings of an audiences that was anticipated to be returned. In order to get detail of the specific audience settings, audience id is used as a parameter that will be passed to the `AudiencesSettingsGetAsync` method. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail   
The **id** is the only required parameter which will indicate the audience id of String_type. 
   
![53](https://user-images.githubusercontent.com/110983629/188470579-ec73fae8-0c20-4f39-876b-d17883538e2f.png)

  
#### Responses  

The response of this endpoint service request contains the `Task<object>` object that will indicate whether the audiences setting is successfully retrieved or not.
  

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

  

  
   
### Audiences Settings Put
#### Description
This service endpoint will allow the user to update an audience settings by adding its details. In order to enable the TFA (Two Factor Authentication), configure your settings with the key for TFA and make its value true for receiving each time the code when you logged into the system. For enabling the audience callback url, enter the key as "NotificationUri" and make its value true. Moreover, for enabling the notifications, enter the key as "TFAProvider" and makes its value 'EmailCode' or 'PhoneCode' for receiving notifications.
For this purpose, the `AudiencesSettingsPutAsync` method is called by creating an instance of audiencesController class which is accessed from the API client. 
  
```markdown
 AudiencesSettingsPutAsync(
    string id,
    Models.AudienceSettingBindingModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
string id = "id0";
var model = new AudienceSettingBindingModel();
model.Key = "Key6";
model.MValue = "Value0";

try
{
    object result = await audiencesController.AudiencesSettingsPutAsync(id, model);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "audiencesController" object fails to update an audience setting that was anticipated to be returned. In order to edit audience setting, model object is created which will be of `AudienceSettingBindingModel` type and id of string type. Both of them will be passed as a parameter to the `AudiencesSettingsPutAsync` method in order to update an audience setting. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
The **model** object is required parameter to enter that includes Key (String_type), MValue (String_type), Description (String_type), Level (String_type), Enabled (bool) and DataType (String_type). Where the Key and MValue are required to enter for updating audience setting. In order to update the audience setting, you need to enter the audience id which is also a required parameter update the setting.
  
  
![55](https://user-images.githubusercontent.com/110983629/188476440-2be32eb6-cbae-42ee-941f-9fd7e28def1d.png)

  

The class name of the model is   
  
```markdown  
  AudienceSettingBindingModel
```   
  
#### model Object Parameters 
   
![54](https://user-images.githubusercontent.com/110983629/188476073-de3b24f2-4fcf-44f1-a416-ddd0446a1a34.png)

  
#### Explorer 

|Names|Description|
|-----|-----------|
|model (required)|[Models.AudienceSettingBindingModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/audience-setting-binding-model)|
  
 
#### Responses  

The response of this endpoint service request contains the `Task<object>` object that will returns the value whether the audience setting get updated or not.
 

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

     
 
### Audiences Settings Post
#### Description
The user can add or assign an audience setting by entering its data using this service endpoint. Configure your settings with the key for TFA and set its value to true for obtaining the code each time you connect into the system in order to enable TFA (two factor authentication). Enter the key "NotificationUri" with the value true to enable the audience callback url. Additionally, enter "TFAProvider" as the key to enable notifications and set "EmailCode" or "PhoneCode" as the value to receive notifications.
For this purpose, the `AudiencesSettingsPostAsync` method is called by creating an instance of audiencesController class which is accessed from the API client. 
  
```markdown
 AudiencesSettingsPostAsync(
    string id,
    Models.AudienceSettingBindingModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
string id = "id0";
var model = new AudienceSettingBindingModel();
model.Key = "Key6";
model.MValue = "Value0";

try
{
    object result = await audiencesController.AudiencesSettingsPostAsync(id, model);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "audiencesController" object fails to add/assign an audience setting that was anticipated to be returned. In order to add audience setting for a specific audience, model object is created which will be of `AudienceSettingBindingModel` type and id of string type. Both of them will be passed as a parameter to the `AudiencesSettingsPostAsync` method in order to add an audience setting. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
The **model** object is required parameter to enter that includes Key (String_type), MValue (String_type), Description (String_type), Level (String_type), Enabled (bool) and DataType (String_type). Where the Key and MValue are required to enter for adding audience setting. In order to add the audience setting, you need to enter the audience id which is also a required parameter adding the audience setting.
  
 
![56](https://user-images.githubusercontent.com/110983629/188479146-ef28afcd-c51c-4c6a-8153-2ce80018f46c.png)


The class name of the model is   
  
```markdown  
   AudienceSettingBindingModel
```   
  
#### model Object Parameters 
   
![57](https://user-images.githubusercontent.com/110983629/188479319-3d261e54-83bc-4779-b3e4-e7cc8b643ba2.png)

  
#### Explorer 

|Names|Description|
|-----|-----------|
|model (required)|[Models.AudienceSettingBindingModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/audience-setting-binding-model)|
  
 
#### Responses  

The response of this endpoint service request contains the `Task<object>` object that will returns the value whether the audience setting added or not.
 

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|


  
### Audiences Settings Delete
#### Description
This service endpoint will allow the user to delete the audience setting by entering the audience Id. For this purpose, the `AudiencesSettingsDeleteAsync` method is called by creating an instance of audiencesController class which is accessed from the API client. 
  
```markdown
 AudiencesSettingsDeleteAsync(
    string id,
    Models.AudienceSettingRemoveModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
string id = "id0";
var model = new AudienceSettingRemoveModel();
model.Key = "Key6";

try
{
    object result = await audiencesController.AudiencesSettingsDeleteAsync(id, model);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "audiencesController" object fails to delete an audience setting that was anticipated to be returned. In order to remove audience setting for a specific audience, model object is created which will be of `AudienceSettingRemoveModel` type and id of string type. Both of them will be passed as a parameter to the `AudiencesSettingsDeleteAsync` method in order to delete an audience setting. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
The **model** object is required parameter to enter that contains Key (String_type) attribute as a parameter. In order to delete the audience setting, you need to enter the audience id which is also a required parameter for removing the audience setting. 
  
![58](https://user-images.githubusercontent.com/110983629/188483558-84d0acc8-e12f-4a17-bf7d-f68540a47862.png)


The class name of the model is   
  
```markdown  
   AudienceSettingRemoveModel
```   
  
#### model Object Parameters 
 
![59](https://user-images.githubusercontent.com/110983629/188483662-8232ea40-7a14-4bd8-a292-59440f6c221f.png)

#### Explorer 

|Names|Description|
|-----|-----------|
|model (required)|[Models.AudienceSettingRemoveModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/audience-setting-remove-model)|
  
 
#### Responses  

The response of this endpoint service request contains the `Task<object>` object that will returns the value whether the audience setting get deleted or not.
 

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

  
  

  
  
### Audiences Users Default Settings Get
#### Description
This service endpoint will allow the user to retrieve the users default settings for the audiences. For this purpose, the `AudiencesUsersDefaultSettingsGetAsync` method is called by creating an instance of audiencesController class which is accessed from the API client. 
  
```markdown
  AudiencesUsersDefaultSettingsGetAsync(string id)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
string id = "id0";
try
{
    object result = await audiencesController.AudiencesUsersDefaultSettingsGetAsync(id);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "audiencesController" object fails to retrieve user's audience default setting that was anticipated to be returned. To get user's default setting details, id will be passed as a parameter to the `AudiencesUsersDefaultSettingsGetAsync` method. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
The **id** is the required parameter to enter which is audience id of String type.  
   
![60](https://user-images.githubusercontent.com/110983629/188485337-a0543685-c049-46b7-b021-6caacf1ccadb.png)

 
#### Responses  

The response of this endpoint service request contains the `Task<object>` object that will returns the value whether the user's audience default setting is shown to the user or not.
 

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

  
  
### Audiences Settings Getby Key
#### Description
By providing the key, the user can access this service endpoint to receive the audiences' default settings. For this purpose, the `AudiencesSettingsGetbyKeyAsync` method is called by creating an instance of audiencesController class which is accessed from the API client. 
  
```markdown
  AudiencesSettingsGetbyKeyAsync(string key)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
string key = "key0";
try
{
    object result = await audiencesController.AudiencesSettingsGetbyKeyAsync(key);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "audiencesController" object fails to retrieve user's audience default setting that was anticipated to be returned. To get default setting details, key will be passed as a parameter to the `AudiencesSettingsGetbyKeyAsync` method. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
The **key** is the required parameter to enter which is unique for each audience setting.
 
![61](https://user-images.githubusercontent.com/110983629/188487010-629b910e-0a4e-4627-8c6b-4b84718b5922.png)

 
#### Responses  

The response of this endpoint service request contains the `Task<object>` object that will returns the value whether audience default setting is shown to the user or not.
 

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

  
  
  
### Audiences Settings Updateby Key
#### Description
This service endpoint will allow the user to update an audience settings which will be accessed by audience key. For this purpose, the `AudiencesSettingsUpdatebyKeyAsync` method is called by creating an instance of audiencesController class which is accessed from the API client. 
  
```markdown
  AudiencesSettingsUpdatebyKeyAsync(Models.AudienceSettingBindingModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
var model = new AudienceSettingBindingModel();
model.Key = "Key6";
model.MValue = "Value0";

try
{
    object result = await audiencesController.AudiencesSettingsUpdatebyKeyAsync(model);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "audiencesController" object fails to update an audience setting that was anticipated to be returned. In order to edit audience setting, model object is created which will be of `AudienceSettingBindingModel` type that will be passed as a parameter to the `AudiencesSettingsUpdatebyKeyAsync` method in order to update an audience setting. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
The **model** object is required parameter to enter that includes Key (String_type), MValue (String_type), Description (String_type), Level (String_type), Enabled (bool) and DataType (String_type). Where the Key and MValue are required to enter for updating audience setting.  

The class name of the model is   
  
```markdown  
  AudienceSettingBindingModel
```   
  
#### model Object Parameters 
   
![62](https://user-images.githubusercontent.com/110983629/188488401-602661e0-bb1a-41dc-b46c-a8e87afdd190.png)

  
#### Explorer 

|Names|Description|
|-----|-----------|
|model (required)|[Models.AudienceSettingBindingModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/audience-setting-binding-model)|
  
 
#### Responses  

The response of this endpoint service request contains the `Task<object>` object that will returns the value whether the audience setting get updated or not.
 

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

  
  
  
  
  
### Audiences Roles Get
#### Description
By supplying the id, the user can use this service endpoint to receive the list of roles that have been allocated to the audience. In order to make informed decisions, it will enable users to learn about the roles that the audience plays. Create an instance of the audiencesController class, which is accessed through the API client, and call the 'AudiencesRolesGetAsync' method to do this.
  
```markdown
    AudiencesRolesGetAsync(string id)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
string id = "id0";

try
{
    object result = await audiencesController.AudiencesRolesGetAsync(id);
}
catch (ApiException e){};
```  


It will be included in the try and catch block to deal with any exceptions that could arise if the "audiencesController" object fails to retrieve an audience roles that was anticipated to be returned. The id is passed as a parameter to the `AudiencesRolesGetAsync` method for retrieving specific roles of audience. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
The **id** is the required parameter to enter which is of String type. It actually unique for each audience to retrieve roles.
 
![63](https://user-images.githubusercontent.com/110983629/188636442-48b9971c-d861-412f-b73e-c8eb5702fb1a.png)

  
#### Responses  

The response of this endpoint service request contains the `Task<object>` object that will returns the value whether the audience roles retrieved or not.
 

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

  
  
### Audiences Roles Post
#### Description
This service endpoint will allow the user to assign roles to the specific audience by adding audience id. For this purpose, the `AudiencesRolesPostAsync` method is called by creating an instance of audiencesController class which is accessed from the API client. 
  
```markdown
   AudiencesRolesPostAsync(
    string id,
    Models.AssignRoleToAudienceModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
string id = "id0";
var model = new AssignRoleToAudienceModel();
model.Roles = new List<string>();
model.Roles.Add("Roles9");
model.Roles.Add("Roles0");
model.Roles.Add("Roles1");

try
{
    await audiencesController.AudiencesRolesPostAsync(id, model);
}
catch (ApiException e){};
  
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "audiencesController" object fails to assign roles to the audience that was anticipated to be returned. In order to assign roles, model object is created which will be of `AssignRoleToAudienceModel` type that will be passed as a parameter to the `AudiencesRolesPostAsync` method in order to assign roles to an audience. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
The audience ID will be used for accessing the specific audience for which the roles needs to be assigned. The **model** object is also a required parameter to enter that contains the list of role names (List<string>) assigned to the audience.
  
![65](https://user-images.githubusercontent.com/110983629/188644529-9b7db97f-fd16-495f-bb1f-1b643869a570.png)


The class name of the model is   
  
```markdown  
   AssignRoleToAudienceModel
```   
  
#### model Object Parameters 

![64](https://user-images.githubusercontent.com/110983629/188639855-6e6beddb-828f-471f-9887-c2c6725f402c.png)

  
#### Explorer 

|Names|Description|
|-----|-----------|
|model (required)|[Models.AssignRoleToAudienceModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/assign-role-to-audience-model)|
  
 
#### Responses  

The response of this endpoint service request contains the `Task` that will returns the value whether the roles assigned to the audience or not.
 

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

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, there are 2 codes 400 and 404. Codes in the 4xx range indicate an error that failed given the information provided (e.g., bad request, Not found etc.) 
 
  
  
  
### Audiences Roles Delete
#### Description
This service endpoint will allow the user to delete roles that are assigned to the specific audience by adding audience id. For this purpose, the `AudiencesRolesDeleteAsync` method is called by creating an instance of audiencesController class which is accessed from the API client. 
  
```markdown
   AudiencesRolesDeleteAsync(
    string id,
    Models.AssignRoleToAudienceModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
string id = "id0";
var model = new AssignRoleToAudienceModel();
model.Roles = new List<string>();
model.Roles.Add("Roles9");
model.Roles.Add("Roles0");
model.Roles.Add("Roles1");

try
{
    await audiencesController.AudiencesRolesDeleteAsync(id, model);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "audiencesController" object fails to delete roles which are assigned the audience that was anticipated to be returned. In order to delete roles, id of string type and model object is created which will be of `AssignRoleToAudienceModel` type that will be passed as a parameter to the `AudiencesRolesDeleteAsync` method in order to delete roles from an audience. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
The audience ID will be used for accessing the specific audience for which the roles needs to be removed. The **model** object is also a required parameter to enter that contains the list of role names (List<string>) assigned to the audience.
  
![67](https://user-images.githubusercontent.com/110983629/188648815-52a4e67e-81c1-4830-a5ae-0e4c844340f0.png)
  
   
The class name of the model is   
  
```markdown  
 AssignRoleToAudienceModel
```   
  
  
#### model Object Parameters 

![66](https://user-images.githubusercontent.com/110983629/188648509-14d09d9d-6156-46ac-b7b4-992caa57d3c4.png)

  
#### Explorer 

|Names|Description|
|-----|-----------|
|model (required)|[Models.AssignRoleToAudienceModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/assign-role-to-audience-model)|
  
 
#### Responses  

The response of this endpoint service request contains the `Task` that will returns the value whether the roles associated with the audience get deleted or not.
 

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

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, there are 2 codes 400 and 404. Codes in the 4xx range indicate an error that failed given the information provided (e.g., bad request, Not found etc.) 
 
  
  
  
  
  
  
### Audiences Users Get
#### Description
This service endpoint will allow the user to retrieve the list of users that are assigned to the specific audience by adding audience id. For this purpose, the `AudiencesUsersGetAsync` method is called by creating an instance of audiencesController class which is accessed from the API client. 
  
```markdown
  AudiencesUsersGetAsync(string id)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
string id = "id0";
try
{
    object result = await audiencesController.AudiencesUsersGetAsync(id);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "audiencesController" object fails to retrieve users list which are assigned the audience that was anticipated to be returned. In order to get users list, audience id will be passed as a parameter to the `AudiencesUsersGetAsync` method in order to get list of users associated with the audience. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
The audience ID (String_type) will be used for accessing the specific audience for which the users needs to be shown.  
  
![68](https://user-images.githubusercontent.com/110983629/188653973-cb24454a-9b7e-4473-aa39-9da14d6657ef.png)
 
#### Responses  

The response of this endpoint service request contains the `Task<object>` that will returns the value whether the users list associated with the audience accessed or not.
 

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

   
  
  
  
  
### Audiences Users Post
#### Description
This service endpoint will allow the user to assign a user to the specific audience by adding audience id. For this purpose, the `AudiencesUsersPostAsync` method is called by creating an instance of audiencesController class which is accessed from the API client. 
  
```markdown
 AudiencesUsersPostAsync(string id, Models.UserAudienceBindingModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
string id = "id0";
var model = new UserAudienceBindingModel();
model.Users = new List<string>();
model.Users.Add("Users5");

try
{
    object result = await audiencesController.AudiencesUsersPostAsync(id, model);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "audiencesController" object fails to assign a user to the audience that was anticipated to be returned. In order to assign user, audience id and model object is created which will be of `UserAudienceBindingModel` type that will be passed as a parameter to the `AudiencesUsersPostAsync` method in order to assign user to the specific audience. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
The audience ID will be used for accessing the specific audience for which the user needs to be assigned. The **model** object is also a required parameter to enter that contains the list of user names (List<string>) assigned to the audience.
   
![69](https://user-images.githubusercontent.com/110983629/188658690-adc473f0-24cf-43f7-9175-37b0fdfd3a2b.png)


The class name of the model is   
  
```markdown  
   UserAudienceBindingModel
```   
  
#### model Object Parameters 
 
![70](https://user-images.githubusercontent.com/110983629/188659075-6892fa0b-af47-4a27-8227-ed1efe18a5d4.png)

  
#### Explorer 

|Names|Description|
|-----|-----------|
|model (required)|[Models.UserAudienceBindingModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/user-audience-binding-model)|
  
 
#### Responses  

The response of this endpoint service request contains the `Task<object>` that will returns the value whether the user assigned to the audience or not.
 

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
 
  

  
### Audiences Users Delete
#### Description
This service endpoint will allow the user to delete user that are assigned to the specific audience by accessing it through audience id. For this purpose, the `AudiencesUsersDeleteAsync` method is called by creating an instance of audiencesController class which is accessed from the API client. 
  
```markdown
   AudiencesUsersDeleteAsync(string id, Models.UserAudienceBindingModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
string id = "id0";
var model = new UserAudienceBindingModel();
model.Users = new List<string>();
model.Users.Add("Users5");

try
{
    string result = await audiencesController.AudiencesUsersDeleteAsync(id, model);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "audiencesController" object fails to delete user which are assigned the audience that was anticipated to be returned. In order to delete user, audience id and model object is created which will be of `UserAudienceBindingModel` type that will be passed as a parameter to the `AudiencesUsersDeleteAsync` method in order to delete user from an audience. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
The audience ID will be used for accessing the specific audience for which the users needs to be removed. The **model** object is also a required parameter to enter that contains the list of user names (List<string>) assigned to the audience.
   
  
![71](https://user-images.githubusercontent.com/110983629/188662320-0b712cb3-3b4d-4e12-ac61-e3f4a4a471ba.png)

   
The class name of the model is   
  
```markdown  
  UserAudienceBindingModel
```   
  
  
#### model Object Parameters 
 
![72](https://user-images.githubusercontent.com/110983629/188662593-014d66b1-a94b-4bfd-8f34-e85de93f8c3d.png)

  
  
#### Explorer 

|Names|Description|
|-----|-----------|
|model (required)|[Models.UserAudienceBindingModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/user-audience-binding-model)|
  
 
#### Responses  

The response of this endpoint service request contains the `Task<string>` that will returns the value whether the users associated with the audience get deleted or not.
 

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

  
  
  
  
  
  
  
  
  
  
### Audiences Permissions Get
#### Description
This service endpoint will allow the user to retrieve permissions which are assigned to the audience. For this purpose, the `AudiencesPermissionsGetAsync` method is called by creating an instance of ApplicationsController class which is accessed from the API client. 
  
```markdown
  
 AudiencesPermissionsGetAsync(string id)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
 string id = "id0";

try
{
    Audience result = await audiencesController.AudiencesPermissionsGetAsync(id);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "ApplicationsController" object fails to retrieve the list of permissions that was anticipated to be returned. In order to get permissions list, the audience id will be passed as a parameter to the `AudiencesPermissionsGetAsync` method. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
The **id** is the only one required parameter to enter which is the audience id unique for each audience.  
  
![73](https://user-images.githubusercontent.com/110983629/188670518-f1377598-35d9-4adb-ac4e-aa495fc52770.png)

 
#### Responses  

The response of this endpoint service request contains the `Task<Models.Audience>` object. The class name of the ResponseType object is 

```markdown 
   Audience
``` 
 
#### Response body-JSON  
```markdown 
 {
  "Id": null,
  "Description": null,
  "AudienceId": null,
  "SecretKey": null
}
```

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

    
##### `Task<Models.Audience>` Object Parameters
  
![74](https://user-images.githubusercontent.com/110983629/188671545-41898da6-51b0-4f0b-b17c-2159b3390040.png)

 
 
#### Explorer 

|Names|Description|
|-----|-----------|
|ResponseType|[Task<Models.Audience>](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/audience)|
 
  
  
   
### Audiences Permissions Post
#### Description
This service endpoint will allow the user to assign permissions to the specific audience by acessing the audience through the audience id. For this purpose, the `AudiencesPermissionsPostAsync` method is called by creating an instance of audiencesController class which is accessed from the API client. 
  
```markdown
  AudiencesPermissionsPostAsync(
    string id,
    Models.PermissionAudienceBindingModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
string id = "id0";
var model = new PermissionAudienceBindingModel();
model.Permissions = new List<string>();
model.Permissions.Add("Permissions6");
model.Permissions.Add("Permissions7");

try
{
    await audiencesController.AudiencesPermissionsPostAsync(id, model);
}
catch (ApiException e){};
  
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "audiencesController" object fails to assign permissions to the audience that was anticipated to be returned. In order to assign permissions, model object is created which will be of `PermissionAudienceBindingModel` type that will be passed as a parameter to the `AudiencesPermissionsPostAsync` method in order to assign roles to an audience. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
The audience ID (String_type) will be used for accessing the specific audience for which the permission needs to be assigned. The **model** object is also a required parameter to enter that contains the list of permission (List<string>) assigned to the audience.
  
 
![75](https://user-images.githubusercontent.com/110983629/188675875-e1111db3-a8f8-49ae-9eb5-1fa3231c95a1.png)


The class name of the model is   
  
```markdown  
    PermissionAudienceBindingModel
```   
  
#### model Object Parameters 

![76](https://user-images.githubusercontent.com/110983629/188676098-71cb8688-f77f-41a1-bb11-b76e9fd3b10f.png)

  
#### Explorer 

|Names|Description|
|-----|-----------|
|model (required)|[Models.PermissionAudienceBindingModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/permission-audience-binding-model)|
  
 
#### Responses  

The response of this endpoint service request contains the `Task` that will returns the value whether the permission assigned to the audience or not.
 

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

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, there are 2 codes 400 and 404. Codes in the 4xx range indicate an error that failed given the information provided (e.g., bad request, Not found etc.) 
 
 
  
  
  
  
  
### Audiences Permission Delete
#### Description
This service endpoint will allow the user to delete permission that are assigned to the specific audience by adding audience id. For this purpose, the `AudiencesPermissionsDeleteAsync` method is called by creating an instance of audiencesController class which is accessed from the API client. 
  
```markdown
  AudiencesPermissionsDeleteAsync(
    string id,
    Models.PermissionAudienceBindingModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
string id = "id0";
var model = new PermissionAudienceBindingModel();
model.Permissions = new List<string>();
model.Permissions.Add("Permissions6");
model.Permissions.Add("Permissions7");

try
{
    await audiencesController.AudiencesPermissionsDeleteAsync(id, model);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "audiencesController" object fails to delete permissions which are assigned the audience that was anticipated to be returned. In order to delete permissions, audience id of string type and model object is created which will be of `PermissionAudienceBindingModel` type that will be passed as a parameter to the `AudiencesPermissionsDeleteAsync` method in order to delete permissions from an audience. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
The audience ID will be used for accessing the specific audience for which the permissions needs to be removed. The **model** object is also a required parameter to enter that contains the list of permissions (List<string>) assigned to the audience.
   
![77](https://user-images.githubusercontent.com/110983629/188682235-b0e7c1ed-dfa2-4980-bf22-493fa6dd1729.png)

  
The class name of the model is   
  
```markdown  
 PermissionAudienceBindingModel
```   
  
  
#### model Object Parameters 

![78](https://user-images.githubusercontent.com/110983629/188682385-03aeddab-381d-4c2f-b1ba-17fee7be4bf5.png)

  
#### Explorer 

|Names|Description|
|-----|-----------|
|model (required)|[Models.PermissionAudienceBindingModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/permission-audience-binding-model)|
  
 
#### Responses  

The response of this endpoint service request contains the `Task` that will returns the value whether the permissions associated with the audience get deleted or not.
 

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

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, there are 2 codes 400 and 404. Codes in the 4xx range indicate an error that failed given the information provided (e.g., bad request, Not found etc.) 
 
  
  
  
  
## API Endpoints
## Permissions 
### Permissions Get
#### Description
This service endpoint will allow the user to retrieve all the permissions. For this purpose, the `PermissionsGetAsync` method is called by creating an instance of `PermissionsController` class which is accessed from the API client. 
  
```markdown  
   PermissionsController permissionsController = client.PermissionsController;
```   
  
```markdown
   PermissionsGetAsync()
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
try
{
    List<PermissionReturnModel> result = await permissionsController.PermissionsGetAsync();
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "permissionsController" object fails to get all permissions that was anticipated to be returned. In order to get permissions, `PermissionsGetAsync` method is used that does not take any parameter. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
This service endpoint does not take any parameter.   
   
 
#### Responses  

The response of this endpoint service request contains the `Task<List<Models.PermissionReturnModel>>` object. The class name of the ResponseType object is 

```markdown 
   PermissionReturnModel
``` 
 
#### Response body-JSON  
```markdown 
  {
  "Url": null,
  "Id": null,
  "Name": null,
  "Description": null
} 
```

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

    
##### 'ResponseType' Object Parameters
The following table describe the parameters of the response type object:
  
|Names|Description|
|-----|-----------| 
|Url|Url of int Type|
|Id|Id of String Type|
|Name|name of permission of String Type|
|Description|Description of String Type|
 
 
#### Explorer 

|Names|Description|
|-----|-----------|
|ResponseType|[Task<List<Models.PermissionReturnModel>>](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/permission-return-model)]

  
  
  
  
### Permissions Post
#### Description
This service endpoint will allow the user to create a new permission by adding its details. For this purpose, the `PermissionsPostAsync` method is called by creating an instance of PermissionsController class which is accessed from the API client. 
  
```markdown
   PermissionsPostAsync(Models.PermissionBindingModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
var model = new PermissionBindingModel();
model.Name = "Name8";
model.Description = "Description4";

try
{
    await permissionsController.PermissionsPostAsync(model);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "permissionsController" object fails to create permission that was anticipated to be returned. In order to create permission, model object is created which will be of `PermissionBindingModel` type and description will be defined for the model. The `model` will be passed as a parameter to the `PermissionsPostAsync` method in order to create the permission. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
The **model** object is required parameter to enter that includes Description(String_type), Name (String_type) as a two required parameters. The **Description** cannot be empty. Its minimum Length is 2 and maximum Length is 256. And the **Name** can be of min Length: 2 and Maximum Length: 128. 
  

The class name of the model is   
  
```markdown 
   PermissionBindingModel
```   
  
  
#### model (Permission model) Object Parameters
   
![79](https://user-images.githubusercontent.com/110983629/188876642-c993b88a-c194-4251-a9d2-917a26ffd4de.png)

   
#### Explorer 

|Names|Description|
|-----|-----------|
|model (required)|[Models.PermissionBindingModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/permission-binding-model)|
  
 
#### Responses  

The response of this endpoint service request contains the `Task` object. 
 
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

This endpoint service request may response codes to indicate the success or failure of an API request. In the above table, there is code 400. Codes in the 4xx range indicate an error that failed given the information provided (e.g., bad request) 
   
  
  
  
  
  
  
  
### Permissions Get 1
#### Description
This service endpoint will allow the user to retrieve the permissions by entering permission name. For this purpose, the `PermissionsGet1Async` method is called by creating an instance of **PermissionsController** class which is accessed from the API client. 
  
```markdown
 PermissionsGet1Async(string name)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
string name = "name0";
try
{
    PermissionReturnModel result = await permissionsController.PermissionsGet1Async(name);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the **permissionsController** object fails to retrieve the permission that was anticipated to be returned. In order to get permission detail, the permission name as a name is passed (as a parameter) to the method `PermissionsGet1Async` so that only the permission whose name is passed will be retrieved in result. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
There is only one required parameter which is **name** that belongs to the one instance of permission. The user must need to enter the permission name for receiving the detail of the specific permission.  
  
![80](https://user-images.githubusercontent.com/110983629/188879991-0483d3df-1b6e-48b4-b6c4-5a4976e0c5c1.png)

 
#### Responses  

The response of this endpoint service request contains the `Task<Models.PermissionReturnModel>` object. The class name of the ResponseType object is 

```markdown  
  PermissionReturnModel
``` 
 
#### Response body-JSON  
```markdown 
 {
  "Url": null,
  "Id": null,
  "Name": null,
  "Description": null
 }
```

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

    
##### `Task<Models.PermissionReturnModel>` Object Parameters  

![81](https://user-images.githubusercontent.com/110983629/188880578-02defd6e-fae4-4cfc-b757-59793d496f0d.png)

  
#### Explorer 

|Names|Description|
|-----|-----------|
|ResponseType|[Task<Models.PermissionReturnModel>](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/permission-return-model)|
 
 
  
  
  
  
### Permissions Put
#### Description
This service endpoint will allow the user to update a permission by editing its details. For this purpose, the `PermissionsPutAsync` method is called by creating an instance of PermissionsController class which is accessed from the API client. 
  
```markdown
  PermissionsPutAsync(
    string name,
    Models.PermissionBindingModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
string name = "name0";
var model = new PermissionBindingModel();
model.Name = "Name8";
model.Description = "Description4";

try
{
    string result = await permissionsController.PermissionsPutAsync(name, model);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "permissionsController" object fails to update permission that was anticipated to be returned. In order to update permission, model object is created which will be of `PermissionBindingModel` type and name and description will be defined for the model. The `model` will be passed as a parameter to the `PermissionsPutAsync` method in order to update the permission details. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
The **model** object is required parameter to enter that includes Description(String_type), Name (String_type) as a two required parameters. The **Description** cannot be empty. Its minimum Length is 2 and maximum Length is 256. And the **Name** can be of min Length: 2 and Maximum Length: 128. The permission id is also a required parameter to enter which will be of String_Type.
  
![83](https://user-images.githubusercontent.com/110983629/188883112-914b582d-2f27-4bb2-859f-4ac64916e8bc.png)


The class name of the model is   
  
```markdown 
    PermissionBindingModel
```   
  
  
#### model (Permission model) Object Parameters
  
![82](https://user-images.githubusercontent.com/110983629/188883183-e54bc2a9-3ec5-45eb-b7dd-46e2017c0865.png)

   
#### Explorer 

|Names|Description|
|-----|-----------|
|model (required)|[Models.PermissionBindingModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/permission-binding-model)|
  
 
#### Responses  

The response of this endpoint service request contains the `Task<string>` object which returns the value whether the permission detail get updated or not.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
  
  
  
  
  
  
### Permissions Delete
#### Description
This service endpoint will allow the user to delete a permission by entering its description. For this purpose, the `PermissionsDeleteAsync` method is called by creating an instance of **PermissionsController** class which is accessed from the API client. 
  
```markdown
   PermissionsDeleteAsync(
    string name,
    string audienceId = null)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
string name = "name0";
try
{
    string result = await permissionsController.PermissionsDeleteAsync(name, null);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "permissionsController" object fails to delete permission that was anticipated to be returned. In order to delete a permission, the name which is permission description and audience id will be passed as parameters to the `PermissionsDeleteAsync`.This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
The required parameters for this endpoint request includes **name** (String_type) which is the description of permission and **audience id** (String_type) which is guid in real.
  
![84](https://user-images.githubusercontent.com/110983629/188886151-298d8b49-51aa-465e-b1a9-9ebb9bce095c.png)

#### Responses  

The response of this endpoint service request contains the `Task<string>` object which returns the value whether the permission get deleted or not.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|


  
  
  
  
  
  
  
  
  
## API Endpoints
## Portal 
### Portal Portal 
#### Description
This service endpoint will allow the user to retrieve the documentation static files that are ready to be deployed. For this purpose, the `PortalPortalAsync` method is called by creating an instance of `PortalController` class which is accessed from the API client. 
  
```markdown  
   PortalController portalController = client.PortalController;
```   
  
```markdown
   PortalPortalAsync()
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
try
{
    object result = await portalController.PortalPortalAsync();
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the **portalController** object fails to retrieve all documentation files (which are ready to deploy) that was anticipated to be returned. In order to get permissions, `PortalPortalAsync` method is used that does not take any parameter. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
This service endpoint does not take any parameter.   
   
 
#### Responses  

The response of this endpoint service request contains the `Task<object>` that returns the documentation files ready to deploy.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

    

  
  
  
  
  
  
  
## API Endpoints
## Roles 
### Roles Get by Audience
#### Description
This service endpoint will allow the user to retrieve all the roles that includes the role id and role name. For this purpose, the `RolesGetByAudienceAsync` method is called by creating an instance of `RolesController` class which is accessed from the API client. 
  
```markdown  
   RolesController rolesController = client.RolesController;
```   
  
```markdown
   RolesGetByAudienceAsync()
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
try
{
    List<RoleReturnModel> result = await rolesController.RolesGetByAudienceAsync();
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the **rolesController** object fails to get all roles that was anticipated to be returned. In order to get roles, `RolesGetByAudienceAsync` method is used that does not take any parameter but retrieve all roles with respect to the audience. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
This service endpoint does not take any parameter.   
   
 
#### Responses  

The response of this endpoint service request contains the `Task<List<Models.RoleReturnModel>>` object. The class name of the ResponseType object is 

```markdown 
    RoleReturnModel
``` 
 
#### Response body-JSON  
```markdown 
   {
  "Id": null,
  "Name": null
  }
```

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

    
##### 'ResponseType' Object Parameters
 
![85](https://user-images.githubusercontent.com/110983629/188892462-5774f4a9-129a-46c6-b5c2-5a24b3b90561.png)

  
 
#### Explorer 

|Names|Description|
|-----|-----------|
|ResponseType|[Task<List<Models.RoleReturnModel>>](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/role-return-model)]

 

  
### Roles Get 
#### Description
This service endpoint will allow the user to retrieve the list of roles. For this purpose, the `RolesGetAsync` method is called by creating an instance of `RolesController` class which is accessed from the API client. 
  
```markdown
  RolesGetAsync()
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
try
{
    List<string> result = await rolesController.RolesGetAsync();
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the **rolesController** object fails to get the list of roles that was anticipated to be returned. In order to get roles, `RolesGetAsync` method is used that does not take any parameter but retrieve the list of roles. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
This service endpoint does not take any parameter.   
   
 
#### Responses  

The response of this endpoint service request contains the `Task<List<string>>` object that returns the list of string items which are roles actually.


#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

  
  
  
### Roles Post
#### Description
This service endpoint will allow the user to create a new role by adding its details. For this purpose, the `RolesPostAsync` method is called by creating an instance of `RolesController` class which is accessed from the API client. 
  
```markdown
    RolesPostAsync(Models.CreateRoleBindingModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
var model = new CreateRoleBindingModel();
model.Roles = new List<string>();
model.Roles.Add("Roles9");
model.Roles.Add("Roles0");
model.Roles.Add("Roles1");

try
{
    string result = await rolesController.RolesPostAsync(model);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the **rolesController** object fails to create role that was anticipated to be returned. In order to create role, model object is created which will be of `CreateRoleBindingModel` type and roles will be defined for the model. The `model` will be passed as a parameter to the `RolesPostAsync` method in order to create the roles. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
The **model** object is required object to enter that includes Roles(List<string>) as a parameter. The user can create multiple roles at a time by adding them in linear manner. 

The class name of the model is   
  
```markdown 
   CreateRoleBindingModel
```   
  
  
#### model (Permission model) Object Parameters
    
![86](https://user-images.githubusercontent.com/110983629/188898174-c3cf3ea0-a443-445a-9c5e-1777f11e4a49.png)


   
#### Explorer 

|Names|Description|
|-----|-----------|
|model (required)|[Models.CreateRoleBindingModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/create-role-binding-model)|
  
 
#### Responses  

The response of this endpoint service request contains the `Task<string>` object that returns the value whether the roles are created or not. 
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
  
  
  
  
  
### Roles Get 1
#### Description
This service endpoint will allow the user to retrieve the roles by entering role name. For this purpose, the `RolesGet1Async` method is called by creating an instance of **RolesController** class which is accessed from the API client. 
  
```markdown
  RolesGet1Async(string name)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
string name = "name0";

try
{
    RoleReturnModel result = await rolesController.RolesGet1Async(name);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the **rolesController** object fails to retrieve the role that was anticipated to be returned. In order to get role detail, the role name as a name is passed as a parameter to the method `RolesGet1Async` so that only the roles whose name is passed will be retrieved in result. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
There is only one required parameter which is **name** that belongs to the one instance of role. The user must need to enter the role name for receiving the detail of the specific role.  
   
![87](https://user-images.githubusercontent.com/110983629/188901257-1d65a67d-d8d4-4905-8614-5a25575f5aef.png)

 
#### Responses  

The response of this endpoint service request contains the `Task<Models.RoleReturnModel>` object. The class name of the ResponseType object is 

```markdown  
  RoleReturnModel
``` 
 
#### Response body-JSON  
```markdown 
 {
  "Id": null,
  "Name": null
}
```

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

    
##### `Task<Models.RoleReturnModel>` Object Parameters  
  
![88](https://user-images.githubusercontent.com/110983629/188901771-90dbf582-ec17-46f1-8f75-8d05631ab39f.png)

  
#### Explorer 

|Names|Description|
|-----|-----------|
|ResponseType|[Task<Models.RoleReturnModel>](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/role-return-model)|
 

  
  
  
  
  
### Roles Put
#### Description
This service endpoint will allow the user to update the role by entering role name. For this purpose, the `RolesPutAsync` method is called by creating an instance of **RolesController** class which is accessed from the API client. 
  
```markdown
 RolesPutAsync(
    string name,
    string newName)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
string name = "name0";
string newName = "newName4";

try
{
    string result = await rolesController.RolesPutAsync(name, newName);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the **rolesController** object fails to update the role that was anticipated to be returned. In order to edit role name, the role name as a name and new role name are passed as a parameter to the method `RolesPutAsync` so that only the role whose name is passed will be updated in result. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
There are two required parameters which are **name** and **newName** of string type. The user must need to enter the old role name for updating the specific role name. 

![89](https://user-images.githubusercontent.com/110983629/188903963-fc59a288-6367-47bd-9081-208ead078a6f.png)

 
#### Responses  

The response of this endpoint service request contains the `Task<string>` object that returns the value whether the new role name is updated or not.
  
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

  
  
### Roles Delete
#### Description
This service endpoint will allow the user to delete the role by entering role name. For this purpose, the `RolesDeleteAsync` method is called by creating an instance of **RolesController** class which is accessed from the API client. 
  
```markdown
  RolesDeleteAsync(string name)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
string name = "name0";
try
{
    string result = await rolesController.RolesDeleteAsync(name);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the **rolesController** object fails to delete the role that was anticipated to be returned. In order to remove role name, the role name as a name is passed as a parameter to the method `RolesDeleteAsync` so that only the role whose name is passed will be deleted in result. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
There is only one required parameters which are **name** of string type. This parameter indicates the role name for accessing the role. The user must need to enter the role name for deleting the specific one. 
 
![90](https://user-images.githubusercontent.com/110983629/188906559-a22d165b-1f41-482c-ba30-6f2ab6a0c204.png)

  
#### Responses  

The response of this endpoint service request contains the `Task<string>` object that returns the value whether the role name is deleted or not.
  
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

  
### Roles Tree Get
#### Description
This service endpoint will allow the user to retrieve the tree of Roles by entering the Parent name of role. For this purpose, the `RolesTreeGetAsync` method is called by creating an instance of **RolesController** class which is accessed from the API client. 
  
```markdown
 RolesTreeGetAsync(string name = null)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
try
{
    List<ComplexRole> result = await rolesController.RolesTreeGetAsync(null);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the `rolesController` object fails to retrieve the tree of roles that was anticipated to be returned. In order to get tree of role that come under the one parent name, `RolesTreeGetAsync` method is used that take the role name as a parameter. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
This service endpoint requires only one parameter which is **name** parent role name. It is optional for the user to enter the parent role name which is of String type.
   
![91](https://user-images.githubusercontent.com/110983629/188910899-6f21ad41-0224-4658-b86a-cf1d174f734b.png)

  
#### Responses  

The response of this endpoint service request contains the `Task<List<Models.ComplexRole>>` object. The class name of the ResponseType object is 

```markdown 
  ComplexRole
``` 
 
#### Response body-JSON  
```markdown 
 {
  "Name": null,
  "Id": null,
  "ChildRoles": null
}
```

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

    
##### 'ResponseType' Object Parameters 
  
![92](https://user-images.githubusercontent.com/110983629/188911662-3ca89304-43b5-4b3d-9a25-a1e144438a4c.png)

  
#### Explorer 

|Names|Description|
|-----|-----------|
|ResponseType|[Task<List<Models.ComplexRole>>](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/complex-role)|
  
  
  
  
  
  
  
  
### Roles Child Get
#### Description
This service endpoint will allow the user to retrieve the child roles by entering the parent name of role. For this purpose, the `RolesChildGetAsync` method is called by creating an instance of **RolesController** class which is accessed from the API client. 
  
```markdown
 RolesChildGetAsync(string name)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
string name = "name0";
try
{
    List<RoleReturnModel> result = await rolesController.RolesChildGetAsync(name);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the `rolesController` object fails to retrieve the child roles that was anticipated to be returned. In order to get child roles that come under the one parent name, `RolesChildGetAsync` method is used that take the parent role name as a parameter. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
This service endpoint requires only one parameter which is **name** parent role name. It is required for the user to enter the parent role name which is of String type.
  
![93](https://user-images.githubusercontent.com/110983629/188914074-e7deb317-95e1-4b23-b380-deb241c2dbb4.png)
  
  
#### Responses  

The response of this endpoint service request contains the `Task<List<Models.RoleReturnModel>>` object. The class name of the ResponseType object is 

```markdown 
  RoleReturnModel
``` 
 
#### Response body-JSON  
```markdown 
 {
  "Id": null,
  "Name": null
}
```

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

    
##### 'ResponseType' Object Parameters 
  
![94](https://user-images.githubusercontent.com/110983629/188914501-28be8707-a68c-4638-adc0-6d05fec96ec4.png)

  
  
#### Explorer 

|Names|Description|
|-----|-----------|
|ResponseType|[Task<List<Models.RoleReturnModel>>](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/role-return-model)|
  
  
  
  
  
  
  
  
  
### Roles Effective Permissions Get by Id
#### Description
This service endpoint will allow the user to retrieve the effectivePermissions by entering the role ID. For this purpose, the `RolesEffectivePermissionsGetByIdAsync` method is called by creating an instance of **RolesController** class which is accessed from the API client. 
  
```markdown
 RolesEffectivePermissionsGetByIdAsync(
    string id)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
string id = "id0";
try
{
    List<Permission> result = await rolesController.RolesEffectivePermissionsGetByIdAsync(id);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the `rolesController` object fails to retrieve the effective permissions that was anticipated to be returned. In order to get effective permissions, `RolesEffectivePermissionsGetByIdAsync` method is used that takes the role id as a parameter. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
This service endpoint requires only one parameter which is role id **id** unique for each role. It is required for the user to enter the role id which is of String type for retrieving the effective permissions.
  
![95](https://user-images.githubusercontent.com/110983629/188917187-a6910121-1ff3-4ddd-b91e-b2865f70a947.png)

  
#### Responses  

The response of this endpoint service request contains the `Task<List<Models.Permission>>` object. The class name of the ResponseType object is 

```markdown 
  Permission
``` 
 
#### Response body-JSON  
```markdown 
 {
  "Id": null,
  "Name": null,
  "Description": null
}
```

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

    
##### 'Task<List<Models.Permission>>' Object Parameters 
   
![96](https://user-images.githubusercontent.com/110983629/188917751-bd6ca709-f0a9-4f3f-9de9-1c757b9083e8.png)
  
  
#### Explorer 

|Names|Description|
|-----|-----------|
|ResponseType|[Task<List<Models.Permission>>](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/permission)|
  

  
  
### Roles Effective Permissions Get  
#### Description
This service endpoint will allow the user to retrieve the effectivePermissions by entering the role name. For this purpose, the `RolesEffectivePermissionsGetAsync` method is called by creating an instance of **RolesController** class which is accessed from the API client. 
  
```markdown
  RolesEffectivePermissionsGetAsync(string name)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
string name = "name0";
try
{
    List<ReturnEffecivePermissionV2> result = await rolesController.RolesEffectivePermissionsGetAsync(name);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the `rolesController` object fails to retrieve the effective permissions that was anticipated to be returned. In order to get effective permissions, `RolesEffectivePermissionsGetAsync` method is used that takes the role name as a parameter. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
This service endpoint requires only one parameter which is role name **name** unique for each role. It is required for the user to enter the role name which is of String type for retrieving the effective permissions.
  
 
![97](https://user-images.githubusercontent.com/110983629/188919378-a399c807-41ff-44b3-9906-749122e56b8c.png)

  
#### Responses  

The response of this endpoint service request contains the `Task<List<Models.ReturnEffecivePermissionV2>>` object. The class name of the ResponseType object is 

```markdown 
   ReturnEffecivePermissionV2
``` 
 
#### Response body-JSON  
```markdown 
{
  "Permissions": null,
  "AudienceId": null
}
```

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

    
##### 'Task<List<Models.ReturnEffecivePermissionV2>>' Object Parameters 
  
![97](https://user-images.githubusercontent.com/110983629/188920016-262b82db-b9be-467e-8c3a-56d6d4c1e080.png)

  
#### Explorer 

|Names|Description|
|-----|-----------|
|ResponseType|[Task<List<Models.ReturnEffecivePermissionV2>>](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/return-effecive-permission-v2)|

  
  
### Roles Permissions Get 
#### Description
This service endpoint will allow the user to retrieve the direct permissions which are assigned by role name. For this purpose, the `RolesPermissionsGetAsync` method is called by creating an instance of **RolesController** class which is accessed from the API client. 
  
```markdown
 RolesPermissionsGetAsync(string name)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
string name = "name0";
try
{
    List<ReturnEffecivePermissionV2> result = await rolesController.RolesPermissionsGetAsync(name);
}
catch (ApiException e){};
  
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the `rolesController` object fails to retrieve the direct permissions that was anticipated to be returned. In order to get direct permissions, `RolesPermissionsGetAsync` method is called that takes the role name as a parameter. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
This service endpoint requires only one parameter which is role name **name** unique for each role. It is required for the user to enter the role name which is of String type for retrieving the direct permissions which are associated by the role name.
  
![98](https://user-images.githubusercontent.com/110983629/188922141-0275902b-8f2e-4338-a080-19c9012c817c.png)

  
#### Responses  

The response of this endpoint service request contains the `Task<List<Models.ReturnEffecivePermissionV2>>` object. The class name of the ResponseType object is 

```markdown 
   ReturnEffecivePermissionV2
``` 
 
#### Response body-JSON  
```markdown 
 {
  "Permissions": null,
  "AudienceId": null
}
```

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

    
##### 'Task<List<Models.ReturnEffecivePermissionV2>>' Object Parameters 
 
![99](https://user-images.githubusercontent.com/110983629/188922932-a26c50fa-5d3c-4805-8a42-500a5f0f9698.png)

  
#### Explorer 

|Names|Description|
|-----|-----------|
|ResponseType|[Task<List<Models.ReturnEffecivePermissionV2>>](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/return-effecive-permission-v2)|
 
  
  
### Roles Permissions Post 
#### Description
This service endpoint will allow the user to assign permissions to a role by accessing it through the role name. You can retrieve a role by entering the role name that can be used as an identifier. For this purpose, the `RolesPermissionsPostAsync` method is called by creating an instance of **RolesController** class which is accessed from the API client. 
  
  
```markdown
    RolesPermissionsPostAsync(
    string name,
    Models.AssignPermisionRoleModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
string name = "name0";
var model = new AssignPermisionRoleModel();
try
{
    string result = await rolesController.RolesPermissionsPostAsync(name, model);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the `rolesController` object fails to assign permission to the role that was anticipated to be returned. In order to assign permissions, the model object of `AssignPermisionRoleModel` class used and will be passed as a parameter to `RolesPermissionsPostAsync` method along with the role name. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
This service endpoint requires two parameters which are role name **name** unique for each role and **model** object. It is required for the user to enter the role name which is of String type for accessing the specific role. The **model** object contains the list of permissions and audience id for assigning the permissions to the specific role of an application whose id is included in the model object.
  
![100](https://user-images.githubusercontent.com/110983629/189115179-84a898d8-b705-4968-bdcc-e3c541c643b4.png)

  
The class name of **model** object is:
 
```markdown
  AssignPermisionRoleModel
```
  
  
#### Model object Parameters
  
![101](https://user-images.githubusercontent.com/110983629/189115466-5f9c7cf1-8590-4bad-bf9e-343adb29897b.png)

#### Permissions object class name and Parameters
  
  
![102](https://user-images.githubusercontent.com/110983629/189115652-4a3227b5-82b0-46b9-abbc-408969e3f939.png)

  
  
#### Responses  

The response of this endpoint service request contains the `Task<string>` object that returns the value whether the permissions assigned to the specific role of the application or not. 

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

 
  
  
### Roles Permissions Delete
#### Description
This service endpoint will allow the user to delete the list of permissions by entering the role name. Through this process call, only those permissions will get deleted that are associated with a role whose name is entered. For this purpose, the `RolesPermissionsDeleteAsync` method is called by creating an instance of **RolesController** class which is accessed from the API client.  
  
```markdown
  RolesPermissionsDeleteAsync(
    string name,
    Models.DropPermisionRoleModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
string name = "name0";
var model = new DropPermisionRoleModel();
model.Permissions = new List<string>();
model.Permissions.Add("Permissions6");
model.Permissions.Add("Permissions7");

try
{
    string result = await rolesController.RolesPermissionsDeleteAsync(name, model);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the **rolesController** object fails to delete the list of permissions that was anticipated to be returned. In order to remove permissions, the role name as a name is passed as a parameter to the method `RolesPermissionsDeleteAsync` along with the **model** object of `DropPermisionRoleModel` class. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
There is two required parameters which includes role name as **name**  of string type and **model** object. The user must need to enter the role name for deleting the specific list of permissions. The user also also add the audience id which is optional parameter to add for this process call. 
  
![103](https://user-images.githubusercontent.com/110983629/189119771-4ed2ce6d-c331-42f8-bc14-c6fd441e109a.png)

The class name of the **model** object is  
  
```markdown
  DropPermisionRoleModel
 ```
#### Model object parameters
  
![104](https://user-images.githubusercontent.com/110983629/189120054-8b874fcd-2605-4c6a-b58c-39cfbd11c9a4.png)
  
#### Responses  

The response of this endpoint service request contains the `Task<string>` parameter that returns the value whether the list of permissions get deleted or not.
  
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

  
  
  
  
### Roles Child Post
#### Description
This service endpoint will allow the user to create a child role through the parent role. You must need to access the parent role for creating child roles. For this purpose, the `RolesChildPostAsync` method is called by creating an instance of `RolesController` class which is accessed from the API client. 
  
```markdown
   RolesChildPostAsync(
    Models.CreateChildRoleBindingModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
var model = new CreateChildRoleBindingModel();
model.ChildRoles = new List<string>();
model.ChildRoles.Add("ChildRoles6");
model.ParentRoleName = "ParentRoleName0";

try
{
    object result = await rolesController.RolesChildPostAsync(model);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the **rolesController** object fails to create child roles that was anticipated to be returned. In order to create child roles, **model** object is created which will be of `CreateChildRoleBindingModel` type and the list of string type needs to created for adding the child roles that will be defined for the **model** object. The `model` will be passed as a parameter to the `RolesChildPostAsync` method in order to create the child roles. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
The **model** object is required object to enter that includes ChildRoles(List<string>) and ParentRoleName (String type). The user can add multiple child roles as many as he want against one parent role name.  

The class name of the model is   
  
```markdown 
    CreateChildRoleBindingModel
```   
  
#### model Object Parameters
  
![105](https://user-images.githubusercontent.com/110983629/189124366-01e1c612-54b3-49d5-bc50-258112085184.png)

   
#### Explorer 

|Names|Description|
|-----|-----------|
|model (required)|[Models.CreateChildRoleBindingModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/create-child-role-binding-model)|
  
 
#### Responses  

The response of this endpoint service request contains the `Task<object>` object that returns the value whether the child roles are created or not for a parent role. 
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
  
 
  
### Roles Child Delete
#### Description
This service endpoint will allow the user to delete the list of child roles by entering the parent role name. Through this process call, only those child roles will get deleted that are associated with a parent role whose name is entered. For this purpose, the `RolesChildDeleteAsync` method is called by creating an instance of **RolesController** class which is accessed from the API client.  
  
```markdown
   RolesChildDeleteAsync(Models.ChildRoleBindingModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
var model = new ChildRoleBindingModel();
model.ChildRoles = new List<string>();
model.ChildRoles.Add("ChildRoles6");
model.ParentRoleName = "ParentRoleName0";

try
{
    string result = await rolesController.RolesChildDeleteAsync(model);
}
catch (ApiException e){}; 
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the **rolesController** object fails to delete the list of child roles that was anticipated to be returned. In order to remove child roles, the parent role name as a name is added into the model's parent role name. And set the child roles that you wanted to delete. This model will pass to the `RolesChildDeleteAsync` method for deleting the child roles.
  

#### Parameters Detail  
There is one required object **model** which contains child role as **ChildRoles** (list of Strings) and **ParentRoleName** (String type). The user must need to enter the parent role name for which he wanted to delete the child roles. 
     
  
The class name of the **model** object is  
  
```markdown
   ChildRoleBindingModel
 ```
#### Model object parameters
  
![106](https://user-images.githubusercontent.com/110983629/189144230-5d3d0faf-649d-408f-abe6-4a09f5f7dfd8.png)

  
#### Explorer 

|Names|Description|
|-----|-----------|
|model (required)|[Models.ChildRoleBindingModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/child-role-binding-model)|
  
  
#### Responses  

The response of this endpoint service request contains the `Task<string>` parameter that returns the value whether the list of child roles get deleted or not.
  
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

 

  
  
  
  
### Roles Default Settings Put
#### Description 
This service endpoint will allow the user to modify User Default Setting by entering the role name. As it is define that the role name is an identifier for a specific list of roles. It can also be used for updating the default setting of the user. For this purpose, the `RolesDefaultSettingsPutAsync` method is called by creating an instance of **RolesController** class which is accessed from the API client.   
  
  
```markdown
   RolesDefaultSettingsPutAsync(
    string name,
    Models.UserDefaultSettingBindingModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
string name = "name0";
var model = new UserDefaultSettingBindingModel();
model.Key = "string";
model.MValue = "string";
model.AudienceId = 1;
model.Description = "string";
model.Level = "string";
model.Enabled = true;
model.DataType = "string";
model.Propagate = false;

try
{
    object result = await rolesController.RolesDefaultSettingsPutAsync(name, model);
}
catch (ApiException e){};
```  
It will be included in the try and catch block to deal with any exceptions that could arise if the `rolesController` object fails to update default settings of the user that was anticipated to be returned. In order to update default settings, model object is created which will be of `UserDefaultSettingBindingModel` type and will be passed as a parameter to the `RolesDefaultSettingsPutAsync` method in order to update an default settings for the user through the role name. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.    

#### Parameters Detail  
There are two required parameters **name** and **model** object where the name will be role name of string type and model object contains the Key (string_type), MValue (string_type), AudienceId (integer_type), Description (string_type), Level (string_type), Enabled (Boolean), DataType (string_type) and Propagate (Boolean). The values of these parameters are unique for each user and the user can modify them if needed by accessing them through the role name. 
  
  
![107](https://user-images.githubusercontent.com/110983629/189154382-b9528127-5cc7-43c9-b651-2ed7198186dc.png)

  
The class name of the model is   
  
```markdown 
   UserDefaultSettingBindingModel
```   
  
#### model Object Parameters 
 
![108](https://user-images.githubusercontent.com/110983629/189154736-bd887433-1090-4eea-a2ed-e10c2c72a1f3.png)

   
#### Explorer 

|Names|Description|
|-----|-----------|
|model (required)|[Models.UserDefaultSettingBindingModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/user-default-setting-binding-model)|
  
 
#### Responses  

The response of this endpoint service request contains the `Task<object>` that will indicate whether the user default setting is updated or not.
  

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

 
  
  
  
### Roles Default Settings Post
#### Description 
This service endpoint will allow the user to assign Default Settings to all Users in a Role. As it is define that the role name is an identifier for a specific list of roles. It can also be used for assigning the default setting of all the user. For this purpose, the `RolesDefaultSettingsPostAsync` method is called by creating an instance of **RolesController** class which is accessed from the API client.   
  
  
```markdown
  RolesDefaultSettingsPostAsync(
    string name,
    Models.UserDefaultSettingBindingModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
string name = "name0";
var model = new UserDefaultSettingBindingModel();
model.Key = "string";
model.MValue = "string";
model.AudienceId = 1;
model.Description = "string";
model.Level = "string";
model.Enabled = true;
model.DataType = "string";
model.Propagate = false;

try
{
    object result = await rolesController.RolesDefaultSettingsPostAsync(name, model);
}
catch (ApiException e){};
```  
  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the `rolesController` object fails to assign default settings of the users that was anticipated to be returned. In order to assign default settings, model object is created which will be of `UserDefaultSettingBindingModel` type and will be passed as a parameter to the `RolesDefaultSettingsPostAsync` method in order to assign the default settings for the users through the role name. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.    

#### Parameters Detail  
There are two required parameters **name** and **model** object where the name will be role name of string type and model object contains the Key (string_type), MValue (string_type), AudienceId (integer_type), Description (string_type), Level (string_type), Enabled (Boolean), DataType (string_type) and Propagate (Boolean). The values of these parameters are unique for each user and by this process call, the default setting will be assigned to all the users through the role name. 
  
![109](https://user-images.githubusercontent.com/110983629/189158525-d65b0929-5b7d-4286-b3bc-c3d423412121.png)

   
The class name of the model is   
  
```markdown 
    UserDefaultSettingBindingModel
```   
  
#### model Object Parameters 
  
![110](https://user-images.githubusercontent.com/110983629/189158704-9c5ccd07-7c6d-4a2b-b782-4b573a04346f.png)

   
#### Explorer 

|Names|Description|
|-----|-----------|
|model (required)|[Models.UserDefaultSettingBindingModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/user-default-setting-binding-model)|
  
 
#### Responses  

The response of this endpoint service request contains the `Task<object>` that will indicate whether default setting is assigned to all users or not.

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

  
  
  
  
  
  
  
  
  
### Roles Default Settings Delete
#### Description 
This service endpoint will allow the user to delete user Default Settings in a Role. As it is define that the role name is an identifier for a specific list of roles. It can also be used for removing the default setting of the user. For this purpose, the `RolesDefaultSettingsDeleteAsync` method is called by creating an instance of **RolesController** class which is accessed from the API client.   
  
  
```markdown
  RolesDefaultSettingsDeleteAsync(
    string name,
    Models.UserDefaultSettingRemoveModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
string name = "name0";
var model = new UserDefaultSettingRemoveModel();
model.Key = "Key6";

try
{
    object result = await rolesController.RolesDefaultSettingsDeleteAsync(name, model);
}
catch (ApiException e){};
```  
  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the `rolesController` object fails to delete default settings of the user that was anticipated to be returned. In order to remove default settings, model object is created which will be of `UserDefaultSettingRemoveModel` type and will be passed as a parameter to the `RolesDefaultSettingsDeleteAsync` method in order to delete the default settings for the user through the role name. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.    

#### Parameters Detail  
There are two required parameters **name** and **model** object where the name will be role name of string type and model object contains the Key (string_type), AudienceId (integer_type), and Propagate (Boolean). The values of these parameters are unique for each user and by this process call, the default setting will get deleted for the user through the role name. 
  
![111](https://user-images.githubusercontent.com/110983629/189162312-799cca93-fda7-4e44-b0f9-8c4d66b01908.png)

   
The class name of the model is   
  
```markdown 
     UserDefaultSettingRemoveModel
```   
  
#### model Object Parameters 
  
![112](https://user-images.githubusercontent.com/110983629/189162509-2f3eee33-4181-4409-aae2-30b3023d160c.png)

  
#### Explorer 

|Names|Description|
|-----|-----------|
|model (required)|[Models.UserDefaultSettingRemoveModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/user-default-setting-remove-model)|
  
 
#### Responses  

The response of this endpoint service request contains the `Task<object>` that will indicate whether default setting is deleted for the user or not.

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

  
  
### Roles Users Get
#### Description 
This service endpoint will allow the user to retrieve users details by entering the Role. As it is define that the role name is an identifier for a specific list of roles. Through this process call, the users who are associated with the role entered will be shown. For this purpose, the `RolesUsersGetAsync` method is called by creating an instance of **RolesController** class which is accessed from the API client.   
  
  
```markdown
  RolesUsersGetAsync(string name)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
string name = "name0";
try
{
    UserReturnModel result = await rolesController.RolesUsersGetAsync(name);
}
catch (ApiException e){};
```  

It will be included in the try and catch block to deal with any exceptions that could arise if the `rolesController` object fails to retrieve the user details that was anticipated to be returned. In order to get user details of a specific role, name will be passed as a parameter to the `RolesUsersGetAsync` method in order to get the users details. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.      

#### Parameters Detail  
There is only one required parameter **name** which is the role name of string type. It is used for retrieving the users that belongs to the specific role entered.

![113](https://user-images.githubusercontent.com/110983629/189345071-755d444f-1d13-41e5-872f-76c7fab95400.png)

  
#### Responses  

The response of this endpoint service request contains the `Task<Models.UserReturnModel>` object. The class name of the ResponseType object is 

```markdown 
    UserReturnModel
``` 
 
#### Response body-JSON  
```markdown  
{
  "Url": null,
  "Id": null,
  "UserName": null,
  "FullName": null,
  "FirstName": null,
  "LastName": null,
  "Email": null,
  "MobilePhone": null,
  "HomePhone": null,
  "OfficePhone": null,
  "PostalCode": null,
  "EmailConfirmed": null,
  "Lockout": null,
  "Level": null,
  "Address": null,
  "Address2": null,
  "City": null,
  "State": null,
  "Country": null,
  "JoinDate": null,
  "Roles": null,
  "Settings": null,
  "PasswordExpDate": null,
  "CustomDaysToExpired": null,
  "TwoFactorEnabled": null,
  "IsPasswordCreated": null
} 
```
  
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

    
##### 'Task<Models.UserReturnModel>' Object Parameters 
  
![114](https://user-images.githubusercontent.com/110983629/189346307-40aac3c8-8089-4355-9982-adb9965acf72.png)
![115](https://user-images.githubusercontent.com/110983629/189346336-d7455aae-4381-4d1e-98a3-38aa7a92ed50.png)

  
#### Explorer 

|Names|Description|
|-----|-----------|
|ResponseType|[Task<Models.UserReturnModel>](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/user-return-model)|

  
  
  
## API Endpoints
## Users  
### Users Get
#### Description 
This service endpoint will allow the user to retrieve all the users details who are registered in the icheckgateway application. You can view the list of all users because there may be a chance where the user does not have any role, permission or audience associated with them. So, through this process call, all the users get retrieved with applying any filter. For this purpose, the `UsersGetAsync()` method is called by creating an instance of **UsersController** class which is accessed from the API client.
   
  
 ```markdown
 UsersController usersController = client.UsersController; 
 ```

  
```markdown
  RolesUsersGetAsync(string name)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
try
{
    UserReturnModel result = await usersController.UsersGetAsync();
}
catch (ApiException e){};
```  

It will be included in the try and catch block to deal with any exceptions that could arise if the `usersController` object fails to retrieve the user details that was anticipated to be returned. In order to get user details registered in the system, the `UsersGetAsync` method is called through the usersController object. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.      

#### Parameters Detail  
This endpoint does not take any parameter as it is showing all the users details. 
  
  
#### Responses  

The response of this endpoint service request contains the `Task<Models.UserReturnModel>` object. The class name of the ResponseType object is 

```markdown 
 UserReturnModel
``` 
 
#### Response body-JSON  
```markdown  
{
  "Url": null,
  "Id": null,
  "UserName": null,
  "FullName": null,
  "FirstName": null,
  "LastName": null,
  "Email": null,
  "MobilePhone": null,
  "HomePhone": null,
  "OfficePhone": null,
  "PostalCode": null,
  "EmailConfirmed": null,
  "Lockout": null,
  "Level": null,
  "Address": null,
  "Address2": null,
  "City": null,
  "State": null,
  "Country": null,
  "JoinDate": null,
  "Roles": null,
  "Settings": null,
  "PasswordExpDate": null,
  "CustomDaysToExpired": null,
  "TwoFactorEnabled": null,
  "IsPasswordCreated": null
} 
```
  
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

    
##### 'Task<Models.UserReturnModel>' Object Parameters 
  
![114](https://user-images.githubusercontent.com/110983629/189346307-40aac3c8-8089-4355-9982-adb9965acf72.png)
![115](https://user-images.githubusercontent.com/110983629/189346336-d7455aae-4381-4d1e-98a3-38aa7a92ed50.png)

  
#### Explorer 

|Names|Description|
|-----|-----------|
|ResponseType|[Task<Models.UserReturnModel>](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/user-return-model)|

  
  
  
  
  
  
  
  

### Users Post
#### Description 
This service endpoint will provide the facility to the user to create a user account by adding all required information. The user will have to enter the registration details where the roles, permissions and audiences are optional to add in order to create a user in the system successfully so that the created user can utilize platform's provided services. For this purpose, the `UsersPostAsync` method is called to create user account on in instance of `UsersController` class from the API client. 
   
 
```markdown
  UsersPostAsync(
    Models.CreateUserBindingModel createUserModel)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
var createUserModel = new CreateUserBindingModel();
createUserModel.Email = "Email8";
createUserModel.Username = "Username4";
createUserModel.FirstName = "FirstName8";
createUserModel.LastName = "LastName8";

try
{
    List<string> result = await usersController.UsersPostAsync(createUserModel);
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "usersController" object fails to create a user that was anticipated to be returned. The **createUserModel** object will be created which will be of `CreateUserBindingModel` type and the user's required details such as first name etc will be defined in the model. The `createUserModel` model is passed as a parameter to the `UsersPostAsync` method. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes. 


#### Parameters Detail  
The parameter of this endpoint service contains **createUserModel** as a required object. It further contains the Email, Username, FirstName, LastName, Password, ConfirmPassword, MobilePhone, HomePhone, OfficePhone, PostalCode, Address, Address2, City, State, Country, CallBackUrl, Level, CustomerDaysToExpired. Whereas, the **UserSettings**, **Roles**, **Applications** and **Permissions** objects are further contains parameters. In all of these parameters, the Email, Username, FirstName, LastName, Applications and UserSettings are required ones. These all parameters are actually the user properties that needs to be added for creating user account. 
  

The class name of the **createUserModel** is
```markdown
  CreateUserBindingModel
```  
  
#### createUserModel object Parameters
   
![116](https://user-images.githubusercontent.com/110983629/189354384-fd052795-c737-4fe5-8414-746a3fb2a964.png)

![117](https://user-images.githubusercontent.com/110983629/189354420-0fd00b47-6ceb-43e0-867f-1dc20c2372c9.png)

  
#### UserSettings object class name and Parameters   

![118](https://user-images.githubusercontent.com/110983629/189354650-746c14cc-fa66-48a1-9325-ed5e9bf2abec.png)  

#### Roles object class name and Parameters   
  
![119](https://user-images.githubusercontent.com/110983629/189354817-7ddc9728-fc01-4dfa-b701-84e0dec42248.png)


#### Permissions object class name and Parameters     
  
![120](https://user-images.githubusercontent.com/110983629/189354972-d7fd8c4c-36e6-4619-b9bc-9e19a3414b64.png)
  

#### Applications object class name and Parameters     
  
![121](https://user-images.githubusercontent.com/110983629/189355097-2a179140-8735-4df4-b10a-5dfd8d558e2f.png)
  
#### Explorer 

|Names|Description|
|-----|-----------|
|createUserModel (required)|[Models.CreateUserBindingModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/create-user-binding-model)| 
  
  
#### Responses 

The response of this endpoint service request contains the "Task<List<string>>" parameter that returns the list of user details whose account is created. 
  
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

  
  
  
### Users Get 1
#### Description 
This service endpoint will allow the user to retrieve the user detail by entering the username in the system. As username is unique for each user so only a user detail will be shown against this service request. For this purpose, the `UsersGet1Async` method is called by creating an instance of **UsersController** class which is accessed from the API client.
   
 
```markdown
   UsersGet1Async(string username)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
string username = "username0";
try
{
    UserReturnModel result = await usersController.UsersGet1Async(username);
}
catch (ApiException e){};
```  

It will be included in the try and catch block to deal with any exceptions that could arise if the `usersController` object fails to retrieve the user details that was anticipated to be returned. In order to get user details, the `UsersGet1Async` method is called through the usersController object that receive the username as a parameter. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.    
  
#### Parameters Detail  
There is only one required parameter for this api call which is **username** of String type. You must need to enter the valid username so that the system will retrieve the user details successfully.
  
![124](https://user-images.githubusercontent.com/110983629/189360342-3f56866c-2f16-48d3-8ca9-c95b07b41653.png)

#### Responses  

The response of this endpoint service request contains the `Task<Models.UserReturnModel>` object. The class name of the ResponseType object is 

```markdown 
  UserReturnModel
``` 
 
#### Response body-JSON  
```markdown  
 {
  "Url": null,
  "Id": null,
  "UserName": null,
  "FullName": null,
  "FirstName": null,
  "LastName": null,
  "Email": null,
  "MobilePhone": null,
  "HomePhone": null,
  "OfficePhone": null,
  "PostalCode": null,
  "EmailConfirmed": null,
  "Lockout": null,
  "Level": null,
  "Address": null,
  "Address2": null,
  "City": null,
  "State": null,
  "Country": null,
  "JoinDate": null,
  "Roles": null,
  "Settings": null,
  "PasswordExpDate": null,
  "CustomDaysToExpired": null,
  "TwoFactorEnabled": null,
  "IsPasswordCreated": null
}
```
  
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

    
##### 'Task<Models.UserReturnModel>' Object Parameters 
  
![114](https://user-images.githubusercontent.com/110983629/189346307-40aac3c8-8089-4355-9982-adb9965acf72.png)
![115](https://user-images.githubusercontent.com/110983629/189346336-d7455aae-4381-4d1e-98a3-38aa7a92ed50.png)

  
#### Explorer 

|Names|Description|
|-----|-----------|
|ResponseType|[Task<Models.UserReturnModel>](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/user-return-model)|


  
  
  
  
  
  
### Users Put
#### Description 
This service endpoint will provide the facility to the user to update a user details by accessing it through the username. The user will have to enter the user details where the roles, permissions and audiences are optional to add in order to update a user in the system successfully. For this purpose, the `UsersPutAsync` method is called to edit user details by creating an instance of `UsersController` class from the API client. 
   
 
```markdown
  UsersPutAsync(
    string username,
    Models.ModifyUserBindingModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
string username = "username0";
var model = new ModifyUserBindingModel();
model.FirstName = "FirstName2";
model.LastName = "LastName2";

try
{
    List<string> result = await usersController.UsersPutAsync(username, model);
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "usersController" object fails to update a user that was anticipated to be returned. The **model** object will be created which will be of `ModifyUserBindingModel` type and the user's required details such as first name etc will be define in the model. The model is passed as a parameter to the `UsersPutAsync` method. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes. 


#### Parameters Detail  
The parameter of this endpoint service contains **username** (string type) and **model** as a required parameter. The model object further contains the Email, Username, FirstName, LastName, Password, ConfirmPassword, MobilePhone, HomePhone, OfficePhone, PostalCode, Address, Address2, City, State, Country, CallBackUrl, Level, CustomerDaysToExpired. Whereas, the **UserSettings**, **Roles**, **Applications** and **Permissions** objects are further contains parameters. In all of these parameters, the FirstName, LastName, Applications and UserSettings are required ones. These all parameters are actually the user properties that needs to be added for updating user details. 
  

The class name of the **model** is
```markdown
   ModifyUserBindingModel
```  
  
#### model object Parameters
   
![116](https://user-images.githubusercontent.com/110983629/189354384-fd052795-c737-4fe5-8414-746a3fb2a964.png)

![117](https://user-images.githubusercontent.com/110983629/189354420-0fd00b47-6ceb-43e0-867f-1dc20c2372c9.png)

  
#### UserSettings object class name and Parameters   

![118](https://user-images.githubusercontent.com/110983629/189354650-746c14cc-fa66-48a1-9325-ed5e9bf2abec.png)  

#### Roles object class name and Parameters   
  
![119](https://user-images.githubusercontent.com/110983629/189354817-7ddc9728-fc01-4dfa-b701-84e0dec42248.png)


#### Permissions object class name and Parameters     
  
![120](https://user-images.githubusercontent.com/110983629/189354972-d7fd8c4c-36e6-4619-b9bc-9e19a3414b64.png)
  

#### Applications object class name and Parameters     
  
![121](https://user-images.githubusercontent.com/110983629/189355097-2a179140-8735-4df4-b10a-5dfd8d558e2f.png)
  
#### Explorer 

|Names|Description|
|-----|-----------|
|model (required)|[Models.ModifyUserBindingModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/modify-user-binding-model)| 
  
  
#### Responses 

The response of this endpoint service request contains the "Task<List<string>>" that returns the list of user details whose detail is updated. 
  
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

  

  
### Users Delete
#### Description 
Through this service endpoint, you will be able to delete a user by accessing it through the username. The user will have to enter the username in order to remove a user from the system successfully. For this purpose, the `UsersDeleteAsync` method is called to delete user account by creating an the instance of `UsersController` class from the API client. 
   
 
```markdown
   UsersDeleteAsync(
    string username)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
string username = "username0";
try
{
    string result = await usersController.UsersDeleteAsync(username);
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "usersController" object fails to delete a user that was anticipated to be returned. The **username** will be passed as a parameter to the `UsersDeleteAsync` method. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes. 


#### Parameters Detail  
The parameter of this endpoint service contains **username** (string type) as a required parameter. The user must have to enter the correct username for accessing a user and deleting it from the system.
   
  
#### Responses 

The response of this endpoint service request contains the "Task<string>>" that returns value whether the respective user get deleted or not.   
  
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

 
  
  
  
  
### Users Get Locked
#### Description 
This service endpoint will allow the user to retrieve all locked users which means that the users whose lockout value is true/yes, their user details will get retrieved against this api call. For this purpose, the `UsersGetLockedAsync` method is called by creating an instance of **UsersController** class which is accessed from the API client.
   
 
```markdown
   UsersGetLockedAsync()
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
try
{
    UserReturnModel result = await usersController.UsersGetLockedAsync();
}
catch (ApiException e){};
```  

It will be included in the try and catch block to deal with any exceptions that could arise if the `usersController` object fails to retrieve the locked user details that was anticipated to be returned. In order to get user details, the `UsersGetLockedAsync` method is called through the usersController object that does not receive any parameter. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.    
  
#### Parameters Detail   
This endpoint does not take any parameter as the system will automatically retrieve all locked users details.  

#### Responses  

The response of this endpoint service request contains the `Task<Models.UserReturnModel>` object. The class name of the ResponseType object is 

```markdown 
  UserReturnModel
``` 
 
#### Response body-JSON  
```markdown  
 {
  "Url": null,
  "Id": null,
  "UserName": null,
  "FullName": null,
  "FirstName": null,
  "LastName": null,
  "Email": null,
  "MobilePhone": null,
  "HomePhone": null,
  "OfficePhone": null,
  "PostalCode": null,
  "EmailConfirmed": null,
  "Lockout": null,
  "Level": null,
  "Address": null,
  "Address2": null,
  "City": null,
  "State": null,
  "Country": null,
  "JoinDate": null,
  "Roles": null,
  "Settings": null,
  "PasswordExpDate": null,
  "CustomDaysToExpired": null,
  "TwoFactorEnabled": null,
  "IsPasswordCreated": null
}
```
  
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

    
##### 'Task<Models.UserReturnModel>' Object Parameters 
  
![114](https://user-images.githubusercontent.com/110983629/189346307-40aac3c8-8089-4355-9982-adb9965acf72.png)
![115](https://user-images.githubusercontent.com/110983629/189346336-d7455aae-4381-4d1e-98a3-38aa7a92ed50.png)

  
#### Explorer 

|Names|Description|
|-----|-----------|
|ResponseType|[Task<Models.UserReturnModel>](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/user-return-model)|

 
  
  
  
  
### Users Change Email
#### Description 
This service endpoint will provide the facility to the user to update email by accessing user through the username. For this purpose, the `UsersChangeEmailAsync` method is called to edit user details by creating an instance of `UsersController` class from the API client. 
   
 
```markdown
  UsersChangeEmailAsync(
    string username,
    Models.ChangeEmailBindingModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
string username = "username0";
var model = new ChangeEmailBindingModel();
model.OldEmail = "OldEmail6";
model.NewEmail = "NewEmail8";
model.ConfirmEmail = "ConfirmEmail4";

try
{
    object result = await usersController.UsersChangeEmailAsync(username, model);
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "usersController" object fails to change the email of a user that was anticipated to be returned. The **model** object will be created which will be of `ChangeEmailBindingModel` type and the user's username along with the updated email in model object will be passed as a parameter to the `UsersChangeEmailAsync` method. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes. 


#### Parameters Detail  
The parameter of this endpoint service contains **username** (string type) and **model** as a required parameter. The model object further contains the OldEmail, NewEmail, ConfirmEmail, and CallBackUrl. Whereas, all the parameters of the model object are required except CallBackUrl. In all of these parameters, the OldEmail must be different from the new email and new email and confirm email should be same. The new email must be of Minimum Length: 0, Maximum Length: 100.
  
![125](https://user-images.githubusercontent.com/110983629/189376377-ee8c74c2-7e24-448f-a982-3977d8f11604.png)

  
The class name of the **model** is
```markdown
    ChangeEmailBindingModel
```  
  
#### model object Parameters

![126](https://user-images.githubusercontent.com/110983629/189376589-f33a4507-9884-4d4e-8c10-058ece44e8e5.png)
 
#### Explorer 

|Names|Description|
|-----|-----------|
|model (required)|[Models.ChangeEmailBindingModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/change-email-binding-model)| 
  
  
#### Responses 

The response of this endpoint service request contains the "Task<object>" that returns the value for the changing the user's email.
  
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

 
  
  
  
  
    
### Users Change Password
#### Description 
This service endpoint will provide the facility to update password of user by accessing the user through the username. For this purpose, the `UsersChangePasswordAsync` method is called to change user's password by creating an instance of `UsersController` class from the API client. 
   
 
```markdown
 UsersChangePasswordAsync(
    string username,
    Models.ChangePasswordBindingModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
string username = "username0";
var model = new ChangePasswordBindingModel();
model.OldPassword = "OldPassword4";
model.NewPassword = "NewPassword2";
model.ConfirmPassword = "ConfirmPassword0";

try
{
    object result = await usersController.UsersChangePasswordAsync(username, model);
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "usersController" object fails to change the password of a user that was anticipated to be returned. The **model** object will be created which will be of `ChangePasswordBindingModel` type and the user's username along with the updated password in model object will be passed as a parameter to the `UsersChangePasswordAsync` method. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes. 


#### Parameters Detail  
The parameter of this endpoint service contains **username** (string type) and **model** as a required parameter. The model object further contains the OldPassword, NewPassword, ConfirmPassword. Whereas, all the parameters of the model object are required to enter. In all of these parameters, the OldPassword must be different from the new password and new password and confirm password should be same. The new password must be of Minimum Length: 8, Maximum Length: 128.
   
![127](https://user-images.githubusercontent.com/110983629/189380421-75621873-7422-4fb2-838b-63e75b3b22fe.png)
  
  
The class name of the **model** is
```markdown
    ChangePasswordBindingModel
```  
  
#### model object Parameters

![128](https://user-images.githubusercontent.com/110983629/189380822-15005335-8f08-4717-a0d3-34411ff00b2d.png)

  
#### Explorer 

|Names|Description|
|-----|-----------|
|model (required)|[Models.ChangePasswordBindingModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/change-password-binding-model)| 
  
  
#### Responses 

The response of this endpoint service request contains the "Task<object>" that returns the value for the changing the user's password.
  
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

  
  
  
  
  

### Users Reset Password
#### Description 
This service endpoint will provide the facility to reset password of user by accessing the user through the username. For this purpose, the `UsersResetPasswordAsync` method is called to reset user's password by creating an instance of `UsersController` class from the API client. 
   
 
```markdown
 UsersResetPasswordAsync(
    string username)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
string username = "username0";
try
{
    object result = await usersController.UsersResetPasswordAsync(username);
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "usersController" object fails to reset the password of a user that was anticipated to be returned. The **username** will be passed as a parameter to the `UsersResetPasswordAsync` method. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes. 


#### Parameters Detail  
The parameter of this endpoint service contains **username** (string type) as a required parameter. When user adds the username and trigger for resetting password, the system will autogenerate the password for user's account whose username is entered.  
 
![129](https://user-images.githubusercontent.com/110983629/189384197-c9351b36-06cb-4cac-a2e5-7c70598faf55.png)

  
#### Responses 

The response of this endpoint service request contains the `Task<object>` that returns the value for the resetting the user's password.
  
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
  
  
  
  
  

### Users Send Confirmation Email
#### Description 
This service endpoint will provide the facility to send confirmation email by accessing the user through the username. For this purpose, the `UsersSendConfirmationEmailAsync` method is called to send confirmation email by creating an instance of `UsersController` class from the API client. 
   
 
```markdown
 UsersSendConfirmationEmailAsync(
    string username,
    string callbackUrl = null)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
string username = "username0";
try
{
    object result = await usersController.UsersSendConfirmationEmailAsync(username, null);
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "usersController" object fails to send confirmation email to a user that was anticipated to be returned. The **username** will be passed as a parameter to the `UsersSendConfirmationEmailAsync` method. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes. 


#### Parameters Detail  
The parameter of this endpoint service contains **username** (string type) and **callbackUrl** (String type) as a required parameter. When user adds the username and trigger for sending confirmation email, the system will send the confirmation email to the user without any delay whose username is entered.
  
![130](https://user-images.githubusercontent.com/110983629/189387156-95ae5962-d586-42e8-a817-704f041c4fc7.png)

  
#### Responses 

The response of this endpoint service request contains the `Task<object>` that returns the value for the sending confirmation email.
  
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
  
  
  
  

### Users Get Lock Asyc
#### Description 
This service endpoint will provide the facility to get lock a user. For this purpose, the `UsersGetLockAsyncAsync` method is called to get lock user by creating an instance of `UsersController` class from the API client. 
   
 
```markdown
 UsersGetLockAsyncAsync(
    string username)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
string username = "username0";
try
{
    object result = await usersController.UsersGetLockAsyncAsync(username);
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "usersController" object fails to  lock a user that was anticipated to be returned. The **username** will be passed as a parameter to the `UsersGetLockAsyncAsync` method. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes. 


#### Parameters Detail  
The parameter of this endpoint service contains **username** (string type) only as a required parameter. When user adds the username and trigger for locking user, the system will lock user account without any delay whose username is entered.
 
![131](https://user-images.githubusercontent.com/110983629/189389716-e9a68430-d870-4ecd-b99b-55718a8465ad.png)

  
#### Responses 

The response of this endpoint service request contains the `Task<object>` that returns the value for locking the user account.
  
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
  
  
  
  
### Users Lock Asyc
#### Description 
This service endpoint will provide the facility to lock a user by accessing it through the username. For this purpose, the `UsersLockAsyncAsync` method is called to lock the account of user by creating an instance of `UsersController` class from the API client. 
   
 
```markdown
 UsersLockAsyncAsync(string username)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
string username = "username0";
try
{
    object result = await usersController.UsersLockAsyncAsync(username);
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "usersController" object fails to  lock a user that was anticipated to be returned. The **username** will be passed as a parameter to the `UsersLockAsyncAsync` method. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes. 


#### Parameters Detail  
The parameter of this endpoint service contains **username** (string type) only as a required parameter. When user adds the username and trigger for locking user, the system will lock user account without any delay whose username is entered.
 
![132](https://user-images.githubusercontent.com/110983629/189483711-9426eba5-7353-44a5-9de1-4ad4257e1596.png)
  
  
#### Responses 

The response of this endpoint service request contains the `Task<object>` that returns the value for locking the user account.
  
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
  
  
  
  
  
### Users UnLock Asyc
#### Description 
This service endpoint will provide the facility to unlock a user account by accessing it through the username. When the user's account get locked due to the failed login attempts, the system will provide the facility to the admin to unlock the user account which get locked automatically. For this purpose, the `UsersUnlockAsyncAsync` method is called to unlock the account of user by creating an instance of `UsersController` class from the API client. 
   
 
```markdown
 UsersUnlockAsyncAsync(string username)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
string username = "username0";
try
{
    object result = await usersController.UsersUnlockAsyncAsync(username);
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "usersController" object fails to  unlock a user that was anticipated to be returned. The **username** will be passed as a parameter to the `UsersUnlockAsyncAsync` method. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes. 


#### Parameters Detail  
The parameter of this endpoint service contains **username** (string type) only as a required parameter. When admin adds the username and trigger for unlocking user, the system will unlock user account without any delay whose username is entered.
 
![132](https://user-images.githubusercontent.com/110983629/189483711-9426eba5-7353-44a5-9de1-4ad4257e1596.png)
  
  
#### Responses 

The response of this endpoint service request contains the `Task<object>` that returns the value for unlocking the user account.
  
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
  

  
  
  

### Users Roles Get
#### Description 
By using the username, this service endpoint will make it possible to get user roles. The roles that are associated with the one user whose username is entered will be shown to you through this process call. To do this, a new instance of the 'UsersController' class is created from the API client, and the 'UsersRolesGetAsync' method is invoked to retrieve user roles.
 
```markdown
 UsersRolesGetAsync(string username)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
string username = "username0";
try
{
    List<string> result = await usersController.UsersRolesGetAsync(username);
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "usersController" object fails to retrieve user roles that was anticipated to be returned. The **username** will be passed as a parameter to the `UsersRolesGetAsync` method. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes. 


#### Parameters Detail  
The parameter of this endpoint service contains **username** (string type) only as a required parameter. When user adds the username and trigger for getting user roles, the system will show the list of roles that are associated with the user whose username is entered. 
![133](https://user-images.githubusercontent.com/110983629/189484498-77985c0f-525d-4b9a-a8de-102b0a193b34.png)

  
  
#### Responses 

The response of this endpoint service request contains the `Task<List<string>>` that returns the list of user roles.
  
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
    
  
  
### Users Roles Put
#### Description
This service endpoint will allow the user to update the list of roles that are assigned to a user. You can update the roles by accessing the user through the username. For this purpose, the `UsersRolesPutAsync` method is called by creating an instance of **UsersController** class which is accessed from the API client. 
  
```markdown
   UsersRolesPutAsync(
    string username,
    Models.AddRolesViewModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
string username = "username0";
var model = new AddRolesViewModel();
model.RolesToAdd = new List<RolesBindingModel>();

var modelRolesToAdd0 = new RolesBindingModel();
model.RolesToAdd.Add(modelRolesToAdd0);

var modelRolesToAdd1 = new RolesBindingModel();
model.RolesToAdd.Add(modelRolesToAdd1);

try
{
    List<string> result = await usersController.UsersRolesPutAsync(username, model);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "usersController" object fails to update roles that was anticipated to be returned. In order to update roles, model object is created which will be of `AddRolesViewModel` type and list of roles will be defined for the model through the `RolesToAdd.Add` method. The `model` will be passed as a parameter to the `UsersRolesPutAsync` method in order to update the roles of a user. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
There are two required parameters for this API request which includes the **username** (String_type) and **model** object. The model object further contains the array of roles that needs to be updated for the user. Moreover, the audience id is an optional parameter to add for updating the roles. 

![134](https://user-images.githubusercontent.com/110983629/189485185-3158de0b-3a43-4b6d-a08b-9349d9e1025d.png)


The class name of the model is   
  
```markdown 
    AddRolesViewModel
```   
  
  
#### model Object Parameters
  
![135](https://user-images.githubusercontent.com/110983629/189485230-1cdbfdbd-f56c-4c7b-87a7-c9c11673c79e.png)

  
#### Explorer 

|Names|Description|
|-----|-----------|
|model (required)|[Models.AddRolesViewModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/add-roles-view-model)|
  
 
#### Responses  

The response of this endpoint service request contains the `Task<List<string>>` object which returns the list of updated roles for the user.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
  
  
  
  
### Users Roles Delete
#### Description
This service endpoint will allow the user to delete the list of roles that are assigned to a user. You can delete the roles by accessing the user roles through the username. For this purpose, the `UsersRolesDeleteAsync` method is called by creating an instance of **UsersController** class which is accessed from the API client. 
  
```markdown
   UsersRolesDeleteAsync(
    string username,
    Models.RemoveRolesViewModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
string username = "username0";
var model = new RemoveRolesViewModel();
model.RolesToRemove = new List<string>();
model.RolesToRemove.Add("RolesToRemove3");
model.RolesToRemove.Add("RolesToRemove2");

try
{
    string result = await usersController.UsersRolesDeleteAsync(username, model);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "usersController" object fails to delete roles that was anticipated to be returned. In order to delete roles, model object is created which will be of `RemoveRolesViewModel` type and list of roles that needs to be deleted will be defined for the model through the `RolesToRemove.Add` method. The `model` will be passed as a parameter to the `UsersRolesDeleteAsync` method in order to delete the roles of a user. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
There are two required parameters for this API request which includes the **username** (String_type) and **model** object. The model object further contains the array of roles that needs to be removed for the user.  
   
![136](https://user-images.githubusercontent.com/110983629/189485915-9d89aa8f-249f-439e-a660-e0bf82131c19.png)

  
The class name of the model is   
  
```markdown 
     RemoveRolesViewModel
```   
  
  
#### model Object Parameters

![137](https://user-images.githubusercontent.com/110983629/189486036-02635249-e0dd-4a3d-97d8-504c1b469166.png)

    
#### Explorer 

|Names|Description|
|-----|-----------|
|model (required)|[Models.RemoveRolesViewModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/remove-roles-view-model)|
  
 
#### Responses  

The response of this endpoint service request contains the `Task<string>` object which returns value for deleting the roles of the user.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
  
  
  
  
  
  
### Users Effective Permissions Get 
#### Description
This service endpoint will allow the user to retrieve the effectivePermissions by entering the username. These effective permissions will be associated with the one user whose username is entered to access them. For this purpose, the `UsersEffectivePermissionsGetAsync` method is called by creating an instance of **UsersController** class which is accessed from the API client.  
  
  
```markdown
 UsersEffectivePermissionsGetAsync(string username)
``` 
  
This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
string username = "username0";
try
{
    await usersController.UsersEffectivePermissionsGetAsync(username);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the `usersController` object fails to retrieve the effective permissions that was anticipated to be returned. In order to get effective permissions of the user, `UsersEffectivePermissionsGetAsync` method is used that takes the username as a parameter. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
This service endpoint requires only one parameter which is **username** unique for each user. It is required for the user to enter username which is of String type for retrieving the effective permissions.
  
![138](https://user-images.githubusercontent.com/110983629/189486633-b9515c4e-104c-4f3b-934b-66af04c0b8b9.png)
  
  
#### Responses  
 
The response of this endpoint service request contains the `Task` which returns the value for successfully retrieving the user's effective permissions.   
  

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

  
#### Errors

|HTTP Status Code|Error Description| Exception Class|
|-----|-----------|----|
|400|Bad Request|ApiException|
 
The errors that can be reported in response to this API call are listed in the error table above. The 4xx demonstrates that it is possible to make a poor request while requesting a user's actual permissions.  

  

  
  
  
  
### Users Permissions Get 
#### Description
This service endpoint will allow the user to retrieve the permissions by entering the username. All the permissions associated with the user account get retrieved whose username is entered to access them. For this purpose, the `UsersPermissionsGetAsync` method is called by creating an instance of **UsersController** class which is accessed from the API client.  
  
  
```markdown
   UsersPermissionsGetAsync(
    string username)
``` 
  
This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
string username = "username0";
try
{
    await usersController.UsersPermissionsGetAsync(username);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the `usersController` object fails to retrieve the permissions that was anticipated to be returned. In order to get permissions of the user, `UsersPermissionsGetAsync` method is used that takes the username as a parameter. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail   
This service endpoint requires only one parameter which is **username** unique for each user. It is required for the user to enter username which is of String type for retrieving all the permissions associated with it.
   
  
#### Responses  
 
The response of this endpoint service request contains the `Task` which returns the value for successfully retrieving the user's permissions.   
  

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

  
#### Errors

|HTTP Status Code|Error Description| Exception Class|
|-----|-----------|----|
|400|Bad Request|ApiException|
 
The errors that can be reported in response to this API call are listed in the error table above. The 4xx demonstrates that it is possible to make a poor request while requesting a user's actual permissions.  
  
  
  
  
  
  

  
### Users Permissions Put
#### Description
This service endpoint will allow the user to update the list of permissions that are assigned to a user. You can update the permissions by accessing them through the username. For this purpose, the `UsersPermissionsPutAsync` method is called by creating an instance of **UsersController** class which is accessed from the API client. 
  
```markdown
  UsersPermissionsPutAsync(
    string username,
    Models.UserAssignPermissionViewModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
string username = "username0";
var model = new UserAssignPermissionViewModel();
try
{
    List<string> result = await usersController.UsersPermissionsPutAsync(username, model);
}
catch (ApiException e){}; 
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "usersController" object fails to update permissions that was anticipated to be returned. In order to update permissions, model object is created which will be of `UserAssignPermissionViewModel` type and passed as a parameter to the `UsersPermissionsPutAsync` method in order to update the permissions of a user. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
There are two required parameters for this API request which includes the **username** (String_type) and **model** object. The model object further contains the list of permissions and **TargetAudienceId** which will be of string type. Moreover,  Target Audience Id is optional to add in case that we were assigning permissions in AUTH Audience to execute actions to any particular Audience (Not All).
 
![139](https://user-images.githubusercontent.com/110983629/189488077-5ef28fd2-0327-4ee0-a8f6-ae00238ab836.png)
  
  
The class name of the model is   
  
```markdown 
    UserAssignPermissionViewModel
```   
  
#### model Object Parameters
  
![140](https://user-images.githubusercontent.com/110983629/189488141-8210e1fb-6852-4e21-8484-6c12816e7ff4.png)

    
#### permission Object classs name and Parameters  
  
![141](https://user-images.githubusercontent.com/110983629/189488194-3554b3bf-2786-448c-9aaf-1fb552ae6389.png)
  
  
#### Explorer 

|Names|Description|
|-----|-----------|
|model (required)|[Models.UserAssignPermissionViewModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/user-assign-permission-view-model)|
  
 
#### Responses  

The response of this endpoint service request contains the `Task<List<string>>` object which returns the list of updated permissions for the user.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
  
    
  

  
  
  
  
  
  

### Users Permissions Delete
#### Description
This service endpoint will allow the user to delete the list of permissions that are assigned to a user. You can delete the permissions by accessing them through the username. For this purpose, the `UsersPermissionsDeleteAsync` method is called by creating an instance of **UsersController** class which is accessed from the API client. 
  
```markdown
  UsersPermissionsDeleteAsync(
    string username,
    Models.UserDropPermissionViewModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
string username = "username0";
var model = new UserDropPermissionViewModel();
try
{
    string result = await usersController.UsersPermissionsDeleteAsync(username, model);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "usersController" object fails to delete permissions that was anticipated to be returned. In order to remove permissions, model object is created which will be of `UserDropPermissionViewModel` type and passed as a parameter to the `UsersPermissionsDeleteAsync` method in order to remove the permissions of a user. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
There are two required parameters for this API request which includes the **username** (String_type) and **model** object. The model object further contains the list of permissions and **TargetAudienceId** which will be of string type. Moreover,  Target Audience Id is optional in case that we were assigning permissions in AUTH Audience to execute actions to any particular Audience (Not All). And the username must be entered for deleting the permissions associated with it.
 
![142](https://user-images.githubusercontent.com/110983629/189488631-f40e35ed-c2d1-47c8-b788-53208bc35434.png)

  
The class name of the model is   
  
```markdown 
   UserDropPermissionViewModel
```   
  
#### model Object Parameters
  
![143](https://user-images.githubusercontent.com/110983629/189488831-55d4ce96-5d66-4e29-85d4-5af583322d39.png)

 
#### Explorer 

|Names|Description|
|-----|-----------|
|model (required)|[Models.UserDropPermissionViewModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/user-drop-permission-view-model)|
  
 
#### Responses  

The response of this endpoint service request contains the `Task<string>` object which returns the value for deleting the permissions.
 
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
  
  
  
  
### Users Disable TFA
#### Description
This service endpoint will disable the two factor authentication for the user account by accessing it through the username. The API client will obtain an instance of the 'UsersController' class and invoke the 'UsersDisableTFAAsync` method in order to disable the TFA.  
  
 
```markdown
   UsersDisableTFAAsync(
    string username)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
string username = "username0";
try
{
    List<string> result = await usersController.UsersDisableTFAAsync(username);
}
catch (ApiException e){};
```

It will be included in the try and catch block to deal with any exceptions that could arise if the "usersController" object fails to disable the two factor authentication process for the user account that was anticipated to be returned. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

  
#### Parameters 
There is only one required parameter which is **username** (String type) for disabling the TFA for only one user account whose username is provided.
  
![144](https://user-images.githubusercontent.com/110983629/189489424-4ba7ff1d-ac81-4bdc-aa11-ce0c25e0845a.png)

  
  
#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|  
 

#### Response
##### 'ResponseType' Object Parameters   
The response of this endpoint service request contains the "ResponseType" object. The `Task<List<string>>` is the parameter that will return the list of the strings for disabling 2 factor authentication.

  
  
  
  
  
  
  
  
  
### Users Default Settings Get
#### Description
This service endpoint will allow the user to retrieve the default settings of the user that will be automatically added to each new user account when it is created. For this purpose, the `UsersDefaultSettingsGetAsync` method is called by creating an instance of **UsersController** class which is accessed from the API client. 
  
```markdown
 UsersDefaultSettingsGetAsync()
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
try
{
    List<UserDefaultSetting> result = await usersController.UsersDefaultSettingsGetAsync();
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "usersController" object fails to retrieve the user's default settings details that was anticipated to be returned. The list of default settings will get returned against this endpoint request through method `UsersDefaultSettingsGetAsync` invoked. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail   
This endpoint does not take any parameter to process and retrieve the user default settings 
 
#### Responses  

The response of this endpoint service request contains the `Task<List<Models.UserDefaultSetting>>` object. The class name of the ResponseType object is 

```markdown 
   UserDefaultSetting
``` 
 
#### Response body-JSON  
```markdown 
  {
  "Id": null,
  "Key": null,
  "Value": null,
  "Description": null,
  "AudienceId": null,
  "Level": null,
  "Enabled": false,
  "DataType": "DataType4",
  "Audience": null
}
```

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

    
##### `Task<List<Models.UserDefaultSetting>>` Object Parameters  
  
![145](https://user-images.githubusercontent.com/110983629/189489953-ab064730-d03f-4758-a216-1ca94aec7bb1.png)

  
#### Explorer 

|Names|Description|
|-----|-----------|
|ResponseType|[Task<List<Models.UserDefaultSetting>>](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/user-default-setting)|

  
  

  
  
  
  
### Users Default Settings Put
#### Description
This service endpoint will allow the user to modify Default Settings that will be automatically added to each new user account. For this purpose, the `UsersDefaultSettingsPutAsync` method is called by creating an instance of UsersController class which is accessed from the API client. 
  
```markdown
 UsersDefaultSettingsPutAsync(
    Models.UserDefaultSettingBindingModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
var model = new UserDefaultSettingBindingModel();
model.Key = "string";
model.MValue = "string";
model.AudienceId = 1;
model.Description = "string";
model.Level = "string";
model.Enabled = true;
model.DataType = "string";
model.Propagate = false;

try
{
    object result = await usersController.UsersDefaultSettingsPutAsync(model);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "usersController" object fails to update default settings of the user that was anticipated to be returned. In order to update default settings, model object is created which will be of `UserDefaultSettingBindingModel` type and will be passed as a parameter to the `UsersDefaultSettingsPutAsync` method in order to update an default setting for user. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
The **model** object is the required parameter to enter that contains Key (String_type), MValue (String_type), AudienceId (Integer_type), Description (String_type), Level (String_type), Enabled (bool_type), DataType (String_type), and Propagate (bool_type) parameters. The key and MValue are the required parameters to enter for updating the user's default setting. 
  
The class name of the model is   
  
```markdown 
   UserDefaultSettingBindingModel
```   
  
#### model Object Parameters 

![146](https://user-images.githubusercontent.com/110983629/189490747-cd6cbde8-dc4d-4013-a871-633610b22ee8.png)
   
#### Explorer 

|Names|Description|
|-----|-----------|
|model (required)|[Models.UserDefaultSettingBindingModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/user-default-setting-binding-model)|
  
 
#### Responses  

The response of this endpoint service request contains the `Task<object>` object that will indicate whether the user default setting is updated or not.
  

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

  
  
  
  
  

### Users Default Settings Post
#### Description
This service endpoint will allow the user to assign Default Settings to a user by adding all the required information in the given input fields such as key, mvalue etc. For this purpose, the `UsersDefaultSettingsPostAsync` method is called by creating an instance of UsersController class which is accessed from the API client. 
  
```markdown
 UsersDefaultSettingsPostAsync(
    Models.UserDefaultSettingBindingModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
var model = new UserDefaultSettingBindingModel();
model.Key = "string";
model.MValue = "string";
model.AudienceId = 1;
model.Description = "string";
model.Level = "string";
model.Enabled = true;
model.DataType = "string";
model.Propagate = false;

try
{
    object result = await usersController.UsersDefaultSettingsPostAsync(model);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "usersController" object fails to assign default settings of the user that was anticipated to be returned. In order to assign default settings, model object is created which will be of `UserDefaultSettingBindingModel` type and will be passed as a parameter to the `UsersDefaultSettingsPostAsync` method in order to update an default setting for user. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
The **model** object is the required parameter to enter that contains Key (String_type), MValue (String_type), AudienceId (Integer_type), Description (String_type), Level (String_type), Enabled (bool_type), DataType (String_type), and Propagate (bool_type) parameters. The key and MValue are the required parameters to enter for updating the user's default setting. 
  
The class name of the model is   
  
```markdown 
    UserDefaultSettingBindingModel
```   
  
#### model Object Parameters 

![146](https://user-images.githubusercontent.com/110983629/189490747-cd6cbde8-dc4d-4013-a871-633610b22ee8.png)
   
#### Explorer 

|Names|Description|
|-----|-----------|
|model (required)|[Models.UserDefaultSettingBindingModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/user-default-setting-binding-model)|
  
 
#### Responses  

The response of this endpoint service request contains the `Task<object>` object that will indicate whether the user default setting is assigned or not.
  

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
  
  
  
  

  

### Users Default Settings Delete
#### Description
This service endpoint will allow the user to delete Default Settings of a user by adding the required key in the input field. For this purpose, the `UsersDefaultSettingsDeleteAsync` method is called by creating an instance of UsersController class which is accessed from the API client. 
  
```markdown
 UsersDefaultSettingsDeleteAsync(
    Models.UserDefaultSettingRemoveModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
var model = new UserDefaultSettingRemoveModel();
model.Key = "Key6";
try
{
    object result = await usersController.UsersDefaultSettingsDeleteAsync(model);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "usersController" object fails to remove default settings of the user that was anticipated to be returned. In order to delete default settings, model object is created which will be of `UserDefaultSettingRemoveModel` type and will be passed as a parameter to the `UsersDefaultSettingsDeleteAsync` method in order to delete an default setting for user. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
The **model** object is the required parameter to enter that contains Key (String_type), AudienceId (Integer_type), and Propagate (bool_type) parameters. The key is the required parameter to enter for removing the user's default setting. 
  
The class name of the model is   
  
```markdown 
     UserDefaultSettingRemoveModel
```   
  
#### model Object Parameters 
 
![147](https://user-images.githubusercontent.com/110983629/189491424-c7456952-fd1b-4985-9d2b-0b27dbbd0593.png)

  
#### Explorer 

|Names|Description|
|-----|-----------|
|model (required)|[Models.UserDefaultSettingRemoveModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/user-default-setting-remove-model)|
  
 
#### Responses  

The response of this endpoint service request contains the `Task<object>` object that will indicate whether the user default setting is deleted or not.
  

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|
    
  
  
  
  
  
### Users General Default Settings Get
#### Description
This service endpoint will allow the user to retrieve the general default settings of the user that will be automatically added to each new user account when it is created. For this purpose, the `UsersGeneralDefaultSettingsGetAsync` method is called by creating an instance of **UsersController** class which is accessed from the API client. 
  
```markdown
 UsersGeneralDefaultSettingsGetAsync()
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
try
{
    List<UserDefaultSetting> result = await usersController.UsersGeneralDefaultSettingsGetAsync();
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "usersController" object fails to retrieve the user's general default settings details that was anticipated to be returned. The list of default settings will get returned against this endpoint request through method `UsersGeneralDefaultSettingsGetAsync` invoked. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail   
This endpoint does not take any parameter to process and retrieve the user default settings 
 
#### Responses  

The response of this endpoint service request contains the `Task<List<Models.UserDefaultSetting>>` object. The class name of the ResponseType object is 

```markdown 
    UserDefaultSetting
``` 
 
#### Response body-JSON  
```markdown 
{
  "Id": null,
  "Key": null,
  "Value": null,
  "Description": null,
  "AudienceId": null,
  "Level": null,
  "Enabled": false,
  "DataType": "DataType4",
  "Audience": null
} 
```

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

    
##### `Task<List<Models.UserDefaultSetting>>` Object Parameters  
   
![148](https://user-images.githubusercontent.com/110983629/189491822-6533d544-dbc2-458a-8968-25dbe87aebf3.png)

  
#### Explorer 

|Names|Description|
|-----|-----------|
|ResponseType|[Task<List<Models.UserDefaultSetting>>](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/user-default-setting)|

 
  
  
  
  
  
  
  
  
  
  
### Users General Default Settings Put
#### Description
This service endpoint will allow the user to modify General Default Settings that can be propagated to each User in Active Audience. For this purpose, the `UsersGeneralDefaultSettingsPutAsync` method is called by creating an instance of UsersController class which is accessed from the API client. 
  
```markdown
 UsersGeneralDefaultSettingsPutAsync(
    Models.UpdateUsersGeneralDefaultSettingsBindingModel model)
```

This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization)

#### Class-Object
```markdown
var model = new UpdateUsersGeneralDefaultSettingsBindingModel();
try
{
    object result = await usersController.UsersGeneralDefaultSettingsPutAsync(model);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the "usersController" object fails to update general default settings of the user that was anticipated to be returned. In order to update general default settings, model object is created which will be of `UpdateUsersGeneralDefaultSettingsBindingModel` type and will be passed as a parameter to the `UsersGeneralDefaultSettingsPutAsync` method in order to update an General default setting for user. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail  
The **model** object is the required parameter to enter that contains UsersGeneralDefaultSettings object and Reset (bool type) parameter. The **UsersGeneralDefaultSettings** object is required to enter that further contains the  key (String_type), MValue (String_type), AudienceId (Integer_type), Description (String_type), Level (String_type), Enabled (bool_type), DataType (String_type), and Propagate (bool_type) parameters. The key and MValue are the required parameters of the UsersGeneralDefaultSettings object.
  
The class name of the model is   
  
```markdown 
    UserDefaultSettingBindingModel
```   
  
#### model Object Parameters 
 
![149](https://user-images.githubusercontent.com/110983629/189492323-e5d5b701-926c-4a8a-a9d7-93ea762f2a81.png)

  
#### Explorer 

|Names|Description|
|-----|-----------|
|model (required)|[Models.UpdateUsersGeneralDefaultSettingsBindingModel](https://developers.icheckdev.com/auth/#/net-standard-library/models/structures/user-default-setting-binding-model)|
  
 
#### Responses  

The response of this endpoint service request contains the `Task<object>` object that will indicate whether the users general default setting is updated or not.
  

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

  
  
  
  
### Users Apps Get 
#### Description
This service endpoint will allow the user to retrieve the apps by entering the username. All the apps associated with the user account get retrieved whose username is entered to access them. For this purpose, the `UsersAppsGetAsync` method is called by creating an instance of **UsersController** class which is accessed from the API client.  
  
  
```markdown
   UsersAppsGetAsync(
    string username)
``` 
  
This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
string username = "username0";
try
{
    await usersController.UsersAppsGetAsync(username);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the `usersController` object fails to retrieve the apps that was anticipated to be returned. In order to get apps of the user, `UsersAppsGetAsync` method is used that takes the username as a parameter. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail   
This service endpoint requires only one parameter which is **username** unique for each user. It is required for the user to enter username which is of String type for retrieving all the apps associated with it.
  
![150](https://user-images.githubusercontent.com/110983629/189492653-242444d8-3d7c-4e82-9dd8-73d0de7ed4a1.png)

    
#### Responses  
 
The response of this endpoint service request contains the `Task` which returns the value for successfully retrieving the user's apps.   
  

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

  
#### Errors

|HTTP Status Code|Error Description| Exception Class|
|-----|-----------|----|
|400|Bad Request|ApiException|
 
The errors that can be reported in response to this API call are listed in the error table above. The 4xx demonstrates that it is possible to make a poor request while requesting a user's apps.  
 
  
  
  
  

  
### Users Settings Get 
#### Description
This service endpoint will allow the user to retrieve the permissions by entering the username. All the permissions associated with the user account get retrieved whose username is entered to access them. For this purpose, the `UsersSettingsGetAsync` method is called by creating an instance of **UsersController** class which is accessed from the API client.  
  
  
```markdown 
  UsersSettingsGetAsync(
    string username)
``` 
  
This endpoint requires [Authentication](https://developers.icheckdev.com/auth/#/net-standard-library/getting-started/how-to-get-started/authorization) 

#### Class-Object
```markdown
string username = "username0";
try
{
    await usersController.UsersSettingsGetAsync(username);
}
catch (ApiException e){};
```  
  
It will be included in the try and catch block to deal with any exceptions that could arise if the `usersController` object fails to retrieve the permissions that was anticipated to be returned. In order to get permissions of the user, `UsersSettingsGetAsync` method is used that takes the username as a parameter. This try catch block will take care of any exceptions that are thrown in order to prevent unhandled exceptions, user error, or application crashes.  

#### Parameters Detail   
This service endpoint requires only one parameter which is **username** unique for each user. It is required for the user to enter username which is of String type for retrieving all the permissions associated with it.
   
![151](https://user-images.githubusercontent.com/110983629/189492869-328c898c-9af7-41ac-a508-7a67c33e868d.png)

#### Responses  
 
The response of this endpoint service request contains the `Task` which returns the value for successfully retrieving the user's permissions.   
  

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

  
#### Errors

|HTTP Status Code|Error Description| Exception Class|
|-----|-----------|----|
|400|Bad Request|ApiException|
 
The errors that can be reported in response to this API call are listed in the error table above. The 4xx demonstrates that it is possible to make a poor request while requesting a user's permissions.  
   
  
  
  
  
  
  
  
  
  
  
  
  
  
  

  
  
  
  
  
  
  
  
