# XfloorFloorMemorySdkJs.AuthApi

All URIs are relative to *https://appfloor.in*

Method | HTTP request | Description
------------- | ------------- | -------------
[**changeEmail**](AuthApi.md#changeEmail) | **POST** /auth-service/change/email | Change email ID
[**changeMobileNumber**](AuthApi.md#changeMobileNumber) | **POST** /auth-service/change/mobile | Change Mobile number
[**changePassword**](AuthApi.md#changePassword) | **POST** /auth-service/password/change | Change Password
[**registerExternalUserIdentity**](AuthApi.md#registerExternalUserIdentity) | **POST** /memory/identity/external-user | External User Registration
[**resetPassword**](AuthApi.md#resetPassword) | **POST** /auth-service/password/reset | Reset Password
[**sendValidationCode**](AuthApi.md#sendValidationCode) | **POST** /auth-service/send/validation/code | Send Validation code
[**signInWithEmail**](AuthApi.md#signInWithEmail) | **POST** /auth-service/sign/in/with/email | Sign In with email ID
[**signInWithMobileNumber**](AuthApi.md#signInWithMobileNumber) | **POST** /auth-service/sign/in/with/mobile/number | Sign In with Mobile number
[**signUp**](AuthApi.md#signUp) | **POST** /auth-service/sign/up | Sign Up
[**validateCode**](AuthApi.md#validateCode) | **POST** /auth-service/validate/activation/code | Validation



### changeEmail

> ChangeEmail200Response changeEmail(newEmailId, activationCode)

Change email ID

Updates the email ID associated with an existing user account after validating a one-time activation code sent to the **new email address**. This operation can only be performed by a **logged-in user**. When a user initiates an email change, an activation code is sent to the newly provided email ID. The email update takes effect only after the activation code is successfully validated. If the activation code validation fails, the email ID remains unchanged.

---

### **Authentication**

This endpoint requires **Bearer Token authentication**.

``` Authorization: Bearer <access_token>

```

---

### **Request Body**

```json { \"user_id\": \"string\", \"new_email_id\": \"string\", \"activation_code\": \"string\", \"app_id\":\"string\" }

``` **Field Description**
* `user_id` – Unique identifier of the logged-in user
* `new_email_id` – New email address to be associated with the account * `activation_code` – One-time activation code sent to the new email ID for verification

---

### **Flow Summary**
1. User is authenticated and logged in
2. User requests to change email ID 3. System sends an activation code to the **new email address**
4. User submits the activation code via this API
5. On successful validation, the email ID is updated

---

### **Successful Response**

On successful validation:
* The activation code is verified
* The user’s email ID is updated immediately * A `success` string is returned confirming the email change

---

### **Error Response**

 The API returns an error response if:
* The activation code is invalid or expired
* The activation code does not match the user or email * The new email ID is already in use * Authorization fails or the bearer token is missing or invalid In all error cases, the existing email ID remains unchanged.

---

### **Behavior

Notes**
* Requires a prior call to `/auth-service/send/validation/code` with the proper mode.

---

### **Security

Notes (Recommended)**
* Activation codes are single-use and time-bound
* Email changes require prior authentication * Rate limiting may be applied to prevent abuse

---

### **One-Line Summary**

> Changes a user’s email ID after validating an activation code sent to the new email address.

### Example

```javascript
import XfloorFloorMemorySdkJs from '@xfloor/floor-memory-sdk-js';
let defaultClient = XfloorFloorMemorySdkJs.ApiClient.instance;
// Configure Bearer access token for authorization: bearer
let bearer = defaultClient.authentications['bearer'];
bearer.accessToken = "YOUR ACCESS TOKEN"

let apiInstance = new XfloorFloorMemorySdkJs.AuthApi();
let newEmailId = "newEmailId_example"; // String | New Email ID
let activationCode = "activationCode_example"; // String | Validation code
apiInstance.changeEmail(newEmailId, activationCode, (error, data, response) => {
  if (error) {
    console.error(error);
  } else {
    console.log('API called successfully. Returned data: ' + data);
  }
});
```

### Parameters


Name

| Type | Description |

Notes
-------------

| ------------- | ------------- |

-------------
 **newEmailId**

| **String**| New Email ID |
 **activationCode**

| **String**| Validation code |

### Return type

[**ChangeEmail200Response**](ChangeEmail200Response.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

- **Content-Type**: multipart/form-data
- **Accept**: application/json


### changeMobileNumber

> ChangeEmail200Response changeMobileNumber(newMobileNumber, activationCode)

Change Mobile number

Updates the mobile number associated with an existing user account after validating a one-time activation code sent to the **new mobile number**. This operation can only be performed by a **logged-in user**. When a user initiates a mobile number change, an activation code is sent to the newly provided mobile number. The mobile number update takes effect only after the activation code is successfully validated. If the activation code validation fails, the mobile number remains unchanged.

---

### **Authentication**

This endpoint requires **Bearer Token authentication**.

``` Authorization: Bearer <access_token>

```

---

### **Request Body**

```json { \"user_id\": \"string\", \"new_mobile_number\": \"string\", \"activation_code\": \"string\" }

``` **Field Description**
* `user_id` – Unique identifier of the logged-in user
* `new_mobile_number` – New mobile number to be associated with the account * `activation_code` – One-time activation code sent to the new mobile number for verification

---

### **Flow Summary**
1. User is authenticated and logged in
2. User requests to change mobile number 3. System sends an activation code to the **new mobile number**
4. User submits the activation code via this API
5. On successful validation, the mobile number is updated

---

### **Successful Response**

On successful validation:
* The activation code is verified
* The user’s mobile number is updated immediately * A `success` string is returned confirming the mobile number change

---

### **Error Response**

 The API returns an error response if:
* The activation code is invalid or expired
* The activation code does not match the user or mobile number * The new mobile number is already in use * Authorization fails or the bearer token is missing or invalid In all error cases, the existing mobile number remains unchanged.

---

### **Behavior

Notes**
* Requires a prior call to `/auth-service/send/validation/code` with the proper mode.

---

### **Security

Notes (Recommended)**
* Activation codes are single-use and time-bound
* Mobile number changes require prior authentication * Rate limiting may be applied to prevent abuse

---

### **One-Line Summary**

> Changes a user’s mobile number after validating an activation code sent to the new mobile number.

### Example

```javascript
import XfloorFloorMemorySdkJs from '@xfloor/floor-memory-sdk-js';
let defaultClient = XfloorFloorMemorySdkJs.ApiClient.instance;
// Configure Bearer access token for authorization: bearer
let bearer = defaultClient.authentications['bearer'];
bearer.accessToken = "YOUR ACCESS TOKEN"

let apiInstance = new XfloorFloorMemorySdkJs.AuthApi();
let newMobileNumber = "newMobileNumber_example"; // String | New mobile number
let activationCode = "activationCode_example"; // String | Activation code
apiInstance.changeMobileNumber(newMobileNumber, activationCode, (error, data, response) => {
  if (error) {
    console.error(error);
  } else {
    console.log('API called successfully. Returned data: ' + data);
  }
});
```

### Parameters


Name

| Type | Description |

Notes
-------------

| ------------- | ------------- |

-------------
 **newMobileNumber**

| **String**| New mobile number |
 **activationCode**

| **String**| Activation code |

### Return type

[**ChangeEmail200Response**](ChangeEmail200Response.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

- **Content-Type**: multipart/form-data
- **Accept**: application/json


### changePassword

> ChangePassword200Response changePassword(newPassword, activationCode, opts)

Change Password

1) `POST /password/change` — Change Password (Logged-in User)

Changes the password of an **authenticated user** who is currently logged in.

This endpoint is used when a user is already signed in and wants to update their password as a security or preference action. The system validates a **one-time password-change verification code** (`activation_code`) issued specifically for the change-password flow. If the code is valid and not expired, the user’s password is updated to `new_password` and takes effect immediately. If verification fails, the password remains unchanged and an error response is returned.

### Authentication ✅ **Required**:

Bearer token for the logged-in session

``` Authorization: Bearer <access_token>

```

**Request Body**

(Form Data)
* `user_id` (optional if derived from token)
* `activation_code` (required) * `new_password` (required)

### Behavior

Notes
* Typically requires a prior call to **send a verification code** for password change (mode = password change).
* `user_id` can be taken from the access token; include it only if your system requires it explicitly.

### One-Line Summary > Changes the password for a logged-in user after validating a one-time password-change code.

### Example

```javascript
import XfloorFloorMemorySdkJs from '@xfloor/floor-memory-sdk-js';
let defaultClient = XfloorFloorMemorySdkJs.ApiClient.instance;
// Configure Bearer access token for authorization: bearer
let bearer = defaultClient.authentications['bearer'];
bearer.accessToken = "YOUR ACCESS TOKEN"

let apiInstance = new XfloorFloorMemorySdkJs.AuthApi();
let newPassword = "newPassword_example"; // String | New Password
let activationCode = "activationCode_example"; // String | Validation code
let opts = {
  'userId': "userId_example" // String | User ID
};
apiInstance.changePassword(newPassword, activationCode, opts, (error, data, response) => {
  if (error) {
    console.error(error);
  } else {
    console.log('API called successfully. Returned data: ' + data);
  }
});
```

### Parameters


Name

| Type | Description |

Notes
-------------

| ------------- | ------------- |

-------------
 **newPassword**

| **String**| New Password |
 **activationCode**

| **String**| Validation code |
 **userId**

| **String**| User ID |

[optional]

### Return type

[**ChangePassword200Response**](ChangePassword200Response.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

- **Content-Type**: multipart/form-data
- **Accept**: application/json


### registerExternalUserIdentity

> ChangeEmail200Response registerExternalUserIdentity(opts)

External User Registration

This API allows a calling application to **pass externally authenticated user identity information to xfloor** after completing authentication within its own system. xfloor **does not perform authentication, credential verification, or session management** as part of this API. The calling application is fully responsible for validating the user and ensuring the correctness of the identity data provided. Upon invocation, xfloor will:
* **Create a new user profile** if no matching user exists, or
* **Update the existing user profile** if the user is already present. xfloor returns a unique `xfloor_user_id`, which serves as the **canonical user identifier** and must be used in all subsequent xfloor APIs, including floors, blocks, conversations, memory interactions, and analytics.

### Example

```javascript
import XfloorFloorMemorySdkJs from '@xfloor/floor-memory-sdk-js';
let defaultClient = XfloorFloorMemorySdkJs.ApiClient.instance;
// Configure Bearer access token for authorization: bearer
let bearer = defaultClient.authentications['bearer'];
bearer.accessToken = "YOUR ACCESS TOKEN"

let apiInstance = new XfloorFloorMemorySdkJs.AuthApi();
let opts = {
  'mobileNumber': "mobileNumber_example", // String | 
  'emailId': "emailId_example", // String | 
  'name': "name_example", // String | 
  'appId': "appId_example" // String | 
};
apiInstance.registerExternalUserIdentity(opts, (error, data, response) => {
  if (error) {
    console.error(error);
  } else {
    console.log('API called successfully. Returned data: ' + data);
  }
});
```

### Parameters


Name

| Type | Description |

Notes
-------------

| ------------- | ------------- |

-------------
 **mobileNumber**

| **String**|
|

[optional]
 **emailId**

| **String**|
|

[optional]
 **name**

| **String**|
|

[optional]
 **appId**

| **String**|
|

[optional]

### Return type

[**ChangeEmail200Response**](ChangeEmail200Response.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

- **Content-Type**: multipart/form-data
- **Accept**: application/json


### resetPassword

> ResetPassword200Response resetPassword(newPassword, activationCode, opts)

Reset Password

---

### Reset Password (Forgot Password, Not Logged In) Resets the password of a user who **cannot log in** and is using a **forgot-password** flow. This endpoint is used when the user is not authenticated and requests a password reset using a verified identity channel such as **email** or **mobile number**. The system validates a **one-time reset verification code** (`activation_code`) issued for the reset-password flow. If valid and not expired, the password is updated to `new_password` and takes effect immediately. If verification fails, the password remains unchanged and an error response is returned.

### Authentication ✅ **Recommended** (better security): a short-lived **reset token** issued after initiating reset

``` Authorization: Bearer <reset_token>

``` > If you don’t use a reset token, you must enforce strong rate limiting + OTP attempt throttling on this endpoint.

**Request Body**

(Form Data)
* `email_id` or `mobile_number` (required to identify user)
* `activation_code` (required) * `new_password` (required) * `user_id` (optional, if your reset flow already resolved it)

### Behavior Notes
* Requires a prior call to **initiate reset** and send OTP/code (mode = forgot password).
* Must enforce code attempt limits and expiration strictly.

### One-Line Summary > Resets a user’s password (forgot-password flow) after validating a one-time reset code sent to email or mobile.

### Example

```javascript
import XfloorFloorMemorySdkJs from '@xfloor/floor-memory-sdk-js';

let apiInstance = new XfloorFloorMemorySdkJs.AuthApi();
let newPassword = "newPassword_example"; // String | 
let activationCode = "activationCode_example"; // String | 
let opts = {
  'mobileNumber': "mobileNumber_example", // String | 
  'emailId': "emailId_example", // String | 
  'appId': "appId_example" // String | 
};
apiInstance.resetPassword(newPassword, activationCode, opts, (error, data, response) => {
  if (error) {
    console.error(error);
  } else {
    console.log('API called successfully. Returned data: ' + data);
  }
});
```

### Parameters


Name

| Type | Description |

Notes
-------------

| ------------- | ------------- |

-------------
 **newPassword**

| **String**|
|
 **activationCode**

| **String**|
|
 **mobileNumber**

| **String**|
|

[optional]
 **emailId**

| **String**|
|

[optional]
 **appId**

| **String**|
|

[optional]

### Return type

[**ResetPassword200Response**](ResetPassword200Response.md)

### Authorization

No authorization required

### HTTP request headers

- **Content-Type**: multipart/form-data
- **Accept**: application/json


### sendValidationCode

> SendValidationCode200Response sendValidationCode(mode, opts)

Send Validation code

Generates and sends a one-time validation code to the user for verification of sensitive or critical account operations. This API is used across multiple authentication and account-management flows. The validation code is delivered to the user via the appropriate channel (**email or mobile number**), based on the requested operation mode and the input provided. The generated code is **time-bound**, **single-use**, and must be validated using the corresponding verification APIs to complete the requested action.

---

### **Usage Scenarios (Mode Definition)**

| Mode | Purpose |
| ---- | ----------------------------- |
| `0` | Email or mobile number change |
| `1` | Password change |
| `2` | Delete account |
| `3` | Clear account |
| `4` | Signup Verification |
| `5` | Using OTP for Login |
| `6` | OTP for forgot password |

**Mode `4` – Signup Verification** For login verification, the validation code is sent to **either the email ID or the mobile number provided in the request**. At least **one of email or mobile number must be supplied** for this mode.

---

### **Behavior**
* Generates a secure, one-time validation code
* Sends the code to the appropriate channel:
* Email or mobile number, depending on the operation mode and input
* Associates the code with:
* User identity (or login identifier)
* Requested operation (`mode`)
* Application context (if applicable)
* Validation codes are valid for a limited duration and **cannot be reused**

---

### **Authentication**

This endpoint requires **Bearer Token authentication**, **except** where explicitly allowed (for example, login-related flows).

``` Authorization: Bearer <access_token>

```

---

### **Successful Response**

On success, the API confirms that the validation code has been generated and successfully dispatched to the user.

---

### **Error Response**

 The API returns an error response if:
* The user does not exist or is not eligible for the requested operation
* The requested mode is invalid or unsupported * Required identifiers (email or mobile number for login verification) are missing * Rate limits are exceeded * Authorization fails (where applicable)

---

### **Security

Notes (Recommended)**
* Validation codes are single-use and time-bound
* Rate limiting is enforced to prevent abuse * Repeated failures may trigger temporary blocking or additional verification

---

### **One-Line Summary**

> Sends a one-time validation code for secure account and authentication operations, including login via email or mobile number.

### Example

```javascript
import XfloorFloorMemorySdkJs from '@xfloor/floor-memory-sdk-js';
let defaultClient = XfloorFloorMemorySdkJs.ApiClient.instance;
// Configure Bearer access token for authorization: bearer
let bearer = defaultClient.authentications['bearer'];
bearer.accessToken = "YOUR ACCESS TOKEN"

let apiInstance = new XfloorFloorMemorySdkJs.AuthApi();
let mode = "mode_example"; // String | 
let opts = {
  'userId': "userId_example", // String | 
  'mobileNumber': "mobileNumber_example", // String | 
  'emailId': "emailId_example", // String | 
  'appId': "appId_example" // String | 
};
apiInstance.sendValidationCode(mode, opts, (error, data, response) => {
  if (error) {
    console.error(error);
  } else {
    console.log('API called successfully. Returned data: ' + data);
  }
});
```

### Parameters


Name

| Type | Description |

Notes
-------------

| ------------- | ------------- |

-------------
 **mode**

| **String**|
|
 **userId**

| **String**|
|

[optional]
 **mobileNumber**

| **String**|
|

[optional]
 **emailId**

| **String**|
|

[optional]
 **appId**

| **String**|
|

[optional]

### Return type

[**SendValidationCode200Response**](SendValidationCode200Response.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

- **Content-Type**: multipart/form-data
- **Accept**: application/json


### signInWithEmail

> SignInResponse signInWithEmail(emailId, passCode, loginType, opts)

Sign In with email ID

Authenticates a user using a registered email ID. The authentication mechanism is determined by the specified `mode`.
* When `login_type` is set to **`1`**, the user is authenticated using the provided **password**.
* When `login_type` is set to **`2`**, the user is authenticated using a **one-time activation code (OTP)**. For OTP-based authentication (`login_type = 2`), the client **must first invoke the Send Validation Code API** with the appropriate login mode to generate and deliver the activation code to the user.

---

### **Request Body**

| Field | Type | Required | Description |
| ------------ | ------------- | -------- | ----------------------------------------------------------------- |
| `email_id` | string | Yes | Email ID |
| `pass_code` | string | Yes | Password/Validation code depending on the login_type|
| `login_type` | string | Yes | login type 1 for password 2 for validation code|
|`app_id` | string | Yes | App ID |

**Field Description**
* `email_id` – Registered email address of the user
* `pass_code` – password or activation code (this is password if it is 1 and 2 it is validation code) * `app_id`
- App ID which is a 13 digit numeric value
* `login_type` – Login type
* `1` → Password-based login
* `2` → Activation code (OTP)–based login

---

### **Behavior

Notes**
* When `login_type = 2`, password validation is bypassed.
* OTP-based login requires a prior call to ` /auth-service/send/sign/in/validation/code`. * If the required credentials for the selected mode are missing or invalid, authentication fails.

---

### **Successful Response**

On successful authentication, the user is signed in and a success response is returned as per the authentication flow.

---

### **Error Response**

 The API returns an error response if:
* The email ID is not registered
* The password is incorrect (`login_type = 1 `) * The activation code is missing, invalid, or expired (`login_type = 2`) * The mode value is invalid or unsupported

---

### **One-Line Summary**

> Signs in a user using an email ID with either password-based or OTP-based authentication, based on the selected mode.

### Example

```javascript
import XfloorFloorMemorySdkJs from '@xfloor/floor-memory-sdk-js';
let defaultClient = XfloorFloorMemorySdkJs.ApiClient.instance;
// Configure Bearer access token for authorization: bearer
let bearer = defaultClient.authentications['bearer'];
bearer.accessToken = "YOUR ACCESS TOKEN"

let apiInstance = new XfloorFloorMemorySdkJs.AuthApi();
let emailId = "emailId_example"; // String | Email ID
let passCode = "passCode_example"; // String | Validation code or password depends on the login_type
let loginType = "loginType_example"; // String | 1 is for password, 2 is for validation code
let opts = {
  'appId': "appId_example" // String | App ID
};
apiInstance.signInWithEmail(emailId, passCode, loginType, opts, (error, data, response) => {
  if (error) {
    console.error(error);
  } else {
    console.log('API called successfully. Returned data: ' + data);
  }
});
```

### Parameters


Name

| Type | Description |

Notes
-------------

| ------------- | ------------- |

-------------
 **emailId**

| **String**| Email ID |
 **passCode**

| **String**| Validation code or password depends on the login_type |
 **loginType**

| **String**| 1 is for password, 2 is for validation code |
 **appId**

| **String**| App ID |

[optional]

### Return type

[**SignInResponse**](SignInResponse.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

- **Content-Type**: multipart/form-data
- **Accept**: application/json


### signInWithMobileNumber

> SignInResponse signInWithMobileNumber(mobileNumber, passCode, loginType, opts)

Sign In with Mobile number

Authenticates a user using a registered mobile number. The authentication method is determined by the specified `mode`.
* When `login_type` is set to **`1`**, the user is authenticated using the **password** associated with the account.
* When `login_type` is set to **`2`**, the user is authenticated using a **one-time activation code (OTP)** sent to the registered mobile number. For OTP-based authentication (`login_type = 1`), the client **must first call the Send Validation Code API** with the appropriate login mode to generate and deliver the activation code.

---

### **Request Formdata**

| Field | Type | Required | Description |
| ------------ | ------------- | -------- | ----------------------------------------------------------------- |
| `mobile_number` | string | Yes | Mobile number|
| `pass_code` | string | Yes | Password/Validation code depending on the login_type|
| `login_type` | string | Yes | login type 1 for password 2 for validation code|
|`app_id` | string | Yes | App ID |

**Field Description**
* `mobile_number` – Registered mobile number of the user
* `pass_code` – Password / Validation code (password when `login_type= 1`; validation code when `login_type = 2`) * `login_type` – Login type
* `1` → Password-based login
* `2` → Activation code (OTP)–based login

---

### **Behavior

Notes**
* When `login_type = 2`, password validation is skipped.
* OTP-based login requires a prior call to `/auth-service/send/sign/in/validation/code`. * Missing or invalid credentials for the selected mode will result in authentication failure.

---

### **Successful Response**

On successful authentication, the user is signed in and a success response is returned according to the authentication flow.

---

### **Error Response**

 The API returns an error response if:
* The mobile number is not registered
* The password is incorrect (`login_type = 1`) * The activation code is missing, invalid, or expired (`login_type = 2`) * An invalid or unsupported mode is provided

---

### **One-Line Summary**

> Signs in a user using a mobile number with either password-based or OTP-based authentication, based on the selected mode.

### Example

```javascript
import XfloorFloorMemorySdkJs from '@xfloor/floor-memory-sdk-js';
let defaultClient = XfloorFloorMemorySdkJs.ApiClient.instance;
// Configure Bearer access token for authorization: bearer
let bearer = defaultClient.authentications['bearer'];
bearer.accessToken = "YOUR ACCESS TOKEN"

let apiInstance = new XfloorFloorMemorySdkJs.AuthApi();
let mobileNumber = "mobileNumber_example"; // String | Mobile number
let passCode = "passCode_example"; // String | Pass code takes either password or validation code depending on the login_type
let loginType = "loginType_example"; // String | 1 for password, 2 for activate code
let opts = {
  'appId': "appId_example" // String | App ID
};
apiInstance.signInWithMobileNumber(mobileNumber, passCode, loginType, opts, (error, data, response) => {
  if (error) {
    console.error(error);
  } else {
    console.log('API called successfully. Returned data: ' + data);
  }
});
```

### Parameters


Name

| Type | Description |

Notes
-------------

| ------------- | ------------- |

-------------
 **mobileNumber**

| **String**| Mobile number |
 **passCode**

| **String**| Pass code takes either password or validation code depending on the login_type |
 **loginType**

| **String**| 1 for password, 2 for activate code |
 **appId**

| **String**| App ID |

[optional]

### Return type

[**SignInResponse**](SignInResponse.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

- **Content-Type**: multipart/form-data
- **Accept**: application/json


### signUp

> SignUp200Response signUp(name, password, opts)

Sign Up

Creates a new user account in the Floor POD using **either a mobile number or an email ID**. At least **one of `mobile_number` or `email_id` is required** to register a user. Both may be provided if available. The API registers the user under the specified application context and prepares the account for subsequent authentication and usage. Upon successful registration, the API returns: - a unique user_id identifying the newly created user, and - a success string indicating the outcome of the sign-up operation. The user account is created under the specified application context and can be used for subsequent interactions with Floor POD APIs.

---

### **Parameter Clarification (Recommended)**
* `name` is mandatory for user profile creation
* Either `mobile_number` **or** `email_id` must be present * `app_id` is optional and used to associate the user with a specific application

### Example

```javascript
import XfloorFloorMemorySdkJs from '@xfloor/floor-memory-sdk-js';
let defaultClient = XfloorFloorMemorySdkJs.ApiClient.instance;
// Configure Bearer access token for authorization: bearer
let bearer = defaultClient.authentications['bearer'];
bearer.accessToken = "YOUR ACCESS TOKEN"

let apiInstance = new XfloorFloorMemorySdkJs.AuthApi();
let name = "name_example"; // String | New User Name
let password = "password_example"; // String | Password
let opts = {
  'emailId': "emailId_example", // String | Email ID of the user
  'mobileNumber': "mobileNumber_example", // String | Mobile number
  'appId': "appId_example" // String | Registered App ID
};
apiInstance.signUp(name, password, opts, (error, data, response) => {
  if (error) {
    console.error(error);
  } else {
    console.log('API called successfully. Returned data: ' + data);
  }
});
```

### Parameters


Name

| Type | Description |

Notes
-------------

| ------------- | ------------- |

-------------
 **name**

| **String**| New User Name |
 **password**

| **String**| Password |
 **emailId**

| **String**| Email ID of the user |

[optional]
 **mobileNumber**

| **String**| Mobile number |

[optional]
 **appId**

| **String**| Registered App ID |

[optional]

### Return type

[**SignUp200Response**](SignUp200Response.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

- **Content-Type**: multipart/form-data
- **Accept**: application/json


### validateCode

> UserDetails validateCode(userId, activationCode, mode, opts)

Validation

### **Validate Activation / Verification Code**

This API **validates a one-time verification code** submitted by a user and **executes the corresponding account operation** based on the specified **mode**. Depending on the mode, the API may:
* Activate a newly registered account
* Confirm a login attempt * Verify a password change or reset * Validate email or mobile updates * Confirm account deletion or clearing requests The API verifies the provided `activation_code` against the given `user_id`, `mode`, and application context. If validation succeeds, the requested operation is completed and the API returns the relevant **POD information** and **user profile details** (where applicable). If validation fails, the operation is **not performed** and an appropriate error response is returned.

---

### **Authentication**

This endpoint requires **Bearer Token authentication**. **Header**

``` Authorization: Bearer <access_token>

```

---

### **Request Body**

```json { \"user_id\": \"string\", \"activation_code\": \"string\", \"app_id\": \"string\", \"mode\": \"string\" }

```

### **Field Descriptions**
* **user_id** – Unique identifier of the user initiating the operation
* **activation_code** – One-time verification code sent to the user * **app_id** – Application identifier (optional or context-specific) * **mode** – Operation context for which the verification is being performed

---

### **Usage Scenarios (Mode Definitions)**

| Mode | Purpose |
| ---- | ---------------------------------------- |
| 0 | Email or mobile number change |
| 1 | Password change |
| 2 | Delete account |
| 3 | Clear account |
| 4 | Signup verification (account activation) |
| 5 | Login verification |
| 6 | Forgot password verification |

---

### **Successful Response**

On successful validation:
* The requested operation (based on `mode`) is completed
* The API returns:
* **POD information** associated with the user (if applicable)
* **User profile details** (if applicable) Examples:
* For **signup verification**, the user account is activated
* For **login**, access is confirmed * For **password reset**, the user may proceed to set a new password * For **account deletion**, the request is confirmed

---

### **Error Response**

 The API returns an error response when:
* The activation code is invalid or expired
* The activation code does not match the user or operation mode * The requested operation is already completed (e.g., user already activated) * Authorization fails or the bearer token is missing or invalid ⚠️ In all error cases, **no account state change occurs**.

---

### **One-Line Summary**

> Validates a one-time verification code and securely completes the requested user account operation (signup, login, password change, or account actions), returning POD and profile details on success.

### Example

```javascript
import XfloorFloorMemorySdkJs from '@xfloor/floor-memory-sdk-js';
let defaultClient = XfloorFloorMemorySdkJs.ApiClient.instance;
// Configure Bearer access token for authorization: bearer
let bearer = defaultClient.authentications['bearer'];
bearer.accessToken = "YOUR ACCESS TOKEN"

let apiInstance = new XfloorFloorMemorySdkJs.AuthApi();
let userId = "userId_example"; // String | 
let activationCode = "activationCode_example"; // String | 
let mode = "mode_example"; // String | 
let opts = {
  'appId': "appId_example" // String | 
};
apiInstance.validateCode(userId, activationCode, mode, opts, (error, data, response) => {
  if (error) {
    console.error(error);
  } else {
    console.log('API called successfully. Returned data: ' + data);
  }
});
```

### Parameters


Name

| Type | Description |

Notes
-------------

| ------------- | ------------- |

-------------
 **userId**

| **String**|
|
 **activationCode**

| **String**|
|
 **mode**

| **String**|
|
 **appId**

| **String**|
|

[optional]

### Return type

[**UserDetails**](UserDetails.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

- **Content-Type**: multipart/form-data
- **Accept**: application/json

