# occupancy-provider
This provider supplies all the occupancy information about relevant spaces in the organization. This also hs information about sites, buildings, floors and locations(spaces). This doesn't contain the location(space) capacity information. To get the capacity information you need a `space-provider` and a `space-mapping-provider`. Please refer the relevant providers for more information.
<br>
<br>

## Actions 
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
Example Response
```
{
    "floors": [
        {
            "id": "uX2S",
            "name": "",
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
Example Response
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
    ]
}
```

<br>

### GetAllSpaces
This action is similar to `GetSpaces` action. Only difference is this action doesn't have any inputs and it returns all the spaces/locations for all floor and buildings. 

response structure is the same as `GetSpaces`. It contains a field called `spaces` which contains an array of objects of space details described above in `GetSpaces` action


