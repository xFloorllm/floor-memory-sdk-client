# XfloorFloorMemorySdkJs.EventApi

All URIs are relative to *https://appfloor.in*

Method | HTTP request | Description
------------- | ------------- | -------------
[**event**](EventApi.md#event) | **POST** /api/memory/events | Create Event (Post Content)



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
  'files': ["null"] // [String] | Attach relevant media here, which includes, jpg, mp3, pdf, mp4 files. More than one media can be selected
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

| [**[String]**](String.md)| Attach relevant media here, which includes, jpg, mp3, pdf, mp4 files. More than one media can be selected |

[optional]

### Return type

[**EventResponse**](EventResponse.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

- **Content-Type**: multipart/form-data
- **Accept**: application/json

