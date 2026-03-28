# Lab8 Persistent Volumes and .YAML Files
## Todd O'Neil

### Links
<a href="https://www.youtube.com/watch?v=rRrht5EeIWk">Lab 8 Video Submission</a>

### Azure managed services for MongoDB
<p>
    The first service that comes to mind to replace a self-hosted mongodb instance would be CosmoDB.  It would make configuration of the aps-all-in-one.yaml file much simpler by eliminating the need for a deployment and service description entirely.  The makeline-service could use the connection string a an ENV variable directly without needing to worry about if a the database no is healthy or not.  It also can provide much more complex redundecy such as geographically redundent storage and zone redundancy.  On top of that since it's managed security patching and updates are automatically taken care of, and setting up backups and DR is much simpler.
</p>

### Azure managed services for RabbitMQ
<p>
    Azure Event Bus is the obvious choice to replace rabbitMQ with.  It can handle millions of messages per second, as well as makes configuring more advanced features simpler such as dead letter queues, automatic retries, message caching, etc. Switching to a managed service also simplfies the aps-all-in-one.yaml file as it eliminates another deployment and service description.
</p>