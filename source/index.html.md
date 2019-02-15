---
title: GoHire API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

search: true
---
# GoHire

GoHire API Documentation
<br>
<br>
`All endpoint requests should be authorized, must contain an api-key.`

## Contact search

```shell
curl -X POST --header 'Content-Type: application/json' --header 'api-key: <key>' -d '{
  "searchKey": "test",
  "groupContacts": "[{\"id\":\"aeb3d11c-301c-11e9-b210-d663bd873d93\"}]",
  "pagination": "{\"numberOfRows\":20,\"page\":1}",
  "filter": "name"
}' 'http://beta.gohire.com:8787/api/v1/contacts/search'
```

> The above command returns JSON structured like this:

```json
{
  "statusCode": 200,
  "data": {
    "rows": [
      {
        "id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
        "mobile": "+11234567890",
        "name": "test test",
        "botmap_id": null,
        "deleted_at": null,
        "created_at": "2019-02-13T06:12:39.912Z",
        "updated_at": "2019-02-13T06:12:39.912Z",
        "company_id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
        "blacklist": false,
        "department_id": null,
        "status": null,
        "notes": null,
        "meta": null,
        "lat": null,
        "lng": null,
        "default_department": null,
        "source": null,
        "contactdetails": [
          {
            "contact_id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
            "field": "mobile",
            "value": "+11234567890",
            "created_at": "2019-02-13T06:12:39.921Z",
            "updated_at": "2019-02-13T06:12:39.921Z"
          }
        ],
        "value": "+11234567890"
      }
    ],
    "total": 1
  }
}
```

This endpoint will return searched contacts.

### HTTP Request

`POST /api/v1/contacts/search`

### Request Payload
Payload | Data Type | Data Description | Required
--------- | ------- | ----------- | ------
`searchKey` | `String` | `Contact's search key` | `no`
`groupContacts` | `JSON String` | `Contacts to exclude from search data: [{id: "1"}]` | `no`
`pagination` | `JSON String` | `Page details data: {numberOfRows: 1, page: 1}` | `no`
`filter` | `String` | `Search type - 'name', 'phone'. ` | `no`

<aside class="success">Authorized</aside>

## Get all contacts

```shell
curl -X GET --header 'api-key: <key>' 
'http://beta.gohire.com:8787/api/v1/companies/aeb3d11c-301c-11e9-b210-d663bd873d93/%7B%22numberOfRows%22%3A20%2C%22page%22%3A1%7D
%7B%22field%22%3A%22contact.name%22%2C%22filterVal%22%3A%22sample%20user%22%7D/contacts'
```

> The above command returns JSON structured like this:

```json
{
  "statusCode": 200,
  "data": {
    "rows": [
      {
        "created_at": "2018-11-21T10:49:36.544Z",
        "id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
        "name": "sample user",
        "mobile": "",
        "status": null,
        "notes": null
      }
    ],
    "total": 1,
    "contacts": [
      {
        "created_at": "2018-11-21T10:49:36.544Z",
        "id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
        "name": "sample user",
        "mobile": "",
        "status": null,
        "notes": null
      }
    ]
  }
}
```

This endpoint will return contacts by company.

### HTTP Request

`GET /api/v1/companies/{id}/{paginate}/{filters}/contacts`

### Request Parameter
Parameter | Data Type | Data Description | Required
--------- | ------- | ----------- | ------
`id` | `String` | `Company ID` | `yes`
`paginate` | `URL encoded` | `Page details data: {numberOfRows: 1, page: 1}` | `yes`
`filters` | `URL encoded` | `Employee search filters data: {field: "sample", fieldVal: "sample"}` | `no`

<aside class="success">Authorized</aside>

## Add contact

```shell
curl -X POST --header 'Content-Type: application/json' --header 'api-key: <key>' -d '{
  "company_id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
  "firstname": "test",
  "lastname": "test",
  "mobile": "+19388887884",
  "status": "active",
  "notes": "test",
  "botMapDetails": {"botmap_id": "aeb3d11c-301c-11e9-b210-d663bd873d93", "id":"aeb3d11c-301c-11e9-b210-d663bd873d93", "mobile": "+19388887884", "name": "GoHire Test Number", "type": "twilio"}
}' 'http://beta.gohire.com:8787/api/v1/contacts'
```

> The above command returns JSON structured like this:

```json
{
  "statusCode": 200,
  "data": "aeb3d11c-301c-11e9-b210-d663bd873d93"
}
```

