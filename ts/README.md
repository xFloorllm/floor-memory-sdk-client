# @xfloor/floor-memory-sdk-ts@1.0.22
A TypeScript SDK client for the appfloor.in API.

### Usage

First, install the SDK from npm.

```bash
npm install @xfloor/floor-memory-sdk-ts --save
```

Next, try it out.


```ts
import {
  Configuration,
  AuthApi,
} from '@xfloor/floor-memory-sdk-ts';
import type { ChangeEmailRequest } from '@xfloor/floor-memory-sdk-ts';

async function example() {
  console.log("🚀 Testing @xfloor/floor-memory-sdk-ts SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearer
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new AuthApi(config);

  const body = {
    // string | New Email ID
    newEmailId: newEmailId_example,
    // string | Validation code
    activationCode: activationCode_example,
  } satisfies ChangeEmailRequest;

  try {
    const data = await api.changeEmail(body);
    console.log(data);
  } catch (error) {
    console.error(error);
  }
}

// Run the test
example().catch(console.error);
```


### Documentation

### API Endpoints

All URIs are relative to *https://appfloor.in*

| Class | Method | HTTP request |

Description
| ----- | ------ | ------------ |

-------------
*AuthApi*

| [**changeEmail**](docs/AuthApi.md#changeemail) | **POST** /auth-service/change/email |

Change email ID
*AuthApi*

| [**changeMobileNumber**](docs/AuthApi.md#changemobilenumber) | **POST** /auth-service/change/mobile |

Change Mobile number
*AuthApi*

| [**changePassword**](docs/AuthApi.md#changepassword) | **POST** /auth-service/password/change |

Change Password
*AuthApi*

| [**resetPassword**](docs/AuthApi.md#resetpassword) | **POST** /auth-service/password/reset |

Reset Password
*AuthApi*

| [**sendValidationCode**](docs/AuthApi.md#sendvalidationcode) | **POST** /auth-service/send/validation/code |

Send Validation code
*AuthApi*

| [**signInWithEmail**](docs/AuthApi.md#signinwithemail) | **POST** /auth-service/sign/in/with/email |

Sign In with email ID
*AuthApi*

| [**signInWithMobileNumber**](docs/AuthApi.md#signinwithmobilenumber) | **POST** /auth-service/sign/in/with/mobile/number |

Sign In with Mobile number
*AuthApi*

| [**signUp**](docs/AuthApi.md#signup) | **POST** /auth-service/sign/up |

Sign Up
*AuthApi*

| [**validateCode**](docs/AuthApi.md#validatecode) | **POST** /auth-service/validate/activation/code |

Validation
*EventApi*

| [**event**](docs/EventApi.md#event) | **POST** /api/memory/events |

Create Event (Post Content)
*EventApi*

| [**getRecentEvents**](docs/EventApi.md#getrecentevents) | **GET** /api/memory/recent/events |

Recent Events
*FloorApi*

| [**editFloor**](docs/FloorApi.md#editfloor) | **POST** /api/memory/edit/floor/{floor_id} |

Edit floor
*FloorApi*

| [**getFloorInformation**](docs/FloorApi.md#getfloorinformation) | **GET** /api/memory/floor/info/{floor_id} |

Basic information of a floor
*FloorApi*

| [**makeFloorPrivate**](docs/FloorApi.md#makefloorprivate) | **POST** /api/memory/make/floor/private/{floor_id} |

Make floor Private
*FloorApi*

| [**makeFloorPublic**](docs/FloorApi.md#makefloorpublic) | **POST** /api/memory/make/floor/public/{floor_id} |

Make floor public
*FloorApi*

| [**renameFloor**](docs/FloorApi.md#renamefloor) | **POST** /api/memory/change/floor/id |

Rename floor
*QueryApi*

| [**query**](docs/QueryApi.md#queryoperation) | **POST** /agent/memory/query |

Query (Primary API)


### Models

- [BlockDetails](docs/BlockDetails.md)
- [ChangePassword200Response](docs/ChangePassword200Response.md)
- [EditFloor200Response](docs/EditFloor200Response.md)
- [EditFloor400Response](docs/EditFloor400Response.md)
- [EditFloor400ResponseError](docs/EditFloor400ResponseError.md)
- [Event400Response](docs/Event400Response.md)
- [Event400ResponseError](docs/Event400ResponseError.md)
- [EventResponse](docs/EventResponse.md)
- [FloorInfo](docs/FloorInfo.md)
- [GetRecentEvents200Response](docs/GetRecentEvents200Response.md)
- [GetRecentEvents200ResponseItemsInner](docs/GetRecentEvents200ResponseItemsInner.md)
- [GetRecentEvents200ResponseItemsInnerAuthor](docs/GetRecentEvents200ResponseItemsInnerAuthor.md)
- [GetRecentEvents400Response](docs/GetRecentEvents400Response.md)
- [GetRecentEvents400ResponseError](docs/GetRecentEvents400ResponseError.md)
- [Media](docs/Media.md)
- [Model400ErrorCode](docs/Model400ErrorCode.md)
- [Query422Response](docs/Query422Response.md)
- [Query422ResponseError](docs/Query422ResponseError.md)
- [QueryRequest](docs/QueryRequest.md)
- [QueryRequestFilters](docs/QueryRequestFilters.md)
- [QueryResponse](docs/QueryResponse.md)
- [QueryResponseItemsInner](docs/QueryResponseItemsInner.md)
- [Remaining](docs/Remaining.md)
- [ResetPassword200Response](docs/ResetPassword200Response.md)
- [ResetPassword400Response](docs/ResetPassword400Response.md)
- [SendValidationCode200Response](docs/SendValidationCode200Response.md)
- [SignInResponse](docs/SignInResponse.md)
- [SignUp200Response](docs/SignUp200Response.md)
- [SignUpResponse](docs/SignUpResponse.md)
- [UserDetails](docs/UserDetails.md)
- [UserDetailsPodInfo](docs/UserDetailsPodInfo.md)
- [UserDetailsProfile](docs/UserDetailsProfile.md)
- [UserDetailsProfileAvatar](docs/UserDetailsProfileAvatar.md)
- [ValidateCode400Response](docs/ValidateCode400Response.md)
- [ValidateCode400ResponseError](docs/ValidateCode400ResponseError.md)
- [ValidateCode412Response](docs/ValidateCode412Response.md)

### Authorization


Authentication schemes defined for the API:
<a id="bearer"></a>
#### bearer


- **Type**: HTTP Bearer Token authentication

### About

This TypeScript SDK client supports the [Fetch API](https://fetch.spec.whatwg.org/)
and is automatically generated by the
[OpenAPI Generator](https://openapi-generator.tech) project:

- API version: `1.0.0`
- Package version: `1.0.22`
- Generator version: `7.18.0`
- Build package: `org.openapitools.codegen.languages.TypeScriptFetchClientCodegen`

The generated npm module supports the following:

- Environments
  * Node.js
  * Webpack
  * Browserify
- Language levels
  * ES5 - you must have a Promises/A+ library installed
  * ES6
- Module systems
  * CommonJS
  * ES6 module system

For more information, please visit [https://xfloor.ai/ipomo/blog1551084548304/](https://xfloor.ai/ipomo/blog1551084548304/)

### Development

### Building

To build the TypeScript source code, you need to have Node.js and npm installed.
After cloning the repository, navigate to the project directory and run:

```bash
npm install
npm run build
```

### Publishing

Once you've built the package, you can publish it to npm:

```bash
npm publish
```

### License

[MIT](https://xfloor.ai/ipomo/blog1551084548304/1642341504453)




<!-- xfloor:platform-notes:start -->
## Platform Notes (macOS, Linux, Windows)

### macOS / Linux
```bash
npm install
npm run build
```

### Windows (PowerShell or CMD)
```powershell
npm install
npm run build
```

The npm commands are the same across operating systems. For local path references, use OS-specific path formats:
- macOS/Linux: `/path/to/project`
- Windows: `C:\path\to\project`
<!-- xfloor:platform-notes:end -->
