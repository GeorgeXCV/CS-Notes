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
