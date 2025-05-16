
# Coin Price API

Retrieve the latest price and price change (24-hour, 7-day, and 30-day) for a specific coin.

---

## **Endpoint**
```
GET /api/v1/partner/coin-price
```



## **Request Parameters**

| Name      | Type   | Required | Description                                                                 |
|-----------|--------|----------|-----------------------------------------------------------------------------|
| `coin_id` | string | Yes      | The unique identifier of the coin (e.g., `0x...::module::COIN`)             |

---

## **Headers**

| Header        | Required | Description                                 |
|---------------|----------|---------------------------------------------|
| `x-api-key`       | Yes  | API key for authorization.                  |
| `x-chain`         | Yes  | Blockchain identifier (e.g., `sui`).        |

---

## **cURL Example**
```bash
curl --location 'https://api.noodles.fi/api/v1/partner/coin-price?coin_id=0x006734e1fe4c43141f47326a88c748c8900ab222e8794d0dfe545a90943ee7ab%3A%3Asuia%3A%3ASUIA' \
--header 'Accept-Encoding: application/json' \
--header 'x-api-key: YOUR_API_KEY' \
--header 'x-chain: sui'
```

---

## **Response**

### Field
| Field               | Type     | Nullable | Description |
|---------------------|----------|----------|-------------|
| `price`             | `number` | No       | Price of the coin. |
| `price_change_24h`  | `number` | Yes      | Percentage change in price over the last 24 hours. |
| `price_change_7d`   | `number` | Yes      | Percentage change in price over the last 7 days.   |
| `price_change_30d`  | `number` | Yes      | Percentage change in price over the last 30 days.  |



### Success Response
```json
{
    "data": {
        "price": 0.000002105688571,
        "price_change_24h": 12.1,
        "price_change_7d": -7.2,
        "price_change_30d": -83.3
    }
}
```


### Response coin has no data
```json
{
    "data": null
}
```

---

## Error Responses

### Invalid Parameters
**Status Code:** `400 Bad Request`
```json
{
    "message":"invalid coin_id"
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

