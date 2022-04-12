# Greymarket_api
It is used for RFID scanning equipment to access greymarket app

# Document & Toys
swagger:
https://app.swaggerhub.com/apis/sam135/device_api/1.0.0

greymarket.app admin login:
https://greymarket.app/admin/

api test:
https://greymarket.app/api/test

## Device login
Each device needs to have a separate login account. The login account can be added in "admin".
### `Post https://greymarket.app/api/login`
#### Parameters
`req` _(string*)_ 

Request parameters

Example:
```json
{
  "username": "Desk1All4Labels",
  "password": "yujie301415",
  "deviceid": "desk001", //Identification ID of the device
  "localip": "192.168.0.123", //IP of device in LAN
  "devicetype": "desktop" //Device type desktop or handheld
}
```
#### Response

Example:
```json
{
  "code":1, //1 is returned for success and 0 is returned for error
  "ticket":"ZAC3RbweCsDG88nD7F3wEZncampMfknY", //It is used for identity verification when submitting information later
  "message":"", //If an error occurs, an error message is returned
  "timeStamp":1649766284712
}
```

## Heart beat

Maintain equipment online status

### `Post https://greymarket.app/api/heartbeat`
#### Parameters
`req` _(string*)_ 

Request parameters

Example:
```json
{
  "username": "Desk1All4Labels", //Logged username
  "ticket": "ZAC3RbweCsDG88nD7F3wEZncampMfknY", //Ticket obtained when logging in
  "state": "ready" //Describe device status
}
```

#### Response

Example:
```json
{
  "code":1,
  "message":"",
  "timeStamp":1649768167629
}
```

## Box class

Get boxclass list

### `Post https://greymarket.app/api/boxclass`
#### Parameters
`req` _(string*)_ 

Request parameters

Example:
```json
{
  "username": "Desk1All4Labels",
  "ticket": "ZAC3RbweCsDG88nD7F3wEZncampMfknY"
}
```

#### Response

Example:
```json
{
  "code":1,
  "message":"",
  "timeStamp":1649768478002,
  "data":[
            {
              "classid":"304F3", //Common parts of box type EPC, used to identify box type
              "itemquantity":24 //Number of items in a box
            }
         ]
}
```

## Add box

Upload the EPC of box and items to add box and items

### `Post https://greymarket.app/api/addbox`
#### Parameters
`req` _(string*)_ 

Request parameters

Example:
```json
{
  "username": "Desk1All4Labels",
  "ticket": "ZAC3RbweCsDG88nD7F3wEZncampMfknY",
  "box": "304F3F7618E06A80000000CD",
  "items": [
    "302F3F7618E06A8000000008",
    "302F3F7618E06A8000000009"
  ]
}
```

#### Response

Example:
```json
{
  "code":1,
  "message":"",
  "insertedBox":"304F3F7618E06A80000000CD", //"Box EPC" affected by this operation
  "items":["302F3F7618E06A8000000008","302F3F7618E06A8000000009"] //Items list in box
  "insertedItems":["302F3F7618E06A8000000009"], //Successfully added "item EPC". Not in this list indicates that it has been added before
  "timeStamp":1649768905472
}
```
