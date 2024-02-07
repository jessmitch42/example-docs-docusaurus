---
sidebar_position: 6
---

# Create status report

### POST `https://api.adcreative.com/v1/ad-creative/query`

Create a status report of existing ad creatives tied to an account using a `POST` request to this endpoint.

This endpoint accepts a start and end date to filter for ad creatives that were created or updated within that date range.

## Requests

### Body parameters

It is recommended to include both a `start_date` and an `end_date` when using this endpoint.

If the `start_date` is not included, the response will include all ad creatives created/updated up until the specified `end_date`.

If the `end_date` is not included, the response will include all ad creatives created/updated after the specified `start_date`.

If neither the `start_date` or `end_date` parameters are included in the request, the entire ad creative list will be returned. Please see the [Retrieve ad creative list](./retrieve-ad-creatives) endpoint as a better option for this functionality.

The `start_date` must be before the `end_date` to be valid.

| Param        | Type                | Required | Example                 |
| ------------ | ------------------- | -------- | ----------------------- |
| `start_date` | `string` (ISO date) | no ❌    | `'2024-01-31 23:59:59'` |
| `end_date`   | `string` (ISO date) | no ❌    | `'2024-01-31 23:59:59'` |

### Request examples

#### cURL

```bash
curl -X POST 'https://api.adcreative.com/v1/ad-creative/query' \
  -H 'Authorization: Bearer '"$X_TOKEN"'' \
  -H "Content-Type: application/json" \
  --data '{
    "start_date": "2024-01-29 23:59:59",
    "end_date": "2024-01-31 23:59:59",
  }'
```

#### JavaScript

```jsx
async function queryAdCreativeList() {
  const token = process.env.X_TOKEN;
  const baseURL = "https://api.adcreative.com/v1/ad-creative/query";

  // Make POST request
  try {
    const response = await fetch(baseURL, {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
        Authorization: `Bearer ${token}`,
      },
    });

    return await response.json();
  } catch (error) {
    console.error("Error:", error);
    return error;
  }
}

const filteredList = queryAdCreativeList();
```

## Responses

### Success (`200` )

#### Response body

Successful requests will respond with a `200` status code, as well as an object including a key for each date included in the search. The value of the key will be an object with information related to ad creatives updated and created on that date.

| Field             | Type          |
| ----------------- | ------------- |
| `<date-included>` | Status object |

##### Status object

| Field           | Type                                                                      |
| --------------- | ------------------------------------------------------------------------- |
| `ids`           | `array` of ad creative IDs                                                |
| `total_created` | `number`: the total number of ad creatives created on the specified date. |
| `total_updated` | `number`: the total number of ad creatives updated on the specified date. |

#### Response example

```json
  {
    "2024-01-29": { "ids": ["jess1", "bob1"], "total_created": 1, "total_updated": 1},
    "2024-01-30": { "ids": ["jess2", "bob2"], "total_created": 2, "total_updated": 0},
    "2024-01-31": { }
  },
```

### Error (`400` )

Errors while querying ad creative lists occur when the `start_date` specified is after the `end_date` specified _or_ the `start_date`/`end_date` are not in the ISO date format.

```json
{
  { "error_msg": "'January, 01, 2024' is not a valid start_date."  },
}
```