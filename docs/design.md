# Antfarm Design

## Scheduling of work
When an [Orchestrator](terminology.md#orchestrator) wants to get some work done it post tasks on a 
[Work Queue](terminology.md#work-queue).

The [Work Queue](terminology.md#work-queue) is unique for communication between the specific instance of 
[Orchestrator](terminology.md#orchestrator) node and the [Worker](terminology.md#worker) nodes is to perform the work.
Each [Worker](terminology.md#worker) node listen to only one [Work Queue](terminology.md#work-queue).

When a [Worker](terminology.md#worker) has completed its work it stores its result on [Storage](terminology.md#storage) and report back to the [Orchestrator](terminology.md#orchestrator) 
using a [Response Queue](terminology.md#response-queue).

## Load Balancing of Work between Nodes
The Antfarm framework uses many [Worker](terminology.md#worker) nodes that each will contribute to the work. A problem that can occur is that some nodes get harder tasks to execute and 
if tasks are evenly distributed between the nodes then some nodes will complete all their work while others still are executing, the idle nodes will  waste their resources while
they wait for all nodes to complete their work.

Therefore it is important that work is distributed based on availability of the nodes, not that all nodes execute the same number of tasks.

A simple solution to a load based distribution of work is to use a [Work Queue](terminology.md#work-queue) where all tasks are posted. When a [Worker](terminology.md#worker) node does
not have an active task it connect to the [Work Queue](terminology.md#work-queue) and read the first task, as it only can work on one task it only reads one task. This way there is 
never idle nodes unless all tasks has been processed.

## Fault Tolerance
Fault tolerance is not a priority for Antfarm at this point in time, but below are some thoughts on how to take advantage of fault tolerance in cloud technologies.

### Storage
To ensure that the [Storage](terminology.md#storage) used by an application does not run the risk of loosing any result for data processing it is a good idea to use a cloud based
storage mechanism, they provide automatic redundancy of storage to ensure no data is lost.

### Queuing Technology
A good implementation of [Work Queue](terminology.md#work-queue) is to use a persistent cloud-based queue mechanism with built-in retry mechanism, e.g. Azure Service Bus. These types of 
technologies ensure that once a message is posted to the queue it will not be lost, it is securely stored in the cloud and is not dependent on any single computer being online. 
They also often have mechanism that allow unprocessed messages to be processed by other nodes.

## Different ways to parallalize
Old style: Special hw like CM2 with 65000 processors
New style: Commodity hw

## Comparing with other frameworks

### MapReduce
The best know general framework of execution for parallelization is MapReduce, it is intended for really massive parallelization handling terabytes of data.
- MapReduce use a single master node to drive the execution, Antfarm use a hierarchy of Orchestrators.
- MapReduce use local disk on the worker nodes to store data used between stages (called intermediate files), Antfarm use persistent storage outside the worker nodes.

The reason for using persistent storage outside the worker nodes is that in a scientific applications the intermediate files are often relevant after calculations are completed.
As an example, when the [Clouds](clouds.md) application execute it download satellite images that may be reused in future re-executions of the application with an updated
analysis-algorithm or they may be used during visualization of results. 
