## Add Image Template
```shell
curl --location --globoff 'https://api.sobot.in/api/template/' \
--header 'x-api-key: yourapiaccesskey' \
--header 'x-api-secret: yourapisecretkey' \
--header 'content-type': 'application/json' \
--data '{
    "category": "MARKETING",
    "entity_name": "hello_world",
    "body": "Welcome and congratulations!! This message demonstrates 
    your ability to send a WhatsApp message notification from the Cloud API, 
    hosted by Meta. Thank you for taking the time to test with us.",
    "template_type": "MEDIA"
    "header_type":"IMAGE",
    "example":"https://example.com/images/20230625_003239.jpg"
}'
```

```python
import requests
import json
url = "https://api.sobot.in/api/template/"

payload = json.dumps(
  {
    "category": "MARKETING",
    "entity_name": "hello_world",
    "body": "Welcome and congratulations!! This message demonstrates \
    your ability to send a WhatsApp message notification from the Cloud API, \
    hosted by Meta. Thank you for taking the time to test with us.",
    "template_type": "MEDIA"
    "header_type":"IMAGE",
    "example":"https://example.com/images/20230625_003239.jpg"
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
     "category": "MARKETING",\n
    "entity_name": "hello_world",\n
    "body": "Welcome and congratulations!! This message demonstrates \
    your ability to send a WhatsApp message notification from the Cloud API, \
    hosted by Meta. Thank you for taking the time to test with us.",
    "template_type": "MEDIA"\n
    "header_type":"IMAGE",\n
    "example":"https://example.com/images/20230625_003239.jpg"\n}'
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
This API allows you to Add Image Template to your WABA account using Sobot platform. Once it is added, it will go through approval process from Meta.

### HTTP Request

`POST https://api.sobot.in/api/template/`

### Body Parameters

Parameter | Required | Description |
--------- | ------- | ----------- | 
category | Yes | Defines the type of template. Possible values are <ul><li> MARKETING </li><li>UTILITY</li><li>AUTHENTICATION</li></ul> | 
entity_name | Yes | This is to refer template in future use. Duplicate ```entity_name``` is not allowed. No spaces allowed in ```entity_name```. (if space is added, it will be replaced with _.) <br/> <br/> Maximum Length: 128 Characters. |
template_type | Yes | Type of template contents. Set to ```MEDIA``` in case of Image templates. |
body | Yes | Main body of Template. You should have text in same language as mentioned in ```lang_code``` parameter. Emojis, markdown, and links are supported. <br/> <br/> Maximum length: 1024 Characters. |
lang_code | Yes | Specify the language code for body content. (Incorrect language specification may result in temlplate rejection.) For supported languages, check table below. Default is ```en_US``` |
header_type | Yes | Required if want add header. Type of header for template. Set to ```IMAGE``` in case of Image header. |
example | Yes |  Public URL of a header image. This image acts like example for the header, Meta use this as an example image in approval process. You can change this image while you use this template to send the message. example is required if header_type is ```IMAGE```. <br/>Please check supported Media Types below. <br/> <br/> Maximum Length : 60 characters |
footer | No | This is text for footer, can contain Emojis but not markdown. <br/> <br/> Maximum Length : 60 characters |

### Supported Languages 
Lang code | Language |
----------|----------|
en | English |
en_US | English (US) |
en_GB | English (UK) |
hi | Hindi |
mr | Marathi |

### Supported Media Types

| Media     | Supported Types| Size Limit |
|-----------|----------------|-----------|
| image | image/jpeg, image/png Images must be 8-bit, RGB or RGBA | 5MB |
