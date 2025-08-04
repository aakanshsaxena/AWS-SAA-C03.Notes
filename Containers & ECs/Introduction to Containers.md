
>[!note]- Post-Processing
>## Key Insights and Information from the Transcript:
>
>**1. Containers vs. Virtual Machines:**
>
>* **Containers** are lightweight, isolated environments that run within a host operating system. They share the host OS kernel but have their own file systems and resources.
>* **Virtual Machines** are isolated environments that run their own complete operating systems on top of a hypervisor. They are heavier and require more resources.
>
>**2. Benefits of Containers:**
>
>* **Density:** Containers can run many more applications on the same hardware compared to virtual machines.
>* **Resource Efficiency:** Containers consume fewer resources because they share the host OS kernel and don't need a full OS for each application.
>* **Portability:** Containers can be easily moved between different environments because they package the application and its dependencies together.
>* **Scalability:** Containerized applications can be easily scaled up or down as needed.
>
>**3. Docker and Docker Images:**
>
>* **Docker** is a popular container engine that allows you to create, manage, and run containers.
>* **Docker Images** are read-only templates that define the environment for a container. They are built in layers, with each layer containing incremental changes.
>* **Docker Hub** is a public registry for Docker images.
>
>**4. Container Architecture:**
>
>* A container is a running instance of a Docker image with an additional read-write layer for storing application data and changes.
>* Layers in a Docker image are read-only and contain incremental changes, allowing for efficient storage and reuse.
>* The read-write layer is unique to each container and allows for isolation and customization.
>
>**5. Use Cases:**
>
>* Containerization is widely used for deploying and managing applications in various environments, including cloud, on-premises, and edge computing.
>
>
>
>This transcript provides a good overview of container computing and its benefits. It highlights the key differences between containers and virtual machines, introduces Docker and Docker images, and explains the architecture of containers.
>

>[!note]- Post-Processing
>## Key Insights and Information from the Transcript:
>
>**What is a Container Registry?**
>
>* A container registry is a repository for storing container images.
>* Developers and architects use Dockerfiles to create images, which are then uploaded to registries like Docker Hub (public) or private registries.
>* Images can be shared and reused across different Docker hosts.
>
>**Docker Terminology:**
>
>* **Dockerfile:** Used to build Docker images.
>* **Docker image:** Multi-layered file system image used to run containers.
>* **Docker container:** A running instance of a Docker image.
>* **Docker host:** A server running a container engine (e.g., Docker).
>* **Docker Hub:** A public container registry operated by Docker.
>
>**Benefits of Containerization:**
>
>* **Portability:** Containers run consistently across different environments.
>* **Consistency:** Applications run as expected regardless of the underlying infrastructure.
>* **Lightweight:** Containers share the host OS kernel, reducing resource consumption.
>* **Density:** Multiple containers can run efficiently on a single host.
>* **Isolation:** Containers provide a degree of isolation from the host and other containers.
>
>**Key Concepts:**
>
>* **Layers:** Images are built in layers, allowing for sharing and reuse.
>* **Port Exposure:** Containers expose ports to allow external access to services.
>* **Multi-Container Architectures:** Complex applications can utilize multiple containers for scaling and functionality.
>
>**Overall:**
>
>The transcript emphasizes the core concepts of containerization with Docker, highlighting its benefits and key terminology. It stresses the portability, consistency, and efficiency of containers, making them a valuable tool for developers and architects.
>
>
>

- Normal virtualization has a host, and then a hypervisor, and then multiple "full" systems running on top of the hypervisor, each with its own OS
- The OS is memory and storage consumption heavy
Containerization
- Instead we can run a container engine, like Docker, on top of our OS and then run isolated containers on top of the container engine
- We can use something like a dockerfile to create Docker images. Each step creates file system layers, and these images contain readonly layers, changes are layered onto the image using a differential architecture.
- Each docker image can create docker containers which have their own unique read/write layer which separates them from other containers.
- The shared file system layers (in the docker image) make it even more efficient.
- Dockerfile/container image is stored on the Docker Hub/container registry and is run on viable Docker Hosts
Container Key Concepts
- Dockerfiles are used to build images
- Portable, self-contained, always run as expected, and lightweight (because parent OS is shared, and filesystem layers are shared)
- Container only runs the application and environment it needs
- Provides much of the isolation VM's do
- Ports are exposed to the host and beyond 
- Application stacks can be multiple containers



