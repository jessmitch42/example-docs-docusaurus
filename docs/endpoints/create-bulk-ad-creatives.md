---
sidebar_position: 3
---

# Create bulk ad creatives

### POST `https://api.adcreative.com/v1/ad-creative`

Bulk ad creatives can be created with `POST` request to this endpoint.

> To create a single ad creative, see the [Create ad creatives](/docs/endpoints/create-an-ad-creatives) endpoint.

## Requests

`POST` requests must include an array of [ad creative objects](/docs/endpoints/create-bulk-ad-creatives#ad-creative-object) being created.

### Body parameters

| Param             | Type                                                                                          | Required | Example                                            |
| ----------------- | --------------------------------------------------------------------------------------------- | -------- | -------------------------------------------------- |
| Ad creative array | `array` of [ad creative objects](/docs/endpoints/create-bulk-ad-creatives#ad-creative-object) | yes ✅   | `[<ad-creative-object-1>, <ad-creative-object-2>]` |

#### Ad creative object

| Param             | Type                                               | Required | Example                                                                       |
| ----------------- | -------------------------------------------------- | -------- | ----------------------------------------------------------------------------- |
| `id`              | `string`                                           | yes ✅   | `"jyh7"`                                                                      |
| `name`            | `string`                                           | yes ✅   | `"Ad Creative 1"  `                                                           |
| `type`            | `string`                                           | yes ✅   | `"text"`                                                                      |
| `content`         | `string`                                           | yes ✅   | `"Here is some text for an ad"`                                               |
| `additional_data` | `array` of key (`string`) ⇒ value (`any`) elements | no ❌    | `[{ "example1": 15 },{ "example2": "another value" },{ "example3": false },]` |

### Request examples

#### cURL

```bash
curl -X POST 'https://api.adcreative.com/v1/ad-creative' \
  -H 'Authorization: Bearer '"$X_TOKEN"'' \
  -H "Content-Type: application/json" \
  --data '[
  {
    "id": "jess1",
    "name": "First Ad Creative",
    "type": "image",
    "content": "/images/first_ad_creative.png",
    "additional_data": [
      {
        "client": "Sigma"
      },
    ]
  },
  {
    "id": "bob's example",
    "name": "Second Ad Creative",
    "type": "image",
    "content": "/images/second_ad_creative.png",
  }
  ]'
```

#### JavaScript

```jsx
async function createBulkAdCreatives(adArray) {
  const token = process.env.X_TOKEN;
  const baseURL = "https://api.adcreative.com/v1/ad-creative";
  // (Add client-side data validation for array as needed)

  // Make POST request
  try {
    const response = await fetch(baseURL, {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
        "Authorization": `Bearer ${token}`,
      },
      body: JSON.stringify(adArray),
    });

    return await response.json();
  } catch (error) {
    console.error("Error:", error);
    return error;
  }

const data = [
  {
    id: "jess1",
    name: "First Ad Creative",
    type: "image",
    content: "/images/first_ad_creative.png",
    additional_data: [ { client: "TBD" } ],
  },
  {
    id: "bob's example",
    name: "Another Ad Creative",
    type: "text",
    content: "Here is some text for an ad!",
  }
]

const newBulkACs = createBulkAdCreatives(data);
```

## Responses

### Success (`200` )

#### Response body

Successful requests will respond with a `200` status code, as well as and array of ad creative objects that was successfully created.

| Param             | Type                                                                                          |
| ----------------- | --------------------------------------------------------------------------------------------- |
| Ad creative array | `array` of [ad creative objects](/docs/endpoints/create-bulk-ad-creatives#ad-creative-object) |

#### Response example

```json
[
  {
    "id": "jess1",
    "name": "First Ad Creative",
    "type": "image",
    "content": "/images/first_ad_creative.png",
    "additional_data": [{ "client": "TBD" }],
    "created_time": "2024-01-31 23:59:58",
    "last_edited_time": "2024-01-31 23:59:58"
  },
  {
    "id": "bob1",
    "name": "Another Ad Creative",
    "type": "text",
    "content": "Here is some text for an ad!",
    "additional_data": [],
    "created_time": "2024-01-31 23:59:59",
    "last_edited_time": "2024-01-31 23:59:59"
  }
]
```

### Error (`400` )

Errors while retrieving ad creatives can occur for different reasons, such as a missing or invalid token.

Refer to the `error_msg` in the response body for more information on the error that occurred.

```json
{
  { "error_msg": "Invalid token." },
}
```
