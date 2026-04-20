## Container Documentation for Opentelemetry-Collector-Contrib Documentation

The CleanStart Opentelemetry-Collector-Contrib image provides a production-ready, security-hardened container optimized for enterprise environments. Built on a minimal base OS with comprehensive security hardening, this image delivers reliable application execution with advanced security features.

📌 **Base Foundation**: Production-ready container from cleanstart.

**Image Path**: `ghcr.io/cleanstart-containers/opentelemetry-collector-contrib`

**Registry**: cleanstart Registry

## Pull Latest Image
Download the container image from the registry

```bash
docker pull ghcr.io/cleanstart-containers/opentelemetry-collector-contrib:latest
```
```bash
docker pull ghcr.io/cleanstart-containers/opentelemetry-collector-contrib:latest-dev
```

## Basic config file
Create config file (vi otel-config.yaml)

```bash
receivers:
  otlp:
    protocols:
      grpc:
        endpoint: 0.0.0.0:4317
      http:
        endpoint: 0.0.0.0:4318

processors:
  batch:

exporters:
  debug:
    verbosity: detailed

service:
  pipelines:
    traces:
      receivers: [otlp]
      processors: [batch]
      exporters: [debug]
    metrics:
      receivers: [otlp]
      processors: [batch]
      exporters: [debug]
    logs:
      receivers: [otlp]
      processors: [batch]
      exporters: [debug]
```


## Basic Run
Run the container with basic configuration and volume mount

```bash
docker run -it --name opentelemetry-collector-contrib \
  -v $(pwd)/otel-config.yaml:/etc/otel/config.yaml \
  ghcr.io/cleanstart-containers/opentelemetry-collector-contrib:latest \
  --config /etc/otel/config.yaml
```

## Production Deployment
Deploy with production security settings

```bash
docker run -d \
  --name opentelemetry-collector-contrib-prod \
  --security-opt=no-new-privileges \
  --user 1000:1000 \
  --restart unless-stopped \
  -v /app:/app \
  -v $(pwd)/otel-config.yaml:/etc/otel/config.yaml:ro \
  ghcr.io/cleanstart-containers/opentelemetry-collector-contrib:latest \
  --config /etc/otel/config.yaml
```

Port Forwarding Run with custom port mappings

```bash
docker run --name opentelemetry-collector-contrib-prod \
  --security-opt=no-new-privileges \
  --user 1000:1000 \
  --restart unless-stopped \
  -p 4317:4317 \
  -p 4318:4318 \
  -p 8888:8888 \
  -v /app:/app \
  -v $(pwd)/otel-config.yaml:/etc/otel/config.yaml:ro \
  ghcr.io/cleanstart-containers/opentelemetry-collector-contrib:latest \
  --config /etc/otel/config.yaml
```

## Environment Variables
Configuration options available through environment variables

| Variable | Default | Description |
|----------|---------|-------------|
| ENV | production | Environment mode |
| LOG_LEVEL | info | Logging level |


## Kubernetes Security Context
Recommended security context for Kubernetes deployments

```yaml
securityContext:
  allowPrivilegeEscalation: false
  capabilities:
    drop:
    - ALL
  readOnlyRootFilesystem: true
  runAsUser: 1000
  runAsGroup: 1000
```

## Documentation Resources
Essential links and resources for further information
 
**CleanStart Images**: https://images.cleanstart.com/
 
**Community Images**:
**Docker Hub**: https://hub.docker.com/u/cleanstart<br>
**GitHub**: https://github.com/cleanstart-containers<br>
**AWS ECR Public Gallery**: https://gallery.ecr.aws/cleanstart/
 
**Presence on Social Media**:
**Community**: https://www.linkedin.com/groups/18324021/<br>
**YouTube**: https://www.youtube.com/@CleanStartOfficial<br>
 
**Contribute to Container Use Cases**: https://github.com/cleanstart-dev/cleanstart-use-cases/