This endpoint will create a new contact.

### HTTP Request

`POST api/v1/contacts`

### Request Payload
Payload | Data Type | Data Description | Required
--------- | ------- | ----------- | ------
`company_id` | `String` | `Company ID` | `yes`
`fistname` | `String` | `Contact's first name` | `yes`
`lastname` | `String` | `Contact's last name` | `yes`
`mobile` | `String` | `Mobile number` | `yes`
`status` | `String` | `Contact status`  | `no`
`notes` | `String` | `Contact notes` | `no`
`botMapDetails` | `Object` | `Bot details data: {botmap_id: "1", id: "1", mobile: "1", name: "1", type: "1"}`  | `yes`

<aside class="success">Authorized</aside>

## Send SMS to contact

```shell
curl -X POST --header 'Content-Type: application/json' --header 'api-key: <key>' -d '{
"to": "+11234567890",
  "body": "Hello",
  "firstname": "test",
  "lastname": "test",
  "sendType": "new-message"
}' 'http://beta.gohire.com:8787/api/v1/conversation/send'
```

> The above command returns JSON structured like this:

```json
{
  "statusCode": 200,
  "data": {
    "convoRes": {
      "bot_name": "Default short code",
      "bot_mobile": "GH-5f11206b89",
      "bot_id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
      "type": "messagemedia",
      "app_name": "test test",
      "app_mobile": "+11234567890",
      "botblacklisted": false,
      "botmap_id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
      "completed": false,
      "contact_id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
      "created_at": "2019-02-13T09:28:10.555Z",
      "id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
      "talk_to_agent": true,
      "updated_at": "2019-02-13T10:51:46.084Z"
    },
    "messageRes": [
      {
        "id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
        "message": "Hello",
        "conversation_id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
        "direction": "outbound",
        "to": "+11234567890",
        "from": "GH-5f11206b89",
        "meta": "{\"body\":\"Hello\",\"to\":\"+11234567890\",\"from\":\"GH-5f11206b89\",\"status\":\"queued\"}",
        "created_at": "2019-02-13T10:51:46.060Z",
        "updated_at": "2019-02-13T10:51:46.060Z",
        "deleted_at": null
      }
    ],
    "contact": {
      "id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
      "mobile": "+11234567890",
      "name": "test test",
      "botmap_id": null,
      "deleted_at": null,
      "created_at": "2019-02-13T05:55:11.867Z",
      "updated_at": "2019-02-13T05:55:11.867Z",
      "company_id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
      "blacklist": false,
      "department_id": null,
      "status": "active",
      "notes": "test",
      "meta": null,
      "lat": null,
      "lng": null,
      "default_department": null,
      "source": null
    }
  }
}
```

This endpoint will send a new message and returns a success message.

### HTTP Request

`POST /api/v1/conversation/send`

### Request Payload
Payload | Data Type | Data Description | Required
--------- | ------- | ----------- | ------
`to` | `String` | `Contact's number` | `yes`
`body` | `String` | `Message` | `yes`
`firstname` | `String` | `Contact's first name` | `no`
`lastname` | `String` | `Contact's last name` | `no`
`sendType` | `String` | `Message type` | `yes`
`botmapId` | `String` | `Bot ID` | `no`
`contactId` | `String` | `Contact ID` | `no`
`moduleGroup` | `String` | `Module Group` | `no`

<aside class="success">Authorized</aside>

## View conversations

```shell
curl -X GET --header 'api-key: <key>' 
'http://beta.gohire.com:8787/api/v1/userbot/conversations?limit=1&next=1'
```

> The above command returns JSON structured like this:

```json
{
  "statusCode": 200,
  "data": [
    {
      "id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
      "botmap_id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
      "contact_id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
      "bot_name": "Default short code",
      "bot_mobile": "GH-5f11206b89",
      "app_name": "test send",
      "app_mobile": "+12252300108",
      "contact_meta": null,
      "updated_at": "2019-02-13T09:27:04.568Z",
      "type": "messagemedia",
      "contactDetails": [
        {
          "contact_id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
          "field": "firstname",
          "value": "test",
          "created_at": "2018-12-17T06:02:30.507Z",
          "updated_at": "2018-12-17T06:02:30.507Z"
        },
        {
          "contact_id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
          "field": "lastname",
          "value": "send",
          "created_at": "2018-12-17T06:02:30.507Z",
          "updated_at": "2018-12-17T06:02:30.507Z"
        },
        {
          "contact_id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
          "field": "mobile",
          "value": "+12252300108",
          "created_at": "2018-12-17T06:02:30.507Z",
          "updated_at": "2018-12-17T06:02:30.507Z"
        }
      ]
    }
  ]
}
```

