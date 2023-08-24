# Templates
Templates are used in template messages to open marketing, utility, and authentication conversations with customers. Unlike free-form messages, template messages are the only type of message that can be sent to customers who have yet to message you, or who have not sent you a message in the last 24 hours.

Templates must be approved before they can be sent in template messages. In addition, templates may be disabled automatically based on customer feedback. Once disabled, a template cannot be sent in a template message until its quality rating has improved or it no longer violates our business or commerce policies.

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

## Add Text Template with Variables
```shell
curl --location --globoff 'https://api.sobot.in/api/template/' \
--header 'x-api-key: yourapiaccesskey' \
--header 'x-api-secret: yourapisecretkey' \
--header 'content-type': 'application/json' \
--data '{
    "category": "UTILITY",
    "entity_name": "hello_world",
    "body": "Welcome and congratulations!! This message demonstrates 
    your ability to send a {{1}} message notification from the {{2}}, 
    hosted by Meta. Thank you for taking the time to test with us.",
    "template_type": "TEXT",
    "example_body_param": {
        "body_text":
        [
            ["WhatsApp","Cloud API"]
        ]
        }
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
    your ability to send a {{1}} message notification from the {{2}}, \
    hosted by Meta. Thank you for taking the time to test with us.",
    "template_type": "TEXT",
    "example_body_param": {
        "body_text":
        [
            ["WhatsApp","Cloud API"]
        ]
        }
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
    your ability to send a {{1}} message notification from the {{2}}, 
    hosted by Meta. Thank you for taking the time to test with us.",\n
    "template_type": "TEXT",\n
    "example_body_param": {\n
        "body_text":\n
        [\n
            ["WhatsApp","Cloud API"]\n
        ]\n
        }
    }\n'
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

### Template Variables
Template variables help you add template with placeholders whose value can be set at the time of sending this template as a message.  Any template that has one or more variables requires a sample in order to be submitted for review. You can add samples by including the example property in API request.

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
header | No | This is text for header, cannot contain Emojis, markdown. One variable parameter is allowed. Header is required if header_type is ```TEXT```. <br/> <br/> Maximum Length : 60 characters |
footer | No | This is text for footer, can contain Emojis but not markdown. <br/> <br/> Maximum Length : 60 characters |
example_body_param | No | If template ```body``` has variables then this parameter is required. This parameter holds json object of array of strings as example values. (Check format in code example) |
example_header_param | No | If template ```header``` has variable then this parameter is required. This parameter holds json object of array of a single string as example value. (Check format in code example) |  

### Supported Languages 
Lang code | Language |
----------|----------|
en | English |
en_US | English (US) |
en_GB | English (UK) |
hi | Hindi |
mr | Marathi |

## Add Button Template
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
    "buttons": ["Yes", "No", "May be"]
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
    "template_type": "TEXT",
    "buttons": ["Yes", "No", "May be"]
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
    "template_type": "TEXT"\n
    "buttons: ["Yes", "No", "May be"]\n
    \n}'
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
This API allows you to Add Text Template with Buttons(Quick replies) to your WABA account using Sobot platform. Once it is added, it will go through approval process from Meta.

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
buttons | Yes | Array of strings consist of Title of buttons. You can have up to 3 buttons. It cannot be an empty string and must be unique within the message. Emojis are supported, markdown is not. <br/> <br/>Maximum length: 20 characters for each botton title.
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

## Add Video Template
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
    "header_type":"VIDEO",
    "example":"https://example.com/images/20230625_003239.mp4"
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
    "header_type":"VIDEO",
    "example":"https://example.com/images/20230625_003239.mp4"
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
    "header_type":"VIDEO",\n
    "example":"https://example.com/images/20230625_003239.mp4"\n}'
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
This API allows you to Add Video Template to your WABA account using Sobot platform. Once it is added, it will go through approval process from Meta.

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
header_type | Yes | Required if want add header. Type of header for template. Set to ```VIDEO``` in case of Video header. |
example | Yes |  Public URL of a header video. This video acts like example for the header, Meta use this as an example video in approval process. You can change this video while you use this template to send the message. example is required if header_type is ```VIDEO```. <br/>Please check supported Media Types below. <br/> <br/> Maximum Length : 60 characters |
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

| Media     | Supported Types| Size Limit                                       |
|-----------|----------------|-----------|
| video | video/mp4, video/3gp<br/><br/> Notes: <br/>Only H.264 video codec and AAC audio codec is supported. <br/>We support videos with a single audio stream or no audio stream. | 16MB |


## Add document Template
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
    "header_type":"DOCUMENT",
    "example":"https://example.com/images/20230625_003239.pdf"
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
    "header_type":"DOCUMENT",
    "example":"https://example.com/images/20230625_003239.pdf"
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
    "header_type":"DOCUMENT",\n
    "example":"https://example.com/images/20230625_003239.pdf"\n}'
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
This API allows you to Add Document Template to your WABA account using Sobot platform. Once it is added, it will go through approval process from Meta.

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
header_type | Yes | Required if want add header. Type of header for template. Set to ```DOCUMENT``` in case of Document header. |
example | Yes |  Public URL of a header document. This document acts like example for the header, Meta use this as an example video in approval process. You can change this document while you use this template to send the message. example is required if header_type is ```DOCUMENT```. <br/>Please check supported Media Types below. <br/> <br/> Maximum Length : 60 characters |
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
| Media     | Supported Types| Size Limit                                       |
|-----------|----------------|-----------|
| document | text/plain, application/pdf, application/vnd.ms-powerpoint, application/msword, application/vnd.ms-excel, application/vnd.openxmlformats-officedocument.wordprocessingml.document, application/vnd.openxmlformats-officedocument.presentationml.presentation, application/vnd.openxmlformats-officedocument.spreadsheetml.sheet | 100MB |

## Get All Templates
```shell
curl --location --globoff 'https://api.sobot.in/api/template/' \
--header 'x-api-key: yourapiaccesskey' \
--header 'x-api-secret: yourapisecretkey' \
--header 'content-type': 'application/json' \
```

```python
import requests
import json
url = "https://api.sobot.in/api/template/"
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
$request->setUrl('https://api.sobot.in/api/template/');
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
    "count": 80,
    "size": 20,
    "next": "http://api.sobot.in/api/template/?page=2",
    "previous": null,
    "code": 200,
    "data": [
        {
            "id": 584,
            "phone_numbers": null,
            "template": "Dear customer,\n\nYou have not filed one or more GSTR 3B returns. Kindly file your returns immediately to avoid late fee and Interest. Ignore if filed. GSTN",
            "entity_name": "march_ending",
            "category": "UTILITY",
            "template_id": "759559305816228",
            "header": null,
            "header_type": null,
            "template_type": "TEXT",
            "sub_type": null,
            "buttons": null,
            "footer": null,
            "url": null,
            "example": null,
            "example_website": null,
            "url_name": null,
            "created_at": "2023-03-25T13:26:20.034623+05:30",
            "updated_at": null,
            "status": 0, // 
            "rejected_reason": null,
            "added_by": 156,
            "lang_code": "en"
        }
    ]
}
```

This API allows you to Get all Templates from your WABA account using Sobot platform. API response is paginated with page size of 20.


### HTTP Request

`GET https://api.sobot.in/api/template/`

