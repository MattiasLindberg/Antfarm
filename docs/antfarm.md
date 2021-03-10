# AntFarm - A framework for parallell execution of tasks
AntFarm is a general purpose framework intended to support parallell execution of tasks. 
It is a design pattern with reusable components, and there is also a reference implementation to show how it can be used.

## Terminology

### Node
A computer instance.

A node can either be used as an [Orchestrator](/antfarm.md#orchestrator) or as a [Worker](/antfarm.md#worker).

### Orchestrator
Responsible for distribution of work.

A solution may contain several different types of Orchestrators, each specialized in distribution of work to a single type of [Worker](/antfarm.md#worker) node.

### Worker
Responsible for execution of work.

A solution may contain several different types of workers, each specialized in performing a single task. E.g., the reference implementation [Clouds](/clouds.md) has one worker responsible for downloading images and one worker for analysing the images.

### Storage
Location where results from a Worker is stored.

Storage can be files on a shared disk, in cloud storage, in a NoSQL database, or any other type of location where data
can be stored. A key characteristic of Storage is that all Storage is accessible by all Nodes in the AntFarm, i.e. 
local disk on a Worker is not considered to be Storage.

Storage hold all types of data that is used for input to a Worker or as output from a Worker.

### Transient Storage
Location where temporary data is stored, i.e. data which are only used locally within a specific Node.

### Work Queue
An ordered list of tasks that are to be executed.

A Work Queue is used by an Orchestrator to publish task that needs to be execute to Workers.
Communication from up-stream Orchestrators to assign tasks to down-stream Orchestrators also uses a Work Queue.

Each Work Queue is used for communication between a specific [Orchestrator](/antfarm.md#orchestrator) and a specific type of [Workers](/antfarm.md#worker), the direction of
communication is from [Orchestrator](/antfarm.md#orchestrator) to [Worker](/antfarm.md#worker).

### Report Queue
An ordered list of execution reports.

A Report Queue is used by Workers to communicate the result of an execution back to the Orchestrator.
Communication from down-stream Orchestrators to report back status to up-stream Orchestrators also uses a Report Queue.

Each Report Queue is used for communication between a specific [Orchestrator](/antfarm.md#orchestrator) and a specific type of [Workers](/antfarm.md#worker), the direction of
communication is from [Worker](/antfarm.md#worker) to [Orchestrator](/antfarm.md#orchestrator).

## Scheduling of work

## Fault Tolerance

### Hardware failures

### Software issues


## Different ways to parallalize
Old style: Special hw like CM2 with 65000 processors
New style: Commodity hw