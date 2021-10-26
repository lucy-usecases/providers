# occupancy-provider
This provider supplies all the occupancy information about relevant spaces in the organization. This also has information about sites, buildings, floors and locations(spaces). This doesn't contain the location(space) capacity information. To get the capacity information you need a `space-provider` and a `space-mapping-provider`. Please refer the relevant providers for more information.
<br>

## Configurations 
Need to provide a master space mapping provider (`space-mapping-provider`). This provider will gives a mapping for the spaces. Configure this in model settings. 

## Actions 
<br>

### GetFloors
This action returns the details of the floors of a particular building. 

This action takes a single input `building`, which is the id of the building. If the building id is not given, action will find the firs building it can and, returns the details of the floors for that building. 

This action will returns a field called `floors`, which contains an array of objects.
Each object contains the followings.

- `id` - The id of the floor 
- `name` - The name of the floor 
- `layout` - The the layout of the floor. This is again an object, which contains the followings 
  * `floorPlan` - The url for the floor plan (image). this(image) should be publicly accessible. 
  * `width` - The width of the floor 
  * `height` - The height of the floor 

<br>
Example Response:

```
{
    "floors": [
        {
            "id": "uX2S",
            "name": "Flor 01",
            "layout": {
                "floorPlan": "https://abc.com/abc/1.jpg",
                "width": 50.5,
                "height": 97.2
            }
        },
        ...
    ]
}
```
<br>
<br>

### GetSpaces 
This action returns the details of the locations(spaces) in a given floor. <br>
This takes a single input `floor`, which is the id of the floor. 

This action returns a field called `spaces`, which contains an array of objects. Each object contains the followings,

- `id` - The id of the space/location 
- `name` - The name of the space/location 
- `masterName` - The respective name from the `space-provider`. 
- `capacity` - The capacity of the space
- `coordinates` - The coordinates of the space. This is an array of objects of x, y coordinates. 
   * `x` - x coordinate 
   * `y` - y coordinate

<br>
Example Response:

```
{
    "spaces": [
        {
            "id" : "xyc",
            "name" "Room_01",
            "masterName": "Room 01",
            "capacity" : 10,
            "coordinates": [
                {
                    "x": 37.1,
                    "y": 43.51
                },
                {
                    "x": 42.61,
                    "y": 42.54
                },
                {
                    "x": 44.5,
                    "y": 53.27
                },
                {
                    "x": 38.99,
                    "y": 54.24
                }
            ]

        },
        ...
    ]
}
```

<br>

### GetAllSpaces
This action is similar to `GetSpaces` action. Only difference is this action doesn't have any inputs and it returns all the spaces/locations for all floor and buildings. 

response structure is the same as `GetSpaces`. It contains a field called `spaces` which contains an array of objects of space details described above in `GetSpaces` action.
<br>
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

### GetCurrentOccupancyForFloor
This action returns the current occupancy details for a given floor. 

This action takes single input, `floor`, which is the id of the floor. It returns a filed `occupancy`, which contains an array of objects. Each object contains the followings. 

- `id` - location id 
- `value` - occupancy count 

Example Response:

```
{
    "occupancy": [
        {
            "id" : "xyz",
            "value": 5
        },
        ...
    ]
}
```
<br>

### GetHistoricalOccupancyForFloor
This action returns the historical occupancy details for a given floor. 

This action takes four(4) inputs. <br> 
- `floor` - id of the floor 
- `start` - start datetime to get occupancy
- `end` - end datetime to get occupancy 
- `bucket` - this takes one of the following values `hour, day, week, month`

<br>

It returns a filed `occupancy`, which contains an array of objects. Each object contains the followings. 

- `id` - location id 
- `value` - occupancy count 
  
<br>

Example Response:

```
{
    "occupancy": [
        {
            "id" : "xyz",
            "value": 5
        },
        ...
    ]
}
```

<br>

### Trend
This action returns the occupancy trend for a given room. 

This takes four(4) inputs.
- `Room` - name of the room 
- `start` - start datetime to get the occupancy 
- `end` - end datetime to get the occupancy
- `bucket` - takes one of the following values `hour, day, week, month`

This returns an array of objects. Each object contains the followings.

- `Time` - datetime 
- `Value` - occupancy (string)
  
<br>

Example Response: 

```
[
    {
        "Time":"2021-10-19T00:00:00Z",
        "Value":"0"
    },
    ...
]
```

<br>

### TrendByMasterName
This is similar to the `Trend` action described above. Only difference here is this take the name as master space provider (`space-provider`). 

This will/can be used to get the trends in a application (model action), which doesn't know the `occupancy-provider`. 

Example: A composed chart(meeting room analytics) , which shows IQA data and occupancy data.

This returns the same output as `Trend` action above.

<br>

## Note 
This model must have other actions to subscribe/unsubscribe, sync site, building, floor and location details and retrieve/receive occupancy data and store them locally in iviva/lucy. These can be construct in any manner as long as they provide the necessary data/information described above in details. 