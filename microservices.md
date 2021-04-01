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
