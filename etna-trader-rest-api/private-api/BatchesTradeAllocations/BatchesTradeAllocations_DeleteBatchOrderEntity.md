
<a name="batchestradeallocations_deletebatchorderentity"></a>
#### Delete batch allocation entity
```
DELETE /v{version}/batches/{batchId}/allocations/{entityId}
```


##### Description
Delete batch allocation entity


##### Parameters

|Type|Name|Description|Schema|Default|
|---|---|---|---|---|
|**Header**|**Authorization**  <br>*required*|Bearer type token string|string||
|**Header**|**Et-App-Key**  <br>*required*|Application key|string||
|**Path**|**batchId**  <br>*required*|Order batch identifier|integer (int32)||
|**Path**|**entityId**  <br>*required*|Batch allocation entity identifier|integer (int32)||
|**Path**|**version**  <br>*required*|The requested API version|string|`"1"`|


##### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|OK|object|
|**204**|Batch allocation entity was successfully deleted|No Content|
|**401**|Authorization has been denied for this request.|No Content|
|**403**|Application key is not defined or does not exist|No Content|
|**409**|Conflict|No Content|
|**422**|Validation error occurred while processing entity|No Content|
|**500**|Internal server error|No Content|


##### Produces

* `application/json`
* `text/json`



