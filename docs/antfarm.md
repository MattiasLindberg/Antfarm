# Antfarm - A framework for parallell execution of tasks
Antfarm is a general purpose framework intended to support parallell execution of tasks. 
It is a design pattern with reusable components, and there is also a reference implementation to show how it can be used.

Antfarm is my first attempt at this type of framework and the guiding priciples has been "reduce the problem" and KISS.

Antfarm is NOT intended to be a multi-threaded, GPU-aware, shared-memory and storage optimized framework.

## Terminology and definitions
See [Terminology](terminology.md) to learn about the terminology used in Artfarm.

## Processing pattern
In the Antfarm framework everything starts with the first [Orchestrator](terminology.md#orchestrator) in the pipeline.

## Scheduling of work
When an [Orchestrator](terminology.md#orchestrator) wants to get some work done it post tasks on a 
[Work Queue](terminology.md#work-queue).

The [Work Queue](terminology.md#work-queue) is unique for communication between the specific instance of 
[Orchestrator](terminology.md#orchestrator) node and the [Worker](terminology.md#worker) nodes is to perform the work.
Each [Worker](terminology.md#worker) node listen to only one [Work Queue](terminology.md#work-queue).

When a [Worker](terminology.md#worker) has completed its work it stores its result on [Storage](terminology.md#storage) and report back to the [Orchestrator](terminology.md#orchestrator) 
using a [Report Queue](terminology.md#report-queue).

## Fault Tolerance
Fault tolerance is not a priority for Antfarm at this point in time, it is still under development.

### Hardware failures

### Software issues

## Reference implementation
The reference implementation of the Antfarm framework is done in Python and the target environment is Linux containers running in Azure Container Instances.

A key feature of the reference implementation is usage of dependency injection, this enable a user of the framework to inject the code unique to their solution while still reusing the generic 
code for [Orchestrators](terminology.md#orchestrator) and [Workers](terminology.md#worker). 

More details see [Antfarm Framework Implementation](fx-implementation.md).

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
