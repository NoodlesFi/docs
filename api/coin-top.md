
# Coin Top API

Retrieve a list of top coins base on volume USD in 24h

## Endpoint

```http
POST /api/v1/partner/coin-top
```


## Request Body

### Parameters

| Field            | Type      | Required | Description |
|------------------|-----------|----------|-------------|
| `pagination`     | `object`  | No       | Pagination |
| ├─ `limit`       | `number`  | No       | Max number of items to return. Default: `20`, Max: `40`. |
| └─ `offset`      | `number`  | No       | Index to start the results from. Default: `0`. |
| `filters`        | `object`  | No       | Filters |
| └─ `coin_ids`    | `string[]`| No       | Array of coin_id to filter (use to filter favorite coins). |


### Example

```json
{
  "pagination": {
    "limit": 10,
    "offset": 0
  },
  "filters": {
    "coin_ids": [
      "0x32a976482bf4154961bf20bfa3567a80122fdf8e8f8b28d752b609d8640f7846::miu::MIU",
      "0xdeeb7a4662eec9f2f3def03fb937a663dddaa2e215b8078a284d026b7946c270::deep::DEEP"
    ]
  }
}
```

## Headers

| Header         | Required | Description |
|---------------|----------|-------------|
| `x-api-key`   | No     | API key for authentication. |


## Response Body

### Fields

| Field               | Type     | Description |
|--------------------|----------|-------------|
| `data`             | `array`  | List of trending coin objects. |
| ├─ `coin_type`     | `string` | Coin Identifier |
| ├─ `name`          | `string` | Name of the coin. |
| ├─ `symbol`        | `string` | Symbol of the coin. |
| ├─ `logo`          | `string` | URL to the coin's logo. |
| ├─ `price`         | `string` | Current price of the coin. |
| ├─ `price_change_1h` | `number` | % price change in the last hour. |
| ├─ `price_change_6h` | `number` | % price change in the last 6 hours. |
| ├─ `price_change_1d` | `number` | % price change in the last 24 hours. |
| ├─ `vol_change_1d` | `number` | % volume change in the last 24 hours. |
| ├─ `liq_change_1d` | `number` | % liquidity of coin (usd) change in the last 24 hours. |
| ├─ `tx_change_1d` | `number` | % Number of transactions change in the last 24 hours. |
| ├─ `tx_24h`        | `number` | Number of transactions in 24h. |
| ├─ `volume_24h`    | `string` | Trading volume in 24h. |
| ├─ `maker_24h`     | `number` | Number of makers in 24h. |
| ├─ `market_cap`    | `string` | Market cap. |
| ├─ `liquidity_usd` | `string` | Liquidity in USD. |
| ├─ `circulating_supply` | `string` | Circulating supply. |
| ├─ `total_supply`  | `string` | Total coin supply. |
| ├─ `published_at`  | `string` | Created time of the coin (RFC3339 format). |
| └─ `verified`      | `boolean`| Indicates if the coin is verified by Blockvision. |
| `pagination`       | `object` | Pagination object (limit & offset). |


### Success Response

```json
{
    "data": [
        {
            "coin_type": "0xdeeb7a4662eec9f2f3def03fb937a663dddaa2e215b8078a284d026b7946c270::deep::DEEP",
            "name": "DeepBook Token",
            "symbol": "DEEP",
            "logo": "https://imagedelivery.net/cBNDGgkrsEA-b_ixIp9SkQ/DEEP_BlueBackground.png/public",
            "price": "0.0947",
            "price_change_1h": 0.08,
            "price_change_6h": 6.31,
            "price_change_1d": 6.24,
            "vol_change_1d": -47.62,
            "liq_change_1d": 47.49,
            "tx_change_1d": -40.16,
            "tx_24h": 79491,
            "volume_24h": "32805870",
            "maker_24h": 10524,
            "market_cap": "236635701",
            "liquidity_usd": "4310216",
            "circulating_supply": "2500000000",
            "total_supply": "9992870898",
            "published_at": "2024-03-28T13:18:43.56Z",
            "verified": true
        },
        {
            "coin_type": "0x32a976482bf4154961bf20bfa3567a80122fdf8e8f8b28d752b609d8640f7846::miu::MIU",
            "name": "MIU",
            "symbol": "MIU",
            "logo": "https://miucoin.io/favicon.ico",
            "price": "0.0000000645",
            "price_change_1h": 0,
            "price_change_6h": 0.43,
            "price_change_1d": 0.01,
            "vol_change_1d": -27.63,
            "liq_change_1d": 0.82,
            "tx_change_1d": 4.04,
            "tx_24h": 386,
            "volume_24h": "6773",
            "maker_24h": 65,
            "market_cap": "58074718",
            "liquidity_usd": "17540",
            "circulating_supply": "900000000000000",
            "total_supply": "900000000000000",
            "published_at": "2024-12-03T15:37:33.334Z",
            "verified": true
        }
    ],
    "pagination": {
        "limit": 10,
        "offset": 0
    }
}
```

## Error Responses

### Invalid Parameters
**Status Code:** `400 Bad Request`
```json
{
    "message":"invalid request body"
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