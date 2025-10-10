# CST8915-Lab5

## 1. Recording lab5 link:

https://youtu.be/Bb8vu-ZHRYs?si=XlAwNz7kaNYcMYqK


## 2. Docker Compose.yml 


#Specifies the version of Docker Compose format being used
version: '3'

services:

   Definition for RabbitMQ service
  rabbitmq:

    # Uses the RabbitMQ Docker image with the management plugin enabled

    image: "rabbitmq:3-management"

    # Maps the container's internal RabbitMQ ports to the host machine

    ports:

      - "5672:5672"   # Default RabbitMQ port (for messaging)
      - 
      - "15672:15672" # Management plugin UI port (for monitoring and managing)
      - 
    # Environment variables for default user credentials for RabbitMQ

    environment:

      - RABBITMQ_DEFAULT_USER=myuser      # Sets the default RabbitMQ username
      - 
      - RABBITMQ_DEFAULT_PASS=mypassword  # Sets the default RabbitMQ password

   Definition for Order Service

  order-service:

    image: ahmedboudouh/order-service:latest
    
    # Maps the container's port 3000 to port 3000 on the host machine

    ports:

      - "3000:3000"
      - 
    # Environment variables for the Order Service

    environment:

      # Connection string for RabbitMQ, allowing communication with the messaging broker

      - RABBITMQ_CONNECTION_STRING=amqp://myuser:mypassword@rabbitmq:5672/
      - 
      - PORT=3000
      - 
    # Ensures that RabbitMQ starts before the Order Service

    depends_on:

      - rabbitmq

   Definition for Product Service

  product-service:

    image: ahmedboudouh/product-service:latest 

    # Maps the container's port 3030 to port 3030 on the host machine

    ports:

      - "3030:3030"
      - 
    environment:

      # Connection string for RabbitMQ, allowing communication with the messaging broker

      - PORT=3030

   Definition for Store Front (Frontend Service)

  store-front:

    image: ahmedboudouh/store-front:latest

    # Maps the container's port 80 (HTTP) to port 80 on the host machine

    ports:

      - "80:80"
      - 
    # Environment variables for the Store Front Service

    environment:

      # URL to access the Order Service from within the Docker network

      - VUE_APP_ORDER_SERVICE_URL=http://order-service:3000
      - 
      # URL to access the Product Service from within the Docker network

      - VUE_APP_PRODUCT_SERVICE_URL=http://product-service:3030
      - 
    depends_on:

      - product-service
      - 
      - order-service
  

## 3. setup challenges & lessons learned:

      Problem: Port conflicts (80, 3000, 3030, 5672/15672) from leftover containers blocked my stack.

      Symptom: “Bind for 0.0.0.0:<port> failed: port is already allocated.”

      Lesson: Don’t chase each service one by one.

     Solution: Run docker compose down -v to stop/remove containers, network and volumes, then docker compose up -d --build. This resets everything cleanly and avoids port conflicts.