# API Documentation (Verify API)
# For HTTP
## Getting Started

### Description

Welcome to the iCheckGateway Verify API. iCheckGateway.com makes it easy to integrate any online application or back office solution for ACH check payment processing and credit card processing. Using iCheckGateway.com’s APIs, developer tools, and plugins, you can create a payment platform that is customized to the needs of your business. The integration of these APIs will allow the customers to pay by echeck, ACH transfer, or credit/debit card. 
ICG Verify API endpoints include all the information to use the ICG Verify Service and perform ACH Verification

#### Base URL
The API uses the following base URL:

> https://verify.icheckdev.com 

#### Authorization 
This API uses the following header parameters for authentication.
|Header       | Default   |Description|
|-------------|-----------|-----------|
|Authorization| None      | API Access token provided by the Auth API after User authentication| 

The request looks like this:
```markdown
curl https://verify.icheckdev.com \
  -H 'Authorization: {AUTHORIZATION}'
 ```
 
 ```markdown
 GET / HTTP/1.1
Host: {HOST}
Authorization: {AUTHORIZATION}
```

## API Endpoints
## ICG Verify
### ICG Verify Process
#### Description
ICG Verify Process is the process where we validate a pair of information containing both routingNumber that must be of 9-digits and accountNumber that must be of 14 digits for the same bank that is being validated. After the account has been created,  you will need to verify the information by making a **POST /IcgVerify/Process** request
#### POST-JSON
```markdown
curl -X POST \
  --url 'https://verify.icheckdev.com/IcgVerify/Process' \
  -H 'Authorization: Authorization'\
  -H 'Accept: application/json'\
  -H 'Content-Type: application/json' \
  --data-raw '{
  "bankAccount": {
    "routingNumber": "routingNumber0",
    "accountNumber": "accountNumber4"
  }
}`
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

