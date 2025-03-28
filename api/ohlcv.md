# OHLC API

## Overview
The OHLC API provides OHLCV (Open, High, Low, Close, Volume) data for a given token over a specified time range and bucket size.

## Endpoint
```
GET /api/v1/partner/ohlcv
```

## Base URL
```
Staging: https://api-staging.noodles.fi
Production: https://api.noodles.fi
```

## Request Parameters

| Parameter     | Type   | Required | Description |
|--------------|--------|----------|-------------|
| `coin_type`  | string | Yes      | The token type, represented in a specific format. Example: `0x027792d9fed7f9844eb4839566001bb6f6cb4804f66aa2da6fe1ee242d896881::coin::COIN` |
| `bucketMinute` | int  | Yes      | Time bucket size in minutes (e.g., `240` for 4-hour intervals). |
| `from`       | string | Yes      | Start timestamp in ISO 8601 format (e.g., `2023-06-22T09:39:53Z`). |
| `to`         | string | Yes      | End timestamp in ISO 8601 format (e.g., `2025-03-09T09:39:53Z`). |
| `limit`      | int    | No       | Maximum number of data points to return. Default: 100. |

## Headers

| Header         | Required | Description |
|---------------|----------|-------------|
| `Accept-Encoding` | No  | Suggested value: `application/json`. |
| `x-api-key`   | Yes     | API key for authentication. |

## Example Request

```sh
curl --location 'https://api-staging.noodles.fi/api/v1/partner/ohlcv?coin_type=0x027792d9fed7f9844eb4839566001bb6f6cb4804f66aa2da6fe1ee242d896881%3A%3Acoin%3A%3ACOIN&bucketMinute=240&from=2023-06-22T09%3A39%3A53Z&to=2025-03-09T09%3A39%3A53Z&limit=329' \
--header 'Accept-Encoding: application/json' \
--header 'x-api-key: YOUR_API_KEY'
```

## Response

### Success Response

```json
{
    "data": [
        {
            "t": "2025-01-13T16:00:00Z",
            "ohlcv": [
                92373.55683931554,
                92599.21711082783,
                91284.1439397996,
                92132.05740023508,
                165996.02019695172
            ]
        },
        {
            "t": "2025-01-13T20:00:00Z",
            "ohlcv": [
                92132.05740023508,
                93919.00101274817,
                91893.93648733592,
                93685.67657255827,
                109096.25048818799
            ]
        }
    ]
}
```

### Response Data Format
Each data entry is an object with the following structure:

| Field | Type   | Description |
|-------|--------|-------------|
| `t`   | string | Timestamp in ISO 8601 format. |
| `ohlcv` | array | OHLCV values in the following order: Open, High, Low, Close, Volume. |

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

