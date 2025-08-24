Docker Networking – Direct docker run vs docker-compose

When using docker run:

You must manually create or attach to a network if you want containers to talk to each other.

Example:

docker network create my-network
docker run -d --name mongo --network my-network mongo
docker run -d --name app --network my-network my-app


If you don’t specify a network, containers go into the default bridge network (not good for service-to-service communication by name).

When using docker-compose (YAML file):

You don’t need to create or specify a network explicitly.

Docker Compose automatically creates a default network for all services defined in the file.

All containers in the same docker-compose.yml can communicate with each other by service name.

Example docker-compose.yml:

version: '3'
services:
  mongo:
    image: mongo
  app:
    image: my-app
    depends_on:
      - mongo


In this setup, the container app can reach Mongo just by using hostname mongo (no IPs or manual network setup needed).

👉 Quick Reminder:

docker run → you handle the network.

docker-compose → it creates and manages the network for you automatically.