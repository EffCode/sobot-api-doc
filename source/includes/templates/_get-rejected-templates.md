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