
<a name="watchlists_editwatchlistname"></a>
#### Rename watchlist.
```
PUT /v{version}/users/{userId}/watchlists/{watchlistId}/name
```


##### Description
Renames user watchlist.


##### Parameters

|Type|Name|Description|Schema|Default|
|---|---|---|---|---|
|**Header**|**Authorization**  <br>*required*|Bearer type token string|string||
|**Header**|**Et-App-Key**  <br>*required*|Application key|string||
|**Path**|**userId**  <br>*required*|User identifie|integer (int32)||
|**Path**|**version**  <br>*required*|The requested API version|string|`"1"`|
|**Path**|**watchlistId**  <br>*required*|Watchlist identifier|integer (int32)||
|**Query**|**name**  <br>*required*|New name|string||


##### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|Watchlist id and changed name tuple|[Tuple[Int32,String]](#tuple-int32-string)|
|**401**|Authorization has been denied for this request.|No Content|
|**403**|Application key is not defined or does not exist|No Content|
|**409**|Conflict|No Content|
|**422**|Validation error occurred while processing entity|No Content|
|**500**|Internal server error|No Content|


##### Produces

* `application/json`
* `text/json`