#### Verify process configuration
![image](https://user-images.githubusercontent.com/110983629/185741727-7d22226f-cc5f-4649-a0c6-e28c24ec9858.png)


Above are listed all the possible codes returned from the process

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


This endpoint requires [authentication](https://developers.icheckdev.com/Verify/#/http/getting-started/how-to-get-started/authorization).
```markdown
POST /IcgVerify/Process
```
#### Parameters details
Listed below is a list of all the parameters that the end point can receive. We have request object here that collects **bankAccount*** information as the parameter. bankAccount requires **routingNumber** and **accountNumber** as necessary fields that must be filled during the verification process. Whereas, two fields act as optional fields that are not necessary to be filled during the verification process; one is **orgInfo(organization information)** and other one is **typeofBankAcct (Type of bank account)**. User can enter name in *string* format for the orgInfo and select from the displayed list options for bank account type.

##### 'request' Object Parameters
![image](https://user-images.githubusercontent.com/110983629/185380812-6612f04c-39d8-4d0d-9d9b-63ed3eee0c69.png)
##### 'bankAccount' Object Parameters
![image](https://user-images.githubusercontent.com/110983629/185381223-722ea2c6-fe07-4fcf-821a-b0d83ec477e9.png)


#### Explorer 

|Names|Description|
|-----|-----------|
|bankAccount(required)|[ICG Verify Models Icg Verification ICG Verify Bank Account](https://developers.icheckdev.com/Verify/#/http/models/structures/icg-verify-models-icg-verification-icg-verify-bank-account)
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

The response of the ICG verification process is 200, OK. It will contain a **Type** object that have the following parameters:
  1. **Code:** It will be of _string_ type. This code is the identification key for each type of response, this API call returns.
  2. **decision:** It will be of _string_ type. This parameter specifies the status of the response whether it is accepted response, declined etc as mentioned in the above table of responses. 
  4. **description:** It will be of _string_ type which will acknowledge user about the API response in form of text information. 
  5. **addendaRecords:** It will be an _object_ that further contains the key, value, description fields of string type. This object basically used for providing additional information to the consumers.
  6. **error:** It will be of _string_ type that specifies the error if that occur during the API call. 
  
 ##### 'Type' Object Parameters
 
 ![2  response of simple verify](https://user-images.githubusercontent.com/110983629/185617059-6db57703-12ca-4286-8da1-6bfa70d6b586.png)


### ICG Verify Process Extended
#### Description
This is the extended version of the ICG Verify feature. It only can be used if the merchant provided has the permission _FEATURE_ICG_VERIFY_EXTENDED_  assigned to the related user authenticated. As this extended verification process is for the commercial users i.e., merchants so this will need more verification parameters than the usual user. This feature exploits all the microbilt options to validate the merchant account based on many other parameters besides the Bank Route Number and Account Number.

The responses and response codes on this endpoint are same as the one listed above in the 'ICG Verify Process' section.

#### POST-JSON
```markdown
curl -X POST \
  --url 'https://verify.icheckdev.com/IcgVerify/ProcessExt' \
  -H 'Authorization: Authorization'\
  -H 'Accept: application/json'\
  -H 'Content-Type: application/json' \
  --data-raw '{
  "bankAccount": {
    "routingNumber": "routingNumber0",
    "accountNumber": "accountNumber4"
  }
}'
```

#### Response body-JSON
![image](https://user-images.githubusercontent.com/110983629/186658697-5ec5e081-daa8-46a0-b62b-0297748d3f72.png)

#### Response header-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

#### Verify process extended configuration
![image](https://user-images.githubusercontent.com/110983629/185741637-4488ded8-0adf-4e9f-a9c5-30edf47fad06.png)

This endpoint requires [authentication](https://developers.icheckdev.com/Verify/#/http/getting-started/how-to-get-started/authorization)
```markdown
POST /IcgVerify/ProcessExt
```
#### Parameters details
The following list describes the parameters that user must have to define for getting verified through the ICG extended process. Many of them are not required depends upon the importance of the parameter. For example, the **bankAccount** object is required to add in order to get verified successfully. Lets have a look on the following image for getting informations about all the parameters i.e. objects and single attributes of this API call.    

![API-extended-1](https://user-images.githubusercontent.com/110983629/185582289-e785b0b8-07c6-469b-8509-fba38bd1182c.png)

1. The required **bankAccount** is the object that contains the _orgInfo_(organization info) object which further consists of the name of the employer. The employer name is of _string_ type. The other parameters are _routingNumber_ (9-digit string), _accountNumber_ (String), _typeOfBankAcct_ object (having Checking, Savings, Personal Loan in String type). The _routingNumber_ and _accountNumber_ both are required for ICG extended verification process.

##### 'bankAccount' Object Parameters
![api-extended-2](https://user-images.githubusercontent.com/110983629/185610417-305af729-4d11-48ae-8bb1-13c7c0b3f1d2.png)

2. The personal Info object consists of the following objects further:
##### 'personInfo' Object Parameters
![personal info](https://user-images.githubusercontent.com/110983629/185611209-decd5035-3b5a-4162-9797-972db2ad240e.png)

    - personName (It has consumer's first name and last name of string type)
    - contactInfo (It has phoneNumber object (phoneType, 10-digit phone number), emailAddress (string type), postAddr (addr1 (String type), city (String type), stateProv (String type), postalCode(String type)))
    - tinInfo is the object that contains the tinType (integer type of >= 0 and <=8), taxId which is a text identification number of string type.
    - diverseLicense is the object that contains licenseNum, stateProv parameters (both of string type) where the licenseNum is the driver's license number and stateProv is the state of issuence which is 2-digit state code. 
    - employmentHistory is the object that contains the organziation info object which further contains the employer name (of string type)
    
    
**3. 'incomeInfo' Object Parameters**

![income info](https://user-images.githubusercontent.com/110983629/185611627-769b1abc-d303-4233-b1fa-2b38344d4400.png)


**4. 'references' Object Parameters**

![5  references](https://user-images.githubusercontent.com/110983629/185611831-1b3ebddd-c49a-4ac2-a878-d05fc7a44d24.png)


**5.'checkAmt' Object Parameters**

![6  checkAmt](https://user-images.githubusercontent.com/110983629/185611998-13e65e85-d21b-49c9-8dff-4ba7a690c388.png)


#### Explorer 


|Names|Description|
|-----|-----------|
|bankAccount(required)|[ICG Verify Models Icg Verification ICG Verify Bank Account](https://developers.icheckdev.com/Verify/#/http/models/structures/icg-verify-models-icg-verification-icg-verify-bank-account)
|personInfo|[ICG Verify Models Icg Verification ICG Verify Person Info](https://developers.icheckdev.com/Verify/#/http/models/structures/icg-verify-models-icg-verification-icg-verify-person-info)
|incomeInfo|[ICG Verify Models Icg Verification ICG Verify Income Info](https://developers.icheckdev.com/Verify/#/http/models/structures/icg-verify-models-icg-verification-icg-verify-income-info)
|references|[array<ICG Verify Models Icg Verification ICG Verify References>](https://developers.icheckdev.com/Verify/#/http/models/structures/icg-verify-models-icg-verification-icg-verify-references)
|checkAmt|[ICG Verify Models Icg Verification ICG Verify Check Amt](https://developers.icheckdev.com/Verify/#/http/models/structures/icg-verify-models-icg-verification-icg-verify-check-amt)
|checkNum|Check number of string type|
|laneId|Lane number of string type|
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


The response of the ICG verification extend process is 200, ok. It will contain a **Type** object that have the following parameters:
  1. Code: It will be of _string_ type. This code is the identification key for each type of response, this API call returns.
  2. decision: It will be of _string_ type. This parameter specifies the status of the response whether it is accepted response, declined etc as mentioned in the above table of responses. 
  4. description: It will be of _string_ type which will acknowledge user about the API response in form of text information. 
  5. addendaRecords: It will be an object that further contains the key, value, description fields of _string_ type. This object basically used for providing additional information to the consumers.
  6. error: It will be of _string_ type that specifies the error if that occur during the API call. 
  
 ##### 'Type' Object Parameters
  
![1  extend response](https://user-images.githubusercontent.com/110983629/185638275-5193e691-00cd-49a5-8b04-224fc5a94a5c.png)


 
## ICG Verify Legacy
### ICG Verify Legacy Process
#### Description
This is the ICG verify legacy process that will validate the routing number and account number. Both of these fields are required fields. This API call is executed when the merchant want to verify the data by updating merchant rule after getting authenticated. This feature will not exploit the microbilt options to validate an account based on many other parameters besides the Bank Route Number and Consumer Account Number.

The responses on this endpoint are same as the one listed above in the 'ICG Verify Process' section  
  
#### POST

```markdown
curl -X POST \
  --url 'https://verify.icheckdev.com/IcgVerifyLegacy/Process' \
  -H 'Authorization: Authorization'\
  -H 'Accept: application/json'\
  -H 'Content-Type: application/json' \
  --data-raw '{
  "bankAccount": {
    "routingNumber": "routingNumber0",
    "accountNumber": "accountNumber4"
  }
}'
```
This endpoint requires [authentication](https://developers.icheckdev.com/Verify/#/http/getting-started/how-to-get-started/authorization)
```markdown
POST /IcgVerifyLegacy/Process
```

  
#### Parameters details
  
The following list describes the parameters that user must have to define for getting verified through the ICG legacy process.The bank routing number and consumer's account number are required fields for this API call. The organization info, type of bank account etc are other parameters that needs to add for this API call. Lets have a look on the following image for getting informations about all the parameters i.e. objects and single attributes of this API call.    
  
  ##### 'ICG Legacy verification Process' API call Parameters
  
![1  legacy](https://user-images.githubusercontent.com/110983629/185653468-2b73071b-07c0-4465-a865-ce674e9a1027.png)

  
 1. The bankAccount object further contains the 6-digits rounting number, account number, and organization info, type of bank objects. The organization info object contains the employeer name parameter which is of string type. The type of bank account contains the three fields which are checking, Savings, PersonalLoan as shown in the following image:
  
##### 'bankAccount' Object Parameters
  
![1  legacy bank account](https://user-images.githubusercontent.com/110983629/185653358-059ecf87-af16-4254-b37e-bf0002e4e856.png)
  

#### Explorer 


|Names|Description|
|-----|-----------|
|bankAccount(required)|[ICG Verify Models Icg Verification ICG Verify Bank Account](https://developers.icheckdev.com/Verify/#/http/models/structures/icg-verify-models-icg-verification-icg-verify-bank-account)
|updateMerchant|Boolean Enable or disable for updating merchant|
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

The response of the ICG legacy verification process is 200, OK. It will contain a **Type** object that have the following parameters:
  1. **Code:** It will be of _string_ type. This code is the identification key for each type of response, this API call returns.
  2. **decision:** It will be of _string_ type. This parameter specifies the status of the response whether it is accepted response, declined etc as mentioned in the above table of responses. 
  4. **description:** It will be of _string_ type which will acknowledge user about the API response in form of text information. 
  5. **addendaRecords:** It will be an _object_ that further contains the key, value, description fields of string type. This object basically used for providing additional information to the consumers.
  6. **error:** It will be of _string_ type that specifies the error if that occur during the API call. 
  
 ##### 'Type' Object Parameters
 
![1  legacy response](https://user-images.githubusercontent.com/110983629/186683541-5914fc6b-4a1d-4904-9361-cf530a78cff4.png)


# For Java
## How to get started
#### Description 
  
Welcome to the iCheckGateway Verify API. iCheckGateway.com makes it easy to integrate any online application or back office solution for ACH check payment processing and credit card processing. Using iCheckGateway.com’s APIs, developer tools, and plugins, you can create a payment platform that is customized to the needs of your business. The integration of these APIs will allow the customers to pay by echeck, ACH transfer, or credit/debit card. 
ICG Verify API endpoints include all the information to use the ICG Verify Service and perform ACH Verification

#### Install the Package
For utilizing this API, Install the SDK by adding the following dependency in your project's pom.xml file:

```markdown
<dependency>
  <groupId>com.payquicker</groupId>
  <artifactId>sample-sdk-artifact-id</artifactId>
  <version>1.0.0</version>
</dependency>
```
  
You can also access the package at:
> https://mvnrepository.com/artifact/com.payquicker/sample-sdk-artifact-id/1.0.0
  
  
#### API Client Configuration Parameters: 
|Parameter       | Type                           |Description|
|----------------|--------------------------------|-----------------------------------|
|httpClientConfig|ReadonlyHttpClientConfiguration |Http Client Configuration instance.|   
|authorization   | String                         |                                   |
  
  
#### Authorization 
This API uses the ```markdown Custom Header Signature ```

The API client configuration looks like this:
```markdown
 ICGAPIVerifyClient client = new ICGAPIVerifyClient.Builder()
    .httpClientConfig(configBuilder -> configBuilder
            .timeout(0))
    .customHeaderAuthenticationCredentials("Authorization")
    .build(); 
 ```
 
  
## API Endpoints
### ICG Verify
### ICG Verify Prcoess
#### Description
In order to be identified effectively, the ICG verify procedure involves checking the customer's account number and routing number. The JAVA's ICG Verify process endpoints include all the data necessary to use the ICG Verify Service and carry out ACH Verification. By sending the parameters included in the POST request, you must validate the information.
 
  
#### Class-Object
```markdown 
ICGVerifyModelsIcgVerificationICGVerifyRequest request = new ICGVerifyModelsIcgVerificationICGVerifyRequest();
request.setBankAccount(new ICGVerifyModelsIcgVerificationICGVerifyBankAccount());
request.getBankAccount().setRoutingNumber("routingNumber0");
request.getBankAccount().setAccountNumber("accountNumber4");

icgVerifyController.iCGVerifyProcessAsync(request).thenAccept(result -> {
    // TODO success callback handler
}).exceptionally(exception -> {
    // TODO failure callback handler
    return null;
});
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
 

The Following table describes all the possible codes returned from the process.

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


This endpoint requires [authentication](https://developers.icheckdev.com/Verify/#/java/getting-started/how-to-get-started/authorization).
```markdown
   CompletableFuture<ICGVerifyModelsICGVerifyResponse> iCGVerifyProcessAsync(
    final ICGVerifyModelsIcgVerificationICGVerifyRequest request)
```
#### Parameters details  

The parameters of the basic request are members of particular classes that are used to validate the ICG process in Java. For the base request, which also includes the **OrgInfo** object, **RoutingNumber**, **AccountNumber**, and **typeofBankAcct**, the **bankAccount** object. The necessary parameters are the consumer's account number (String) and routing number (9 digits). While two fields—orgInfo (organisation information) and typeofBankAcct (type of bank account)—serve as optional entries that are not required to be filled out throughout the verification procedure. The user may choose the bank account type from the list of types and provide their name in *string* format for the orgInfo.
  
  
##### 'request' Object Parameters 
![1  java-verify process-request](https://user-images.githubusercontent.com/110983629/186711002-7bbc3b60-2be1-4d20-b07a-67c4fa503bf9.png)

The Class Name of the **bankAccount** object is ```markdown ICGVerifyModelsIcgVerificationICGVerifyBankAccount ```
  
##### 'bankAccount' Object Parameters 

![2  java request- verify process](https://user-images.githubusercontent.com/110983629/186711705-96ed9a8d-cc93-4929-a6f3-688f226b14e5.png)
  
The Class Name of the **OrgInfo** object is ```markdown ICGVerifyModelsIcgVerificationICGVerifyOrgInfo```
  
##### 'OrgInfo' Object Parameters  

![3  java ](https://user-images.githubusercontent.com/110983629/186712170-968902c9-3682-4774-a440-018ca381dc35.png)

  
The Class Name of the **TypeOfBankAcct** object is ```markdown TypeOfBankAcctEnum```
  
##### 'TypeOfBankAcct' Object Parameters  

![4  java -verify](https://user-images.githubusercontent.com/110983629/186712666-23120dca-e2ba-4ec6-8568-d1000c5d014d.png)


#### Explorer 

|Names|Description|
|-----|-----------|
|bankAccount(required)|[ICGVerifyModelsIcgVerificationICGVerifyBankAccount](https://developers.icheckdev.com/Verify/#/java/models/structures/icg-verify-models-icg-verification-icg-verify-bank-account)
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

The response of the ICG verification process is 200, OK. It will contain a **ResponseType** object that have the following parameters:
  1. **Code:** It will be of _string_ type. This code is the identification key for each type of response, this API call returns.
  2. **decision:** It will be of _string_ type. This parameter specifies the status of the response whether it is accepted response, declined etc as mentioned in the above table of responses. 
  4. **description:** It will be of _string_ type which will acknowledge user about the API response in form of text information. 
  5. **addendaRecords:** It will be an _object_ that further contains the key, value, description fields of string type. This object basically used for providing additional information to the consumers. The class Name of **theaddendaRecords** object is ```markdown ICGVerifyModelsICGVerifyResposeAddendaRecords```
  6. **error:** It will be of _string_ type that specifies the error if that occur during the API call. 
    
 
 The Class Name of the **ResposneType** object is ```markdown ICGVerifyModelsICGVerifyResponse```
  
 ##### 'ResposneType' Object Parameters
 
![5  java verify response](https://user-images.githubusercontent.com/110983629/186715139-2f820787-7d15-4ed4-afcd-a84de6e6ec92.png)


#### Explorer 

|Names|Description|
|-----|-----------|
|ResponseType|[ICGVerifyModelsICGVerifyResponse](https://developers.icheckdev.com/Verify/#/java/models/structures/icg-verify-models-icg-verify-response)
 
  
### ICG Verify Process Extended
#### Description
This is the Java-based ICG verify process' expanded version. It may only be used if the merchant given has assigned the corresponding user authenticated the permission FEATURE ICG VERIFY EXTENDED. This functionality makes use of every microbilt option available to validate an account using criteria other than the Bank Route Number and Account Number. The replies on this endpoint are identical to those in the section above titled "ICG Verify Process." 
  
The responses and response codes on this endpoint are same as the one listed above in the 'ICG Verify Process' section.

#### Class-Object
  
```markdown
ICGVerifyModelsIcgVerificationICGVerifyRequestExt request = new ICGVerifyModelsIcgVerificationICGVerifyRequestExt();
request.setBankAccount(new ICGVerifyModelsIcgVerificationICGVerifyBankAccount());
request.getBankAccount().setRoutingNumber("routingNumber0");
request.getBankAccount().setAccountNumber("accountNumber4");

icgVerifyController.iCGVerifyProcessExtendedAsync(request).thenAccept(result -> {
    // TODO success callback handler
}).exceptionally(exception -> {
    // TODO failure callback handler
    return null;
});
```
   
#### Response body-JSON
{
  "Message": "Authorization has been denied for this request."
}
 
#### Response header-JSON
|Header|Value|
|------|-----|
|Cache-control|Private|
|Content-Length|61|
|Content-type|application/json;charset=utf-8|

 
This endpoint requires [authentication](https://developers.icheckdev.com/Verify/#/java/getting-started/how-to-get-started/authorization)
 
```markdown
  CompletableFuture<ICGVerifyModelsICGVerifyResponse> iCGVerifyProcessExtendedAsync(final ICGVerifyModelsIcgVerificationICGVerifyRequestExt request)
  ```  
  
  
#### Parameters details
The following parameters are employed for ICG extended process. Where many of them are not required to add. Only the **bankAccount** object is required. Lets have a look on the following image for getting information about all the parameters i.e. objects and single attributes of this API call.       
   
![7  java extend](https://user-images.githubusercontent.com/110983629/186726899-0c73dca4-1d16-4616-90fb-9a0bf55d2381.png)

  
The class name of the extend verify request is ```markdown ICGVerifyModelsIcgVerificationICGVerifyRequestExt ```

1. The required **BankAccount** is the object that contains the _orgInfo_(organization info) object which further consists of the name of the employer. The employer name is of _string_ type. The other parameters are _routingNumber_ (9-digit string), _accountNumber_ (String), _typeOfBankAcct_ object (having Checking, Savings, Personal Loan in String type). The _routingNumber_ and _accountNumber_ both are required for ICG extended verification process. The class name of the **bankAccount** object ```markdown ICGVerifyModelsIcgVerificationICGVerifyBankAccount ```
  
  
##### 'BankAccount' Object Parameters
![6  java verify extend](https://user-images.githubusercontent.com/110983629/186724604-19621235-bb7f-4b0e-909d-ab07adb0b0bd.png)


2. The **PersonInfo** object consists of the following objects further:
![1  java extend personinfo](https://user-images.githubusercontent.com/110983629/187030694-50347bb8-4131-4f3b-826b-e83df4be8911.png)
  
The Class Name for the **PersonInfo** object is ```markdown ICGVerifyModelsIcgVerificationICGVerifyPersonInfo ```. It further contains the _PersonName_, _ContactInfo_, _TinInfo_, _DriversLicense_, _EmploymentHistory_ objects that are shown below:
  
  ##### 'PersonName' Object Class name and Parameters  
  ![2  java extend personinfo](https://user-images.githubusercontent.com/110983629/187030838-9f27b5aa-5b12-476e-ab81-d07a80d8cdb9.png)

  ##### 'ContactInfo' Object Class name and Parameters   
  ![3  java extend](https://user-images.githubusercontent.com/110983629/187030981-74685bdc-e52c-4583-8a06-295f5fcdea94.png)

  ##### 'TinInfo' Object Class name and Parameters   
  ![4  java extend ](https://user-images.githubusercontent.com/110983629/187031014-4486b633-8aa7-414f-a0f1-fe6ecbdc099a.png)

   ##### 'DriversLicense' Object Class name and Parameters   
   ![5  java extend](https://user-images.githubusercontent.com/110983629/187031050-83fa1b41-69b6-4b06-ade3-5c96fbbf2604.png)

   ##### 'EmploymentHistory' Object Class name and Parameters  
   ![6  java extend](https://user-images.githubusercontent.com/110983629/187031086-93d8403f-8b85-43af-ba71-a3b2917f4c90.png)

  
3. The **IncomeInfo** object contains the _DtOfNextPaycheck_ parameter which is the date of next paycheck and _DtOfSecondPaycheck_ parameter which is the date of next second pay check. Both of these dates are of _string_ type. The class name for the **IncomeInfo** object is ```markdown ICGVerifyModelsIcgVerificationICGVerifyIncomeInfo```
  
   ![7  java extend income info](https://user-images.githubusercontent.com/110983629/187031425-751f0c3d-f467-4768-9cc7-40db643a9c9c.png)
  
   The **MonthlyIncome** Object Class name and Parameters  
   ![8](https://user-images.githubusercontent.com/110983629/187031812-35ae335e-a44e-4d12-8d78-3b9fa3a9ca45.png)
  
   The **PmtFreq** Object Class name and Parameters  
   ![9](https://user-images.githubusercontent.com/110983629/187032071-5d1f2a15-36fd-48ec-ac78-fff4c36a1be8.png)

  
   The **PayPerPeriod** Object Class name and Parameters  
   ![10](https://user-images.githubusercontent.com/110983629/187032128-73f8a1e2-bc14-47d9-a870-9d14845ff2cd.png)

4. The **References** object contains the **PhoneNum** object and **ContactName** parameter which is the name of the reference(_string_ type). The class name for the **References** object is ```markdown ICGVerifyModelsIcgVerificationICGVerifyReferences```
  
  
   ![11](https://user-images.githubusercontent.com/110983629/187033389-d529dbb2-a3b7-487b-9d28-00ec8c7c01c0.png)

  

   The **PhoneNum** object class name and Parameters
  
   ![12](https://user-images.githubusercontent.com/110983629/187032709-5a2c5f97-7d43-4d9c-8107-93dd3ffd6a9a.png)
  
  
   The **PhoneType** object class name and parameters
  
   ![13](https://user-images.githubusercontent.com/110983629/187032780-6a70b900-6527-4554-9239-d3337c2deadc.png)

  
  
 5. The **CheckAmt** object contains the **Amt** check amount parameter which is of _String_ type. The class name of this object is ```markdown ICGVerifyModelsIcgVerificationICGVerifyCheckAmt ```  
  
  ![14](https://user-images.githubusercontent.com/110983629/187033005-19498e23-06cb-49ac-bbf9-3a83a506ac07.png)
  
  
  
 #### Explorer 


|Names|Description|
|-----|-----------|
|BankAccount(required)|[ICGVerifyModelsIcgVerificationICGVerifyBankAccount](https://developers.icheckdev.com/Verify/#/java/models/structures/icg-verify-models-icg-verification-icg-verify-bank-account)
|PersonInfo|[ICGVerifyModelsIcgVerificationICGVerifyPersonInfo](https://developers.icheckdev.com/Verify/#/java/models/structures/icg-verify-models-icg-verification-icg-verify-person-info) 
|IncomeInfo|[ICGVerifyModelsIcgVerificationICGVerifyIncomeInfo](https://developers.icheckdev.com/Verify/#/java/models/structures/icg-verify-models-icg-verification-icg-verify-income-info)
|References|[List<ICGVerifyModelsIcgVerificationICGVerifyReferences>](https://developers.icheckdev.com/Verify/#/java/models/structures/icg-verify-models-icg-verification-icg-verify-references)
|CheckAmt|[ICGVerifyModelsIcgVerificationICGVerifyCheckAmt](https://developers.icheckdev.com/Verify/#/java/models/structures/icg-verify-models-icg-verification-icg-verify-check-amt)
|CheckNum|Check number of string type|
|LaneId|Lane number of string type|
|RuleNum|String Rule number-assigned by MicroBilt|
|GatewayLive|Boolean Enable or disable the live|


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


The response of the ICG verification extend process in JAVA is 200, ok. The class name of the **ResponseType** object is ```markdown ICGVerifyModelsICGVerifyResponse ```
It will contain a **ResponseType** object that have the following parameters:
  
  1. Code: It will be of _string_ type. This code is the identification key for each type of response, this API call returns.
  2. decision: It will be of _string_ type. This parameter specifies the status of the response whether it is accepted response, declined etc as mentioned in the above table of responses. 
  4. description: It will be of _string_ type which will acknowledge user about the API response in form of text information. 
  5. addendaRecords: It will be an object that further contain the key, value, description fields of _string_ type. This object basically used for providing additional information to the consumers.
  6. error: It will be of _string_ type that specifies the error if that occur during the API call. 
  
 ##### 'ResponseType' Object Parameters
  
 ![15](https://user-images.githubusercontent.com/110983629/187036736-55938c07-4157-46cb-9abb-1ef3a193cae0.png)


 
## ICG Verify Legacy
### ICG Verify Legacy Process
#### Description

The **routing number** and **account number** of the consumer given as the API call parameters are verified by this legacy ICG process in **JAVA**. The user must submit the aforementioned parameters for the legacy verification in order to research and assess the consumer for identification needs. This API request is sent by the merchant after authentication when they wish to update their merchant rules and check the data.      
  

The responses on this endpoint are same as the one listed above in the 'ICG Verify Process' section but it will appear in JAVa here as shown below:

```markdown
CompletableFuture<ICGVerifyModelsICGVerifyResponse> iCGVerifyLegacyProcessAsync(final ICGVerifyModelsIcgVerificationICGVerifyRequestLegacy request)
```
This endpoint also requires [Authentication](https://developers.icheckdev.com/Verify/#/java/getting-started/how-to-get-started/authorization)
  

  
#### Parameters details
  
The parameters for the ICG verify legacy process in JAVA includes **BankAccount**, **UpdateMerchant**, **RuleNum**, **GatewayLive**. The **BankAccount** object is required for this process call that contain the **RountingNumber** and Consumer's **AccountNumber** as a required parameters. The **RountingNumber** is the 9-digit number (_String_type). The **BankAccount** also contains the **OrgInfo** and **TypeOfBankAcct** as a non-required parameters. The following image shows the parameters for this process call.
    
![16](https://user-images.githubusercontent.com/110983629/187041248-6823dd17-c8a6-4a2e-9da7-72d1e7b6e1dd.png)

##### 'BankAccount' Object Parameters
  
![17](https://user-images.githubusercontent.com/110983629/187041289-76bffe2f-972d-4584-9054-5ddf4bd7b525.png)

The class name for the **BankAccount** object is ```markdown ICGVerifyModelsIcgVerificationICGVerifyBankAccount ```
  
The class name for the **OrgInfo** object is ```markdown ICGVerifyModelsIcgVerificationICGVerifyOrgInfo ```
  
The class name for the **TypeOfBankAcct** object is ```markdown TypeOfBankAcctEnum ```

#### Explorer 


|Names|Description|
|-----|-----------|
|BankAccount(required)|[ICGVerifyModelsIcgVerificationICGVerifyBankAccount](https://developers.icheckdev.com/Verify/#/java/models/structures/icg-verify-models-icg-verification-icg-verify-bank-account)
|UpdateMerchant|Boolean Enable or disable for updating merchant|
|RuleNum|String Rule number-assigned by MicroBilt|
|GatewayLive|Boolean Enable or disable the live|


 
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

The response of this ICG legacy verification process provides the information to the user to understand whether the process is successful or not. The **ResponseType** object contains the following parameters:   
  1. **Code:** It will be of _string_ type. This code is the identification key for each type of response, this API call returns.
  2. **decision:** It will be of _string_ type. This parameter specifies the status of the response whether it is accepted response, declined etc as mentioned in the above table of responses. 
  4. **description:** It will be of _string_ type which will acknowledge user about the API response in form of text information. 
  5. **addendaRecords:** It will be an _object_ that further contains the key, value, description fields of string type. This object basically used for providing additional information to the consumers.
  6. **error:** It will be of _string_ type that specifies the error if that occur during the API call. 
  
  The class name of the **ResponseType** object is 
 ```markdown 
  ICGVerifyModelsICGVerifyResponse 
  ```
  
 ##### 'ResponseType' object Parameters
 
![18](https://user-images.githubusercontent.com/110983629/187042084-eec78002-ba36-491a-87b3-aaee9bbd108b.png)



 
      
  
# For .NET
  
## Getting Started
  
### Description
For developers and users alike, the iCheckGateway verify API in.NET streamlines the process of integrating other web programmes that might serve as a back office solution. It places a strong focus on processing credit card payments and ACH checks. Your company will become more productive while offering the merchants and the intended audience the efficient and effective services by implementing it into your payment-configured platforms. Customers will be able to pay via eCheck, ACH transfer, or credit/debit card in a more secure method thanks to the integration of these APIs. All the information needed to use the ICG Verify Service and conduct ACH Verification is included in the ICG Verify API endpoints.
  
#### Building
  
This API requires you to install 
  
  ```markdown Newtonsoft Json.NET NuGet ``` 
  
package. If you have enabled the **automatic NuGet package restore** then all the dependencies will get installed automatically. Therefore, you will need internet access for build.

**Steps to Proceed:**
  
1. Open the solution (ICGAPIVerify.sln) file
2. Invoke the build process using 
  
  ```markdown Ctrl + Shift + B ``` 
  
  shortcut key or using the Build menu.
  
3. The build process generates a portable class library, which can be used like a normal class library. The generated library is compatible with 
  
     I) Windows Forms
    II) Windows RT
    III) Windows Phone 8
    IV) Silverlight 5 
     V) Xamarin iOS 
    VI) Xamarin Android and Mono
  
More information on how to use can be found at the **MSDN Portable Class Libraries documentation**.  
  
  
The API uses the following base URL:

> https://verify.icheckdev.com 

#### Authorization 
This API uses the following header parameters for authentication.
|Header       | Default   |Description|
|-------------|-----------|-----------|
|Authorization| None      | API Access token provided by the Auth API after User authentication| 

The request looks like this:
```markdown
curl https://verify.icheckdev.com \
  -H 'Authorization: {AUTHORIZATION}'
 ```
 
 ```markdown
 GET / HTTP/1.1
Host: {HOST}
Authorization: {AUTHORIZATION}
```

## API Endpoints
## ICG Verify
### ICG Verify Process
#### Description
ICG Verify Process is the process where we validate a pair of information containing both routingNumber that must be of 9-digits and accountNumber that must be of 14 digits for the same bank that is being validated. After the account has been created,  you will need to verify the information by making a **POST /IcgVerify/Process** request
#### POST-JSON
```markdown
curl -X POST \
  --url 'https://verify.icheckdev.com/IcgVerify/Process' \
  -H 'Authorization: Authorization'\
  -H 'Accept: application/json'\
  -H 'Content-Type: application/json' \
  --data-raw '{
  "bankAccount": {
    "routingNumber": "routingNumber0",
    "accountNumber": "accountNumber4"
  }
}`
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

#### Verify process configuration
![image](https://user-images.githubusercontent.com/110983629/185741727-7d22226f-cc5f-4649-a0c6-e28c24ec9858.png)


Above are listed all the possible codes returned from the process

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


This endpoint requires [authentication](https://developers.icheckdev.com/Verify/#/http/getting-started/how-to-get-started/authorization).
```markdown
POST /IcgVerify/Process
```
#### Parameters details
Listed below is a list of all the parameters that the end point can receive. We have request object here that collects **bankAccount*** information as the parameter. bankAccount requires **routingNumber** and **accountNumber** as necessary fields that must be filled during the verification process. Whereas, two fields act as optional fields that are not necessary to be filled during the verification process; one is **orgInfo(organization information)** and other one is **typeofBankAcct (Type of bank account)**. User can enter name in *string* format for the orgInfo and select from the displayed list options for bank account type.

##### 'request' Object Parameters
![image](https://user-images.githubusercontent.com/110983629/185380812-6612f04c-39d8-4d0d-9d9b-63ed3eee0c69.png)
##### 'bankAccount' Object Parameters
![image](https://user-images.githubusercontent.com/110983629/185381223-722ea2c6-fe07-4fcf-821a-b0d83ec477e9.png)


#### Explorer 

|Names|Description|
|-----|-----------|
|bankAccount(required)|[ICG Verify Models Icg Verification ICG Verify Bank Account](https://developers.icheckdev.com/Verify/#/http/models/structures/icg-verify-models-icg-verification-icg-verify-bank-account)
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

The response of the ICG verification process is 200, OK. It will contain a **Type** object that have the following parameters:
  1. **Code:** It will be of _string_ type. This code is the identification key for each type of response, this API call returns.
  2. **decision:** It will be of _string_ type. This parameter specifies the status of the response whether it is accepted response, declined etc as mentioned in the above table of responses. 
  4. **description:** It will be of _string_ type which will acknowledge user about the API response in form of text information. 
  5. **addendaRecords:** It will be an _object_ that further contains the key, value, description fields of string type. This object basically used for providing additional information to the consumers.
  6. **error:** It will be of _string_ type that specifies the error if that occur during the API call. 
  
 ##### 'Type' Object Parameters
 
 ![2  response of simple verify](https://user-images.githubusercontent.com/110983629/185617059-6db57703-12ca-4286-8da1-6bfa70d6b586.png)



  
  
  
  
  
  
  
  
  
  
  
  
  
# For typescript
# For PHP
# For Python
# For Ruby

  
  
  

  
