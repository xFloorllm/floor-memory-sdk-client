# XfloorFloorMemorySdkJs.EventApi

All URIs are relative to *https://appfloor.in*

Method | HTTP request | Description
------------- | ------------- | -------------
[**event**](EventApi.md#event) | **POST** /api/memory/events | Create Event (Post Content)
[**getRecentEvents**](EventApi.md#getRecentEvents) | **GET** /api/memory/recent/events | Recent Events



### event

> EventResponse event(inputInfo, appId, userId, opts)

Create Event (Post Content)

### Create Event (Content Ingestion)

Posts content into the specified `floor_id`. This API performs **asynchronous ingestion** — a `200 OK` response means the content has been **accepted and queued**, not immediately retrievable. This API allows a user to **post personal content into their POD (Personal Object Database)**. The posted content is stored under a specified **floor**, embedded by the platform, and made available for **semantic querying, conversational retrieval, and memory-based interactions** once processing completes. It is primarily used to:
* Save reminders, notes, write-ups, or personal knowledge
* Upload content the user wants the system to remember * Add information that should later be discoverable via conversational queries The content may consist of **text only** or **text combined with one or more media files**.

---

### Key Capabilities
* Stores user-generated content inside a specific floor
* Supports **multi-modal inputs** (text + media) * Automatically embeds content for semantic search * Makes content available to:
* `/agent/memory/query`
* conversational agents
* future recall and analytics
* Associates content with **user**, **block**, and **application** context (when provided)

---

### Authentication
* Requires a valid, authenticated `user_id`
* The calling application is responsible for user authentication
* `app_id` identifies the application context

---

### Request Type **Content-Type:** `multipart/form-data`

---

**Request Parameters
1. Files (Optional)**

| Field | Type | Required | Description |
| ------- | -------- | -------- | --------------------------------------------------------------------- |
| `files` | `file[]` | Optional | Media files to attach to the content. Multiple files may be uploaded. |

**Supported formats include (but are not limited to):**
* Images: `jpg`, `png`
* Audio: `mp3` * Documents: `pdf` * Video: `mp4` These files are processed and embedded along with the textual content where applicable.

---
2. Input Information (Required)

| Field | Type | Required | Description |
| ------------ | --------------- | -------- | ----------------------------------------------------------------- |
| `input_info` | `string (JSON)` | Yes | JSON string containing metadata and textual content for the post. |

---

### `input_info` Structure

```json { \"floor_id\":

\"my_floor\", \"block_id\": \"17845683456\", \"block_type\": \"1\", \"user_id\": \"145623907625\", \"title\": \"My note\", \"description\": \"Things I should remember\" }

```

---

### Field Descriptions

| Field | Type | Required | Description |
| ------------- | -------- | -------- | --------------------------------------------------------------------------------------------------------- |
| `floor_id` | `string` | Yes | Identifier of the user’s floor (POD) where the content will be stored. |
| `block_id` | `string` | Optional | Identifier of the block within the floor used to group or categorize content. |
| `block_type` | `string` | Optional | Logical category of the content (e.g., `0 for post`, `1 for forum`). Used for routing and UI organization. |
| `user_id` | `string` | Yes | Unique identifier of the user posting the content. |
| `title` | `string` | Optional | Short title or heading for the content. |
| `description` | `string` | Yes | Main textual content to be stored and embedded. |
| `app_id` | `string` | Optional | Identifier of the calling application context. |

---

### Behavior
1. The API validates the user and floor context.
2. Textual content (`title` and `description`) is ingested. 3. Attached media files (if any) are processed and linked to the content. 4. Embeddings are generated for:
* text
* supported media (where applicable)
5. The content becomes part of the user’s **personal memory store (POD)**.
6. Once background processing completes, the content becomes available for:
* semantic search
* conversational retrieval
* memory-based interactions

---

### Successful Response

On success, the API confirms that:
* The content has been **accepted**
* Processing has been **queued**
* Reference identifiers are returned > A successful response indicates **acceptance**, not immediate availability.

---

### Error Handling The API may return errors if:
* Required fields are missing (`floor_id`, `user_id`, `description`)
* Uploaded files use unsupported formats * The user does not have access to the specified floor * The request payload is malformed * Internal embedding or storage operations fail

---

### Typical Use Cases
* Saving personal reminders
* Posting notes or observations * Uploading documents for later recall * Building a personal knowledge base
* Feeding content into conversational agents

---

### ⚠️ Asynchronous Ingestion Notice Content ingestion is **asynchronous**. A `200 OK` response means the request was **successfully queued**. Newly ingested content may take time to become searchable via the Query API. Use **Recent Events** or retry queries after a short delay to confirm availability.

---

### One-Line Summary 

> Stores user-generated text and media into a personal POD, embeds it asynchronously, and makes it available for semantic and conversational querying.

If you want, next I can:
* align this **exactly** with the OpenAPI schema fields
* generate **JS / TS / Python / Java snippets** using this definition * add **state diagrams** (queued → processing → searchable)

for docs

### Example

```javascript
import XfloorFloorMemorySdkJs from '@xfloor/floor-memory-sdk-js';
let defaultClient = XfloorFloorMemorySdkJs.ApiClient.instance;
// Configure Bearer access token for authorization: bearer
let bearer = defaultClient.authentications['bearer'];
bearer.accessToken = "YOUR ACCESS TOKEN"

let apiInstance = new XfloorFloorMemorySdkJs.EventApi();
let inputInfo = "inputInfo_example"; // String | Input parameters, bid is optional
let appId = "appId_example"; // String | App ID created in developer console.
let userId = "userId_example"; // String | 
let opts = {
  'files': ["null"] // [File] | Attach relevant media here, which includes, jpg, mp3, pdf, mp4 files. More than one media can be selected
};
apiInstance.event(inputInfo, appId, userId, opts, (error, data, response) => {
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
 **inputInfo**

| **String**| Input parameters, bid is optional |
 **appId**

| **String**| App ID created in developer console. |
 **userId**

| **String**|
|
 **files**

| **[File]**| Attach relevant media here, which includes, jpg, mp3, pdf, mp4 files. More than one media can be selected |

[optional]

### Return type

[**EventResponse**](EventResponse.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

- **Content-Type**: multipart/form-data
- **Accept**: application/json


### getRecentEvents

> GetRecentEvents200Response getRecentEvents(floorId, appId, opts)

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
* A **floor** represents a content space (independent floor, followed floor, or pod floor)
* A **pod floor** may aggregate content across multiple related floors * Posts are returned **in reverse chronological order** (latest first) * Each post belongs to a specific **block** within the floor

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

```json { \"post_count\": \"18\", \"items\": [ { \"event_id\": \"1766557274836\", \"block_type\": \"0\", \"title\": \"voice-note-1766557272764.wav\", \"text\": \"You\", \"created_at_ms\": \"1766557275000\", \"author\": { \"name\": \"MEGHANA G\", \"floor_uid\": \"meghanag\", \"avatar\": { \"type\": \"IMAGE\", \"url\": \"https://...\" } }, \"media\": [ { \"type\": \"AUDIO\", \"url\": \"https://...\" } ] } ] }

```

---

### **Notes**
* Posts may contain **plain text or HTML**
* Media is optional and may be absent * Ordering is **latest first**
* The API is read-only and does not require authentication by default
* Access control (public/private floors) is enforced internally

---

### **Typical Use Cases**
* Floor activity feed
* Pod-level dashboards * User-personalized timelines * Public floor landing pages * External developer pods using `app_id`

### Example

```javascript
import XfloorFloorMemorySdkJs from '@xfloor/floor-memory-sdk-js';
let defaultClient = XfloorFloorMemorySdkJs.ApiClient.instance;
// Configure Bearer access token for authorization: bearer
let bearer = defaultClient.authentications['bearer'];
bearer.accessToken = "YOUR ACCESS TOKEN"

let apiInstance = new XfloorFloorMemorySdkJs.EventApi();
let floorId = "floorId_example"; // String | 
let appId = "appId_example"; // String | 
let opts = {
  'userId': "userId_example" // String | 
};
apiInstance.getRecentEvents(floorId, appId, opts, (error, data, response) => {
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
 **floorId**

| **String**|
|
 **appId**

| **String**|
|
 **userId**

| **String**|
|

[optional]

### Return type

[**GetRecentEvents200Response**](GetRecentEvents200Response.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: application/json

