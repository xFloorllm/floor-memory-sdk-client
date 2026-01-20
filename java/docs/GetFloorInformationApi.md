# GetFloorInformationApi

All URIs are relative to *https://appfloor.in*

| Method | HTTP request | Description |
|------------- | ------------- | -------------|
| [**getFloorInformation**](GetFloorInformationApi.md#getFloorInformation) | **GET** /api/memory/floor/info/{floor_id} | Basic information of a floor |


<a id="getFloorInformation"></a>
# **getFloorInformation**
> GetFloorInformation200Response getFloorInformation(floorId, userId, appId)

Basic information of a floor

This API returns the **basic profile information of a floor**. It is used to fetch all essential metadata required to **render a floor landing page, header, or navigation context**.  The response includes:  * Floor identity and type * Ownership information relative to the requesting user * Floor metadata (title, description, avatar) * List of blocks available in the floor * App association (for pod / developer use cases)  This API does **not** return posts or content; it only provides **structural and descriptive information** about the floor.  ---  ## Typical Use Cases  * Render floor header (title, logo, description) * Decide UI permissions (owner vs non-owner) * Display available blocks (Feeds, Blog, Quiz, etc.) * Pod discovery or developer-managed floor rendering * Lightweight floor metadata fetch before loading content  ---  ## Authorization &amp; Context  * The API may be called by authenticated or unauthenticated users (depending on floor visibility). * The &#x60;is_owner&#x60; field is calculated **relative to the requesting user context** (if authenticated).  ---  ## Response Format  &#x60;application/json&#x60;  ---  ## Response Structure  ### Top-Level Fields  | Field        | Type                   | Description                                                      | | ------------ | ---------------------- | ---------------------------------------------------------------- | | &#x60;floor_id&#x60;   | String                 | Public, human-readable identifier of the floor                   | | &#x60;floor_uid&#x60;  | String                 | Internal unique identifier of the floor                          | | &#x60;title&#x60;      | String                 | Display title of the floor                                       | | &#x60;details&#x60;    | String                 | Short description or summary of the floor                        | | &#x60;floor_type&#x60; | String                 | Type of floor (&#x60;PUBLIC&#x60;, &#x60;PRIVATE&#x60;, &#x60;POD&#x60;)                       | | &#x60;is_owner&#x60;   | String (&#x60;\&quot;0\&quot;&#x60; / &#x60;\&quot;1\&quot;&#x60;) | Indicates whether the requesting user is the owner               | | &#x60;blocks&#x60;     | Array                  | List of blocks available in the floor                            | | &#x60;avatar&#x60;     | Object                 | Floor logo / avatar metadata                                     | | &#x60;app_id&#x60;     | String                 | Associated application ID (used mainly for pod/developer floors) |  ---  ## Ownership Indicator  ### &#x60;is_owner&#x60;  &#x60;&#x60;&#x60;json \&quot;is_owner\&quot;: \&quot;0\&quot; &#x60;&#x60;&#x60;  | Value | Meaning                                   | | ----- | ----------------------------------------- | | &#x60;\&quot;1\&quot;&#x60; | Requesting user is the owner of the floor | | &#x60;\&quot;0\&quot;&#x60; | Requesting user is not the owner          |  This field is typically used by clients to:  * Enable or disable edit/settings UI * Show owner-only actions  ---  ## Blocks Object  &#x60;&#x60;&#x60;json \&quot;blocks\&quot;: [   {     \&quot;BID\&quot;: \&quot;1765960948723\&quot;,     \&quot;type\&quot;: \&quot;1\&quot;,     \&quot;title\&quot;: \&quot;Feeds\&quot;   } ] &#x60;&#x60;&#x60;  Each block represents a **content category or service** available inside the floor.  ### Block Fields  | Field   | Type   | Description                                           | | ------- | ------ | ----------------------------------------------------- | | &#x60;BID&#x60;   | String | Unique identifier of the block                        | | &#x60;type&#x60;  | String | Block type identifier (e.g., feed, blog, forum, quiz) | | &#x60;title&#x60; | String | Display name of the block                             |  ---  ## Avatar Object  &#x60;&#x60;&#x60;json \&quot;avatar\&quot;: {   \&quot;id\&quot;: \&quot;1767009204367\&quot;,   \&quot;url\&quot;: \&quot;https://...\&quot; } &#x60;&#x60;&#x60;  | Field | Type   | Description                    | | ----- | ------ | ------------------------------ | | &#x60;id&#x60;  | String | Media identifier of the avatar | | &#x60;url&#x60; | String | CDN URL of the floor logo      |  Used to render the floor’s profile image or banner.  ---  ## Floor Type  &#x60;&#x60;&#x60;json \&quot;floor_type\&quot;: \&quot;POD\&quot; &#x60;&#x60;&#x60;  | Value     | Meaning                               | | --------- | ------------------------------------- | | &#x60;PUBLIC&#x60;  | Open floor visible to everyone        | | &#x60;PRIVATE&#x60; | Restricted floor                      | | &#x60;POD&#x60;     | Aggregated or developer-managed floor |  &#x60;POD&#x60; floors are often associated with an &#x60;app_id&#x60; and may aggregate or serve content programmatically.  ---  ## Sample Success Response  &#x60;&#x60;&#x60;json {   \&quot;is_owner\&quot;: \&quot;0\&quot;,   \&quot;blocks\&quot;: [     {       \&quot;BID\&quot;: \&quot;1765960948723\&quot;,       \&quot;type\&quot;: \&quot;1\&quot;,       \&quot;title\&quot;: \&quot;Feeds\&quot;     }   ],   \&quot;floor_uid\&quot;: \&quot;1765960956967\&quot;,   \&quot;floor_id\&quot;: \&quot;raghupodfloor1\&quot;,   \&quot;details\&quot;: \&quot;raghu\&quot;,   \&quot;avatar\&quot;: {     \&quot;id\&quot;: \&quot;1767009204367\&quot;,     \&quot;url\&quot;: \&quot;https://d2e5822u5ecuq8.cloudfront.net/room/1765960956967/logo/1765960956967.jpg\&quot;   },   \&quot;title\&quot;: \&quot;raghu\&quot;,   \&quot;floor_type\&quot;: \&quot;POD\&quot;,   \&quot;app_id\&quot;: \&quot;1765949734005\&quot; } &#x60;&#x60;&#x60;  ---  ## Notes for Developers  * This is a **lightweight metadata API** and is safe to call frequently. * Use this API **before** loading posts or analytics. * &#x60;blocks&#x60; ordering can be used directly for navigation UI. * &#x60;floor_type&#x60; + &#x60;is_owner&#x60; together determine which UI actions are allowed.  ---  ## Common Error Scenarios  ### Floor Not Found  &#x60;&#x60;&#x60;json {   \&quot;status\&quot;: \&quot;ERROR\&quot;,   \&quot;message\&quot;: \&quot;Floor not found\&quot; } &#x60;&#x60;&#x60;  ### Access Restricted  &#x60;&#x60;&#x60;json {   \&quot;status\&quot;: \&quot;ERROR\&quot;,   \&quot;message\&quot;: \&quot;Access denied for this floor\&quot; } &#x60;&#x60;&#x60;  ---  ### Final Mental Model  &gt; **This API answers: “What is this floor, who owns it, and what can I do here?”** 

### Example
```java
// Import classes:
import ai.xfloor.memory.client.ApiClient;
import ai.xfloor.memory.client.ApiException;
import ai.xfloor.memory.client.Configuration;
import ai.xfloor.memory.client.auth.*;
import ai.xfloor.memory.client.models.*;
import ai.xfloor.memory.api.GetFloorInformationApi;

public class Example {
  public static void main(String[] args) {
    ApiClient defaultClient = Configuration.getDefaultApiClient();
    defaultClient.setBasePath("https://appfloor.in");
    
    // Configure HTTP bearer authorization: bearer
    HttpBearerAuth bearer = (HttpBearerAuth) defaultClient.getAuthentication("bearer");
    bearer.setBearerToken("BEARER TOKEN");

    GetFloorInformationApi apiInstance = new GetFloorInformationApi(defaultClient);
    String floorId = "floorId_example"; // String | 
    String userId = "1345896753"; // String | User ID  - 13 digit numeric identity
    String appId = "1387654378"; // String | App ID - 13 digit numeric identity
    try {
      GetFloorInformation200Response result = apiInstance.getFloorInformation(floorId, userId, appId);
      System.out.println(result);
    } catch (ApiException e) {
      System.err.println("Exception when calling GetFloorInformationApi#getFloorInformation");
      System.err.println("Status code: " + e.getCode());
      System.err.println("Reason: " + e.getResponseBody());
      System.err.println("Response headers: " + e.getResponseHeaders());
      e.printStackTrace();
    }
  }
}
```

### Parameters

| Name | Type | Description  | Notes |
|------------- | ------------- | ------------- | -------------|
| **floorId** | **String**|  | |
| **userId** | **String**| User ID  - 13 digit numeric identity | [optional] |
| **appId** | **String**| App ID - 13 digit numeric identity | [optional] |

### Return type

[**GetFloorInformation200Response**](GetFloorInformation200Response.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

 - **Content-Type**: Not defined
 - **Accept**: application/json

### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** |  |  -  |
| **400** |  |  -  |

