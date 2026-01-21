
# SendValidationCodeRequest


## Properties

Name | Type
------------ | -------------
`userId` | string
`mode` | string
`mobilesNumber` | string
`emailId` | string

## Example

```typescript
import type { SendValidationCodeRequest } from '@xfloor/floor-memory-sdk-ts'

// TODO: Update the object below with actual values
const example = {
  "userId": null,
  "mode": null,
  "mobilesNumber": null,
  "emailId": null,
} satisfies SendValidationCodeRequest

console.log(example)

// Convert the instance to a JSON string
const exampleJSON: string = JSON.stringify(example)
console.log(exampleJSON)

// Parse the JSON string back to an object
const exampleParsed = JSON.parse(exampleJSON) as SendValidationCodeRequest
console.log(exampleParsed)
```

[[Back to top]](#) [[Back to API list]](../README.md#api-endpoints) [[Back to Model list]](../README.md#models) [[Back to README]](../README.md)


