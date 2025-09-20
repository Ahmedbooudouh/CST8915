1. Demo video link: https://youtu.be/NDNl4JY5kkk?si=ogkBhDxu3XVy7ZwH

2. Reflection Questions

a) What changes did you make to the order-service and product-service to comply with the Configurations and Backing Services factors

I removed hard-coded settings from the code and put them into environment variables using a .env file. For example, instead of writing the RabbitMQ connection string or the service port directly in the code, I stored them as variables like PORT and RABBITMQ_URL. This way, the services can connect to RabbitMQ (our backing service) through values that can change without editing code.

b) Why use environment variables instead of hard-coding configurations

Environment variables make the app flexible and portable. If we change a port number or a RabbitMQ URL, we just update the variable without touching the code. This keeps the code the same in all environments (development, test, production) and avoids problems with secrets or connection details being exposed in the source.

c) Why have separate repositories for each microservice How does this help independence and scalability

Each microservice has its own repository so it can be developed, updated, and deployed on its own. This means changes in one service don’t break the others, and we can scale only the service that needs more resources. It also makes it easier to manage updates and keep the code for each service clean and independent.