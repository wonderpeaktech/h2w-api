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
| Response Fields | Description |
| ------ | ------ |
| location_id | A unique location id |
| location_name | Name of a location  |
| location_address | Complete address of a location |
| location_code | Code of a location if set any during creation |
| google_map_postition | Position (latitude, longitude) of a location on google map |
| manager_name | Name of the location manager |
| manager_email | Email of the location manager |
| manager_phone | Contact No of the location manager |
| created_time | Time when the location was created |
| updated_time | Time when the location was last updated |


### List of all the queues of a location
List of all the queues created for a particular location.

### GET /{location_id}/queues
### Request Example


```sh
$ curl https://app.hate2wait.io/api/v1/{location_id}/queues
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
    "queues": [
        {
            "queue_id": "903000000000099",
            "queue_name": "Bowman Furniture",
            "updated_time": "2016-06-05T02:30:08-0700",
            "created_time": "2016-06-05T12:30:08-0700"
        },
        {...},
        {...}
    ]
}

```
| Response Fields | Description |
| ------ | ------ |
| queue_id | A unique queue id |
| queue_name | Name of a queue  |
| created_time | Time when the location was created |
| updated_time | Time when the location was last updated |

### Create a queue booking
Create a queue booking.

### POST /queue_bookings
### Request Example


```sh
$ curl https://app.hate2wait.io/api/v1/queue_bookings
-H "Authorization: h2w-authtoken ba4604e8e433g9c892e360d53463oec5"
-H "Content-Type: application/json;charset=UTF-8"
-d '{
    "queue_id": "23213dasda212121",
    "first_name": "John",
    "last_name": "Doe",
    "phone_number": "9999999999",
    "source": "app",
    "additional_info": {
        "gender": "male",
        "dob": "13-05-1992",
        "notes": "",
        "latitude": "",
        "longitude": ""
    }
    
}
```

| Request Parameters | Description |
| ------ | ------ |
| queue_id | The ID of the queue for which you want to create a booking (required) |
| first_name | First name of the person for whom booking is created (optional)  |
| last_name | Last name of the person for whom booking is created (optional) |
| phone_number | Phone number on which booking sms is to be send (required) |
| source | Source of booking. "APP", "WEB", "CALL" or "WALKIN" (optional). Default value is "WALKIN" |
| additional_info | Additional info about the person for whom booking is created (optional) |

### Response Example


```sh
HTTP/1.1 200 OK
Content-Type:application/json;charset=UTF-8
{
    "code": 0,
    "message": "success",
    "booking_details": {
        "booking_id": "903000000000099",
        "queue_id": "23213dasda212121",
        "token_number": "A010",
        "queue_position": 10,
        "wait_time": "24 mins (approx)",
        "status": "Queued",
        "updated_time": "2016-06-05T02:30:08-0700",
        "created_time": "2016-06-05T12:30:08-0700"
    },
}

```

| Response Fields | Description |
| ------ | ------ |
| booking_id | A unique booking id |
| queue_id | A unique queue id for which booking is made  |
| token_number | Token Number  |
| queue_position | Current position in queue |
| wait_time | Approx waiting time for the turn to come up  |
| status | "QUEUED", "NOSHOW", "CANCELLED" or "SERVED"  |
| created_time | Time when the location was created |
| updated_time | Time when the location was last updated |


### Create an appointment
Create an appointment.

### POST /appointments
### Request Example


```sh
$ curl https://app.hate2wait.io/api/v1/appointments
-H "Authorization: h2w-authtoken ba4604e8e433g9c892e360d53463oec5"
-H "Content-Type: application/json;charset=UTF-8"
-d '{
    "queue_id": "23213dasda212121",
    "first_name": "John",
    "last_name": "Doe",
    "phone_number": "9999999999",
    "source": "app",
    "appointment_time": "2016-06-05T02:30:08-0700",
    "additional_info": {
        "gender": "male",
        "dob": "13-05-1992",
        "notes": "",
        "latitude": "",
        "longitude": ""
    }
    
}
```

