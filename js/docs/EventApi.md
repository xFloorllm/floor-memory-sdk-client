# XfloorFloorMemorySdkJs.EventApi

All URIs are relative to *https://appfloor.in*

Method | HTTP request | Description
------------- | ------------- | -------------
[**event**](EventApi.md#event) | **POST** /api/memory/events | Create Event (Post Content)



### event

> EventResponse event(inputInfo, opts)

Create Event (Post Content)

Posts into the given floor_id. This is asynchronous ingestion. 200 OK means queued, not immediately retrievable. This API allows a user to **post personal content into their POD (Personal Object Database)**. The posted content is stored under a specified **floor**, embedded by the platform, and made available for **semantic querying, conversational retrieval, and memory-based interactions**. It is primarily used to:
* Save reminders, notes, writeups, or personal knowledge * Upload content that the user wants the system to remember * Add information that should later be discoverable via conversational queries The content may consist of **text only** or **text combined with one or more media files**.

---

### **Key Capabilities**
* Stores user-generated content inside a specific floor * Supports **multi-modal inputs** (text + media) * Automatically embeds content for semantic search * Makes content available to:
* `/agent/memory/query`
* conversational agents
* future recall and analytics * Associates content with user, block, and application context

---

### **Authentication**
* Requires a valid, authenticated `user_id` * The calling application is responsible for user authentication * `app_id` identifies the application context

---

### **Request Type** **Content-Type:** `multipart/form-data`

---

### **Request Parameters**

### **1. Files (Optional)** | Field | Type | Required | Description |
| ------- | ------ | -------- | --------------------------------------------------------------------- |
| `files` | file[] | Optional | Media files to attach to the content. Multiple files may be uploaded. | **Supported formats include (but are not limited to):**
* Images: `jpg`, `png` * Audio: `mp3` * Documents: `pdf` * Video: `mp4` These files are processed and embedded along with the textual content where applicable.

---

### **2. Input Information (Required)** | Field | Type | Required | Description |
| ------------ | ------------- | -------- | ----------------------------------------------------------------- |
| `input_info` | string (JSON) | Yes | JSON string containing metadata and textual content for the post. |

---

### **`input_info` Structure**

```json { \"floor_id\": \"my_floor\", \"BID\": \"17845683456\", \"user_id\": \"145623907625\", \"title\": \"My floor\", \"description\": \"My floor details\", \"app_id\": \"165434879028\" } ```

---

### **Field Descriptions** | Field | Type | Required | Description |
| ------------- | ------ | -------- | ---------------------------------------------------------------------------------- |
| `floor_id` | string | Yes | Identifier of the user’s floor (POD) where the content will be stored. |
| `block_type` | string | Yes | Type of block under which the content is categorized (e.g., post, note, reminder). |
| `BID` | string | Yes | Block identifier associated with this content. |
| `user_id` | string | Yes | Unique identifier of the user posting the content. |
| `title` | string | Optional | Title or short heading for the content. |
| `description` | string | Yes | Main textual content to be stored and embedded. |
| `app_id` | string | Optional | Identifier of the calling application. |

---

### **Behavior**
1. The API validates the user and floor context. 2. Textual content (`title` and `description`) is ingested. 3. Attached media files are processed and linked to the content. 4. Embeddings are generated for:
* Text
* Supported media (where applicable) 5. The content becomes part of the user’s **personal memory store**. 6. The stored data is immediately available for querying and conversational retrieval.

---

### **Successful Response** On success, the API confirms that:
* The content has been stored * Embeddings have been generated * The memory item is available for future queries A success status and reference identifiers are returned.

---

### **Error Handling** The API may return errors if:
* Required fields are missing (`floor_id`, `user_id`, `description`) * Unsupported file formats are uploaded * The user does not have access to the specified floor * The request payload is malformed * Internal embedding or storage operations fail

---

### **Typical Use Cases**
* Saving personal reminders * Posting notes or observations * Uploading documents for future reference * Creating a personal knowledge base * Feeding data into conversational agents

---

### **One-Line Summary** > Stores user-generated text and media into a personal POD, embeds it for semantic search, and makes it available for conversational querying. ⚠️ Content Ingestion is Asynchronous The Create Event API queues content for processing. A successful response indicates **acceptance**, not availability. Newly ingested content may take time to become searchable via the Query API.

### Example

```javascript
import XfloorFloorMemorySdkJs from '@xfloor/floor-memory-sdk-js';
let defaultClient = XfloorFloorMemorySdkJs.ApiClient.instance;
// Configure Bearer access token for authorization: bearer
let bearer = defaultClient.authentications['bearer'];
bearer.accessToken = "YOUR ACCESS TOKEN"

let apiInstance = new XfloorFloorMemorySdkJs.EventApi();
let inputInfo = "inputInfo_example"; // String | Input parameters, bid is optional
let opts = {
  'files': "/path/to/file" // File | Attach relevant media here, which includes, jpg, mp3, pdf, mp4 files. More than one media can be selected
};
apiInstance.event(inputInfo, opts, (error, data, response) => {
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
 **inputInfo** | **String**| Input parameters, bid is optional | 
 **files** | **File**| Attach relevant media here, which includes, jpg, mp3, pdf, mp4 files. More than one media can be selected | [optional] 

### Return type

[**EventResponse**](EventResponse.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

- **Content-Type**: multipart/form-data
- **Accept**: application/json

