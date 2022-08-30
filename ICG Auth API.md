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
### ICG Verify Process
#### Description
     
ICG Verify Process is the process where we validate a pair of information containing both routingNumber that must be of 9-digits and accountNumber that must be of 14 digits for the same bank that is being validated. After the account has been created,  you will need to verify the information by accessing the intance of the **IcgVerifyController** from the API client. 
  
```markdown
  IcgVerifyController icgVerifyController = client.IcgVerifyController;
```
  

#### Class-Object
```markdown
 var request = new ICGVerifyModelsIcgVerificationICGVerifyRequest();
 request.BankAccount = new ICGVerifyModelsIcgVerificationICGVerifyBankAccount();
 request.BankAccount.RoutingNumber = "routingNumber0";
 request.BankAccount.AccountNumber = "accountNumber4";

 try
 {
    ICGVerifyModelsICGVerifyResponse result = await icgVerifyController.ICGVerifyProcessAsync(request);
 }
 catch (ApiException e){};
```
  
#### Response body-JSON
{
  "Message": "Authorization has been denied for this request."
}
  

#### Response headers-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

 
Below are listed all the possible codes returned from the process

|ICG Code | ICG Decision Value | Description |
|---------|--------------------|-------------|
|I001|ACCEPT |There is no negative information known on the account|
|I002|DECLINED|Customer has returned item(s) in the past 12 months that were returned due to unauthorized.The number of unauthorized returns reported with also be returned in a property message field|
|I003|DECLINED|The RVD database does not have a current unpaid return but the account has been reported as closed or a returned item that has been paid was returned as account closed|
|I004|DECLINED|The RVD database does not have a current unpaid return but we have seen returns in the past for Account not Fount or Invalid account number at the bank|
|I005|DECLINED|Customer has returned items(s) in the past 12 months that were returned due to being ineligible|
|I006|DECLINED|Customer has no unpaid returns at this time in RVD but has a history of returns in the last 12 months|
|I007|DECLINED|Account reported Closed|
|I008|DECLINED|Bank routing number is not a vaild US routing #|
|I009|DECLINED|Negative Data - Negative information was found|
|I010|WARNING|The routing number submitted belongs to a financial institution; however, this financial institution does not report information to the National Shared Database.No positive or negative information found for this routing number and account number.|
|I011|WARNING|Account number format is suspicious|
|I012|DECLINED|Account Number is less than 3 digits or contains an invalid character|


This endpoint requires [authentication](https://developers.icheckdev.com/Verify/#/net-standard-library/getting-started/how-to-get-started/authorization).
  
```markdown
ICGVerifyProcessAsync(Models.ICGVerifyModelsIcgVerificationICGVerifyRequest request)
```
  
  
#### Parameters details
The parameters for the ICG verify process in **.NET** are **BankAccount**, **RuleNum** and **GatewayLive**.  We have one required object here that collects information as the parameter which includes **RoutingNumber** and **AccountNumber** as necessary fields that must be filled during the verification process. Whereas, two fields act as optional fields that are not necessary to be filled during the verification process; one is **OrgInfo(organization information)** and other one is **TypeofBankAcct (Type of bank account)**. User can enter name in *string* format for the orgInfo and select from the displayed list options for bank account type which are Checking, Savings, Personal Loan.      

##### 'request' Object Parameters
  
![25](https://user-images.githubusercontent.com/110983629/187240602-4a74b5ad-f274-48f7-8b77-898cc10fa968.png)

  
The class name for the ICG verify base request is
  
 ```markdown
ICGVerifyModelsIcgVerificationICGVerifyRequest
  ```
  
##### 'BankAccount' Object Parameters

![26](https://user-images.githubusercontent.com/110983629/187240843-0813bd45-6759-466a-b9c0-1a6dc2d195b6.png)

The class name for the **BankAccount** is 
  
 ```markdown
 ICGVerifyModelsIcgVerificationICGVerifyBankAccount
  ```
  
  
 
#### Explorer 

|Names|Description|
|-----|-----------|
|BankAccount(required)|[Models.ICGVerifyModelsIcgVerificationICGVerifyBankAccount](https://developers.icheckdev.com/Verify/#/net-standard-library/models/structures/icg-verify-models-icg-verification-icg-verify-bank-account)
|ruleNum|String Rule number-assigned by MicroBilt|
|gatewayLive|Boolean Enable or disable the live|


#### Responses 

#### Response headers-JSON

|Header|Value|
|------|-----|
|Authorization|Authorization|
|Accept|application/json|
|Content-type|application/json;charset=utf-8|

#### Response body-JSON

```markdown
 {
  "code": null,
  "decision": null,
  "description": null,
  "addendaRecords": null,
  "error": null
}
```
  
The following parameters are provided in the response from the ICG verification procedure in **.NET** to inform the user of the base request response:  
  
  1. **Code:** It will be of _string_ type. This code is the identification key for each type of response, this API call returns.
  2. **decision:** It will be of _string_ type. This parameter specifies the status of the response whether it is accepted response, declined etc as mentioned in the above table of responses. 
  4. **description:** It will be of _string_ type which will acknowledge user about the API response in form of text information. 
  5. **addendaRecords:** It will be an _object_ that further contains the key, value, description fields of string type. This object basically used for providing additional information to the consumers.
  6. **error:** It will be of _string_ type that specifies the error if that occur during the API call. 
  
 ##### 'ResponseType' Object Parameters
  
 ![27](https://user-images.githubusercontent.com/110983629/187244317-b99e5e79-18a2-44a7-ae57-9a39e2faa264.png)

The class name for the **ResponseType** object is 
  
  ```markdown
  ICGVerifyModelsICGVerifyResponse
  ```
  
  
