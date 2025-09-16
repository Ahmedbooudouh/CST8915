# YouTube video link

https://youtu.be/EnYVbMD8Zm8



# Technical Explanation of Services

## Order Service (Node.js)
The Order Service is responsible for receiving orders from the store-front and pushing them to RabbitMQ so they can be queued for downstream processing. It exposes an HTTP POST endpoint at `/orders` on port 3000. The service uses Express to build the server and CORS to accept requests from the front end. When a request arrives, the order payload from the client is parsed as JSON and published to RabbitMQ (AMQP) into the order queue.

This service is written in Node.js with Express and the amqplib client for RabbitMQ. All required dependencies are declared in `package.json`. In short: HTTP in (REST, JSON) → RabbitMQ out (AMQP message), keeping the front end decoupled from the processing workflow.

## Product Service (Rust)
The Product Service is responsible for serving product data (id, name, price) to the store-front. It’s a small REST API built with Rust using the Warp framework, listening on port 3030. A GET request to `/products` returns a JSON array of product objects that the front end can display.

This service uses Warp filters and enables CORS so the Vue app can fetch the data from a different origin. Its job is simple and focused: provide the product list over HTTP in JSON format.

## Store Front (Vue.js)
The Store Front is a Vue.js app (HTML template + CSS styles + JavaScript script) that talks to the two back-end services. First, it fetches products with a GET to `http://localhost:3030/products` to display the catalog. Then, when the user places an order, it sends a POST to `http://localhost:3000/orders` with the selected product, quantity, and computed total—all as JSON.

So the front end reads from the Product Service (GET/JSON) and writes to the Order Service (POST/JSON). This clean separation keeps the UI simple while the back end and queue handle the heavy lifting.

## Notes on Setup Challenges and Learnings
1. Configuration and creation of VM with Linux OS and SSH for remote access.  
2. Configuration of SSH in VS Code to connect to the VM.  
3. Gained a better understanding of how APIs work.  
4. Learned the importance of using scripts to avoid repetition and save time.  
5. Noticed that each programming language has its unique environment and dependencies that need to be configured properly for the services to run.  
