# Kubernetes Factorio Server
Factorio server hosted on Kubernetes.

# Table Of Contents
- [Overview](#overview)
- [Finding The Factorio Pod Name](#finding-the-factorio-pod-name)
- [Accessing Factorio Data](#accessing-factorio-data)
	- [Save File Example](#save-file-example)
	- [Factorio Configuration File Example](#factorio-configuration-file-example)
- [Viewing Server Logs](#viewing-server-logs)
- [Running A Terminal On The Server](#running-a-terminal-on-the-server)
- [Gracefully Shutting Down The Server](#gracefully-shutting-down-the-server)

# Overview
Provides a Helm chart in `factorio/` which runs the 
[Factorio headless server](https://www.factorio.com/download-headless).  

Deploy this chart by navigating into `factorio/` and running:

```
make
```

# Finding The Factorio Pod Name
To find the name of the pod running your Factorio server run:

```
kubectl -n factorio get pods
```

# Accessing Factorio Data
The container which runs the Factorio server stores data in `/factorio`.  

The `kubectl cp` command can be used to transfer save and / or mod files to 
the server:

## Save File Example
Example of transferring a save file to the server:

```
kubectl cp ./factorio-save.zip factorio/<factorio pod name>:/factorio/saves/
```

## Factorio Configuration File Example
The same command can be used to tweak a Factorio server's 
`server-settings.json` file.  

First download the config file to your local computer:

```
kubectl cp factorio/<factorio pod name>:/factorio/config/server-settings.json .
```

Edit the downloaded `server-settings.json` file which is now in your current 
working directory.  

Then upload the edited config file back up to your Factorio server:

```
kubectl cp factorio/<factorio pod name>:/factorio/config/ ./server-settings.json
```

# Viewing Server Logs
To view the Factorio server's logs run the following command on your local 
computer:

```
kubectl -n factorio logs -l app=factorio --timestamps
```

# Running A Terminal On The Server
To gain more detailed insight or simply to perform maintenance tasks it may be 
useful to run a shell on the machine hosting your Factorio server.  

To do so run the following on your local computer:

```
kubectl -n factorio exec -it <factorio pod name> -- /bin/sh
```

To exit this shell hit Ctrl + d.

# Gracefully Shutting Down The Server
When Kubernetes shuts down a pod it sends the SIGTERM signal to the main 
process (In our case the Factorio server).  

The Factorio server is built to save the game and exit when it receives a 
SIGTERM signal.  

Because of this no extra steps must be taken for a Factorio server to be 
shut down gracefully.
