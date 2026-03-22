# Lab 7 Kubernetes Basics
## Todd O'Neil

### Links:
<a href="https://www.youtube.com/watch?v=XvCXIg3rLQs">Lab 7 video submission</a>

### Rabbit MQ Stateful vs Stateless
<p>
    The RabbitMQ configuration as it stands is a stateless application. The container itself is ephemeral and currently has no volumes attached to the container to ensure peristent data.  Once the container fails or is restarted all of the data in the queue is lost.
</p>

### Implications Of No Persistant Storage
<p>
    As mentions briefly above ths issue with having rabbitMQ not having peristent storage is all data currently not processed in the queue could be lost if a failure occurs or if the pob needs to be restarted for any reason. This would bbe unacceptable if it was reponsible for processing any kind of critical data such as payment information.
</p>

### Solutions
<p>
    A solution to the issue would be to define a volume in the container portion of the rabbitMQ deployment section of the yaml file.  Adding a volume to the container allows for persistnce of data even if a container is restarted, since each container points to the same location in memory that the volume was created in.
</p>

### Azure Service Bus
<p>
    ASB would be a good alternative for rabbitMQ.  We could remove the deployment and service all together from our yaml configuration file and just have the services that need it reference the ASB connection string.  ASB offers managed queues with geo-reducdancy in case of failures.
</p>