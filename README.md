# Kubernetes Factorio Server
Factorio server hosted on Kubernetes.

# Table Of Contents
- [Overview](#overview)

# Overview
Provides a Helm chart in `factorio/` which runs the 
[Factorio headless server](https://www.factorio.com/download-headless).  

Deploy this chart by navigating into `factorio/` and running:

```
make
```

To host an existing save use the `kubectl cp` command.
