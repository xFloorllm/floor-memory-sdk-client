# xfloor_memory_sdk.DefaultApi

All URIs are relative to *https://appfloor.in*

Method | HTTP request | Description
------------- | ------------- | -------------
[**change_email**](DefaultApi.md#change_email) | **POST** /auth-service/change/email | Change email ID
[**change_mobile_number**](DefaultApi.md#change_mobile_number) | **POST** /auth-service/change/mobile | Change Mobile number
[**change_password**](DefaultApi.md#change_password) | **POST** /auth-service/password/change | Change Password
[**make_floor_private**](DefaultApi.md#make_floor_private) | **POST** /api/memory/make/floor/private | Make floor Private
[**make_floor_public**](DefaultApi.md#make_floor_public) | **POST** /api/memory/make/floor/public | Make floor public
[**register_external_user_identity**](DefaultApi.md#register_external_user_identity) | **POST** /memory/identity/external-user | External User Registration
[**rename_floor**](DefaultApi.md#rename_floor) | **POST** /api/memory/change/floor/id | Rename floor
[**reset_password**](DefaultApi.md#reset_password) | **POST** /auth-service/password/reset | Reset Password
[**send_validation_code**](DefaultApi.md#send_validation_code) | **POST** /auth-service/send/validation/code | Send Validation code
[**sign_in_with_email**](DefaultApi.md#sign_in_with_email) | **POST** /auth-service/sign/in/with/email | Sign In with email ID
[**sign_in_with_mobile_number**](DefaultApi.md#sign_in_with_mobile_number) | **POST** /auth-service/sign/in/with/mobile/number | Sign In with Mobile number
[**sign_up**](DefaultApi.md#sign_up) | **POST** /auth-service/sign/up | Sign Up
[**validate_code**](DefaultApi.md#validate_code) | **POST** /auth-service/validate/activation/code | Validation


# **change_email**
> object change_email(new_email_id, activation_code)

Change email ID

Updates the email ID associated with an existing user account after validating a one-time activation code sent to the **new email address**.

This operation can only be performed by a **logged-in user**. When a user initiates an email change, an activation code is sent to the newly provided email ID. The email update takes effect only after the activation code is successfully validated.

If the activation code validation fails, the email ID remains unchanged.

---

### **Authentication**

This endpoint requires **Bearer Token authentication**.

```
Authorization: Bearer <access_token>
```

---

### **Request Body**

```json
{
  "user_id": "string",
  "new_email_id": "string",
  "activation_code": "string",
  "app_id":"string"
}
```

**Field Description**

* `user_id` – Unique identifier of the logged-in user
* `new_email_id` – New email address to be associated with the account
* `activation_code` – One-time activation code sent to the new email ID for verification

---

### **Flow Summary**

1. User is authenticated and logged in
2. User requests to change email ID
3. System sends an activation code to the **new email address**
4. User submits the activation code via this API
5. On successful validation, the email ID is updated

---

### **Successful Response**

On successful validation:

* The activation code is verified
* The user’s email ID is updated immediately
* A `success` string is returned confirming the email change

---

### **Error Response**

The API returns an error response if:

* The activation code is invalid or expired
* The activation code does not match the user or email
* The new email ID is already in use
* Authorization fails or the bearer token is missing or invalid

In all error cases, the existing email ID remains unchanged.

---
### **Behavior Notes**

* Requires a prior call to `/auth-service/send/validation/code` with the proper mode.

---

### **Security Notes (Recommended)**

* Activation codes are single-use and time-bound
* Email changes require prior authentication
* Rate limiting may be applied to prevent abuse

---

### **One-Line Summary**

> Changes a user’s email ID after validating an activation code sent to the new email address.


### Example

* Bearer Authentication (bearer):

```python
import xfloor_memory_sdk
from xfloor_memory_sdk.rest import ApiException
from pprint import pprint

# Defining the host is optional and defaults to https://appfloor.in
# See configuration.py for a list of all supported configuration parameters.
configuration = xfloor_memory_sdk.Configuration(
    host = "https://appfloor.in"
)

# The client must configure the authentication and authorization parameters
# in accordance with the API server security policy.
# Examples for each auth method are provided below, use the example that
# satisfies your auth use case.

# Configure Bearer authorization: bearer
configuration = xfloor_memory_sdk.Configuration(
    access_token = os.environ["BEARER_TOKEN"]
)

# Enter a context with an instance of the API client
with xfloor_memory_sdk.ApiClient(configuration) as api_client:
    # Create an instance of the API class
    api_instance = xfloor_memory_sdk.DefaultApi(api_client)
    new_email_id = 'new_email_id_example' # str | New Email ID
    activation_code = 'activation_code_example' # str | Validation code

    try:
        # Change email ID
        api_response = api_instance.change_email(new_email_id, activation_code)
        print("The response of DefaultApi->change_email:\n")
        pprint(api_response)
    except Exception as e:
        print("Exception when calling DefaultApi->change_email: %s\n" % e)
```



### Parameters


Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **new_email_id** | **str**| New Email ID | 
 **activation_code** | **str**| Validation code | 

### Return type

**object**

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

 - **Content-Type**: multipart/form-data
 - **Accept**: application/json

### HTTP response details

| Status code | Description | Response headers |
|-------------|-------------|------------------|
**200** |  |  -  |
**400** |  |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **change_mobile_number**
> object change_mobile_number(body)

Change Mobile number

Updates the mobile number associated with an existing user account after validating a one-time activation code sent to the **new mobile number**.

This operation can only be performed by a **logged-in user**. When a user initiates a mobile number change, an activation code is sent to the newly provided mobile number. The mobile number update takes effect only after the activation code is successfully validated.

If the activation code validation fails, the mobile number remains unchanged.

---

### **Authentication**

This endpoint requires **Bearer Token authentication**.

```
Authorization: Bearer <access_token>
```

---

### **Request Body**

```json
{
  "user_id": "string",
  "new_mobile_number": "string",
  "activation_code": "string"
}
```

**Field Description**

* `user_id` – Unique identifier of the logged-in user
* `new_mobile_number` – New mobile number to be associated with the account
* `activation_code` – One-time activation code sent to the new mobile number for verification

---

### **Flow Summary**

1. User is authenticated and logged in
2. User requests to change mobile number
3. System sends an activation code to the **new mobile number**
4. User submits the activation code via this API
5. On successful validation, the mobile number is updated

---

### **Successful Response**

On successful validation:

* The activation code is verified
* The user’s mobile number is updated immediately
* A `success` string is returned confirming the mobile number change

---

### **Error Response**

The API returns an error response if:

* The activation code is invalid or expired
* The activation code does not match the user or mobile number
* The new mobile number is already in use
* Authorization fails or the bearer token is missing or invalid

In all error cases, the existing mobile number remains unchanged.

---
### **Behavior Notes**

* Requires a prior call to `/auth-service/send/validation/code` with the proper mode.
---

### **Security Notes (Recommended)**

* Activation codes are single-use and time-bound
* Mobile number changes require prior authentication
* Rate limiting may be applied to prevent abuse

---

### **One-Line Summary**

> Changes a user’s mobile number after validating an activation code sent to the new mobile number.

### Example

* Bearer Authentication (bearer):

```python
import xfloor_memory_sdk
from xfloor_memory_sdk.rest import ApiException
from pprint import pprint

# Defining the host is optional and defaults to https://appfloor.in
# See configuration.py for a list of all supported configuration parameters.
configuration = xfloor_memory_sdk.Configuration(
    host = "https://appfloor.in"
)

# The client must configure the authentication and authorization parameters
# in accordance with the API server security policy.
# Examples for each auth method are provided below, use the example that
# satisfies your auth use case.

# Configure Bearer authorization: bearer
configuration = xfloor_memory_sdk.Configuration(
    access_token = os.environ["BEARER_TOKEN"]
)

# Enter a context with an instance of the API client
with xfloor_memory_sdk.ApiClient(configuration) as api_client:
    # Create an instance of the API class
    api_instance = xfloor_memory_sdk.DefaultApi(api_client)
    body = None # object | 

    try:
        # Change Mobile number
        api_response = api_instance.change_mobile_number(body)
        print("The response of DefaultApi->change_mobile_number:\n")
        pprint(api_response)
    except Exception as e:
        print("Exception when calling DefaultApi->change_mobile_number: %s\n" % e)
```



### Parameters


Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **body** | **object**|  | 

### Return type

**object**

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json

### HTTP response details

| Status code | Description | Response headers |
|-------------|-------------|------------------|
**200** |  |  -  |
**400** |  |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **change_password**
> ChangePassword200Response change_password(new_password, activation_code, user_id=user_id)

Change Password

## 1) `POST /password/change` — Change Password (Logged-in User)

Changes the password of an **authenticated user** who is currently logged in.

This endpoint is used when a user is already signed in and wants to update their password as a security or preference action. The system validates a **one-time password-change verification code** (`activation_code`) issued specifically for the change-password flow. If the code is valid and not expired, the user’s password is updated to `new_password` and takes effect immediately.

If verification fails, the password remains unchanged and an error response is returned.

### Authentication

✅ **Required**: Bearer token for the logged-in session

```
Authorization: Bearer <access_token>
```

### Request Body (Form Data)

* `user_id` (optional if derived from token)
* `activation_code` (required)
* `new_password` (required)

### Behavior Notes

* Typically requires a prior call to **send a verification code** for password change (mode = password change).
* `user_id` can be taken from the access token; include it only if your system requires it explicitly.

### One-Line Summary

> Changes the password for a logged-in user after validating a one-time password-change code.


### Example

* Bearer Authentication (bearer):

```python
import xfloor_memory_sdk
from xfloor_memory_sdk.models.change_password200_response import ChangePassword200Response
from xfloor_memory_sdk.rest import ApiException
from pprint import pprint

# Defining the host is optional and defaults to https://appfloor.in
# See configuration.py for a list of all supported configuration parameters.
configuration = xfloor_memory_sdk.Configuration(
    host = "https://appfloor.in"
)

# The client must configure the authentication and authorization parameters
# in accordance with the API server security policy.
# Examples for each auth method are provided below, use the example that
# satisfies your auth use case.

# Configure Bearer authorization: bearer
configuration = xfloor_memory_sdk.Configuration(
    access_token = os.environ["BEARER_TOKEN"]
)

# Enter a context with an instance of the API client
with xfloor_memory_sdk.ApiClient(configuration) as api_client:
    # Create an instance of the API class
    api_instance = xfloor_memory_sdk.DefaultApi(api_client)
    new_password = 'new_password_example' # str | New Password
    activation_code = 'activation_code_example' # str | Validation code
    user_id = 'user_id_example' # str | User ID (optional)

    try:
        # Change Password
        api_response = api_instance.change_password(new_password, activation_code, user_id=user_id)
        print("The response of DefaultApi->change_password:\n")
        pprint(api_response)
    except Exception as e:
        print("Exception when calling DefaultApi->change_password: %s\n" % e)
```



### Parameters


Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **new_password** | **str**| New Password | 
 **activation_code** | **str**| Validation code | 
 **user_id** | **str**| User ID | [optional] 

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
**200** |  |  -  |
**400** |  |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **make_floor_private**
> GetFloorInformation200Response make_floor_private(floor_id=floor_id, user_id=user_id, app_id=app_id)

Make floor Private

This API changes a floor’s visibility to **PRIVATE**.

It is used when a floor owner wants to **restrict access** to a floor that is currently public. After the update, the floor becomes private and is no longer accessible to non-authorized users (based on your platform’s access rules).

This endpoint is **state-changing**:

* If the floor is **PUBLIC**, it will be converted to **PRIVATE**
* If the floor is already **PRIVATE**, the API returns success (idempotent) or an “already private” response depending on implementation

This API is commonly used in:

* Floor settings → “Privacy” toggle
* Developer-managed pod workflows (app_id context)
* Admin tools (if applicable)

---

## Request Method

`POST`

---

## Content-Type

`application/x-www-form-urlencoded` (or `multipart/form-data` if your system uses form-data)
*(Document whichever you actually accept; below assumes standard form fields.)*

---

## Request Parameters (Form Fields)

| Field      | Type   | Required | Description                                                          |
| ---------- | ------ | -------- | -------------------------------------------------------------------- |
| `user_id`  | String | **Yes**  | User requesting the change. Must be the **owner** of the floor.      |
| `floor_id` | String | **Yes**  | Public identifier of the floor to update.                            |
| `app_id`   | String | No       | Calling application identifier (used for developer/pod integration). |

---

## Authorization Rules (Critical)

* The caller must be authenticated as `user_id`
* **Only the floor owner** can change floor visibility
* If the user is not the owner, the request must be rejected

---

## Behavior Rules

* Converts visibility from **PUBLIC → PRIVATE**
* Does not modify floor content or blocks
* Access enforcement for private floors is applied immediately after the change

**Idempotency**

* Calling this API multiple times should not cause repeated changes
* If already private, the API should either:

  * return success with a message like `"already private"`, or
  * return a specific error/status indicating no-op

---

## Response Format

`application/json`

---

## Sample Success Response

*(Example — adjust to match your actual response format)*

```json
{
  "status": "SUCCESS",
  "floor_id": "my_floor",
  "visibility": "PRIVATE",
  "message": "Floor is now private"
}
```

---

## Sample No-Op Response (Already Private)

```json
{
  "status": "SUCCESS",
  "floor_id": "my_floor",
  "visibility": "PRIVATE",
  "message": "Floor is already private"
}
```

---

## Error Responses (Examples)

### Not Authorized (Not Owner)

```json
{
  "status": "ERROR",
  "message": "Only the floor owner can change floor visibility"
}
```

### Floor Not Found

```json
{
  "status": "ERROR",
  "message": "Floor not found"
}
```

### Invalid Request

```json
{
  "status": "ERROR",
  "message": "user_id and floor_id are required"
}
```

---

## Notes

* This API is intended to control floor visibility only; membership/invite rules (for private floors) are handled elsewhere.
* `app_id` is provided for developer/pod applications and is optional unless enforced by your app model.
* If you support floor types like `POD`, document whether pods are allowed to be private or not (some platforms restrict this).


### Example

* Bearer Authentication (bearer):

```python
import xfloor_memory_sdk
from xfloor_memory_sdk.models.get_floor_information200_response import GetFloorInformation200Response
from xfloor_memory_sdk.rest import ApiException
from pprint import pprint

# Defining the host is optional and defaults to https://appfloor.in
# See configuration.py for a list of all supported configuration parameters.
configuration = xfloor_memory_sdk.Configuration(
    host = "https://appfloor.in"
)

# The client must configure the authentication and authorization parameters
# in accordance with the API server security policy.
# Examples for each auth method are provided below, use the example that
# satisfies your auth use case.

# Configure Bearer authorization: bearer
configuration = xfloor_memory_sdk.Configuration(
    access_token = os.environ["BEARER_TOKEN"]
)

# Enter a context with an instance of the API client
with xfloor_memory_sdk.ApiClient(configuration) as api_client:
    # Create an instance of the API class
    api_instance = xfloor_memory_sdk.DefaultApi(api_client)
    floor_id = 'floor_id_example' # str | Floor ID (optional)
    user_id = 'user_id_example' # str | User ID (optional)
    app_id = 'app_id_example' # str | App ID (optional)

    try:
        # Make floor Private
        api_response = api_instance.make_floor_private(floor_id=floor_id, user_id=user_id, app_id=app_id)
        print("The response of DefaultApi->make_floor_private:\n")
        pprint(api_response)
    except Exception as e:
        print("Exception when calling DefaultApi->make_floor_private: %s\n" % e)
```



### Parameters


Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **floor_id** | **str**| Floor ID | [optional] 
 **user_id** | **str**| User ID | [optional] 
 **app_id** | **str**| App ID | [optional] 

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
**200** |  |  -  |
**400** |  |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **make_floor_public**
> GetFloorInformation200Response make_floor_public(floor_id=floor_id, user_id=user_id, app_id=app_id)

Make floor public

This API changes a floor’s visibility to **PUBLIC**.

It is used when a floor owner wants to **make a private floor accessible to everyone**. After the update, the floor becomes public and can be viewed and discovered by any user, subject to platform rules (search, feeds, pods, etc.).

This endpoint performs a **visibility state transition**:

* **PRIVATE → PUBLIC**
* If the floor is already public, the operation is treated as **idempotent** (no state change).

This API is typically used from:

* Floor settings → Privacy / Visibility controls
* Owner or admin tools
* Developer or pod-based applications using `app_id`

---

## Request Method

`POST`

---

## Content-Type

`application/x-www-form-urlencoded`
(or `multipart/form-data`, depending on your implementation)

---

## Request Parameters (Form Fields)

| Field      | Type   | Required | Description                                                                     |
| ---------- | ------ | -------- | ------------------------------------------------------------------------------- |
| `user_id`  | String | **Yes**  | User requesting the change. Must be the **owner** of the floor.                 |
| `floor_id` | String | **Yes**  | Public identifier of the floor whose visibility is to be changed.               |
| `app_id`   | String | No       | Identifier of the calling application (used mainly for pod/developer contexts). |

---

## Authorization Rules (Critical)

* The caller must be authenticated as `user_id`
* **Only the floor owner** is allowed to change the floor’s visibility
* Requests from non-owners must be rejected

---

## Behavior Rules

* Converts floor visibility from **PRIVATE → PUBLIC**
* Does not modify floor content, blocks, or ownership
* Visibility change takes effect immediately

### Idempotency

* If the floor is already public, the API should:

  * Return success with a message indicating no change, or
  * Return a specific “already public” status (implementation-dependent)

---

## Response Format

`application/json`

---

## Sample Success Response

```json
{
  "status": "SUCCESS",
  "floor_id": "my_floor",
  "visibility": "PUBLIC",
  "message": "Floor is now public"
}
```

---

## Sample No-Op Response (Already Public)

```json
{
  "status": "SUCCESS",
  "floor_id": "my_floor",
  "visibility": "PUBLIC",
  "message": "Floor is already public"
}
```

---

## Error Responses (Examples)

### Not Authorized (Not Owner)

```json
{
  "status": "ERROR",
  "message": "Only the floor owner can change floor visibility"
}
```

---

### Floor Not Found

```json
{
  "status": "ERROR",
  "message": "Floor not found"
}
```

---

### Invalid Request

```json
{
  "status": "ERROR",
  "message": "user_id and floor_id are required"
}
```

---

## Notes for Developers

* This API controls **visibility only**. Membership, invitations, and moderation rules are handled by separate APIs.
* `app_id` is optional and primarily used for developer-managed or pod floors.
* Clients should refresh floor metadata (e.g., via `/api/floor/info`) after a successful visibility change.

---

### Mental Model (One Line)

> **This API answers: “Make this floor visible to everyone.”**


### Example

* Bearer Authentication (bearer):

```python
import xfloor_memory_sdk
from xfloor_memory_sdk.models.get_floor_information200_response import GetFloorInformation200Response
from xfloor_memory_sdk.rest import ApiException
from pprint import pprint

# Defining the host is optional and defaults to https://appfloor.in
# See configuration.py for a list of all supported configuration parameters.
configuration = xfloor_memory_sdk.Configuration(
    host = "https://appfloor.in"
)

# The client must configure the authentication and authorization parameters
# in accordance with the API server security policy.
# Examples for each auth method are provided below, use the example that
# satisfies your auth use case.

# Configure Bearer authorization: bearer
configuration = xfloor_memory_sdk.Configuration(
    access_token = os.environ["BEARER_TOKEN"]
)

# Enter a context with an instance of the API client
with xfloor_memory_sdk.ApiClient(configuration) as api_client:
    # Create an instance of the API class
    api_instance = xfloor_memory_sdk.DefaultApi(api_client)
    floor_id = 'floor_id_example' # str | Floor ID (optional)
    user_id = 'user_id_example' # str | User ID (optional)
    app_id = 'app_id_example' # str | App ID (optional)

    try:
        # Make floor public
        api_response = api_instance.make_floor_public(floor_id=floor_id, user_id=user_id, app_id=app_id)
        print("The response of DefaultApi->make_floor_public:\n")
        pprint(api_response)
    except Exception as e:
        print("Exception when calling DefaultApi->make_floor_public: %s\n" % e)
```



### Parameters


Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **floor_id** | **str**| Floor ID | [optional] 
 **user_id** | **str**| User ID | [optional] 
 **app_id** | **str**| App ID | [optional] 

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
**200** |  |  -  |
**400** |  |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **register_external_user_identity**
> SignInWithEmail200Response register_external_user_identity(mobile_number=mobile_number, email_id=email_id, name=name, app_id=app_id)

External User Registration

This API allows a calling application to **pass externally authenticated user identity information to xfloor** after completing authentication within its own system.

xfloor **does not perform authentication, credential verification, or session management** as part of this API. The calling application is fully responsible for validating the user and ensuring the correctness of the identity data provided.

Upon invocation, xfloor will:

* **Create a new user profile** if no matching user exists, or
* **Update the existing user profile** if the user is already present.

xfloor returns a unique `xfloor_user_id`, which serves as the **canonical user identifier** and must be used in all subsequent xfloor APIs, including floors, blocks, conversations, memory interactions, and analytics.

### Example

* Bearer Authentication (bearer):

```python
import xfloor_memory_sdk
from xfloor_memory_sdk.models.sign_in_with_email200_response import SignInWithEmail200Response
from xfloor_memory_sdk.rest import ApiException
from pprint import pprint

# Defining the host is optional and defaults to https://appfloor.in
# See configuration.py for a list of all supported configuration parameters.
configuration = xfloor_memory_sdk.Configuration(
    host = "https://appfloor.in"
)

# The client must configure the authentication and authorization parameters
# in accordance with the API server security policy.
# Examples for each auth method are provided below, use the example that
# satisfies your auth use case.

# Configure Bearer authorization: bearer
configuration = xfloor_memory_sdk.Configuration(
    access_token = os.environ["BEARER_TOKEN"]
)

# Enter a context with an instance of the API client
with xfloor_memory_sdk.ApiClient(configuration) as api_client:
    # Create an instance of the API class
    api_instance = xfloor_memory_sdk.DefaultApi(api_client)
    mobile_number = 'mobile_number_example' # str |  (optional)
    email_id = 'email_id_example' # str |  (optional)
    name = 'name_example' # str |  (optional)
    app_id = 'app_id_example' # str |  (optional)

    try:
        # External User Registration
        api_response = api_instance.register_external_user_identity(mobile_number=mobile_number, email_id=email_id, name=name, app_id=app_id)
        print("The response of DefaultApi->register_external_user_identity:\n")
        pprint(api_response)
    except Exception as e:
        print("Exception when calling DefaultApi->register_external_user_identity: %s\n" % e)
```



### Parameters


Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **mobile_number** | **str**|  | [optional] 
 **email_id** | **str**|  | [optional] 
 **name** | **str**|  | [optional] 
 **app_id** | **str**|  | [optional] 

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
**200** |  |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **rename_floor**
> GetFloorInformation200Response rename_floor(user_id=user_id, app_id=app_id, var_from=var_from, to=to)

Rename floor

This API renames a floor by changing knowing the **floor identifier (floor_id)**.

It allows the **floor owner** to update the public-facing floor ID (slug/handle) from an old value to a new value. This is typically used when the owner wants to rebrand, reorganize, or correct the floor’s identifier.

⚠️ **This operation affects how the floor is accessed and referenced externally**, so it must be performed carefully.

---

## Ownership & Authorization (Critical)

* The caller **must be authenticated**
* **Only the floor owner** is allowed to rename a floor
* Members, followers, or non-owners **cannot** perform this operation
* Ownership is validated internally using `user_id`

> If the user is not the owner, the request must be rejected.

---

## Request Method

`POST`

---

## Content-Type

`application/x-www-form-urlencoded`
(or equivalent form-data encoding)

---

## Request Parameters (Form Fields)

| Parameter | Type   | Required | Description                                                                     |
| --------- | ------ | -------- | ------------------------------------------------------------------------------- |
| `user_id` | String | **Yes**  | User requesting the rename. Must be the **owner** of the floor.                 |
| `from`    | String | **Yes**  | Existing floor ID (current identifier to be renamed).                           |
| `to`      | String | **Yes**  | New floor ID to assign to the floor.                                            |
| `app_id`  | String | No       | Identifier of the calling application (used mainly for pod/developer contexts). |

---

## Rename Rules & Constraints

* The `from` floor ID **must exist**
* The `to` floor ID **must be unique** and not already in use
* The rename operation updates **only the floor ID**

  * Floor ownership, blocks, posts, and internal `fid` remain unchanged
* Any links or references using the old floor ID may no longer be valid after rename

---

## Behavior Summary

| Scenario                     | Result                                            |
| ---------------------------- | ------------------------------------------------- |
| Valid owner + unique new ID  | Floor ID renamed successfully                     |
| Non-owner user               | Request rejected                                  |
| `from` floor ID not found    | Error                                             |
| `to` floor ID already exists | Error                                             |
| `from` == `to`               | No-op or validation error (implementation choice) |

---

## Response Format

`application/json`

---

## Sample Success Response

```json
{
  "status": "SUCCESS",
  "old_floor_id": "oldfloorid",
  "new_floor_id": "newfloorid",
  "message": "Floor ID renamed successfully"
}
```

---

## Sample Error Responses

### Not Floor Owner

```json
{
  "status": "ERROR",
  "message": "Only the floor owner can rename the floor"
}
```

---

### Floor Not Found

```json
{
  "status": "ERROR",
  "message": "Source floor ID does not exist"
}
```

---

### Floor ID Already Exists

```json
{
  "status": "ERROR",
  "message": "Target floor ID is already in use"
}
```

---

### Invalid Request

```json
{
  "status": "ERROR",
  "message": "user_id, from, and to are required"
}
```

---

## Notes for Developers

* This API **renames the public identifier only**; the internal immutable floor ID (`fid`) is not affected.
* Clients should refresh cached floor metadata after a successful rename.
* If your platform supports deep links or bookmarks, consider redirect or alias handling for old floor IDs (if supported).

---

### One-Line Mental Model

> **This API answers: “Change the public identity (ID) of a floor, owner-only.”**


### Example


```python
import xfloor_memory_sdk
from xfloor_memory_sdk.models.get_floor_information200_response import GetFloorInformation200Response
from xfloor_memory_sdk.rest import ApiException
from pprint import pprint

# Defining the host is optional and defaults to https://appfloor.in
# See configuration.py for a list of all supported configuration parameters.
configuration = xfloor_memory_sdk.Configuration(
    host = "https://appfloor.in"
)


# Enter a context with an instance of the API client
with xfloor_memory_sdk.ApiClient(configuration) as api_client:
    # Create an instance of the API class
    api_instance = xfloor_memory_sdk.DefaultApi(api_client)
    user_id = 'user_id_example' # str | User ID (optional)
    app_id = 'app_id_example' # str | App ID (optional)
    var_from = 'var_from_example' # str | Old floor ID (optional)
    to = 'to_example' # str | New floor ID (optional)

    try:
        # Rename floor
        api_response = api_instance.rename_floor(user_id=user_id, app_id=app_id, var_from=var_from, to=to)
        print("The response of DefaultApi->rename_floor:\n")
        pprint(api_response)
    except Exception as e:
        print("Exception when calling DefaultApi->rename_floor: %s\n" % e)
```



### Parameters


Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **user_id** | **str**| User ID | [optional] 
 **app_id** | **str**| App ID | [optional] 
 **var_from** | **str**| Old floor ID | [optional] 
 **to** | **str**| New floor ID | [optional] 

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
**200** |  |  -  |
**400** |  |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **reset_password**
> ResetPassword200Response reset_password(activation_code, email_id=email_id, mobile_number=mobile_number, app_id=app_id)

Reset Password

---

## Reset Password (Forgot Password, Not Logged In)

Resets the password of a user who **cannot log in** and is using a **forgot-password** flow.

This endpoint is used when the user is not authenticated and requests a password reset using a verified identity channel such as **email** or **mobile number**. The system validates a **one-time reset verification code** (`activation_code`) issued for the reset-password flow. If valid and not expired, the password is updated to `new_password` and takes effect immediately.

If verification fails, the password remains unchanged and an error response is returned.

### Authentication

✅ **Recommended** (better security): a short-lived **reset token** issued after initiating reset

```
Authorization: Bearer <reset_token>
```

> If you don’t use a reset token, you must enforce strong rate limiting + OTP attempt throttling on this endpoint.

### Request Body (Form Data)

* `email_id` or `mobile_number` (required to identify user)
* `activation_code` (required)
* `new_password` (required)
* `user_id` (optional, if your reset flow already resolved it)

### Behavior Notes

* Requires a prior call to **initiate reset** and send OTP/code (mode = forgot password).
* Must enforce code attempt limits and expiration strictly.

### One-Line Summary

> Resets a user’s password (forgot-password flow) after validating a one-time reset code sent to email or mobile.




### Example


```python
import xfloor_memory_sdk
from xfloor_memory_sdk.models.reset_password200_response import ResetPassword200Response
from xfloor_memory_sdk.rest import ApiException
from pprint import pprint

# Defining the host is optional and defaults to https://appfloor.in
# See configuration.py for a list of all supported configuration parameters.
configuration = xfloor_memory_sdk.Configuration(
    host = "https://appfloor.in"
)


# Enter a context with an instance of the API client
with xfloor_memory_sdk.ApiClient(configuration) as api_client:
    # Create an instance of the API class
    api_instance = xfloor_memory_sdk.DefaultApi(api_client)
    activation_code = 'activation_code_example' # str | Activation Code
    email_id = 'email_id_example' # str | Email ID (optional)
    mobile_number = 'mobile_number_example' # str | Mobile number (optional)
    app_id = 'app_id_example' # str | App ID (optional)

    try:
        # Reset Password
        api_response = api_instance.reset_password(activation_code, email_id=email_id, mobile_number=mobile_number, app_id=app_id)
        print("The response of DefaultApi->reset_password:\n")
        pprint(api_response)
    except Exception as e:
        print("Exception when calling DefaultApi->reset_password: %s\n" % e)
```



### Parameters


Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **activation_code** | **str**| Activation Code | 
 **email_id** | **str**| Email ID | [optional] 
 **mobile_number** | **str**| Mobile number | [optional] 
 **app_id** | **str**| App ID | [optional] 

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
**200** |  |  -  |
**400** |  |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **send_validation_code**
> SendValidationCode200Response send_validation_code(send_validation_code_request)

Send Validation code

Generates and sends a one-time validation code to the user for verification of sensitive or critical account operations.

This API is used across multiple authentication and account-management flows. The validation code is delivered to the user via the appropriate channel (**email or mobile number**), based on the requested operation mode and the input provided.

The generated code is **time-bound**, **single-use**, and must be validated using the corresponding verification APIs to complete the requested action.

---

### **Usage Scenarios (Mode Definition)**

| Mode | Purpose                       |
| ---- | ----------------------------- |
| `0`  | Email or mobile number change |
| `1`  | Password change               |
| `2`  | Delete account                |
| `3`  | Clear account                 |
| `4`  | Signup Verification           |

**Mode `5` – Signup Verification**
For login verification, the validation code is sent to **either the email ID or the mobile number provided in the request**.
At least **one of email or mobile number must be supplied** for this mode.

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

This endpoint requires **Bearer Token authentication**,
**except** where explicitly allowed (for example, login-related flows).

```
Authorization: Bearer <access_token>
```

---

### **Successful Response**

On success, the API confirms that the validation code has been generated and successfully dispatched to the user.

---

### **Error Response**

The API returns an error response if:

* The user does not exist or is not eligible for the requested operation
* The requested mode is invalid or unsupported
* Required identifiers (email or mobile number for login verification) are missing
* Rate limits are exceeded
* Authorization fails (where applicable)

---

### **Security Notes (Recommended)**

* Validation codes are single-use and time-bound
* Rate limiting is enforced to prevent abuse
* Repeated failures may trigger temporary blocking or additional verification

---

### **One-Line Summary**

> Sends a one-time validation code for secure account and authentication operations, including login via email or mobile number.

### Example

* Bearer Authentication (bearer):

```python
import xfloor_memory_sdk
from xfloor_memory_sdk.models.send_validation_code200_response import SendValidationCode200Response
from xfloor_memory_sdk.models.send_validation_code_request import SendValidationCodeRequest
from xfloor_memory_sdk.rest import ApiException
from pprint import pprint

# Defining the host is optional and defaults to https://appfloor.in
# See configuration.py for a list of all supported configuration parameters.
configuration = xfloor_memory_sdk.Configuration(
    host = "https://appfloor.in"
)

# The client must configure the authentication and authorization parameters
# in accordance with the API server security policy.
# Examples for each auth method are provided below, use the example that
# satisfies your auth use case.

# Configure Bearer authorization: bearer
configuration = xfloor_memory_sdk.Configuration(
    access_token = os.environ["BEARER_TOKEN"]
)

# Enter a context with an instance of the API client
with xfloor_memory_sdk.ApiClient(configuration) as api_client:
    # Create an instance of the API class
    api_instance = xfloor_memory_sdk.DefaultApi(api_client)
    send_validation_code_request = xfloor_memory_sdk.SendValidationCodeRequest() # SendValidationCodeRequest | 

    try:
        # Send Validation code
        api_response = api_instance.send_validation_code(send_validation_code_request)
        print("The response of DefaultApi->send_validation_code:\n")
        pprint(api_response)
    except Exception as e:
        print("Exception when calling DefaultApi->send_validation_code: %s\n" % e)
```



### Parameters


Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **send_validation_code_request** | [**SendValidationCodeRequest**](SendValidationCodeRequest.md)|  | 

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
**200** |  |  -  |
**400** |  |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **sign_in_with_email**
> SignInWithEmail200Response sign_in_with_email(email_id, pass_code, login_type, app_id=app_id)

Sign In with email ID

Authenticates a user using a registered email ID.
The authentication mechanism is determined by the specified `mode`.

* When `login_type` is set to **`1`**, the user is authenticated using the provided **password**.
* When `login_type` is set to **`2`**, the user is authenticated using a **one-time activation code (OTP)**.

For OTP-based authentication (`login_type = 2`), the client **must first invoke the Send Validation Code API** with the appropriate login mode to generate and deliver the activation code to the user.

---
### **Request Body**

| Field        | Type          | Required | Description                                                       |
| ------------ | ------------- | -------- | ----------------------------------------------------------------- |
| `email_id` | string | Yes      | Email ID |
| `pass_code` | string | Yes      | Password/Validation code depending on the login_type|
| `login_type` | string | Yes      | login type 1 for password 2 for validation code| 
 |`app_id` | string | Yes      | App ID | 



**Field Description**

* `email_id` – Registered email address of the user
* `pass_code` – password or activation code  (this is password if it is 1 and 2 it is validation code)
* `app_id` - App ID which is a 13 digit numeric value
* `login_type` – Login type
  * `1` → Password-based login
  * `2` → Activation code (OTP)–based login

---

### **Behavior Notes**

* When `login_type = 2`, password validation is bypassed.
* OTP-based login requires a prior call to `
/auth-service/send/sign/in/validation/code`.
* If the required credentials for the selected mode are missing or invalid, authentication fails.

---

### **Successful Response**

On successful authentication, the user is signed in and a success response is returned as per the authentication flow.

---

### **Error Response**

The API returns an error response if:

* The email ID is not registered
* The password is incorrect (`login_type = 1 `)
* The activation code is missing, invalid, or expired (`login_type = 2`)
* The mode value is invalid or unsupported

---

### **One-Line Summary**

> Signs in a user using an email ID with either password-based or OTP-based authentication, based on the selected mode.



### Example

* Bearer Authentication (bearer):

```python
import xfloor_memory_sdk
from xfloor_memory_sdk.models.sign_in_with_email200_response import SignInWithEmail200Response
from xfloor_memory_sdk.rest import ApiException
from pprint import pprint

# Defining the host is optional and defaults to https://appfloor.in
# See configuration.py for a list of all supported configuration parameters.
configuration = xfloor_memory_sdk.Configuration(
    host = "https://appfloor.in"
)

# The client must configure the authentication and authorization parameters
# in accordance with the API server security policy.
# Examples for each auth method are provided below, use the example that
# satisfies your auth use case.

# Configure Bearer authorization: bearer
configuration = xfloor_memory_sdk.Configuration(
    access_token = os.environ["BEARER_TOKEN"]
)

# Enter a context with an instance of the API client
with xfloor_memory_sdk.ApiClient(configuration) as api_client:
    # Create an instance of the API class
    api_instance = xfloor_memory_sdk.DefaultApi(api_client)
    email_id = 'email_id_example' # str | Email ID
    pass_code = 'pass_code_example' # str | Validation code or password depends on the login_type
    login_type = 'login_type_example' # str | 1 is for password, 2 is for validation code
    app_id = 'app_id_example' # str | App ID (optional)

    try:
        # Sign In with email ID
        api_response = api_instance.sign_in_with_email(email_id, pass_code, login_type, app_id=app_id)
        print("The response of DefaultApi->sign_in_with_email:\n")
        pprint(api_response)
    except Exception as e:
        print("Exception when calling DefaultApi->sign_in_with_email: %s\n" % e)
```



### Parameters


Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **email_id** | **str**| Email ID | 
 **pass_code** | **str**| Validation code or password depends on the login_type | 
 **login_type** | **str**| 1 is for password, 2 is for validation code | 
 **app_id** | **str**| App ID | [optional] 

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
**200** |  |  -  |
**400** |  |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **sign_in_with_mobile_number**
> SignInWithEmail200Response sign_in_with_mobile_number(body)

Sign In with Mobile number

Authenticates a user using a registered mobile number.
The authentication method is determined by the specified `mode`.

* When `login_type` is set to **`1`**, the user is authenticated using the **password** associated with the account.
* When `login_type` is set to **`2`**, the user is authenticated using a **one-time activation code (OTP)** sent to the registered mobile number.

For OTP-based authentication (`login_type = 1`), the client **must first call the Send Validation Code API** with the appropriate login mode to generate and deliver the activation code.

---

### **Request Formdata**

| Field        | Type          | Required | Description                                                       |
| ------------ | ------------- | -------- | ----------------------------------------------------------------- |
| `mobile_number` | string | Yes      | Mobile number|
| `pass_code` | string | Yes      | Password/Validation code depending on the login_type|
| `login_type` | string | Yes      | login type 1 for password 2 for validation code| 
 |`app_id` | string | Yes      | App ID | 


**Field Description**

* `mobile_number` – Registered mobile number of the user
* `pass_code` – Password / Validation code (password when `login_type= 1`; validation code when `login_type = 2`)
* `login_type` – Login type

  * `1` → Password-based login
  * `2` → Activation code (OTP)–based login

---

### **Behavior Notes**

* When `login_type = 2`, password validation is skipped.
* OTP-based login requires a prior call to `/auth-service/send/sign/in/validation/code`.
* Missing or invalid credentials for the selected mode will result in authentication failure.

---

### **Successful Response**

On successful authentication, the user is signed in and a success response is returned according to the authentication flow.

---

### **Error Response**

The API returns an error response if:

* The mobile number is not registered
* The password is incorrect (`login_type = 1`)
* The activation code is missing, invalid, or expired (`login_type = 2`)
* An invalid or unsupported mode is provided

---

### **One-Line Summary**

> Signs in a user using a mobile number with either password-based or OTP-based authentication, based on the selected mode.

### Example

* Bearer Authentication (bearer):

```python
import xfloor_memory_sdk
from xfloor_memory_sdk.models.sign_in_with_email200_response import SignInWithEmail200Response
from xfloor_memory_sdk.rest import ApiException
from pprint import pprint

# Defining the host is optional and defaults to https://appfloor.in
# See configuration.py for a list of all supported configuration parameters.
configuration = xfloor_memory_sdk.Configuration(
    host = "https://appfloor.in"
)

# The client must configure the authentication and authorization parameters
# in accordance with the API server security policy.
# Examples for each auth method are provided below, use the example that
# satisfies your auth use case.

# Configure Bearer authorization: bearer
configuration = xfloor_memory_sdk.Configuration(
    access_token = os.environ["BEARER_TOKEN"]
)

# Enter a context with an instance of the API client
with xfloor_memory_sdk.ApiClient(configuration) as api_client:
    # Create an instance of the API class
    api_instance = xfloor_memory_sdk.DefaultApi(api_client)
    body = None # object | 

    try:
        # Sign In with Mobile number
        api_response = api_instance.sign_in_with_mobile_number(body)
        print("The response of DefaultApi->sign_in_with_mobile_number:\n")
        pprint(api_response)
    except Exception as e:
        print("Exception when calling DefaultApi->sign_in_with_mobile_number: %s\n" % e)
```



### Parameters


Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **body** | **object**|  | 

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
**200** |  |  -  |
**400** |  |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **sign_up**
> SignUp200Response sign_up(name, password, email_id=email_id, mobile_number=mobile_number, app_id=app_id)

Sign Up

Creates a new user account in the Floor POD using **either a mobile number or an email ID**.
At least **one of `mobile_number` or `email_id` is required** to register a user. Both may be provided if available.

The API registers the user under the specified application context and prepares the account for subsequent authentication and usage.

Upon successful registration, the API returns:
- a unique user_id identifying the newly created user, and
- a success string indicating the outcome of the sign-up operation.
The user account is created under the specified application context and can be used for subsequent interactions with Floor POD APIs.

---

### **Parameter Clarification (Recommended)**

* `name` is mandatory for user profile creation
* Either `mobile_number` **or** `email_id` must be present
* `app_id` is optional and used to associate the user with a specific application




### Example

* Bearer Authentication (bearer):

```python
import xfloor_memory_sdk
from xfloor_memory_sdk.models.sign_up200_response import SignUp200Response
from xfloor_memory_sdk.rest import ApiException
from pprint import pprint

# Defining the host is optional and defaults to https://appfloor.in
# See configuration.py for a list of all supported configuration parameters.
configuration = xfloor_memory_sdk.Configuration(
    host = "https://appfloor.in"
)

# The client must configure the authentication and authorization parameters
# in accordance with the API server security policy.
# Examples for each auth method are provided below, use the example that
# satisfies your auth use case.

# Configure Bearer authorization: bearer
configuration = xfloor_memory_sdk.Configuration(
    access_token = os.environ["BEARER_TOKEN"]
)

# Enter a context with an instance of the API client
with xfloor_memory_sdk.ApiClient(configuration) as api_client:
    # Create an instance of the API class
    api_instance = xfloor_memory_sdk.DefaultApi(api_client)
    name = 'name_example' # str | New User Name
    password = 'password_example' # str | Password
    email_id = 'email_id_example' # str | Email ID of the user (optional)
    mobile_number = 'mobile_number_example' # str | Mobile number (optional)
    app_id = 'app_id_example' # str | Registered App ID (optional)

    try:
        # Sign Up
        api_response = api_instance.sign_up(name, password, email_id=email_id, mobile_number=mobile_number, app_id=app_id)
        print("The response of DefaultApi->sign_up:\n")
        pprint(api_response)
    except Exception as e:
        print("Exception when calling DefaultApi->sign_up: %s\n" % e)
```



### Parameters


Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **name** | **str**| New User Name | 
 **password** | **str**| Password | 
 **email_id** | **str**| Email ID of the user | [optional] 
 **mobile_number** | **str**| Mobile number | [optional] 
 **app_id** | **str**| Registered App ID | [optional] 

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
**200** |  |  -  |
**400** |  |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **validate_code**
> UserDetails validate_code(validate_code_request)

Validation

## **Validate Activation / Verification Code**

This API **validates a one-time verification code** submitted by a user and **executes the corresponding account operation** based on the specified **mode**.

Depending on the mode, the API may:

* Activate a newly registered account
* Confirm a login attempt
* Verify a password change or reset
* Validate email or mobile updates
* Confirm account deletion or clearing requests

The API verifies the provided `activation_code` against the given `user_id`, `mode`, and application context.
If validation succeeds, the requested operation is completed and the API returns the relevant **POD information** and **user profile details** (where applicable).

If validation fails, the operation is **not performed** and an appropriate error response is returned.

---

## **Authentication**

This endpoint requires **Bearer Token authentication**.

**Header**

```
Authorization: Bearer <access_token>
```

---

## **Request Body**

```json
{
  "user_id": "string",
  "activation_code": "string",
  "app_id": "string",
  "mode": "string"
}
```

### **Field Descriptions**

* **user_id** – Unique identifier of the user initiating the operation
* **activation_code** – One-time verification code sent to the user
* **app_id** – Application identifier (optional or context-specific)
* **mode** – Operation context for which the verification is being performed

---

## **Usage Scenarios (Mode Definitions)**

| Mode | Purpose                                  |
| ---- | ---------------------------------------- |
| 0    | Email or mobile number change            |
| 1    | Password change                          |
| 2    | Delete account                           |
| 3    | Clear account                            |
| 4    | Signup verification (account activation) |
| 5    | Login verification                       |
| 6    | Forgot password verification             |

---

## **Successful Response**

On successful validation:

* The requested operation (based on `mode`) is completed
* The API returns:

  * **POD information** associated with the user (if applicable)
  * **User profile details** (if applicable)

Examples:

* For **signup verification**, the user account is activated
* For **login**, access is confirmed
* For **password reset**, the user may proceed to set a new password
* For **account deletion**, the request is confirmed

---

## **Error Response**

The API returns an error response when:

* The activation code is invalid or expired
* The activation code does not match the user or operation mode
* The requested operation is already completed (e.g., user already activated)
* Authorization fails or the bearer token is missing or invalid

⚠️ In all error cases, **no account state change occurs**.

---

## **One-Line Summary**

> Validates a one-time verification code and securely completes the requested user account operation (signup, login, password change, or account actions), returning POD and profile details on success.

### Example

* Bearer Authentication (bearer):

```python
import xfloor_memory_sdk
from xfloor_memory_sdk.models.user_details import UserDetails
from xfloor_memory_sdk.models.validate_code_request import ValidateCodeRequest
from xfloor_memory_sdk.rest import ApiException
from pprint import pprint

# Defining the host is optional and defaults to https://appfloor.in
# See configuration.py for a list of all supported configuration parameters.
configuration = xfloor_memory_sdk.Configuration(
    host = "https://appfloor.in"
)

# The client must configure the authentication and authorization parameters
# in accordance with the API server security policy.
# Examples for each auth method are provided below, use the example that
# satisfies your auth use case.

# Configure Bearer authorization: bearer
configuration = xfloor_memory_sdk.Configuration(
    access_token = os.environ["BEARER_TOKEN"]
)

# Enter a context with an instance of the API client
with xfloor_memory_sdk.ApiClient(configuration) as api_client:
    # Create an instance of the API class
    api_instance = xfloor_memory_sdk.DefaultApi(api_client)
    validate_code_request = xfloor_memory_sdk.ValidateCodeRequest() # ValidateCodeRequest | 

    try:
        # Validation
        api_response = api_instance.validate_code(validate_code_request)
        print("The response of DefaultApi->validate_code:\n")
        pprint(api_response)
    except Exception as e:
        print("Exception when calling DefaultApi->validate_code: %s\n" % e)
```



### Parameters


Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **validate_code_request** | [**ValidateCodeRequest**](ValidateCodeRequest.md)|  | 

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
**200** |  |  -  |
**400** |  |  -  |
**412** |  |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