This endpoint will return all conversations.

### HTTP Request

`GET /api/v1/userbot/conversations`

### Request Queries
Queries | Data Type | Data Description | Required
--------- | ------- | ----------- | ------
`limit` | `integer` | `Number of entries per page` | `no`
`next` | `integer` | `Offset or next set` | `no`

<aside class="success">Authorized</aside>

## View conversation threads

```shell
curl -X GET --header 'api-key: <key>' 
'http://beta.gohire.com:8787/api/v1/conversations/aeb3d11c-301c-11e9-b210-d663bd873d93/threads'
```

> The above command returns JSON structured like this:

```json
{
  "statusCode": 200,
  "data": [
    {
      "id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
      "message": "",
      "conversation_id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
      "direction": "inbound",
      "to": "+19388887884",
      "from": "+19388887884",
      "meta": "",
      "created_at": "2019-02-13T06:04:45.941Z",
      "updated_at": "2019-02-13T06:04:45.941Z",
      "deleted_at": null,
      "conversation": {
        "id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
        "botmap_id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
        "contact_id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
        "completed": false,
        "deleted_at": null,
        "created_at": "2019-02-13T06:04:45.932Z",
        "updated_at": "2019-02-13T06:04:45.941Z",
        "talk_to_agent": false,
        "botblacklisted": false,
        "botmap": {
          "id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
          "bot_id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
          "mobile": "+19388887884",
          "deleted_at": null,
          "created_at": "2018-12-17T02:57:10.582Z",
          "updated_at": "2018-12-17T02:57:10.582Z",
          "type": "twilio",
          "page_token": null,
          "desktop_view": "full",
          "mobile_view": "full",
          "default": null
        }
      }
    }
  ]
}
```

This endpoint will return threads with the given id.

### HTTP Request

`GET /api/v1/conversations/{contactId}/threads`

### Request Parameter
Parameter | Data Type | Data Description | Required
--------- | ------- | ----------- | ------
`id` | `String` | `Contact ID` | `yes`

### Query Parameter
Query | Data Type | Data Description | Required
--------- | ------- | ----------- | ------
`page` | `integer` | `Page number`| `no`
`convoType` | `String` | `Conversation Type` | `no`

<aside class="success">Authorized</aside>

## View groups

```shell
curl -X GET --header 'api-key: <key>' 
'http://beta.gohire.com:8787/api/v1/groups'
```

> The above command returns JSON structured like this:

```json
{
  "statusCode": 200,
  "data": [
    {
      "id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
      "name": "Group-20181113-18:32",
      "deleted_at": null,
      "created_at": "Nov 13 2018",
      "updated_at": "2018-11-13T10:32:47.352Z",
      "user_id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
      "contact_count": "162",
      "campaign_count": "1"
    },
    {
      "id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
      "name": "Import-20181018-14:27",
      "deleted_at": null,
      "created_at": "Oct 18 2018",
      "updated_at": "2018-10-18T06:27:32.329Z",
      "user_id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
      "contact_count": "1",
      "campaign_count": "0"
    }
  ]
}
```

This endpoint will return all groups.

### HTTP Request

`GET /api/v1/groups`

<aside class="success">Authorized</aside>

## View specific group

```shell
curl -X GET --header 'api-key: <key>' 
'http://beta.gohire.com:8787/api/v1/groups/aeb3d11c-301c-11e9-b210-d663bd873d93'
```

> The above command returns JSON structured like this:

```json
{
  "statusCode": 200,
  "data": {
    "id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
    "name": "Group-20181113-18:32",
    "deleted_at": null,
    "created_at": "Nov 13 2018",
    "updated_at": "2018-11-13T10:32:47.352Z",
    "user_id": "aeb3d11c-301c-11e9-b210-d663bd873d93"
  }
}
```

This endpoint will return the specific group.

### HTTP Request

`GET /api/v1/groups/{group_id}`

### Request Parameter
Parameter | Data Type | Data Description | Required
--------- | ------- | ----------- | ------
`group_id` | `String` | `Group ID` | `yes`

<aside class="success">Authorized</aside>

## View contacts in group

