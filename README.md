# Kubernetes Factorio Server
Factorio server hosted on Kubernetes.

# Table Of Contents
- [Overview](#overview)
- [Setup](#setup)
	- [Saves FTP](#saves-ftp)
	- [Multiplayer Server](#multiplayer-server)

# Overview
Provides a Helm chart in `factorio/` which runs the 
[Factorio headless server](https://www.factorio.com/download-headless).  

# Setup
The chart in `factorio/` allows one to access the saves directory used by the 
Factorio server over FTP and then run the Factorio server with this saves 
directory.  

This lets you upload / download your own saves and then play these saves.

## Saves FTP
To access the saves directory used by the Factorio server run the chart in 
`factorio/` with the `operatingMode` value set to `ftp`.  

This will stop the hosting of the multiplayer Factorio server and start an 
FTP server with access to the game saves directory.  

Simply FTP into the address of the Kubernetes ingress object made by the chart. 
Then place save files in the root directory of the FTP server.  

You can launch the chart with the correct operating mode setting by running: 

```
make ftp
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
