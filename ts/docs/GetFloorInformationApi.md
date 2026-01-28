# GetFloorInformationApi

All URIs are relative to *https://appfloor.in*

| Method | HTTP request | Description |
|------------- | ------------- | -------------|
| [**getFloorInformation**](GetFloorInformationApi.md#getfloorinformation) | **GET** /api/memory/floor/info/{floor_id} | Basic information of a floor |



### getFloorInformation

> GetFloorInformation200Response getFloorInformation(floorId, userId, appId)

Basic information of a floor

This API returns the **basic profile information of a floor**. It is used to fetch all essential metadata required to **render a floor landing page, header, or navigation context**. The response includes:
* Floor identity and type
* Ownership information relative to the requesting user * Floor metadata (title, description, avatar) * List of blocks available in the floor * App association (for pod / developer use cases) This API does **not** return posts or content; it only provides **structural and descriptive information** about the floor.

---

### Typical Use Cases
* Render floor header (title, logo, description)
* Decide UI permissions (owner vs non-owner) * Display available blocks (Feeds, Blog, Quiz, etc.)
* Pod discovery or developer-managed floor rendering
* Lightweight floor metadata fetch before loading content

---

### Authorization & Context
* The API may be called by authenticated or unauthenticated users (depending on floor visibility).
* The `is_owner` field is calculated **relative to the requesting user context** (if authenticated).

---

### Response Format `application/json`

---

### Response Structure

### Top-Level Fields

| Field | Type | Description |
| ------------ | ---------------------- | ---------------------------------------------------------------- |
| `floor_id` | String | Public, human-readable identifier of the floor |
| `floor_uid` | String | Internal unique identifier of the floor |
| `title` | String | Display title of the floor |
| `details` | String | Short description or summary of the floor |
| `floor_type` | String | Type of floor (`PUBLIC`, `PRIVATE`, `POD`) |
| `is_owner` | String (`\"0\"` / `\"1\"`) | Indicates whether the requesting user is the owner |
| `blocks` | Array | List of blocks available in the floor |
| `avatar` | Object | Floor logo / avatar metadata |
| `app_id` | String | Associated application ID (used mainly for pod/developer floors) |

---

### Ownership Indicator

### `is_owner`

```json \"is_owner\":

\"0\"

```

| Value | Meaning |
| ----- | ----------------------------------------- |
| `\"1\"` | Requesting user is the owner of the floor |
| `\"0\"` | Requesting user is not the owner |

This field is typically used by clients to:
* Enable or disable edit/settings UI
* Show owner-only actions

---

### Blocks Object

```json \"blocks\":

[ { \"block_id\": \"1765960948723\", \"type\": \"1\", \"title\": \"Feeds\" } ]

``` Each block represents a **content category or service** available inside the floor.

### Block Fields

| Field | Type | Description |
| ------- | ------ | ----------------------------------------------------- |
| `block_id` | String | Unique identifier of the block |
| `type` | String | Block type identifier (e.g., feed, blog, forum, quiz) |
| `title` | String | Display name of the block |

---

### Avatar Object

```json \"avatar\":

{ \"id\": \"1767009204367\", \"url\": \"https://...\" }

```

| Field | Type | Description |
| ----- | ------ | ------------------------------ |
| `id` | String | Media identifier of the avatar |
| `url` | String | CDN URL of the floor logo |

Used to render the floor’s profile image or banner.

---

### Floor Type

```json \"floor_type\":

\"POD\"

```

| Value | Meaning |
| --------- | ------------------------------------- |
| `PUBLIC` | Open floor visible to everyone |
| `PRIVATE` | Restricted floor |
| `POD` | Aggregated or developer-managed floor |

`POD` floors are often associated with an `app_id` and may aggregate or serve content programmatically.

---

### Sample

Success Response

```json { \"is_owner\":

\"0\", \"blocks\": [ { \"block_id\": \"1765960948723\", \"type\": \"1\", \"title\": \"Feeds\" } ], \"floor_uid\": \"1765960956967\", \"floor_id\": \"raghupodfloor1\", \"details\": \"raghu\", \"avatar\": { \"id\": \"1767009204367\", \"url\": \"https://d2e5822u5ecuq8.cloudfront.net/room/1765960956967/logo/1765960956967.jpg\" }, \"title\": \"raghu\", \"floor_type\": \"POD\", \"app_id\": \"1765949734005\" }

```

---

### Notes for Developers
* This is a **lightweight metadata API** and is safe to call frequently.
* Use this API **before** loading posts or analytics. * `blocks` ordering can be used directly for navigation UI. * `floor_type` + `is_owner` together determine which UI actions are allowed.

---

### Common

Error Scenarios

### Floor Not Found

```json { \"status\":

\"ERROR\", \"message\": \"Floor not found\" }

```

### Access Restricted

```json { \"status\": \"ERROR\", \"message\": \"Access denied for this floor\" }

```

---

### Final Mental Model 

> **This API answers:

“What is this floor, who owns it, and what can I do here?”**

### Example

```ts
import {
  Configuration,
  GetFloorInformationApi,
} from '@xfloor/floor-memory-sdk-ts';
import type { GetFloorInformationRequest } from '@xfloor/floor-memory-sdk-ts';

async function example() {
  console.log("🚀 Testing @xfloor/floor-memory-sdk-ts SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearer
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new GetFloorInformationApi(config);

  const body = {
    // string | 
    floorId: floorId_example,
    // string | User ID  - 13 digit numeric identity (optional)
    userId: 1345896753,
    // string | App ID - 13 digit numeric identity (optional)
    appId: 1387654378,
  } satisfies GetFloorInformationRequest;

  try {
    const data = await api.getFloorInformation(body);
    console.log(data);
  } catch (error) {
    console.error(error);
  }
}

// Run the test
example().catch(console.error);
```

### Parameters


| Name | Type | Description | Notes |
|------------- | ------------- | ------------- | -------------|
| **floorId** | `string` |
| [Defaults to `undefined`] |
| **userId** | `string` | User ID
- 13 digit numeric identity | [Optional] [Defaults to `undefined`] |
| **appId** | `string` | App ID - 13 digit numeric identity | [Optional] [Defaults to `undefined`] |

### Return type

[**GetFloorInformation200Response**](GetFloorInformation200Response.md)

### Authorization

[bearer](../README.md#bearer)

### HTTP request headers

- **Content-Type**: Not defined
- **Accept**: `application/json`


### HTTP response details
| Status code | Description | Response headers |
|-------------|-------------|------------------|
| **200** |
|
- |
| **400** |
|
- |

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)

