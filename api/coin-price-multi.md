
# Coin Price API

Retrieve the latest price and 24-hour price change for multiple coins in a single request.
You can use either the GET or POST method to retrieve the data. 

Maximum 100 items can be requested at once. If you need to request large items, please consider using the POST method.

---

## **Endpoint**
You can use the following endpoints to retrieve coin prices:
```
GET /api/v1/partner/coin-price-multi
```
```
POST /api/v1/partner/coin-price-multi
```


## Parameters

### GET Request Parameters

| Name       | Type   | Required | Description                                                                 |
|------------|--------|----------|-----------------------------------------------------------------------------|
| `coin_ids` | string | Yes      | The unique identifier of the coins, separated by commas (e.g., `0x...::module::COIN,0x...::module::COIN`). Maximum 100 items. Consider using the POST method for larger requests. (url length limit) |


### POST Request Parameters
| Name      | Type   | Required | Description                                                                 |
|-----------|--------|----------|-----------------------------------------------------------------------------|
| `coin_ids` | string[] | Yes      | An array of unique identifiers for the coins (e.g., [`0x...::module::COIN`,`0x...::module::COIN`]). Maximum 100 items. |

## **Headers**

| Header        | Required | Description                                 |
|---------------|----------|---------------------------------------------|
| `x-api-key`       | Yes  | API key for authorization.                  |
| `x-chain`         | Yes  | Blockchain identifier (e.g., `sui`).        |

---

## **cURL Example**
### GET
```bash
curl --location 'https://api.noodles.fi/api/v1/partner/coin-price-multi?coin_ids=0xdeeb7a4662eec9f2f3def03fb937a663dddaa2e215b8078a284d026b7946c270%3A%3Adeep%3A%3ADEEP%2C0x12f4f6f3b8352e1d1ba1df4d6941e8720b8e37342f95ebb7780898621f7692ab%3A%3Ajelly%3A%3AJELLY%2C006734e1fe4c43141f47326a88c748c8900ab222e8794d0dfe545a90943ee7ab%3A%3Asuia%3A%3ASUIA' \
--header 'Accept-Encoding: application/json' \
--header 'x-api-key: YOUR_API_KEY' \
--header 'x-chain: sui'
```

### POST
```bash
curl --location 'https://api.noodles.fi/api/v1/partner/coin-price-multi' \
--header 'Accept-Encoding: application/json' \
--header 'x-api-key: YOUR_API_KEY' \
--header 'x-chain: sui' \
--header 'Content-Type: application/json' \
--data '{
    "coin_ids": ["0xdeeb7a4662eec9f2f3def03fb937a663dddaa2e215b8078a284d026b7946c270::deep::DEEP", "0x0000000000000000000000000000000000000000000000000000000000000002::sui::SUI", 
    "006734e1fe4c43141f47326a88c748c8900ab222e8794d0dfe545a90943ee7ab::suia::SUIA"]
}'
```

---

## **Response**

### Field

Each coin in the response will have a mapping of its unique identifier to its price data:
- Key: Coin Identifier (e.g., `0x0000000000000000000000000000000000000000000000000000000000000002::sui::SUI`)
- Value: Coin Price Data
- If the coin has no data, the value will be `null`.
- If the coin has data, the value will be an object containing the following fields:

| Field               | Type     | Nullable | Description                                        |
|---------------------|----------|----------|----------------------------------------------------|
| `price`             | `number` | No       | Price of the coin.                                 |
| `price_change_24h`  | `number` | Yes      | Percentage change in price over the last 24 hours. |
| `price_change_7d`   | `number` | Yes      | Percentage change in price over the last 7 days.   |
| `price_change_30d`  | `number` | Yes      | Percentage change in price over the last 30 days.  |


### Success Response
```json
{
    "data": {
        "0x006734e1fe4c43141f47326a88c748c8900ab222e8794d0dfe545a90943ee7ab::suia::SUIA": null,
        "0x0000000000000000000000000000000000000000000000000000000000000002::sui::SUI": {
            "price": 3.72,
            "price_change_24h": -5.58,
            "price_change_7d": -0.27,
            "price_change_30d": 69.09
        },
        "0xdeeb7a4662eec9f2f3def03fb937a663dddaa2e215b8078a284d026b7946c270::deep::DEEP": {
            "price": 0.1839792539,
            "price_change_24h": -7.88,
            "price_change_7d": -2.4,
            "price_change_30d": 137.57
        }
    }
}
```

---

## Error Responses

### Invalid Parameters
**Status Code:** `400 Bad Request`
```json
{
    "message":"invalid coin_ids"
}
```

### Unauthorized
**Status Code:** `401 Unauthorized`
```json
{
    "message": "invalid api key"
}
```

### Rate Limited
**Status Code:** `429 Too Many Requests`
```json
{
    "message": "rate limit exceeded"
}
```

### Internal server error
**Status Code:** `500 Internal Server Error`
```json
{
    "message": "internal server error"
}
```
---

