# Antfarm - A framework for parallell execution of tasks
Antfarm is a general purpose framework intended to support parallell execution of tasks. 
It is a design pattern with reusable components, and there is also a reference implementation to show how it can be used.

Antfarm is my first attempt at this type of framework and the guiding priciples has been "reduce the problem" and KISS.

Antfarm is NOT intended to be a multi-threaded, GPU-aware, shared-memory and storage optimized framework.

## Overview of the  Design Pattern
In the Antfarm framework everything starts with the first [Orchestrator](terminology.md#orchestrator) in the pipeline.

## Terminology and Definitions
See [Terminology](terminology.md) to learn about the terminology used in Artfarm.

## Design of Antfarm
To learn about the design of Antfarm please see [Antfarm Design](design.md).

## Reference Implementation
The reference implementation of the Antfarm framework is done in Python and the target environment is Linux containers running in Azure Container Instances.

More details are available at [Antfarm Framework Implementation](fx-implementation.md).

## Validating the Reference Implementation
To validate the reference implementation a very simple application will be created that show how to plugin an application into the reference implementation.
