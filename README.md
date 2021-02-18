# Clouds
The purpose of the Clouds solution is to analyze cloud converage in satellite images.

This solution is developed as part of the course Computational Physics: Introductory Course at Malmö University in the spring 2021.

## Design overview
The Clouds solution use a staged approach where each stage is controlled by a specialized Orchestrator, and on top of everything there is another Orchestrator that control the specialized Orchestrators.
- Stage 1: Download images from soure on Internet
- Stage 2: Analyze images

The result from each stage is stored as files and can be retrieved for validation and analysis.

![High Level Design for the Clouds soluton](images/HighLevelDesign.png)

## Technologies
Technologies used in this solution are:
- Phyton 
- Azure Containers running Linux
- Azure Service Bus
- Azure Blob Storage 
- Powershell
- Matlab

## Detailed design
The Clouds solution uses containers to create a large number of simple Processor instances that are controlled by an Orchestrator instance. The Orchestrator use a queue to communicate with the Processors, this both provides a reliable delivery mechanism and an automatic load-balancing between the Processors.

![Detailed Design for the Clouds soluton](images/DetailedDesign.png)

