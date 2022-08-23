# Terrachallange

This is a challnage to test your knowledge of Terraform and supporting Terraform in various environments. There is a series of requirements which must be met to confirm your skill in particular areas. This challenge touches on the most common items required to be proficient in Terraform.

## Getting Started

Get started by creating a repo in your personal github account. Make sure the project is public - make sure you do not store credentials in the repo ;)

Consider using a readme.md file in your repo for your notes, works in progres, etc. to track your own progress on the project.

I suggest using VSCode as your editor. There is no requirement to use this for Terraform or Azure, however, its free and has a lot fo support around opensource projects.

You will need to install Terraform locally.
https://learn.hashicorp.com/tutorials/terraform/install-cli

You will need Git locally as well:
https://git-scm.com/download/win

Learn the basics of using git. commits, branches, merge requests, merge conflicts, rebase, switching between branches, etc.

Get started by understanding what IaC is, not just Terraform. Terraform is a IaC tool, its not IaC...

https://medium.com/workfall/how-to-manage-infrastructure-as-code-iac-with-terraform-on-aws-1fa6cd6bccfe
Let me know if you find something else that helps you pick up on the concepts

Get to know Terraform!
Here is the documentation for Terraform:
https://www.terraform.io/docs/cli/index.html
Focus on the CLI features (init, plan, apply, destroy, validate, fmt, etc.)

## Getting Setup

Spend some time getting everything configured that you will need for this challenge. This would include setting up your editor, installing Terraform, and get access to an Azure environment (for most of this, you can use your MPN account). To start, you will work from you local machine, which will make the inital setup much easier.

> To complete this setup, make sure you have everything ready to go and you can execute the terraform init command to ensure everything is connected to Azure correctly.

## Inital Resources

This project will continue to build upon itself. This is the beginning to make sure we have everything we need to build the complex components later.

> Use TF to build and deploy an Azure Resource Group in the East US region with the following naming standard "rg-tftraining-tpeterson", replace the tpeterson w/ your first inital and last name. To complete this task, commit to your public GitHub account w/ a commit message of "inital commit". Confirm that once you run the TF commands to build the RG that you see the RG in the correct subscription.

## Variables

Variables are important in TF allowing the code to dynmaic based on the requirements of the environment. There are multiple ways to pass vairables to Terraform for use within your project. Lets confirm a few ways of using variables. Spend the time to become fimilar with the different types of variables including lists, maps, strings, numbers, etc. Truly understand where each of these variables can be used and how to structure variables correctly. Make sure you understand when and where different variable types should be used, Ie, command line, tfvars, auto.tfvars, or inline.

> Provide examples of the following variable usage
* Provide a variable in code and use the default value option. This can be used for the location.
* Use auto.tfvars to update the name of the resource group.
* Use terraform.tfvars to manage a password variable.
* Pass a variable via the command line.
> When done, commit to your github repo with a commit message of "variables".

## Full deployment

This full deployment will require some additional resources which will be used throughout this challenge. Create the following resources which will be used to test your TF skill. Keep in mind, I did not provide an exhustive list intentionally, as some troubleshooting and additional resources may be required, just like in a live environment.

* Virtual machine - either windows or ubuntu, ideally, ubuntu
* Standard Load Balancer - make sure the VM is added to the backend pool
* vNet and subnets -  single vNet with two subnets, web and lb
* Key vault - used to store the virtual machine password
* VM Extension - used to configure the web server

> Deploy the required resources to get a simple web sever working behind a load balancers. If you're deploying ubuntu, you can use `sudo apt-get update && sudo apt-get upgrade -y && sudo apt-get install nginx -y` to install nginx which will provide a simple website which can be used for testing. The end result would be that when you hit the standard load balancer, you're able to access the website. Commit this to your github using a commit message of "full deployment".

## Using count and other functions

Much like other programming and scripting languages, Terraform provides functions which can be used to augment the code and make it more dynamic. This section will require you to dig in and find use-cases for some of these functions.

> Use a number variable to dynamicly create x number of virtual machines. For example, set the variable equal to 2 and you should end up with two virtual machines. Update the variable to 3 and make sure you have 3 virtual machines. This should include all the additional confguration required including adding the VMs to the LB backend pool. When complete, commit your code using "count".

## Looping

Sometimes, rather than count, you will need to use a loop of for_each statement. These can be used to pass additional information and also can be used in resources which do not currently support their own resource. 

> Create a variable that is a list of objects which will become your new virtual machine list. Provide some additional information in this list to change the sku of some vms. For example, provide the information to create two VMs, one VM should use a b-series sku and the other should use a d-series sku. The end result is that you have two web server VMs created for the list of objects variable.

## Modules

Modules are very important in Terraform code. Essentially, a module is a small collection of resources. Simply put, a module could be created for the virtual machine allowing subsequent VMs to be configured the same as other VMs. This VM module may contain the virutal machine, the network interface, any required disks, monitoring details, etc. to properlly configure a VM for this project.

> Create two modules which can be re-used during the entire project. Create a module for the resource group and the virtual machine. Move all the resources associated with each to their respective module and then use module calls to deploy those resources. Make sure you using variables in your modules to pass parameters to the module dynamically. The end result is that everything is deployed and working with your module calls vs. hard coded resources in the code.

## Remote Backend

Up until this point, the TF State was being managed locally, this is fine when working solo or on a small project, however, once you need to work on the same project with someone else, you begin to have issues managing the state. There are plenty of additional benefits to use a remote backend including backups or versioning of your state and more.

> Convert your project to use remote state for its backend. Ideally, use an Azure Storage Account w/ blob storage. Setup your project to store the state in the storage account and then run all the commands locally to validate. This will likely require you to destroy your existing setup unless you upload your current tfstate file to the storage account.

## Deploy multiple environments

One advantage of Terraform is that it can be used to reproduce environments by just changing or pointing to a different set of variables.

> Create a second set of auto.tfvars to a second envionemt. This environment should be deployed to North Central US. You should be able to deploy and manage each environment seperately using different variables for each environment. For example. change the number of VMs being created in the first env and then re-run TF to make sure you're able to update the previous env. Both environments should have their state files in the storage account.

## Outputs

Outputs are used to link Terraform to other processes within IaC. Template files allow you to update values based on information from the project.

> Create an output with the load balancer's public IP address, username of the VM(s), password for the VM(s), and the location of the resource group. This should be a template that gets called provide a structured output when needed.