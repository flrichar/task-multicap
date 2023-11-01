# Task-Multicap
Perform multiple packet captures within a pods' network namespace.

## Description
This is a small mvp for a issue I had, we needed a way to see, in real-time tcpdumps, and/or run them concurrently and save the output, so that all traffic is accounted for in mutliple interfaces. This is a Taskfile that uses [go-task](https://taskfile.dev) to run nsenter-ed commands like tcpdump, determines the container-id and proceess-id.

### Requirements
* 1 pod with multiple interfaces ie Multus
* 1 K8S node for the test
* typical linux tooling, xargs, tcpdump on the node 
* `go-task` binary under `/usr/local/bin`
* `crictl` included with RKE2, and/or `nerdctl` under `/usr/local/bin`

### Usage
* Create a `.env` file with a regex of the pod/deployment in question, ie `SUSE`, `arch`, `some-app`,
  ... Example: `PODNAME=arch`
* Function `cri-name` and `nerd-name` creates a new dotenv environment file `.cids-env` with container-id
* Function `cri-inspect` and `nerd-inspect` appends to the cids-env environment with the process-id of the container-id
* Must run as root

### TODO
* a lot, this is a work in progress
* more concurrent operations

### Purpose
* Automate some bash-like functions with go-task.

