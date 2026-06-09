# Tdarr Helm Chart

Baseline Helm chart for [Tdarr](https://github.com/HaveAGitGat/Tdarr): distributed transcoding with a server and internal node. Built on the [bjw-s app-template](https://github.com/bjw-s/helm-charts).

## What this baseline does

- Deploys Tdarr server (`ghcr.io/haveagitgat/tdarr`) with internal node enabled.
- Exposes Web UI on port `8265` and server API on `8266` (ClusterIP by default).
- PVC-backed volumes for server data, configs, logs, and cache.
- Media mount defaults to `emptyDir`; override with `existingClaim` in your values to align with Plex or other media charts.

## Key values

| Area | Where | Default |
|------|-------|---------|
| Ingress | `tdarr.ingress.main.enabled` | `false` |
| Server storage | `tdarr.persistence.server.*` | PVC 5Gi |
| Configs / logs / cache | `tdarr.persistence.configs` / `logs` / `cache` | PVC 1Gi / 1Gi / 10Gi |
| Media | `tdarr.persistence.media.*` | `emptyDir` (override with `existingClaim`) |

## Install

```bash
helm repo add expectedbehaviors https://expectedbehaviors.github.io/tdarr
helm install tdarr expectedbehaviors/tdarr -f my-values.yaml -n tdarr --create-namespace
```

## Render & validation

```bash
helm dependency update . && helm template tdarr . -f values.yaml -n tdarr
```

## Argo CD

Point your Application at this repo (path: `.`) and pass your values. Override persistence with `existingClaim` for server, configs, logs, cache, and media mounts in your private values repo.

## Support this project

I build tools to get the best homelab experience I can from what's available and to grow as a programmer along the way. If you'd like to contribute, donations go toward homelab operating costs and subscriptions that keep this tooling maintained. Optional and appreciated.

[![Donate with PayPal](https://www.paypalobjects.com/en_US/i/btn/btn_donate_LG.gif)](https://www.paypal.com/donate/?business=9RHVW92WMWQNL&no_recurring=0&item_name=Optional+donations+help+support+Expected+Behaviors%E2%80%99+open+source+work.+Thank+you.&currency_code=USD)
