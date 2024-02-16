# TODO


## Issues

### Postgres pod in CrashLoopBackOff state
Check the logs of the pod:
```
kubectl logs pod/postgres-5fc87f568b-qb7dh -n n8n
```

The issue is related to storage configuration:
```
chown: changing ownership of '/var/lib/postgresql/data/pgdata': Operation not permitted
```

Connect to your storage server (Synology in my case) and modify the folder permissions:
```

```
