---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/mingrammer/diagrams

examples [here](https://diagrams.mingrammer.com/docs/getting-started/examples)

```
from diagrams import Diagram
from diagrams.aws.compute import EC2
from diagrams.aws.database import RDS
from diagrams.aws.network import ELB

with Diagram("Grouped Workers", show=False, direction="TB"):
    ELB("lb") >> [EC2("worker1"),
                  EC2("worker2"),
                  EC2("worker3"),
                  EC2("worker4"),
                  EC2("worker5")] >> RDS("events")
```