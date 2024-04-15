## Kuadrant Getting Started - Single Cluster

### Overview

We've got a quickstart script to quickly set up Kuadrant in a single local `kind` cluster, automating the installation of essential components like Istio, cert-manager, MetalLB and Kuadrant. This is useful for development, or for checking the project out.

### Prerequisites
- **Docker**: Version 20.10 or newer. [Install Docker](https://docs.docker.com/engine/install/)
- **Kind**: Version 0.11 or newer. [Install Kind](https://kind.sigs.k8s.io/)
- **Kubectl**: Compatible with your Kubernetes version. [Install Kubectl](https://kubernetes.io/docs/tasks/tools/)
- **OpenSSL**: Version 3 or newer. [Check and install OpenSSL](https://www.openssl.org/source/)
- **DNS Management**: AWS with Route 53 or GCP with Cloud DNS. Choose based on your existing infrastructure.

Optional for macOS: Tools for L3 connectivity (for convienience):
- [Docker Mac Net Connect](https://github.com/chipmk/docker-mac-net-connect)
- [Podman Mac Net Connect](https://github.com/jasonmadigan/podman-mac-net-connect)

### Environmental Variables
Configure environment variables for Istio and DNS settings based on your chosen DNS provider. Replace example values with your actual values.

#### For AWS Users:
| Env Var | Example Value | Description |
|---------|---------------|-------------|
| `KUADRANT_ZONE_ROOT_DOMAIN` | `example.com` | Root domain for DNS settings. |
| `KUADRANT_AWS_DNS_PUBLIC_ZONE_ID` | `Z01234567US0IQE3YLO00` | AWS Route 53 Zone ID. |
| `KUADRANT_AWS_ACCESS_KEY_ID` | `AKIA1234567890000000` | AWS Access Key ID. |
| `KUADRANT_AWS_SECRET_ACCESS_KEY` | `your-secret-key` | AWS Secret Access Key. |
| `KUADRANT_AWS_REGION` | `eu-west-1` | AWS Region. |

#### For GCP Users:
| Env Var | Example Value | Description |
|---------|---------------|-------------|
| `GOOGLE_CLIENT_ID` | `your-google-client-id` | Google Cloud client ID. |
| `GOOGLE_CLIENT_SECRET` | `your-google-client-secret` | Google Cloud client secret. |
| `GOOGLE_REFRESH_TOKEN` | `your-google-refresh-token` | Google Cloud refresh token. |
| `PROJECT_ID` | `your-google-project-id` | ID of the Google project. |
| `ZONE_NAME` | `example-google` | GCP DNS zone name. |
| `ZONE_DNS_NAME` | `example.google.hcpapps.net` | Full DNS zone name. |
| `LOG_LEVEL` | `1` | Log level for the Controller. |


#### Istio installation method
| Env Var              | Example Value | Description                                                   |
|----------------------|---------------|---------------------------------------------------------------|
| `ISTIO_INSTALL_SAIL` | `true`        | Enable Istio installation via Project Sail, default `false`. |

> Configure these variables in your `.zshrc` or `.bash_profile` for persistence.

### Installation
Set the script version and execute the setup script:

```bash
export KUADRANT_REF=main
curl "https://raw.githubusercontent.com/kuadrant/kuadrant-operator/${KUADRANT_REF}/hack/quickstart-setup.sh" | bash
```

> **Security Note**: Review script (contents)[https://raw.githubusercontent.com/kuadrant/kuadrant-operator/main/hack/quickstart-setup.sh] before execution for safety.

### Verify Installation

Check that all components are running:

```bash
kubectl get pods -n kuadrant-system
```

### What's Next

The next step is to set up and use the policies provided by Kuadrant. For detailed instructions, visit:

[Secure, Protect and Connect your Gateway](https://docs.kuadrant.io/kuadrant-operator/doc/user-guides/secure-protect-connect/)
