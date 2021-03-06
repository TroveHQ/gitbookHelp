# Syntax

## Get price alerts

```text
GET /v{version}/users/{userId}/pricealerts
```

### Description

This API endpoint enables you to retrieve all price alerts of a specific user.

### Parameters

| Type | Name | Description | Schema | Default |
| :--- | :--- | :--- | :--- | :--- |
| **Header** | **Authorization**   _required_ | This is the authorization token that you retrieved from the first endpoint \(/token\). | string |  |
| **Header** | **Et-App-Key**   _required_ | This is your app’s unique key that can be retrieved from the BO Companies widget in ETNA Trader. | string |  |
| **Path** | **userId**   _required_ | This is the internal identifier of the user whose price alerts must be retrieved. | integer \(int32\) |  |
| **Path** | **version**   _required_ | This is the version of the API. Unless you have multiple versions of ETNA Trader’s API deployed in your environment, leave it at 1.0. | string | `"1"` |
| **Query** | **isDesc**   _required_ | This is a boolean field that indicates if the returned price alerts should be sorted in  descending \(true\) or ascending \(false\) order. | boolean |  |
| **Query** | **pageNumber**   _required_ | This is the page number \(all price alerts are split into pages\). | integer \(int32\) |  |
| **Query** | **pageSize**   _required_ | This is the number of price alerts that should be retrieved from the specified page. | integer \(int32\) |  |
| **Query** | **sortBy**   _required_ | Sorting field | string |  |

### Responses

| HTTP Code | Description | Schema |
| :--- | :--- | :--- |
| **200** | Successful request, JSON data containing the user’s price alerts is returned. | [PagingResult\[PriceAlertInfoModel\]](pricealerts_getpricealerts.md#pagingresult-pricealertinfomodel) |
| **401** | The access level of the provided authorization token is not sufficient to perform this operation. | No Content |
| **403** | The provided Et-App-Key is incorrect. | No Content |
| **422** | A validation error occurred while processing the request. | No Content |
| **500** | Internal server error | No Content |

### Produces

* `application/json`
* `text/json`

