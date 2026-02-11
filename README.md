# iac-charts (public-repo)
A github repo as helm-chart repository

### What is in this repo?
A collection of forked/customize charts that we use, so we can avoid external dependencies. All credits to their authors. 

NOTE: one custom thing that we add to charts is the extra-manifest.yaml that allow us to create other resources that are not defined by the chart, like istio virtualservice

| chart | based on 
| -- | -- | 
| consul | https://artifacthub.io/packages/helm/hashicorp/consul
| metabase | https://artifacthub.io/packages/helm/metabase-helm/metabase
| node-local-dns | https://artifacthub.io/packages/helm/deliveryhero/node-local-dns
| prometheus-elasticsearch-exporter | https://artifacthub.io/packages/helm/prometheus-community/prometheus-elasticsearch-exporter
| prometheus-kafka-exporter | https://artifacthub.io/packages/helm/prometheus-community/prometheus-kafka-exporter
| raw | https://github.com/bedag/helm-charts/tree/master/charts/raw

### How is it work?
To transform this repo into a helm-chart repo, we use the chart-releaser-action, 
for more information about it, please visit https://github.com/helm/chart-releaser-action

### Usage
Adding the repository is as simple as that:

```
helm repo add li https://lojaintegrada.github.io/iac-charts
```


### How to Use This Repository

This repository is a **local mirror of third-party Helm charts**.  
Charts are downloaded from external Helm repositories or OCI registries and stored here to avoid runtime dependencies on external URLs.

The process below describes how to properly mirror a chart into this repository.

---

# Mirroring Charts from a Helm Repository (HTTP/HTTPS)

## 1️⃣ Add the Upstream Repository

First, add the external Helm repository locally:

```bash
helm repo add <repo_name> <repo_url>
helm repo update
```

Example:

```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update
```

You can verify the chart exists:

```bash
helm search repo <repo_name>/<chart_name>
```

---

## 2️⃣ Pull the Chart (Download It)

From the root of this repository, run:

```bash
mkdir -p charts/<repo_name>

helm pull <repo_name>/<chart_name> \
  --version <chart_version> \
  --untar \
  --untardir charts/<repo_name>
```

Example:

```bash
mkdir -p charts/bitnami

helm pull bitnami/nginx \
  --version 15.10.0 \
  --untar \
  --untardir charts/bitnami
```

This will create:

```
charts/
  bitnami/
    nginx/
      Chart.yaml
      values.yaml
      templates/
      ...
```

---

## 3️⃣ Vendor Dependencies (If Any)

If the chart defines dependencies in `Chart.yaml`, vendor them locally:

```bash
cd charts/<repo_name>/<chart_name>
helm dependency update
cd -
```

This ensures subcharts are stored inside the repository.

---

## 4️⃣ Commit the Chart

```bash
git add charts/<repo_name>/<chart_name>
git commit -m "Mirror <repo_name>/<chart_name> <chart_version>"
git push
```

---

# Mirroring Charts from an OCI Registry

Some charts are distributed using OCI registries (e.g., GHCR, ECR, ACR, Harbor).

---

## 1️⃣ Login (If Required)

If the registry requires authentication:

```bash
helm registry login <registry_host>
```

Examples:

```bash
helm registry login ghcr.io
helm registry login my-registry.example.com
```

---

## 2️⃣ Pull the OCI Chart

From the root of this repository:

```bash
mkdir -p charts/oci

helm pull oci://<registry_host>/<organization>/<chart_name> \
  --version <chart_version> \
  --untar \
  --untardir charts/oci
```

Example:

```bash
mkdir -p charts/oci

helm pull oci://ghcr.io/my-org/my-chart \
  --version 1.2.3 \
  --untar \
  --untardir charts/oci
```

This will create:

```
charts/
  oci/
    my-chart/
      Chart.yaml
      values.yaml
      templates/
      ...
```

---

## 3️⃣ Commit the Chart

```bash
git add charts/oci/<chart_name>
git commit -m "Mirror OCI chart <chart_name> <chart_version>"
git push
```

---
