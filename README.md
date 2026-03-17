# kubernetes-n8n

## Create PostgreSQL secret
```
kubectl create secret generic postgres-secret --from-literal=POSTGRES_NON_ROOT_USER=n8n --from-literal=POSTGRES_NON_ROOT_PASSWORD=<PASSWORD> -n n8n
```

## Requirements
To deploy n8n is required to have a PostgreSQL instance running. Follow (kubernetes-postgres)[https://github.com/hfolguera/kubernetes-postgres] repository to deploy it.

Once PostgreSQL instance is up&running, create a dedicated database with the following code as ADMIN user:
```
CREATE USER n8n WITH PASSWORD <password>;
CREATE DATABASE n8n OWNER=n8n;
GRANT ALL PRIVILEGES ON n8n TO n8n;
```

## SSO Federation
n8n deployment has been modified to support SSO federation without Enterprise Plan. Refer to (https://github.com/cweagans/n8n-oidc)

If SSO federation stops working, try to login through `https://your-n8n-domain.com/signin?showLogin=true`


## Deploy n8n instance
```
kubectl apply -f n8n-namespace.yaml
kubectl apply -f n8n-pvc.yaml
kubectl apply -f n8n-configmap.yaml

kubectl create secret generic n8n-authentik-secret -n n8n --from-literal=OIDC_CLIENT_ID=<ClientID> --from-literal=OIDC_CLIENT_SECRET=<ClientSecret>

kubectl apply -f n8n-deployment.yaml
kubectl apply -f n8n-service.yaml
```