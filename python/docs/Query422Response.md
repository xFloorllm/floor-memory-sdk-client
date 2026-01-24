# Query422Response


### Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**error** | [**Query422ResponseError**](Query422ResponseError.md) |  | 

### Example

```python
from xfloor_memory_sdk.models.query422_response import Query422Response

# TODO update the JSON string below
json = "{}"
# create an instance of Query422Response from a JSON string
query422_response_instance = Query422Response.from_json(json)
# print the JSON string representation of the object
print(Query422Response.to_json())

# convert the object into a dict
query422_response_dict = query422_response_instance.to_dict()
# create an instance of Query422Response from a dict
query422_response_from_dict = Query422Response.from_dict(query422_response_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


