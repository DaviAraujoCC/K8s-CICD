# k8s-node-app-simple

[![AKS](https://github.com/DaviAraujoCC/k8s-node-app-simple/actions/workflows/main.yml/badge.svg)](https://github.com/DaviAraujoCC/k8s-node-app-simple/actions/workflows/main.yml)

Simple project created to scale an application in k8s (aws/gcp/azure)

It has the following architecture

![image](https://user-images.githubusercontent.com/70732391/128958652-af2d1ed4-5506-4341-9884-c61c2cd6fb9b.png)

It contains a simple script in node.js v12 that will show a screen of "Nice app" if it runs successfully, but to achieve that you need to have all containers communicating with each other (api, db and web)

In data directory there are some folders containing the code of api/web applications, with dockerfile used by me for making the images

you can use the docker-compose to test on local example : http://localhost:8080

<b>Example of successfully request:</b>

![image](https://user-images.githubusercontent.com/70732391/128959370-12533c9c-42f7-4ec9-837c-00e0774b1939.png)

![image](https://user-images.githubusercontent.com/70732391/130360982-e88d9d15-2201-453d-9372-a5ddfefb3d4d.png)

