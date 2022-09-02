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


#### API Parameters
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


#### API Parameters
  
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


#### API object Parameters
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

#### Model object Parameters 
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

  
#### Model object Parameters 
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


#### API object Parameters
  
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

#### API Parameters 
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

#### API Parameters 
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

#### API Parameters 
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

#### API Parameters 
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

#### API Parameters 
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

#### API Parameters 
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

#### API Parameters 
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

#### API Parameters 
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
  
  
  


  
  
  
  
  
  
