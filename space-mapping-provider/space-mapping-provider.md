# space-mapping-provider
This provider supplies information about location/space mappings between different systems/sources (example: `cognipoint, condeco, officeRND, etc`).

## Configurations 
Need to provide a master space provider (`space-provider`). This provider will have capacity information of the spaces. Configure this in model settings. 

<br>

## Actions 

### LoadMasterData
This action is used to load the master data from master space provider configure above. 
Master space provider(or any `space-provider` must have) must have a `GetAllLocations`   action which returns a  field `locations`, which contains an array of objects. Each object will have the followings. 

- `id` - id of the space 
- `name` - name of the space
- `source` - source of the data (Ex: condeco) 
- `capacity` - capacity of the space

This action(`LoadMasterData`) will get the data from master source and store them in a collection in lucy. 

<br> 

### AddASource
This action will add another source of data to the collection (sources), and it will get the locations from the given `space-provider`(model) and map them to the master source using the space/location name. This mapping happens automatically based on the name, this may not be an exact match depending how the name is constructed. Therefore a user must manually verify the mapping. For adding a source and verification we don't have a proper UI yet. But you can use model designer to to add a source and collection editor, which is available in the model designer to verify and update these. Proper UIs will be provided as soon as possible. 

This action takes two(2) inputs. 
- `id` - this is the source id (Ex: cognipoint, condeco - these will be pre defined and provided with the UI)
- `model` - name of the provider (model) 


Name mapping (automatic) will be as follows: <br>
Assume, 
- master source has a location named `Room 01` and - on all the UIs/widget master name should be displayed 
- another source (ex: cognipoint) has a location named `room_01` and id is `xyz`
  
when mapping, it will remove all the none alphanumerics and convert it to lowercase. So the names will math each other. If the alphanumerics in the names are different you will have to manually map them. 

if the names match it adds another field to the collection `<source id>: <location id from the source>`. 

Example: `cognipoint: 'xyz'`

if the names does not match id will be null 

Example: `cognipoint: null`

<br>

### GetMappingSpaces
This action returns all the rooms that mach for a given system and array of ids. 

This action takes two(2) inputs 
- `system` - system/source name (Ex: cognipoint, condeco)
- `ids` - ids(of the system above)  for the locations 

This returns a field `spaces`, which contains an array of objects. Each object contains the followings. 

- `id` - id of the location (from master source)
- `name` - id of the location (from master source)
- `capacity` - id of the location (from master source)
- `source` - id of the location (from master source)
- `<system/source id>` - source id with id from source 

Example Response: 

```
{
    "spaces": [
        {
            "id": 93,
            "name": "Boardroom",
            "capacity": 1,
            "source": "Condeco",
            "cognipoint": "OTdsgNhPQvGP265Kd8YSoA",
        },
        ...
    ]
}

```

<br>

### LookUpByMasterName
This action returns the `id` for a given source and a name(from master source).
 
This action takes two(2) inputs.
- `name` - space name from the master source 
- `source` - source/system, which you want to get the id for 

This returns the id of the mapping source. 






