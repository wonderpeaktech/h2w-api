# hate2wait API Documentation

[![N|Solid](https://business.hatetowaitapp.com/assets/logo.png)](https://nodesource.com/products/nsolid)


# Quick Reference
The hate2wait API endpoint is https://app.hate2wait.io/api/v1 and all paths below are relative to that. hate2wait uses HTTP Basic Auth for authentication and all calls must be over HTTPS.

### List All Locations
List of all locations

### GET /locations
### Request Example


```sh
$ curl https://app.hate2wait.io/api/v1/locations
-H "Authorization: h2w-authtoken ba4604e8e433g9c892e360d53463oec5"
-H "Content-Type: application/json;charset=UTF-8"
```

### Response Example


```sh
HTTP/1.1 200 OK
Content-Type:application/json;charset=UTF-8
{
    "code": 0,
    "message": "success",
    "locations": [
        {
            "location_id": "903000000000099",
            "location_name": "Bowman Furniture",
            "location_address": "Mr.",
            "location_code": "Benjamin",
            "google_map_position": "",
            "manager_name": "George",
            "manager_email": "benjamin.george@bowmanfurniture.com",
            "manager_phone": 23467278,
            "updated_time": "2016-06-05T02:30:08-0700",
            "created_time": "2016-06-05T12:30:08-0700"
        },
        {...},
        {...}
    ]
}

```



License
----

Wonder Peak Tech Pvt. Ltd.

