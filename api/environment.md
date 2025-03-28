---
icon: plug-circle-plus
---
# Environment Setup

## Overview
This guide explains how to set up your environment for accessing the Noodles API. It includes details on the available environments 

## API Environments
The Noodles API is available in two environments:

| Environment | Base URL |
|------------|--------------------------------|
| **Staging** | `https://api-staging.noodles.fi` |
| **Production** | `https://api.noodles.fi` |

- **Staging**: Use this environment for testing and development.
- **Production**: Use this environment for live applications.

## Obtaining an API Key
An API key is required to authenticate, access and rate limit the API.

### Steps to Get an API Key:
1. **How to get API Key**: 
   - Contact: richard@noodles.fi for more detail

2. **Use the API Key**:
   - Include the API key in the `x-api-key` header when making requests.

### Example Usage
```sh
curl --location 'https://api.noodles.fi/api/v1/partner/ohlcv' \
--header 'Accept-Encoding: application/json' \
--header 'x-api-key: YOUR_API_KEY'
```

## Notes
- Keep your API key secure and do not share it.
- Only use `YOUR_API_KEY` on backend server side.
- Contact support if you need help with API key generation.

---

_Last updated: March 2025_