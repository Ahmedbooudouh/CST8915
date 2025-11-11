## Demo Video link: 
https://youtu.be/xnClQmz8ftg

## RabbitMQ Configuration Analysis: 
RabbitMQ is stateful and requires persistent storage for messages and queues. The current problem of using a Deployment without persistence causes complete data loss when pods restart after deletion or failure. The immediate solution is switching to StatefulSet with persistent volumes so messages survive restarts, though a better alternative is using Azure Service Bus since it's fully managed, automatically persistent, highly available, and solves all RabbitMQ's configuration issues with zero maintenance required.