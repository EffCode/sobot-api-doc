## Add Text Template
```shell
curl --location --globoff 'https://api.sobot.in/api/template/' \
--header 'x-api-key: yourapiaccesskey' \
--header 'x-api-secret: yourapisecretkey' \
--header 'content-type': 'application/json' \
--data '{
    "category": "UTILITY",
    "entity_name": "hello_world",
    "body": "Welcome and congratulations!! This message demonstrates 
    your ability to send a WhatsApp message notification from the Cloud API, 
    hosted by Meta. Thank you for taking the time to test with us.",
    "template_type": "TEXT"
}'
```

```python
import requests
import json
url = "https://api.sobot.in/api/template/"

payload = json.dumps(
  {
    "category": "UTILITY",
    "entity_name": "hello_world",
    "body": "Welcome and congratulations!! This message demonstrates \
    your ability to send a WhatsApp message notification from the Cloud API, \
    hosted by Meta. Thank you for taking the time to test with us.",
    "template_type": "TEXT"
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
$request->setUrl('https://api.sobot.in/api/template/');
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
    "category": "UTILITY",\n
    "entity_name": "hello_world",\n
    "body": "Welcome and congratulations!! This message demonstrates 
    your ability to send a WhatsApp message notification from the Cloud API, 
    hosted by Meta. Thank you for taking the time to test with us.",\n
    "template_type": "TEXT"\n}'
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
    "message": "Template created successfully",
    "code": 201
}
```
This API allows you to Add Text Template to your WABA account using Sobot platform. Once it is added, it will go through approval process from Meta.

### HTTP Request

`POST https://api.sobot.in/api/template/`

### Body Parameters

Parameter | Required | Description |
--------- | ------- | ----------- | 
category | Yes | Defines the type of template. Possible values are <ul><li> MARKETING </li><li>UTILITY</li><li>AUTHENTICATION</li></ul> | 
entity_name | Yes | This is to refer template in future use. Duplicate ```entity_name``` is not allowed. No spaces allowed in ```entity_name```. (if space is added, it will be replaced with _.) <br/> <br/> Maximum Length: 128 Characters. |
template_type | Yes | Type of template contents. Set to ```TEXT``` in case of Text templates. |
body | Yes | Main body of Template. You should have text in same language as mentioned in ```lang_code``` parameter. Emojis, markdown, and links are supported. <br/> <br/> Maximum length: 1024 Characters. |
lang_code | Yes | Specify the language code for body content. (Incorrect language specification may result in temlplate rejection.) For supported languages, check table below. Default is ```en_US``` |
header_type | No | Required if want add header. Type of header for template. Set to ```TEXT``` in case of Text header. |
header | No | This is text for header, cannot contain Emojis, markdown. Header is required if header_type is ```TEXT```. <br/> <br/> Maximum Length : 60 characters |
footer | No | This is text for footer, can contain Emojis but not markdown. <br/> <br/> Maximum Length : 60 characters |

### Supported Languages 
Lang code | Language |
----------|----------|
en | English |
en_US | English (US) |
en_GB | English (UK) |
hi | Hindi |
mr | Marathi |