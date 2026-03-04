# EditFloor200Response


### Properties

Name

| Type | Description |

Notes
------------

| ------------- | ------------- |

-------------
**floor_id**

| **str** | Pod floor ID |
**title**

| **str** | Title |
**details**

| **str** | Brief description about the Pod floor |

[optional]
**floor_uid**

| **str** | Unique numeric ID of the pod floor |
**blocks**

| [**List[BlockDetails]**](BlockDetails.md) | List of blocks |

[optional]
**avatar**

| [**Media**](Media.md) |
|

[optional]
**is_owner**

| **str** | Is the user Owner |
**floor_type**

| **str** | Type of floor (POD, PUBLIC or PRIVATE) |
**app_id**

| **str** | Optional - Applicable only if pod is present. |

[optional]

### Example

```python
from xfloor_memory_sdk.models.edit_floor200_response import EditFloor200Response

# TODO update the JSON string below
json = "{}"
# create an instance of EditFloor200Response from a JSON string
edit_floor200_response_instance = EditFloor200Response.from_json(json)
# print the JSON string representation of the object
print(EditFloor200Response.to_json())

# convert the object into a dict
edit_floor200_response_dict = edit_floor200_response_instance.to_dict()
# create an instance of EditFloor200Response from a dict
edit_floor200_response_from_dict = EditFloor200Response.from_dict(edit_floor200_response_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


