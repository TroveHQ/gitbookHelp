# Validate Order Placement

### Overview

This POST endpoint enables you to validate an order before placing it in ETNA Trader. This might be useful for ensuring that the user has properly constructed an order and prevent any issues related with defective orders.

{% hint style="warning" %}
In order to validate an order, you must use an [authorization token](../../public-api/authentication/requesting-tokens/) of an administrator. Using authorization tokens of regular users will lead to the 401 status code.
{% endhint %}

There are five required parameters that must be provided in the request:

1. **Et-App-Key** \(header\). This is the unique key of your app that identifies your app when communicating with our service. It can be found it in the **BO Companies** widget. When editing the company's settings, navigate to the **WebApi** tab and look for the required key \(it could be a key for the web terminal, the mobile app, or a custom key\). 
2. **Authorization** \(header\). This is the authorization token from the very first [token request](../../public-api/authentication/requesting-tokens/).
3. **API version** \(path\). Unless necessary, leave it at "1.0".
4. **Trading Account ID** \(path\). This is the numeric ID of the trading account on which an existing order replacement must be validated.
5. **placeParams** \(body\). This is a JSON file that contains the parameters of a new order that must be validated.

Here's the final template for this API request:

```text
POST apiURL/v1.0/accounts/{accountID}/preview/orders
```

### Request Body

The body of this request represents the information of the new order that must be validated before you can proceed to place it. The order must be sent in the JSON format with mandatory parameters about the order.

The first five parameters — **Symbol**, **Quantity**, **Type**, and **Side** — are mandatory, while the remaining parameters should only be provided if necessary.

#### Order Modification Validation Sample

```javascript
{
  "Symbol": "VMSFT",
  "Type": "Market",
  "Side": "Buy",
  "Quantity": 8
}
```

### Response

In response to this request, you'll receive a JSON file confirming \(or rejecting\) that the new order has been properly constructed.

```javascript
{
  "IsSuccessful": true,
  "Commission": 3.75,
  "Commissions": {
    "Per Trade Commission": 3.75
  },
  "Cost": 169000,
  "NetCost": 168996.25,
  "Quotes": [
    {
      "Ask": 184,
      "Bid": 175.76,
      "Last": 175.875,
      "Volume": 1,
      "OpenInterest": 0
    }
  ],
  "MarginChange": 16900
}
```

where:

| Parameter | Description |
| :--- | :--- |
| IsSuccessful | This field indicates if the order has been successfully constructed. |
| Commission | This is the total commission applicable to the order. |
| Commissions | This is an array that breaks down the applicable commissions. |
| Cost | This is the total cost of the order \(including commission\). |
| NetCost | This is the cost of the order less commission. |
| Quotes | This is the last batch of quotes for this security. |
| MarginChange | This is the amount by which the trading account margin requirements will be affected once this order is filled. |

### Common Mistakes

Here are some of the common mistakes that developers make when attempting to validate a new order.

#### Requesting as a Non-Administrator

One of the most common mistakes that developers make when making this API request is to use the authorization token of a non-administrator. It's critical to understand that in order to be eligible for validating new orders, the requester must be an administrator. Otherwise you'll receive the 401 status code with the following message:

```javascript
{
    "Message": "Authorization has been denied for this request."
}
```

So be sure to use the authorization token generated with an administrator's credentials.

#### Failing to Specify the Et-App-Key Parameter

If you specify the wrong Et-App-Key parameter or fail to include it in the header altogether, you'll get the following error:

```javascript
{
    "error": "Application key is not defined or does not exist"
}
```

#### Providing an Incorrect Set of Parameters 

Another common mistake made when sending this API request is failing to provide all mandatory parameters. Doing so will result in the 500 status code and the following error message:

```javascript
{
  "message": "An error occurred while processing your request",
  "error": "Unexpected server error"
}
```

### 
