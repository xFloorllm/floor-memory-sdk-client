# QueryApi

All URIs are relative to *https://appfloor.in*

| Method | HTTP request | Description |
|------------- | ------------- | -------------|
| [**query**](QueryApi.md#query) | **POST** /agent/memory/query | Query (Primary API) |


<a id="query"></a>
# **query**
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
| `answer` | Yes | Assistant-generated conversational response | **Render prominently** |
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
```java
// Import classes:
import ai.xfloor.memory.client.ApiClient;
import ai.xfloor.memory.client.ApiException;
import ai.xfloor.memory.client.Configuration;
import ai.xfloor.memory.client.auth.*;
import ai.xfloor.memory.client.models.*;
import ai.xfloor.memory.api.QueryApi;

public class Example {
  public static void main(String[] args) {
    ApiClient defaultClient = Configuration.getDefaultApiClient();
    defaultClient.setBasePath("https://appfloor.in");
    
    // Configure HTTP bearer authorization: bearer
    HttpBearerAuth bearer = (HttpBearerAuth) defaultClient.getAuthentication("bearer");
    bearer.setBearerToken("BEARER TOKEN");

    QueryApi apiInstance = new QueryApi(defaultClient);
    QueryRequest queryRequest = new QueryRequest(); // QueryRequest | 
    try {
      QueryResponse result = apiInstance.query(queryRequest);
      System.out.println(result);
    } catch (ApiException e) {
      System.err.println("Exception when calling QueryApi#query");
      System.err.println("Status code: " + e.getCode());
      System.err.println("Reason: " + e.getResponseBody());
      System.err.println("Response headers: " + e.getResponseHeaders());
      e.printStackTrace();
    }
  }
}
```

### Parameters

| Name | Type | Description | Notes |
|------------- | ------------- | ------------- | -------------|
| **queryRequest** | [**QueryRequest**](QueryRequest.md)|
| |

### Return type

[**QueryResponse**](QueryResponse.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

 - **Content-Type**: application/json
 - **Accept**: application/json

### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** |

Primary response payload containing assistant output and retrieved content. This response represents the successful execution of a **conversational query** processed by the agent. The API performs:
1. Interpretation of the user’s query
2. Optional retrieval of relevant content (posts/events/blocks) 3. Generation of a final **natural-language answer** The response contains **two logical parts**:
* **`answer`** → the assistant’s final conversational response (what should be shown to the user)
* **`items`** → the list of retrieved content items that were matched and used (or considered) during answer generation

---

### Response Structure

```json { \"answer\":

\"string\", \"items\": [ ... ] }

```

---

### Top-Level Fields

| Field | Type | Description |
| -------- | ------ | --------------------------------------------------------- |
| `answer` | String | Final assistant-generated response to the user query |
| `items` | Array | List of matched content items retrieved during processing |

---

### `answer`

```json \"answer\":

\"non veniam reprehenderit labore\"

```

### Description
* This is the **final conversational output** generated by the agent.
* It is intended to be **directly rendered** in the chat or UI. * The content may be:
* A direct answer
* A summary
* A synthesized response based on retrieved items

---

### `items[]` – Retrieved Content Items Each entry in `items` represents a **content block or event** that matched the query.

These items are typically used for:
* Explainability (“why this answer?”)
* Debugging or analytics * Showing sources or related content (optional UI)

---

### Item Object Structure

```json { \"block_type\":

25453249, \"block_id\": \"96\", \"floor_uid\": \"87\", \"event_id\": \"59\", \"text\": \"Deficio cruentus voluptatem...\", \"score\": -80399794.92417637, \"block_title\": \"furthermore separately skeleton...\", \"block_details\": \"Duis magna dolore\", \"from_floor_uid\": \"73\", \"user_id\": \"32\", \"match_type\": \"culpa mollit\" }

```

---

### Item Fields

| Field | Type | Description |
| ---------------- | ------ | ------------------------------------------------------------------------ |
| `block_type` | Number | Identifier of the block type (e.g., feed, blog, forum, quiz) |
| `block_id` | String | Unique identifier of the block containing the content |
| `block_title` | String | Title of the block |
| `block_details` | String | Description or metadata associated with the block |
| `event_id` | String | Identifier of the specific event/post within the block |
| `floor_uid` | String | Internal floor ID where the content belongs |
| `from_floor_uid` | String | Source floor ID (used when content is derived, federated, or aggregated) |
| `user_id` | String | Identifier of the user who created the content |
| `text` | String | Content text used for matching or retrieval |
| `score` | Number | Similarity or relevance score assigned by the retrieval system |
| `match_type` | String | Type or category of match (e.g., semantic, keyword, hybrid) |

---

### Interpretation of `score`
* Higher relevance is typically indicated by **better score ranking** (interpretation depends on backend logic)
* Scores may be positive or negative depending on normalization and similarity model * Clients should **not rely on absolute score values**, only relative ordering

---

### Typical Usage Patterns

### Chat UI
* Display only `answer`
* Ignore `items` unless showing “Sources” or “Related content”

### Debug / Analytics
* Inspect `items` to understand what content influenced the answer
* Use `score`, `match_type`, and block metadata

### Explainable AI
* Show selected `items` as citations or expandable references

---

### Notes for Developers
* `items` may be an empty array if no relevant content was retrieved
* The `answer` is always present on success * The order of `items` is typically sorted by relevance
* Field values and score scales are implementation-specific and may evolve

---

### Minimal Mental Model > **Answer** = what the agent says

> **Items** = what the agent looked at

| - |
| **422** |
|
- |

