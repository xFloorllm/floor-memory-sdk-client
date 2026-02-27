# xfloor_memory_sdk.EditFloorApi

All URIs are relative to *https://appfloor.in*

Method | HTTP request | Description
------------- | ------------- | -------------
[**edit_floor**](EditFloorApi.md#edit_floor) | **POST** /api/memory/edit/floor/{floor_id} | Edit floor


# **edit_floor**
> GetFloorInformation200Response edit_floor(floor_id, user_id, app_id, logo_file=logo_file, title=title, details=details)

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
    api_instance = xfloor_memory_sdk.EditFloorApi(api_client)
    floor_id = 'floor_id_example' # str | 
    user_id = 'user_id_example' # str | User ID
    app_id = 'app_id_example' # str | App ID
    logo_file = None # bytearray | Floor avatar (optional)
    title = 'title_example' # str | Floor title (optional)
    details = 'details_example' # str | Floor decription (optional)

    try:
        # Edit floor
        api_response = api_instance.edit_floor(floor_id, user_id, app_id, logo_file=logo_file, title=title, details=details)
        print("The response of EditFloorApi->edit_floor:\n")
        pprint(api_response)
    except Exception as e:
        print("Exception when calling EditFloorApi->edit_floor: %s\n" % e)
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

[**GetFloorInformation200Response**](GetFloorInformation200Response.md)

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

