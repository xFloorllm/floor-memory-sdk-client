# XfloorFloorMemorySdkJs.QueryApi

All URIs are relative to *https://appfloor.in*

Method | HTTP request | Description
------------- | ------------- | -------------
[**query**](QueryApi.md#query) | **POST** /agent/memory/query | Query (Primary API)



### query

> QueryResponse query(queryRequest)

Query (Primary API)

# **Conversational Query API** This is the **core API** of xfloor. It accepts a natural language query and returns a conversational response derived from: - Content ingested into the specified Floor - The user’s prior conversation history (if provided) - Relevant metadata and context This API is designed for **multi-turn conversations** and can be used to build: - AI chatbots - Knowledge assistants - Floor-specific copilots This API enables **conversational, context-aware querying** over data stored within xfloor. It accepts a natural language query (for example, *“What options do I have in your institute?”*) and returns relevant information derived from the specified floors and their associated content. The API is designed for **multi-turn conversations**. Follow-up questions from the same user automatically build upon prior context, allowing the system to refine, expand, or clarify results across successive calls.

---

### **Core Capabilities**
* Interprets **natural language queries**
* Retrieves relevant information from one or more floors * Applies **time-, type-, and tag-based filters**
* Supports **Top-K retrieval** for result control
* Optionally includes metadata with responses * Can generate **summarized responses** when requested * Maintains **conversation continuity** across multiple queries from the same user

---

### **Authentication & Identity**
* A valid `user_id` is **required**
* User authentication is assumed to be completed **before** calling this API * `app_id` identifies the calling application context * Conversational continuity is maintained **per `user_id`**

> **Note:** All queries from the same `user_id` are treated as part of a single conversational context unless explicitly reset by the application.

---

### **Request Contract**

### **HTTP Method** `POST`

### **Content-Type**

``` application/json

``` > **Important:**

> This API accepts **JSON requests only**. > `multipart/form-data` is **not supported**.

---

### **Request Body (JSON)**

### **Field Descriptions**

| Field | Type | Required | Description |
| ------------------- | ----------------------- | -------- | ---------------------------------------------------------------------------------------------- |
| `user_id` | string | Yes | Unique xfloor user identifier. Used to maintain conversational continuity and personalization. |
| `query` | string | Yes | Natural language query provided by the user. |
| `floor_ids` | array of strings | Yes | List of floor identifiers that define the search scope. Must be provided as a JSON array. |
| `filters` | object | Optional | Additional constraints to narrow search results. |
| `filters.time_from` | string (ISO-8601) | Optional | Start timestamp for filtering content by creation or update time. |
| `filters.time_to` | string (ISO-8601) | Optional | End timestamp for filtering content by creation or update time. |
| `filters.types` | array of strings | Optional | Content types to include (e.g., `post`, `blog`, `forum`). |
| `filters.tags` | array of strings | Optional | Tags used to further refine results. |
| `k` | integer | Optional | Maximum number of results to retrieve (Top-K). Defaults to system-defined behavior if omitted. |
| `include_metadata` | string (`\"0\"` or `\"1\"`) | Optional | Whether to include metadata (source, timestamps, tags) in the response. Defaults to `\"0\"`. |
| `summary_needed` | string (`\"0\"` or `\"1\"`) | Optional | Whether a summarized conversational answer should be generated. Defaults to `\"0\"`. |
| `app_id` | string | Optional | Identifies the application invoking the API. Useful for multi-app integrations. |

---

### **Important Encoding Rules**
* `floor_ids` **must** be provided as a JSON array

```json \"floor_ids\": [\"floor_1\", \"floor_2\"]

``` * Boolean-style flags (`include_metadata`, `summary_needed`) are encoded as **string values**: `\"0\"` or `\"1\"` * `filters` must be provided as a **JSON object**, not a string

---

### **Canonical Request Example**

```json { \"user_id\": \"xf_user_123\", \"query\": \"What options do I have in your institute?\", \"floor_ids\": [\"institute_floor\"], \"filters\": { \"types\": [\"post\", \"blog\"], \"tags\": [\"admissions\"] }, \"k\": 5, \"include_metadata\": \"1\", \"summary_needed\": \"1\", \"app_id\": \"student_portal\" }

```

---

### **Behavior**
1. The query is analyzed using conversational and semantic understanding.
2. Relevant content is retrieved from the specified floors. 3. Filters (time, type, tags) are applied if provided. 4. Results are ranked and limited based on `k`. 5. If `summary_needed = \"1\"`, a synthesized conversational summary is generated. 6. If `include_metadata = \"1\"`, metadata is attached to each result item. 7. The response is returned in a conversational format suitable for follow-up questions.

---

### **Response Contract**

### **High-Level Response Structure**

```json { \"answer\": \"Assistant-generated conversational response\", \"items\": [ { \"id\": \"content_id\", \"type\": \"post\", \"text\": \"Original content snippet\", \"metadata\": { } } ] }

```

---

### **Response Field Semantics**

| Field | Always Present | Description | Rendering Guidance |
| ------------------ | ------------------ | ------------------------------------------- | ---------------------- |
| `answer` | No | Assistant-generated conversational response. Depends on summary_needed. Is present if summary_needed=1 | **Render prominently** |
| `items` | Yes (may be empty) | List of matched content used for grounding | Render optionally |
| `items[].metadata` | Conditional | Included only if `include_metadata = \"1\"` | Render on demand |

> **No-Result Case:**

> If no relevant content is found, `items` will be an empty array and `answer` will contain a conversational fallback response.

---

### **Conversation Continuity**
* Conversation state is maintained **per `user_id`**
* Follow-up queries automatically reference prior context * The API does not require explicit conversation IDs * Applications may reset conversation context by using a new `user_id`

---

### **Error Handling**

 The API may return errors in the following cases:
* Missing or invalid `user_id`
* Empty or unsupported `query` * Invalid or inaccessible `floor_ids` * Authorization or application context errors * Internal processing failures All errors are returned with appropriate HTTP status codes and descriptive messages.

---

### **Typical Use Case Flow**
1. User asks an initial question *“What options do I have in your institute?”*
2. Application calls `/agent/memory/query` 3. Results are displayed to the user 4. User asks a follow-up *“Which ones are available on weekends?”* 5. Application calls the same API again with the new query 6. Conversation continues seamlessly using prior context

---

### **One-Line Summary**

> Executes a conversational query over xfloor content, returning context-aware, filtered, and optionally summarized results with support for multi-turn interactions.

### Example

```javascript
import XfloorFloorMemorySdkJs from '@xfloor/floor-memory-sdk-js';
let defaultClient = XfloorFloorMemorySdkJs.ApiClient.instance;
// Configure Bearer access token for authorization: bearer
let bearer = defaultClient.authentications['bearer'];
bearer.accessToken = "YOUR ACCESS TOKEN"

let apiInstance = new XfloorFloorMemorySdkJs.QueryApi();
let queryRequest = new XfloorFloorMemorySdkJs.QueryRequest(); // QueryRequest | 
apiInstance.query(queryRequest, (error, data, response) => {
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
 **queryRequest**

| [**QueryRequest**](QueryRequest.md)|
|

### Return type

[**QueryResponse**](QueryResponse.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

- **Content-Type**: application/json
- **Accept**: application/json

