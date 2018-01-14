# Redis on k8s

This work uses Kubernetes deployments, while the official example still uses Replication Controllers: https://github.com/kubernetes/examples/blob/master/staging/storage/redis/README.md

I tested this deployment on K8s v1.8.3 with the Openstack cloud provider.

The Redis Master mounts a Cinder Volume to make the Redis Data persistent.

I expose with a clusterIP the Redis master the Redis slaves and the Redis sentinels.

When running Docker containers for the client applications that will use redis, you can use in their `entrypoint.sh` scripts the following env vars:

```
${REDIS_MASTER_SERVICE_HOST}
${REDIS_SLAVES_SERVICE_HOST}
${REDIS_SENTINEL_SERVICE_HOST}```

Remember that you can connect to the master for Read/Write data, but if you connect to the slaves those are Read-Only.

If you have a modern client that connects to the sentinel, then you will benefit from the HA features of the cluster. If the master stops working the sentinels will elect a new master and your client will be able to discover it.
Look at this example: https://github.com/KabbageInc/django-redis-sentinel/

The slaves are not mounting persistent storage, so even if one slave is elected to master you will have to manually fix the situation.
