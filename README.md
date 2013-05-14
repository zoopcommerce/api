# Overview
The Zoop API allows merchants to simply and easily access their structured data from our systems. Initially the API only returns product data, however we will be consistently adding additional functionality.
## API Endpoint
`https://{STORE_SUB_DOMAIN}.api.zoopcommerce.com/`
## Summary of Resource URL Patterns
```
/0.1/product
/0.1/product/{URL_SLUG}
```
### Example Request
```
curl https://demo.api.zoopcommerce.com/0.1/product
```
## Errors
TBD
## Products
You can retrieve your entire product catalog, as well as individual items,
### Request Attributes
**range**: string eg. `range: 0-9`

**sort**: string eg. `sort(+type,-name)`

### Request Filters
**name**: string eg. `name=Product+Name`

**brand**: string eg. `brand=Product+Brand+Name`

**type**: string eg. `type=Product+Type`

### Examples
#### curl
```
curl http://demo.api.zoopcommerce.com/0.1/product?name=Test+Name&sort(+price.full) \
  -r 0-9
```
#### php (with curl)
```php
<?php

$url = 'http://demo.api.zoopcommerce.com/0.1/product?name=Test+Name&sort(+price.full)';

$ch = curl_init();

curl_setopt_array($ch, array(
    CURLOPT_RETURNTRANSFER => 1,
    CURLOPT_URL => $url,
    CURLOPT_HTTPHEADER, array(
        'accept: application/json'
    ),
    CURLOPT_RANGE => '0-9'
));

// errors
if (!curl_exec($ch)) {
    die('Error: "' . curl_error($ch) . '" - Code: ' . curl_errno($ch));
}

$output = curl_exec($ch);
curl_close($ch);

$products = json_decode($output, true);
foreach ($products as $product) {
    echo $product['name'] . "<br>";
}
```
#### jQuery