### Response Parameters

**First level Keys**

Parameter | Description | 
--------- | ----------- |
Data | Array of json objects of template data. Check below table for detail object specification.|
count | Total count of templates in your account |
size | size of a current page |
next | Link to the next page (if any, else null)
previous | Link to the previous page (if any, else null) |
code | 200 in case of success. Check Errors for other codes. |


**Data Object**

Parameter | Description |
--------- | ----------- | 
| id              | System generated ID for each template |
| template        | Body of the template. Usually a text including Emojis, variables, markdown for formatting. |
| entity_name     | Name of the template |
| category        | Category of template It can be: <ul><li>Marketing</li><li>Utility</li><li>Authentication</li></ul>  |
| template_type   | Template type value can be: <ul><li>TEXT</li><li>MEDIA</li></ul> |
| lang_code       | Language code of ```template``` content. Actaully denotes the Language of the template. |
| template_id     | A Meta generated unique ID for template. You can refer this for future operations. |
| header          | Text of header in case of ```header_type = Text```.|
| header_type     | Header type value can be: <ul><li>TEXT</li><li>IMAGE</li><li>VIDEO</li><li>DOUCMENT</li></ul> |
| footer          | Text of footer. It can have emojis in it. |
| example         | a public URL of header data excpet for ```TEXT```. |
| sub_type        | This can be either ```null``` or ```CTA```. If it is set to ```CTA ```, it specifies that this template has CTAs in its button. CTAs can be either phone numbers and/or website. For phone number check ```phone_numbers``` and for website check ```url```, ```url_name``` and ```example_website``` |
| buttons         | This helps to identify buttons (Quick reply) of templates. It will return array of strings. <br /> <br /> e.g. ["Yes", "NO", "May be"] |
| phone_numbers   | This return json object with following keys: <ul><li>phone_number: A phone number with country-code e.g. 919970XXXXXX</li><li>text: Name of CTA button</li></ul> |
| url             | If  ```sub_type ``` is set to CTA, and added CTA is a website, this parameter will give you static part of URL. |
| example_website | If  ```sub_type ``` is set to CTA, and added CTA is a website, this parameter will give you example value of variable that was added in ```url```.  |
| url_name        | If  ```sub_type ``` is set to CTA, and added CTA is a website, this parameter will give you name to be shown for CTA button. |
| created_at      | Date of template creation. Its a timestamp. <br/> <br/> e.g. 2023-03-25T13:26:20.034623+05:30 |
| updated_at      | Date of template last updated. Its a timestamp. <br/> <br/> e.g. 2023-03-25T13:26:20.034623+05:30 |
| status          | Status of the template. It denotes the status in numbers. Please find below the number & its meaning. <ul><li>0: Pending</li><li> 1: Approved</li><li>2: Rejected</li><ul> |
| rejected_reason | Reason of rejection, if the template ```status = rejected```. Else, this is always ```null``` |
| added_by        | The unique ID of a user who has added this template on Sobot Platform.  |



