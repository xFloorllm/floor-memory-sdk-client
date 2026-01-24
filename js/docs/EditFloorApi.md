# XfloorFloorMemorySdkJs.EditFloorApi

All URIs are relative to *https://appfloor.in*

Method | HTTP request | Description
------------- | ------------- | -------------
[**editFloor**](EditFloorApi.md#editFloor) | **POST** /api/memory/edit/floor/{floor_id} | Edit floor



## editFloor

> GetFloorInformation200Response editFloor(floorId, userId, appId, opts)

Edit floor

This API updates an existing floor’s profile metadata using **multipart form data**. A floor **can be edited only by its owner**. If the authenticated user is **not the owner of the floor**, the request will be rejected, even if the user is a member or follower of the floor. The API allows the floor owner to update:
* Floor **title** * Floor **details/description** * Floor **logo/avatar image** After a successful update, the API returns the **latest floor object**, including the updated avatar and the current list of blocks associated with the floor.

---

## Authorization Rules (Critical)
* The caller **must be authenticated** * The caller **must be the owner of the floor** * Members, followers, or pod consumers **cannot** edit the floor * Ownership is validated internally using the authenticated user context &gt; **Ownership is mandatory. There are no partial permissions for this API.**

---

## Content-Type &#x60;multipart/form-data&#x60;

---

## Request Body (Multipart Form Data)

### Form Fields | Field Name | Type | Required | Description |
| ---------- | ------ | ------------ | ---------------------------------------- |
| &#x60;fid&#x60; | String | Recommended* | Immutable internal floor ID |
| &#x60;floor_id&#x60; | String | Optional* | Public / human-readable floor identifier |
| &#x60;title&#x60; | String | Optional | New floor title |
| &#x60;details&#x60; | String | Optional | New floor description |
| &#x60;logo&#x60; | File | Optional | New floor logo image (PNG/JPG/WebP) |
* At least **one floor identifier** (&#x60;fid&#x60; or &#x60;floor_id&#x60;) must be provided. **Best practice:** Use &#x60;fid&#x60; as the primary identifier.

---

## Update Rules
* At least one of &#x60;title&#x60;, &#x60;details&#x60;, or &#x60;logo&#x60; must be present * Missing update fields result in a validation error * If &#x60;logo&#x60; is provided, the previous logo is replaced

---

## Response Format &#x60;application/json&#x60;

---

## Sample Success Response &#x60;&#x60;&#x60;json { \&quot;floor_id\&quot;: \&quot;my_floor\&quot;, \&quot;title\&quot;: \&quot;daughter ouch upon yummy clamor\&quot;, \&quot;details\&quot;: \&quot;nostrud occaecat incididunt dolor adipisicing\&quot;, \&quot;fid\&quot;: \&quot;86\&quot;, \&quot;blocks\&quot;: [ { \&quot;bid\&quot;: \&quot;83\&quot;, \&quot;type\&quot;: \&quot;pariatur\&quot;, \&quot;title\&quot;: \&quot;wherever demobilise acidly refute\&quot; } ], \&quot;avatar\&quot;: { \&quot;url\&quot;: \&quot;https://legal-availability.name/\&quot;, \&quot;id\&quot;: \&quot;98\&quot; } } &#x60;&#x60;&#x60;

---

## Error Responses (Authorization Focus)

### Not Floor Owner &#x60;&#x60;&#x60;json { \&quot;status\&quot;: \&quot;ERROR\&quot;, \&quot;message\&quot;: \&quot;Only the floor owner can edit this floor\&quot; } &#x60;&#x60;&#x60;

### Floor Not Found &#x60;&#x60;&#x60;json { \&quot;status\&quot;: \&quot;ERROR\&quot;, \&quot;message\&quot;: \&quot;Floor not found\&quot; } &#x60;&#x60;&#x60;

### No Update Fields &#x60;&#x60;&#x60;json { \&quot;status\&quot;: \&quot;ERROR\&quot;, \&quot;message\&quot;: \&quot;No update fields provided\&quot; } &#x60;&#x60;&#x60;

---

## Notes
* This API is **owner-only by design** * Pods and developer tools must operate using **owner credentials** * Blocks are returned for convenience but are **not editable through this API**

---

### Example

```javascript
import XfloorFloorMemorySdkJs from '@xfloor/floor-memory-sdk-js';
let defaultClient = XfloorFloorMemorySdkJs.ApiClient.instance;
// Configure Bearer access token for authorization: bearer
let bearer = defaultClient.authentications['bearer'];
bearer.accessToken = "YOUR ACCESS TOKEN"

let apiInstance = new XfloorFloorMemorySdkJs.EditFloorApi();
let floorId = "floorId_example"; // String | 
let userId = "userId_example"; // String | User ID
let appId = "appId_example"; // String | App ID
let opts = {
  'logoFile': "/path/to/file", // File | Floor avatar
  'title': "title_example", // String | Floor title
  'details': "details_example" // String | Floor decription
};
apiInstance.editFloor(floorId, userId, appId, opts, (error, data, response) => {
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
 **floorId** | **String**|  | 
 **userId** | **String**| User ID | 
 **appId** | **String**| App ID | 
 **logoFile** | **File**| Floor avatar | [optional] 
 **title** | **String**| Floor title | [optional] 
 **details** | **String**| Floor decription | [optional] 

### Return type

[**GetFloorInformation200Response**](GetFloorInformation200Response.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

- **Content-Type**: multipart/form-data
- **Accept**: application/json

