# Google Cloud Platfom

## Google Compute Engine

Corporate data centres => deploy app in physical server 

To deploy app in cloud => Rent virtual machine

The main purpose of the GCE is to provision and manage virtual machine.

__Features:__
+ Create and manage the life cycle of the VM instance
+ Load balancing and auto scaling for multiple VM 
+ Attach storage and network storage to VM
+ Manage network connectivity and configuration for VMs
## Create a Virtual Machine
+ Go to cloud.google.com
+ click `console`
+ search Compute Engine
+ where you can see a pop VM instance click on `create`
+ fill the name and the below details.
+ then give create and you will find `SSH`where it will direct to command page.
### Installing HTTP webserver on GCE virtual machine
```
sudo su
apt update 
apt install apache2
ls /var/www/html
echo "Hello World!"
echo "Hello World!" > /var/www/html/index.html
echo $(hostname)
echo $(hostname -i)
echo "Hello World from $(hostname)"
echo "Hello World from $(hostname) $(hostname -i)"
echo "Hello world from $(hostname) $(hostname -i)" > /var/www/html/index.html
sudo service apache2 start
```
__Setting up HTTP webserver__
- `sudo su` to become a route user
- `apt update` used to update all the package
- to install the Http server give `apt install apache2`
- After installation if want to see the apache default page click on `External IP` 
- To customize the default page `/var/www/html` which can be found in the default page itself
- `echo "Hello World!" > /var/www/html/index.html` will allow you to display hello world instead of default page
- `echo $(hostname)` it prints the name of the VM instance
- `echo $(hostname -i)`gives out the internal ip address of the hostname
### IP address in virtual machine

|        Internal IP                  |           External IP          |
| ----------------------------------- | ------------------------------ |
| 1. permanent address                | 1. Not permanent address       |
| 2. IP address wont be changed       | 2. IP address will be changed  |
| 3. Used only inside the specific network | 3. Used on outside for communication purpose |
|                                          | 4. It remins ephemeral, if want external IP address not to change use static|
### Simplify VM HTTP server setup:

There are few options when it comes to reducing the steps in creating the VM instance and setting the HTTP server:
- Startup Script
- Instance Template
- Custom Image
#### Startup Script
```
#!/bin/bash
apt update 
apt -y install apache2
echo "Hello world from $(hostname) $(hostname -I)" > /var/www/html/index.html
```
- _Bootstrapping_: Install OS patches or software when an VM instance is launched
- the startup script which can be found in the creation of the VM instance.
#### Instance Template
- Each and every time details has to be filled to create the VM instance
- Instead we can use the Instance template
    - Used to create VM instance and manage instance which provides a convenient way to create similar instances
- Cannot be updated. If need to change, copy the existing template and modify it.
#### Custom Image
- Installing OS patches and software at launch of VM instances increases boot up time
- Create a custom image with OS patch for the already installed software (eg:apache)
   - It can be created from an instance, a disk, a snapshot, another image or file in cloud storage
- Can share an image with other projects.
