# Firefly III

**Firefly III** is a modern, self-hosted personal finance manager. This project empowers you to track expenses, incomes, and budgets with robust double-entry bookkeeping—with streamlined Kubernetes deployment, GitOps best practices, and production-ready integrations:

- **MariaDB** as the database (managed by the [MariaDB Operator](https://github.com/mariadb-operator/mariadb-operator))
- **Traefik v3** for ingress
- Optional **HashiCorp Vault** integration for secrets management


## Features

- Accurate double-entry bookkeeping
- Multiple currency support
- Flexible budgeting and spending limits
- Visual reports and analytics
- REST API and mobile apps
- Import/export for CSV and bank data
- Kubernetes-native deployment with [Kustomize](https://kubectl.docs.kubernetes.io/guides/introduction/kustomize/) overlays
- MariaDB backend, managed via MariaDB Operator
- Traefik v3 as ingress controller
- Optional: HashiCorp Vault for secret management


## Getting Started

### Requirements

- Kubernetes cluster (v1.15+)
- `kubectl` configured
- [ArgoCD](https://argo-cd.readthedocs.io/en/stable/) installed
- [MariaDB Operator](https://github.com/mariadb-operator/mariadb-operator) installed
- [Traefik v3](https://doc.traefik.io/traefik/getting-started/quick-start-with-kubernetes/) as Ingress controller
- (Optional) [HashiCorp Vault](https://developer.hashicorp.com/vault/docs/deploy/kubernetes) deployed
- (Optional) Kustomize standalone, or use via `kubectl`


## Kubernetes Deployment Details

### Database: MariaDB via MariaDB Operator

- **Firefly III** connects to a MariaDB database managed as a Kubernetes _Custom Resource_ by the MariaDB Operator.
- Credentials are stored as Kubernetes Secrets (optionally sourced from Vault).
- Persistent storage handled via configurable PersistentVolumeClaims.


### Ingress: Traefik v3

- Traefik v3 handles all ingress, exposed via properly annotated Kubernetes `Ingress` resources.
- Configurations are tailored for seamless Traefik v3 operation.


### (Optional) HashiCorp Vault

- Use Vault to centrally manage secrets.
- Integrate by referencing Vault-injected Kubernetes Secrets, either with Vault Agent injector or Vault Secrets Operator.


## Deployment with Kustomize and ArgoCD

1. **Clone the Repository**

```bash
git clone https://github.com/daniva6/firefly-iii.git
cd firefly-iii
```

2. **Review Kustomize Structure**
    - `base/` – core manifests (app, DB, ingress)
    - `overlays/dev/` and `overlays/prod/` – environment specifics, each with their own `argocd-app.yaml` for ArgoCD
3. **Check MariaDB Operator Installation**
    - Install MariaDB Operator as described in [the project documentation](https://github.com/mariadb-operator/mariadb-operator).
4. **Apply ArgoCD Application**
    - Deploy your environment by applying the overlay’s Application manifest:

```bash
kubectl apply -f overlays/dev/argocd-app.yaml
# or
kubectl apply -f overlays/prod/argocd-app.yaml
```

    - ArgoCD will watch and sync the entire stack, including MariaDB and ingress resources.

## Usage

- Access Firefly III via the Traefik-managed endpoint.
- Follow the web UI setup to connect to MariaDB and start managing finances.


## Documentation, Community \& Contribution

- **Firefly III Documentation:**
[https://docs.firefly-iii.org/](https://docs.firefly-iii.org/)
- **ArgoCD Documentation:**
[https://argo-cd.readthedocs.io/en/stable/](https://argo-cd.readthedocs.io/en/stable/)
- **Kustomize Documentation:**
[https://kubectl.docs.kubernetes.io/guides/introduction/kustomize/](https://kubectl.docs.kubernetes.io/guides/introduction/kustomize/)
- **MariaDB Operator:**
[https://github.com/mariadb-operator/mariadb-operator](https://github.com/mariadb-operator/mariadb-operator)
- **Traefik v3 \& Ingress:**
[https://doc.traefik.io/traefik/getting-started/quick-start-with-kubernetes/](https://doc.traefik.io/traefik/getting-started/quick-start-with-kubernetes/)
- **HashiCorp Vault on Kubernetes:**
[https://developer.hashicorp.com/vault/docs/deploy/kubernetes](https://developer.hashicorp.com/vault/docs/deploy/kubernetes)
- **Firefly III Community \& Issues:**
[Discussions](https://github.com/firefly-iii/firefly-iii/discussions) | [Issues](https://github.com/firefly-iii/firefly-iii/issues)
- **Contributing Guide:**
[https://docs.firefly-iii.org/contributing/](https://docs.firefly-iii.org/contributing/)

Contributions are welcome—fork the repository and submit your improvements for deployment manifests.

**Empower your financial privacy and operations—deployable at scale, fully declarative, featuring MariaDB (managed by MariaDB Operator), Traefik v3, and optional HashiCorp Vault.**



