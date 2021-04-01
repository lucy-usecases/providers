# space-provider
This provider supplies information about all relevant spaces in the organization.

## Actions

### GetSpaces
This action returns all the available spaces and information related to them. This will be called on-demand as and when required.

The result should have a field called `spaces` which contains an array of `{id,name,capacity}` objects.

The fields in each object are:
* `id` - The internal unique id of the space - this would typically be matched against space ids coming from other models
* `name` - A friendly name for the space
* `capacity` - the seating capacity of the space - in the case of a cubicle it could be just `1`. Return `null` if this information is not avaialble or relevant


Example Response:
```
{
    "spaces":[
        {"name":"Room 1","id":"room-a123","capacity":10},
        {"name":"Conference Room","id":"room-a224","capacity":50}

    ]
}
```