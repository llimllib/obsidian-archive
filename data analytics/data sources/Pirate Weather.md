---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://pirateweather.net

> Weather forecasts are primarily determined using models run by government agencies, but the outputs aren't easy to use or in [formats](https://weather.gc.ca/grib/what_is_GRIB_e.html) built for applications. To try to address this, I've put together a service (built on AWS Lambda) that reads public weather forecasts and serves it following the Dark Sky API style. It is **not** a reverse engineering of the API, since their implementation relies on radar forecasts for minutely results, as well as a few additional features. The API aims to return data using the same json structure as what Dark Sky uses, available here: [https://web.archive.org/web/20200723173936/https://darksky.net/dev/docs](https://web.archive.org/web/20200723173936/https://darksky.net/dev/docs). Feel free to register, subscribe to this API (navigate to [APIs](https://pirateweather.net/apis) and **click subscribe**!), and let me know how it works at [api@alexanderrey.ca](https://pirateweather.net/mailto:api@alexanderrey.ca). To help support this project (my student AWS credits run out in June!), I've set up a [donation link](https://www.buymeacoffee.com/pirateweather). There's also an option for a monthly donations, which both supports this project and raises monthly API limit!

Open source, donation-ware weather API!

Used by [[Merry Sky]]