```shell
curl -X GET --header 'api-key: <key>' 
'http://beta.gohire.com:8787/api/v1/groups/aeb3d11c-301c-11e9-b210-d663bd873d93/contacts/%7B%22numberOfRows%22%3A1%2C%22page%22%3A1%7D'
```

> The above command returns JSON structured like this:

```json
{
  "statusCode": 200,
  "data": {
    "rows": [
      {
        "id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
        "mobile": "+17866635574",
        "name": "Louverture Dordoye",
        "botmap_id": null,
        "deleted_at": null,
        "created_at": "2018-11-13T10:32:47.477Z",
        "updated_at": "2018-11-13T10:32:47.477Z",
        "company_id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
        "blacklist": false,
        "department_id": null,
        "status": null,
        "notes": null,
        "meta": null,
        "lat": null,
        "lng": null,
        "default_department": null,
        "source": "Imported",
        "contactdetail": [
          {
            "contact_id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
            "field": "email",
            "value": "Louverturedordoye@yahoo.com",
            "created_at": "2018-11-13T10:32:48.164Z",
            "updated_at": "2018-11-13T10:32:48.164Z"
          },
          {
            "contact_id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
            "field": "mobile",
            "value": "+17866635574",
            "created_at": "2018-11-13T10:32:48.164Z",
            "updated_at": "2018-11-13T10:32:48.164Z"
          }
        ]
      }
    ],
    "total": 162
  }
}
```

This endpoint will return all contacts in group.

### HTTP Request

`GET /api/v1/groups/{group_id}/contacts/{paginate}`

### Request Parameter
Parameter | Data Type | Data Description | Required
--------- | ------- | ----------- | ------
`group_id` | `String` | `Group ID` | `yes`
`paginate` | `URL encoded`| `Page details data: {numberOfRows: 1, page: 1}` | `yes`

<aside class="success">Authorized</aside>

## Create group

```shell
curl -X POST --header 'Content-Type: application/json' --header 'api-key: <key>' -d '{
  "groupName": "test1",
  "groupContacts": "[\"b8d3922d-948c-43f9-9c7b-dd9a654a72d2\"]"
}' 'http://beta.gohire.com:8787/api/v1/groups'
```

> The above command returns JSON structured like this:

```json
{
  "statusCode": 200,
  "data": "Success"
}
```

This endpoint will create group and returns a success message.

### HTTP Request

`POST /api/v1/groups`

Payload | Data Type | Data Description | Required
--------- | ------- | ----------- | ------
`groupName` | `String` | `Group's name` | `yes`
`groupContacts` | `JSON String` | `Contact ID's to add data: ["id"]` | `yes`

<aside class="success">Authorized</aside>

## Edit group details

```shell
curl -X PUT --header 'Content-Type: application/json' --header 'api-key: <key>' -d '{
  "name": "test edit"
}' 'http://beta.gohire.com:8787/api/v1/groups/a973b472-aca1-4b1b-808c-6839d584166e'
```

> The above command returns JSON structured like this:

```json
{
  "statusCode": 200,
  "data": "Success"
}
```

This endpoint will edit group and returns a success message.

### HTTP Request

`PUT /api/v1/groups/{id}`

### Request Parameter
Parameter | Data Type | Data Description | Required
--------- | ------- | ----------- | ------
`id` | `String` | `Group ID` | `yes`

### Request Payload
Payload | Data Type | Data Description | Required
--------- | ------- | ----------- | ------
`name` | `String` | `Group name` | `no`

<aside class="success">Authorized</aside>

## Add contacts to group

```shell
curl -X POST --header 'Content-Type: application/json' --header 'api-key: <key>' -d '{
  "contacts": "[\"b8d3922d-948c-43f9-9c7b-dd9a654a72d2\"]}"
}' 'http://beta.gohire.com:8787/api/v1/groups/a973b472-aca1-4b1b-808c-6839d584166e/contacts'
```

> The above command returns JSON structured like this:

```json
{
  "statusCode": 200,
  "data": "Success"
}
```

This endpoint will add contacts to group and returns a success message.

### HTTP Request

`POST /api/v1/groups/{id}/contacts`

### Request Parameter
Parameter | Data Type | Data Description | Required
--------- | ------- | ----------- | ------
`id` | `String` | `Group ID` | `yes`

### Request Payload
Payload | Data Type | Data Description | Required
--------- | ------- | ----------- | ------
`contacts` | `Array` | `Contact ID's to add data: ["id"]` | `yes`

