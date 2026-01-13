# helm-loki

A Crossplane Configuration package that installs the Loki Helm chart with a minimal, stable interface.

## Overview

`helm-loki` renders a single Helm release for Loki. It exposes only the inputs needed
for chart values, namespace, and release name, keeping the interface stable while allowing full Helm overrides.

## Features

- **Minimal Helm interface**: values and overrideAllValues with stable defaults
- **Predictable naming**: defaults to `<clusterName>-loki` in the `loki` namespace
- **GitOps friendly**: ships a `.gitops/` deploy chart

## Prerequisites

- Crossplane installed in the cluster
- Crossplane providers:
  - `provider-helm` (>=v1.0.2)
- Crossplane function:
  - `function-auto-ready` (>=v0.6.0)

## Quick Start

```yaml
apiVersion: pkg.crossplane.io/v1
kind: Configuration
metadata:
  name: helm-loki
spec:
  package: ghcr.io/hops-ops/helm-loki:latest
```

```yaml
apiVersion: helm.hops.ops.com.ai/v1alpha1
kind: Loki
metadata:
  name: loki
  namespace: example-env
spec:
  clusterName: example-cluster
  values:
    loki:
      limits_config:
        retention_period: 168h
```

## Development

```bash
make render
make validate
make test
```
