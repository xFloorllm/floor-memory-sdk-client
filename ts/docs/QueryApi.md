# QueryApi

All URIs are relative to *https://appfloor.in*

| Method | HTTP request | Description |
|------------- | ------------- | -------------|
| [**query**](QueryApi.md#queryoperation) | **POST** /agent/memory/query | Query (Primary API) |



## query

> QueryResponse query(queryRequest)

Query (Primary API)

# **Conversational Query API** This is the **core API** of xfloor.  It accepts a natural language query and returns a conversational response derived from: - Content ingested into the specified Floor - The user’s prior conversation history (if provided) - Relevant metadata and context  This API is designed for **multi-turn conversations** and can be used to build: - AI chatbots - Knowledge assistants - Floor-specific copilots  This API enables **conversational, context-aware querying** over data stored within xfloor.  It accepts a natural language query (for example, *“What options do I have in your institute?”*) and returns relevant information derived from the specified floors and their associated content.  The API is designed for **multi-turn conversations**. Follow-up questions from the same user automatically build upon prior context, allowing the system to refine, expand, or clarify results across successive calls.  ---  ## **Core Capabilities**  * Interprets **natural language queries** * Retrieves relevant information from one or more floors * Applies **time-, type-, and tag-based filters** * Supports **Top-K retrieval** for result control * Optionally includes metadata with responses * Can generate **summarized responses** when requested * Maintains **conversation continuity** across multiple queries from the same user  ---  ## **Authentication &amp; Identity**  * A valid &#x60;user_id&#x60; is **required** * User authentication is assumed to be completed **before** calling this API * &#x60;app_id&#x60; identifies the calling application context * Conversational continuity is maintained **per &#x60;user_id&#x60;**  &gt; **Note:** All queries from the same &#x60;user_id&#x60; are treated as part of a single conversational context unless explicitly reset by the application.  ---  ## **Request Contract**  ### **HTTP Method**  &#x60;POST&#x60;  ### **Content-Type**  &#x60;&#x60;&#x60; application/json &#x60;&#x60;&#x60;  &gt; **Important:** &gt; This API accepts **JSON requests only**. &gt; &#x60;multipart/form-data&#x60; is **not supported**.  ---  ## **Request Body (JSON)**  ### **Field Descriptions**  | Field               | Type                    | Required | Description                                                                                    | | ------------------- | ----------------------- | -------- | ---------------------------------------------------------------------------------------------- | | &#x60;user_id&#x60;           | string                  | Yes      | Unique xfloor user identifier. Used to maintain conversational continuity and personalization. | | &#x60;query&#x60;             | string                  | Yes      | Natural language query provided by the user.                                                   | | &#x60;floor_ids&#x60;         | array of strings        | Yes      | List of floor identifiers that define the search scope. Must be provided as a JSON array.      | | &#x60;filters&#x60;           | object                  | Optional | Additional constraints to narrow search results.                                               | | &#x60;filters.time_from&#x60; | string (ISO-8601)       | Optional | Start timestamp for filtering content by creation or update time.                              | | &#x60;filters.time_to&#x60;   | string (ISO-8601)       | Optional | End timestamp for filtering content by creation or update time.                                | | &#x60;filters.types&#x60;     | array of strings        | Optional | Content types to include (e.g., &#x60;post&#x60;, &#x60;blog&#x60;, &#x60;forum&#x60;).                                      | | &#x60;filters.tags&#x60;      | array of strings        | Optional | Tags used to further refine results.                                                           | | &#x60;k&#x60;                 | integer                 | Optional | Maximum number of results to retrieve (Top-K). Defaults to system-defined behavior if omitted. | | &#x60;include_metadata&#x60;  | string (&#x60;\&quot;0\&quot;&#x60; or &#x60;\&quot;1\&quot;&#x60;) | Optional | Whether to include metadata (source, timestamps, tags) in the response. Defaults to &#x60;\&quot;0\&quot;&#x60;.     | | &#x60;summary_needed&#x60;    | string (&#x60;\&quot;0\&quot;&#x60; or &#x60;\&quot;1\&quot;&#x60;) | Optional | Whether a summarized conversational answer should be generated. Defaults to &#x60;\&quot;0\&quot;&#x60;.             | | &#x60;app_id&#x60;            | string                  | Optional | Identifies the application invoking the API. Useful for multi-app integrations.                |  ---  ### **Important Encoding Rules**  * &#x60;floor_ids&#x60; **must** be provided as a JSON array    &#x60;&#x60;&#x60;json   \&quot;floor_ids\&quot;: [\&quot;floor_1\&quot;, \&quot;floor_2\&quot;]   &#x60;&#x60;&#x60; * Boolean-style flags (&#x60;include_metadata&#x60;, &#x60;summary_needed&#x60;) are encoded as **string values**: &#x60;\&quot;0\&quot;&#x60; or &#x60;\&quot;1\&quot;&#x60; * &#x60;filters&#x60; must be provided as a **JSON object**, not a string  ---  ### **Canonical Request Example**  &#x60;&#x60;&#x60;json {   \&quot;user_id\&quot;: \&quot;xf_user_123\&quot;,   \&quot;query\&quot;: \&quot;What options do I have in your institute?\&quot;,   \&quot;floor_ids\&quot;: [\&quot;institute_floor\&quot;],   \&quot;filters\&quot;: {     \&quot;types\&quot;: [\&quot;post\&quot;, \&quot;blog\&quot;],     \&quot;tags\&quot;: [\&quot;admissions\&quot;]   },   \&quot;k\&quot;: 5,   \&quot;include_metadata\&quot;: \&quot;1\&quot;,   \&quot;summary_needed\&quot;: \&quot;1\&quot;,   \&quot;app_id\&quot;: \&quot;student_portal\&quot; } &#x60;&#x60;&#x60;  ---  ## **Behavior**  1. The query is analyzed using conversational and semantic understanding. 2. Relevant content is retrieved from the specified floors. 3. Filters (time, type, tags) are applied if provided. 4. Results are ranked and limited based on &#x60;k&#x60;. 5. If &#x60;summary_needed &#x3D; \&quot;1\&quot;&#x60;, a synthesized conversational summary is generated. 6. If &#x60;include_metadata &#x3D; \&quot;1\&quot;&#x60;, metadata is attached to each result item. 7. The response is returned in a conversational format suitable for follow-up questions.  ---  ## **Response Contract**  ### **High-Level Response Structure**  &#x60;&#x60;&#x60;json {   \&quot;answer\&quot;: \&quot;Assistant-generated conversational response\&quot;,   \&quot;items\&quot;: [     {       \&quot;id\&quot;: \&quot;content_id\&quot;,       \&quot;type\&quot;: \&quot;post\&quot;,       \&quot;text\&quot;: \&quot;Original content snippet\&quot;,       \&quot;metadata\&quot;: { }     }   ] } &#x60;&#x60;&#x60;  ---  ### **Response Field Semantics**  | Field              | Always Present     | Description                                 | Rendering Guidance     | | ------------------ | ------------------ | ------------------------------------------- | ---------------------- | | &#x60;answer&#x60;           | Yes                | Assistant-generated conversational response | **Render prominently** | | &#x60;items&#x60;            | Yes (may be empty) | List of matched content used for grounding  | Render optionally      | | &#x60;items[].metadata&#x60; | Conditional        | Included only if &#x60;include_metadata &#x3D; \&quot;1\&quot;&#x60;   | Render on demand       |  &gt; **No-Result Case:** &gt; If no relevant content is found, &#x60;items&#x60; will be an empty array and &#x60;answer&#x60; will contain a conversational fallback response.  ---  ## **Conversation Continuity**  * Conversation state is maintained **per &#x60;user_id&#x60;** * Follow-up queries automatically reference prior context * The API does not require explicit conversation IDs * Applications may reset conversation context by using a new &#x60;user_id&#x60;  ---  ## **Error Handling**  The API may return errors in the following cases:  * Missing or invalid &#x60;user_id&#x60; * Empty or unsupported &#x60;query&#x60; * Invalid or inaccessible &#x60;floor_ids&#x60; * Authorization or application context errors * Internal processing failures  All errors are returned with appropriate HTTP status codes and descriptive messages.  ---  ## **Typical Use Case Flow**  1. User asks an initial question    *“What options do I have in your institute?”* 2. Application calls &#x60;/agent/memory/query&#x60; 3. Results are displayed to the user 4. User asks a follow-up    *“Which ones are available on weekends?”* 5. Application calls the same API again with the new query 6. Conversation continues seamlessly using prior context  ---  ## **One-Line Summary**  &gt; Executes a conversational query over xfloor content, returning context-aware, filtered, and optionally summarized results with support for multi-turn interactions.  

### Example

```ts
import {
  Configuration,
  QueryApi,
} from '@xfloor/floor-memory-sdk-ts';
import type { QueryOperationRequest } from '@xfloor/floor-memory-sdk-ts';

async function example() {
  console.log("🚀 Testing @xfloor/floor-memory-sdk-ts SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearer
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new QueryApi(config);

  const body = {
    // QueryRequest
    queryRequest: ...,
  } satisfies QueryOperationRequest;

  try {
    const data = await api.query(body);
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
| **queryRequest** | [QueryRequest](QueryRequest.md) |  | |

### Return type

[**QueryResponse**](QueryResponse.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

- **Content-Type**: `application/json`
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** | Primary response payload containing assistant output and retrieved content.  This response represents the successful execution of a **conversational query** processed by the agent.  The API performs:  1. Interpretation of the user’s query 2. Optional retrieval of relevant content (posts/events/blocks) 3. Generation of a final **natural-language answer**  The response contains **two logical parts**:  * **&#x60;answer&#x60;** → the assistant’s final conversational response (what should be shown to the user) * **&#x60;items&#x60;** → the list of retrieved content items that were matched and used (or considered) during answer generation  ---  ## Response Structure  &#x60;&#x60;&#x60;json {   \&quot;answer\&quot;: \&quot;string\&quot;,   \&quot;items\&quot;: [ ... ] } &#x60;&#x60;&#x60;  ---  ## Top-Level Fields  | Field    | Type   | Description                                               | | -------- | ------ | --------------------------------------------------------- | | &#x60;answer&#x60; | String | Final assistant-generated response to the user query      | | &#x60;items&#x60;  | Array  | List of matched content items retrieved during processing |  ---  ## &#x60;answer&#x60;  &#x60;&#x60;&#x60;json \&quot;answer\&quot;: \&quot;non veniam reprehenderit labore\&quot; &#x60;&#x60;&#x60;  ### Description  * This is the **final conversational output** generated by the agent. * It is intended to be **directly rendered** in the chat or UI. * The content may be:    * A direct answer   * A summary   * A synthesized response based on retrieved items  ---  ## &#x60;items[]&#x60; – Retrieved Content Items  Each entry in &#x60;items&#x60; represents a **content block or event** that matched the query.  These items are typically used for:  * Explainability (“why this answer?”) * Debugging or analytics * Showing sources or related content (optional UI)  ---  ### Item Object Structure  &#x60;&#x60;&#x60;json {   \&quot;block_type\&quot;: 25453249,   \&quot;block_id\&quot;: \&quot;96\&quot;,   \&quot;floor_uid\&quot;: \&quot;87\&quot;,   \&quot;event_id\&quot;: \&quot;59\&quot;,   \&quot;text\&quot;: \&quot;Deficio cruentus voluptatem...\&quot;,   \&quot;score\&quot;: -80399794.92417637,   \&quot;block_title\&quot;: \&quot;furthermore separately skeleton...\&quot;,   \&quot;block_details\&quot;: \&quot;Duis magna dolore\&quot;,   \&quot;from_floor_uid\&quot;: \&quot;73\&quot;,   \&quot;user_id\&quot;: \&quot;32\&quot;,   \&quot;match_type\&quot;: \&quot;culpa mollit\&quot; } &#x60;&#x60;&#x60;  ---  ### Item Fields  | Field            | Type   | Description                                                              | | ---------------- | ------ | ------------------------------------------------------------------------ | | &#x60;block_type&#x60;     | Number | Identifier of the block type (e.g., feed, blog, forum, quiz)             | | &#x60;block_id&#x60;       | String | Unique identifier of the block containing the content                    | | &#x60;block_title&#x60;    | String | Title of the block                                                       | | &#x60;block_details&#x60;  | String | Description or metadata associated with the block                        | | &#x60;event_id&#x60;       | String | Identifier of the specific event/post within the block                   | | &#x60;floor_uid&#x60;      | String | Internal floor ID where the content belongs                              | | &#x60;from_floor_uid&#x60; | String | Source floor ID (used when content is derived, federated, or aggregated) | | &#x60;user_id&#x60;        | String | Identifier of the user who created the content                           | | &#x60;text&#x60;           | String | Content text used for matching or retrieval                              | | &#x60;score&#x60;          | Number | Similarity or relevance score assigned by the retrieval system           | | &#x60;match_type&#x60;     | String | Type or category of match (e.g., semantic, keyword, hybrid)              |  ---  ## Interpretation of &#x60;score&#x60;  * Higher relevance is typically indicated by **better score ranking** (interpretation depends on backend logic) * Scores may be positive or negative depending on normalization and similarity model * Clients should **not rely on absolute score values**, only relative ordering  ---  ## Typical Usage Patterns  ### Chat UI  * Display only &#x60;answer&#x60; * Ignore &#x60;items&#x60; unless showing “Sources” or “Related content”  ### Debug / Analytics  * Inspect &#x60;items&#x60; to understand what content influenced the answer * Use &#x60;score&#x60;, &#x60;match_type&#x60;, and block metadata  ### Explainable AI  * Show selected &#x60;items&#x60; as citations or expandable references  ---  ## Notes for Developers  * &#x60;items&#x60; may be an empty array if no relevant content was retrieved * The &#x60;answer&#x60; is always present on success * The order of &#x60;items&#x60; is typically sorted by relevance * Field values and score scales are implementation-specific and may evolve  ---  ## Minimal Mental Model  &gt; **Answer** &#x3D; what the agent says &gt; **Items** &#x3D; what the agent looked at   |  -  |
| **422** |  |  -  |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)

