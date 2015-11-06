# Login and Pay with Amazon CSHARP SDK
Login and Pay with Amazon API Integration

## Requirements

* Login and Pay With Amazon account - [Register here](https://payments.amazon.com/signup)
* .NET 2.0 or higher
* Newtonsoft.json (JSON.NET)

## Documentation

* The Integration steps can be found [here](https://payments.amazon.com/documentation)

## Sample

* View the sample integration demo [here](https://amzn.github.io/login-and-pay-with-amazon-sdk-samples/)

## Quick Start

Instantiating the client:
Client takes in parameters in the following format

1. Configuration class object
2. Path to the JSON file containing configuration information.

## Installing using nuget
```
```

## Directory Structure
```
Folder PATH listing
+---Helpdocs
|       Pay With Amazon Documentation.chm
|       
+---lib
|       config.json
|       Json.txt
|       Newtonsoft.Json.dll
|       nunit.framework.dll
|       PayWithAmazon.dll
|       TestResult.xml
|       UnitTests.dll
|                     
+---PayWithAmazon
|   |   Client.cs
|   |   Constants.cs
|   |   HttpImpl.cs
|   |   IpnHandler.cs
|   |   NestedJsonToDictionary.cs
|   |   PayWithAmazon.csproj
|   |   region.Designer.cs
|   |   Regions.cs
|   |   ResponseParser.cs
|   |   Signature.cs     
|   +---ProviderCreditRequests
|   |       GetProviderCreditDetailsRequest.cs
|   |       GetProviderCreditReversalDetailsRequest.cs
|   |       ReverseProviderCreditRequest.cs
|   |       
|   +---RecurringPaymentRequests
|   |       AuthorizeOnBillingAgreementRequest.cs
|   |       CloseBillingAgreementRequest.cs
|   |       ConfirmBillingAgreementRequest.cs
|   |       CreateOrderReferenceForIdRequest.cs
|   |       GetBillingAgreementDetailsRequest.cs
|   |       SetBillingAgreementDetailsRequest.cs
|   |       ValidateBillingAgreementRequest.cs
|   |       
|   +---Responses
|   |       AuthorizeResponse.cs
|   |       BillingAddressDetails.cs
|   |       BillingAgreementDetailsResponse.cs
|   |       CancelOrderReferenceResponse.cs
|   |       CaptureResponse.cs
|   |       CloseAuthorizationResponse.cs
|   |       CloseBillingAgreementResponse.cs
|   |       CloseOrderReferenceResponse.cs
|   |       ConfirmBillingAgreementResponse.cs
|   |       ConfirmOrderReferenceResponse.cs
|   |       ErrorResponse.cs
|   |       GetProviderCreditDetailsResponse.cs
|   |       GetProviderCreditReversalDetailsResponse.cs
|   |       GetServiceStatusResponse.cs
|   |       OrderReferenceDetailsResponse.cs
|   |       RefundResponse.cs
|   |       ValidateBillingAgreementResponse.cs
|   |       
|   \---StandardPaymentRequests
|           AuthorizeRequest.cs
|           CancelOrderReferenceRequest.cs
|           CaptureRequest.cs
|           ChargeRequest.cs
|           CloseAuthorizationRequest.cs
|           CloseOrderReferenceRequest.cs
|           ConfirmOrderReferenceRequest.cs
|           GetAuthorizationDetailsRequest.cs
|           GetCaptureDetailsRequest.cs
|           GetOrderReferenceDetailsRequest.cs
|           GetRefundDetailsRequest.cs
|           RefundRequest.cs
|           SetOrderReferenceDetailsRequest.cs
|           
+---snk
|       PayWithAmazonPublic.snk
|                 
\---UnitTests
    |   config.json
    |   Json.txt
    |   packages.config
    |   PayWithAmazonTest.cs
    |   UnitTests.csproj
```

##Parameters List


####Mandatory Parameters
| Parameter    | Json file Key name | Values          								|
|--------------|--------------------|-----------------------------------------------|
| Merchant Id  | `merchant_id` 		| Default : `null`								|
| Access Key   | `access_key`  		| Default : `null`								|
| Secret Key   | `secret_key`  		| Default : `null`								|
| Region       | `region`      		| Default : `null`<br>Other: `us`,`de`,`uk`,`jp`|

####Optional Parameters
| Parameter           		| Json file Key name         	| Values                                      	   	|
|---------------------------|-------------------------------|---------------------------------------------------|
| Currency Code       		| `currency_code`       	   	| Default : `null`<br>Other: `USD`,`EUR`,`GBP`,`JPY`|
| Environment         		| `sandbox`             		| Default : `false`<br>Other: `true`	    		|
| Platform ID         		| `platform_id`         		| Default : `null` 			    				   	|
| CA Bundle File      		| `cabundle_file`       		| Default : `null`			    				   	|
| Application Name    		| `application_name`    		| Default : `null`			    				   	|
| Application Version 		| `application_version` 		| Default : `null`			    				   	|
| Proxy Host          		| `proxy_host`          		| Default : `null`			    				   	|
| Proxy Port          		| `proxy_port`          		| Default : `-1`  			    				   	|
| Proxy Username      		| `proxy_username`      		| Default : `null`			    				   	|
| Proxy Password      		| `proxy_password`      		| Default : `null`			    				   	|
| LWA Client ID       		| `client_id`           		| Default : `null`			    				   	|
| Auto Retry On Throttle   	| `auto_retry_on_throttle`    	| Default : `true`<br>Other: `false`	    		|

## Setting Configuration

Setting configuration while instantiating the Client object
```csharp
using PayWithAmazon;
using PayWithAmazon.CommonRequests;

// Your Login and Pay with Amazon keys are available in your Seller Central account

// Configuration class object
Configuration config = new Configuration();
clientConfig.WithAccessKey("YOUR_ACCESS_KEY")
	.WithMerchantId("YOUR_MERCHANT_ID")
	.WithSecretKey("YOUR_SECRET_KEY")
	
	/* Supported regions are mentioned in the Regions class and accessed by the enum supportedRegions. 
	 * Example for 'us' is shown below
	 /
	.WithRegion(Regions.supportedRegions.us);

// Or you can also provide a JSON file path which has the above configuration information in JSON format
string config = "PATH_TO_JSON_FILE\filename.fileextension";

// Instantiate the client class with the config type
Client client = new Client(config);
```
Setting configuration while instantiating the Client object with Json file
* follow the key values mentioned in the table above
* keys are not case sensitive, Ex `merchant_id` can also be named as `Merchant_ID`
* The full path with the file name that has correct readbale permissions should be provided to the client class constructor

```csharp
using PayWithAmazon;
using PayWithAmazon.CommonRequests;

// Your Login and Pay with Amazon keys are available in your Seller Central account
// Sample Json file input
{
	// Required parameters
	"merchant_id": "YOUR_MERCHANT_ID",
	"access_key": "YOUR_ACCESS_KEY",
	"secret_key": "YOUR_SECRET_KEY",
	"region": "REGION",
   
	// Optional parameters
	"currency_code": "CURRENCY_CODE",
	"client_id": "amzn.oa2.client.xxx",
	"sandbox": true,
	"application_name": "sdk testing",
	"application_version": "1.0",
	"proxy_host": null,
	"proxy_port": -1,
	"proxy_username": null,
	"proxy_password": null
	"auto_retry_on_throttle": true
}

string config = "PATH_TO_JSON_FILE\filename.fileextension";

// Instantiate the client class with the Json file path
Client client = new Client(config);
```

### Testing in Sandbox Mode

The sandbox parameter is defaults to false if not specified:
```csharp
using PayWithAmazon;
using PayWithAmazon.CommonRequests;

Configuration config = new Configuration();
clientConfig.WithAccessKey("YOUR_ACCESS_KEY")
	.WithMerchantId("YOUR_MERCHANT_ID")
	.WithSecretKey("YOUR_SECRET_KEY")
	.WithRegion(Regions.supportedRegions.us)
	.WithSandbox(true);

Client client = new Client(config);
```

### Making an API Call

Below is an example on how to make the GetOrderReferenceDetails API call:

```csharp
using PayWithAmazon;
using PayWithAmazon.CommonRequests;
using Newtonsoft.json;
using PayWithAmazon.StandardPaymentRequests;

// STEP 1 : Create the object of the GetOrderReferenceDetailsRequest class to add the parameters for the API call
GetOrderReferenceDetailsRequest requestParameters = new GetOrderReferenceDetailsRequest();

// AMAZON_ORDER_REFERENCE_ID is obtained from the Pay with Amazon Address/Wallet widgets
// ACCESS_TOKEN is obtained from the GET parameter from the URL.

// Required Parameter
requestParameters.WithAmazonOrderReferenceId("AMAZON_ORDER_REFERENCE_ID");

// Optional Parameters
requestParameters.WithAddressConsentToken("ACCESS_TOKEN");
requestParameters.WithMWSAuthToken("MWS_AUTH_TOKEN");

// STEP 2 : Making the API call by passing in the GetOrderReferenceDetailsRequest object i.e requestParameters from step 1.
// response here is the object of the GetOrderReferenceDetailsResponse class
OrderReferenceDetailsResponse response = client.GetOrderReferenceDetails(requestParameters);

// Getting response variables
// Variable values can be obtained directly from the GetOrderReferenceDetailsResponse object received from making the API call in step 2

// Check if the API call was successful
bool isGetOrderReferenceDetailsSuccess = response.GetSuccess(); 
	if(isGetOrderReferenceDetailsSuccess)
	{
		string amazonOrderReferenceId = response.GetAmazonOrderReferenceId();
		if(hasConstraint)
		{
			List<string> constraintIdList = response.GetConstraintIdList();
			List<string> constraintDescriptionList = response.GetDescriptionList();
		}
	}
	else
	{
		string errorCode = response.GetErrorCode();
		string ErrorMessage = response.GetErrorMessage();
	}
```
See the [GetOrderReferenceDetailsResponse](https://github.com/amzn/login-and-pay-with-amazon-sdk-csharp#api-response) section for all the parameters returned.

* Similarly other API calls can be made. 
sections for Request classes for the required API calls.
	* [Standard Payments Requests](https://github.com/amzn/login-and-pay-with-amazon-sdk-csharp/tree/DoDo/PayWithAmazon/StandardPaymentRequests)
	* [Recurring Payments Requests](https://github.com/amzn/login-and-pay-with-amazon-sdk-csharp/tree/DoDo/PayWithAmazon/RecurringPaymentRequests)
	* [Provider Credit Requests](https://github.com/amzn/login-and-pay-with-amazon-sdk-csharp/tree/DoDo/PayWithAmazon/ProviderCreditRequests)
	* [Common Requests](https://github.com/amzn/login-and-pay-with-amazon-sdk-csharp/tree/DoDo/PayWithAmazon/CommonRequests) - This folder contains Configuration class and GerServiceStatus API call.
* Pass the created Request object to the respective API function in the class [Client.cs](https://github.com/amzn/login-and-pay-with-amazon-sdk-csharp/blob/DoDo/PayWithAmazon/Client.cs)
* The Response object returned will be specefic to the API call made See . See API call functions in [Client.cs](https://github.com/amzn/login-and-pay-with-amazon-sdk-csharp/blob/DoDo/PayWithAmazon/Client.cs) to see the return type.
Also [Response](https://github.com/amzn/login-and-pay-with-amazon-sdk-csharp/tree/DoDo/PayWithAmazon/Responses) section for Response classes.

### Setting the Currency Code parameter
For API calls that need the currency code parameter, there are two ways to set it

1. Setting it in the configuration class object globally
```csharp
using PayWithAmazon;
using PayWithAmazon.CommonRequests;
using Newtonsoft.json;
using PayWithAmazon.StandardPaymentRequests;

Configuration config = new Configuration();
clientConfig.WithAccessKey("YOUR_ACCESS_KEY")
	.WithMerchantId("YOUR_MERCHANT_ID")
	.WithSecretKey("YOUR_SECRET_KEY")
	.WithRegion(Regions.supportedRegions.us)
	.WithSandbox(true)
	.WithCurrencyCode(Regions.currencyCode.USD);

Client client = new Client(config);
```

2. Setting it while making the API call
This takes priority over setting it globally. If this is not set via the following way the global value is taken.
```csharp
using PayWithAmazon;
using PayWithAmazon.CommonRequests;
using Newtonsoft.json;
using PayWithAmazon.StandardPaymentRequests;

Configuration config = new Configuration();
clientConfig.WithAccessKey("YOUR_ACCESS_KEY")
	.WithMerchantId("YOUR_MERCHANT_ID")
	.WithSecretKey("YOUR_SECRET_KEY")
	.WithRegion(Regions.supportedRegions.us)
	.WithSandbox(true);

Client client = new Client(config);

// Creating the SetOrderReferenceDetailsRequest object
SetOrderReferenceDetailsRequest requestParameters = new SetOrderReferenceDetailsRequest();
requestParameters.WithCurrencyCode(Regions.currencyCode.USD);

// Making the SetOrderReferenceDetails API call 
OrderReferenceDetailsResponse setOrderReferenceDetailsResponse = client.SetOrderReferenceDetails(requestParameters);
```

### IPN Handling

1. To receive IPN's successfully you will need an valid SSL on your domain.
2. You can set up your Notification endpoints in Seller Central by accessing the Integration Settings page in the Settings tab.
3. IpnHandler.cs class handles verification of the source and the data of the IPN

In your web project you can create a file (for example ipn.aspx with a CodeBehind file ipn.aspx.cs).  Add the below code into that file and set the URL to the file (ipn.aspx) location in Merchant/Integrator URL by accessing Integration Settings page in the Settings tab.

See [IPN Documentation](https://payments.amazon.com/documentation/lpwa/201749840#201750560) for all the information on IPN and types.
```csharp
using PayWithAmazon;

// Get the IPN headers and Message body
Stream s = Request.InputStream;
StreamReader sr = new StreamReader(s);
string ipnMessage = sr.ReadToEnd();
NameValueCollection headers = Request.Headers;

// Create an object of the IpnHandler class
IpnHandler ipnObject = new IpnHandler(headers, ipnMessage);
string xml = ipn.ToXml();
string json = ipn.ToJson();
Dictionary<string,object> dictionary = ipn.ToDict();

// Getting IPN common elements
string notificationType = ipnObject.GetNotificationType();
string merchantId = ipnObject.GetSellerId();
string notificationReferenceId = ipnObject.GetNotificationReferenceId();
string releaseEnvironment = ipnObject.GetReleaseEnvironment();
```

IPN's also have the XML response for the selective API calls made
Notification types returned
* OrderReferenceNotification
* BillingAgreementNotification
* PaymentAuthorize
* PaymentCapture
* PaymentRefund
* ProviderCredit
* ProviderCreditReversal
```csharp
using PayWithAmazon;

// Getting response objects.
string notificationType = ipnObject.GetNotificationType();
// Example - In this case the Authorize notification was returned 
if (notificationType.Equals(NotificationType.PaymentAuthorize.ToString()))
{
	AuthorizeResponse authResponse = ipnObject.GetAuthorizeResponse();
}
// With the authResponse object you can get the required variable values
// Example - see AuthorizeResponse class for all variables and their Getter functions. 
string amazonAuthorizationId = authResponse.GetAmazonAuthorizationId();
```

### Convenience Methods

#####Charge Method

The charge method combines the following API calls:

**Standard Payments / Recurring Payments**

1. SetOrderReferenceDetails / SetBillingAgreementDetails
2. ConfirmOrderReference / ConfirmBillingAgreement
3. Authorize / AuthorizeOnBillingAgreement

For **Standard payments** the first `charge` call will make the SetOrderReferenceDetails, ConfirmOrderReference, Authorize API calls.
Subsequent call to `charge` method for the same Order Reference ID will make the call only to Authorize.

For **Recurring payments** the first `charge` call will make the SetBillingAgreementDetails, ConfirmBillingAgreement, AuthorizeOnBillingAgreement API calls.
Subsequent call to `charge` method for the same Billing Agreement ID will make the call only to AuthorizeOnBillingAgreement.

> **Capture Now** can be set to `true` for digital goods . For Physical goods it's highly recommended to set the Capture Now to `false`
and the amount captured by making the `capture` API call after the shipment is complete.


| Parameter                  | Mandatory | Values                                                                                              	     |
|----------------------------|-----------|-----------------------------------------------------------------------------------------------------------|
| Amazon Reference ID 	     | yes       | OrderReference ID (`starts with P01 or S01`) or <br>Billing Agreement ID (`starts with B01 or C01`)       |
| Merchant ID         	     | no        | Value taken from configuration in the Client class.                                                       |
| Charge Amount       	     | yes       | Amount that needs to be captured        																	 |
| Currency code       	     | no        | If no value is provided, value is taken from the configuration of the Client class  		             	 |
| Authorization Reference ID | yes       | Unique string to be passed									                                             |
| Transaction Timeout 	     | no        | Timeout for Authorization - Defaults to 1440 minutes						                                 |
| Capture Now	             | no        | Will capture the payment automatically when set to `true`. Defaults to `false`						     |
| Charge Note         	     | no        | Note that is sent to the buyer. <br>Maps to API call variables `seller_note` , `seller_authorization_note`|
| Charge Order ID     	     | no        | Custom order ID provided <br>Maps to API call variables `seller_order_id` , `seller_billing_agreement_id` |
| Store Name          	     | no        | Name of the store                                                                                         |
| Platform ID         	     | no        | Merchant ID of the Solution Provider                                                                      |
| Custom Information  	     | no        | Any custom string                                                                                         |
| Inherit Shipping Address   | no        | Specifies whether to inherit the shipping address details, Default: true                                  |
| Soft Descriptor  			 | no        | The description to be shown on the buyer's payment instrument statement, Default: AMZ*                    |
| Provider Credit Details  	 | no        | Marketplace information                                                                                   |
| MWS Auth Token      	     | no        | MWS Auth Token required if API call is made on behalf of the seller                                       |

```csharp
using PayWithAmazon;
using PayWithAmazon.CommonRequests;
using Newtonsoft.json;
using PayWithAmazon.StandardPaymentRequests;
using PayWithAmazon.RecurringPaymentRequests;
try
{
	// ChargeRequest class object
	ChargeRequest requestParameters = new ChargeRequest();

	// Adding the parameters values to the ChargeRequest class
	requestParameters.WithAmazonReferenceId("AMAZON_REFERENCE_ID")
		.WithChargeReferenceId("AUTHORIZATION_REFERENCE_ID")
		.WithAmount("100.50")
		.WithMerchantId("MERCHANT_ID")
		.WithCurrencyCode(Regions.currencyCode.USD)
		.WithPlatformId("SOLUTION_PROVIDER_MERCHANT_ID")
		.WithSoftDescriptor("AMZ*")
		.WithStoreName("cool stuff store")
		.WithMWSAuthToken("MWS_AUTH_TOKEN")
		.WithChargeNote("sample note")
		.WithChargeOrderId("1234-1234")
		.WithCaptureNow(false)
		.WithProviderCreditDetails("PROVIDER_MERCHANT_ID", "10", Regions.currencyCode.USD)
		.WithInheritShippingAddress(true)
		.WithTransactionTimeout(5)
		.WithCustomInformation("custom information");

	// Get the Authorization response from the charge method
	AuthorizeResponse response = client.Charge(requestParameters);
}
catch (InvalidDataException ex)
{
 string errorMessage = ex.Data["errorMessage"];
 string errorCode = ex.Data["errorCode"];
 string exceptionMessage = ex.Message;
}
```
#####Obtain profile information (GetUserInfo method)
1. obtains the user's profile information from Amazon using the access token returned by the Button widget.
2. An access token is granted by the authorization server when a user logs in to a site.
3. An access token is specific to a client, a user, and an access scope. A client must use an access token to retrieve customer profile data.

| Parameter           | Variable Name         | Mandatory | Values                                                                       	     		|
|---------------------|-----------------------|-----------|---------------------------------------------------------------------------------------------|
| Access Token        | `access_token`        | yes       | Retrieved as GET parameter from the URL                                      	     		|
| Region              | `region`              | yes       | Default :`null` <br>Other:`us`,`de`,`uk`,`jp`<br>Value is set in Client class Configuration |
| LWA Client ID       | `client_id`           | yes       | Default: null<br>Value should be set in the Client class Configuration                        	     	|

```csharp
using PayWithAmazon;
using PayWithAmazon.CommonRequests;

// Your Login and Pay with Amazon keys are available in your Seller Central account

// Configuration class object
Configuration config = new Configuration();
clientConfig.WithAccessToken("ACCESS_TOKEN")
	.WithClientId("YOUR_LWA_CLIENT_ID");

Client client = new Client(config);

// Get the Access Token from the URL
string access_token = "ACCESS_TOKEN";
// Calling the function getUserInfo with the access token parameter returns object
string jsonResponse = client.GetUserInfo(access_token);

//using Newtonsoft library
Jobject jsonObject = JObject.Parse(jsonResponse);

// Buyer name
string buyerName = jsonObject.GetValue("name").ToString();
// Buyer Email
string email = jsonObject.GetValue("email").ToString();
// Buyer User Id
string userId = jsonObject.GetValue("user_id").ToString();
```
