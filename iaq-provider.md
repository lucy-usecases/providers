# iaq-provider

This provider supplies IAQ data on demand.

## Actions

### GetIAQData
This action returns the current (ie, latest) IAQ sensor readings for all locations. The IAQ parameters it returns are temperature, humidity and co2.
If the sensor does not supply any of those metrics it can return `null`.

This action will be called periodically to gather data.

The action should return data reasonably quickly. It's assumed that the latest values are already stored and ready to send.

This action takes no inputs and returns a field called `values` which contains an array of `{name,temp,rh,co2}` objects.

The fields in each object are:
* `name` - The location for which IAQ data is returned. This would often be some internal location id.
* `temp` - The temperature in degrees celcius
* `rh` - The humidity as a percentage (ie, 66.5 implies '66.5%')
* `co2` - The CO2 levels expressed as parts per million


Example Response:
```
{
    "values":[
        {"name":"Room 1","temp":24.2,"rh":67,"co2":500},
        {"name":"Room 2","temp":24.2,"rh":67,"co2":500}
    ]
}
```



