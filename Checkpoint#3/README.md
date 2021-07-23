# Checkpoint #3

This is the entry point to modules within Terraform. Modules are just chunks of TF code that have their own configuration and are called into a root project. You can also string modules together as well if you wanted. The idea around modules is that you create a collection of components that are required for a specific requirement and store the configuration of those resources in a single module. You can then call that module from your project code and other projects as well...

Lets start small on our modules and create a simple module for the resource group. This module should expect input variables for the name, location, and tags. This module should output values for the name, location, tags and the resource id.

 - Build and use a single resource group module in your current project, replace the existing statis resource.

# Objective

 - Understand modules at a high level, we will expand on this in later checkpoints
 - Use your resource group module in your project

## Azure Resources:
 - Resource Group
 - Virtual Network
 - Subnets
 - Linux Virtual Machines
 - Public IP Address
 - Network Security Group

 ## Azure Refrence Architecture

 ![Architecture One](Diagram.png)