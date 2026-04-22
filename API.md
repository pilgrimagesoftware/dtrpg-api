# API

The file documents the API endpoints for DriveThruRPG

## Server info

URL: `https://api.drivethrurpg.com`

Path: `/api/vBeta`

## Endpoints

### POST /auth_key

#### Query parameters

* `applicationKey`: Value of application key from DriveThruRPG account

#### Request Headers

* `Content-type`: `application/json`

#### Request Body

* None

#### Response Headers

* `Content-type`: `application/json`

#### Response Body

```json
{
  "token": "<phnx_auth_cookie_hp>.<phnx_auth_cookie_s>",
  "refreshToken": "<refresh-token-value>",
  "refreshTokenTTL": 1775404003
}
```

#### Cookies

* `phnx_auth_cookie_hp`: first part of token from response body
* `phnx_auth_cookie_s`: second part of token from response body
* `phnx_auth_refresh_timer`: Unix timestamp, same as from response body
* `refreshToken`: refreshToken from response body

#### Notes

### /images

#### Query parameters

#### Request Headers

#### Request Body

#### Response Headers

#### Response Body

#### Notes

### /library-client/current-version-osx.txt

#### Query parameters

#### Request Headers

#### Request Body

#### Response Headers

#### Response Body

#### Notes

### /order_products

#### Query parameters

#### Request Headers

#### Request Body

#### Response Headers

#### Response Body

#### Notes

### /product_list_items

#### Query parameters

*

#### Request Headers

* `Authorization`: the token acquired from the call to `/auth`
* `Content-type`: `application/json`

#### Request Body

#### Response Headers

#### Response Body

#### Notes
