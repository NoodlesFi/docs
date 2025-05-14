# OHLC API

## Overview
The OHLC API provides OHLCV (Open, High, Low, Close, Volume) data for a given coin over a specified time range and bucket size.

## Endpoint
```
GET /api/v1/partner/ohlcv
```

## Parameters
| Parameter  |  Type   | Required | Description | 
|------------|---------|----------|-------------|
| `coin_id`  | String  | Yes | The coin identifier. |
| `bucket`   | Integer | Yes | The time bucket size in minutes. Choices are:  1, 5, 15, 60(1 hour), 240(4 hours) , 1440 (1 day) |
| `from`     | Integer | No  | Start timestamp (Unix time). |
| `to`       | Integer | No  | End timestamp (Unix time). |
| `limit`    | Integer | No  | The maximum number of bucket to return. Max value: 500, Default value: 500 |

## Headers

| Header        | Required | Description |
|---------------|----------|-------------|
| `x-api-key`   | No     | API key for authentication. Contact richard@noodles.fi for PRO Plan |

## Request Example
```sh
curl --location 'https://api.noodles.fi/api/v1/partner/ohlcv?coin_id=0x027792d9fed7f9844eb4839566001bb6f6cb4804f66aa2da6fe1ee242d896881%3A%3Acoin%3A%3ACOIN&bucket=15&to=1741513193&limit=329' \
--header 'Accept-Encoding: application/json' \
--header 'x-api-key: YOUR_API_KEY'
```

## Response Format
```json
{
    "data": [
        [
            1701857700,
            1.7467633222351549e-7,
            1.7467633222351549e-7,
            1.7178829066103107e-7,
            1.7178829066103107e-7,
            268.0347809207526,
            5101.582571424068
        ],
        [
            1701858600,
            1.7178829066103107e-7,
            1.7223573417271332e-7,
            1.711429546004599e-7,
            1.711429546004599e-7,
            0,
            2151.777993731664
        ]
    ]
}
```

## Response Fields

| Index | Field     | Description |
|-------|----------|-------------|
| 0     | `timestamp` | Unix timestamp for the bucket period. |
| 1     | `open`       | The opening price. |
| 2     | `high`       | The highest price. |
| 3     | `low`        | The lowest price.  |
| 4     | `close`      | The closing price. |
| 5     | `volume`   | Trading volume. |


## Error Responses

### Invalid Parameters
**Status Code:** `400 Bad Request`
```json
{
    "message": "invalid request parameters"
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

## Notes
- The response is optimized for speed and may include only the most recent bucket that has trades, ignoring some buckets.
---


