# Terminology
Here you can find an explaination of the different terminology used in Antfarm. These terms are used throughout the documentation without further explaination.

## Node
A computer instance.

A node can either be used as an [Orchestrator](terminology.md#orchestrator) or as a [Worker](terminology.md#worker).

## Orchestrator
Responsible for distribution of work.

A solution may contain several different types of Orchestrators, each specialized in distribution of work to a single type of [Worker](terminology.md#worker) or [Orchestrator](terminology.md#orchestrator) node. 

When work is distributed to a [Orchestrator](terminology.md#orchestrator) node, it is always just a single node receiving the request. 
The design pattern is that the first [Orchestrator](terminology.md#orchestrator) node then drives a multi-stage process and the second [Orchestrator](terminology.md#orchestrator) node drives the execution of a single stage, using [Worker](terminology.md#worker) nodes execute the actual work.

The purpose of this design is that an [Orchestrator](terminology.md#orchestrator) node should be as simple as
possible: "Do one thing, and do it well!".

## Worker
Responsible for execution of work.

A solution may contain several different types of workers, each specialized in performing a single task. E.g., the reference implementation [Clouds](/clouds.md) has one worker responsible for downloading images and one worker for analysing the images.

## Storage
Location where results from a Worker is stored.

Storage can be files on a shared disk, in cloud storage, in a NoSQL database, or any other type of location where data
can be stored. A key characteristic of Storage is that all Storage is accessible by all Nodes in the AntFarm, i.e. 
local disk on a Worker is not considered to be Storage.

Storage hold all types of data that is used for input to a Worker or as output from a Worker.

## Transient Storage
Location where temporary data is stored, i.e. data which are only used locally within a specific Node.

## Work Queue
An ordered list of tasks that are to be executed.

A Work Queue is used by an Orchestrator to publish task that needs to be execute to Workers.
Communication from up-stream Orchestrators to assign tasks to down-stream Orchestrators also uses a Work Queue.

Each Work Queue is used for communication between a specific [Orchestrator](terminology.md#orchestrator) and a specific type of [Workers](terminology.md#worker), the direction of
communication is from [Orchestrator](terminology.md#orchestrator) to [Worker](terminology.md#worker).

## Response Queue
An ordered list of execution results.

A Response Queue is used by Workers to communicate the result of an execution back to the Orchestrator.
Communication from down-stream Orchestrators to report back status to up-stream Orchestrators also uses a Response Queue.

Each Response Queue is used for communication between a specific [Orchestrator](terminology.md#orchestrator) and a specific type of [Workers](terminology.md#worker), the direction of
communication is from [Worker](terminology.md#worker) to [Orchestrator](terminology.md#orchestrator).

## Pipeline
An ordered sequence of steps to solve a computational problem using Antfarm.

The minimal pipeline possible is a single [Orchestrator](terminology.md#orchestrator) node that distribute work to 
[Worker](terminology.md#worker) nodes.

But it may also be several layers of meta-[Orchestrator](terminology.md#orchestrator) nodes that drive a larger process that involve many different types of [Worker](terminology.md#worker) nodes.