# Running Locally

## Pre-requisites

* [Go](https://golang.org/dl/) (The project currently uses version 1.13)
* [Yarn](https://classic.yarnpkg.com/en/docs/install/#mac-stable)
* [Docker](https://docs.docker.com/get-docker/)
* [Kustomize](https://github.com/kubernetes-sigs/kustomize/blob/master/docs/INSTALL.md)
* [protoc](http://google.github.io/proto-lens/installing-protoc.html) `brew install protobuf`
* [`jq`](https://stedolan.github.io/jq/download/)
* A local Kubernetes cluster

We recommend using [K3D](https://k3d.io/) to set up the local Kubernetes cluster since this will allow you to test RBAC set-up and is fast. You can set-up K3D to be part of your default kube config as follows:

    k3d cluster start --wait
    
Alternatively, you can use [Minikube](https://github.com/kubernetes/minikube) to set up the local Kubernetes cluster. Once a local Kubernetes cluster has started via `minikube start`, your kube config will use Minikube's context automatically.

Add to /etc/hosts:

    127.0.0.1 dex
    127.0.0.1 minio
    127.0.0.1 postgres
    127.0.0.1 mysql

To install into the “argo” namespace of your cluster: Argo and MinIO (for saving artifacts and logs):

    make start 

If you want MySQL for the workflow archive:

    make start PROFILE=mysql

You’ll now have

* Argo Server API on https://localhost:2746
* UI on http://localhost:8080
* MinIO  http://localhost:9000 (use admin/password)

Either:

* Postgres on  http://localhost:5432, run `make postgres-cli` to access.
* MySQL on  http://localhost:3306, run `make mysql-cli` to access.

At this point you’ll have everything you need to use the CLI and UI.

## Clean

To clean-up everything:

    make clean
    kubectl delete ns argo
    docker system prune -af
