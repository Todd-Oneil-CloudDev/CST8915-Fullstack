# Lab 5 Containerizing the Pet Store App and Docker Compose
## Todd O'Neil

### Links:
<a href="https://www.youtube.com/watch?v=a2r0UnMn-9k">Lab 5 video submission</a>

### Docker-Compose.yml File
 

    services:
    # Definition for RabbitMQ service
    rabbitmq:
    # Uses the RabbitMQ Docker image with the management plugin enabled
        image: "rabbitmq:3-management"
        # Maps the container's internal RabbitMQ ports to the host machine
        ports:
            - "5672:5672"   # Default RabbitMQ port (for messaging)
            - "15672:15672" # Management plugin UI port (for monitoring and managing)
        # Environment variables for default user credentials for RabbitMQ
        environment:
            - RABBITMQ_DEFAULT_USER=myuser      # Sets the default RabbitMQ username
            - RABBITMQ_DEFAULT_PASS=mypassword  # Sets the default RabbitMQ password
        healthcheck: 
            test: ["CMD", "rabbitmq-diagnostics", "ping"] 
            interval: 5s 
            timeout: 5s 
            retries: 10

    # Definition for Order Service
    order-service:
        # Builds the Docker image for order-service using the local directory
        image: clouddevac/order-service:latest
        # Maps the container's port 3000 to port 3000 on the host machine
        ports:
            - "3000:3000"
        # Environment variables for the Order Service
        environment:
            # Connection string for RabbitMQ, allowing communication with the messaging broker
            RABBITMQ_CONNECTION_STRING=amqp://myuser:mypassword@rabbitmq:5672/
            PORT=3000
        # Ensures that RabbitMQ starts before the Order Service
        depends_on:
            rabbitmq:
                condition: service_healthy 

    # Definition for Product Service
    product-service:
        # Builds the Docker image for product-service using the local directory
        image: clouddevac/product-service:latest
        # Maps the container's port 3030 to port 3030 on the host machine
        ports:
            - "3030:3030"
        environment:
        # Connection string for RabbitMQ, allowing communication with the messaging broker
            - PORT=3030

    # Definition for Store Front (Frontend Service)
    store-front:
        # Builds the Docker image for store-front using the local directory
        image: clouddevac/store-front:latest
        # Maps the container's port 80 (HTTP) to port 80 on the host machine
        ports:
            - "80:80"
        # Environment variables for the Store Front Service
        environment:
        # URL to access the Order Service from within the Docker network
            - VUE_APP_ORDER_SERVICE_URL=http://order-service:3000
        # URL to access the Product Service from within the Docker network
            - VUE_APP_PRODUCT_SERVICE_URL=http://product-service:3030
        depends_on:
            - product-service
            - order-service`


### Notes & Lessons Learned
<p>
    I noticed when running the docker compose command that even though the order-service depended on the rabbitmq service. The order service would still be created first.  I googled a solution and discovered that the "depends_on" criteria only checks if the container was successfully created or not, not if the application was running.
</p>
<p>
by adding: 

    healthcheck: 
            test: ["CMD", "rabbitmq-diagnostics", "ping"] 
            interval: 5s 
            timeout: 5s 
            retries: 10
to the rabbitmq service, and adding:

    depends_on:
            rabbitmq:
                condition: service_healthy
to the order-service, that ensured that the order-service would not be created until rabbitmq responsed to the ping sent from the docker engine singlaing that rabbitmq was actually running.
</p>