## Get Pending Templates
```shell
curl --location --globoff 'https://api.sobot.in/api/template/?status=0' \
--header 'x-api-key: yourapiaccesskey' \
--header 'x-api-secret: yourapisecretkey' \
--header 'content-type': 'application/json' \
```

```python
import requests
import json
url = "https://api.sobot.in/api/template/?status=0"
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
$request->setUrl('https://api.sobot.in/api/template/?status=0');
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
    "count": 80,
    "size": 20,
    "next": "http://api.sobot.in/api/template/?status=0&page=2",
    "previous": null,
    "code": 200,
    "data": [
        {
            "id": 584,
            "phone_numbers": null,
            "template": "Dear customer,\n\nYou have not filed one or more GSTR 3B returns. Kindly file your returns immediately to avoid late fee and Interest. Ignore if filed. GSTN",
            "entity_name": "march_ending",
            "category": "UTILITY",
            "template_id": "759559305816228",
            "header": null,
            "header_type": null,
            "template_type": "TEXT",
            "sub_type": null,
            "buttons": null,
            "footer": null,
            "url": null,
            "example": null,
            "example_website": null,
            "url_name": null,
            "created_at": "2023-03-25T13:26:20.034623+05:30",
            "updated_at": null,
            "status": 0, // 
            "rejected_reason": null,
            "added_by": 156,
            "lang_code": "en"
        }
    ]
}
```

This API allows you to Get all approval pending Templates from your WABA account using Sobot platform. API response is paginated with page size of 20.


### HTTP Request

