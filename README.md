# Kubernetes for Data Engineering

This repository contains the configuration files and DAGs (Directed Acyclic Graphs) for setting up containerized namespaces in Kubernetes and automatically scheduled workflows in Airflow. Within this project, we set up the Kubernetes Dashboard which manages our Kubernetes clusters and set up Apache Airflow to programmatically author, schedule, and monitor workflows.

## Requirements
- Docker
- Kubernetes
- Helm

## DAGs
- fetch_and_preview.py : A DAG for fetching and previewing data
- hello.py : An example DAG to demonstrate basic Airflow concepts

## k8s
- dashboard-adminuser.yaml : YAML file for setting up an admin user for the Kubernetes Dashboard
- dashboard-clusterrole.yaml : YAML file for setting up the cluster role for the Kubernetes Dashboard.
- dashboard-secret.yaml : YAML file for managing secrets used by the Kubernetes Dashboard
- values.yaml : YAML file containing values for customizing the Kubernetes setup

## Installation, Setup, and Usage
1. Clone this repository.
2. Deploy the Kubernetes Dashboard by applying the k8s 'kubectl apply -f k8s/'
3. Port forward 'kubectl port-forward svc/airflow-webserver 8080:8080 --namespace airflow'
4. Access the Kubernetes Dashboard by starting a proxy server 'kubectl proxy'
   Access the dashboard via: http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/
5. Get the secret: 'kubectl get secret admin-user -n kubernetes-dashboard -o jsonpath={".data.token"} | base64 -d'
6. Enter the secret token generated to log into Kubernetes
7. Deploy Apache Airflow using helm:
- 'helm repo add apache-airflow https://airflow.apache.org'
- 'helm install airflow apache-airflow/airflow -f k8s/values.yaml'
9. Add DAGs to Airflow by copying your DAG files into the DAGs folder of your Airflow deployment (e.g. via Persistent Volume, Git-sync)
