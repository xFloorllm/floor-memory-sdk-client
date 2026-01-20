# SignInWithEmail200Response


## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**pod_info** | [**FloorInfo**](FloorInfo.md) |  | 
**profile** | [**SignInWithEmail200ResponseProfile**](SignInWithEmail200ResponseProfile.md) |  | 
**app_id** | **str** | App ID | 

## Example

```python
from xfloor_memory_sdk.models.sign_in_with_email200_response import SignInWithEmail200Response

# TODO update the JSON string below
json = "{}"
# create an instance of SignInWithEmail200Response from a JSON string
sign_in_with_email200_response_instance = SignInWithEmail200Response.from_json(json)
# print the JSON string representation of the object
print(SignInWithEmail200Response.to_json())

# convert the object into a dict
sign_in_with_email200_response_dict = sign_in_with_email200_response_instance.to_dict()
# create an instance of SignInWithEmail200Response from a dict
sign_in_with_email200_response_from_dict = SignInWithEmail200Response.from_dict(sign_in_with_email200_response_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


