# Checkpoint #5

Now that we have a load balancer... Lets add a second web server. Create a module for your web server and create a module for an availability set as well. Use the module to create 2 machines using the count operator vs. copying-pasting the machine config twice.

Replace the Terraform provisioner with the VM Extension option. This will be used and is a better use-case for Azure than allowing Terraform to communicate with the machines directly.

# Objective

 - Convert your webserver to a module. Include all the required components for configuring a webserver in the module.
 - Use a web_server_count variable to create two VMs - test with changing that to 3 or 4 or 1.
 - Make sure the VMs get added to the backend pool
 - Update the NGINX config so you know which server you're connecting to... Use a script to update the homepage to reflect the hostname? - dont burn a ton of time on this, let me know if you want the commands!

## Azure Resources:
 - Resource Group
 - Virtual Network
 - Subnets
 - Linux Virtual Machines
 - Public IP Address
 - Network Security Group
 - Azure Bastion Service
 - Azure Load Balancer
 - Web Servers
 - Availability Set

 ## Azure Refrence Architecture

 ![Architecture One](Diagram.png)