### Response Example


```sh
HTTP/1.1 200 OK
Content-Type:application/json;charset=UTF-8
{
    "code": 0,
    "message": "success",
    "appointment_details": {
        "appointment_id": "903000000000099",
        "queue_id": "23213dasda212121",
        "appointment_time": "2016-06-05T02:30:08-0700",
        "status": "APPOINTMENT",
        "updated_time": "2016-06-05T02:30:08-0700",
        "created_time": "2016-06-05T12:30:08-0700"
    },
    "booking_details": {}
}

```

| Parameter | Description |
| ------ | ------ |
| queue_id | The ID of the queue for which you want to create a booking (required) |
| first_name | First name of the person for whom booking is created (optional)  |
| last_name | Last name of the person for whom booking is created (optional) |
| phone_number | Phone number on which booking sms is to be send (required) |
| appointment_time | Appointment time (required)  |
| source | Source from which booking is created i.e App, Widget, Kiosk, IVR (required) |
| additional_info | Additional info about the person for whom booking is created (optional) |

### Cancel a queue booking
Cancel a queue booking.

### GET /queue_bookings/{booking_id}/cancel
### Request Example


```sh
$ curl https://app.hate2wait.io/api/v1/queue_bookings/{booking_id}/cancel
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
}

```

### Cancel an appointment
Cancel an appointment

### GET /appointments/{appointment_id}/cancel
### Request Example


```sh
$ curl https://app.hate2wait.io/api/v1/appointments/{appointment_id}/cancel
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
}

```

### Get live status of a queue booking
Get live status of a queue booking

### GET /queue_bookings/{booking_id}/status
### Request Example


```sh
$ curl https://app.hate2wait.io/api/v1/queue_bookings/{booking_id}/status
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
    "booking_details": {
        "booking_id": "903000000000099",
        "queue_id": "23213dasda212121",
        "token_number": "A010",
        "queue_position": 10,
        "wait_time": "24 mins (approx)",
        "status": "Queued",
        "updated_time": "2016-06-05T02:30:08-0700",
        "created_time": "2016-06-05T12:30:08-0700"
    },
}

```

### Get status of an appointment
Get status of an appointment

### GET /appointments/{appointment_id}/status
### Request Example


```sh
$ curl https://app.hate2wait.io/api/v1/appointments/{appointment_id}/status
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
    "appointment_details": {
        "appointment_id": "903000000000099",
        "queue_id": "23213dasda212121",
        "appointment_time": "2016-06-05T02:30:08-0700",
        "status": "QUEUED",
        "updated_time": "2016-06-05T02:30:08-0700",
        "created_time": "2016-06-05T12:30:08-0700"
    },
    "booking_details": {
        "booking_id": "9030012130000000099",
        "queue_id": "23213dasda212121",
        "token_number": "A010",
        "queue_position": 10,
        "wait_time": "24 mins (approx)",
        "status": "Queued",
        "updated_time": "2016-06-05T02:30:08-0700",
        "created_time": "2016-06-05T12:30:08-0700"    
    }
}

```

### Get current status of a queue
Get current status of a queue

### GET /queue/{queue_id}/status
### Request Example


```sh
$ curl https://app.hate2wait.io/api/v1/queue/{queue_id}/status
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
    "queue_details": {
        "people_in_queue": 10,
        "wait_time": "24 mins (approx)",
        "last_updated_at": "2016-06-05T02:30:08-0700"
    }
}

```

### Response Status Codes

All hate2wait APIs return a response in json format. The API returns one of the following HTTP status codes.

| Status Code | Description |
| ------ | ------ |
| 200 | Request has been executed |
| 201 | Resource created |
| 202 | Resource changed |
| 204 | Resource deleted |
| 400 | A parameter is missing or is invalid |
| 401 | Authentication failed |
| 404 | Resource cannot be found |
| 405 | HTTP method not allowed |
| 500 | Server error |


License
----

Wonder Peak Tech Pvt. Ltd.

