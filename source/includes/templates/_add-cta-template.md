## Add Template with CTA
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
    "template_type": "TEXT",
    "sub_type": "CTA",
    "phone_numbers": [{"phone_number": "919561XXXXXX", "text": "Call Now"}],
    "url" : "https://example.com/register/customer/{{1}}",
    "example_webiste": "https://example.com/register/customer/delhi",
    "url_name": "Register Now"
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
    "sub_type": "CTA",
    "phone_numbers": [{"phone_number": "919561XXXXXX", "text": "Call Now"}],
    "url" : "https://example.com/register/customer/{{1}}",
    "example_webiste": "https://example.com/register/customer/delhi",
    "url_name": "Register Now"
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
    "template_type": "TEXT",\n
    "sub_type": "CTA",\n
    "phone_numbers": [{"phone_number": "919561XXXXXX", "text": "Call Now"}],\n
    "url" : "https://example.com/register/customer/{{1}}",\n
    "example_webiste": "https://example.com/register/customer/delhi",\n
    "url_name": "Register Now"\n}'
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
This API allows you to Add Text Template with Call-to-Action buttons to your WABA account using Sobot platform. Once it is added, it will go through approval process from Meta.

**Call-to-Action** buttons can be of two types:
<ol><li>Website link</li><li>Phone number</li></ol>

You can have maximum two CTA buttons as per following combinations:
<ul><li>Single button with website link </li>
<li> Single button with Phone number </li>
<li> Two buttons, one for website link & another for phone number </li> </ul>

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
sub_type | Yes | Set its value to ```CTA``` if you want to add Call-to-Action buttons in your template.
phone_numbers | Yes | Required if you want to add Phone number as on of the Call-to-Action. It accepts JSON Array of single json object which has two keys as follows. <ul><li>phone_number: A phone number with country-code e.g. 919970XXXXXX</li><li>text: Name of CTA button <br/> <br/> Maximum Length : 20 characters</li></ul> |
url | Yes |If  ```sub_type ``` is set to CTA and you want to add Call-to-Action as a website, you will specify website URL here. A website URL can be of of two types: <ol><li>Static : In this case you will specify entire URL in this parameter. No ```example_website``` parameter needed.</li> <li>Dyanmic: In this case you can specify some part of website URL as a variable part. Variable part is always at the end of URL & supports single variable only. If your url is of this type, you will specifiy complete URL as a example URL in ```example_website``` parameter. <br/> Example of Dynamic URL: https://example.com/register/customer/{{1}} </li></ol>|
example_website | Yes | If  ```sub_type ``` is set to CTA and you want to add Call-to-Action as a website, with this parameter you will specify example value for a dynamic URL that was added in ```url```. parameter. <br> e.g. https://example.com/register/customer/delhi|
url_name | Yes | If  ```sub_type ``` is set to CTA and you want to add Call-to-Action as a website, with this parameter you will specify name to show for CTA button. <br/> <br/> Maximum Length : 20 characters|
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