<aside class="success">Authorized</aside>

## Remove contacts from group

```shell
curl -X PUT --header 'Content-Type: application/json' --header 'api-key: <key>' -d '{
  "contacts": "[\"b8d3922d-948c-43f9-9c7b-dd9a654a72d2\"]"
}' 'http://beta.gohire.com:8787/api/v1/groups/35babf35-c5f6-4fc1-8c4d-c996e5c4db62/contacts'
```

> The above command returns JSON structured like this:

```json
{
  "statusCode": 200,
  "data": "Success"
}
```

This endpoint will remove contacts from group and returns a success message.
### HTTP Request

`PUT /api/v1/groups/{id}/contacts`

### Request Parameter
Parameter | Data Type | Data Description | Required
--------- | ------- | ----------- | ------
`id` | `String` | `Group ID` | `yes`


### Request Payload
Payload | Data Type | Data Description | Required
--------- | ------- | ----------- | ------
`contacts` | `Array` | `Contact ID's to add data: ["id"]` | `yes`

<aside class="success">Authorized</aside>

## View campaign

```shell
curl -X GET --header 'api-key: <key>' 
'http://beta.gohire.com:8787/api/v1/campaigns'
```

> The above command returns JSON structured like this:

```json
{
  "statusCode": 200,
  "data": [
    {
      "id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
      "user_id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
      "group_id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
      "name": "test campaign edit",
      "message": "test message",
      "timezone": "-07:00",
      "schedule": "Feb 14, 2019 03:31 PM",
      "status": false,
      "is_active": false,
      "created_at": "2019-02-13T10:32:53.886Z",
      "updated_at": "2019-02-13T10:44:42.037Z",
      "is_inprogress": false,
      "nontcpa_count": 0,
      "modulegroup_id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
      "user": {
        "id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
        "name": "nicolereya@gmail.com",
        "username": "nicolereya@gmail.com",
        "password": "$2a$10$nxvBZAyTXwfgN0EEwFTz0OfZ29A61NnjDuo6L/DOwumxI/8ETyJhS",
        "department_id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
        "deleted_at": null,
        "created_at": "2018-10-04T11:27:15.021Z",
        "updated_at": "2018-11-12T05:59:58.042Z",
        "text_optin": "yes",
        "text_optin_created_at": "2018-11-12 05:59:58.04283+00",
        "text_optout_created_at": null,
        "mobile": "",
        "desktop_notification": false,
        "email_notification": false,
        "sms_notification": false,
        "nickname": "",
        "email": "nicolereya@gmail.com",
        "active": false,
        "job_title": "",
        "new_user": false,
        "sms_default": "shortcode",
        "department": {
          "id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
          "name": "HQ",
          "company_id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
          "deleted_at": null,
          "created_at": "2018-09-06T11:27:15.021Z",
          "updated_at": "2018-09-06T11:27:15.021Z",
          "keyword": null,
          "address1": null,
          "city": null,
          "state": null,
          "zipcode": null,
          "address2": null,
          "location_url": null,
          "customer_department_id": null,
          "directions": null,
          "phone_number": null,
          "recruiting_email": null,
          "primary_user_contact_name": null,
          "recruiting_phone": null,
          "primary_user_phone": null,
          "lat": null,
          "lng": null
        }
      },
      "group": {
        "id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
        "name": "test group campaign",
        "deleted_at": null,
        "created_at": "2019-02-13T07:19:21.230Z",
        "updated_at": "2019-02-13T07:19:21.230Z",
        "user_id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
        "contactgroups": [
          {
            "contact_id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
            "group_id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
            "deleted_at": null,
            "created_at": "2019-02-13T07:19:21.236Z",
            "updated_at": "2019-02-13T07:19:21.236Z"
          }
        ]
      },
      "broadcasthistories": [],
      "username": "nicolereya@gmail.com",
      "companyName": "Lanex",
      "noOfContacts": 1,
      "noOfAttempts": 1,
      "msgSent": 0,
      "msgDelivered": 0,
      "msgFailed": 0
    }
  ]
}
```

This endpoint will return all campaigns.

### HTTP Request

`GET /api/v1/campaigns`

<aside class="success">Authorized</aside>

## View specific campaign

```shell
curl -X GET --header 'api-key: <key>' 
'http://beta.gohire.com:8787/api/v1/campaigns/aeb3d11c-301c-11e9-b210-d663bd873d93'
```

