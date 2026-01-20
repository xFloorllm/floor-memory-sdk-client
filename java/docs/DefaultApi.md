# DefaultApi

All URIs are relative to *https://appfloor.in*

| Method | HTTP request | Description |
|------------- | ------------- | -------------|
| [**changeEmail**](DefaultApi.md#changeEmail) | **POST** /auth-service/change/email | Change email ID |
| [**changeMobileNumber**](DefaultApi.md#changeMobileNumber) | **POST** /auth-service/change/mobile | Change Mobile number |
| [**changePassword**](DefaultApi.md#changePassword) | **POST** /auth-service/change/password | Change Password |
| [**makeFloorPrivate**](DefaultApi.md#makeFloorPrivate) | **POST** /api/memory/make/floor/private | Make floor Private |
| [**makeFloorPublic**](DefaultApi.md#makeFloorPublic) | **POST** /api/memory/make/floor/public | Make floor public |
| [**registerExternalUserIdentity**](DefaultApi.md#registerExternalUserIdentity) | **POST** /memory/identity/external-user | External User Registration |
| [**renameFloor**](DefaultApi.md#renameFloor) | **POST** /api/memory/change/floor/id | Rename floor |
| [**sendSignInValidationCode**](DefaultApi.md#sendSignInValidationCode) | **POST** /auth-service/send/sign/in/validation/code | Send Sign-In Validation Code (OTP) |
| [**sendValidationCode**](DefaultApi.md#sendValidationCode) | **POST** /auth-service/send/validation/code | Send Validation code |
| [**signInWithEmail**](DefaultApi.md#signInWithEmail) | **POST** /auth-service/sign/in/with/email | Sign In with email ID |
| [**signInWithMobileNumber**](DefaultApi.md#signInWithMobileNumber) | **POST** /auth-service/sign/in/with/mobile/number | Sign In with Mobile number |
| [**signUp**](DefaultApi.md#signUp) | **POST** /auth-service/sign/up | Sign Up |
| [**validateCode**](DefaultApi.md#validateCode) | **POST** /auth-service/validate/activation/code | Validation |


<a id="changeEmail"></a>
# **changeEmail**
> Object changeEmail(newEmailId, activationCode)

Change email ID

Updates the email ID associated with an existing user account after validating a one-time activation code sent to the **new email address**.  This operation can only be performed by a **logged-in user**. When a user initiates an email change, an activation code is sent to the newly provided email ID. The email update takes effect only after the activation code is successfully validated.  If the activation code validation fails, the email ID remains unchanged.  ---  ### **Authentication**  This endpoint requires **Bearer Token authentication**.  &#x60;&#x60;&#x60; Authorization: Bearer &lt;access_token&gt; &#x60;&#x60;&#x60;  ---  ### **Request Body**  &#x60;&#x60;&#x60;json {   \&quot;user_id\&quot;: \&quot;string\&quot;,   \&quot;new_email_id\&quot;: \&quot;string\&quot;,   \&quot;activation_code\&quot;: \&quot;string\&quot;,   \&quot;app_id\&quot;:\&quot;string\&quot; } &#x60;&#x60;&#x60;  **Field Description**  * &#x60;user_id&#x60; – Unique identifier of the logged-in user * &#x60;new_email_id&#x60; – New email address to be associated with the account * &#x60;activation_code&#x60; – One-time activation code sent to the new email ID for verification  ---  ### **Flow Summary**  1. User is authenticated and logged in 2. User requests to change email ID 3. System sends an activation code to the **new email address** 4. User submits the activation code via this API 5. On successful validation, the email ID is updated  ---  ### **Successful Response**  On successful validation:  * The activation code is verified * The user’s email ID is updated immediately * A &#x60;success&#x60; string is returned confirming the email change  ---  ### **Error Response**  The API returns an error response if:  * The activation code is invalid or expired * The activation code does not match the user or email * The new email ID is already in use * Authorization fails or the bearer token is missing or invalid  In all error cases, the existing email ID remains unchanged.  --- ### **Behavior Notes**  * Requires a prior call to &#x60;/auth-service/send/validation/code&#x60; with the proper mode.  ---  ### **Security Notes (Recommended)**  * Activation codes are single-use and time-bound * Email changes require prior authentication * Rate limiting may be applied to prevent abuse  ---  ### **One-Line Summary**  &gt; Changes a user’s email ID after validating an activation code sent to the new email address. 

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

| Name | Type | Description  | Notes |
|------------- | ------------- | ------------- | -------------|
| **newEmailId** | **String**| New Email ID | |
| **activationCode** | **String**| Validation code | |

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
| **200** |  |  -  |
| **400** |  |  -  |

<a id="changeMobileNumber"></a>
# **changeMobileNumber**
> Object changeMobileNumber(body)

Change Mobile number

Updates the mobile number associated with an existing user account after validating a one-time activation code sent to the **new mobile number**.  This operation can only be performed by a **logged-in user**. When a user initiates a mobile number change, an activation code is sent to the newly provided mobile number. The mobile number update takes effect only after the activation code is successfully validated.  If the activation code validation fails, the mobile number remains unchanged.  ---  ### **Authentication**  This endpoint requires **Bearer Token authentication**.  &#x60;&#x60;&#x60; Authorization: Bearer &lt;access_token&gt; &#x60;&#x60;&#x60;  ---  ### **Request Body**  &#x60;&#x60;&#x60;json {   \&quot;user_id\&quot;: \&quot;string\&quot;,   \&quot;new_mobile_number\&quot;: \&quot;string\&quot;,   \&quot;activation_code\&quot;: \&quot;string\&quot; } &#x60;&#x60;&#x60;  **Field Description**  * &#x60;user_id&#x60; – Unique identifier of the logged-in user * &#x60;new_mobile_number&#x60; – New mobile number to be associated with the account * &#x60;activation_code&#x60; – One-time activation code sent to the new mobile number for verification  ---  ### **Flow Summary**  1. User is authenticated and logged in 2. User requests to change mobile number 3. System sends an activation code to the **new mobile number** 4. User submits the activation code via this API 5. On successful validation, the mobile number is updated  ---  ### **Successful Response**  On successful validation:  * The activation code is verified * The user’s mobile number is updated immediately * A &#x60;success&#x60; string is returned confirming the mobile number change  ---  ### **Error Response**  The API returns an error response if:  * The activation code is invalid or expired * The activation code does not match the user or mobile number * The new mobile number is already in use * Authorization fails or the bearer token is missing or invalid  In all error cases, the existing mobile number remains unchanged.  --- ### **Behavior Notes**  * Requires a prior call to &#x60;/auth-service/send/validation/code&#x60; with the proper mode. ---  ### **Security Notes (Recommended)**  * Activation codes are single-use and time-bound * Mobile number changes require prior authentication * Rate limiting may be applied to prevent abuse  ---  ### **One-Line Summary**  &gt; Changes a user’s mobile number after validating an activation code sent to the new mobile number.

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

| Name | Type | Description  | Notes |
|------------- | ------------- | ------------- | -------------|
| **body** | **Object**|  | |

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
| **200** |  |  -  |
| **400** |  |  -  |

<a id="changePassword"></a>
# **changePassword**
> ChangePassword200Response changePassword(userId, newPassword, acticationCode)

Change Password

Changes the password of an existing user after validating a one-time password change activation code.  This API validates the provided &#x60;activation_code&#x60; for the given &#x60;user_id&#x60;. If the activation code is valid and not expired, the user’s password is updated to the supplied &#x60;new_password&#x60; and takes effect immediately.  If the activation code validation fails, the password remains unchanged and an error response is returned.  ---  ### **Authentication**  This endpoint requires **Bearer Token authentication**.  &#x60;&#x60;&#x60; Authorization: Bearer &lt;access_token&gt; &#x60;&#x60;&#x60;  ---  ### **Request Body (Form Data)**  | Field        | Type          | Required | Description                                                       | | ------------ | ------------- | -------- | ----------------------------------------------------------------- | | &#x60;user_id&#x60; | string | Yes      | User ID | | &#x60;new_password&#x60; | string | Yes      | New Password | | &#x60;activation_code&#x60; | string | Yes      | Activation code |   **Field Description**  * &#x60;user_id&#x60; – Unique identifier of the user requesting the password change * &#x60;new_password&#x60; – New password to be set for the user * &#x60;activation_code&#x60; – One-time activation code generated for password change verification  ---  ### **Successful Response**  On successful validation:  * The activation code is verified * The user password is updated immediately * The API returns a &#x60;success&#x60; string indicating that the password change was completed  ---  ### **Error Response**  The API returns an error response if:  * The activation code is invalid or expired * The activation code does not match the specified user * The password does not meet security or policy requirements * Authorization fails or the bearer token is missing or invalid  In all error cases, the existing password remains unchanged.  --- ### **Behavior Notes**  * Requires a prior call to &#x60;/auth-service/send/validation/code&#x60; with the proper mode. ---  ### **Security Notes**  * Activation codes are single-use and time-bound * Passwords are never returned in API responses * Rate limiting may be applied to prevent brute-force attempts  ---  ### **One-Line Summary**  &gt; Updates a user’s password after validating a one-time activation code.  

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
    String userId = "userId_example"; // String | User ID
    String newPassword = "newPassword_example"; // String | New Password
    String acticationCode = "acticationCode_example"; // String | Validation code
    try {
      ChangePassword200Response result = apiInstance.changePassword(userId, newPassword, acticationCode);
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

| Name | Type | Description  | Notes |
|------------- | ------------- | ------------- | -------------|
| **userId** | **String**| User ID | [optional] |
| **newPassword** | **String**| New Password | [optional] |
| **acticationCode** | **String**| Validation code | [optional] |

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
| **200** |  |  -  |
| **400** |  |  -  |

<a id="makeFloorPrivate"></a>
# **makeFloorPrivate**
> GetFloorInformation200Response makeFloorPrivate(floorId, userId, appId)

Make floor Private

This API changes a floor’s visibility to **PRIVATE**.  It is used when a floor owner wants to **restrict access** to a floor that is currently public. After the update, the floor becomes private and is no longer accessible to non-authorized users (based on your platform’s access rules).  This endpoint is **state-changing**:  * If the floor is **PUBLIC**, it will be converted to **PRIVATE** * If the floor is already **PRIVATE**, the API returns success (idempotent) or an “already private” response depending on implementation  This API is commonly used in:  * Floor settings → “Privacy” toggle * Developer-managed pod workflows (app_id context) * Admin tools (if applicable)  ---  ## Request Method  &#x60;POST&#x60;  ---  ## Content-Type  &#x60;application/x-www-form-urlencoded&#x60; (or &#x60;multipart/form-data&#x60; if your system uses form-data) *(Document whichever you actually accept; below assumes standard form fields.)*  ---  ## Request Parameters (Form Fields)  | Field      | Type   | Required | Description                                                          | | ---------- | ------ | -------- | -------------------------------------------------------------------- | | &#x60;user_id&#x60;  | String | **Yes**  | User requesting the change. Must be the **owner** of the floor.      | | &#x60;floor_id&#x60; | String | **Yes**  | Public identifier of the floor to update.                            | | &#x60;app_id&#x60;   | String | No       | Calling application identifier (used for developer/pod integration). |  ---  ## Authorization Rules (Critical)  * The caller must be authenticated as &#x60;user_id&#x60; * **Only the floor owner** can change floor visibility * If the user is not the owner, the request must be rejected  ---  ## Behavior Rules  * Converts visibility from **PUBLIC → PRIVATE** * Does not modify floor content or blocks * Access enforcement for private floors is applied immediately after the change  **Idempotency**  * Calling this API multiple times should not cause repeated changes * If already private, the API should either:    * return success with a message like &#x60;\&quot;already private\&quot;&#x60;, or   * return a specific error/status indicating no-op  ---  ## Response Format  &#x60;application/json&#x60;  ---  ## Sample Success Response  *(Example — adjust to match your actual response format)*  &#x60;&#x60;&#x60;json {   \&quot;status\&quot;: \&quot;SUCCESS\&quot;,   \&quot;floor_id\&quot;: \&quot;my_floor\&quot;,   \&quot;visibility\&quot;: \&quot;PRIVATE\&quot;,   \&quot;message\&quot;: \&quot;Floor is now private\&quot; } &#x60;&#x60;&#x60;  ---  ## Sample No-Op Response (Already Private)  &#x60;&#x60;&#x60;json {   \&quot;status\&quot;: \&quot;SUCCESS\&quot;,   \&quot;floor_id\&quot;: \&quot;my_floor\&quot;,   \&quot;visibility\&quot;: \&quot;PRIVATE\&quot;,   \&quot;message\&quot;: \&quot;Floor is already private\&quot; } &#x60;&#x60;&#x60;  ---  ## Error Responses (Examples)  ### Not Authorized (Not Owner)  &#x60;&#x60;&#x60;json {   \&quot;status\&quot;: \&quot;ERROR\&quot;,   \&quot;message\&quot;: \&quot;Only the floor owner can change floor visibility\&quot; } &#x60;&#x60;&#x60;  ### Floor Not Found  &#x60;&#x60;&#x60;json {   \&quot;status\&quot;: \&quot;ERROR\&quot;,   \&quot;message\&quot;: \&quot;Floor not found\&quot; } &#x60;&#x60;&#x60;  ### Invalid Request  &#x60;&#x60;&#x60;json {   \&quot;status\&quot;: \&quot;ERROR\&quot;,   \&quot;message\&quot;: \&quot;user_id and floor_id are required\&quot; } &#x60;&#x60;&#x60;  ---  ## Notes  * This API is intended to control floor visibility only; membership/invite rules (for private floors) are handled elsewhere. * &#x60;app_id&#x60; is provided for developer/pod applications and is optional unless enforced by your app model. * If you support floor types like &#x60;POD&#x60;, document whether pods are allowed to be private or not (some platforms restrict this). 

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

| Name | Type | Description  | Notes |
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
| **200** |  |  -  |
| **400** |  |  -  |

<a id="makeFloorPublic"></a>
# **makeFloorPublic**
> GetFloorInformation200Response makeFloorPublic(floorId, userId, appId)

Make floor public

This API changes a floor’s visibility to **PUBLIC**.  It is used when a floor owner wants to **make a private floor accessible to everyone**. After the update, the floor becomes public and can be viewed and discovered by any user, subject to platform rules (search, feeds, pods, etc.).  This endpoint performs a **visibility state transition**:  * **PRIVATE → PUBLIC** * If the floor is already public, the operation is treated as **idempotent** (no state change).  This API is typically used from:  * Floor settings → Privacy / Visibility controls * Owner or admin tools * Developer or pod-based applications using &#x60;app_id&#x60;  ---  ## Request Method  &#x60;POST&#x60;  ---  ## Content-Type  &#x60;application/x-www-form-urlencoded&#x60; (or &#x60;multipart/form-data&#x60;, depending on your implementation)  ---  ## Request Parameters (Form Fields)  | Field      | Type   | Required | Description                                                                     | | ---------- | ------ | -------- | ------------------------------------------------------------------------------- | | &#x60;user_id&#x60;  | String | **Yes**  | User requesting the change. Must be the **owner** of the floor.                 | | &#x60;floor_id&#x60; | String | **Yes**  | Public identifier of the floor whose visibility is to be changed.               | | &#x60;app_id&#x60;   | String | No       | Identifier of the calling application (used mainly for pod/developer contexts). |  ---  ## Authorization Rules (Critical)  * The caller must be authenticated as &#x60;user_id&#x60; * **Only the floor owner** is allowed to change the floor’s visibility * Requests from non-owners must be rejected  ---  ## Behavior Rules  * Converts floor visibility from **PRIVATE → PUBLIC** * Does not modify floor content, blocks, or ownership * Visibility change takes effect immediately  ### Idempotency  * If the floor is already public, the API should:    * Return success with a message indicating no change, or   * Return a specific “already public” status (implementation-dependent)  ---  ## Response Format  &#x60;application/json&#x60;  ---  ## Sample Success Response  &#x60;&#x60;&#x60;json {   \&quot;status\&quot;: \&quot;SUCCESS\&quot;,   \&quot;floor_id\&quot;: \&quot;my_floor\&quot;,   \&quot;visibility\&quot;: \&quot;PUBLIC\&quot;,   \&quot;message\&quot;: \&quot;Floor is now public\&quot; } &#x60;&#x60;&#x60;  ---  ## Sample No-Op Response (Already Public)  &#x60;&#x60;&#x60;json {   \&quot;status\&quot;: \&quot;SUCCESS\&quot;,   \&quot;floor_id\&quot;: \&quot;my_floor\&quot;,   \&quot;visibility\&quot;: \&quot;PUBLIC\&quot;,   \&quot;message\&quot;: \&quot;Floor is already public\&quot; } &#x60;&#x60;&#x60;  ---  ## Error Responses (Examples)  ### Not Authorized (Not Owner)  &#x60;&#x60;&#x60;json {   \&quot;status\&quot;: \&quot;ERROR\&quot;,   \&quot;message\&quot;: \&quot;Only the floor owner can change floor visibility\&quot; } &#x60;&#x60;&#x60;  ---  ### Floor Not Found  &#x60;&#x60;&#x60;json {   \&quot;status\&quot;: \&quot;ERROR\&quot;,   \&quot;message\&quot;: \&quot;Floor not found\&quot; } &#x60;&#x60;&#x60;  ---  ### Invalid Request  &#x60;&#x60;&#x60;json {   \&quot;status\&quot;: \&quot;ERROR\&quot;,   \&quot;message\&quot;: \&quot;user_id and floor_id are required\&quot; } &#x60;&#x60;&#x60;  ---  ## Notes for Developers  * This API controls **visibility only**. Membership, invitations, and moderation rules are handled by separate APIs. * &#x60;app_id&#x60; is optional and primarily used for developer-managed or pod floors. * Clients should refresh floor metadata (e.g., via &#x60;/api/floor/info&#x60;) after a successful visibility change.  ---  ### Mental Model (One Line)  &gt; **This API answers: “Make this floor visible to everyone.”** 

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

| Name | Type | Description  | Notes |
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
| **200** |  |  -  |
| **400** |  |  -  |

<a id="registerExternalUserIdentity"></a>
# **registerExternalUserIdentity**
> SignInWithEmail200Response registerExternalUserIdentity(mobileNumber, emailId, name, appId)

External User Registration

This API allows a calling application to **pass externally authenticated user identity information to xfloor** after completing authentication within its own system.  xfloor **does not perform authentication, credential verification, or session management** as part of this API. The calling application is fully responsible for validating the user and ensuring the correctness of the identity data provided.  Upon invocation, xfloor will:  * **Create a new user profile** if no matching user exists, or * **Update the existing user profile** if the user is already present.  xfloor returns a unique &#x60;xfloor_user_id&#x60;, which serves as the **canonical user identifier** and must be used in all subsequent xfloor APIs, including floors, blocks, conversations, memory interactions, and analytics.

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

| Name | Type | Description  | Notes |
|------------- | ------------- | ------------- | -------------|
| **mobileNumber** | **String**|  | [optional] |
| **emailId** | **String**|  | [optional] |
| **name** | **String**|  | [optional] |
| **appId** | **String**|  | [optional] |

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
| **200** |  |  -  |

<a id="renameFloor"></a>
# **renameFloor**
> GetFloorInformation200Response renameFloor(userId, appId, from, to)

Rename floor

This API renames a floor by changing knowing the **floor identifier (floor_id)**.  It allows the **floor owner** to update the public-facing floor ID (slug/handle) from an old value to a new value. This is typically used when the owner wants to rebrand, reorganize, or correct the floor’s identifier.  ⚠️ **This operation affects how the floor is accessed and referenced externally**, so it must be performed carefully.  ---  ## Ownership &amp; Authorization (Critical)  * The caller **must be authenticated** * **Only the floor owner** is allowed to rename a floor * Members, followers, or non-owners **cannot** perform this operation * Ownership is validated internally using &#x60;user_id&#x60;  &gt; If the user is not the owner, the request must be rejected.  ---  ## Request Method  &#x60;POST&#x60;  ---  ## Content-Type  &#x60;application/x-www-form-urlencoded&#x60; (or equivalent form-data encoding)  ---  ## Request Parameters (Form Fields)  | Parameter | Type   | Required | Description                                                                     | | --------- | ------ | -------- | ------------------------------------------------------------------------------- | | &#x60;user_id&#x60; | String | **Yes**  | User requesting the rename. Must be the **owner** of the floor.                 | | &#x60;from&#x60;    | String | **Yes**  | Existing floor ID (current identifier to be renamed).                           | | &#x60;to&#x60;      | String | **Yes**  | New floor ID to assign to the floor.                                            | | &#x60;app_id&#x60;  | String | No       | Identifier of the calling application (used mainly for pod/developer contexts). |  ---  ## Rename Rules &amp; Constraints  * The &#x60;from&#x60; floor ID **must exist** * The &#x60;to&#x60; floor ID **must be unique** and not already in use * The rename operation updates **only the floor ID**    * Floor ownership, blocks, posts, and internal &#x60;fid&#x60; remain unchanged * Any links or references using the old floor ID may no longer be valid after rename  ---  ## Behavior Summary  | Scenario                     | Result                                            | | ---------------------------- | ------------------------------------------------- | | Valid owner + unique new ID  | Floor ID renamed successfully                     | | Non-owner user               | Request rejected                                  | | &#x60;from&#x60; floor ID not found    | Error                                             | | &#x60;to&#x60; floor ID already exists | Error                                             | | &#x60;from&#x60; &#x3D;&#x3D; &#x60;to&#x60;               | No-op or validation error (implementation choice) |  ---  ## Response Format  &#x60;application/json&#x60;  ---  ## Sample Success Response  &#x60;&#x60;&#x60;json {   \&quot;status\&quot;: \&quot;SUCCESS\&quot;,   \&quot;old_floor_id\&quot;: \&quot;oldfloorid\&quot;,   \&quot;new_floor_id\&quot;: \&quot;newfloorid\&quot;,   \&quot;message\&quot;: \&quot;Floor ID renamed successfully\&quot; } &#x60;&#x60;&#x60;  ---  ## Sample Error Responses  ### Not Floor Owner  &#x60;&#x60;&#x60;json {   \&quot;status\&quot;: \&quot;ERROR\&quot;,   \&quot;message\&quot;: \&quot;Only the floor owner can rename the floor\&quot; } &#x60;&#x60;&#x60;  ---  ### Floor Not Found  &#x60;&#x60;&#x60;json {   \&quot;status\&quot;: \&quot;ERROR\&quot;,   \&quot;message\&quot;: \&quot;Source floor ID does not exist\&quot; } &#x60;&#x60;&#x60;  ---  ### Floor ID Already Exists  &#x60;&#x60;&#x60;json {   \&quot;status\&quot;: \&quot;ERROR\&quot;,   \&quot;message\&quot;: \&quot;Target floor ID is already in use\&quot; } &#x60;&#x60;&#x60;  ---  ### Invalid Request  &#x60;&#x60;&#x60;json {   \&quot;status\&quot;: \&quot;ERROR\&quot;,   \&quot;message\&quot;: \&quot;user_id, from, and to are required\&quot; } &#x60;&#x60;&#x60;  ---  ## Notes for Developers  * This API **renames the public identifier only**; the internal immutable floor ID (&#x60;fid&#x60;) is not affected. * Clients should refresh cached floor metadata after a successful rename. * If your platform supports deep links or bookmarks, consider redirect or alias handling for old floor IDs (if supported).  ---  ### One-Line Mental Model  &gt; **This API answers: “Change the public identity (ID) of a floor, owner-only.”** 

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

| Name | Type | Description  | Notes |
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
| **200** |  |  -  |
| **400** |  |  -  |

<a id="sendSignInValidationCode"></a>
# **sendSignInValidationCode**
> SendSignInValidationCode200Response sendSignInValidationCode(appId, mobileNumber, emailId)

Send Sign-In Validation Code (OTP)

This API initiates the **sign-in validation process** by sending a **one-time validation code (OTP)** to the user.  The OTP is delivered to **either the mobile number or the email address** provided in the request. This endpoint is typically called **before completing sign-in**, to verify that the user owns the supplied contact identifier.  The calling application is responsible for:  * Collecting the OTP from the user * Submitting it to the OTP verification API (handled separately)  ---  ## **Use Case**  * User attempts to sign in * User provides **mobile number or email** * System sends a **validation code (OTP)** * User enters OTP to complete sign-in  ---  ## **Request Method**  &#x60;POST&#x60;  ---  ## **Formdata Parameters**  | Parameter Name  | Type   | Required  | Description                                 | | --------------- | ------ | --------- | ------------------------------------------- | | &#x60;mobile_number&#x60; | String | Optional* | Mobile number to which the OTP will be sent | | &#x60;email_id&#x60;      | String | Optional* | Email address to which the OTP will be sent | | &#x60;app_id&#x60;        | String | Optional  | Identifier of the calling application       |  * **Either &#x60;mobile_number&#x60; or &#x60;email_id&#x60; must be provided.** Providing both is allowed; the system may choose one based on configuration.  ---  ## **Request Rules**  * At least **one** of &#x60;mobile_number&#x60; or &#x60;email_id&#x60; is mandatory * If both are missing, the request will be rejected * OTP delivery channel depends on the provided identifier  ---  ## **Response Format**  &#x60;application/json&#x60;  ---  ## **Sample Success Response**  &#x60;&#x60;&#x60;json {   \&quot;status\&quot;: \&quot;SUCCESS\&quot;,   \&quot;message\&quot;: \&quot;Validation code sent successfully\&quot; } &#x60;&#x60;&#x60;  ---  ## **Sample Error Responses**  ### Missing Identifier  &#x60;&#x60;&#x60;json {   \&quot;status\&quot;: \&quot;ERROR\&quot;,   \&quot;message\&quot;: \&quot;Either mobile_number or email_id must be provided\&quot; } &#x60;&#x60;&#x60;  ### Invalid Identifier  &#x60;&#x60;&#x60;json {   \&quot;status\&quot;: \&quot;ERROR\&quot;,   \&quot;message\&quot;: \&quot;Invalid mobile number or email address\&quot; } &#x60;&#x60;&#x60;  ---  ## **Notes**  * This API **only sends** the validation code * OTP verification must be performed using the corresponding **verify validation code** API * Rate limiting and retry restrictions may apply to prevent abuse  

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
    String appId = "appId_example"; // String | App ID
    String mobileNumber = "mobileNumber_example"; // String | Mobile number
    String emailId = "emailId_example"; // String | Email ID
    try {
      SendSignInValidationCode200Response result = apiInstance.sendSignInValidationCode(appId, mobileNumber, emailId);
      System.out.println(result);
    } catch (ApiException e) {
      System.err.println("Exception when calling DefaultApi#sendSignInValidationCode");
      System.err.println("Status code: " + e.getCode());
      System.err.println("Reason: " + e.getResponseBody());
      System.err.println("Response headers: " + e.getResponseHeaders());
      e.printStackTrace();
    }
  }
}
```

### Parameters

| Name | Type | Description  | Notes |
|------------- | ------------- | ------------- | -------------|
| **appId** | **String**| App ID | |
| **mobileNumber** | **String**| Mobile number | [optional] |
| **emailId** | **String**| Email ID | [optional] |

### Return type

[**SendSignInValidationCode200Response**](SendSignInValidationCode200Response.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

 - **Content-Type**: multipart/form-data
 - **Accept**: application/json

### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** |  |  -  |
| **400** |  |  -  |

<a id="sendValidationCode"></a>
# **sendValidationCode**
> SendValidationCode200Response sendValidationCode(sendValidationCodeRequest)

Send Validation code

Generates and sends a one-time validation code to the user for verification of sensitive or critical account operations.  This API is used across multiple authentication and account-management flows. The validation code is delivered to the user via the appropriate channel (**email or mobile number**), based on the requested operation mode and the input provided.  The generated code is **time-bound**, **single-use**, and must be validated using the corresponding verification APIs to complete the requested action.  ---  ### **Usage Scenarios (Mode Definition)**  | Mode | Purpose                       | | ---- | ----------------------------- | | &#x60;0&#x60;  | Email or mobile number change | | &#x60;1&#x60;  | Password change               | | &#x60;2&#x60;  | Delete account                | | &#x60;3&#x60;  | Clear account                 | | &#x60;4&#x60;  | Signup Verification           |  **Mode &#x60;5&#x60; – Signup Verification** For login verification, the validation code is sent to **either the email ID or the mobile number provided in the request**. At least **one of email or mobile number must be supplied** for this mode.  ---  ### **Behavior**  * Generates a secure, one-time validation code * Sends the code to the appropriate channel:    * Email or mobile number, depending on the operation mode and input * Associates the code with:    * User identity (or login identifier)   * Requested operation (&#x60;mode&#x60;)   * Application context (if applicable) * Validation codes are valid for a limited duration and **cannot be reused**  ---  ### **Authentication**  This endpoint requires **Bearer Token authentication**, **except** where explicitly allowed (for example, login-related flows).  &#x60;&#x60;&#x60; Authorization: Bearer &lt;access_token&gt; &#x60;&#x60;&#x60;  ---  ### **Successful Response**  On success, the API confirms that the validation code has been generated and successfully dispatched to the user.  ---  ### **Error Response**  The API returns an error response if:  * The user does not exist or is not eligible for the requested operation * The requested mode is invalid or unsupported * Required identifiers (email or mobile number for login verification) are missing * Rate limits are exceeded * Authorization fails (where applicable)  ---  ### **Security Notes (Recommended)**  * Validation codes are single-use and time-bound * Rate limiting is enforced to prevent abuse * Repeated failures may trigger temporary blocking or additional verification  ---  ### **One-Line Summary**  &gt; Sends a one-time validation code for secure account and authentication operations, including login via email or mobile number.

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

| Name | Type | Description  | Notes |
|------------- | ------------- | ------------- | -------------|
| **sendValidationCodeRequest** | [**SendValidationCodeRequest**](SendValidationCodeRequest.md)|  | |

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
| **200** |  |  -  |
| **400** |  |  -  |

<a id="signInWithEmail"></a>
# **signInWithEmail**
> SignInWithEmail200Response signInWithEmail(emailId, passCode, loginType, appId)

Sign In with email ID

Authenticates a user using a registered email ID. The authentication mechanism is determined by the specified &#x60;mode&#x60;.  * When &#x60;login_type&#x60; is set to **&#x60;1&#x60;**, the user is authenticated using the provided **password**. * When &#x60;login_type&#x60; is set to **&#x60;2&#x60;**, the user is authenticated using a **one-time activation code (OTP)**.  For OTP-based authentication (&#x60;login_type &#x3D; 2&#x60;), the client **must first invoke the Send Validation Code API** with the appropriate login mode to generate and deliver the activation code to the user.  --- ### **Request Body**  | Field        | Type          | Required | Description                                                       | | ------------ | ------------- | -------- | ----------------------------------------------------------------- | | &#x60;email_id&#x60; | string | Yes      | Email ID | | &#x60;pass_code&#x60; | string | Yes      | Password/Validation code depending on the login_type| | &#x60;login_type&#x60; | string | Yes      | login type 1 for password 2 for validation code|   |&#x60;app_id&#x60; | string | Yes      | App ID |     **Field Description**  * &#x60;email_id&#x60; – Registered email address of the user * &#x60;pass_code&#x60; – password or activation code  (this is password if it is 1 and 2 it is validation code) * &#x60;app_id&#x60; - App ID which is a 13 digit numeric value * &#x60;login_type&#x60; – Login type   * &#x60;1&#x60; → Password-based login   * &#x60;2&#x60; → Activation code (OTP)–based login  ---  ### **Behavior Notes**  * When &#x60;login_type &#x3D; 2&#x60;, password validation is bypassed. * OTP-based login requires a prior call to &#x60; /auth-service/send/sign/in/validation/code&#x60;. * If the required credentials for the selected mode are missing or invalid, authentication fails.  ---  ### **Successful Response**  On successful authentication, the user is signed in and a success response is returned as per the authentication flow.  ---  ### **Error Response**  The API returns an error response if:  * The email ID is not registered * The password is incorrect (&#x60;login_type &#x3D; 1 &#x60;) * The activation code is missing, invalid, or expired (&#x60;login_type &#x3D; 2&#x60;) * The mode value is invalid or unsupported  ---  ### **One-Line Summary**  &gt; Signs in a user using an email ID with either password-based or OTP-based authentication, based on the selected mode.  

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

| Name | Type | Description  | Notes |
|------------- | ------------- | ------------- | -------------|
| **emailId** | **String**| Email ID | |
| **passCode** | **String**| Validation code or password depends on the login_type | |
| **loginType** | **String**| 1 is for password, 2 is for validation code | |
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
| **200** |  |  -  |
| **400** |  |  -  |

<a id="signInWithMobileNumber"></a>
# **signInWithMobileNumber**
> SignInWithEmail200Response signInWithMobileNumber(body)

Sign In with Mobile number

Authenticates a user using a registered mobile number. The authentication method is determined by the specified &#x60;mode&#x60;.  * When &#x60;login_type&#x60; is set to **&#x60;1&#x60;**, the user is authenticated using the **password** associated with the account. * When &#x60;login_type&#x60; is set to **&#x60;2&#x60;**, the user is authenticated using a **one-time activation code (OTP)** sent to the registered mobile number.  For OTP-based authentication (&#x60;login_type &#x3D; 1&#x60;), the client **must first call the Send Validation Code API** with the appropriate login mode to generate and deliver the activation code.  ---  ### **Request Formdata**  | Field        | Type          | Required | Description                                                       | | ------------ | ------------- | -------- | ----------------------------------------------------------------- | | &#x60;mobile_number&#x60; | string | Yes      | Mobile number| | &#x60;pass_code&#x60; | string | Yes      | Password/Validation code depending on the login_type| | &#x60;login_type&#x60; | string | Yes      | login type 1 for password 2 for validation code|   |&#x60;app_id&#x60; | string | Yes      | App ID |    **Field Description**  * &#x60;mobile_number&#x60; – Registered mobile number of the user * &#x60;pass_code&#x60; – Password / Validation code (password when &#x60;login_type&#x3D; 1&#x60;; validation code when &#x60;login_type &#x3D; 2&#x60;) * &#x60;login_type&#x60; – Login type    * &#x60;1&#x60; → Password-based login   * &#x60;2&#x60; → Activation code (OTP)–based login  ---  ### **Behavior Notes**  * When &#x60;login_type &#x3D; 2&#x60;, password validation is skipped. * OTP-based login requires a prior call to &#x60;/auth-service/send/sign/in/validation/code&#x60;. * Missing or invalid credentials for the selected mode will result in authentication failure.  ---  ### **Successful Response**  On successful authentication, the user is signed in and a success response is returned according to the authentication flow.  ---  ### **Error Response**  The API returns an error response if:  * The mobile number is not registered * The password is incorrect (&#x60;login_type &#x3D; 1&#x60;) * The activation code is missing, invalid, or expired (&#x60;login_type &#x3D; 2&#x60;) * An invalid or unsupported mode is provided  ---  ### **One-Line Summary**  &gt; Signs in a user using a mobile number with either password-based or OTP-based authentication, based on the selected mode.

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

| Name | Type | Description  | Notes |
|------------- | ------------- | ------------- | -------------|
| **body** | **Object**|  | |

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
| **200** |  |  -  |
| **400** |  |  -  |

<a id="signUp"></a>
# **signUp**
> SignUp200Response signUp(name, password, emailId, mobileNumber, appId)

Sign Up

Creates a new user account in the Floor POD using **either a mobile number or an email ID**. At least **one of &#x60;mobile_number&#x60; or &#x60;email_id&#x60; is required** to register a user. Both may be provided if available.  The API registers the user under the specified application context and prepares the account for subsequent authentication and usage.  Upon successful registration, the API returns: - a unique user_id identifying the newly created user, and - a success string indicating the outcome of the sign-up operation. The user account is created under the specified application context and can be used for subsequent interactions with Floor POD APIs.  ---  ### **Parameter Clarification (Recommended)**  * &#x60;name&#x60; is mandatory for user profile creation * Either &#x60;mobile_number&#x60; **or** &#x60;email_id&#x60; must be present * &#x60;app_id&#x60; is optional and used to associate the user with a specific application   

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

| Name | Type | Description  | Notes |
|------------- | ------------- | ------------- | -------------|
| **name** | **String**| New User Name | |
| **password** | **String**| Password | |
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
| **200** |  |  -  |
| **400** |  |  -  |

<a id="validateCode"></a>
# **validateCode**
> UserDetails validateCode(validateCodeRequest)

Validation

Validates the activation code submitted by a newly registered user and completes the account activation process.  This API verifies the provided &#x60;activation_code&#x60; against the specified &#x60;user_id&#x60; and activation &#x60;mode&#x60; (e.g., email or mobile). Upon successful validation, the user account is activated and the API returns the associated **POD information** along with the user’s **profile details**.  If the activation code is invalid, expired, or does not match the user context, the API returns an appropriate error response and the account remains inactive.  ---  ### **Authentication**  This endpoint requires **Bearer Token authentication**.  * The token must be included in the &#x60;Authorization&#x60; header:    &#x60;&#x60;&#x60;   Authorization: Bearer &lt;access_token&gt;   &#x60;&#x60;&#x60;  ---  ### **Request Body**  &#x60;&#x60;&#x60;json {   \&quot;user_id\&quot;: \&quot;string\&quot;,   \&quot;activation_code\&quot;: \&quot;string\&quot;,   \&quot;app_id\&quot;: \&quot;string\&quot;,   \&quot;mode\&quot;: \&quot;string\&quot; } &#x60;&#x60;&#x60;  **Field Description**  * &#x60;user_id&#x60; – Unique identifier of the newly registered user * &#x60;activation_code&#x60; – One-time validation code sent to the user * &#x60;app_id&#x60; – Application identifier (optional or context-specific) * &#x60;mode&#x60; – Activation channel used (e.g., &#x60;email&#x60;, &#x60;mobile&#x60;)  --- ### **Usage Scenarios (Mode Definition)**  | Mode | Purpose                       | | ---- | ----------------------------- | | &#x60;0&#x60;  | Email or mobile number change | | &#x60;1&#x60;  | Password change               | | &#x60;2&#x60;  | Delete account                | | &#x60;3&#x60;  | Clear account                 | | &#x60;5&#x60;  | Login verification            |  ### **Successful Response**  On successful validation:  * The user account is activated * The API returns:    * &#x60;pod_info&#x60; associated with the user   * User &#x60;profile&#x60; information  The activated account can now be used for login and other Floor POD operations.  ---  ### **Error Response**  The API returns an error response when:  * The activation code is invalid or expired * The activation code does not match the user or mode * The user is already activated * Authorization fails or the bearer token is missing/invalid  In all error cases, **account activation is not completed**.  ---  ### **One-Line Summary**  &gt; Validates a user’s activation code, activates the account, and returns POD and profile details on success.  

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

| Name | Type | Description  | Notes |
|------------- | ------------- | ------------- | -------------|
| **validateCodeRequest** | [**ValidateCodeRequest**](ValidateCodeRequest.md)|  | |

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
| **200** |  |  -  |
| **400** |  |  -  |
| **412** |  |  -  |

