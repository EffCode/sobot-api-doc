## Get All Customers
```shell
curl --location --globoff 'https://api.sobot.in/api/customer' \
--header 'x-api-key: yourapiaccesskey' \
--header 'x-api-secret: yourapisecretkey' \
--header 'content-type': 'application/json' \
```

```python
import requests
import json
url = "https://api.sobot.in/api/customer"
headers = {
  'x-api-key': 'yourapiaccesskey',
  'x-api-secret': 'yourapisecretkey',
  'content-type': 'application/json'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```

```php
require_once 'HTTP/Request2.php';
$request = new HTTP_Request2();
$request->setUrl('https://api.sobot.in/api/customer');
$request->setMethod(HTTP_Request2::METHOD_GET);
$request->setConfig(array(
  'follow_redirects' => TRUE
));
$request->setHeader(array(
  'x-api-key' => 'yourapiaccesskey',
  'x-api-secret' => 'yourapisecretkey',
  'content-type' => 'application/json'
));
try {
  $response = $request->send();
  if ($response->getStatus() == 200) {
    echo $response->getBody();
  }
  else {
    echo 'Unexpected HTTP status: ' . $response->getStatus() . ' ' .
    $response->getReasonPhrase();
  }
}
catch(HTTP_Request2_Exception $e) {
  echo 'Error: ' . $e->getMessage();
}

```

> The above API call returns JSON response like this:

```json
{
    "count": 145,
    "size": 20,
    "next": "https://api.sobot.in/api/customer?page=2",
    "previous": null,
    "code": 200,
    "data": [
        {
            "id": 3588183,
            "name": "John Doe",
            "first_name": "John",
            "last_name": "Doe",
            "mobile": "919561XXXXXX"
        },
        {
            "id": 3418855,
            "name": "Jane Doe",
            "first_name": "Jane",
            "last_name": "Doe",
            "mobile": "919970XXXXXX"
        }
    ]
}
```

This API allows you to get all customer from your Sobot account. API response is paginated with page size of 20.


### HTTP Request

`GET https://api.sobot.in/api/customer`

### Response Parameters

**First level Keys**

Parameter | Description | 
--------- | ----------- |
Data | Array of json objects of customer's data. Check below table for detail object specification.|
count | Total count of customers in your account |
size | size of a current page |
next | Link to the next page (if any, else null)
previous | Link to the previous page (if any, else null) |
code | 200 in case of success. Check Errors for other codes. |


**Data Object**

Parameter | Description |
--------- | ----------- | 
id | Unique identifier for each customer. |
name | A full name of a customer. |
first_name | A first name of a customer (if any).|
last_name | A last name of a customer (if any).|
mobile | Mobile number of a customer with country code but without '+' or '#' sign. | 


