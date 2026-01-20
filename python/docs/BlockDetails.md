# BlockDetails

Block Details

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**bid** | **str** | Block ID | 
**type** | **str** | Block Type | 
**title** | **str** | Title of the block | 

## Example

```python
from xfloor_memory_sdk.models.block_details import BlockDetails

# TODO update the JSON string below
json = "{}"
# create an instance of BlockDetails from a JSON string
block_details_instance = BlockDetails.from_json(json)
# print the JSON string representation of the object
print(BlockDetails.to_json())

# convert the object into a dict
block_details_dict = block_details_instance.to_dict()
# create an instance of BlockDetails from a dict
block_details_from_dict = BlockDetails.from_dict(block_details_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


