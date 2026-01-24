# XfloorFloorMemorySdkJs.GetRecentEventsApi

All URIs are relative to *https://appfloor.in*

Method | HTTP request | Description
------------- | ------------- | -------------
[**getRecentEvents**](GetRecentEventsApi.md#getRecentEvents) | **GET** /api/memory/recent/events | Recent Events



### getRecentEvents

> GetRecentEvents200Response getRecentEvents(floorId, opts)

Recent Events

This API retrieves the **latest posts (events)** from a specified floor. The behaviour of the API changes based on whether a **user ID** is provided:
* **If `user_id` is provided** → The API returns **recent posts relevant to that user**, scoped within the given floor. This includes posts from:
* Floors the user follows
* Floors created by the user
* Pod floors associated with the user (if applicable)
* **If `user_id` is NOT provided** → The API returns the **most recent posts available in the specified floor**, without user-specific filtering. This makes the API suitable for:
* Personalized activity feeds * Floor-level public timelines * Pod-based content aggregation * Developer-built pods and custom clients

---

### **Key Concepts**
* A **floor** represents a content space (independent floor, followed floor, or pod floor) * A **pod floor** may aggregate content across multiple related floors * Posts are returned **in reverse chronological order** (latest first) * Each post belongs to a specific **block** within the floor

---

### **Request Method** `GET`

---

### **Request Parameters (Query Params)** | Parameter Name | Type | Required | Description |
| -------------- | ------ | -------- | -------------------------------------------------------------------------------------------------------------------------- |
| `floor_id` | String | **Yes** | Floor identifier from which events should be fetched. Can be a pod floor ID, followed floor ID, or an independent floor ID |
| `user_id` | String | No | If provided, returns posts relevant to the user within the given floor |
| `app_id` | String | No | Identifier for external developers or pod-based applications consuming this API |

---

### **Behavior Summary** | Scenario | Result |
| ---------------------- | ----------------------------------------- |
| `floor_id` only | Latest posts from the specified floor |
| `floor_id` + `user_id` | User-relevant posts within that floor |
| Pod floor ID | Aggregated posts across pod-linked floors |
| Independent floor ID | Posts only from that floor |

---

### **Response Format** `application/json`

---

### **Response Structure**

### **Top-Level Fields** | Field | Type | Description |
| ------------ | ------ | ------------------------------ |
| `post_count` | String | Total number of posts returned |
| `items` | Array | List of recent post objects |

---

### **Post Object (`items[]`)** | Field | Type | Description |
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

### **Author Object** | Field | Type | Description |
| ----------- | ------ | ---------------------------- |
| `name` | String | Display name of the author |
| `floor_uid` | String | Author’s floor/user handle |
| `avatar` | Object | Author profile image details |

---

### **Media Object** | Field | Type | Description |
| ------ | ------ | ----------------------------------- |
| `type` | String | Media type (e.g., `AUDIO`, `IMAGE`) |
| `url` | String | Public URL of the media file |

---

### **Sample Success Response** *(structure abbreviated for clarity)*

```json { \"post_count\": \"18\", \"items\": [ { \"event_id\": \"1766557274836\", \"block_type\": \"0\", \"title\": \"voice-note-1766557272764.wav\", \"text\": \"You\", \"created_at_ms\": \"1766557275000\", \"author\": { \"name\": \"MEGHANA G\", \"floor_uid\": \"meghanag\", \"avatar\": { \"type\": \"IMAGE\", \"url\": \"https://...\" } }, \"media\": [ { \"type\": \"AUDIO\", \"url\": \"https://...\" } ] } ] } ```

---

### **Notes**
* Posts may contain **plain text or HTML** * Media is optional and may be absent * Ordering is **latest first** * The API is read-only and does not require authentication by default * Access control (public/private floors) is enforced internally

---

### **Typical Use Cases**
* Floor activity feed * Pod-level dashboards * User-personalized timelines * Public floor landing pages * External developer pods using `app_id`

### Example

```javascript
import XfloorFloorMemorySdkJs from '@xfloor/floor-memory-sdk-js';
let defaultClient = XfloorFloorMemorySdkJs.ApiClient.instance;
// Configure Bearer access token for authorization: bearer
let bearer = defaultClient.authentications['bearer'];
bearer.accessToken = "YOUR ACCESS TOKEN"

let apiInstance = new XfloorFloorMemorySdkJs.GetRecentEventsApi();
let floorId = "floorId_example"; // String | 
let opts = {
  'userId': "userId_example", // String | 
  'appId': "appId_example" // String | 
};
apiInstance.getRecentEvents(floorId, opts, (error, data, response) => {
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
 **floorId** | **String**|  | 
 **userId** | **String**|  | [optional] 
 **appId** | **String**|  | [optional] 

### Return type

[**GetRecentEvents200Response**](GetRecentEvents200Response.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: application/json

