# Cluster with local registry

## Create a cluster and registry

```bash
./kind-with-registry.sh
```

Please refer to the [Kind document](https://kind.sigs.k8s.io/docs/user/local-registry/) for details.

## Create a cluster and registry (+ registry UI)

```bash
mv docker-registry
mkdir -p registry/data
chmod 777 registry
chmod 777 registry/data

docker compose up -d
mv ..
./kind-with-existring-registry.sh registry-server
```

URL
- Registry Server: `localhost:5001`
- Registry UI: `localhost:8080`


## Using the registry

```bash
docker pull gcr.io/google-samples/hello-app:1.0
docker tag gcr.io/google-samples/hello-app:1.0 localhost:5001/hello-app:1.0
docker push localhost:5001/hello-app:1.0
kubectl create deployment hello-server --image=localhost:5001/hello-app:1.0
```