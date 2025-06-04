# PgBouncer Helm Chart

[![Artifact Hub](https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/pgbouncer-helm)](https://artifacthub.io/packages/helm/pgbouncer-helm)

This Helm chart deploys [PgBouncer](https://www.pgbouncer.org/) on Kubernetes. PgBouncer is a lightweight and high-performance connection pooler for PostgreSQL databases.

## Installation

```bash
helm repo add pgbouncer-helm https://enbiyagoral.github.io/pgbouncer-helm
helm repo update
helm install pgbouncer pgbouncer-helm/pgbouncer --namespace pgbouncer --create-namespace
```

## Configuration

The following table lists the configurable parameters of the PgBouncer chart and their default values:

| Parameter            | Description                        | Default              |
|----------------------|------------------------------------|----------------------|
| `replicaCount`       | Number of PgBouncer pods           | `1`                  |
| `image.repository`   | PgBouncer image repository         | `edoburu/pgbouncer`  |
| `image.tag`          | PgBouncer image tag                | `1.18.0`             |
| `service.port`       | PgBouncer service port             | `6432`               |
| `databases`          | Database connection settings       | See `values.yaml`    |
| `users`              | PgBouncer users                    | See `values.yaml`    |
| ...                  | ...                                | ...                  |

For all available configuration options, see the [values.yaml](./values.yaml) file.

## Usage Example

After installation, you can connect to PgBouncer using the following commands:

```bash
# Get the pod name
export POD_NAME=$(kubectl get pods --namespace pgbouncer -l "app.kubernetes.io/name=pgbouncer,app.kubernetes.io/instance=pgbouncer" -o jsonpath="{.items[0].metadata.name}")

# Connect using psql
kubectl exec -it $POD_NAME --namespace pgbouncer -- psql -h localhost -p 6432 -U <user> <database>
```

## Contributing

Contributions are welcome! Please open an issue or submit a pull request.

## License

This chart is licensed under the Apache License 2.0.