`GET https://api.sobot.in/api/template/?status=0`

### Response Parameters

**First level Keys**

Parameter | Description | 
--------- | ----------- |
Data | Array of json objects of template data. Check below table for detail object specification.|
count | Total count of templates in your account |
size | size of a current page |
next | Link to the next page (if any, else null)
previous | Link to the previous page (if any, else null) |
code | 200 in case of success. Check Errors for other codes. |


**Data Object**

Parameter | Description |
--------- | ----------- | 
| id              | System generated ID for each template |
| template        | Body of the template. Usually a text including Emojis, variables, markdown for formatting. |
| entity_name     | Name of the template |
| category        | Category of template It can be: <ul><li>Marketing</li><li>Utility</li><li>Authentication</li></ul>  |
| template_type   | Template type value can be: <ul><li>TEXT</li><li>MEDIA</li></ul> |
| lang_code       | Language code of ```template``` content. Actaully denotes the Language of the template. |
| template_id     | A Meta generated unique ID for template. You can refer this for future operations. |
| header          | Text of header in case of ```header_type = Text```.|
| header_type     | Header type value can be: <ul><li>TEXT</li><li>IMAGE</li><li>VIDEO</li><li>DOUCMENT</li></ul> |
| footer          | Text of footer. It can have emojis in it. |
| example         | a public URL of header data excpet for ```TEXT```. |
| sub_type        | This can be either ```null``` or ```CTA```. If it is set to ```CTA ```, it specifies that this template has CTAs in its button. CTAs can be either phone numbers and/or website. For phone number check ```phone_numbers``` and for website check ```url```, ```url_name``` and ```example_website``` |
| buttons         | This helps to identify buttons (Quick reply) of templates. It will return array of strings. <br /> <br /> e.g. ["Yes", "NO", "May be"] |
| phone_numbers   | This return json object with following keys: <ul><li>phone_number: A phone number with country-code e.g. 919970XXXXXX</li><li>text: Name of CTA button</li></ul> |
| url             | If  ```sub_type ``` is set to CTA, and added CTA is a website, this parameter will give you static part of URL. |
| example_website | If  ```sub_type ``` is set to CTA, and added CTA is a website, this parameter will give you example value of variable that was added in ```url```.  |
| url_name        | If  ```sub_type ``` is set to CTA, and added CTA is a website, this parameter will give you name to be shown for CTA button. |
| created_at      | Date of template creation. Its a timestamp. <br/> <br/> e.g. 2023-03-25T13:26:20.034623+05:30 |
| updated_at      | Date of template last updated. Its a timestamp. <br/> <br/> e.g. 2023-03-25T13:26:20.034623+05:30 |
| status          | Status of the template. In thi case its always ```0``` for pending templates. |
| rejected_reason | Reason of rejection, if the template ```status = 2``` i.e. Rejected. Else, this is always ```null``` |
| added_by        | The unique ID of a user who has added this template on Sobot Platform.  |

## Get Approved Templates
```shell
curl --location --globoff 'https://api.sobot.in/api/template/?status=1' \
--header 'x-api-key: yourapiaccesskey' \
--header 'x-api-secret: yourapisecretkey' \
--header 'content-type': 'application/json' \
```

```python
import requests
import json
url = "https://api.sobot.in/api/template/?status=1"
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
$request->setUrl('https://api.sobot.in/api/template/?status=1');
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
    "count": 80,
    "size": 20,
    "next": "http://api.sobot.in/api/template/?status=1&page=2",
    "previous": null,
    "code": 200,
    "data": [
        {
            "id": 584,
            "phone_numbers": null,
            "template": "Dear customer,\n\nYou have not filed one or more GSTR 3B returns. Kindly file your returns immediately to avoid late fee and Interest. Ignore if filed. GSTN",
            "entity_name": "march_ending",
            "category": "UTILITY",
            "template_id": "759559305816228",
            "header": null,
            "header_type": null,
            "template_type": "TEXT",
            "sub_type": null,
            "buttons": null,
            "footer": null,
            "url": null,
            "example": null,
            "example_website": null,
            "url_name": null,
            "created_at": "2023-03-25T13:26:20.034623+05:30",
            "updated_at": null,
            "status": 0, // 
            "rejected_reason": null,
            "added_by": 156,
            "lang_code": "en"
        }
    ]
}
```

