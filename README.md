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


License
----

Wonder Peak Tech Pvt. Ltd.

