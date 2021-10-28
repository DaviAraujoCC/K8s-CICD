# About

This project is a demo of an implementation of GitOps practices and CI/CD Pipeline with the objective to build a nodejs application and deploy to k8s in an autonomous way.

## Features

* ArgoCD (https://argo-cd.readthedocs.io/en/stable/)
* Jenkins (https://www.jenkins.io/)
* Kustomize (https://kustomize.io/)
* Istio (https://istio.io/)
* Kubernetes (https://kubernetes.io/)

## How the solution works ?

![jenkins](https://user-images.githubusercontent.com/70732391/139169010-9afaa623-1956-4e4b-b4d0-61083f43bf54.jpg)


There will be two repositories, one for app source code(https://github.com/DaviAraujoCC/node_simple_app) and this for k8s configuration/manifests files.

The repository used for store configuration files will be synced with ArgoCD and the app source code repo will be used in pipeline by jenkins, we will be using kustomize to centralize the configuration and make this integration possible.

After a change is made in branch 'main' of source code repo, we can use the pipeline (Jenkinsfile.web/Jenkinsfile.api) integrated with jenkins to build, push and deploy the app (web or api) changing the configuration in the actual repository.

The access for the web application will be made through istio ingress-gateway at port 80. 

## How the nodejs application works ?

Please access https://github.com/DaviAraujoCC/node_simple_app for more info.

## What is the benefit of implementing GitOps solution with ArgoCD like this ?

Instead of creating various accesses for your team to kubernetes cluster, making it hard to manage the certificates and possible failures and security breaches, with GitOps practices all you need is to focus on managing the access to the Git environment (users, branches etc.), every configuration/modification will be centered in a repository, since argoCD will be responsible to sync your manifests for you, it will be easy to track for changes and simpler rollbacks. 

