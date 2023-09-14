## Add Customer
```shell
curl --location --globoff 'https://api.sobot.in/api/customer' \
--header 'x-api-key: yourapiaccesskey' \
--header 'x-api-secret: yourapisecretkey' \
--header 'content-type': 'application/json' \
--data '{
    "mobile": "919561XXXXXX",
    "name": "John Doe"
}'
```

```python
import requests
import json
url = "https://api.sobot.in/api/customer"

payload = json.dumps(
  {
    "mobile": "919561XXXXXX",
    "name": "John Doe"
}
)
headers = {
  'x-api-key': 'yourapiaccesskey',
  'x-api-secret': 'yourapisecretkey',
  'content-type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)
```

```php
require_once 'HTTP/Request2.php';
$request = new HTTP_Request2();
$request->setUrl('https://api.sobot.in/api/customer');
$request->setMethod(HTTP_Request2::METHOD_POST);
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
    "name": "John Doe"\n}'
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
    "message": "Customer added successfully",
    "code": 201
}
```

> If customer already exist with same mobile number, you will get following response.

```json
{
    "message": "Customer already exists",
    "code": 400
}
```

> If number is not valid as per the required length or as per the standard rules, you will get following response. 

```json
{
    "message": "Invalid mobile number",
    "code": 400
}
```

This API allows you to Add Customer to Sobot Platform. Once it is added and that phone number is available on WhatsApp, you are ready to send WhatsApp messages to them.

### HTTP Request

`POST https://api.sobot.in/api/customer`

### Body Parameters

Parameter | Required | Description |
--------- | ------- | ----------- | 
mobile | Yes | A WhatsApp enabled mobile number with country code. Don't prefix '+' or '#'.<br/><br/>  Maximum Length: 15 Characters (including country code)
name | Yes | A name of customer. <br/><br/>Maximum Length: 100 Characters


### Supported Languages 
Lang code | Language |
----------|----------|
en | English |
en_US | English (US) |
en_GB | English (UK) |
hi | Hindi |
mr | Marathi |
