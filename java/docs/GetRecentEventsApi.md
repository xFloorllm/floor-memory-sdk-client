# GetRecentEventsApi

All URIs are relative to *https://appfloor.in*

| Method | HTTP request | Description |
|------------- | ------------- | -------------|
| [**getRecentEvents**](GetRecentEventsApi.md#getRecentEvents) | **GET** /api/memory/recent/events | Recent Events |


<a id="getRecentEvents"></a>
# **getRecentEvents**
> GetRecentEvents200Response getRecentEvents(floorId, userId, appId)

Recent Events

This API retrieves the **latest posts (events)** from a specified floor. The behaviour of the API changes based on whether a **user ID** is provided:
* **If &#x60;user_id&#x60; is provided** → The API returns **recent posts relevant to that user**, scoped within the given floor. This includes posts from:
* Floors the user follows
* Floors created by the user
* Pod floors associated with the user (if applicable)
* **If &#x60;user_id&#x60; is NOT provided** → The API returns the **most recent posts available in the specified floor**, without user-specific filtering. This makes the API suitable for:
* Personalized activity feeds * Floor-level public timelines * Pod-based content aggregation * Developer-built pods and custom clients

---

## **Key Concepts**
* A **floor** represents a content space (independent floor, followed floor, or pod floor) * A **pod floor** may aggregate content across multiple related floors * Posts are returned **in reverse chronological order** (latest first) * Each post belongs to a specific **block** within the floor

---

## **Request Method** &#x60;GET&#x60;

---

## **Request Parameters (Query Params)** | Parameter Name | Type | Required | Description |
| -------------- | ------ | -------- | -------------------------------------------------------------------------------------------------------------------------- |
| &#x60;floor_id&#x60; | String | **Yes** | Floor identifier from which events should be fetched. Can be a pod floor ID, followed floor ID, or an independent floor ID |
| &#x60;user_id&#x60; | String | No | If provided, returns posts relevant to the user within the given floor |
| &#x60;app_id&#x60; | String | No | Identifier for external developers or pod-based applications consuming this API |

---

## **Behavior Summary** | Scenario | Result |
| ---------------------- | ----------------------------------------- |
| &#x60;floor_id&#x60; only | Latest posts from the specified floor |
| &#x60;floor_id&#x60; + &#x60;user_id&#x60; | User-relevant posts within that floor |
| Pod floor ID | Aggregated posts across pod-linked floors |
| Independent floor ID | Posts only from that floor |

---

## **Response Format** &#x60;application/json&#x60;

---

## **Response Structure**

### **Top-Level Fields** | Field | Type | Description |
| ------------ | ------ | ------------------------------ |
| &#x60;post_count&#x60; | String | Total number of posts returned |
| &#x60;items&#x60; | Array | List of recent post objects |

---

### **Post Object (&#x60;items[]&#x60;)** | Field | Type | Description |
| --------------- | ------ | ------------------------------------------------------------------------- |
| &#x60;event_id&#x60; | String | Unique identifier of the post/event |
| &#x60;block_type&#x60; | String | Type of block where the post was created (e.g., blog, forum, audio, etc.) |
| &#x60;block_id&#x60; | String | Identifier of the block within the floor |
| &#x60;floor_uid&#x60; | String | Floor identifier where the post belongs |
| &#x60;title&#x60; | String | Title of the post (may be empty) |
| &#x60;text&#x60; | String | Text or HTML content of the post |
| &#x60;media&#x60; | Array | Media objects (audio, image, etc.), if any |
| &#x60;created_at_ms&#x60; | String | Post creation time in milliseconds (epoch) |

---

### **Author Object** | Field | Type | Description |
| ----------- | ------ | ---------------------------- |
| &#x60;name&#x60; | String | Display name of the author |
| &#x60;floor_uid&#x60; | String | Author’s floor/user handle |
| &#x60;avatar&#x60; | Object | Author profile image details |

---

### **Media Object** | Field | Type | Description |
| ------ | ------ | ----------------------------------- |
| &#x60;type&#x60; | String | Media type (e.g., &#x60;AUDIO&#x60;, &#x60;IMAGE&#x60;) |
| &#x60;url&#x60; | String | Public URL of the media file |

---

## **Sample Success Response** *(structure abbreviated for clarity)* &#x60;&#x60;&#x60;json { \&quot;post_count\&quot;: \&quot;18\&quot;, \&quot;items\&quot;: [ { \&quot;event_id\&quot;: \&quot;1766557274836\&quot;, \&quot;block_type\&quot;: \&quot;0\&quot;, \&quot;title\&quot;: \&quot;voice-note-1766557272764.wav\&quot;, \&quot;text\&quot;: \&quot;You\&quot;, \&quot;created_at_ms\&quot;: \&quot;1766557275000\&quot;, \&quot;author\&quot;: { \&quot;name\&quot;: \&quot;MEGHANA G\&quot;, \&quot;floor_uid\&quot;: \&quot;meghanag\&quot;, \&quot;avatar\&quot;: { \&quot;type\&quot;: \&quot;IMAGE\&quot;, \&quot;url\&quot;: \&quot;https://...\&quot; } }, \&quot;media\&quot;: [ { \&quot;type\&quot;: \&quot;AUDIO\&quot;, \&quot;url\&quot;: \&quot;https://...\&quot; } ] } ] } &#x60;&#x60;&#x60;

---

## **Notes**
* Posts may contain **plain text or HTML** * Media is optional and may be absent * Ordering is **latest first** * The API is read-only and does not require authentication by default * Access control (public/private floors) is enforced internally

---

## **Typical Use Cases**
* Floor activity feed * Pod-level dashboards * User-personalized timelines * Public floor landing pages * External developer pods using &#x60;app_id&#x60;

### Example
```java
// Import classes:
import ai.xfloor.memory.client.ApiClient;
import ai.xfloor.memory.client.ApiException;
import ai.xfloor.memory.client.Configuration;
import ai.xfloor.memory.client.auth.*;
import ai.xfloor.memory.client.models.*;
import ai.xfloor.memory.api.GetRecentEventsApi;

public class Example {
  public static void main(String[] args) {
    ApiClient defaultClient = Configuration.getDefaultApiClient();
    defaultClient.setBasePath("https://appfloor.in");
    
    // Configure HTTP bearer authorization: bearer
    HttpBearerAuth bearer = (HttpBearerAuth) defaultClient.getAuthentication("bearer");
    bearer.setBearerToken("BEARER TOKEN");

    GetRecentEventsApi apiInstance = new GetRecentEventsApi(defaultClient);
    String floorId = "floorId_example"; // String | 
    String userId = "userId_example"; // String | 
    String appId = "appId_example"; // String | 
    try {
      GetRecentEvents200Response result = apiInstance.getRecentEvents(floorId, userId, appId);
      System.out.println(result);
    } catch (ApiException e) {
      System.err.println("Exception when calling GetRecentEventsApi#getRecentEvents");
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
| **userId** | **String**|  | [optional] |
| **appId** | **String**|  | [optional] |

### Return type

[**GetRecentEvents200Response**](GetRecentEvents200Response.md)

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

