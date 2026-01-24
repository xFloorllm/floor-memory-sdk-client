# SignInWithEmail200ResponseProfile

User profile details

### Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**floor_id** | **str** | Associated floor ID | 
**fid** | **str** | Unique ID of floor | 
**blocks** | [**List[BlockDetails]**](BlockDetails.md) | List of Blocks | [optional] 
**name** | **str** | User Name | [optional] 
**email** | **str** | Email ID | [optional] 
**mobile_number** | **str** | Mobile number | [optional] 
**user_id** | **str** | Unique User ID | 
**avatar** | [**SignInWithEmail200ResponseProfileAvatar**](SignInWithEmail200ResponseProfileAvatar.md) |  | [optional] 

### Example

```python
from xfloor_memory_sdk.models.sign_in_with_email200_response_profile import SignInWithEmail200ResponseProfile

# TODO update the JSON string below
json = "{}"
# create an instance of SignInWithEmail200ResponseProfile from a JSON string
sign_in_with_email200_response_profile_instance = SignInWithEmail200ResponseProfile.from_json(json)
# print the JSON string representation of the object
print(SignInWithEmail200ResponseProfile.to_json())

# convert the object into a dict
sign_in_with_email200_response_profile_dict = sign_in_with_email200_response_profile_instance.to_dict()
# create an instance of SignInWithEmail200ResponseProfile from a dict
sign_in_with_email200_response_profile_from_dict = SignInWithEmail200ResponseProfile.from_dict(sign_in_with_email200_response_profile_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


