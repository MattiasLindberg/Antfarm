# Antfarm Framework Implementation

## Python
The reference implementation of Antfarm is built using Python. The language was choose because it is a very popular language in general
(see [Stackoverflow Developer Survey 2020](https://insights.stackoverflow.com/survey/2020#technology-programming-scripting-and-markup-languages-professional-developers)) 
and that it has many libraries available that are useful for solving problems in physics.

## Dependency Injection
The code uses depedency injection to minimize the need to change the framework code, the user should focus his work on implementing
the orchestration and work code that is unique to his solution. 

A key feature of the reference implementation is usage of dependency injection, this enable a user of the framework to inject the code unique to their solution while still reusing the generic 
code for [Orchestrators](terminology.md#orchestrator) and [Workers](terminology.md#worker). 

The [python-dependency-injection](https://pypi.org/project/python-dependency-injection/) framework is used to support dependency injection.

## Worker and Return Queue
The implementation of [Work Queue](terminology.md#work-queue) and [Result Queue](terminology.md#result-queue) will use 
[Azure Service Bus](https://docs.microsoft.com/en-us/azure/service-bus-messaging/service-bus-messaging-overview). It provides persistent storage, ordered delivery, retry mechanism and more.

Each queue in the [Pipeline](terminology.md#pipeline) will be represented as a [Topic](https://docs.microsoft.com/en-us/azure/service-bus-messaging/service-bus-queues-topics-subscriptions#topics-and-subscriptions) in an Azure Service Bus.
 
When a [Orchestrators](terminology.md#orchestrator) or [Workers](terminology.md#worker) node is created it will have to be initated with connection string to the queus it is going to work with.

## Storage
The implementation of [Storage](terminology.md#storage) will use [Azure Blob Storage](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction). A single Blob Storage will be created and a [Container](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction#containers) will be used to represent a specific [Storage](terminology.md#storage) instance.