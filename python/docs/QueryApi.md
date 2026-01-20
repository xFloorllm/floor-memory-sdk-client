# xfloor_memory_sdk.QueryApi

All URIs are relative to *https://appfloor.in*

Method | HTTP request | Description
------------- | ------------- | -------------
[**query**](QueryApi.md#query) | **POST** /agent/memory/query | Query (Primary API)


# **query**
> QueryResponse query(query_request)

Query (Primary API)

# **Conversational Query API**
This is the **core API** of xfloor.

It accepts a natural language query and returns a conversational response
derived from:
- Content ingested into the specified Floor
- The user’s prior conversation history (if provided)
- Relevant metadata and context

This API is designed for **multi-turn conversations** and can be used
to build:
- AI chatbots
- Knowledge assistants
- Floor-specific copilots

This API enables **conversational, context-aware querying** over data stored within xfloor.

It accepts a natural language query (for example, *“What options do I have in your institute?”*) and returns relevant information derived from the specified floors and their associated content.

The API is designed for **multi-turn conversations**. Follow-up questions from the same user automatically build upon prior context, allowing the system to refine, expand, or clarify results across successive calls.

---

## **Core Capabilities**

* Interprets **natural language queries**
* Retrieves relevant information from one or more floors
* Applies **time-, type-, and tag-based filters**
* Supports **Top-K retrieval** for result control
* Optionally includes metadata with responses
* Can generate **summarized responses** when requested
* Maintains **conversation continuity** across multiple queries from the same user

---

## **Authentication & Identity**

* A valid `user_id` is **required**
* User authentication is assumed to be completed **before** calling this API
* `app_id` identifies the calling application context
* Conversational continuity is maintained **per `user_id`**

> **Note:** All queries from the same `user_id` are treated as part of a single conversational context unless explicitly reset by the application.

---

## **Request Contract**

### **HTTP Method**

`POST`

### **Content-Type**

```
application/json
```

> **Important:**
> This API accepts **JSON requests only**.
> `multipart/form-data` is **not supported**.

---

## **Request Body (JSON)**

### **Field Descriptions**

| Field               | Type                    | Required | Description                                                                                    |
| ------------------- | ----------------------- | -------- | ---------------------------------------------------------------------------------------------- |
| `user_id`           | string                  | Yes      | Unique xfloor user identifier. Used to maintain conversational continuity and personalization. |
| `query`             | string                  | Yes      | Natural language query provided by the user.                                                   |
| `floor_ids`         | array of strings        | Yes      | List of floor identifiers that define the search scope. Must be provided as a JSON array.      |
| `filters`           | object                  | Optional | Additional constraints to narrow search results.                                               |
| `filters.time_from` | string (ISO-8601)       | Optional | Start timestamp for filtering content by creation or update time.                              |
| `filters.time_to`   | string (ISO-8601)       | Optional | End timestamp for filtering content by creation or update time.                                |
| `filters.types`     | array of strings        | Optional | Content types to include (e.g., `post`, `blog`, `forum`).                                      |
| `filters.tags`      | array of strings        | Optional | Tags used to further refine results.                                                           |
| `k`                 | integer                 | Optional | Maximum number of results to retrieve (Top-K). Defaults to system-defined behavior if omitted. |
| `include_metadata`  | string (`"0"` or `"1"`) | Optional | Whether to include metadata (source, timestamps, tags) in the response. Defaults to `"0"`.     |
| `summary_needed`    | string (`"0"` or `"1"`) | Optional | Whether a summarized conversational answer should be generated. Defaults to `"0"`.             |
| `app_id`            | string                  | Optional | Identifies the application invoking the API. Useful for multi-app integrations.                |

---

### **Important Encoding Rules**

* `floor_ids` **must** be provided as a JSON array

  ```json
  "floor_ids": ["floor_1", "floor_2"]
  ```
* Boolean-style flags (`include_metadata`, `summary_needed`) are encoded as **string values**: `"0"` or `"1"`
* `filters` must be provided as a **JSON object**, not a string

---

### **Canonical Request Example**

```json
{
  "user_id": "xf_user_123",
  "query": "What options do I have in your institute?",
  "floor_ids": ["institute_floor"],
  "filters": {
    "types": ["post", "blog"],
    "tags": ["admissions"]
  },
  "k": 5,
  "include_metadata": "1",
  "summary_needed": "1",
  "app_id": "student_portal"
}
```

---

## **Behavior**

1. The query is analyzed using conversational and semantic understanding.
2. Relevant content is retrieved from the specified floors.
3. Filters (time, type, tags) are applied if provided.
4. Results are ranked and limited based on `k`.
5. If `summary_needed = "1"`, a synthesized conversational summary is generated.
6. If `include_metadata = "1"`, metadata is attached to each result item.
7. The response is returned in a conversational format suitable for follow-up questions.

---

## **Response Contract**

### **High-Level Response Structure**

```json
{
  "answer": "Assistant-generated conversational response",
  "items": [
    {
      "id": "content_id",
      "type": "post",
      "text": "Original content snippet",
      "metadata": { }
    }
  ]
}
```

---

### **Response Field Semantics**

| Field              | Always Present     | Description                                 | Rendering Guidance     |
| ------------------ | ------------------ | ------------------------------------------- | ---------------------- |
| `answer`           | Yes                | Assistant-generated conversational response | **Render prominently** |
| `items`            | Yes (may be empty) | List of matched content used for grounding  | Render optionally      |
| `items[].metadata` | Conditional        | Included only if `include_metadata = "1"`   | Render on demand       |

> **No-Result Case:**
> If no relevant content is found, `items` will be an empty array and `answer` will contain a conversational fallback response.

---

## **Conversation Continuity**

* Conversation state is maintained **per `user_id`**
* Follow-up queries automatically reference prior context
* The API does not require explicit conversation IDs
* Applications may reset conversation context by using a new `user_id`

---

## **Error Handling**

The API may return errors in the following cases:

* Missing or invalid `user_id`
* Empty or unsupported `query`
* Invalid or inaccessible `floor_ids`
* Authorization or application context errors
* Internal processing failures

All errors are returned with appropriate HTTP status codes and descriptive messages.

---

## **Typical Use Case Flow**

1. User asks an initial question
   *“What options do I have in your institute?”*
2. Application calls `/agent/memory/query`
3. Results are displayed to the user
4. User asks a follow-up
   *“Which ones are available on weekends?”*
5. Application calls the same API again with the new query
6. Conversation continues seamlessly using prior context

---

## **One-Line Summary**

> Executes a conversational query over xfloor content, returning context-aware, filtered, and optionally summarized results with support for multi-turn interactions.



### Example

* Bearer Authentication (bearer):

```python
import xfloor_memory_sdk
from xfloor_memory_sdk.models.query_request import QueryRequest
from xfloor_memory_sdk.models.query_response import QueryResponse
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
    api_instance = xfloor_memory_sdk.QueryApi(api_client)
    query_request = xfloor_memory_sdk.QueryRequest() # QueryRequest | 

    try:
        # Query (Primary API)
        api_response = api_instance.query(query_request)
        print("The response of QueryApi->query:\n")
        pprint(api_response)
    except Exception as e:
        print("Exception when calling QueryApi->query: %s\n" % e)
```



### Parameters


Name | Type | Description  | Notes
------------- | ------------- | ------------- | -------------
 **query_request** | [**QueryRequest**](QueryRequest.md)|  | 

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
**200** | Primary response payload containing assistant output and retrieved content.  This response represents the successful execution of a **conversational query** processed by the agent.  The API performs:  1. Interpretation of the user’s query 2. Optional retrieval of relevant content (posts/events/blocks) 3. Generation of a final **natural-language answer**  The response contains **two logical parts**:  * **&#x60;answer&#x60;** → the assistant’s final conversational response (what should be shown to the user) * **&#x60;items&#x60;** → the list of retrieved content items that were matched and used (or considered) during answer generation  ---  ## Response Structure  &#x60;&#x60;&#x60;json {   \&quot;answer\&quot;: \&quot;string\&quot;,   \&quot;items\&quot;: [ ... ] } &#x60;&#x60;&#x60;  ---  ## Top-Level Fields  | Field    | Type   | Description                                               | | -------- | ------ | --------------------------------------------------------- | | &#x60;answer&#x60; | String | Final assistant-generated response to the user query      | | &#x60;items&#x60;  | Array  | List of matched content items retrieved during processing |  ---  ## &#x60;answer&#x60;  &#x60;&#x60;&#x60;json \&quot;answer\&quot;: \&quot;non veniam reprehenderit labore\&quot; &#x60;&#x60;&#x60;  ### Description  * This is the **final conversational output** generated by the agent. * It is intended to be **directly rendered** in the chat or UI. * The content may be:    * A direct answer   * A summary   * A synthesized response based on retrieved items  ---  ## &#x60;items[]&#x60; – Retrieved Content Items  Each entry in &#x60;items&#x60; represents a **content block or event** that matched the query.  These items are typically used for:  * Explainability (“why this answer?”) * Debugging or analytics * Showing sources or related content (optional UI)  ---  ### Item Object Structure  &#x60;&#x60;&#x60;json {   \&quot;block_type\&quot;: 25453249,   \&quot;block_id\&quot;: \&quot;96\&quot;,   \&quot;floor_uid\&quot;: \&quot;87\&quot;,   \&quot;event_id\&quot;: \&quot;59\&quot;,   \&quot;text\&quot;: \&quot;Deficio cruentus voluptatem...\&quot;,   \&quot;score\&quot;: -80399794.92417637,   \&quot;block_title\&quot;: \&quot;furthermore separately skeleton...\&quot;,   \&quot;block_details\&quot;: \&quot;Duis magna dolore\&quot;,   \&quot;from_floor_uid\&quot;: \&quot;73\&quot;,   \&quot;user_id\&quot;: \&quot;32\&quot;,   \&quot;match_type\&quot;: \&quot;culpa mollit\&quot; } &#x60;&#x60;&#x60;  ---  ### Item Fields  | Field            | Type   | Description                                                              | | ---------------- | ------ | ------------------------------------------------------------------------ | | &#x60;block_type&#x60;     | Number | Identifier of the block type (e.g., feed, blog, forum, quiz)             | | &#x60;block_id&#x60;       | String | Unique identifier of the block containing the content                    | | &#x60;block_title&#x60;    | String | Title of the block                                                       | | &#x60;block_details&#x60;  | String | Description or metadata associated with the block                        | | &#x60;event_id&#x60;       | String | Identifier of the specific event/post within the block                   | | &#x60;floor_uid&#x60;      | String | Internal floor ID where the content belongs                              | | &#x60;from_floor_uid&#x60; | String | Source floor ID (used when content is derived, federated, or aggregated) | | &#x60;user_id&#x60;        | String | Identifier of the user who created the content                           | | &#x60;text&#x60;           | String | Content text used for matching or retrieval                              | | &#x60;score&#x60;          | Number | Similarity or relevance score assigned by the retrieval system           | | &#x60;match_type&#x60;     | String | Type or category of match (e.g., semantic, keyword, hybrid)              |  ---  ## Interpretation of &#x60;score&#x60;  * Higher relevance is typically indicated by **better score ranking** (interpretation depends on backend logic) * Scores may be positive or negative depending on normalization and similarity model * Clients should **not rely on absolute score values**, only relative ordering  ---  ## Typical Usage Patterns  ### Chat UI  * Display only &#x60;answer&#x60; * Ignore &#x60;items&#x60; unless showing “Sources” or “Related content”  ### Debug / Analytics  * Inspect &#x60;items&#x60; to understand what content influenced the answer * Use &#x60;score&#x60;, &#x60;match_type&#x60;, and block metadata  ### Explainable AI  * Show selected &#x60;items&#x60; as citations or expandable references  ---  ## Notes for Developers  * &#x60;items&#x60; may be an empty array if no relevant content was retrieved * The &#x60;answer&#x60; is always present on success * The order of &#x60;items&#x60; is typically sorted by relevance * Field values and score scales are implementation-specific and may evolve  ---  ## Minimal Mental Model  &gt; **Answer** &#x3D; what the agent says &gt; **Items** &#x3D; what the agent looked at   |  -  |
**422** |  |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to Model list]](../README.md#documentation-for-models) [[Back to README]](../README.md)

