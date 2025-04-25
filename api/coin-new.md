
# Coin Top API

Retrieve a list of new coins based on their published time of the coin. Coins with less than $1 liquidity will be hidden from this list.

## Endpoint

```http
POST /api/v1/partner/coin-new
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
        "offset": 0,
        "limit": 40
    },
    "filters": {
        "coin_ids": ["0xb06a3f707841a749ffb421660d020f9f995cba77f60871db46d425d1c8f54c9f::popepe::POPEPE", "0xb4604e1101a2a696a20f9a1e53518c2c3dbb06614f8d65e31b88f81af7169733::groksui::GROKSUI"]
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
            "coin_type": "0xb06a3f707841a749ffb421660d020f9f995cba77f60871db46d425d1c8f54c9f::popepe::POPEPE",
            "name": "Vatican New Pope",
            "symbol": "POPEPE",
            "logo": "https://dd.dexscreener.com/ds-data/tokens/solana/GiGfQSPdzEvtggnzN8YHwB56EoeAYDyRsdfe5d22pump.png?size=lg&key=1cfc1c",
            "price": "0.0000221",
            "price_change_1h": 0,
            "price_change_6h": 0,
            "price_change_1d": 2.65,
            "vol_change_1d": 10.2,
            "liq_change_1d": 0,
            "tx_change_1d": 0,
            "tx_24h": 0,
            "volume_24h": "0",
            "maker_24h": 0,
            "market_cap": "0",
            "liquidity_usd": "0",
            "circulating_supply": "0",
            "total_supply": "0",
            "published_at": "2025-04-21T08:39:20.777Z",
            "verified": false
        },
        {
            "coin_type": "0xb4604e1101a2a696a20f9a1e53518c2c3dbb06614f8d65e31b88f81af7169733::groksui::GROKSUI",
            "name": "GROKSUI",
            "symbol": "GROKSUI",
            "logo": "https://movepump.com/_next/image?url=https%3A%2F%2Fapi.movepump.com%2Fuploads%2F0_G_Roke_robot_surfing_f7994d3dae.png&w=640&q=75",
            "price": "0.0000234",
            "price_change_1h": 0,
            "price_change_6h": 0,
            "price_change_1d": 117.58,
            "vol_change_1d": 0,
            "liq_change_1d": 3.12,
            "tx_change_1d": 0,
            "tx_24h": 0,
            "volume_24h": "0",
            "maker_24h": 0,
            "market_cap": "0",
            "liquidity_usd": "0",
            "circulating_supply": "0",
            "total_supply": "0",
            "published_at": "2025-04-21T01:59:13.777Z",
            "verified": false
        }
    ],
    "pagination": {
        "limit": 2,
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