This API allows you to Get all approval pending Templates from your WABA account using Sobot platform. API response is paginated with page size of 20.


### HTTP Request

`GET https://api.sobot.in/api/template/?status=1`

### Response Parameters

**First level Keys**

Parameter | Description | 
--------- | ----------- |
Data | Array of json objects of template data. Check below table for detail object specification.|
count | Total count of templates in your account |
size | size of a current page |
next | Link to the next page (if any, else null)
previous | Link to the previous page (if any, else null) |
code | 200 in case of success. Check Errors for other codes. |


**Data Object**

Parameter | Description |
--------- | ----------- | 
| id              | System generated ID for each template |
| template        | Body of the template. Usually a text including Emojis, variables, markdown for formatting. |
| entity_name     | Name of the template |
| category        | Category of template It can be: <ul><li>Marketing</li><li>Utility</li><li>Authentication</li></ul>  |
| template_type   | Template type value can be: <ul><li>TEXT</li><li>MEDIA</li></ul> |
| lang_code       | Language code of ```template``` content. Actaully denotes the Language of the template. |
| template_id     | A Meta generated unique ID for template. You can refer this for future operations. |
| header          | Text of header in case of ```header_type = Text```.|
| header_type     | Header type value can be: <ul><li>TEXT</li><li>IMAGE</li><li>VIDEO</li><li>DOUCMENT</li></ul> |
| footer          | Text of footer. It can have emojis in it. |
| example         | a public URL of header data excpet for ```TEXT```. |
| sub_type        | This can be either ```null``` or ```CTA```. If it is set to ```CTA ```, it specifies that this template has CTAs in its button. CTAs can be either phone numbers and/or website. For phone number check ```phone_numbers``` and for website check ```url```, ```url_name``` and ```example_website``` |
| buttons         | This helps to identify buttons (Quick reply) of templates. It will return array of strings. <br /> <br /> e.g. ["Yes", "NO", "May be"] |
| phone_numbers   | This return json object with following keys: <ul><li>phone_number: A phone number with country-code e.g. 919970XXXXXX</li><li>text: Name of CTA button</li></ul> |
| url             | If  ```sub_type ``` is set to CTA, and added CTA is a website, this parameter will give you static part of URL. |
| example_website | If  ```sub_type ``` is set to CTA, and added CTA is a website, this parameter will give you example value of variable that was added in ```url```.  |
| url_name        | If  ```sub_type ``` is set to CTA, and added CTA is a website, this parameter will give you name to be shown for CTA button. |
| created_at      | Date of template creation. Its a timestamp. <br/> <br/> e.g. 2023-03-25T13:26:20.034623+05:30 |
| updated_at      | Date of template last updated. Its a timestamp. <br/> <br/> e.g. 2023-03-25T13:26:20.034623+05:30 |
| status          | Status of the template. In thi case its always ```1``` for approved templates. |
| rejected_reason | Reason of rejection, if the template ```status = 2``` i.e. Rejected. Else, this is always ```null``` |
| added_by        | The unique ID of a user who has added this template on Sobot Platform.  |

## Get Rejected Templates
```shell
curl --location --globoff 'https://api.sobot.in/api/template/?status=2' \
--header 'x-api-key: yourapiaccesskey' \
--header 'x-api-secret: yourapisecretkey' \
--header 'content-type': 'application/json' \
```

