---
icon: network-wired
---
# OHLCV-Pair API

## Overview
The OHLC-Pair API provides OHLCV (Open, High, Low, Close, Volume) data for a given pair of tokens over a specified time range and bucket size.

## Endpoint
```
GET /api/v1/partner/ohlcv-pair
```

## Base URL
```
**Staging**: https://api-staging.noodles.fi
**Production**: https://api.noodles.fi
```

## Request Parameters

| Parameter   | Type   | Required | Description |
|------------|--------|----------|-------------|
| `coin_a`   | string | Yes      | The first token in the pair, represented in a specific format. Example: `0x06864a6f921804860930db6ddbe2e16acdf8504495ea7481637a1c8b9a8fe54b::cetus::CETUS` |
| `coin_b`   | string | Yes      | The second token in the pair, represented in a specific format. Example: `0x2::sui::SUI` |
| `bucket`   | int    | Yes      | Time bucket size in minutes (e.g., `60` for 1-hour intervals). Choices are:  1, 5, 15, 60(1 hour), 240(4 hours) , 1440 (1 day) |
| `from`     | int    | Yes      | Start timestamp (Unix epoch time in seconds). |
| `to`       | int    | Yes      | End timestamp (Unix epoch time in seconds). |
| `limit`    | int    | No       | Maximum number of data points to return. Max value: 500 |

## Headers

| Header         | Required | Description |
|---------------|----------|-------------|
| `x-api-key`   | No     | API key for authentication. Contact richard@noodles.fi for PRO Plan |

## Example Request

```sh
curl --location 'https://api-staging.noodles.fi/api/v1/partner/ohlcv-pair?coin_a=0x06864a6f921804860930db6ddbe2e16acdf8504495ea7481637a1c8b9a8fe54b%3A%3Acetus%3A%3ACETUS&coin_b=0x2%3A%3Asui%3A%3ASUI&bucket=60&from=1717113600&to=1743120000&limit=20' \
--header 'Accept-Encoding: application/json' \
--header 'x-api-key: YOUR_API_KEY'
```

## Response

### Success Response

```json
{
    "data": [
        [
            1743048000,
            0.04908233001742937,
            0.04927861311354048,
            0.049008963864295665,
            0.049008963864295665,
            186885.97466471087,
            2247403.952830868
        ],
        [
            1743051600,
            0.04888959850011181,
            0.04909518361324993,
            0.04856462724447137,
            0.04909518361324993,
            400729.021566083,
            2118999.1037942683
        ]
    ]
}
```

### Response Data Format
Each data entry is an array with the following structure:

| Index | Field     | Description |
|-------|----------|-------------|
| 0     | `timestamp` | Unix timestamp for the bucket period. |
| 1     | `open`       | Open price of `coin_a` in terms of `coin_b`. |
| 2     | `high`       | Highest price during the period. |
| 3     | `low`        | Lowest price during the period. |
| 4     | `close`      | Closing price of the period. |
| 5     | `volume_a`   | Trading volume of `coin_a` in the period. |
| 6     | `volume_b`   | Trading volume of `coin_b` in the period. |

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

## Notes
- The API key for the Pro plan will have a higher rate limit and access to more APIs.
- The `from` and `to` timestamps should be within a reasonable range to avoid performance issues. If the `from` and `to` range is too large, the data will automatically be truncated to a maximum of 500 buckets.
- The API response is optimized for speed and may include only the most relevant data points based on the `limit` parameter.

---

_Last updated: March 2025_

