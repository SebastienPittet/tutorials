---
title: "Scaling an Instance"
slug: "instance-scaling"
meta_desc: "Learn how to scale up CPU, memory or disk space of your Instance. Exoscale Compute makes it very easy to scale up your cloud server to best suit your needs"
tags: "compute"
---

Your application will grow in time, and so will your virtual machines! During
the life of your project you will be able to resize your instance up and down,
scaling its service level (the combination of CPU's cores and RAM) and its disk
size, optimizing it for your needs.

Select the instance you wish to operate on, and from the instance detail you
will be able to access the scaling interface.

**Please note that every scaling operation needs to be performed on a stopped
instance.**

## Scaling the Service Level
Scaling your CPU's cores and the RAM of your machine is pretty straightforward:
stop your instance, access the scaling view, choose your new Service Level and
restart when finished. Remember that some Service Levels may be unavailable due
to eventual restrictions of your selected operative system.

## Scaling the disk size
As for scaling the Service Level, scaling your disk size is easy. You can resize your volume up by steps of 1 GB. Instances from *Micro* up to *Huge* type can scale up to 400 GB, *Mega* instances scale up to 800 GB and Titan instances scale up to 1600 GB.

For linux OS, filesystem resize happens at boot time automatically. For Windows Os, you will need to extend the partition size from Disk Management after boot.
