# DefaultApi

All URIs are relative to *https://appfloor.in*

| Method | HTTP request | Description |
|------------- | ------------- | -------------|
| [**changeEmail**](DefaultApi.md#changeEmail) | **POST** /auth-service/change/email | Change email ID |
| [**changeMobileNumber**](DefaultApi.md#changeMobileNumber) | **POST** /auth-service/change/mobile | Change Mobile number |
| [**changePassword**](DefaultApi.md#changePassword) | **POST** /auth-service/password/change | Change Password |
| [**makeFloorPrivate**](DefaultApi.md#makeFloorPrivate) | **POST** /api/memory/make/floor/private | Make floor Private |
| [**makeFloorPublic**](DefaultApi.md#makeFloorPublic) | **POST** /api/memory/make/floor/public | Make floor public |
| [**registerExternalUserIdentity**](DefaultApi.md#registerExternalUserIdentity) | **POST** /memory/identity/external-user | External User Registration |
| [**renameFloor**](DefaultApi.md#renameFloor) | **POST** /api/memory/change/floor/id | Rename floor |
| [**resetPassword**](DefaultApi.md#resetPassword) | **POST** /auth-service/password/reset | Reset Password |
| [**sendValidationCode**](DefaultApi.md#sendValidationCode) | **POST** /auth-service/send/validation/code | Send Validation code |
| [**signInWithEmail**](DefaultApi.md#signInWithEmail) | **POST** /auth-service/sign/in/with/email | Sign In with email ID |
| [**signInWithMobileNumber**](DefaultApi.md#signInWithMobileNumber) | **POST** /auth-service/sign/in/with/mobile/number | Sign In with Mobile number |
| [**signUp**](DefaultApi.md#signUp) | **POST** /auth-service/sign/up | Sign Up |
| [**validateCode**](DefaultApi.md#validateCode) | **POST** /auth-service/validate/activation/code | Validation |


<a id="changeEmail"></a>
# **changeEmail**
> Object changeEmail(newEmailId, activationCode)

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
```java
// Import classes:
import ai.xfloor.memory.client.ApiClient;
import ai.xfloor.memory.client.ApiException;
import ai.xfloor.memory.client.Configuration;
import ai.xfloor.memory.client.auth.*;
import ai.xfloor.memory.client.models.*;
import ai.xfloor.memory.api.DefaultApi;

public class Example {
  public static void main(String[] args) {
    ApiClient defaultClient = Configuration.getDefaultApiClient();
    defaultClient.setBasePath("https://appfloor.in");
    
    // Configure HTTP bearer authorization: bearer
    HttpBearerAuth bearer = (HttpBearerAuth) defaultClient.getAuthentication("bearer");
    bearer.setBearerToken("BEARER TOKEN");

    DefaultApi apiInstance = new DefaultApi(defaultClient);
    String newEmailId = "newEmailId_example"; // String | New Email ID
    String activationCode = "activationCode_example"; // String | Validation code
    try {
      Object result = apiInstance.changeEmail(newEmailId, activationCode);
      System.out.println(result);
    } catch (ApiException e) {
      System.err.println("Exception when calling DefaultApi#changeEmail");
      System.err.println("Status code: " + e.getCode());
      System.err.println("Reason: " + e.getResponseBody());
      System.err.println("Response headers: " + e.getResponseHeaders());
      e.printStackTrace();
    }
  }
}
```

### Parameters

| Name | Type | Description | Notes |
|------------- | ------------- | ------------- | -------------|
| **newEmailId** | **String**| New Email ID |
|
| **activationCode** | **String**| Validation code |
|

### Return type

**Object**

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

 - **Content-Type**: multipart/form-data
 - **Accept**: application/json

### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** |
|
- |
| **400** |
|
- |

<a id="changeMobileNumber"></a>
# **changeMobileNumber**
> Object changeMobileNumber(body)

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
```java
// Import classes:
import ai.xfloor.memory.client.ApiClient;
import ai.xfloor.memory.client.ApiException;
import ai.xfloor.memory.client.Configuration;
import ai.xfloor.memory.client.auth.*;
import ai.xfloor.memory.client.models.*;
import ai.xfloor.memory.api.DefaultApi;

public class Example {
  public static void main(String[] args) {
    ApiClient defaultClient = Configuration.getDefaultApiClient();
    defaultClient.setBasePath("https://appfloor.in");
    
    // Configure HTTP bearer authorization: bearer
    HttpBearerAuth bearer = (HttpBearerAuth) defaultClient.getAuthentication("bearer");
    bearer.setBearerToken("BEARER TOKEN");

    DefaultApi apiInstance = new DefaultApi(defaultClient);
    Object body = null; // Object | 
    try {
      Object result = apiInstance.changeMobileNumber(body);
      System.out.println(result);
    } catch (ApiException e) {
      System.err.println("Exception when calling DefaultApi#changeMobileNumber");
      System.err.println("Status code: " + e.getCode());
      System.err.println("Reason: " + e.getResponseBody());
      System.err.println("Response headers: " + e.getResponseHeaders());
      e.printStackTrace();
    }
  }
}
```

### Parameters

| Name | Type | Description | Notes |
|------------- | ------------- | ------------- | -------------|
| **body** | **Object**|
| |

### Return type

**Object**

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json

### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** |
|
- |
| **400** |
|
- |

<a id="changePassword"></a>
# **changePassword**
> ChangePassword200Response changePassword(newPassword, activationCode, userId)

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
```java
// Import classes:
import ai.xfloor.memory.client.ApiClient;
import ai.xfloor.memory.client.ApiException;
import ai.xfloor.memory.client.Configuration;
import ai.xfloor.memory.client.auth.*;
import ai.xfloor.memory.client.models.*;
import ai.xfloor.memory.api.DefaultApi;

public class Example {
  public static void main(String[] args) {
    ApiClient defaultClient = Configuration.getDefaultApiClient();
    defaultClient.setBasePath("https://appfloor.in");
    
    // Configure HTTP bearer authorization: bearer
    HttpBearerAuth bearer = (HttpBearerAuth) defaultClient.getAuthentication("bearer");
    bearer.setBearerToken("BEARER TOKEN");

    DefaultApi apiInstance = new DefaultApi(defaultClient);
    String newPassword = "newPassword_example"; // String | New Password
    String activationCode = "activationCode_example"; // String | Validation code
    String userId = "userId_example"; // String | User ID
    try {
      ChangePassword200Response result = apiInstance.changePassword(newPassword, activationCode, userId);
      System.out.println(result);
    } catch (ApiException e) {
      System.err.println("Exception when calling DefaultApi#changePassword");
      System.err.println("Status code: " + e.getCode());
      System.err.println("Reason: " + e.getResponseBody());
      System.err.println("Response headers: " + e.getResponseHeaders());
      e.printStackTrace();
    }
  }
}
```

### Parameters

| Name | Type | Description | Notes |
|------------- | ------------- | ------------- | -------------|
| **newPassword** | **String**| New Password |
|
| **activationCode** | **String**| Validation code |
|
| **userId** | **String**| User ID | [optional] |

### Return type

[**ChangePassword200Response**](ChangePassword200Response.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

 - **Content-Type**: multipart/form-data
 - **Accept**: application/json

### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** |
|
- |
| **400** |
|
- |

<a id="makeFloorPrivate"></a>
# **makeFloorPrivate**
> GetFloorInformation200Response makeFloorPrivate(floorId, userId, appId)

Make floor Private

This API changes a floor’s visibility to **PRIVATE**. It is used when a floor owner wants to **restrict access** to a floor that is currently public. After the update, the floor becomes private and is no longer accessible to non-authorized users (based on your platform’s access rules). This endpoint is **state-changing**:
* If the floor is **PUBLIC**, it will be converted to **PRIVATE**
* If the floor is already **PRIVATE**, the API returns success (idempotent) or an “already private” response depending on implementation This API is commonly used in:
* Floor settings → “Privacy” toggle
* Developer-managed pod workflows (app_id context) * Admin tools (if applicable)

---

**Request Method**

 `POST`

---

**Content-Type**

 `application/x-www-form-urlencoded` (or `multipart/form-data` if your system uses form-data)

*(Document whichever you actually accept; below assumes standard form fields.)*

---

**Request Parameters (Form Fields)**

| Field | Type | Required | Description |
| ---------- | ------ | -------- | -------------------------------------------------------------------- |
| `user_id` | String | **Yes** | User requesting the change. Must be the **owner** of the floor. |
| `floor_id` | String | **Yes** | Public identifier of the floor to update. |
| `app_id` | String | No | Calling application identifier (used for developer/pod integration). |

---

### Authorization Rules (Critical)
* The caller must be authenticated as `user_id`
* **Only the floor owner** can change floor visibility * If the user is not the owner, the request must be rejected

---

### Behavior Rules
* Converts visibility from **PUBLIC → PRIVATE**
* Does not modify floor content or blocks * Access enforcement for private floors is applied immediately after the change **Idempotency**
* Calling this API multiple times should not cause repeated changes
* If already private, the API should either:
* return success with a message like `\"already private\"`, or
* return a specific error/status indicating no-op

---

### Response Format `application/json`

---

### Sample

Success Response *(Example — adjust to match your actual response format)*

```json { \"status\":

\"SUCCESS\", \"floor_id\": \"my_floor\", \"visibility\": \"PRIVATE\", \"message\": \"Floor is now private\" }

```

---

### Sample No-Op Response (Already Private)

```json { \"status\": \"SUCCESS\", \"floor_id\": \"my_floor\", \"visibility\": \"PRIVATE\", \"message\": \"Floor is already private\" }

```

---

### Error Responses (Examples)

### Not Authorized (Not Owner)

```json { \"status\": \"ERROR\", \"message\": \"Only the floor owner can change floor visibility\" }

```

### Floor Not Found

```json { \"status\": \"ERROR\", \"message\": \"Floor not found\" }

```

### Invalid Request

```json { \"status\": \"ERROR\", \"message\": \"user_id and floor_id are required\" }

```

---

### Notes
* This API is intended to control floor visibility only; membership/invite rules (for private floors)

are handled elsewhere. * `app_id` is provided for developer/pod applications and is optional unless enforced by your app model. * If you support floor types like `POD`, document whether pods are allowed to be private or not (some platforms restrict this).

### Example
```java
// Import classes:
import ai.xfloor.memory.client.ApiClient;
import ai.xfloor.memory.client.ApiException;
import ai.xfloor.memory.client.Configuration;
import ai.xfloor.memory.client.auth.*;
import ai.xfloor.memory.client.models.*;
import ai.xfloor.memory.api.DefaultApi;

public class Example {
  public static void main(String[] args) {
    ApiClient defaultClient = Configuration.getDefaultApiClient();
    defaultClient.setBasePath("https://appfloor.in");
    
    // Configure HTTP bearer authorization: bearer
    HttpBearerAuth bearer = (HttpBearerAuth) defaultClient.getAuthentication("bearer");
    bearer.setBearerToken("BEARER TOKEN");

    DefaultApi apiInstance = new DefaultApi(defaultClient);
    String floorId = "floorId_example"; // String | Floor ID
    String userId = "userId_example"; // String | User ID
    String appId = "appId_example"; // String | App ID
    try {
      GetFloorInformation200Response result = apiInstance.makeFloorPrivate(floorId, userId, appId);
      System.out.println(result);
    } catch (ApiException e) {
      System.err.println("Exception when calling DefaultApi#makeFloorPrivate");
      System.err.println("Status code: " + e.getCode());
      System.err.println("Reason: " + e.getResponseBody());
      System.err.println("Response headers: " + e.getResponseHeaders());
      e.printStackTrace();
    }
  }
}
```

### Parameters

| Name | Type | Description | Notes |
|------------- | ------------- | ------------- | -------------|
| **floorId** | **String**| Floor ID | [optional] |
| **userId** | **String**| User ID | [optional] |
| **appId** | **String**| App ID | [optional] |

### Return type

[**GetFloorInformation200Response**](GetFloorInformation200Response.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** |
|
- |
| **400** |
|
- |

<a id="makeFloorPublic"></a>
# **makeFloorPublic**
> GetFloorInformation200Response makeFloorPublic(floorId, userId, appId)

Make floor public

This API changes a floor’s visibility to **PUBLIC**. It is used when a floor owner wants to **make a private floor accessible to everyone**. After the update, the floor becomes public and can be viewed and discovered by any user, subject to platform rules (search, feeds, pods, etc.). This endpoint performs a **visibility state transition**:
* **PRIVATE → PUBLIC**
* If the floor is already public, the operation is treated as **idempotent** (no state change). This API is typically used from:
* Floor settings → Privacy / Visibility controls
* Owner or admin tools * Developer or pod-based applications using `app_id`

---

**Request Method**

 `POST`

---

**Content-Type**

 `application/x-www-form-urlencoded` (or `multipart/form-data`, depending on your implementation)

---

**Request Parameters (Form Fields)**

| Field | Type | Required | Description |
| ---------- | ------ | -------- | ------------------------------------------------------------------------------- |
| `user_id` | String | **Yes** | User requesting the change. Must be the **owner** of the floor. |
| `floor_id` | String | **Yes** | Public identifier of the floor whose visibility is to be changed. |
| `app_id` | String | No | Identifier of the calling application (used mainly for pod/developer contexts). |

---

### Authorization Rules (Critical)
* The caller must be authenticated as `user_id`
* **Only the floor owner** is allowed to change the floor’s visibility * Requests from non-owners must be rejected

---

### Behavior Rules
* Converts floor visibility from **PRIVATE → PUBLIC**
* Does not modify floor content, blocks, or ownership * Visibility change takes effect immediately

### Idempotency
* If the floor is already public, the API should:
* Return success with a message indicating no change, or
* Return a specific “already public” status (implementation-dependent)

---

### Response Format `application/json`

---

### Sample

Success Response

```json { \"status\":

\"SUCCESS\", \"floor_id\": \"my_floor\", \"visibility\": \"PUBLIC\", \"message\": \"Floor is now public\" }

```

---

### Sample No-Op Response (Already Public)

```json { \"status\": \"SUCCESS\", \"floor_id\": \"my_floor\", \"visibility\": \"PUBLIC\", \"message\": \"Floor is already public\" }

```

---

### Error Responses (Examples)

### Not Authorized (Not Owner)

```json { \"status\": \"ERROR\", \"message\": \"Only the floor owner can change floor visibility\" }

```

---

### Floor Not Found

```json { \"status\":

\"ERROR\", \"message\": \"Floor not found\" }

```

---

### Invalid Request

```json { \"status\":

\"ERROR\", \"message\": \"user_id and floor_id are required\" }

```

---

### Notes for Developers
* This API controls **visibility only**. Membership, invitations, and moderation rules are handled by separate APIs.
* `app_id` is optional and primarily used for developer-managed or pod floors. * Clients should refresh floor metadata (e.g., via `/api/floor/info`)

after a successful visibility change.

---

### Mental Model (One Line)

> **This API answers: “Make this floor visible to everyone.”**

### Example
```java
// Import classes:
import ai.xfloor.memory.client.ApiClient;
import ai.xfloor.memory.client.ApiException;
import ai.xfloor.memory.client.Configuration;
import ai.xfloor.memory.client.auth.*;
import ai.xfloor.memory.client.models.*;
import ai.xfloor.memory.api.DefaultApi;

public class Example {
  public static void main(String[] args) {
    ApiClient defaultClient = Configuration.getDefaultApiClient();
    defaultClient.setBasePath("https://appfloor.in");
    
    // Configure HTTP bearer authorization: bearer
    HttpBearerAuth bearer = (HttpBearerAuth) defaultClient.getAuthentication("bearer");
    bearer.setBearerToken("BEARER TOKEN");

    DefaultApi apiInstance = new DefaultApi(defaultClient);
    String floorId = "floorId_example"; // String | Floor ID
    String userId = "userId_example"; // String | User ID
    String appId = "appId_example"; // String | App ID
    try {
      GetFloorInformation200Response result = apiInstance.makeFloorPublic(floorId, userId, appId);
      System.out.println(result);
    } catch (ApiException e) {
      System.err.println("Exception when calling DefaultApi#makeFloorPublic");
      System.err.println("Status code: " + e.getCode());
      System.err.println("Reason: " + e.getResponseBody());
      System.err.println("Response headers: " + e.getResponseHeaders());
      e.printStackTrace();
    }
  }
}
```

### Parameters

| Name | Type | Description | Notes |
|------------- | ------------- | ------------- | -------------|
| **floorId** | **String**| Floor ID | [optional] |
| **userId** | **String**| User ID | [optional] |
| **appId** | **String**| App ID | [optional] |

### Return type

[**GetFloorInformation200Response**](GetFloorInformation200Response.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** |
|
- |
| **400** |
|
- |

<a id="registerExternalUserIdentity"></a>
# **registerExternalUserIdentity**
> SignInWithEmail200Response registerExternalUserIdentity(mobileNumber, emailId, name, appId)

External User Registration

This API allows a calling application to **pass externally authenticated user identity information to xfloor** after completing authentication within its own system. xfloor **does not perform authentication, credential verification, or session management** as part of this API. The calling application is fully responsible for validating the user and ensuring the correctness of the identity data provided. Upon invocation, xfloor will:
* **Create a new user profile** if no matching user exists, or
* **Update the existing user profile** if the user is already present. xfloor returns a unique `xfloor_user_id`, which serves as the **canonical user identifier** and must be used in all subsequent xfloor APIs, including floors, blocks, conversations, memory interactions, and analytics.

### Example
```java
// Import classes:
import ai.xfloor.memory.client.ApiClient;
import ai.xfloor.memory.client.ApiException;
import ai.xfloor.memory.client.Configuration;
import ai.xfloor.memory.client.auth.*;
import ai.xfloor.memory.client.models.*;
import ai.xfloor.memory.api.DefaultApi;

public class Example {
  public static void main(String[] args) {
    ApiClient defaultClient = Configuration.getDefaultApiClient();
    defaultClient.setBasePath("https://appfloor.in");
    
    // Configure HTTP bearer authorization: bearer
    HttpBearerAuth bearer = (HttpBearerAuth) defaultClient.getAuthentication("bearer");
    bearer.setBearerToken("BEARER TOKEN");

    DefaultApi apiInstance = new DefaultApi(defaultClient);
    String mobileNumber = "mobileNumber_example"; // String | 
    String emailId = "emailId_example"; // String | 
    String name = "name_example"; // String | 
    String appId = "appId_example"; // String | 
    try {
      SignInWithEmail200Response result = apiInstance.registerExternalUserIdentity(mobileNumber, emailId, name, appId);
      System.out.println(result);
    } catch (ApiException e) {
      System.err.println("Exception when calling DefaultApi#registerExternalUserIdentity");
      System.err.println("Status code: " + e.getCode());
      System.err.println("Reason: " + e.getResponseBody());
      System.err.println("Response headers: " + e.getResponseHeaders());
      e.printStackTrace();
    }
  }
}
```

### Parameters

| Name | Type | Description | Notes |
|------------- | ------------- | ------------- | -------------|
| **mobileNumber** | **String**|
| [optional] |
| **emailId** | **String**|
| [optional] |
| **name** | **String**|
| [optional] |
| **appId** | **String**|
| [optional] |

### Return type

[**SignInWithEmail200Response**](SignInWithEmail200Response.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

 - **Content-Type**: multipart/form-data
 - **Accept**: application/json

### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** |
|
- |

<a id="renameFloor"></a>
# **renameFloor**
> GetFloorInformation200Response renameFloor(userId, appId, from, to)

Rename floor

This API renames a floor by changing knowing the **floor identifier (floor_id)**. It allows the **floor owner** to update the public-facing floor ID (slug/handle) from an old value to a new value. This is typically used when the owner wants to rebrand, reorganize, or correct the floor’s identifier. ⚠️ **This operation affects how the floor is accessed and referenced externally**, so it must be performed carefully.

---

### Ownership & Authorization (Critical)
* The caller **must be authenticated**
* **Only the floor owner** is allowed to rename a floor * Members, followers, or non-owners **cannot** perform this operation * Ownership is validated internally using `user_id` > If the user is not the owner, the request must be rejected.

---

**Request Method**

 `POST`

---

**Content-Type**

 `application/x-www-form-urlencoded` (or equivalent form-data encoding)

---

**Request Parameters (Form Fields)**

| Parameter | Type | Required | Description |
| --------- | ------ | -------- | ------------------------------------------------------------------------------- |
| `user_id` | String | **Yes** | User requesting the rename. Must be the **owner** of the floor. |
| `from` | String | **Yes** | Existing floor ID (current identifier to be renamed). |
| `to` | String | **Yes** | New floor ID to assign to the floor. |
| `app_id` | String | No | Identifier of the calling application (used mainly for pod/developer contexts). |

---

### Rename Rules & Constraints
* The `from` floor ID **must exist**
* The `to` floor ID **must be unique** and not already in use * The rename operation updates **only the floor ID**
* Floor ownership, blocks, posts, and internal `fid` remain unchanged
* Any links or references using the old floor ID may no longer be valid after rename

---

### Behavior Summary

| Scenario | Result |
| ---------------------------- | ------------------------------------------------- |
| Valid owner + unique new ID | Floor ID renamed successfully |
| Non-owner user | Request rejected |
| `from` floor ID not found | Error |
| `to` floor ID already exists | Error |
| `from` == `to` | No-op or validation error (implementation choice) |

---

### Response Format `application/json`

---

### Sample

Success Response

```json { \"status\":

\"SUCCESS\", \"old_floor_id\": \"oldfloorid\", \"new_floor_id\": \"newfloorid\", \"message\": \"Floor ID renamed successfully\" }

```

---

### Sample

Error Responses

### Not Floor Owner

```json { \"status\":

\"ERROR\", \"message\": \"Only the floor owner can rename the floor\" }

```

---

### Floor Not Found

```json { \"status\":

\"ERROR\", \"message\": \"Source floor ID does not exist\" }

```

---

### Floor ID Already Exists

```json { \"status\":

\"ERROR\", \"message\": \"Target floor ID is already in use\" }

```

---

### Invalid Request

```json { \"status\":

\"ERROR\", \"message\": \"user_id, from, and to are required\" }

```

---

### Notes for Developers
* This API **renames the public identifier only**; the internal immutable floor ID (`fid`)

is not affected. * Clients should refresh cached floor metadata after a successful rename. * If your platform supports deep links or bookmarks, consider redirect or alias handling for old floor IDs (if supported).

---

### One-Line Mental Model 

> **This API answers:

“Change the public identity (ID)

of a floor, owner-only.”**

### Example
```java
// Import classes:
import ai.xfloor.memory.client.ApiClient;
import ai.xfloor.memory.client.ApiException;
import ai.xfloor.memory.client.Configuration;
import ai.xfloor.memory.client.models.*;
import ai.xfloor.memory.api.DefaultApi;

public class Example {
  public static void main(String[] args) {
    ApiClient defaultClient = Configuration.getDefaultApiClient();
    defaultClient.setBasePath("https://appfloor.in");

    DefaultApi apiInstance = new DefaultApi(defaultClient);
    String userId = "userId_example"; // String | User ID
    String appId = "appId_example"; // String | App ID
    String from = "from_example"; // String | Old floor ID
    String to = "to_example"; // String | New floor ID
    try {
      GetFloorInformation200Response result = apiInstance.renameFloor(userId, appId, from, to);
      System.out.println(result);
    } catch (ApiException e) {
      System.err.println("Exception when calling DefaultApi#renameFloor");
      System.err.println("Status code: " + e.getCode());
      System.err.println("Reason: " + e.getResponseBody());
      System.err.println("Response headers: " + e.getResponseHeaders());
      e.printStackTrace();
    }
  }
}
```

### Parameters

| Name | Type | Description | Notes |
|------------- | ------------- | ------------- | -------------|
| **userId** | **String**| User ID | [optional] |
| **appId** | **String**| App ID | [optional] |
| **from** | **String**| Old floor ID | [optional] |
| **to** | **String**| New floor ID | [optional] |

### Return type

[**GetFloorInformation200Response**](GetFloorInformation200Response.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** |
|
- |
| **400** |
|
- |

<a id="resetPassword"></a>
# **resetPassword**
> ResetPassword200Response resetPassword(activationCode, emailId, mobileNumber, appId)

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
```java
// Import classes:
import ai.xfloor.memory.client.ApiClient;
import ai.xfloor.memory.client.ApiException;
import ai.xfloor.memory.client.Configuration;
import ai.xfloor.memory.client.models.*;
import ai.xfloor.memory.api.DefaultApi;

public class Example {
  public static void main(String[] args) {
    ApiClient defaultClient = Configuration.getDefaultApiClient();
    defaultClient.setBasePath("https://appfloor.in");

    DefaultApi apiInstance = new DefaultApi(defaultClient);
    String activationCode = "activationCode_example"; // String | Activation Code
    String emailId = "emailId_example"; // String | Email ID
    String mobileNumber = "mobileNumber_example"; // String | Mobile number
    String appId = "appId_example"; // String | App ID
    try {
      ResetPassword200Response result = apiInstance.resetPassword(activationCode, emailId, mobileNumber, appId);
      System.out.println(result);
    } catch (ApiException e) {
      System.err.println("Exception when calling DefaultApi#resetPassword");
      System.err.println("Status code: " + e.getCode());
      System.err.println("Reason: " + e.getResponseBody());
      System.err.println("Response headers: " + e.getResponseHeaders());
      e.printStackTrace();
    }
  }
}
```

### Parameters

| Name | Type | Description | Notes |
|------------- | ------------- | ------------- | -------------|
| **activationCode** | **String**| Activation Code |
|
| **emailId** | **String**| Email ID | [optional] |
| **mobileNumber** | **String**| Mobile number | [optional] |
| **appId** | **String**| App ID | [optional] |

### Return type

[**ResetPassword200Response**](ResetPassword200Response.md)

### Authorization

No authorization required

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** |
|
- |
| **400** |
|
- |

<a id="sendValidationCode"></a>
# **sendValidationCode**
> SendValidationCode200Response sendValidationCode(sendValidationCodeRequest)

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
```java
// Import classes:
import ai.xfloor.memory.client.ApiClient;
import ai.xfloor.memory.client.ApiException;
import ai.xfloor.memory.client.Configuration;
import ai.xfloor.memory.client.auth.*;
import ai.xfloor.memory.client.models.*;
import ai.xfloor.memory.api.DefaultApi;

public class Example {
  public static void main(String[] args) {
    ApiClient defaultClient = Configuration.getDefaultApiClient();
    defaultClient.setBasePath("https://appfloor.in");
    
    // Configure HTTP bearer authorization: bearer
    HttpBearerAuth bearer = (HttpBearerAuth) defaultClient.getAuthentication("bearer");
    bearer.setBearerToken("BEARER TOKEN");

    DefaultApi apiInstance = new DefaultApi(defaultClient);
    SendValidationCodeRequest sendValidationCodeRequest = new SendValidationCodeRequest(); // SendValidationCodeRequest | 
    try {
      SendValidationCode200Response result = apiInstance.sendValidationCode(sendValidationCodeRequest);
      System.out.println(result);
    } catch (ApiException e) {
      System.err.println("Exception when calling DefaultApi#sendValidationCode");
      System.err.println("Status code: " + e.getCode());
      System.err.println("Reason: " + e.getResponseBody());
      System.err.println("Response headers: " + e.getResponseHeaders());
      e.printStackTrace();
    }
  }
}
```

### Parameters

| Name | Type | Description | Notes |
|------------- | ------------- | ------------- | -------------|
| **sendValidationCodeRequest** | [**SendValidationCodeRequest**](SendValidationCodeRequest.md)|
| |

### Return type

[**SendValidationCode200Response**](SendValidationCode200Response.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json

### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** |
|
- |
| **400** |
|
- |

<a id="signInWithEmail"></a>
# **signInWithEmail**
> SignInWithEmail200Response signInWithEmail(emailId, passCode, loginType, appId)

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
```java
// Import classes:
import ai.xfloor.memory.client.ApiClient;
import ai.xfloor.memory.client.ApiException;
import ai.xfloor.memory.client.Configuration;
import ai.xfloor.memory.client.auth.*;
import ai.xfloor.memory.client.models.*;
import ai.xfloor.memory.api.DefaultApi;

public class Example {
  public static void main(String[] args) {
    ApiClient defaultClient = Configuration.getDefaultApiClient();
    defaultClient.setBasePath("https://appfloor.in");
    
    // Configure HTTP bearer authorization: bearer
    HttpBearerAuth bearer = (HttpBearerAuth) defaultClient.getAuthentication("bearer");
    bearer.setBearerToken("BEARER TOKEN");

    DefaultApi apiInstance = new DefaultApi(defaultClient);
    String emailId = "emailId_example"; // String | Email ID
    String passCode = "passCode_example"; // String | Validation code or password depends on the login_type
    String loginType = "loginType_example"; // String | 1 is for password, 2 is for validation code
    String appId = "appId_example"; // String | App ID
    try {
      SignInWithEmail200Response result = apiInstance.signInWithEmail(emailId, passCode, loginType, appId);
      System.out.println(result);
    } catch (ApiException e) {
      System.err.println("Exception when calling DefaultApi#signInWithEmail");
      System.err.println("Status code: " + e.getCode());
      System.err.println("Reason: " + e.getResponseBody());
      System.err.println("Response headers: " + e.getResponseHeaders());
      e.printStackTrace();
    }
  }
}
```

### Parameters

| Name | Type | Description | Notes |
|------------- | ------------- | ------------- | -------------|
| **emailId** | **String**| Email ID |
|
| **passCode** | **String**| Validation code or password depends on the login_type |
|
| **loginType** | **String**| 1 is for password, 2 is for validation code |
|
| **appId** | **String**| App ID | [optional] |

### Return type

[**SignInWithEmail200Response**](SignInWithEmail200Response.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

 - **Content-Type**: multipart/form-data
 - **Accept**: application/json

### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** |
|
- |
| **400** |
|
- |

<a id="signInWithMobileNumber"></a>
# **signInWithMobileNumber**
> SignInWithEmail200Response signInWithMobileNumber(body)

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
```java
// Import classes:
import ai.xfloor.memory.client.ApiClient;
import ai.xfloor.memory.client.ApiException;
import ai.xfloor.memory.client.Configuration;
import ai.xfloor.memory.client.auth.*;
import ai.xfloor.memory.client.models.*;
import ai.xfloor.memory.api.DefaultApi;

public class Example {
  public static void main(String[] args) {
    ApiClient defaultClient = Configuration.getDefaultApiClient();
    defaultClient.setBasePath("https://appfloor.in");
    
    // Configure HTTP bearer authorization: bearer
    HttpBearerAuth bearer = (HttpBearerAuth) defaultClient.getAuthentication("bearer");
    bearer.setBearerToken("BEARER TOKEN");

    DefaultApi apiInstance = new DefaultApi(defaultClient);
    Object body = null; // Object | 
    try {
      SignInWithEmail200Response result = apiInstance.signInWithMobileNumber(body);
      System.out.println(result);
    } catch (ApiException e) {
      System.err.println("Exception when calling DefaultApi#signInWithMobileNumber");
      System.err.println("Status code: " + e.getCode());
      System.err.println("Reason: " + e.getResponseBody());
      System.err.println("Response headers: " + e.getResponseHeaders());
      e.printStackTrace();
    }
  }
}
```

### Parameters

| Name | Type | Description | Notes |
|------------- | ------------- | ------------- | -------------|
| **body** | **Object**|
| |

### Return type

[**SignInWithEmail200Response**](SignInWithEmail200Response.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json

### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** |
|
- |
| **400** |
|
- |

<a id="signUp"></a>
# **signUp**
> SignUp200Response signUp(name, password, emailId, mobileNumber, appId)

Sign Up

Creates a new user account in the Floor POD using **either a mobile number or an email ID**. At least **one of `mobile_number` or `email_id` is required** to register a user. Both may be provided if available. The API registers the user under the specified application context and prepares the account for subsequent authentication and usage. Upon successful registration, the API returns: - a unique user_id identifying the newly created user, and - a success string indicating the outcome of the sign-up operation. The user account is created under the specified application context and can be used for subsequent interactions with Floor POD APIs.

---

### **Parameter Clarification (Recommended)**
* `name` is mandatory for user profile creation
* Either `mobile_number` **or** `email_id` must be present * `app_id` is optional and used to associate the user with a specific application

### Example
```java
// Import classes:
import ai.xfloor.memory.client.ApiClient;
import ai.xfloor.memory.client.ApiException;
import ai.xfloor.memory.client.Configuration;
import ai.xfloor.memory.client.auth.*;
import ai.xfloor.memory.client.models.*;
import ai.xfloor.memory.api.DefaultApi;

public class Example {
  public static void main(String[] args) {
    ApiClient defaultClient = Configuration.getDefaultApiClient();
    defaultClient.setBasePath("https://appfloor.in");
    
    // Configure HTTP bearer authorization: bearer
    HttpBearerAuth bearer = (HttpBearerAuth) defaultClient.getAuthentication("bearer");
    bearer.setBearerToken("BEARER TOKEN");

    DefaultApi apiInstance = new DefaultApi(defaultClient);
    String name = "name_example"; // String | New User Name
    String password = "password_example"; // String | Password
    String emailId = "emailId_example"; // String | Email ID of the user
    String mobileNumber = "mobileNumber_example"; // String | Mobile number
    String appId = "appId_example"; // String | Registered App ID
    try {
      SignUp200Response result = apiInstance.signUp(name, password, emailId, mobileNumber, appId);
      System.out.println(result);
    } catch (ApiException e) {
      System.err.println("Exception when calling DefaultApi#signUp");
      System.err.println("Status code: " + e.getCode());
      System.err.println("Reason: " + e.getResponseBody());
      System.err.println("Response headers: " + e.getResponseHeaders());
      e.printStackTrace();
    }
  }
}
```

### Parameters

| Name | Type | Description | Notes |
|------------- | ------------- | ------------- | -------------|
| **name** | **String**| New User Name |
|
| **password** | **String**| Password |
|
| **emailId** | **String**| Email ID of the user | [optional] |
| **mobileNumber** | **String**| Mobile number | [optional] |
| **appId** | **String**| Registered App ID | [optional] |

### Return type

[**SignUp200Response**](SignUp200Response.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

 - **Content-Type**: multipart/form-data
 - **Accept**: application/json

### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** |
|
- |
| **400** |
|
- |

<a id="validateCode"></a>
# **validateCode**
> UserDetails validateCode(validateCodeRequest)

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
```java
// Import classes:
import ai.xfloor.memory.client.ApiClient;
import ai.xfloor.memory.client.ApiException;
import ai.xfloor.memory.client.Configuration;
import ai.xfloor.memory.client.auth.*;
import ai.xfloor.memory.client.models.*;
import ai.xfloor.memory.api.DefaultApi;

public class Example {
  public static void main(String[] args) {
    ApiClient defaultClient = Configuration.getDefaultApiClient();
    defaultClient.setBasePath("https://appfloor.in");
    
    // Configure HTTP bearer authorization: bearer
    HttpBearerAuth bearer = (HttpBearerAuth) defaultClient.getAuthentication("bearer");
    bearer.setBearerToken("BEARER TOKEN");

    DefaultApi apiInstance = new DefaultApi(defaultClient);
    ValidateCodeRequest validateCodeRequest = new ValidateCodeRequest(); // ValidateCodeRequest | 
    try {
      UserDetails result = apiInstance.validateCode(validateCodeRequest);
      System.out.println(result);
    } catch (ApiException e) {
      System.err.println("Exception when calling DefaultApi#validateCode");
      System.err.println("Status code: " + e.getCode());
      System.err.println("Reason: " + e.getResponseBody());
      System.err.println("Response headers: " + e.getResponseHeaders());
      e.printStackTrace();
    }
  }
}
```

### Parameters

| Name | Type | Description | Notes |
|------------- | ------------- | ------------- | -------------|
| **validateCodeRequest** | [**ValidateCodeRequest**](ValidateCodeRequest.md)|
| |

### Return type

[**UserDetails**](UserDetails.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json

### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** |
|
- |
| **400** |
|
- |
| **412** |
|
- |

