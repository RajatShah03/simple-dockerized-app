# **Images**

## Mondodb
- name: mongo *(Official)*

## Backend
- name: node-goals

## Frontent
- name: react-goals

# **Containers**

## Mondodb
- name: mongo-db
- port: 27017

## Backend
- name: node-app
- port: 80

## Frontent
- name: react-app
- port: 3000

# Volumes

# Network
- name: app-net
---
`$ docker network create app-net`

# Build backend image
`$ cd backend`
`$ docker build -t node-goals .`

# Build frontend image
`$ cd frontend`
`$ docker build -t react-goals .`

# Instantiate mongodb container
`$ docker run --name mongo-db --rm -d --network app-net -v data:/data/db -e MONGO_INITDB_ROOT_USERNAME=username -e MONGO_INITDB_ROOT_PASSWORD=secret mongo`

# Instantiate backend container
`$ docker run --name node-app --rm -d -p 80:80 --network app-net -v logs:/app/logs -v "D:/Courses/udemy/Docker and Kubernetes/Resources/multi-01-starting-setup/backend:/app" -v /app/node_modules -e MONGODB_USERNAME=username node-goals`

# Instantiate frontend container
`$ docker run --name react-app --rm -p 3000:3000 -it -v "D:/Courses/udemy/Docker and Kubernetes/Resources/multi-01-starting-setup/frontend/src:/app" react-goals`