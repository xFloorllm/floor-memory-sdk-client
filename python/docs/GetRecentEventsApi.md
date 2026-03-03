# xfloor_memory_sdk.GetRecentEventsApi

All URIs are relative to *https://appfloor.in*

Method | HTTP request | Description
------------- | ------------- | -------------
[**get_recent_events**](GetRecentEventsApi.md#get_recent_events) | **GET** /api/memory/recent/events | Recent Events


# **get_recent_events**
> GetRecentEvents200Response get_recent_events(floor_id, app_id, user_id=user_id)

Recent Events

This API retrieves the **latest posts (events)** from a specified floor.

The behaviour of the API changes based on whether a **user ID** is provided:

* **If `user_id` is provided**
  → The API returns **recent posts relevant to that user**, scoped within the given floor.
  This includes posts from:

  * Floors the user follows
  * Floors created by the user
  * Pod floors associated with the user (if applicable)

* **If `user_id` is NOT provided**
  → The API returns the **most recent posts available in the specified floor**, without user-specific filtering.

This makes the API suitable for:

* Personalized activity feeds
* Floor-level public timelines
* Pod-based content aggregation
* Developer-built pods and custom clients

---

### **Key Concepts**

* A **floor** represents a content space (independent floor, followed floor, or pod floor)
* A **pod floor** may aggregate content across multiple related floors
* Posts are returned **in reverse chronological order** (latest first)
* Each post belongs to a specific **block** within the floor

---

### **Request Method**

`GET`

---

### **Request Parameters (Query Params)**

| Parameter Name | Type | Required | Description |
| -------------- | ------ | -------- | -------------------------------------------------------------------------------------------------------------------------- |
| `floor_id` | String | **Yes** | Floor identifier from which events should be fetched. Can be a pod floor ID, followed floor ID, or an independent floor ID |
| `user_id` | String | No | If provided, returns posts relevant to the user within the given floor |
| `app_id` | String | No | Identifier for external developers or pod-based applications consuming this API |

---

### **Behavior Summary**

| Scenario | Result |
| ---------------------- | ----------------------------------------- |
| `floor_id` only | Latest posts from the specified floor |
| `floor_id` + `user_id` | User-relevant posts within that floor |
| Pod floor ID | Aggregated posts across pod-linked floors |
| Independent floor ID | Posts only from that floor |

---

### **Response Format**

`application/json`

---

### **Response Structure**

### **Top-Level Fields**

| Field | Type | Description |
| ------------ | ------ | ------------------------------ |
| `post_count` | String | Total number of posts returned |
| `items` | Array | List of recent post objects |

---

### **Post Object (`items[]`)**

| Field | Type | Description |
| --------------- | ------ | ------------------------------------------------------------------------- |
| `event_id` | String | Unique identifier of the post/event |
| `block_type` | String | Type of block where the post was created (e.g., blog, forum, audio, etc.) |
| `block_id` | String | Identifier of the block within the floor |
| `floor_uid` | String | Floor identifier where the post belongs |
| `title` | String | Title of the post (may be empty) |
| `text` | String | Text or HTML content of the post |
| `media` | Array | Media objects (audio, image, etc.), if any |
| `created_at_ms` | String | Post creation time in milliseconds (epoch) |

---

### **Author Object**

| Field | Type | Description |
| ----------- | ------ | ---------------------------- |
| `name` | String | Display name of the author |
| `floor_uid` | String | Author’s floor/user handle |
| `avatar` | Object | Author profile image details |

---

### **Media Object**

| Field | Type | Description |
| ------ | ------ | ----------------------------------- |
| `type` | String | Media type (e.g., `AUDIO`, `IMAGE`) |
| `url` | String | Public URL of the media file |

---

### **Sample

Success Response**

*(structure abbreviated for clarity)*

```json
{
  "post_count": "18",
  "items": [
    {
      "event_id": "1766557274836",
      "block_type": "0",
      "title": "voice-note-1766557272764.wav",
      "text": "You",
      "created_at_ms": "1766557275000",
      "author": {
        "name": "MEGHANA G",
        "floor_uid": "meghanag",
        "avatar": {
          "type": "IMAGE",
          "url": "https://..."
        }
      },
      "media": [
        {
          "type": "AUDIO",
          "url": "https://..."
        }
      ]
    }
  ]
}
```

---

### **Notes**

* Posts may contain **plain text or HTML**
* Media is optional and may be absent
* Ordering is **latest first**
* The API is read-only and does not require authentication by default
* Access control (public/private floors) is enforced internally

---

### **Typical Use Cases**

* Floor activity feed
* Pod-level dashboards
* User-personalized timelines
* Public floor landing pages
* External developer pods using `app_id`

### Example

* Bearer Authentication (bearer):

```python
import xfloor_memory_sdk
from xfloor_memory_sdk.models.get_recent_events200_response import GetRecentEvents200Response
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
    api_instance = xfloor_memory_sdk.GetRecentEventsApi(api_client)
    floor_id = 'floor_id_example' # str | 
    app_id = 'app_id_example' # str | 
    user_id = 'user_id_example' # str |  (optional)

    try:
        # Recent Events
        api_response = api_instance.get_recent_events(floor_id, app_id, user_id=user_id)
        print("The response of GetRecentEventsApi->get_recent_events:\n")
        pprint(api_response)
    except Exception as e:
        print("Exception when calling GetRecentEventsApi->get_recent_events: %s\n" % e)
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

| **str**|
|
 **user_id**

| **str**|
|

[optional]

### Return type

[**GetRecentEvents200Response**](GetRecentEvents200Response.md)

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

