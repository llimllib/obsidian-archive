---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
to destroy a cluster and any services in it (this one had no tasks - further stuff may be necessary if there are tasks in it?)

```shell
for cluster in $(aws ecs list-clusters | jq -r .clusterArns[]); do
   aws ecs delete-service --force --cluster $cluster --service \
       $(aws ecs list-services --cluster $cluster | jq -r .serviceArns[]);
   aws ecs delete-cluster --cluster $cluster
done
```