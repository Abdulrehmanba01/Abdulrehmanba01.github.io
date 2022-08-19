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
|Object|Status|Parameters|Data type|Description|
|------|------|----------|---------|-----------|
|Show complete file|Required|Show complete file|-|Show complete file for code, with bootstrap and error handling included.|
|Client configuration|Required|Authorization|String|API Access token provided by the Auth API after User authentication|



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



### ICG Verify Process Extended
#### Description
This is the extended version of the ICG Verify feature. It only can be used if the merchant provided has the permission FEATURE_ICG_VERIFY_EXTENDED assigned to the related user authenticated. This feature exploits all the microbilt options to validate an account based on many other parameters besides the Bank Route Number and Account Number.

The responses on this endpoint are same as the one listed above in the 'ICG Verify Process' section

#### POST
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
This endpoint requires [authentication](https://developers.icheckdev.com/Verify/#/http/getting-started/how-to-get-started/authorization)
```markdown
POST /IcgVerify/ProcessExt
```
#### Parameters details
The following list describes the parameters that user must have to define for getting verified through the ICG extended process. Many of them are not required depends upon the importance of the parameter. For example, the **bankAccount** object is required to add in order to get verified sccuessfully. Lets have a look on the following image for getting informations about all the parameters i.e. objects and single attributes of this API call.    

![API-extended-1](https://user-images.githubusercontent.com/110983629/185582289-e785b0b8-07c6-469b-8509-fba38bd1182c.png)

1. The required **bankAccount** is the object that contains the organziation info object which further consists of the name of the employeer. The employeer name is os string type. The other parameter are routingNumber (9-digit string), accountNumber (String), typeOfBankAcct object (having Checking, Savings, Personal Loan in String type)
2. The personal Info object consists of the following objects further:
    1. personName (It has consumer's first name and last name of string type)
    2. contactInfo (It has phoneNumber object (phoneType, 10-digit phone number), emailAddress (string type), postAddr (addr1 (String type), city (String type), stateProv (String type), postalCode(String type)))
3. tinInfo is the object that contains the tinType (integer type of >= 0 and <=8), taxId which is a text identification number of string type.
4. diverseLicense is the object that contains licenseNum, stateProv parameters (both of string type) where the licenseNum is the driver's license number and stateProv is the state of issuence which is 2-digit state code. 
5. employmentHistory is the object that contains the organziation info object which further contains the employeer name (of string type)
   





## ICG Verify Legacy
### ICG Verify Legacy Process
#### Description
Validates the check based on the routing and account numbers provided.

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
#### Response Type

# For Java
## How to get started
## API Endpoints
### ICG Verify

### ICG Verify Legacy

#### Description
#### 
# For .NET
# For typescript
# For PHP
# For Python
# For Ruby
