# EventApi

All URIs are relative to *https://appfloor.in*

| Method | HTTP request | Description |
|------------- | ------------- | -------------|
| [**event**](EventApi.md#event) | **POST** /api/memory/events | Create Event (Post Content) |



## event

> EventResponse event(inputInfo, files)

Create Event (Post Content)

Posts into the given floor_id. This is asynchronous ingestion. 200 OK means queued, not immediately retrievable. This API allows a user to **post personal content into their POD (Personal Object Database)**. The posted content is stored under a specified **floor**, embedded by the platform, and made available for **semantic querying, conversational retrieval, and memory-based interactions**.  It is primarily used to:  * Save reminders, notes, writeups, or personal knowledge * Upload content that the user wants the system to remember * Add information that should later be discoverable via conversational queries  The content may consist of **text only** or **text combined with one or more media files**.  ---  ## **Key Capabilities**  * Stores user-generated content inside a specific floor * Supports **multi-modal inputs** (text + media) * Automatically embeds content for semantic search * Makes content available to:    * &#x60;/agent/memory/query&#x60;   * conversational agents   * future recall and analytics * Associates content with user, block, and application context  ---  ## **Authentication**  * Requires a valid, authenticated &#x60;user_id&#x60; * The calling application is responsible for user authentication * &#x60;app_id&#x60; identifies the application context  ---  ## **Request Type**  **Content-Type:** &#x60;multipart/form-data&#x60;  ---  ## **Request Parameters**  ### **1. Files (Optional)**  | Field   | Type   | Required | Description                                                           | | ------- | ------ | -------- | --------------------------------------------------------------------- | | &#x60;files&#x60; | file[] | Optional | Media files to attach to the content. Multiple files may be uploaded. |  **Supported formats include (but are not limited to):**  * Images: &#x60;jpg&#x60;, &#x60;png&#x60; * Audio: &#x60;mp3&#x60; * Documents: &#x60;pdf&#x60; * Video: &#x60;mp4&#x60;  These files are processed and embedded along with the textual content where applicable.  ---  ### **2. Input Information (Required)**  | Field        | Type          | Required | Description                                                       | | ------------ | ------------- | -------- | ----------------------------------------------------------------- | | &#x60;input_info&#x60; | string (JSON) | Yes      | JSON string containing metadata and textual content for the post. |  ---  ## **&#x60;input_info&#x60; Structure**  &#x60;&#x60;&#x60;json {   \&quot;floor_id\&quot;: \&quot;my_floor\&quot;,   \&quot;BID\&quot;: \&quot;17845683456\&quot;,   \&quot;user_id\&quot;: \&quot;145623907625\&quot;,   \&quot;title\&quot;: \&quot;My floor\&quot;,   \&quot;description\&quot;: \&quot;My floor details\&quot;,   \&quot;app_id\&quot;: \&quot;165434879028\&quot; } &#x60;&#x60;&#x60;  ---  ### **Field Descriptions**  | Field         | Type   | Required | Description                                                                        | | ------------- | ------ | -------- | ---------------------------------------------------------------------------------- | | &#x60;floor_id&#x60;    | string | Yes      | Identifier of the user’s floor (POD) where the content will be stored.             | | &#x60;block_type&#x60;  | string | Yes      | Type of block under which the content is categorized (e.g., post, note, reminder). | | &#x60;BID&#x60;         | string | Yes      | Block identifier associated with this content.                                     | | &#x60;user_id&#x60;     | string | Yes      | Unique identifier of the user posting the content.                                 | | &#x60;title&#x60;       | string | Optional | Title or short heading for the content.                                            | | &#x60;description&#x60; | string | Yes      | Main textual content to be stored and embedded.                                    | | &#x60;app_id&#x60;      | string | Optional | Identifier of the calling application.                                             |  ---  ## **Behavior**  1. The API validates the user and floor context. 2. Textual content (&#x60;title&#x60; and &#x60;description&#x60;) is ingested. 3. Attached media files are processed and linked to the content. 4. Embeddings are generated for:     * Text    * Supported media (where applicable) 5. The content becomes part of the user’s **personal memory store**. 6. The stored data is immediately available for querying and conversational retrieval.  ---  ## **Successful Response**  On success, the API confirms that:  * The content has been stored * Embeddings have been generated * The memory item is available for future queries  A success status and reference identifiers are returned.  ---  ## **Error Handling**  The API may return errors if:  * Required fields are missing (&#x60;floor_id&#x60;, &#x60;user_id&#x60;, &#x60;description&#x60;) * Unsupported file formats are uploaded * The user does not have access to the specified floor * The request payload is malformed * Internal embedding or storage operations fail  ---  ## **Typical Use Cases**  * Saving personal reminders * Posting notes or observations * Uploading documents for future reference * Creating a personal knowledge base * Feeding data into conversational agents  ---  ## **One-Line Summary**  &gt; Stores user-generated text and media into a personal POD, embeds it for semantic search, and makes it available for conversational querying.  ⚠️ Content Ingestion is Asynchronous  The Create Event API queues content for processing. A successful response indicates **acceptance**, not availability.  Newly ingested content may take time to become searchable via the Query API.  

### Example

```ts
import {
  Configuration,
  EventApi,
} from '@xfloor/floor-memory-sdk-ts';
import type { EventRequest } from '@xfloor/floor-memory-sdk-ts';

async function example() {
  console.log("🚀 Testing @xfloor/floor-memory-sdk-ts SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearer
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new EventApi(config);

  const body = {
    // string | Input parameters, bid is optional
    inputInfo: inputInfo_example,
    // Blob | Attach relevant media here, which includes, jpg, mp3, pdf, mp4 files. More than one media can be selected (optional)
    files: BINARY_DATA_HERE,
  } satisfies EventRequest;

  try {
    const data = await api.event(body);
    console.log(data);
  } catch (error) {
    console.error(error);
  }
}

// Run the test
example().catch(console.error);
```

### Parameters


| Name | Type | Description  | Notes |
|------------- | ------------- | ------------- | -------------|
| **inputInfo** | `string` | Input parameters, bid is optional | [Defaults to `undefined`] |
| **files** | `Blob` | Attach relevant media here, which includes, jpg, mp3, pdf, mp4 files. More than one media can be selected | [Optional] [Defaults to `undefined`] |

### Return type

[**EventResponse**](EventResponse.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

- **Content-Type**: `multipart/form-data`
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | ## **Successful Response (200 OK)**  This API follows an **asynchronous ingestion model**.  On success, the API **confirms acceptance of the content**, but **does not guarantee immediate availability** for retrieval or querying.  ### **What the response means**  A &#x60;200 OK&#x60; response indicates that:  * The request payload is valid * The content has been **accepted and queued** for processing * The content has been published to the internal event pipeline (RabbitMQ) * Embedding and storage will occur asynchronously  ⚠️ **Important:** The newly posted content **will not appear immediately** in query or feed APIs.  ---  ## **Response Body (Example)**  &#x60;&#x60;&#x60;json {   \&quot;status\&quot;: \&quot;success\&quot;,   \&quot;message\&quot;: \&quot;Content accepted for processing\&quot; } &#x60;&#x60;&#x60;  &gt; No content data is returned in this response.  ---  ## **Availability &amp; Retrieval Model**  After receiving a successful response:  1. The content is processed asynchronously 2. The content becomes available in the floor feed **after processing completes** 3. Developers must retrieve the content using:  &#x60;&#x60;&#x60; GET /api/memory/recent/events &#x60;&#x60;&#x60;  ---  ## **Polling Requirement**  Because ingestion is asynchronous:  * Developers **must poll** &#x60;/api/memory/recent/events&#x60; * Polling should be done using:    * &#x60;floor_id&#x60;   * timestamp or last-known event marker * Compare previously retrieved events with new responses to detect newly added content  This design ensures:  * High ingestion throughput * Non-blocking uploads * Reliable embedding and storage pipelines  ---  ## **Typical Developer Flow**  &#x60;&#x60;&#x60;text POST /api/memory/events         ↓ 200 OK (content queued)         ↓ Poll /api/memory/recent/events         ↓ Detect new event         ↓ Use content in /agent/memory/query &#x60;&#x60;&#x60;  ---  ## **Key Design Note (Why This Exists)**  This API is intentionally asynchronous to:  * Support large files and multi-modal uploads * Avoid request timeouts during embedding * Enable scalable background processing * Keep write latency low  ---  ## **One-Line Summary**  &gt; Accepts user-generated text and media, queues it for asynchronous processing, and makes it available for retrieval via the recent events API after ingestion completes. |  -  |
| **400** |  |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)

