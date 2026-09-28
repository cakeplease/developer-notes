Created time: 14:42 10-09-2026

## IP addresses

**Internal IP** - permanent internal IP address that does not change during the lifetime of an instance
**External ephemeral IP address** - temporary external IP address (accesible from internet) that might change when an instance is stopped or restarted
**External static IP address** - permanent external IP address that can be attached to a VM

VPC network -> IP addresses -> promote to static IP address

You pay more when reserved static external IP address is not assigned to a VM!

## Bootstrapping with Startup Script

Automatically install software when VM first starts up

Startup Script: VM config to perform automatic bootstrapping. Increasing launch time

Create VM 
	- Networking: allow http 
	- Advanced -> automation:
	
#!/bin/bash
apt update 
apt -y install apache2
echo "Hello world from $(hostname) $(hostname -I)" > /var/www/html/index.html


## Custom image
To reduce the launch time, create a **custom image** with everything pre-installed. It can be built from an existing VM, disk, snapshot or cloud storage file.

### Best practices

- When your image gets outdated -> deprecate it and specify replacement
- Harden images to meet your organization's security
- Prefer using custom image to start-up script

Custom images make VM creation faster while being secure and reliable

We can create image from VM's disk:
- Stop the VM that you want to make an image of
- Go to **Disks**- menu
- Choose the disk and click on Actions -> **Create image**
- **Create**
- Click on actions on the disk and choose **Create instance**

Now we only need to echo and start the server in the start up script:

#!/bin/bash
echo "Hello world from $(hostname) $(hostname -I)" > /var/www/html/index.html
service apache2 start

Make sure the correct custom image is chosen in the OS and Storage-> Operating system and storage -> Image

**Create**