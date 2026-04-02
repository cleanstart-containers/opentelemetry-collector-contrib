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

## Basic Run
Run the container with basic configuration

```bash
docker run -it --name opentelemetry-collector-contrib ghcr.io/cleanstart-containers/opentelemetry-collector-contrib:latest
```

## Production Deployment
Deploy with production security settings

```bash
docker run -d --name opentelemetry-collector-contrib-prod \
  --security-opt=no-new-privileges \
  --user 1000:1000 \
  --restart unless-stopped \
  ghcr.io/cleanstart-containers/opentelemetry-collector-contrib:latest
```

Volume Mount Mount local directory for persistent data

```bash
docker run -v /app:/app ghcr.io/cleanstart-containers/opentelemetry-collector-contrib:latest
```

Port Forwarding Run with custom port mappings

```bash
docker run -p 8080:8080 ghcr.io/cleanstart-containers/opentelemetry-collector-contrib:latest
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

- **Container Registry**: [https://www.cleanstart.com/](https://www.cleanstart.com/)
- **CleanStart Community Images**: [https://hub.docker.com/u/cleanstart](https://hub.docker.com/u/cleanstart)
- **How-to-Run CleanStart images & sample projects**: [https://github.com/cleanstart-containers](https://github.com/cleanstart-containers)
  - How to run sample projects using Dockerfile
  - How to deploy via Kubernetes YAML
  - How to migrate from public images to CleanStart images

---

**Vulnerability Disclaimer**

CleanStart offers Docker images that include third-party open-source libraries and packages maintained by independent contributors. While CleanStart maintains these images and applies industry-standard security practices, it cannot guarantee the security or integrity of upstream components beyond its control.

Users acknowledge and agree that open-source software may contain undiscovered vulnerabilities or introduce new risks through updates. CleanStart shall not be liable for security issues originating from third-party libraries, including but not limited to zero-day exploits, supply chain attacks, or contributor-introduced risks.

Security remains a shared responsibility: CleanStart provides updated images and guidance where possible, while users are responsible for evaluating deployments and implementing appropriate controls.
