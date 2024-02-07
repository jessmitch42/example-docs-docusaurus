---
sidebar_position: 1
---

# Authentication

All API requests must include the [HTTP `Authorization` header](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Authorization) to be properly authenticated and ensure app security. Unauthenticated requests will respond with a `401` error code.

## Developer tokens

These example docs do not include a section on how to create a token for authenticating API requests. For the purpose of this exercise, we will assume developers already have a secret token, which will be referred to as `X_TOKEN`.

## Example request

The following cURL command demonstrates an example of how to authenticate a `GET` request to [retrieve a list of existing ad creatives](/docs/endpoints/retrieve-ad-creatives).

Note the inclusion of the `Authorization` header, which is set to the user’s `X_TOKEN` .

```bash
curl 'https://api.adcreative.com/v1/ad-creative/<id>' \
  -H 'Authorization: Bearer '"$X_TOKEN"'' \
  -H 'Content-Type: application/json' \
```
