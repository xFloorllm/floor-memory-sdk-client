# xfloor_memory_sdk.FloorApi

All URIs are relative to *https://appfloor.in*

Method | HTTP request | Description
------------- | ------------- | -------------
[**edit_floor**](FloorApi.md#edit_floor) | **POST** /api/memory/edit/floor/{floor_id} | Edit floor
[**get_floor_information**](FloorApi.md#get_floor_information) | **GET** /api/memory/floor/info/{floor_id} | Basic information of a floor
[**make_floor_private**](FloorApi.md#make_floor_private) | **POST** /api/memory/make/floor/private/{floor_id} | Make floor Private
[**make_floor_public**](FloorApi.md#make_floor_public) | **POST** /api/memory/make/floor/public/{floor_id} | Make floor public
[**rename_floor**](FloorApi.md#rename_floor) | **POST** /api/memory/change/floor/id | Rename floor


# **edit_floor**
> EditFloor200Response edit_floor(floor_id, user_id, app_id, logo_file=logo_file, title=title, details=details)

Edit floor

This API updates an existing floor’s profile metadata using **multipart form data**.

A floor **can be edited only by its owner**.
If the authenticated user is **not the owner of the floor**, the request will be rejected, even if the user is a member or follower of the floor.

The API allows the floor owner to update:

* Floor **title**
* Floor **details/description**
* Floor **logo/avatar image**

After a successful update, the API returns the **latest floor object**, including the updated avatar and the current list of blocks associated with the floor.

---

### Authorization Rules (Critical)

* The caller **must be authenticated**
* The caller **must be the owner of the floor**
* Members, followers, or pod consumers **cannot** edit the floor
* Ownership is validated internally using the authenticated user context

> **Ownership is mandatory. There are no partial permissions for this API.**

---

**Content-Type**



`multipart/form-data`

---

**Request Body**

(Multipart Form Data)

### Form Fields

| Field Name | Type | Required | Description |
| ---------- | ------ | ------------ | ---------------------------------------- |
| `floor_id` | String | Optional* | Public / human-readable floor identifier |
| `title` | String | Optional | New floor title |
| `details` | String | Optional | New floor description |
| `logo` | File | Optional | New floor logo image (PNG/JPG/WebP) |

* At least **one floor identifier** (`fid` or `floor_id`) must be provided.
**Best practice:** Use `fid` as the primary identifier.

---

### Update Rules

* At least one of `title`, `details`, or `logo` must be present
* Missing update fields result in a validation error
* If `logo` is provided, the previous logo is replaced

---

### Response Format

`application/json`

---

### Sample

Success Response

```json
{
  "floor_id": "my_floor",
  "title": "daughter ouch upon yummy clamor",
  "details": "nostrud occaecat incididunt dolor adipisicing",
  "fid": "86",
  "blocks": [
    {
      "bid": "83",
      "type": "pariatur",
      "title": "wherever demobilise acidly refute"
    }
  ],
  "avatar": {
    "url": "https://legal-availability.name/",
    "id": "98"
  }
}
```

---

### Error Responses (Authorization Focus)

### Not Floor Owner

```json
{
  "status": "ERROR",
  "message": "Only the floor owner can edit this floor"
}
```

### Floor Not Found

```json
{
  "status": "ERROR",
  "message": "Floor not found"
}
```

### No Update Fields

```json
{
  "status": "ERROR",
  "message": "No update fields provided"
}
```

---

### Notes

* This API is **owner-only by design**
* Pods and developer tools must operate using **owner credentials**
* Blocks are returned for convenience but are **not editable through this API**

---




### Example

* Bearer Authentication (bearer):

```python
import xfloor_memory_sdk
from xfloor_memory_sdk.models.edit_floor200_response import EditFloor200Response
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
    api_instance = xfloor_memory_sdk.FloorApi(api_client)
    floor_id = 'floor_id_example' # str | 
    user_id = 'user_id_example' # str | User ID
    app_id = 'app_id_example' # str | App ID
    logo_file = None # bytearray | Floor avatar (optional)
    title = 'title_example' # str | Floor title (optional)
    details = 'details_example' # str | Floor decription (optional)

    try:
        # Edit floor
        api_response = api_instance.edit_floor(floor_id, user_id, app_id, logo_file=logo_file, title=title, details=details)
        print("The response of FloorApi->edit_floor:\n")
        pprint(api_response)
    except Exception as e:
        print("Exception when calling FloorApi->edit_floor: %s\n" % e)
```



### Parameters


Name

| Type | Description |

Notes
-------------

| ------------- | ------------- |

-------------
 **floor_id**

| **str**|
|
 **user_id**

| **str**| User ID |
 **app_id**

| **str**| App ID |
 **logo_file**

| **bytearray**| Floor avatar |

[optional]
 **title**

| **str**| Floor title |

[optional]
 **details**

| **str**| Floor decription |

[optional]

### Return type

[**EditFloor200Response**](EditFloor200Response.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

 - **Content-Type**: multipart/form-data
 - **Accept**: application/json

### HTTP response details

| Status code | Description | Response headers |
|-------------|-------------|------------------|
**200** |
|
- |
**400** |
|
- |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **get_floor_information**
> FloorInfo get_floor_information(floor_id, app_id, user_id=user_id)

Basic information of a floor

This API returns the **basic profile information of a floor**.
It is used to fetch all essential metadata required to **render a floor landing page, header, or navigation context**.

The response includes:

* Floor identity and type
* Ownership information relative to the requesting user
* Floor metadata (title, description, avatar)
* List of blocks available in the floor
* App association (for pod / developer use cases)

This API does **not** return posts or content; it only provides **structural and descriptive information** about the floor.

---

### Typical Use Cases

* Render floor header (title, logo, description)
* Decide UI permissions (owner vs non-owner)
* Display available blocks (Feeds, Blog, Quiz, etc.)
* Pod discovery or developer-managed floor rendering
* Lightweight floor metadata fetch before loading content

---

### Authorization & Context

* The API may be called by authenticated or unauthenticated users (depending on floor visibility).
* The `is_owner` field is calculated **relative to the requesting user context** (if authenticated).

---

### Response Format

`application/json`

---

### Response Structure

### Top-Level Fields

| Field | Type | Description |
| ------------ | ---------------------- | ---------------------------------------------------------------- |
| `floor_id` | String | Public, human-readable identifier of the floor |
| `floor_uid` | String | Internal unique identifier of the floor |
| `title` | String | Display title of the floor |
| `details` | String | Short description or summary of the floor |
| `floor_type` | String | Type of floor (`PUBLIC`, `PRIVATE`, `POD`) |
| `is_owner` | String (`"0"` / `"1"`) | Indicates whether the requesting user is the owner |
| `blocks` | Array | List of blocks available in the floor |
| `avatar` | Object | Floor logo / avatar metadata |
| `app_id` | String | Associated application ID (used mainly for pod/developer floors) |

---

### Ownership Indicator

### `is_owner`

```json
"is_owner": "0"
```

| Value | Meaning |
| ----- | ----------------------------------------- |
| `"1"` | Requesting user is the owner of the floor |
| `"0"` | Requesting user is not the owner |

This field is typically used by clients to:

* Enable or disable edit/settings UI
* Show owner-only actions

---

### Blocks Object

```json
"blocks": [
  {
    "block_id": "1765960948723",
    "type": "1",
    "title": "Feeds"
  }
]
```

Each block represents a **content category or service** available inside the floor.

### Block Fields

| Field | Type | Description |
| ------- | ------ | ----------------------------------------------------- |
| `block_id` | String | Unique identifier of the block |
| `type` | String | Block type identifier (e.g., feed, blog, forum, quiz) |
| `title` | String | Display name of the block |

---

### Avatar Object

```json
"avatar": {
  "id": "1767009204367",
  "url": "https://..."
}
```

| Field | Type | Description |
| ----- | ------ | ------------------------------ |
| `id` | String | Media identifier of the avatar |
| `url` | String | CDN URL of the floor logo |

Used to render the floor’s profile image or banner.

---

### Floor Type

```json
"floor_type": "POD"
```

| Value | Meaning |
| --------- | ------------------------------------- |
| `PUBLIC` | Open floor visible to everyone |
| `PRIVATE` | Restricted floor |
| `POD` | Aggregated or developer-managed floor |

`POD` floors are often associated with an `app_id` and may aggregate or serve content programmatically.

---

### Sample

Success Response

```json
{
  "is_owner": "0",
  "blocks": [
    {
      "block_id": "1765960948723",
      "type": "1",
      "title": "Feeds"
    }
  ],
  "floor_uid": "1765960956967",
  "floor_id": "raghupodfloor1",
  "details": "raghu",
  "avatar": {
    "id": "1767009204367",
    "url": "https://d2e5822u5ecuq8.cloudfront.net/room/1765960956967/logo/1765960956967.jpg"
  },
  "title": "raghu",
  "floor_type": "POD",
  "app_id": "1765949734005"
}
```

---

### Notes for Developers

* This is a **lightweight metadata API** and is safe to call frequently.
* Use this API **before** loading posts or analytics.
* `blocks` ordering can be used directly for navigation UI.
* `floor_type` + `is_owner` together determine which UI actions are allowed.

---

### Common

Error Scenarios

### Floor Not Found

```json
{
  "status": "ERROR",
  "message": "Floor not found"
}
```

### Access Restricted

```json
{
  "status": "ERROR",
  "message": "Access denied for this floor"
}
```

---

### Final Mental Model

> **This API answers: “What is this floor, who owns it, and what can I do here?”**


### Example

* Bearer Authentication (bearer):

```python
import xfloor_memory_sdk
from xfloor_memory_sdk.models.floor_info import FloorInfo
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
    api_instance = xfloor_memory_sdk.FloorApi(api_client)
    floor_id = 'floor_id_example' # str | 
    app_id = '1387654378393' # str | App ID - 13 digit numeric identity
    user_id = '1345896753484' # str | User ID  - 13 digit numeric identity (optional)

    try:
        # Basic information of a floor
        api_response = api_instance.get_floor_information(floor_id, app_id, user_id=user_id)
        print("The response of FloorApi->get_floor_information:\n")
        pprint(api_response)
    except Exception as e:
        print("Exception when calling FloorApi->get_floor_information: %s\n" % e)
```



### Parameters


Name

| Type | Description |

Notes
-------------

| ------------- | ------------- |

-------------
 **floor_id**

| **str**|
|
 **app_id**

| **str**| App ID - 13 digit numeric identity |
 **user_id**

| **str**| User ID
- 13 digit numeric identity |

[optional]

### Return type

[**FloorInfo**](FloorInfo.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

### HTTP response details

| Status code | Description | Response headers |
|-------------|-------------|------------------|
**200** |
|
- |
**400** |
|
- |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **make_floor_private**
> EditFloor200Response make_floor_private(floor_id, user_id, app_id)

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
* **Only the floor owner** can change floor visibility
* If the user is not the owner, the request must be rejected

---

### Behavior Rules

* Converts visibility from **PUBLIC → PRIVATE**
* Does not modify floor content or blocks
* Access enforcement for private floors is applied immediately after the change

**Idempotency**

* Calling this API multiple times should not cause repeated changes
* If already private, the API should either:

  * return success with a message like `"already private"`, or
  * return a specific error/status indicating no-op

---

### Response Format

`application/json`

---

### Sample

Success Response

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

### Sample No-Op Response (Already Private)

```json
{
  "status": "SUCCESS",
  "floor_id": "my_floor",
  "visibility": "PRIVATE",
  "message": "Floor is already private"
}
```

---

### Error Responses (Examples)

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

### Notes

* This API is intended to control floor visibility only; membership/invite rules (for private floors) are handled elsewhere.
* `app_id` is provided for developer/pod applications and is optional unless enforced by your app model.
* If you support floor types like `POD`, document whether pods are allowed to be private or not (some platforms restrict this).


### Example

* Bearer Authentication (bearer):

```python
import xfloor_memory_sdk
from xfloor_memory_sdk.models.edit_floor200_response import EditFloor200Response
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
    api_instance = xfloor_memory_sdk.FloorApi(api_client)
    floor_id = 'floor_id_example' # str | 
    user_id = 'user_id_example' # str | User ID
    app_id = 'app_id_example' # str | App ID

    try:
        # Make floor Private
        api_response = api_instance.make_floor_private(floor_id, user_id, app_id)
        print("The response of FloorApi->make_floor_private:\n")
        pprint(api_response)
    except Exception as e:
        print("Exception when calling FloorApi->make_floor_private: %s\n" % e)
```



### Parameters


Name

| Type | Description |

Notes
-------------

| ------------- | ------------- |

-------------
 **floor_id**

| **str**|
|
 **user_id**

| **str**| User ID |
 **app_id**

| **str**| App ID |

### Return type

[**EditFloor200Response**](EditFloor200Response.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

### HTTP response details

| Status code | Description | Response headers |
|-------------|-------------|------------------|
**200** |
|
- |
**400** |
|
- |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **make_floor_public**
> EditFloor200Response make_floor_public(floor_id, user_id, app_id)

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

**Request Method**



`POST`

---

**Content-Type**



`application/x-www-form-urlencoded`
(or `multipart/form-data`, depending on your implementation)

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
* **Only the floor owner** is allowed to change the floor’s visibility
* Requests from non-owners must be rejected

---

### Behavior Rules

* Converts floor visibility from **PRIVATE → PUBLIC**
* Does not modify floor content, blocks, or ownership
* Visibility change takes effect immediately

### Idempotency

* If the floor is already public, the API should:

  * Return success with a message indicating no change, or
  * Return a specific “already public” status (implementation-dependent)

---

### Response Format

`application/json`

---

### Sample

Success Response

```json
{
  "status": "SUCCESS",
  "floor_id": "my_floor",
  "visibility": "PUBLIC",
  "message": "Floor is now public"
}
```

---

### Sample No-Op Response (Already Public)

```json
{
  "status": "SUCCESS",
  "floor_id": "my_floor",
  "visibility": "PUBLIC",
  "message": "Floor is already public"
}
```

---

### Error Responses (Examples)

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

### Notes for Developers

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
from xfloor_memory_sdk.models.edit_floor200_response import EditFloor200Response
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
    api_instance = xfloor_memory_sdk.FloorApi(api_client)
    floor_id = 'floor_id_example' # str | 
    user_id = 'user_id_example' # str | User ID
    app_id = 'app_id_example' # str | App ID

    try:
        # Make floor public
        api_response = api_instance.make_floor_public(floor_id, user_id, app_id)
        print("The response of FloorApi->make_floor_public:\n")
        pprint(api_response)
    except Exception as e:
        print("Exception when calling FloorApi->make_floor_public: %s\n" % e)
```



### Parameters


Name

| Type | Description |

Notes
-------------

| ------------- | ------------- |

-------------
 **floor_id**

| **str**|
|
 **user_id**

| **str**| User ID |
 **app_id**

| **str**| App ID |

### Return type

[**EditFloor200Response**](EditFloor200Response.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

### HTTP response details

| Status code | Description | Response headers |
|-------------|-------------|------------------|
**200** |
|
- |
**400** |
|
- |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

# **rename_floor**
> EditFloor200Response rename_floor(user_id, app_id, var_from, to)

Rename floor

This API renames a floor by changing knowing the **floor identifier (floor_id)**.

It allows the **floor owner** to update the public-facing floor ID (slug/handle) from an old value to a new value. This is typically used when the owner wants to rebrand, reorganize, or correct the floor’s identifier.

⚠️ **This operation affects how the floor is accessed and referenced externally**, so it must be performed carefully.

---

### Ownership & Authorization (Critical)

* The caller **must be authenticated**
* **Only the floor owner** is allowed to rename a floor
* Members, followers, or non-owners **cannot** perform this operation
* Ownership is validated internally using `user_id`

> If the user is not the owner, the request must be rejected.

---

**Request Method**



`POST`

---

**Content-Type**



`application/x-www-form-urlencoded`
(or equivalent form-data encoding)

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
* The `to` floor ID **must be unique** and not already in use
* The rename operation updates **only the floor ID**

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

### Response Format

`application/json`

---

### Sample

Success Response

```json
{
  "status": "SUCCESS",
  "old_floor_id": "oldfloorid",
  "new_floor_id": "newfloorid",
  "message": "Floor ID renamed successfully"
}
```

---

### Sample

Error Responses

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

### Notes for Developers

* This API **renames the public identifier only**; the internal immutable floor ID (`fid`) is not affected.
* Clients should refresh cached floor metadata after a successful rename.
* If your platform supports deep links or bookmarks, consider redirect or alias handling for old floor IDs (if supported).

---

### One-Line Mental Model

> **This API answers: “Change the public identity (ID) of a floor, owner-only.”**


### Example

* Bearer Authentication (bearer):

```python
import xfloor_memory_sdk
from xfloor_memory_sdk.models.edit_floor200_response import EditFloor200Response
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
    api_instance = xfloor_memory_sdk.FloorApi(api_client)
    user_id = 'user_id_example' # str | User ID
    app_id = 'app_id_example' # str | App ID
    var_from = 'var_from_example' # str | Old floor ID
    to = 'to_example' # str | New floor ID

    try:
        # Rename floor
        api_response = api_instance.rename_floor(user_id, app_id, var_from, to)
        print("The response of FloorApi->rename_floor:\n")
        pprint(api_response)
    except Exception as e:
        print("Exception when calling FloorApi->rename_floor: %s\n" % e)
```



### Parameters


Name

| Type | Description |

Notes
-------------

| ------------- | ------------- |

-------------
 **user_id**

| **str**| User ID |
 **app_id**

| **str**| App ID |
 **var_from**

| **str**| Old floor ID |
 **to**

| **str**| New floor ID |

### Return type

[**EditFloor200Response**](EditFloor200Response.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

### HTTP response details

| Status code | Description | Response headers |
|-------------|-------------|------------------|
**200** |
|
- |
**400** |
|
- |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

