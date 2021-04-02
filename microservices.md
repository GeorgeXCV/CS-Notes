# Microservices 
Microservices are independently deployable modules.

For example, an e-commerce system can be divided into modules for:
* ordering
* registration
* product search

When the modules are implemented as microservices, the ordering process cannot only be changed independently of the other modules, but it can even be brought into production independently.

This speeds up deployment and reduces the number of necessary tests since only a single module needs to be deployed. Due to this greater level of decoupling, a large project can turn into a number of smaller projects. Each project is in charge of an individual microservice.

To achieve this at the technical level, every microservice has to be an independent process. A better solution for decoupling microservices is to provide an independent virtual machine or Docker container for each microservice.

Advantages:
* It is very compact.

* It is very general and covers all kinds of systems which are commonly denoted as microservices.

* The definition is based on modules and is thus a well-understood concept. This allows us to adopt many ideas concerning modularization. This definition also highlights that microservices are part of a larger system and cannot function entirely on their own. Microservices have to be integrated with other microservices.

* The independent deployment is a feature that creates numerous advantages and is therefore very important. Thus, the definition, in spite of its brevity, explains what the most essential feature of a microservice really is.

The above definition of microservices does not say anything about the size of a microservice. Of course, the term microservice suggests that especially small services are meant. However, in practice, microservices can vary hugely in size. Some microservices keep an entire team busy, while others comprise only a few hundred lines of code. Thus, the size of microservices is ill-suited to be part of the definition.

Microservices substantially increase the number of deployable units compared to a deployment monolith. This is only feasible when the deployment processes are automated.

Each microservice can be independently scaled. It is possible to start additional instances of a microservice and distribute the load of the microservice into the instances. This can improve the scalability of a system significantly.

They are isolated in respect to failures, which improves robustness.

The employed technologies can be chosen for each microservice in isolation, which allows for free technology choice.

## Micro and Macro Architecture
The micro architecture comprises all decisions that can be made individually for each microservice.

The macro architecture consists of all decisions that can be made at a global level and apply to all microservices.

Programming languages, frameworks, and infrastructure can be defined for each microservice individually at the micro architecture.
* Then each microservice can also be implemented with a different language.
* Technology, such as the application server, that best suits the specific problems of each microservice can be used.

Programming languages, frameworks, and infrastructure can be defined uniformly for all microservices in the macro architecture. This is useful if:
* a company’s technology strategy allows only certain technologies* 
* therefore, only developers with knowledge in certain technologies are hired

## Docker
Microservices must be scalable independently of each other. In the event of a crash, a microservice must not be allowed to make other microservices unavailable, too, and thus endanger the robustness of the whole system. Therefore, microservices must at least be separate processes.

Virtual machines require a lot of resources. Docker represents a lightweight alternative to virtualization. Although Docker does not provide as much isolation as a virtualization, it is practically as lightweight as a process.

Docker containers share the kernel of the operating system on the Docker host. The Docker host is the system on which the Docker containers run. The processes from the containers, therefore, appear in the process table of the operating system on which the Docker containers are running.

Ultimately, Docker containers are highly isolated processes due to their own network interface and file system.

Therefore, only one process should run in a Docker container. Running more than one process in a Docker container contradicts the idea of separating processes by means of Docker containers. Because only one process is supposed to run in a Docker container, there should be no background services or daemons in Docker containers.

File systems of Docker containers can be exported as Docker images. These images can be passed on as files or stored in a Docker registry.

The creation of Docker images is done via files named Dockerfile. One of Docker’s strengths is that Dockerfiles are easy to write and therefore, the rolling out of software can be automated without any problems.

### Docker Compose
A typical microservice system contains more than a single Docker container.

It would be good to have a way to start and run several containers together for starting all the modules that the system consists of in one go. This can be done with Docker Compose.

In a Docker Compose environment, a service can simply contact another service via a Docker Compose link and then use the service name as the hostname. So it could use a URL like http://order/ to contact the order microservice.

Docker Compose links offer some kind of service discovery, that is, a way for microservices to find other microservices. Synchronous microservices require a form of service discovery.

Docker Compose links extend Docker links. Docker links only allow communication. Docker Compose links also implement load balancing and set the start order so that the dependent Docker containers start first.

Docker Compose configures the interaction of the Docker containers with a YAML configuration file docker-compose.yml.
