# Threads


### Properties

Name

| Type | Description |

Notes
------------

| ------------- | ------------- |

-------------
**thread_id**

| **str** |
|
**title**

| **str** |
|
**last_updated**

| **str** |
|

### Example

```python
from xfloor_memory_sdk.models.threads import Threads

# TODO update the JSON string below
json = "{}"
# create an instance of Threads from a JSON string
threads_instance = Threads.from_json(json)
# print the JSON string representation of the object
print(Threads.to_json())

# convert the object into a dict
threads_dict = threads_instance.to_dict()
# create an instance of Threads from a dict
threads_from_dict = Threads.from_dict(threads_dict)
```
[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)


