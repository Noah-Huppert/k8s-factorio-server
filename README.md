# Kubernetes Factorio Server
Factorio server hosted on Kubernetes.

# Table Of Contents
- [Overview](#overview)
- [Accessing Factorio Data](#accessing-factorio-data)

# Overview
Provides a Helm chart in `factorio/` which runs the 
[Factorio headless server](https://www.factorio.com/download-headless).  

Deploy this chart by navigating into `factorio/` and running:

```
make
```

To host an existing save use the `kubectl cp` command.

# Accessing Factorio Data
The container which runs the Factorio server stores data in `/factorio`.  

The `kubectl cp` command can be used to transfer save and / or mod files to 
the server:

Example of transferring a mod file to the server:

```
kubectl cp ./factorio-save.zip factorio/factorio-0:/factorio/saves/
```

This command assumes the pod the server is running in is called `factorio-0`. 
This may differ based on your deployment.  

To find the name of the pod running your Factorio server run:

```
kubectl -n factorio get pods
```
