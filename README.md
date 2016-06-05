# lm_collector

## TODO
  - Remove NTP dependency if possible
  - Log directly to the console and not to the console through tailing a log file
  - Reimplement in CentOS v7 for internal usage
  - Insert environment variables from etcd
  - Determine max RAM usage necessary for the container
  - Determine setup procedure for failover collectors and document it
  - Put the updated container on the Docker hub

## Overview
Docker image capable of installing and running a LogicMonitor collector

## Website
http://www.logicmonitor.com

## Docker repository
https://hub.docker.com/r/logicmonitor/lm_collector/

## Requirements
You must have a LogicMonitor account

## Usage
This container will utilize environment variables to authenticate to your
LogicMonitor portal.

company - your company's name

username - your LogicMonitor username

password - your LogicMonitor password

cleanup - if this is non-null, the collector will remove itself from the portal
when the container is stopped.

## Example
```
docker run --name lm_collector -d \
    -e company=<your-company> \
    -e username=<your-username> \
    -e password=<your-password> \
    -e cleanup=true \
logicmonitor/lm_collector:latest
```
