Created time: 14:42 10-09-2026

## IP addresses

**Internal IP** - permanent internal IP address that does not change during the lifetime of an instance
**External ephemeral IP address** - temporary external IP address (accesible from internet) that might change when an instance is stopped or restarted
**External static IP address** - permanent external IP address that can be attached to a VM

VPC network -> IP addresses -> promote to static IP address

You pay more when reserved static external IP address is not assigned to a VM!

## Bootstrapping with Startup Script

Automatically install software when VM first starts up

Startup Script: VM config to perform automatic bootstrapping
