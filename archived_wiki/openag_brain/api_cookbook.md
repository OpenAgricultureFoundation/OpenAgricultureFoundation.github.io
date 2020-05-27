---
layout: wiki_archive
---

Useful API formulas. Want general API docs? See
[0.0.1](../openag_brain/api/0.0.1.md).

## curl

An easy way to test the API is to use the [curl](https://curl.haxx.se/)
command line utility.

For example, you could POST a desired `light_illuminance` to
`environment_1` like this:

``` 
curl -X POST -H "Content-Type:application/json" http://<IP ADDRESS>:5984/_openag/api/<VER>/topic/environment_1/desired/light_illuminance --data "[1.0]"

```

...replacing `<IP_ADDRESS>` with the IP of your Food Computer, and
`<VER>` with the API version.

## CSV Exports

Get all measured environmental variables for environment\_1 as a CSV
file:

``` 
GET http://<IP_ADDRESS>:5984/environmental_data_point/_design/openag/_list/csv/by_variable?group_level=4&startkey=["environment_1", "measured"]&endkey=["environment_1", "measured", {}]

```

Get all measured air\_carbon\_dioxide for environment\_1 as a CSV file:

    GET http://<IP_ADDRESS>:5984/environmental_data_point/_design/openag/_list/csv/by_variable?group_level=4&startkey=["environment_1", "measured", "air_carbon_dioxide"]&endkey=["environment_1", "measured", "air_carbon_dioxide", {}]
