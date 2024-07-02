# Kubernetes Configuration for MongoDB and Web Application

This project contains Kubernetes configurations for deploying a MongoDB database and a web application that interacts with it.

## Files Overview

- [`mongo-app.yaml`](mongo-app.yaml): Defines the MongoDB deployment and service.
- [`mongo-config.yaml`](mongo-config.yaml): Contains the ConfigMap for MongoDB configuration.
- [`secret.yaml`](secret.yaml): Stores the MongoDB username and password as secrets.
- [`web-app.yaml`](web-app.yaml): Defines the deployment and service for the web application.

## MongoDB Setup

### Deployment

The MongoDB deployment is defined in [`mongo-app.yaml`](mongo-app.yaml). It sets up a single replica of MongoDB with the version 6.0. The deployment uses a secret (`mongo-secret`) for the MongoDB root username and password.

### Service

The MongoDB service defined in [`mongo-app.yaml`](mongo-app.yaml) exposes MongoDB on port 27017.

### Secrets

The MongoDB username and password are stored in [`secret.yaml`](secret.yaml) as base64 encoded strings.

### ConfigMap

The MongoDB URL is stored in a ConfigMap defined in [`mongo-config.yaml`](mongo-config.yaml), which is used by the web application to connect to MongoDB.

## Web Application Setup

### Deployment

The web application deployment is defined in [`web-app.yaml`](web-app.yaml). It deploys the `mongo-express` image as the web application that interacts with MongoDB. The deployment uses the same MongoDB secrets for authentication and the ConfigMap for the MongoDB URL.

### Service

The web application service defined in [`web-app.yaml`](web-app.yaml) exposes the application on port 8081 and makes it accessible on a NodePort `30100`.

## Deployment Instructions

To deploy this setup to your Kubernetes cluster, apply the configurations in the following order:

1. Deploy the secrets:

   kubectl apply -f secret.yaml

2. Deploy the ConfigMap:

   kubectl apply -f mongo-app.yaml

3. Deploy the MongoDB setup:

   kubectl apply -f web-app.yaml

4. Deploy the web application:

   kubectl apply -f web-app.yaml
