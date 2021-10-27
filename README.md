# About

This project is a demo of an implementation of GitOps practices and CI/CD Pipeline with the objective to build an nodejs application and deploy to k8s in a automatic way.

## Features

* ArgoCD (https://argo-cd.readthedocs.io/en/stable/)
* Jenkins (https://www.jenkins.io/)
* Kustomize (https://kustomize.io/)
* Istio (https://istio.io/)
* Kubernetes (https://kubernetes.io/pt-br/)

## How this pipeline works ?

![](https://user-images.githubusercontent.com/70732391/139129181-0b1231da-a83e-4ebc-984c-d68b065191ec.jpg)

There will be two repositories, one for app source code(https://github.com/DaviAraujoCC/node_simple_app) and this for k8s configuration/manifests files.

The repository used for store configuration files will be synced with ArgoCD in cluster for Continuous Deployment and the app source code repo with jenkins.
After a change is made in branch 'main' of source code repo, we can use the pipeline integrated with jenkins to build, push and deploy the app changing the configuration in the actual repository.

The access for the web application will be made through istio ingress-gateway at port 80. 

## How the nodejs application works ?

Please access https://github.com/DaviAraujoCC/node_simple_app for more info.

## What is the benefit of implementing GitOps solution with ArgoCD like this ?

Instead of creating various accesses for your team to kubernetes cluster, making it hard to manage the certificates and possible failures and security breaches, with GitOps practices all you need is to focus on managing the access to the Git environment (users, branches etc.), every configuration/modification will be centered in a repository, since argoCD will be responsible to sync your manifests for you, it will be easy to track for changes and simpler rollbacks for disaster recovery. 

