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
 


#### Parameters Detail  
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
This service endpoint will allow the user to reterive all the audiences that are active. For this purpose, the `AudiencesGetAsync` method is called by creating an instance of `AudiencesController` class which is accessed from the API client. 
  
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

  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