```python
import requests
import json
url = "https://api.sobot.in/api/template/?status=2"
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
$request->setUrl('https://api.sobot.in/api/template/?status=2');
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
    "count": 80,
    "size": 20,
    "next": "http://api.sobot.in/api/template/?status=2&page=2",
    "previous": null,
    "code": 200,
    "data": [
        {
            "id": 584,
            "phone_numbers": null,
            "template": "Dear customer,\n\nYou have not filed one or more GSTR 3B returns. Kindly file your returns immediately to avoid late fee and Interest. Ignore if filed. GSTN",
            "entity_name": "march_ending",
            "category": "UTILITY",
            "template_id": "759559305816228",
            "header": null,
            "header_type": null,
            "template_type": "TEXT",
            "sub_type": null,
            "buttons": null,
            "footer": null,
            "url": null,
            "example": null,
            "example_website": null,
            "url_name": null,
            "created_at": "2023-03-25T13:26:20.034623+05:30",
            "updated_at": null,
            "status": 0, // 
            "rejected_reason": null,
            "added_by": 156,
            "lang_code": "en"
        }
    ]
}
```

This API allows you to Get all approval pending Templates from your WABA account using Sobot platform. API response is paginated with page size of 20.


### HTTP Request

`GET https://api.sobot.in/api/template/?status=2`

### Response Parameters

**First level Keys**

Parameter | Description | 
--------- | ----------- |
Data | Array of json objects of template data. Check below table for detail object specification.|
count | Total count of templates in your account |
size | size of a current page |
next | Link to the next page (if any, else null)
previous | Link to the previous page (if any, else null) |
code | 200 in case of success. Check Errors for other codes. |


**Data Object**

Parameter | Description |
--------- | ----------- | 
| id              | System generated ID for each template |
| template        | Body of the template. Usually a text including Emojis, variables, markdown for formatting. |
| entity_name     | Name of the template |
| category        | Category of template It can be: <ul><li>Marketing</li><li>Utility</li><li>Authentication</li></ul>  |
| template_type   | Template type value can be: <ul><li>TEXT</li><li>MEDIA</li></ul> |
| lang_code       | Language code of ```template``` content. Actaully denotes the Language of the template. |
| template_id     | A Meta generated unique ID for template. You can refer this for future operations. |
| header          | Text of header in case of ```header_type = Text```.|
| header_type     | Header type value can be: <ul><li>TEXT</li><li>IMAGE</li><li>VIDEO</li><li>DOUCMENT</li></ul> |
| footer          | Text of footer. It can have emojis in it. |
| example         | a public URL of header data excpet for ```TEXT```. |
| sub_type        | This can be either ```null``` or ```CTA```. If it is set to ```CTA ```, it specifies that this template has CTAs in its button. CTAs can be either phone numbers and/or website. For phone number check ```phone_numbers``` and for website check ```url```, ```url_name``` and ```example_website``` |
| buttons         | This helps to identify buttons (Quick reply) of templates. It will return array of strings. <br /> <br /> e.g. ["Yes", "NO", "May be"] |
| phone_numbers   | This return json object with following keys: <ul><li>phone_number: A phone number with country-code e.g. 919970XXXXXX</li><li>text: Name of CTA button</li></ul> |
| url             | If  ```sub_type ``` is set to CTA, and added CTA is a website, this parameter will give you static part of URL. |
| example_website | If  ```sub_type ``` is set to CTA, and added CTA is a website, this parameter will give you example value of variable that was added in ```url```.  |
| url_name        | If  ```sub_type ``` is set to CTA, and added CTA is a website, this parameter will give you name to be shown for CTA button. |
| created_at      | Date of template creation. Its a timestamp. <br/> <br/> e.g. 2023-03-25T13:26:20.034623+05:30 |
| updated_at      | Date of template last updated. Its a timestamp. <br/> <br/> e.g. 2023-03-25T13:26:20.034623+05:30 |
| status          | Status of the template. In thi case its always ```2``` for rejected templates. |
| rejected_reason | Reason of rejection, if the template ```status = 2``` i.e. Rejected. Else, this is always ```null``` |
| added_by        | The unique ID of a user who has added this template on Sobot Platform.  |