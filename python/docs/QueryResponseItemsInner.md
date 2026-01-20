# QueryResponseItemsInner

Each item description

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**block_type** | **int** | block type ( 0 or 1) | [optional] 
**block_id** | **str** | Will be a 13 digit unque number which identifies the block | [optional] 
**floor_uid** | **str** | Unique ID given to the floor which cannot be modifed | [optional] 
**event_id** | **str** | Content ID | [optional] 
**text** | **str** | Related content | [optional] 
**score** | **float** | Similarity Score | [optional] 
**block_title** | **str** | Block Title | [optional] 
**block_details** | **str** | Block Details | [optional] 
**from_floor_uid** | **str** | Source floor content | [optional] 
**user_id** | **str** | Author of the content | [optional] 
**match_type** | **str** | Match type text or image | [optional] 

## Example

```python
from xfloor_memory_sdk.models.query_response_items_inner import QueryResponseItemsInner

# TODO update the JSON string below
json = "{}"
# create an instance of QueryResponseItemsInner from a JSON string
query_response_items_inner_instance = QueryResponseItemsInner.from_json(json)
# print the JSON string representation of the object
print(QueryResponseItemsInner.to_json())

# convert the object into a dict
query_response_items_inner_dict = query_response_items_inner_instance.to_dict()
# create an instance of QueryResponseItemsInner from a dict
query_response_items_inner_from_dict = QueryResponseItemsInner.from_dict(query_response_items_inner_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


