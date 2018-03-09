# hate2wait API Documentation

[![N|Solid](https://business.hatetowaitapp.com/assets/logo.png)](https://nodesource.com/products/nsolid)


# Quick Reference
----
The hate2wait API endpoint is https://app.hate2wait.io/api/v1 and all paths below are relative to that. hate2wait uses HTTP Basic Auth for authentication and all calls must be over HTTPS.

| Authentication | Description |
| ------ | ------ |
| h2w-authtoken | A unique auth token provided to the user to make API calls. |

# Getting your Auth Token
----
The hate2wait API is tied to your hate2wait Business account. You will receive your auth token on your email post registering it onto hate2wait for Business portal.

# REST API
----
### 1. List All Locations
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
    "message": "success",
    "locations": [
        {
            "location_id": "903000000000099",
            "location_name": "ABC Business",
            "location_address": "ABC, GD Square",
            "location_code": "ABCD",
            "location_latitude": 26.919236,
            "location_longitude": 80.949191,
            "location_phone": "12124121213",
            "manager_name": "ABC",
            "manager_email": "xyz@example.com",
            "created_on": "2016-06-05T12:30:08-0700"
        },
        {...},
        {...}
    ]
}

```
| Response Fields | Description |
| ------ | ------ |
| location_id | A unique location id |
| location_name | Name of the location  |
| location_address | Complete address of the location |
| location_code | Code of the location if set any during creation |
| location_phone | Phone number of the location |
| location_latitude | Latitude of the location |
| location_longitude | Longitude of the location |
| manager_name | Name of the location manager |
| manager_email | Email of the location manager |
| created_on | Time when the location was created |

-----------------------------------------------------------------------------

### 2. List of all the queues of a location
List of all the queues created for a particular location.

### GET /{location_id}/queues
### Request Example


```sh
$ curl https://app.hate2wait.io/api/v1/locations/{location_id}/queues
-H "Authorization: h2w-authtoken ba4604e8e433g9c892e360d53463oec5"
-H "Content-Type: application/json;charset=UTF-8"
```

| Request Parameters | Description |
| ------ | ------ |
| location_id | A unique location id |

### Response Example


```sh
HTTP/1.1 200 OK
Content-Type:application/json;charset=UTF-8
{
    "message": "success",
    "queues": [
        {
            "queue_id": "903000000000099",
            "queue_name": "Service Queue",
            "queue_opening_hours": [
                {
                    "weekday": "Monday",
                    "queue_starting_time": "10:30 AM",
                    "queue_closing_time": "7:00 PM"
                },
                {...},
                {...}
            ],
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
| queue_opening_hours | Weekly queue schedule   |

-----------------------------------------------------------------------------

### 3. Create a queue booking
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
| source | Source of booking. "APP", "WEB", "CALL" or "WALKIN" (optional). Default value is "APP" |
| additional_info | Additional info about the person for whom booking is created (optional) |

### Response Example


```sh
HTTP/1.1 200 OK
Content-Type:application/json;charset=UTF-8
{
    "message": "success",
    "booking_id": "903000000000099"
}

```

| Response Fields | Description |
| ------ | ------ |
| booking_id | A unique booking id |

-----------------------------------------------------------------------------

### 4. Create an appointment
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

| Request Parameters | Description |
| ------ | ------ |
| queue_id | The ID of the queue for which you want to create a booking (required) |
| first_name | First name of the person for whom booking is created (optional)  |
| last_name | Last name of the person for whom booking is created (optional) |
| phone_number | Phone number on which booking sms is to be send (required) |
| appointment_time | Appointment time (required)  |
| source | Source of booking. "APP", "WEB", "CALL" or "WALKIN" (optional). Default value is "WALKIN" |
| additional_info | Additional info about the person for whom booking is created (optional) |

### Response Example


```sh
HTTP/1.1 200 OK
Content-Type:application/json;charset=UTF-8
{
    "message": "success",
    "appointment_id": "903000000000099"
}

```

| Response Fields | Description |
| ------ | ------ |
| appointment_id | A unique appointment id |

-----------------------------------------------------------------------------

### 5. Cancel a queue booking
Cancel a queue booking.

### GET /queue_bookings/{booking_id}/cancel
### Request Example


```sh
$ curl https://app.hate2wait.io/api/v1/queue_bookings/{booking_id}/cancel
-H "Authorization: h2w-authtoken ba4604e8e433g9c892e360d53463oec5"
-H "Content-Type: application/json;charset=UTF-8"
```

| Request Parameters | Description |
| ------ | ------ |
| booking_id | A unique queue booking id |

### Response Example


```sh
HTTP/1.1 200 OK
Content-Type:application/json;charset=UTF-8
{
    "message": "success",
}

```

-----------------------------------------------------------------------------

### 6. Cancel an appointment
Cancel an appointment

### GET /appointments/{appointment_id}/cancel
### Request Example


```sh
$ curl https://app.hate2wait.io/api/v1/appointments/{appointment_id}/cancel
-H "Authorization: h2w-authtoken ba4604e8e433g9c892e360d53463oec5"
-H "Content-Type: application/json;charset=UTF-8"
```

| Request Parameters | Description |
| ------ | ------ |
| appointment_id | A unique appointment id |

### Response Example


```sh
HTTP/1.1 200 OK
Content-Type:application/json;charset=UTF-8
{
    "message": "success",
}

```

-----------------------------------------------------------------------------

### 7. Get current status of a queue booking
Get live status of a queue booking

### GET /queue_bookings/{booking_id}/status
### Request Example


```sh
$ curl https://app.hate2wait.io/api/v1/queue_bookings/{booking_id}/status
-H "Authorization: h2w-authtoken ba4604e8e433g9c892e360d53463oec5"
-H "Content-Type: application/json;charset=UTF-8"
```

| Request Parameters | Description |
| ------ | ------ |
| booking_id | A unique queue booking id |

### Response Example


```sh
HTTP/1.1 200 OK
Content-Type:application/json;charset=UTF-8
{
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
| created_time | Time when the booking was created |
| updated_time | Time when the booking was last updated |

-----------------------------------------------------------------------------

### 8. Get status of an appointment
Get status of an appointment

### GET /appointments/{appointment_id}/status
### Request Example


```sh
$ curl https://app.hate2wait.io/api/v1/appointments/{appointment_id}/status
-H "Authorization: h2w-authtoken ba4604e8e433g9c892e360d53463oec5"
-H "Content-Type: application/json;charset=UTF-8"
```

| Request Parameters | Description |
| ------ | ------ |
| appointment_id | A unique appointment id |

### Response Example


```sh
HTTP/1.1 200 OK
Content-Type:application/json;charset=UTF-8
{
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

| Response Fields | Description |
| ------ | ------ |
| appointment_id | A unique appointment id |
| queue_id | A unique queue id for which appointment is made  |
| status | "APPOINTMENT", "NOSHOW", "CANCELLED" or "QUEUED"  |
| created_time | Time when the appointment was created |
| updated_time | Time when the appointment was last updated |
| booking_details | Once an appointment is moved into the queue, booking details will contain all the details of a queue bookings |

-----------------------------------------------------------------------------

### 9. Get current status of a queue
Get current status of a queue

### GET /queue/{queue_id}/status
### Request Example


```sh
$ curl https://app.hate2wait.io/api/v1/queue/{queue_id}/status
-H "Authorization: h2w-authtoken ba4604e8e433g9c892e360d53463oec5"
-H "Content-Type: application/json;charset=UTF-8"
```

| Request Parameters | Description |
| ------ | ------ |
| queue_id | A unique queue id |

### Response Example


```sh
HTTP/1.1 200 OK
Content-Type:application/json;charset=UTF-8
{
    "message": "success",
    "queue_details": {
        "queue_id": "37892139127391",
        "people_in_queue": 10,
        "wait_time": "24 mins (approx)",
        "last_updated_at": "2016-06-05T02:30:08-0700"
    }
}

```

| Response Fields | Description |
| ------ | ------ |
| queue_id | A unique queue id for which appointment is made  |
| people_in_queue | Total no of people in the queue currently  |
| wait_time | Approx waiting time for a turn to come up of a booking if created now|
| last_updated_at | Time when the queue was last updated i.e someone got checked out, waiting time is reduced, some booking is made, etc |


# Response Status Codes
----
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

# Usage Limits
----
1. hate2wait API supports upto 100,000 requests daily.
2. And not more than 1000 requests per second.

If your API usage reaches your limit on any given day, your application will not be able to access the API for the remainder of that day.

# FAQ
----

Have questions? Need help? Email us at support@hate2wait.io and we'll add them to our list here.



License
----

Wonder Peak Tech Pvt. Ltd.

