# Lab 3 Docker Containers And Docker Compose
## Todd O'Neil

### Links:
<p>
    This video submission is almost 7 min long.  I apoligize for going over time, however I was doing that section of the lab live. I did not complete the lab first and then record, so I made some typos in the commands, as well as reading each of the instructions while creating the video.
</p>
<a href="https://www.youtube.com/watch?v=EolVuNLGcyk">Lab 4 video submission</a>

### Docker Image vs Docker Container:
<p>
    A docker image is basically a blueprint on how to create a container. It is created with a dockerfile that lays out specific instructions as to runtimes, folder structure, commands that need to be run, and what files to use.  A docker container is the finished product that is built using a specific image. If a docker image is the blueprint to the house, the docker container is the house itself.
</p>

### Layered Architecture:
<p>
    Docker's layered architecture makes it so only changed layers need to be rebuilt. So if a dockerfile existed with 5 layers defined already and a 6th layer was added. As long as those previous 5 layers weren't changed they don't need to be rebuilt form scratch, they can just be copied over into a new image along with the new 6th layer. This allows for new images that contain many layers with minor changes to be spun up quickly.
</p>

### Writable Layers:
<p>
    Each container when created, gets its own writable layer. This allows for complete isolation when multiple containers are created from the same image. If this writable layer wasn't there, then each container would write to the already existing layer fundamentally changing the underlying structure. Which would break the immuability of container images. Containers are also meant to be disposable. So any write operations are meant to be temporary unless properly configured. Such as runtime variables (which can change anytime a container is started), or persistent volumes.
</p>

### Docker Compose:
<p>
    Docker compose is very helpful when needing to run multiple containers at once.  It allows you to start all containers associated with a particular application with one configuration file instead of having to start each one seperately.  It also allows you to manage dependencies by enforcing container start up order. So if a service relies on a database you could unsure that service doesn't start until the database container successfully started and is running.
</p>

### Notes:
<p>
    One thing this lab gave me a better grasp of is how the layered architecture works.  How when images are created from the same dockerfile after minimal changes those layers that were already built get copied instead of rebuilt.
</p>