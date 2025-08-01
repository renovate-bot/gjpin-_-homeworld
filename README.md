# Domains
* argocd.${BASE_DOMAIN}
* grpc.argocd.${BASE_DOMAIN}
* grafana.${BASE_DOMAIN}
* immich.${BASE_DOMAIN}
* longhorn.${BASE_DOMAIN}
* nextcloud.${BASE_DOMAIN}

# Variables
```bash
# argocd, grafana, immich, longhorn, nextcloud
export BASE_DOMAIN=domain.com

# external-dns, cert-manager
export CLOUDFLARE_API_TOKEN=

# cert-manager
export ACME_EMAIL=

# external-dns
export EXTERNAL_IP=10.0.0.1

# longhorn
export LONGHORN_ENCRYPTION_PASSPHRASE=

# nextcloud
export NEXTCLOUD_USERNAME=
export NEXTCLOUD_PASSWORD=

# grafana
export GRAFANA_USERNAME=
export GRAFANA_PASSWORD=

# gigapipe
export GIGAPIPE_CLICKHOUSE_PASSWORD=
```

# Helm repos
```bash
# argo
helm repo add argo https://argoproj.github.io/argo-helm

# cert-manager
helm repo add cert-manager https://charts.jetstack.io

# clickhouse
helm repo add altinity-clickhouse-operator https://docs.altinity.com/clickhouse-operator/

# cloudnative-pg
helm repo add cloudnative-pg https://cloudnative-pg.io/charts

# external-dns
helm repo add external-dns https://kubernetes-sigs.github.io/external-dns/

# gitea
helm repo add gitea https://dl.gitea.com/charts/

# grafana
helm repo add grafana https://grafana.github.io/helm-charts

# kube-prometheus-stack
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts

# longhorn
helm repo add longhorn https://charts.longhorn.io

# metrics-server
helm repo add metrics-server https://kubernetes-sigs.github.io/metrics-server/

# minio-operator
helm repo add minio-operator https://operator.min.io

# nextcloud
helm repo add nextcloud https://nextcloud.github.io/helm

# otel-collector
helm repo add open-telemetry https://open-telemetry.github.io/opentelemetry-helm-charts

# s3 operator
helm repo add inseefrlab https://inseefrlab.github.io/helm-charts
```

# New component checklist
* fullnameOverride
* requests/limits
* autoscaling (hpa)
* nodeselector
* httproute + gateway listener (if applicable)
* serviceMonitor

# ArgoCD
* **Sync wave 1**
   * prometheus-operator-crd: CRDs required by service monitors
* **Sync wave 2**
   * envoy-gateway: Gateway API and provides CRDs required by HTTP/GRPC routes
* **Sync wave 3**
   * cert-manager: TLS certificates management
   * external-dns: manages DNS records
   * longhorn: block storage
* **Sync wave 4**
   * argocd
   * cloudnative-pg: postgresql operator
   * dragonfly-operator: dragonfly (redis-compatible) operator
   * minio-operator: s3-compatible storage operator
   * clickhouse-operator
* **Sync wave 5**
   * s3-operator: minio bucket/policies operator
* **Sync wave 6**
   * nextcloud
   * immich
   * otel-collector
   * grafana
   * gigapipe
   * ente-auth