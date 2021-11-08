# transportation-info-provider

This provider provides information about public transportation.
It takes a latitude and longitude as input and returns neary transport and execpted arrival times.

## Actions

### GetNearbyStops

This takes 2 inputs:

* latitude
* longitude

It returns 2 fields:

* status - This should be `"ok"`
* stops - An array of `stop` objects

Example:

```
{
    "status":"ok",
    "stops":[
        {
            "stop": "Swan Street Shopping Centre/Swan St #10 ",
            "route": "Waterfront City Docklands - Wattle Park",
            "departure": "2021-10-28T18:13:00Z"
        },
        {
            "stop": "East Richmond ",
            "route": "Glen Waverley",
            "departure": "2021-10-28T18:20:00Z"
        },
        {
            "stop": "East Richmond ",
            "route": "Glen Waverley",
            "departure": "2021-10-28T18:26:00Z"
        },
        {
            "stop": "Adelaide St/Church St #55 ",
            "route": "North Richmond - Balaclava via Prahran",
            "departure": "2021-10-28T18:29:00Z"
        }
    ]
}
```

### stop object
The stop object has 3 fields:

* `stop` - The name of the bus/train stop
* `route` - The bus route or train route name
* `departure` - The next expected departure time in ISO8601 format