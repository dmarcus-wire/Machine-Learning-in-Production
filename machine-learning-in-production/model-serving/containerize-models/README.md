# Why Containers

1. ship your software with all of it's dependencies
2. run software without installing required interpreters or compilers for it to run

Example, 
- you created a virtual environment on your local machine
- you trained a Deep Learning model using Python with some libraries like Tensorflow
- everything works fine, now you want to share the model with a peer that a) doesn't have Python or b) uses a different version
- they are also missing the required libraries
- without containers, you peer would have to install all the software just to run the model
- with containers, your peer just needs a container engine

# Key concepts
1. Containerfile "the instructions required to build an image"
   1. A Containerfile is a mechanism to automate the building of container images. A Containerfile is a text file named either Containerfile or Dockerfile that contains the instructions needed to build the image.  Building an image from a Containerfile is a three-step process. 
      1. Create a working directory
      2. Write the Containerfile
      3. Build the image with Podman
2. Image "the collection of all your software in one single place"
   1. From the Linux kernel perspective, a container is a process with restrictions. 
   2. However, instead of running a single binary file, a container runs an image. 
   3. An image is a file-system bundle that contains all dependencies required to execute a process: files in the file system, installed packages, available resources, running processes, and kernel modules.
   4. Simply put, an image refers to the collection of all your software in one single place.
3. Container "This a running instance of an image."
   1. Applications can run inside containers, providing an isolated and controlled execution environment. 
   2. Running a containerized application, that is, running an application inside a container, requires 1) a Container Image and 2) a File System bundle that provides all the application files, libraries, and dependencies that the application needs to run. 
   3. Container images are available from image registries that allow users to search and retrieve container images.
4. Container Engines "execute the applications"
   1. Containers, images, and image registries need to be able to interact with each other. For example, you need to be able to build images and put them into image registries. You also need to be able to retrieve an image from the image registry and build a container from that image.
      1. Rocket 
      2. Drawbridge 
      3. LXC 
      4. Docker 
      5. Podman
         1. Podman is an open source tool for managing containers and container images and interacting with image registries.
         2. Podman is available in Red Hat Enterprise Linux 7.6 and later, and is used in this course to start, manage, and terminate individual containers.
5. Container Repositories
   1. Container images need to be locally available for the container runtime to execute them, but the images are usually stored and maintained in an image repository. An image repository is just a service - public or private - where images can be stored, searched and retrieved. 
      1. Red Hat Container Catalog
      2. Docker Hub
      3. Red Hat Quay 
      4. Google Container Registry 
      5. Amazon Elastic Container Registry
   