# Order Microservice Helm Chart

This Helm chart deploys the Order Microservice application on a Kubernetes cluster.

## Prerequisites

- Kubernetes 1.16+
- Helm 3.0+
- Access to Docker registry containing order-microservice image

## Getting Started

### Add Repository
```bash
# Add Helm repository (if hosted)
helm repo add myrepo <repository-url>
helm repo update
```

### Installing the Chart
```bash
# Install with release name 'order-microservice'
helm install order-microservice . -f values.yaml
```

## Configuration

The following table lists the configurable parameters of the order-microservice chart and their default values.

| Parameter | Description | Default |
|-----------|-------------|---------|
| `replicaCount` | Number of replicas | `2` |
| `image.repository` | Image repository | `classpathio/order-microservice` |
| `image.tag` | Image tag | `3.0.0` |
| `image.pullPolicy` | Image pull policy | `IfNotPresent` |
| `service.type` | Kubernetes Service type | `ClusterIP` |
| `service.port` | Service port | `80` |
| `service.targetPort` | Container port | `8222` |
| `spring.profile` | Spring active profile | `dev` |
| `spring.datasource.username` | Database username | `sa` |
| `spring.datasource.password` | Database password | `welcome` |

## Custom Values

Create a YAML file (e.g., `custom-values.yaml`) to override default values:

```yaml
replicaCount: 3
image:
  tag: "3.1.0"
spring:
  profile: qa
```

Install with custom values:
```bash
helm install order-microservice . -f custom-values.yaml
```

## Uninstalling the Chart
```bash
helm uninstall order-microservice
```

## Examples

### Deploy with High Availability
```yaml
replicaCount: 3
resources:
  requests:
    cpu: 500m
    memory: 512Mi
  limits:
    cpu: 1000m
    memory: 1024Mi
```

### Deploy with Custom Configuration
```yaml
configMap:
  dev:
    orderCount: 20
    serverPort: 8333
```

## Upgrading

To upgrade the release:
```bash
helm upgrade order-microservice . -f values.yaml
```

## Development

### Requirements
- Docker
- Kubernetes cluster (minikube, kind, or cloud provider)
- Helm

### Local Development
1. Clone repository:
```bash
git clone <repository-url>
cd order-microservice-chart
```

2. Make changes and test:
```bash
helm lint .
helm template .
```

3. Test installation:
```bash
helm install test-release . --dry-run
```

## Troubleshooting

### Common Issues

1. Pod not starting:
```bash
kubectl describe pod <pod-name>
```

2. Configuration issues:
```bash
kubectl get configmap
kubectl describe configmap <configmap-name>
```

3. Service issues:
```bash
kubectl get svc
kubectl describe svc <service-name>
```
