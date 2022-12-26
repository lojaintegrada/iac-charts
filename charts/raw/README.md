# Raw

Render raw kubernetes manifests managed by a helm release

# Examples

See the following examples to see the full potential:

```
resources:
- apiVersion: v1
  kind: ServiceAccount
  metadata:
    name: kibana
    namespace: kibana
  automountServiceAccountToken: false

- apiVersion: v1
  kind: Service
  metadata:
    name: kibana-product
    namespace: kibana
    labels:
      app: kibana-product
    annotations:
  spec:
    ports:
    - name: http-0-product
      port: 5601
      targetPort: http-0-product
    selector:
        app: kibana-product
```

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| resources | list | `[]` | Define resources to be deployed by the raw chart |
