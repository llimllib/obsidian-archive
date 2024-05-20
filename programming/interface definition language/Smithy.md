---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://awslabs.github.io/smithy/quickstart.html

```smithy
namespace example.weather

service Weather {
    version: "2006-03-01",
    resources: [City],
    operations: [GetCurrentTime]
}

resource City {
    identifiers: { cityId: CityId },
    read: GetCity,
    list: ListCities,
    resources: [Forecast],
}
```

I'd looked at it before but I think it was only available in Java. Now it has a golang library:

https://github.com/aws/smithy-go

(Although that library is half Java too...)

If it has docs, I don't know where to find them