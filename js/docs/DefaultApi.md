# XfloorFloorMemorySdkJs.DefaultApi

All URIs are relative to *https://appfloor.in*

Method | HTTP request | Description
------------- | ------------- | -------------
[**changeEmail**](DefaultApi.md#changeEmail) | **POST** /auth-service/change/email | Change email ID
[**changeMobileNumber**](DefaultApi.md#changeMobileNumber) | **POST** /auth-service/change/mobile | Change Mobile number
[**changePassword**](DefaultApi.md#changePassword) | **POST** /auth-service/password/change | Change Password
[**makeFloorPrivate**](DefaultApi.md#makeFloorPrivate) | **POST** /api/memory/make/floor/private | Make floor Private
[**makeFloorPublic**](DefaultApi.md#makeFloorPublic) | **POST** /api/memory/make/floor/public | Make floor public
[**registerExternalUserIdentity**](DefaultApi.md#registerExternalUserIdentity) | **POST** /memory/identity/external-user | External User Registration
[**renameFloor**](DefaultApi.md#renameFloor) | **POST** /api/memory/change/floor/id | Rename floor
[**resetPassword**](DefaultApi.md#resetPassword) | **POST** /auth-service/password/reset | Reset Password
[**sendValidationCode**](DefaultApi.md#sendValidationCode) | **POST** /auth-service/send/validation/code | Send Validation code
[**signInWithEmail**](DefaultApi.md#signInWithEmail) | **POST** /auth-service/sign/in/with/email | Sign In with email ID
[**signInWithMobileNumber**](DefaultApi.md#signInWithMobileNumber) | **POST** /auth-service/sign/in/with/mobile/number | Sign In with Mobile number
[**signUp**](DefaultApi.md#signUp) | **POST** /auth-service/sign/up | Sign Up
[**validateCode**](DefaultApi.md#validateCode) | **POST** /auth-service/validate/activation/code | Validation



## changeEmail

> Object changeEmail(newEmailId, activationCode)

Change email ID

Updates the email ID associated with an existing user account after validating a one-time activation code sent to the **new email address**.  This operation can only be performed by a **logged-in user**. When a user initiates an email change, an activation code is sent to the newly provided email ID. The email update takes effect only after the activation code is successfully validated.  If the activation code validation fails, the email ID remains unchanged.  ---  ### **Authentication**  This endpoint requires **Bearer Token authentication**.  &#x60;&#x60;&#x60; Authorization: Bearer &lt;access_token&gt; &#x60;&#x60;&#x60;  ---  ### **Request Body**  &#x60;&#x60;&#x60;json {   \&quot;user_id\&quot;: \&quot;string\&quot;,   \&quot;new_email_id\&quot;: \&quot;string\&quot;,   \&quot;activation_code\&quot;: \&quot;string\&quot;,   \&quot;app_id\&quot;:\&quot;string\&quot; } &#x60;&#x60;&#x60;  **Field Description**  * &#x60;user_id&#x60; – Unique identifier of the logged-in user * &#x60;new_email_id&#x60; – New email address to be associated with the account * &#x60;activation_code&#x60; – One-time activation code sent to the new email ID for verification  ---  ### **Flow Summary**  1. User is authenticated and logged in 2. User requests to change email ID 3. System sends an activation code to the **new email address** 4. User submits the activation code via this API 5. On successful validation, the email ID is updated  ---  ### **Successful Response**  On successful validation:  * The activation code is verified * The user’s email ID is updated immediately * A &#x60;success&#x60; string is returned confirming the email change  ---  ### **Error Response**  The API returns an error response if:  * The activation code is invalid or expired * The activation code does not match the user or email * The new email ID is already in use * Authorization fails or the bearer token is missing or invalid  In all error cases, the existing email ID remains unchanged.  --- ### **Behavior Notes**  * Requires a prior call to &#x60;/auth-service/send/validation/code&#x60; with the proper mode.  ---  ### **Security Notes (Recommended)**  * Activation codes are single-use and time-bound * Email changes require prior authentication * Rate limiting may be applied to prevent abuse  ---  ### **One-Line Summary**  &gt; Changes a user’s email ID after validating an activation code sent to the new email address. 

### Example

```javascript
import XfloorFloorMemorySdkJs from '@xfloor/floor-memory-sdk-js';
let defaultClient = XfloorFloorMemorySdkJs.ApiClient.instance;
// Configure Bearer access token for authorization: bearer
let bearer = defaultClient.authentications['bearer'];
bearer.accessToken = "YOUR ACCESS TOKEN"

let apiInstance = new XfloorFloorMemorySdkJs.DefaultApi();
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


Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **newEmailId** | **String**| New Email ID | 
 **activationCode** | **String**| Validation code | 

### Return type

**Object**

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

- **Content-Type**: multipart/form-data
- **Accept**: application/json


## changeMobileNumber

> Object changeMobileNumber(body)

Change Mobile number

Updates the mobile number associated with an existing user account after validating a one-time activation code sent to the **new mobile number**.  This operation can only be performed by a **logged-in user**. When a user initiates a mobile number change, an activation code is sent to the newly provided mobile number. The mobile number update takes effect only after the activation code is successfully validated.  If the activation code validation fails, the mobile number remains unchanged.  ---  ### **Authentication**  This endpoint requires **Bearer Token authentication**.  &#x60;&#x60;&#x60; Authorization: Bearer &lt;access_token&gt; &#x60;&#x60;&#x60;  ---  ### **Request Body**  &#x60;&#x60;&#x60;json {   \&quot;user_id\&quot;: \&quot;string\&quot;,   \&quot;new_mobile_number\&quot;: \&quot;string\&quot;,   \&quot;activation_code\&quot;: \&quot;string\&quot; } &#x60;&#x60;&#x60;  **Field Description**  * &#x60;user_id&#x60; – Unique identifier of the logged-in user * &#x60;new_mobile_number&#x60; – New mobile number to be associated with the account * &#x60;activation_code&#x60; – One-time activation code sent to the new mobile number for verification  ---  ### **Flow Summary**  1. User is authenticated and logged in 2. User requests to change mobile number 3. System sends an activation code to the **new mobile number** 4. User submits the activation code via this API 5. On successful validation, the mobile number is updated  ---  ### **Successful Response**  On successful validation:  * The activation code is verified * The user’s mobile number is updated immediately * A &#x60;success&#x60; string is returned confirming the mobile number change  ---  ### **Error Response**  The API returns an error response if:  * The activation code is invalid or expired * The activation code does not match the user or mobile number * The new mobile number is already in use * Authorization fails or the bearer token is missing or invalid  In all error cases, the existing mobile number remains unchanged.  --- ### **Behavior Notes**  * Requires a prior call to &#x60;/auth-service/send/validation/code&#x60; with the proper mode. ---  ### **Security Notes (Recommended)**  * Activation codes are single-use and time-bound * Mobile number changes require prior authentication * Rate limiting may be applied to prevent abuse  ---  ### **One-Line Summary**  &gt; Changes a user’s mobile number after validating an activation code sent to the new mobile number.

### Example

```javascript
import XfloorFloorMemorySdkJs from '@xfloor/floor-memory-sdk-js';
let defaultClient = XfloorFloorMemorySdkJs.ApiClient.instance;
// Configure Bearer access token for authorization: bearer
let bearer = defaultClient.authentications['bearer'];
bearer.accessToken = "YOUR ACCESS TOKEN"

let apiInstance = new XfloorFloorMemorySdkJs.DefaultApi();
let body = {key: null}; // Object | 
apiInstance.changeMobileNumber(body, (error, data, response) => {
  if (error) {
    console.error(error);
  } else {
    console.log('API called successfully. Returned data: ' + data);
  }
});
```

### Parameters


Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **body** | **Object**|  | 

### Return type

**Object**

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

- **Content-Type**: application/json
- **Accept**: application/json


## changePassword

> ChangePassword200Response changePassword(newPassword, activationCode, opts)

Change Password

## 1) &#x60;POST /password/change&#x60; — Change Password (Logged-in User)  Changes the password of an **authenticated user** who is currently logged in.  This endpoint is used when a user is already signed in and wants to update their password as a security or preference action. The system validates a **one-time password-change verification code** (&#x60;activation_code&#x60;) issued specifically for the change-password flow. If the code is valid and not expired, the user’s password is updated to &#x60;new_password&#x60; and takes effect immediately.  If verification fails, the password remains unchanged and an error response is returned.  ### Authentication  ✅ **Required**: Bearer token for the logged-in session  &#x60;&#x60;&#x60; Authorization: Bearer &lt;access_token&gt; &#x60;&#x60;&#x60;  ### Request Body (Form Data)  * &#x60;user_id&#x60; (optional if derived from token) * &#x60;activation_code&#x60; (required) * &#x60;new_password&#x60; (required)  ### Behavior Notes  * Typically requires a prior call to **send a verification code** for password change (mode &#x3D; password change). * &#x60;user_id&#x60; can be taken from the access token; include it only if your system requires it explicitly.  ### One-Line Summary  &gt; Changes the password for a logged-in user after validating a one-time password-change code. 

### Example

```javascript
import XfloorFloorMemorySdkJs from '@xfloor/floor-memory-sdk-js';
let defaultClient = XfloorFloorMemorySdkJs.ApiClient.instance;
// Configure Bearer access token for authorization: bearer
let bearer = defaultClient.authentications['bearer'];
bearer.accessToken = "YOUR ACCESS TOKEN"

let apiInstance = new XfloorFloorMemorySdkJs.DefaultApi();
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


Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **newPassword** | **String**| New Password | 
 **activationCode** | **String**| Validation code | 
 **userId** | **String**| User ID | [optional] 

### Return type

[**ChangePassword200Response**](ChangePassword200Response.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

- **Content-Type**: multipart/form-data
- **Accept**: application/json


## makeFloorPrivate

> GetFloorInformation200Response makeFloorPrivate(opts)

Make floor Private

This API changes a floor’s visibility to **PRIVATE**.  It is used when a floor owner wants to **restrict access** to a floor that is currently public. After the update, the floor becomes private and is no longer accessible to non-authorized users (based on your platform’s access rules).  This endpoint is **state-changing**:  * If the floor is **PUBLIC**, it will be converted to **PRIVATE** * If the floor is already **PRIVATE**, the API returns success (idempotent) or an “already private” response depending on implementation  This API is commonly used in:  * Floor settings → “Privacy” toggle * Developer-managed pod workflows (app_id context) * Admin tools (if applicable)  ---  ## Request Method  &#x60;POST&#x60;  ---  ## Content-Type  &#x60;application/x-www-form-urlencoded&#x60; (or &#x60;multipart/form-data&#x60; if your system uses form-data) *(Document whichever you actually accept; below assumes standard form fields.)*  ---  ## Request Parameters (Form Fields)  | Field      | Type   | Required | Description                                                          | | ---------- | ------ | -------- | -------------------------------------------------------------------- | | &#x60;user_id&#x60;  | String | **Yes**  | User requesting the change. Must be the **owner** of the floor.      | | &#x60;floor_id&#x60; | String | **Yes**  | Public identifier of the floor to update.                            | | &#x60;app_id&#x60;   | String | No       | Calling application identifier (used for developer/pod integration). |  ---  ## Authorization Rules (Critical)  * The caller must be authenticated as &#x60;user_id&#x60; * **Only the floor owner** can change floor visibility * If the user is not the owner, the request must be rejected  ---  ## Behavior Rules  * Converts visibility from **PUBLIC → PRIVATE** * Does not modify floor content or blocks * Access enforcement for private floors is applied immediately after the change  **Idempotency**  * Calling this API multiple times should not cause repeated changes * If already private, the API should either:    * return success with a message like &#x60;\&quot;already private\&quot;&#x60;, or   * return a specific error/status indicating no-op  ---  ## Response Format  &#x60;application/json&#x60;  ---  ## Sample Success Response  *(Example — adjust to match your actual response format)*  &#x60;&#x60;&#x60;json {   \&quot;status\&quot;: \&quot;SUCCESS\&quot;,   \&quot;floor_id\&quot;: \&quot;my_floor\&quot;,   \&quot;visibility\&quot;: \&quot;PRIVATE\&quot;,   \&quot;message\&quot;: \&quot;Floor is now private\&quot; } &#x60;&#x60;&#x60;  ---  ## Sample No-Op Response (Already Private)  &#x60;&#x60;&#x60;json {   \&quot;status\&quot;: \&quot;SUCCESS\&quot;,   \&quot;floor_id\&quot;: \&quot;my_floor\&quot;,   \&quot;visibility\&quot;: \&quot;PRIVATE\&quot;,   \&quot;message\&quot;: \&quot;Floor is already private\&quot; } &#x60;&#x60;&#x60;  ---  ## Error Responses (Examples)  ### Not Authorized (Not Owner)  &#x60;&#x60;&#x60;json {   \&quot;status\&quot;: \&quot;ERROR\&quot;,   \&quot;message\&quot;: \&quot;Only the floor owner can change floor visibility\&quot; } &#x60;&#x60;&#x60;  ### Floor Not Found  &#x60;&#x60;&#x60;json {   \&quot;status\&quot;: \&quot;ERROR\&quot;,   \&quot;message\&quot;: \&quot;Floor not found\&quot; } &#x60;&#x60;&#x60;  ### Invalid Request  &#x60;&#x60;&#x60;json {   \&quot;status\&quot;: \&quot;ERROR\&quot;,   \&quot;message\&quot;: \&quot;user_id and floor_id are required\&quot; } &#x60;&#x60;&#x60;  ---  ## Notes  * This API is intended to control floor visibility only; membership/invite rules (for private floors) are handled elsewhere. * &#x60;app_id&#x60; is provided for developer/pod applications and is optional unless enforced by your app model. * If you support floor types like &#x60;POD&#x60;, document whether pods are allowed to be private or not (some platforms restrict this). 

### Example

```javascript
import XfloorFloorMemorySdkJs from '@xfloor/floor-memory-sdk-js';
let defaultClient = XfloorFloorMemorySdkJs.ApiClient.instance;
// Configure Bearer access token for authorization: bearer
let bearer = defaultClient.authentications['bearer'];
bearer.accessToken = "YOUR ACCESS TOKEN"

let apiInstance = new XfloorFloorMemorySdkJs.DefaultApi();
let opts = {
  'floorId': "floorId_example", // String | Floor ID
  'userId': "userId_example", // String | User ID
  'appId': "appId_example" // String | App ID
};
apiInstance.makeFloorPrivate(opts, (error, data, response) => {
  if (error) {
    console.error(error);
  } else {
    console.log('API called successfully. Returned data: ' + data);
  }
});
```

### Parameters


Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **floorId** | **String**| Floor ID | [optional] 
 **userId** | **String**| User ID | [optional] 
 **appId** | **String**| App ID | [optional] 

### Return type

[**GetFloorInformation200Response**](GetFloorInformation200Response.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: application/json


## makeFloorPublic

> GetFloorInformation200Response makeFloorPublic(opts)

Make floor public

This API changes a floor’s visibility to **PUBLIC**.  It is used when a floor owner wants to **make a private floor accessible to everyone**. After the update, the floor becomes public and can be viewed and discovered by any user, subject to platform rules (search, feeds, pods, etc.).  This endpoint performs a **visibility state transition**:  * **PRIVATE → PUBLIC** * If the floor is already public, the operation is treated as **idempotent** (no state change).  This API is typically used from:  * Floor settings → Privacy / Visibility controls * Owner or admin tools * Developer or pod-based applications using &#x60;app_id&#x60;  ---  ## Request Method  &#x60;POST&#x60;  ---  ## Content-Type  &#x60;application/x-www-form-urlencoded&#x60; (or &#x60;multipart/form-data&#x60;, depending on your implementation)  ---  ## Request Parameters (Form Fields)  | Field      | Type   | Required | Description                                                                     | | ---------- | ------ | -------- | ------------------------------------------------------------------------------- | | &#x60;user_id&#x60;  | String | **Yes**  | User requesting the change. Must be the **owner** of the floor.                 | | &#x60;floor_id&#x60; | String | **Yes**  | Public identifier of the floor whose visibility is to be changed.               | | &#x60;app_id&#x60;   | String | No       | Identifier of the calling application (used mainly for pod/developer contexts). |  ---  ## Authorization Rules (Critical)  * The caller must be authenticated as &#x60;user_id&#x60; * **Only the floor owner** is allowed to change the floor’s visibility * Requests from non-owners must be rejected  ---  ## Behavior Rules  * Converts floor visibility from **PRIVATE → PUBLIC** * Does not modify floor content, blocks, or ownership * Visibility change takes effect immediately  ### Idempotency  * If the floor is already public, the API should:    * Return success with a message indicating no change, or   * Return a specific “already public” status (implementation-dependent)  ---  ## Response Format  &#x60;application/json&#x60;  ---  ## Sample Success Response  &#x60;&#x60;&#x60;json {   \&quot;status\&quot;: \&quot;SUCCESS\&quot;,   \&quot;floor_id\&quot;: \&quot;my_floor\&quot;,   \&quot;visibility\&quot;: \&quot;PUBLIC\&quot;,   \&quot;message\&quot;: \&quot;Floor is now public\&quot; } &#x60;&#x60;&#x60;  ---  ## Sample No-Op Response (Already Public)  &#x60;&#x60;&#x60;json {   \&quot;status\&quot;: \&quot;SUCCESS\&quot;,   \&quot;floor_id\&quot;: \&quot;my_floor\&quot;,   \&quot;visibility\&quot;: \&quot;PUBLIC\&quot;,   \&quot;message\&quot;: \&quot;Floor is already public\&quot; } &#x60;&#x60;&#x60;  ---  ## Error Responses (Examples)  ### Not Authorized (Not Owner)  &#x60;&#x60;&#x60;json {   \&quot;status\&quot;: \&quot;ERROR\&quot;,   \&quot;message\&quot;: \&quot;Only the floor owner can change floor visibility\&quot; } &#x60;&#x60;&#x60;  ---  ### Floor Not Found  &#x60;&#x60;&#x60;json {   \&quot;status\&quot;: \&quot;ERROR\&quot;,   \&quot;message\&quot;: \&quot;Floor not found\&quot; } &#x60;&#x60;&#x60;  ---  ### Invalid Request  &#x60;&#x60;&#x60;json {   \&quot;status\&quot;: \&quot;ERROR\&quot;,   \&quot;message\&quot;: \&quot;user_id and floor_id are required\&quot; } &#x60;&#x60;&#x60;  ---  ## Notes for Developers  * This API controls **visibility only**. Membership, invitations, and moderation rules are handled by separate APIs. * &#x60;app_id&#x60; is optional and primarily used for developer-managed or pod floors. * Clients should refresh floor metadata (e.g., via &#x60;/api/floor/info&#x60;) after a successful visibility change.  ---  ### Mental Model (One Line)  &gt; **This API answers: “Make this floor visible to everyone.”** 

### Example

```javascript
import XfloorFloorMemorySdkJs from '@xfloor/floor-memory-sdk-js';
let defaultClient = XfloorFloorMemorySdkJs.ApiClient.instance;
// Configure Bearer access token for authorization: bearer
let bearer = defaultClient.authentications['bearer'];
bearer.accessToken = "YOUR ACCESS TOKEN"

let apiInstance = new XfloorFloorMemorySdkJs.DefaultApi();
let opts = {
  'floorId': "floorId_example", // String | Floor ID
  'userId': "userId_example", // String | User ID
  'appId': "appId_example" // String | App ID
};
apiInstance.makeFloorPublic(opts, (error, data, response) => {
  if (error) {
    console.error(error);
  } else {
    console.log('API called successfully. Returned data: ' + data);
  }
});
```

### Parameters


Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **floorId** | **String**| Floor ID | [optional] 
 **userId** | **String**| User ID | [optional] 
 **appId** | **String**| App ID | [optional] 

### Return type

[**GetFloorInformation200Response**](GetFloorInformation200Response.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: application/json


## registerExternalUserIdentity

> SignInWithEmail200Response registerExternalUserIdentity(opts)

External User Registration

This API allows a calling application to **pass externally authenticated user identity information to xfloor** after completing authentication within its own system.  xfloor **does not perform authentication, credential verification, or session management** as part of this API. The calling application is fully responsible for validating the user and ensuring the correctness of the identity data provided.  Upon invocation, xfloor will:  * **Create a new user profile** if no matching user exists, or * **Update the existing user profile** if the user is already present.  xfloor returns a unique &#x60;xfloor_user_id&#x60;, which serves as the **canonical user identifier** and must be used in all subsequent xfloor APIs, including floors, blocks, conversations, memory interactions, and analytics.

### Example

```javascript
import XfloorFloorMemorySdkJs from '@xfloor/floor-memory-sdk-js';
let defaultClient = XfloorFloorMemorySdkJs.ApiClient.instance;
// Configure Bearer access token for authorization: bearer
let bearer = defaultClient.authentications['bearer'];
bearer.accessToken = "YOUR ACCESS TOKEN"

let apiInstance = new XfloorFloorMemorySdkJs.DefaultApi();
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


Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **mobileNumber** | **String**|  | [optional] 
 **emailId** | **String**|  | [optional] 
 **name** | **String**|  | [optional] 
 **appId** | **String**|  | [optional] 

### Return type

[**SignInWithEmail200Response**](SignInWithEmail200Response.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

- **Content-Type**: multipart/form-data
- **Accept**: application/json


## renameFloor

> GetFloorInformation200Response renameFloor(opts)

Rename floor

This API renames a floor by changing knowing the **floor identifier (floor_id)**.  It allows the **floor owner** to update the public-facing floor ID (slug/handle) from an old value to a new value. This is typically used when the owner wants to rebrand, reorganize, or correct the floor’s identifier.  ⚠️ **This operation affects how the floor is accessed and referenced externally**, so it must be performed carefully.  ---  ## Ownership &amp; Authorization (Critical)  * The caller **must be authenticated** * **Only the floor owner** is allowed to rename a floor * Members, followers, or non-owners **cannot** perform this operation * Ownership is validated internally using &#x60;user_id&#x60;  &gt; If the user is not the owner, the request must be rejected.  ---  ## Request Method  &#x60;POST&#x60;  ---  ## Content-Type  &#x60;application/x-www-form-urlencoded&#x60; (or equivalent form-data encoding)  ---  ## Request Parameters (Form Fields)  | Parameter | Type   | Required | Description                                                                     | | --------- | ------ | -------- | ------------------------------------------------------------------------------- | | &#x60;user_id&#x60; | String | **Yes**  | User requesting the rename. Must be the **owner** of the floor.                 | | &#x60;from&#x60;    | String | **Yes**  | Existing floor ID (current identifier to be renamed).                           | | &#x60;to&#x60;      | String | **Yes**  | New floor ID to assign to the floor.                                            | | &#x60;app_id&#x60;  | String | No       | Identifier of the calling application (used mainly for pod/developer contexts). |  ---  ## Rename Rules &amp; Constraints  * The &#x60;from&#x60; floor ID **must exist** * The &#x60;to&#x60; floor ID **must be unique** and not already in use * The rename operation updates **only the floor ID**    * Floor ownership, blocks, posts, and internal &#x60;fid&#x60; remain unchanged * Any links or references using the old floor ID may no longer be valid after rename  ---  ## Behavior Summary  | Scenario                     | Result                                            | | ---------------------------- | ------------------------------------------------- | | Valid owner + unique new ID  | Floor ID renamed successfully                     | | Non-owner user               | Request rejected                                  | | &#x60;from&#x60; floor ID not found    | Error                                             | | &#x60;to&#x60; floor ID already exists | Error                                             | | &#x60;from&#x60; &#x3D;&#x3D; &#x60;to&#x60;               | No-op or validation error (implementation choice) |  ---  ## Response Format  &#x60;application/json&#x60;  ---  ## Sample Success Response  &#x60;&#x60;&#x60;json {   \&quot;status\&quot;: \&quot;SUCCESS\&quot;,   \&quot;old_floor_id\&quot;: \&quot;oldfloorid\&quot;,   \&quot;new_floor_id\&quot;: \&quot;newfloorid\&quot;,   \&quot;message\&quot;: \&quot;Floor ID renamed successfully\&quot; } &#x60;&#x60;&#x60;  ---  ## Sample Error Responses  ### Not Floor Owner  &#x60;&#x60;&#x60;json {   \&quot;status\&quot;: \&quot;ERROR\&quot;,   \&quot;message\&quot;: \&quot;Only the floor owner can rename the floor\&quot; } &#x60;&#x60;&#x60;  ---  ### Floor Not Found  &#x60;&#x60;&#x60;json {   \&quot;status\&quot;: \&quot;ERROR\&quot;,   \&quot;message\&quot;: \&quot;Source floor ID does not exist\&quot; } &#x60;&#x60;&#x60;  ---  ### Floor ID Already Exists  &#x60;&#x60;&#x60;json {   \&quot;status\&quot;: \&quot;ERROR\&quot;,   \&quot;message\&quot;: \&quot;Target floor ID is already in use\&quot; } &#x60;&#x60;&#x60;  ---  ### Invalid Request  &#x60;&#x60;&#x60;json {   \&quot;status\&quot;: \&quot;ERROR\&quot;,   \&quot;message\&quot;: \&quot;user_id, from, and to are required\&quot; } &#x60;&#x60;&#x60;  ---  ## Notes for Developers  * This API **renames the public identifier only**; the internal immutable floor ID (&#x60;fid&#x60;) is not affected. * Clients should refresh cached floor metadata after a successful rename. * If your platform supports deep links or bookmarks, consider redirect or alias handling for old floor IDs (if supported).  ---  ### One-Line Mental Model  &gt; **This API answers: “Change the public identity (ID) of a floor, owner-only.”** 

### Example

```javascript
import XfloorFloorMemorySdkJs from '@xfloor/floor-memory-sdk-js';

let apiInstance = new XfloorFloorMemorySdkJs.DefaultApi();
let opts = {
  'userId': "userId_example", // String | User ID
  'appId': "appId_example", // String | App ID
  'from': "from_example", // String | Old floor ID
  'to': "to_example" // String | New floor ID
};
apiInstance.renameFloor(opts, (error, data, response) => {
  if (error) {
    console.error(error);
  } else {
    console.log('API called successfully. Returned data: ' + data);
  }
});
```

### Parameters


Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **userId** | **String**| User ID | [optional] 
 **appId** | **String**| App ID | [optional] 
 **from** | **String**| Old floor ID | [optional] 
 **to** | **String**| New floor ID | [optional] 

### Return type

[**GetFloorInformation200Response**](GetFloorInformation200Response.md)

### Authorization

No authorization required

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: application/json


## resetPassword

> ResetPassword200Response resetPassword(activationCode, opts)

Reset Password

---  ## Reset Password (Forgot Password, Not Logged In)  Resets the password of a user who **cannot log in** and is using a **forgot-password** flow.  This endpoint is used when the user is not authenticated and requests a password reset using a verified identity channel such as **email** or **mobile number**. The system validates a **one-time reset verification code** (&#x60;activation_code&#x60;) issued for the reset-password flow. If valid and not expired, the password is updated to &#x60;new_password&#x60; and takes effect immediately.  If verification fails, the password remains unchanged and an error response is returned.  ### Authentication  ✅ **Recommended** (better security): a short-lived **reset token** issued after initiating reset  &#x60;&#x60;&#x60; Authorization: Bearer &lt;reset_token&gt; &#x60;&#x60;&#x60;  &gt; If you don’t use a reset token, you must enforce strong rate limiting + OTP attempt throttling on this endpoint.  ### Request Body (Form Data)  * &#x60;email_id&#x60; or &#x60;mobile_number&#x60; (required to identify user) * &#x60;activation_code&#x60; (required) * &#x60;new_password&#x60; (required) * &#x60;user_id&#x60; (optional, if your reset flow already resolved it)  ### Behavior Notes  * Requires a prior call to **initiate reset** and send OTP/code (mode &#x3D; forgot password). * Must enforce code attempt limits and expiration strictly.  ### One-Line Summary  &gt; Resets a user’s password (forgot-password flow) after validating a one-time reset code sent to email or mobile.   

### Example

```javascript
import XfloorFloorMemorySdkJs from '@xfloor/floor-memory-sdk-js';

let apiInstance = new XfloorFloorMemorySdkJs.DefaultApi();
let activationCode = "activationCode_example"; // String | Activation Code
let opts = {
  'emailId': "emailId_example", // String | Email ID
  'mobileNumber': "mobileNumber_example", // String | Mobile number
  'appId': "appId_example" // String | App ID
};
apiInstance.resetPassword(activationCode, opts, (error, data, response) => {
  if (error) {
    console.error(error);
  } else {
    console.log('API called successfully. Returned data: ' + data);
  }
});
```

### Parameters


Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **activationCode** | **String**| Activation Code | 
 **emailId** | **String**| Email ID | [optional] 
 **mobileNumber** | **String**| Mobile number | [optional] 
 **appId** | **String**| App ID | [optional] 

### Return type

[**ResetPassword200Response**](ResetPassword200Response.md)

### Authorization

No authorization required

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: application/json


## sendValidationCode

> SendValidationCode200Response sendValidationCode(sendValidationCodeRequest)

Send Validation code

Generates and sends a one-time validation code to the user for verification of sensitive or critical account operations.  This API is used across multiple authentication and account-management flows. The validation code is delivered to the user via the appropriate channel (**email or mobile number**), based on the requested operation mode and the input provided.  The generated code is **time-bound**, **single-use**, and must be validated using the corresponding verification APIs to complete the requested action.  ---  ### **Usage Scenarios (Mode Definition)**  | Mode | Purpose                       | | ---- | ----------------------------- | | &#x60;0&#x60;  | Email or mobile number change | | &#x60;1&#x60;  | Password change               | | &#x60;2&#x60;  | Delete account                | | &#x60;3&#x60;  | Clear account                 | | &#x60;4&#x60;  | Signup Verification           | | &#x60;5&#x60;  | Using OTP for Login           | | &#x60;6&#x60;  | OTP for forgot password       |  **Mode &#x60;4&#x60; – Signup Verification** For login verification, the validation code is sent to **either the email ID or the mobile number provided in the request**. At least **one of email or mobile number must be supplied** for this mode.  ---  ### **Behavior**  * Generates a secure, one-time validation code * Sends the code to the appropriate channel:    * Email or mobile number, depending on the operation mode and input * Associates the code with:    * User identity (or login identifier)   * Requested operation (&#x60;mode&#x60;)   * Application context (if applicable) * Validation codes are valid for a limited duration and **cannot be reused**  ---  ### **Authentication**  This endpoint requires **Bearer Token authentication**, **except** where explicitly allowed (for example, login-related flows).  &#x60;&#x60;&#x60; Authorization: Bearer &lt;access_token&gt; &#x60;&#x60;&#x60;  ---  ### **Successful Response**  On success, the API confirms that the validation code has been generated and successfully dispatched to the user.  ---  ### **Error Response**  The API returns an error response if:  * The user does not exist or is not eligible for the requested operation * The requested mode is invalid or unsupported * Required identifiers (email or mobile number for login verification) are missing * Rate limits are exceeded * Authorization fails (where applicable)  ---  ### **Security Notes (Recommended)**  * Validation codes are single-use and time-bound * Rate limiting is enforced to prevent abuse * Repeated failures may trigger temporary blocking or additional verification  ---  ### **One-Line Summary**  &gt; Sends a one-time validation code for secure account and authentication operations, including login via email or mobile number.

### Example

```javascript
import XfloorFloorMemorySdkJs from '@xfloor/floor-memory-sdk-js';
let defaultClient = XfloorFloorMemorySdkJs.ApiClient.instance;
// Configure Bearer access token for authorization: bearer
let bearer = defaultClient.authentications['bearer'];
bearer.accessToken = "YOUR ACCESS TOKEN"

let apiInstance = new XfloorFloorMemorySdkJs.DefaultApi();
let sendValidationCodeRequest = new XfloorFloorMemorySdkJs.SendValidationCodeRequest(); // SendValidationCodeRequest | 
apiInstance.sendValidationCode(sendValidationCodeRequest, (error, data, response) => {
  if (error) {
    console.error(error);
  } else {
    console.log('API called successfully. Returned data: ' + data);
  }
});
```

### Parameters


Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **sendValidationCodeRequest** | [**SendValidationCodeRequest**](SendValidationCodeRequest.md)|  | 

### Return type

[**SendValidationCode200Response**](SendValidationCode200Response.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

- **Content-Type**: application/json
- **Accept**: application/json


## signInWithEmail

> SignInWithEmail200Response signInWithEmail(emailId, passCode, loginType, opts)

Sign In with email ID

Authenticates a user using a registered email ID. The authentication mechanism is determined by the specified &#x60;mode&#x60;.  * When &#x60;login_type&#x60; is set to **&#x60;1&#x60;**, the user is authenticated using the provided **password**. * When &#x60;login_type&#x60; is set to **&#x60;2&#x60;**, the user is authenticated using a **one-time activation code (OTP)**.  For OTP-based authentication (&#x60;login_type &#x3D; 2&#x60;), the client **must first invoke the Send Validation Code API** with the appropriate login mode to generate and deliver the activation code to the user.  --- ### **Request Body**  | Field        | Type          | Required | Description                                                       | | ------------ | ------------- | -------- | ----------------------------------------------------------------- | | &#x60;email_id&#x60; | string | Yes      | Email ID | | &#x60;pass_code&#x60; | string | Yes      | Password/Validation code depending on the login_type| | &#x60;login_type&#x60; | string | Yes      | login type 1 for password 2 for validation code|   |&#x60;app_id&#x60; | string | Yes      | App ID |     **Field Description**  * &#x60;email_id&#x60; – Registered email address of the user * &#x60;pass_code&#x60; – password or activation code  (this is password if it is 1 and 2 it is validation code) * &#x60;app_id&#x60; - App ID which is a 13 digit numeric value * &#x60;login_type&#x60; – Login type   * &#x60;1&#x60; → Password-based login   * &#x60;2&#x60; → Activation code (OTP)–based login  ---  ### **Behavior Notes**  * When &#x60;login_type &#x3D; 2&#x60;, password validation is bypassed. * OTP-based login requires a prior call to &#x60; /auth-service/send/sign/in/validation/code&#x60;. * If the required credentials for the selected mode are missing or invalid, authentication fails.  ---  ### **Successful Response**  On successful authentication, the user is signed in and a success response is returned as per the authentication flow.  ---  ### **Error Response**  The API returns an error response if:  * The email ID is not registered * The password is incorrect (&#x60;login_type &#x3D; 1 &#x60;) * The activation code is missing, invalid, or expired (&#x60;login_type &#x3D; 2&#x60;) * The mode value is invalid or unsupported  ---  ### **One-Line Summary**  &gt; Signs in a user using an email ID with either password-based or OTP-based authentication, based on the selected mode.  

### Example

```javascript
import XfloorFloorMemorySdkJs from '@xfloor/floor-memory-sdk-js';
let defaultClient = XfloorFloorMemorySdkJs.ApiClient.instance;
// Configure Bearer access token for authorization: bearer
let bearer = defaultClient.authentications['bearer'];
bearer.accessToken = "YOUR ACCESS TOKEN"

let apiInstance = new XfloorFloorMemorySdkJs.DefaultApi();
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


Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **emailId** | **String**| Email ID | 
 **passCode** | **String**| Validation code or password depends on the login_type | 
 **loginType** | **String**| 1 is for password, 2 is for validation code | 
 **appId** | **String**| App ID | [optional] 

### Return type

[**SignInWithEmail200Response**](SignInWithEmail200Response.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

- **Content-Type**: multipart/form-data
- **Accept**: application/json


## signInWithMobileNumber

> SignInWithEmail200Response signInWithMobileNumber(body)

Sign In with Mobile number

Authenticates a user using a registered mobile number. The authentication method is determined by the specified &#x60;mode&#x60;.  * When &#x60;login_type&#x60; is set to **&#x60;1&#x60;**, the user is authenticated using the **password** associated with the account. * When &#x60;login_type&#x60; is set to **&#x60;2&#x60;**, the user is authenticated using a **one-time activation code (OTP)** sent to the registered mobile number.  For OTP-based authentication (&#x60;login_type &#x3D; 1&#x60;), the client **must first call the Send Validation Code API** with the appropriate login mode to generate and deliver the activation code.  ---  ### **Request Formdata**  | Field        | Type          | Required | Description                                                       | | ------------ | ------------- | -------- | ----------------------------------------------------------------- | | &#x60;mobile_number&#x60; | string | Yes      | Mobile number| | &#x60;pass_code&#x60; | string | Yes      | Password/Validation code depending on the login_type| | &#x60;login_type&#x60; | string | Yes      | login type 1 for password 2 for validation code|   |&#x60;app_id&#x60; | string | Yes      | App ID |    **Field Description**  * &#x60;mobile_number&#x60; – Registered mobile number of the user * &#x60;pass_code&#x60; – Password / Validation code (password when &#x60;login_type&#x3D; 1&#x60;; validation code when &#x60;login_type &#x3D; 2&#x60;) * &#x60;login_type&#x60; – Login type    * &#x60;1&#x60; → Password-based login   * &#x60;2&#x60; → Activation code (OTP)–based login  ---  ### **Behavior Notes**  * When &#x60;login_type &#x3D; 2&#x60;, password validation is skipped. * OTP-based login requires a prior call to &#x60;/auth-service/send/sign/in/validation/code&#x60;. * Missing or invalid credentials for the selected mode will result in authentication failure.  ---  ### **Successful Response**  On successful authentication, the user is signed in and a success response is returned according to the authentication flow.  ---  ### **Error Response**  The API returns an error response if:  * The mobile number is not registered * The password is incorrect (&#x60;login_type &#x3D; 1&#x60;) * The activation code is missing, invalid, or expired (&#x60;login_type &#x3D; 2&#x60;) * An invalid or unsupported mode is provided  ---  ### **One-Line Summary**  &gt; Signs in a user using a mobile number with either password-based or OTP-based authentication, based on the selected mode.

### Example

```javascript
import XfloorFloorMemorySdkJs from '@xfloor/floor-memory-sdk-js';
let defaultClient = XfloorFloorMemorySdkJs.ApiClient.instance;
// Configure Bearer access token for authorization: bearer
let bearer = defaultClient.authentications['bearer'];
bearer.accessToken = "YOUR ACCESS TOKEN"

let apiInstance = new XfloorFloorMemorySdkJs.DefaultApi();
let body = {key: null}; // Object | 
apiInstance.signInWithMobileNumber(body, (error, data, response) => {
  if (error) {
    console.error(error);
  } else {
    console.log('API called successfully. Returned data: ' + data);
  }
});
```

### Parameters


Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **body** | **Object**|  | 

### Return type

[**SignInWithEmail200Response**](SignInWithEmail200Response.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

- **Content-Type**: application/json
- **Accept**: application/json


## signUp

> SignUp200Response signUp(name, password, opts)

Sign Up

Creates a new user account in the Floor POD using **either a mobile number or an email ID**. At least **one of &#x60;mobile_number&#x60; or &#x60;email_id&#x60; is required** to register a user. Both may be provided if available.  The API registers the user under the specified application context and prepares the account for subsequent authentication and usage.  Upon successful registration, the API returns: - a unique user_id identifying the newly created user, and - a success string indicating the outcome of the sign-up operation. The user account is created under the specified application context and can be used for subsequent interactions with Floor POD APIs.  ---  ### **Parameter Clarification (Recommended)**  * &#x60;name&#x60; is mandatory for user profile creation * Either &#x60;mobile_number&#x60; **or** &#x60;email_id&#x60; must be present * &#x60;app_id&#x60; is optional and used to associate the user with a specific application   

### Example

```javascript
import XfloorFloorMemorySdkJs from '@xfloor/floor-memory-sdk-js';
let defaultClient = XfloorFloorMemorySdkJs.ApiClient.instance;
// Configure Bearer access token for authorization: bearer
let bearer = defaultClient.authentications['bearer'];
bearer.accessToken = "YOUR ACCESS TOKEN"

let apiInstance = new XfloorFloorMemorySdkJs.DefaultApi();
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


Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **name** | **String**| New User Name | 
 **password** | **String**| Password | 
 **emailId** | **String**| Email ID of the user | [optional] 
 **mobileNumber** | **String**| Mobile number | [optional] 
 **appId** | **String**| Registered App ID | [optional] 

### Return type

[**SignUp200Response**](SignUp200Response.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

- **Content-Type**: multipart/form-data
- **Accept**: application/json


## validateCode

> UserDetails validateCode(validateCodeRequest)

Validation

## **Validate Activation / Verification Code**  This API **validates a one-time verification code** submitted by a user and **executes the corresponding account operation** based on the specified **mode**.  Depending on the mode, the API may:  * Activate a newly registered account * Confirm a login attempt * Verify a password change or reset * Validate email or mobile updates * Confirm account deletion or clearing requests  The API verifies the provided &#x60;activation_code&#x60; against the given &#x60;user_id&#x60;, &#x60;mode&#x60;, and application context. If validation succeeds, the requested operation is completed and the API returns the relevant **POD information** and **user profile details** (where applicable).  If validation fails, the operation is **not performed** and an appropriate error response is returned.  ---  ## **Authentication**  This endpoint requires **Bearer Token authentication**.  **Header**  &#x60;&#x60;&#x60; Authorization: Bearer &lt;access_token&gt; &#x60;&#x60;&#x60;  ---  ## **Request Body**  &#x60;&#x60;&#x60;json {   \&quot;user_id\&quot;: \&quot;string\&quot;,   \&quot;activation_code\&quot;: \&quot;string\&quot;,   \&quot;app_id\&quot;: \&quot;string\&quot;,   \&quot;mode\&quot;: \&quot;string\&quot; } &#x60;&#x60;&#x60;  ### **Field Descriptions**  * **user_id** – Unique identifier of the user initiating the operation * **activation_code** – One-time verification code sent to the user * **app_id** – Application identifier (optional or context-specific) * **mode** – Operation context for which the verification is being performed  ---  ## **Usage Scenarios (Mode Definitions)**  | Mode | Purpose                                  | | ---- | ---------------------------------------- | | 0    | Email or mobile number change            | | 1    | Password change                          | | 2    | Delete account                           | | 3    | Clear account                            | | 4    | Signup verification (account activation) | | 5    | Login verification                       | | 6    | Forgot password verification             |  ---  ## **Successful Response**  On successful validation:  * The requested operation (based on &#x60;mode&#x60;) is completed * The API returns:    * **POD information** associated with the user (if applicable)   * **User profile details** (if applicable)  Examples:  * For **signup verification**, the user account is activated * For **login**, access is confirmed * For **password reset**, the user may proceed to set a new password * For **account deletion**, the request is confirmed  ---  ## **Error Response**  The API returns an error response when:  * The activation code is invalid or expired * The activation code does not match the user or operation mode * The requested operation is already completed (e.g., user already activated) * Authorization fails or the bearer token is missing or invalid  ⚠️ In all error cases, **no account state change occurs**.  ---  ## **One-Line Summary**  &gt; Validates a one-time verification code and securely completes the requested user account operation (signup, login, password change, or account actions), returning POD and profile details on success.

### Example

```javascript
import XfloorFloorMemorySdkJs from '@xfloor/floor-memory-sdk-js';
let defaultClient = XfloorFloorMemorySdkJs.ApiClient.instance;
// Configure Bearer access token for authorization: bearer
let bearer = defaultClient.authentications['bearer'];
bearer.accessToken = "YOUR ACCESS TOKEN"

let apiInstance = new XfloorFloorMemorySdkJs.DefaultApi();
let validateCodeRequest = new XfloorFloorMemorySdkJs.ValidateCodeRequest(); // ValidateCodeRequest | 
apiInstance.validateCode(validateCodeRequest, (error, data, response) => {
  if (error) {
    console.error(error);
  } else {
    console.log('API called successfully. Returned data: ' + data);
  }
});
```

### Parameters


Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **validateCodeRequest** | [**ValidateCodeRequest**](ValidateCodeRequest.md)|  | 

### Return type

[**UserDetails**](UserDetails.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

- **Content-Type**: application/json
- **Accept**: application/json

