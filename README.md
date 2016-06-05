# lm_collector

## TODO
  - Remove NTP dependency if possible
    - Looks like it is only using the NTP binaries and not running a NTPD instance.
  - Log directly to the console and not to the console through tailing a log file
    - Look at how Nginx does this:
    - [Make a Docker application write to stdout](http://serverfault.com/questions/599103/make-a-docker-application-write-to-stdout)
    - [nginxinc/docker-nginx/stable/alpine/Dockerfile](https://github.com/nginxinc/docker-nginx/blob/master/stable/alpine/Dockerfile)
  - Reimplement in Alpine or CentOS v7 for internal usage
    - [python](https://hub.docker.com/_/python/)
      - Is currently running on [jessie with 2.7](https://github.com/docker-library/python/blob/9383f7d4d2f96068e8957651aa3588fee8b48f71/2.7/Dockerfile)
    - Could possibly switch to [Alpine with 2.7](https://github.com/docker-library/python/blob/9383f7d4d2f96068e8957651aa3588fee8b48f71/2.7/alpine/Dockerfile)
    - If Alpine does not work then switch to CentOS v7
  - Insert environment variables from etcd
    - See: [How do I get etcd values into my systemd service on CoreOS?](http://stackoverflow.com/questions/25396167/how-do-i-get-etcd-values-into-my-systemd-service-on-coreos)
  - Determine max RAM usage necessary for the container
    - Starting with 1GB
      - [Adding collectors](http://www.logicmonitor.com/support/getting-started/i-just-signed-up-for-logicmonitor-now-what/3-adding-collectors/)
      - A minimum of 1GB of RAM (preferably 2GB if you plan to collect data from more than 100 devices). Note that as a rule of thumb, each collector is designed to efficiently monitor 100 - 200 devices.
  - Determine setup procedure for failover collectors and document it
    - [Collector Failover & Failback](http://help.logicmonitor.com/the-new-ui/settings/collectors/collector-failover-failback/)
    - [Do I need a Backup Collector?](http://help.logicmonitor.com/the-new-ui/settings/collectors/do-i-need-a-backup-collector/)
    - [Monitoring your Collector](http://www.logicmonitor.com/support/settings/collectors/monitoring-your-collector/)
  - Run as a non root user
    - From [Installing a Linux Collector](http://www.logicmonitor.com/support/getting-started/i-just-signed-up-for-logicmonitor-now-what/3-adding-collectors/#Installing-a-Linux-Collector):
      - Under Linux/Unix environments, the collector is required to run as root. The primary reason for this requirement is because the collector services needs direct access to the networking stack for the ping collector to function properly. Note: /bin/ping is SUID root.
  - Put the updated container on the Docker hub
    - https://hub.docker.com/u/mywebgrocer/

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
