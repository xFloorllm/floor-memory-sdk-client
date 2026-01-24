# @xfloor/floor-memory-sdk-ts@1.0.4

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
  DefaultApi,
} from '@xfloor/floor-memory-sdk-ts';
import type { ChangeEmailRequest } from '@xfloor/floor-memory-sdk-ts';

async function example() {
  console.log("🚀 Testing @xfloor/floor-memory-sdk-ts SDK...");
  const config = new Configuration({ 
    // Configure HTTP bearer authorization: bearer
    accessToken: "YOUR BEARER TOKEN",
  });
  const api = new DefaultApi(config);

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

| Class | Method | HTTP request | Description
| ----- | ------ | ------------ | -------------
*DefaultApi* | [**changeEmail**](docs/DefaultApi.md#changeemail) | **POST** /auth-service/change/email | Change email ID
*DefaultApi* | [**changeMobileNumber**](docs/DefaultApi.md#changemobilenumber) | **POST** /auth-service/change/mobile | Change Mobile number
*DefaultApi* | [**changePassword**](docs/DefaultApi.md#changepassword) | **POST** /auth-service/password/change | Change Password
*DefaultApi* | [**makeFloorPrivate**](docs/DefaultApi.md#makefloorprivate) | **POST** /api/memory/make/floor/private | Make floor Private
*DefaultApi* | [**makeFloorPublic**](docs/DefaultApi.md#makefloorpublic) | **POST** /api/memory/make/floor/public | Make floor public
*DefaultApi* | [**registerExternalUserIdentity**](docs/DefaultApi.md#registerexternaluseridentity) | **POST** /memory/identity/external-user | External User Registration
*DefaultApi* | [**renameFloor**](docs/DefaultApi.md#renamefloor) | **POST** /api/memory/change/floor/id | Rename floor
*DefaultApi* | [**resetPassword**](docs/DefaultApi.md#resetpassword) | **POST** /auth-service/password/reset | Reset Password
*DefaultApi* | [**sendValidationCode**](docs/DefaultApi.md#sendvalidationcodeoperation) | **POST** /auth-service/send/validation/code | Send Validation code
*DefaultApi* | [**signInWithEmail**](docs/DefaultApi.md#signinwithemail) | **POST** /auth-service/sign/in/with/email | Sign In with email ID
*DefaultApi* | [**signInWithMobileNumber**](docs/DefaultApi.md#signinwithmobilenumber) | **POST** /auth-service/sign/in/with/mobile/number | Sign In with Mobile number
*DefaultApi* | [**signUp**](docs/DefaultApi.md#signup) | **POST** /auth-service/sign/up | Sign Up
*DefaultApi* | [**validateCode**](docs/DefaultApi.md#validatecodeoperation) | **POST** /auth-service/validate/activation/code | Validation
*EditFloorApi* | [**editFloor**](docs/EditFloorApi.md#editfloor) | **POST** /api/memory/edit/floor/{floor_id} | Edit floor
*EventApi* | [**event**](docs/EventApi.md#event) | **POST** /api/memory/events | Create Event (Post Content)
*GetFloorInformationApi* | [**getFloorInformation**](docs/GetFloorInformationApi.md#getfloorinformation) | **GET** /api/memory/floor/info/{floor_id} | Basic information of a floor
*GetRecentEventsApi* | [**getRecentEvents**](docs/GetRecentEventsApi.md#getrecentevents) | **GET** /api/memory/recent/events | Recent Events
*QueryApi* | [**query**](docs/QueryApi.md#queryoperation) | **POST** /agent/memory/query | Query (Primary API)


### Models

- [BlockDetails](docs/BlockDetails.md)
- [ChangePassword200Response](docs/ChangePassword200Response.md)
- [EditFloor400Response](docs/EditFloor400Response.md)
- [EditFloor400ResponseError](docs/EditFloor400ResponseError.md)
- [Event400Response](docs/Event400Response.md)
- [Event400ResponseError](docs/Event400ResponseError.md)
- [EventResponse](docs/EventResponse.md)
- [FloorInfo](docs/FloorInfo.md)
- [GetFloorInformation200Response](docs/GetFloorInformation200Response.md)
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
- [ResetPassword200Response](docs/ResetPassword200Response.md)
- [ResetPassword400Response](docs/ResetPassword400Response.md)
- [SendValidationCode200Response](docs/SendValidationCode200Response.md)
- [SendValidationCodeRequest](docs/SendValidationCodeRequest.md)
- [SignInWithEmail200Response](docs/SignInWithEmail200Response.md)
- [SignInWithEmail200ResponsePodInfo](docs/SignInWithEmail200ResponsePodInfo.md)
- [SignInWithEmail200ResponseProfile](docs/SignInWithEmail200ResponseProfile.md)
- [SignInWithEmail200ResponseProfileAvatar](docs/SignInWithEmail200ResponseProfileAvatar.md)
- [SignUp200Response](docs/SignUp200Response.md)
- [SignUpResponse](docs/SignUpResponse.md)
- [UserDetails](docs/UserDetails.md)
- [ValidateCode400Response](docs/ValidateCode400Response.md)
- [ValidateCode400ResponseError](docs/ValidateCode400ResponseError.md)
- [ValidateCode412Response](docs/ValidateCode412Response.md)
- [ValidateCodeRequest](docs/ValidateCodeRequest.md)

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
- Package version: `1.0.4`
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
