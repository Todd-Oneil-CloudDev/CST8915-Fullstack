# CST8915 Lab 1: Algonquin Pet Store on Azure VM

**Student Name**: Todd O'Neil
**Student ID**: 040573645
**Course**: CST8915 Full-stack Cloud-native Development
**Semester**: Winter 2026

---

## Demo Video

🎥 [Watch Demo Video](https://www.youtube.com/watch?v=003MWhN0t6g)

---

## Technical Explanations

### Order Service (Node.js)

This service is responsible for taking in data sent from the Store Front service as an http request. It processes the data and then in turn publishes a message to the RabbitMQ service It's role in the architecure is to receive order data from the frontend process that data and send it to a message broker.

If the message was sussessfully sent to the RabbitMQ service an http response is sent back to the Store Front service with a body of "Order Received". If there was a communication error between Order service and the RabbitMQ service then an http response declaring the error is sent  in the body back to Store Front instead.

This service uses Javascript with AMQP, CORS and EXPRESS as dependencies. AMQP allows for communication with a message broker such as RabbitMQ, CORS allows browser applications running on different origins (protocol, domain, or port) to make requests to this service when explicitly permitted by the server, and EXPRESS is the most common backend developlemt library for Javascript.

### Product Service (Rust)

This service has a simpler, yet still important role within the architecture.  It is responsible for sending what products are available for users to buy to the Store Front service via http response. If there is a communication failure users will not be able to order any products.

This service uses RUST as the application language. It's known for being a fast as C++ and can be used for services that require fast processing times. It utilizes CORS for the same reason the Order service does, without it the Store Front's web browser application would not be able to make call into this service.

### Store Front (Vue.js)

This store front service is the front facing application that users interact with. It communicates with both the Order service and the Products service via http requests.

When the application loads an http GET request is sent to the Products service to retreive all available products.
Users can click on a prodect they wish to place an order for and how many of that item they would like and the Store Front service then calculate how much it was cost the user based on item price and quantity. That information is then sent via http POST request to the Order service.

This service is written in Javascript, specifically the Vue.js frontend framework. It allows for self contained reusable components that include all logic, styling, and html to be constructed and used throughout an application.

---

## Acknowledgments

MS Copilot -> explaining port forwarding and why I was able to still reach the web application site from my local machine when my local machine wasn't running any local server and didn't even have the code stored on it.