> The above command returns JSON structured like this:

```json
{
  "statusCode": 200,
  "data": {
    "id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
    "user_id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
    "group_id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
    "name": "test campaign",
    "message": "test message",
    "timezone": "-07:00",
    "schedule": "Feb 14, 2019 03:31 PM",
    "status": false,
    "is_active": false,
    "created_at": "2019-02-13T10:32:53.886Z",
    "updated_at": "2019-02-13T10:32:53.886Z",
    "is_inprogress": false,
    "nontcpa_count": 0,
    "modulegroup_id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
    "group": {
      "id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
      "name": "test group campaign",
      "deleted_at": null,
      "created_at": "2019-02-13T07:19:21.230Z",
      "updated_at": "2019-02-13T07:19:21.230Z",
      "user_id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
      "contactgroups": [
        {
          "contact_id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
          "group_id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
          "deleted_at": null,
          "created_at": "2019-02-13T07:19:21.236Z",
          "updated_at": "2019-02-13T07:19:21.236Z"
        }
      ]
    },
    "broadcasthistories": [],
    "noOfContacts": 1,
    "noOfAttempts": 1,
    "msgSent": 0,
    "msgDelivered": 0,
    "msgFailed": 0
  }
}
```

This endpoint will return a specific campaign.

### HTTP Request

`GET /api/v1/campaigns/{id}`

### Request Parameter
Parameter | Data Type | Data Description | Required
--------- | ------- | ----------- | ------
`id` | `String` | `Campaign ID` | `no`

<aside class="success">Authorized</aside>

## Create campaign

```shell
curl -X POST --header 'Content-Type: application/json' --header 'api-key: <key>' -d '{
  "campaign_name": "test campaign",
  "message": "test message",
  "schedule": "Feb 14, 2019 03:31 PM",
  "timezone": "-07:00",
  "group_id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
  "modulegroup_id": "aeb3d11c-301c-11e9-b210-d663bd873d93"
}' 'http://beta.gohire.com:8787/api/v1/campaigns'
```

> The above command returns JSON structured like this:

```json
{
  "statusCode": 200,
  "data": "Success"
}
```

This endpoint will create a campaign and returns a success message.

### HTTP Request

`POST /api/v1/campaigns`

### Request Payload
Payload | Data Type | Data Description | Required
--------- | ------- | ----------- | ------
`campaign_name` | `String` | `Campaign name` | `yes`
`message` | `String` | `Campaign message` | `no`
`schedule` | `String` | `Campaign schedule` | `no`
`timezone` | `String` | `Schedule time zone` | `no`
`group_id` | `String` | `Existing group's ID` | `no`
`group_name` | `String` | `New group's name` | `no`
`file` | `String` | `CSV file containing contact details` | `no`
`selected_fields` | `JSON String` | `List of fields to import data: ["fieldname"]` | `no`
`deleted_rows` | `JSON String` | `List of contacts to exclude from import data: ["row_number"]` | `no`

<aside class="success">Authorized</aside>

## Edit campaign

```shell
curl -X PUT --header 'Content-Type: application/json' --header 'api-key: <key>' -d '{
  "name": "test campaign edit",
  "message": "test message",
  "group_id": "aeb3d11c-301c-11e9-b210-d663bd873d93",
  "schedule": "Feb 14, 2019 03:31 PM",
  "timezone": "-07:00",
  "status": "open"
}' 'http://beta.gohire.com:8787/api/v1/campaigns/0f420880-2e19-43bd-8ea4-201f4ac9227d'
```

> The above command returns JSON structured like this:

```json
{
  "statusCode": 200,
  "data": "Success"
}
```

This endpoint will delete a campaign and returns a success message.

### HTTP Request

`PUT /api/v1/campaigns/{id}`

### Request Parameter
Parameter | Data Type | Data Description | Required
--------- | ------- | ----------- | ------
`id` | `String` | `Campaign ID` | `yes`

### Request Payload
Payload | Data Type | Data Description | Required
--------- | ------- | ----------- | ------
`name` | `String` | `Campaign name` | `no`
`message` | `String` | `Campaign message` | `no`
`group_id` | `String` | `Group ID` | `no`
`schedule` | `String` | `Campaign schedule` | `no`
`timezone` | `String` | `Schedule time zone` | `no`
`status` | `String` | `Campaign status` | `no`
`is_active` | `Boolean` | `for admin only. Review status` | `no`

<aside class="success">Authorized</aside>