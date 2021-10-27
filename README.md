# About

This project is a demo of an implementation of GitOps practices and CI/CD Pipeline with the objective to build an nodejs application and deploy to k8s in a automatic way.

# Features

* ArgoCD (https://argo-cd.readthedocs.io/en/stable/)
* Jenkins (https://www.jenkins.io/)
* Kustomize (https://kustomize.io/)
* Istio (https://istio.io/)
* Kubernetes (https://kubernetes.io/pt-br/)

# How it works ?

![](https://user-images.githubusercontent.com/70732391/139129181-0b1231da-a83e-4ebc-984c-d68b065191ec.jpg)

There will be two repositories, one for app source code(https://github.com/DaviAraujoCC/node_simple_app) and this for k8s configuration/manifests files.

The repository used for store configuration files will be synced with ArgoCD for Continuous Deployment and the app source code repo with jenkins.
After a change is made in branch 'main' of source code repo, we can use the pipeline with jenkins to build, push and deploy the app changing the configuration in this repository. 





