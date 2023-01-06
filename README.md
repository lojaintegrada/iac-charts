# iac-charts (public-repo)
A github repo as helm-chart repository

### What is in this repo?
A collection of forked/customize charts that we use, so we can avoid external dependencies. All credits to their authors. 

NOTE: one custom thing that we add to charts is the extra-manifest.yaml that allow us to create other resources that are not defined by the chart, like istio virtualservice

| chart | based on 
| -- | -- | 
| consul | https://artifacthub.io/packages/helm/hashicorp/consul
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
