# iaq-provider 

This provider supplies all the IAQ information about relevant spaces in the organization, but this doesn't contains capacity information. To get the capacity information you need a `space-provider` and a `space-mapping-provider`. Please refer the relevant providers for more information.


# Configurations
Need to provide a master space mapping provider (space-mapping-provider). This provider will gives a mapping for the spaces. Configure this in model settings.


# Actions

### GetAllSpaces
This action returns the details of all the locations(spaces) <br>
This takes a no inputs.

This action returns a field called `spaces`, which contains an array of objects. Each object contains the followings,

- `id` - The id of the space/location 
- `name` - The name of the space/location 
- `masterName` - The respective name from the `space-provider`. 
- `capacity` - The capacity of the space


<br>
Example Response:

```
{
    "spaces": [
        {
            "id" : "xyc",
            "name" "Room 01",
            "masterName": "Room 01",
            "capacity" : 10
        },
        ...
    ]
}
```

<br>

### GetAllLocations
This actions returns a list of all locations available. This will be used by `space-mapping-provider` when you add a new source. Please refer `space-mapping-provider` for more details.

This takes no inputs and returns field called `locations`, which contains an array of `{id, name}` objects. 

- `id` - The id of the location 
- `name` - name of the location. This will be used to map with the master space provider (`space-provider`).

Example Response: 

```
{
    "locations": [
        {
            "id" : "xyz",
            "name" : "Room_01"
        },
        ...
    ]
}
```
<br>


### GetLatestValues
This action returns the current IAQ details for all spaces.
This action takes no inputs.

This returns a field named `values`, which contains an array of objects. Each object contains the following. 

- `space` - name of the space 
- `temp` - current temperature 
- `co2` - current co2 level 
- `rh` - current humidity 
- `aqi` - current air quality index

<br>

Example Response 

```
{
    "values": [
        {
            "space": "Meeting Room 2",
            "temp": "20.7",
            "co2": "606.0",
            "rh": "69.0",
            "aqi": "65.0" 
        },
        ...
    ]
}
```

<br>


### Trends 
This action returns the IAQ trends for a given space. It takes five (5) inputs. 
- `sensor` - this take one of the followings `co2, temp, rh`
- `room` - name of the room 
- `start` - start date to get data (ISO format)
- `end` - end date to get data (ISO format)
- `bucket` - this takes one of the followings `hour, day, week, month`

<br>

This returns a field names `values`, which contains an array of objects. Each object contains the followings.

- `Time` - datetime 
- `Value` - occupancy (string)
  
<br>

Example Response: 

```
[
    {
        "Time":"2021-10-19T00:00:00Z",
        "Value":"25"
    },
    ...
]
```

<br>

## Note 
This model must have other actions to get the spaces and retrieve/receive IAQ data and store them locally in iviva/lucy. These can be construct in any manner as long as they provide the necessary data/information described above in details. 