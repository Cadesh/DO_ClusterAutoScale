# K8S AUTOSCALABLE DEPLOYMENTS #

### 1. Introduction ###

This folder contains a basic example on how to deploy an Autoscalable app in a DO cluster
Source: https://www.digitalocean.com/docs/kubernetes/resources/autoscaling-with-hpa-ca/

### 2. Requirements ###

A Kubernetes cluster created in DO and running K8s 1.18 or 1.19 (I tested both)

### 3. References ###

https://www.digitalocean.com/docs/kubernetes/resources/autoscaling-with-hpa-ca/
https://www.digitalocean.com/docs/kubernetes/how-to/autoscale/
https://docs.aws.amazon.com/eks/latest/userguide/metrics-server.html
https://stackoverflow.com/questions/59262706/k8s-hpa-cant-get-the-cpu-information

---

### 5. Deploying an Autoscalable Application ###


1 - Deploy the Metrics Server with the command '''kubectl create -f 1_metrics-server.yml'''

Check the deployment with '''kubectl get deployment metrics-server -n kube-system'''

2 - Deploy the test app "hello" with the command '''kubectl create -f 2_hello.yml'''

Note that this scprit defines an *HorizontalPodAutoscaler (HPA)* that defines the CPU utilization that triggers the autoscale

Check the HPA with the command '''kubectl describe hpa hello'''

3 - Deploy the traffic generator with '''kubectl create -f 3_load-generator.yml''' 

Check the number of pods and nodes scaling up/down depending the number of traffic generators. To scale traffic generators use the command '''kubectl scale deployment/load-generator --replicas 2''' 
Where *--replicas 2* defines the creation of 2 pods


