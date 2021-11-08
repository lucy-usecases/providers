# service-request-provider
This provider will provide all the details about service requests. 

<br>

## Actions 
<br>

### CreateRequest
This action will create a new service request. 

This will take two(2) inputs. <br>

- `title` - title of the request 
- `description` - description of the request 


Example Request: 

```
{
    "title":"Requesting service letter",
    "description":"This is to request a service letter ",
}
```

<br>


### GetRequests 
This action will return a list of service requests. It takes three (3) inputs <br>

- `max` - max number of items to return
- `last` - last returned item count 
- `args` - filters. this is an object which contains two items 
  - `status` - status of the request to filter. to get all pass `all`
  - `query` - any query 
  
<br>

It returns a filed `requests`, which contains an array of objects. Each object contains the followings. 

- `_id` - id of the request  
- `title` - title of the request 
- `description` - description of the request  
- `requestedUserKey` - requested user key 
- `requestedUserName` - requested user name
- `requestedAt` - requested data time (in ISO format)
- `status` - request status 
- `processedUserKey` - user key of the person processed the request
- `processedUserName` -  user name of the person processed the request
- `processedAt` - processed date time (in ISO format)
- `referenceNumber` - reference number for the request
- `notes` - any notes. this is a simple list(array) of strings

<br> 

Example Response: 

```
{
    "requests": [
        {
            "_id": "617b9c7ecf90e81e3c6a9f22",
            "title": "Requesting service letter",
            "description": "This is to request a service letter ",
            "requestedUserKey": "1",
            "requestedAt": "2021-10-29T07:02:22.178Z",
            "status": "pending",
            "processedUserKey": "",
            "processedAt": "",
            "notes": [],
            "requestedUserName": "Jane Doe",
            "processedUserName": "",
            "referenceNumber": "sr-2021-10-29-414952"
        },
    ]
}
```

<br>


### GetRequestDetails 
This will return all the details of a given request. This takes a single input `id`, id of the service request. 

This will return a field named `request`, which contains the followings. 

- `_id` - id of the request  
- `title` - title of the request 
- `description` - description of the request  
- `requestedUserKey` - requested user key 
- `requestedUserName` - requested user name
- `requestedAt` - requested data time (in ISO format)
- `status` - request status 
- `processedUserKey` - user key of the person processed the request
- `processedUserName` -  user name of the person processed the request
- `processedAt` - processed date time (in ISO format)
- `referenceNumber` - reference number for the request
- `notes` - any notes. this is a simple list(array) of strings

<br> 

Example Response 

```
{
    "request": {
        "_id": "617b9c7ecf90e81e3c6a9f22",
        "title": "Request 02",
        "description": "Description 02",
        "requestedUserKey": "1",
        "requestedAt": "2021-10-29T07:02:22.178Z",
        "status": "pending",
        "processedUserKey": "",
        "processedAt": "",
        "notes": [],
        "requestedUserName": "Administrator ",
        "processedUserName": "",
        "referenceNumber": "sr-2021-10-29-414952"
    }
}
```

<br>

### UpdateRequestStatus
This action will update the status of a given request. It takes two (2) inputs. <br>

- `id` - id of the request 
- `status` - status to update the request to 


Example Request: 

```
{
    "id": "617b9c7ecf90e81e3c6a9f22",
    "status": "on-going",
}
```


### UpdateRequest 
This action will update the details of a give request . This takes two (2) inputs. <br>

- `id` - id of the request 
- `data` - fields and values to update 

Example Request: 

```
{
    "id": "617b9c7ecf90e81e3c6a9f22",
    "data": "{"notes": ["This will be delayed due to the unavoidable situation in country "]}",
}
```
