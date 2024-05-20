---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://devseed.com/titiler/

> `Titiler`, pronounced **tee-tiler** (_ti_ is the diminutive version of the french _petit_ which means small), is a set of python modules that focus on creating FastAPI application for dynamic tiling.

> ... `TiTiler` has been developed so users can build their own app using only the portions they need. Using [TilerFactories](https://devseed.com/titiler/advanced/tiler_factories/), users can create a fully customized application with only the endpoints needed.

## Dynamic tiling

> TiTiler's first goal is to create a lightweight but performant dynamic tile server... but what do we mean by this?
> 
> The goal of the `Dynamic Tiling` process is to get rid of all the pre-processing steps, by creating a tile server which can access the raw data (COG) and apply operations (rescaling, reprojection, image encoding) to create the visual tiles **on the fly**.

-   Open the file and get internal metadata (stored in the header of the file)
-   Read internal parts needed to construct the output tile
-   Apply data rescaling (if needed)
-   Apply colormap (if needed)
-   Encode the data into a visual image format (JPEG, PNG, WEBP)

> With `Static` tile generation you are often limited because you are visualizing data that is fixed and stored somewhere on a disk. With `Dynamic tiling`, the user has the possibility to apply their own choice of processing (e.g rescaling, masking) before creating the `image`.