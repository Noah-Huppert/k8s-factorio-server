# Kubernetes Factorio Server
Factorio server hosted on Kubernetes.

# Table Of Contents
- [Overview](#overview)
- [Connecting](#connecting)
- [Operating Modes](#operating-modes)
	- [Files](#files)
	- [Multiplayer Server](#multiplayer-server)

# Overview
Provides a Helm chart in `factorio/` which runs the 
[Factorio headless server](https://www.factorio.com/download-headless).  

# Operating Modes
The chart in `factorio/` has two modes of operation. To switch between these 
modes set the `operatingMode` value in `values.yaml` to:


- `files`: Runs an SSH server with the Factorio save directory mounted
- `factorio`: Runs a Factorio multiplayer server

This lets you upload / download your own saves and then play these saves.

## Files
To access the saves directory used by the Factorio server run the chart in 
`factorio/` with the `operatingMode` value set to `files`.  

This will stop the hosting of the multiplayer Factorio server and start an 
SSH server with access to the game saves directory. 

Then copy save data over with a tool like SCP which utilizes an SSH connection 
to transfer files. You can connect to the address of the Kubernetes ingress 
object 

Put save files in the root directory of this server.  

You can launch the chart with the correct operating mode setting by running: 

```
make files
```

in the `factorio/` directory.

## Multiplayer Server
To start a Factorio multiplayer server run the chart in the `factorio/` 
directory with the `operatingMode` value set to `factorio`.  

Then connect to the server via the Factorio game at the address of the 
Kubernetes ingress object made by the chart.

You can launch the chart with the correct operating mode setting by running:

```
make factorio
```
