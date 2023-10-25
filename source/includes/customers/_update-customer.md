## Update Customer
```shell
curl -X PUT --location --globoff 'https://api.sobot.in/api/customer/<mobile_number>' \
--header 'x-api-key: yourapiaccesskey' \
--header 'x-api-secret: yourapisecretkey' \
--header 'content-type': 'application/json' \
--data '{
    "name": "John Doe",
    "email": "john@example.com",
    "facebook_profile": "https://facebook.com/johndoe",
    "linkedin_profile": "https://www.linkedin.com/in/johndoe/",
    "twitter_profile": "https://www.twitter.com/johndoe/",
    "gender": "Male",
    "date_of_birth": "12-12-1991",
    "extra_fields": {
        "joining_data": "2023-01-12"
    },
    "labels": ["label1", "label2", "label3"]
}'
```

```python
import requests
import json
url = "https://api.sobot.in/api/customer"

payload = json.dumps(
  {
    "mobile": "919561XXXXXX",
    "name": "John Doe",
    "email": "john@example.com",
    "facebook_profile": "https://facebook.com/johndoe",
    "linkedin_profile": "https://www.linkedin.com/in/johndoe/",
    "twitter_profile": "https://www.twitter.com/johndoe/",
    "gender": "Male",
    "date_of_birth": "12-12-1991",
    "extra_fields": {
        "joining_data": "2023-01-12"
    },
    "labels": ["label1", "label2", "label3"]
}
)
headers = {
  'x-api-key': 'yourapiaccesskey',
  'x-api-secret': 'yourapisecretkey',
  'content-type': 'application/json'
}

response = requests.request("PUT", url, headers=headers, data=payload)

print(response.text)
```

```php
require_once 'HTTP/Request2.php';
$request = new HTTP_Request2();
$request->setUrl('https://api.sobot.in/api/customer');
$request->setMethod(HTTP_Request2::METHOD_PUT);
$request->setConfig(array(
  'follow_redirects' => TRUE
));
$request->setHeader(array(
  'x-api-key' => 'yourapiaccesskey',
  'x-api-secret' => 'yourapisecretkey',
  'content-type' => 'application/json'
));
$request->setBody('{\n
    "mobile": "919561XXXXXX",
    "name": "John Doe"
    "email": "john@example.com",
    "facebook_profile": "https://facebook.com/johndoe",
    "linkedin_profile": "https://www.linkedin.com/in/johndoe/",
    "twitter_profile": "https://www.twitter.com/johndoe/",
    "gender": "Male",
    "date_of_birth": "12-12-1991",
    "extra_fields": {
        "joining_data": "2023-01-12"
    },
    "labels": ["label1", "label2", "label3"] \n}'
);
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
    "message": "Customer updated successfully",
    "code": 201
}
```

> If number is not valid as per the required length or as per the standard rules, you will get following response. 

```json
{
    "message": "Invalid mobile number",
    "code": 400
}
```

This API allows you to Update Customer data on Sobot Platform. 

### HTTP Request

`PUT https://api.sobot.in/api/customer/<mobile_number>`

### Path Parameters

Parameter | Required | Description |
--------- | ------- | ----------- | 
mobile_number | Yes | A customer mobile number with country code. Don't prefix '+' or '#'.

### Body Parameters

Parameter | Required | Description |
--------- | ------- | ----------- | 
name | Yes | A name of customer. <br/><br/>Maximum Length: 100 Characters
email| No | Email ID of a customer. This should be in a valid format.
gender | No | A gender of a customer. <br/> <br/> Valid values are : Male or Famale
date_of_birth | No | Birthdate of a customer in a valid format. <br> <br> Valid Format: DD-MM-YYYY
facebook_profile | No | A Link of Facebook profile of a customer.
linkedin_profile | No | A Link of LinkedIn profile of a customer.
twitter_profile | No | A Link of Twitter profile of a customer.
extra_fields | No | This is a JSON object which accepts a Key value pair. This allows you to introduce new fields on customer profile as per your need. A Key in JSON should not have a space. If your keys have a space then replace it with underscore (_). <br/><br/> e.g.  ```{ "joining_data": "2023-01-12" }```
labels | No | List of labels to apply to customer. This will replace all earlier labels, if any and apply the new ones. This is a JSON array of strings. 
