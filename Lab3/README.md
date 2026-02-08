# Lab 3 Microservices Via Azure App Service / Static Web App
## Todd O'Neil

### Links:
<ul>
<li><a href="https://www.youtube.com/watch?v=tsdzHEqIhMA">Lab 3 video submission</a></li>
<li><a href="https://github.com/Todd-Oneil-CloudDev/CST8915-order-service">Order Service</a></li>
<li><a href="https://github.com/Todd-Oneil-CloudDev/CST8915-product-service-python">Product Service</a></li>
<li><a href="https://github.com/Todd-Oneil-CloudDev/CST8915-store-front">Store Front</a></li>
</ul>

### Challenges:
<p>
    The most common issue I ran into when configuring environment variables, or even just the initial deployment was running the action too close together with a management action on the Azure platform.  Executing a Github Action shortly after making some sort of management change from the Azure Portal would cause the action to fail and it wold need to be re-run.
</p>

### Differences:
<p>
    Deploying the services from App Service is much easier. It has very straight forward inputs for Github repos, as well as a built in section for environment variables that can automatically be injected into your runtime. There is no need for a .env file in the repo as Azure handles it automatically, you just need to declare and instantiate them.
</p>

### Environment Variables:
<p>
    Using environment variables, especially in a cloud environment, make it far simpler when redeploying an application. For example after deploying something in App Service. if a code change was made because a dependency changed and no environment variables were set the application might deploy fine but overall it wouldn't work.  If an environment variable was used, you could still deploy and would just need to change the value of that variable in a single place and it would be injected at runtime.
</p>