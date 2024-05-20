---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/chrieke/prettymapp

> Prettymapp is a webapp and Python package to create beautiful maps from OpenStreetMap data

> Prettymapp is based on a rewrite of the fantastic [prettymaps](https://github.com/marceloprates/prettymaps) project by @marceloprates. All credit for the original idea, designs and implementation go to him. The prettymapp rewrite focuses on speed and adapted configuration to interface with the webapp. It drops more complex configuration options in favour of improved speed, reduced code complexity and simplified configuration interfaces. It is partially tested and adds a streamlit webapp component.

----

Following some slowness in generating maps using this tool for Portland, Maine, (prettymapp issue [here](https://github.com/chrieke/prettymapp/issues/26)) I discovered and reported [this issue](https://github.com/gboeing/osmnx/issues/1050) in osmnx.

The Gulf of Maine has a [very complicated](https://polygons.openstreetmap.fr/?id=13663366) representation in OpenStreetMap, and doing anything with osmnx (which prettymapp relies on) that intersects with that shape causes osmnx to go very slowly.