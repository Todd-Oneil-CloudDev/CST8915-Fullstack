# Lab 2 - Microservices

## Todd O'Neil

[Lab 2 - Microservices: demonstration](https://www.youtube.com/watch?v=Tkgwpkwjzjg)
<br>

[Order-Service Repository](https://github.com/Todd-Oneil-CloudDev/CST8915-order-service)
<br>

[Product-Service Repository](https://github.com/Todd-Oneil-CloudDev/CST8915-product-service)
<br>

[Store-Front Repository](https://github.com/Todd-Oneil-CloudDev/CST8915-store-front)

### Question 1: product and order service 12-Factor compliance changes:
<p>
    To bring each backend service into compliance with the 12-Factor methodology, specifically the points 3 (Configurations) and 4 (Backing Services). 
</p>
<p>
For the order-service I created a .env file that will house important configuration variables such as port numbers and connection strings. That way if changes need to be made at runtime or compile time they only need to be changed in 1 place. By extracting out the connection string into a .env file that also complies with point 4 (backing services) of the 12-Factor methodologies. The order-service doesn't care what backing service that connection sting belongs to and is effectively decoupled from it.  The rabbitMQ service that the order-service uses could be swapped out for another such as Kafka and order-service would be none the wiser.
</p>
<p>
    For the product-service the same changes as the order service were made. The differences however are, the product-service doesn't use a backing service.  I also needed to add the dotenv with the version I wished to use to the Cargo.toml file.  That ensure what when the service was built it would pull in the dotenv dependency that would allow the service to extract information from the .env file.
</p>

### Question 2: Importance of environment variables:
<p>
    Environment variables are important because it allows for felxibility in deployments. If your connection strings, ports, or other information that can vary are hardcoded into the code base then if you wanted to create different environments such as DEV, TST and PRD. You would need a different codebase for each one. Where if you have environment variables in place of hardcoded variables, you can easily deploy multiple versions of the same codebase but with differing factors ie. ports, connection strings, secrets, etc.
</p>

### Question 3: Seperate Repositories:
<p>
    For a microservice application having a seperate repository to store the codebase for each service is crusial. It allows each service to be deployed, editted, debugged, etc without impacting the rest of the application. It also allows for each service to be scaled up or down independantly. If the order-service is seeing a 500% increase in traffic that service on it's own can be duplicated and scaled up without have to increase capacity of every other aspect of the application.
</p>

## Notes
<p>
    I found the .env.production in the store-front to be a bit challenging. I was able to build it out with npm run build. After that however I ran into trouble running the production distribution server. I needed to enlist the help of Copilot to give me a bit of direction, which pointed me to running:
    <ol>
        <li>sudo npm install -g serve</li>
        <li>serve -s dist -l 8080</li>
    </ol>
    1. installed a static file serve.
    <br>
    2. served the distribution on port 8080.
    <br>
    Since my experience with deploying productoin build is very limited I really enjoyed learning that aspect of the assignment.
</p>