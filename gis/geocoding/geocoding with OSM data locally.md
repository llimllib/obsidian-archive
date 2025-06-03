It was easier than I expected to get OSM geocoding running using [nominatim](https://nominatim.org) locally.

In my case, I only wanted to geocode addresses for my [Portland reassessment map](https://billmill.org/reassess2025/), so I only needed to geocode in Maine. I ran:

```sh
# Get Maine extract (83mb)
# ref: https://download.geofabrik.de/north-america/us/
wget https://download.geofabrik.de/north-america/us/maine-latest.osm.pbf

# Run nominatim on port 8080
# ref: https://github.com/mediagis/nominatim-docker/tree/master/5.1
docker run -it \
  -e PBF_PATH=/data/maine-latest.osm.pbf \
  -p 8080:8080 \
  -v .:/data \
  mediagis/nominatim:5.1
```

After a couple of minutes of processing, that got me a running nominatim. This curl command:

```sh
$ curl --silent --get \
  --data-urlencode "q=255 congress st, Portland, ME" \
  "http://localhost:8080/search" | jq
```

returns:

```json
[
  {
    "place_id": 334475,
    "licence": "Data © OpenStreetMap contributors, ODbL 1.0. http://osm.org/copyright",
    "osm_type": "node",
    "osm_id": 7171974026,
    "lat": "43.6625513",
    "lon": "-70.2521734",
    "category": "amenity",
    "type": "cafe",
    "place_rank": 30,
    "importance": 0.00000999999999995449,
    "addresstype": "amenity",
    "name": "LB Kitchen",
    "display_name": "LB Kitchen, 255, Congress Street, India Street, Portland, Cumberland County, Maine, 04101, United States",
    "boundingbox": [
      "43.6625013",
      "43.6626013",
      "-70.2522234",
      "-70.2521234"
    ]
  }
]
```
