## ssh to the Duke-NUS Office of Research HPC cluster

9 March 2022

### Many people can use the browser-based dashboard

See https://docs.google.com/document/d/1N4ptdEcy8IWBbYXaNW8SQYdzMQ3GncfdETTuqGzbFGQ/edit.

### If you want to log in from an command shell

#### For staff:

`ssh -X nusstf\\gmsfoo@172.25.138.10`

#### For students:

`ssh -X nusstu\\e999999@172.25.138.10`

#### For visitor accounts:

`ssh -X nusext\\gmv999@172.25.138.10`

The `-X` is for X windows forwarding.

***Remember, you have to be on an NUS network, which can be the NUS VPN***

***Remember, you cannot ssh to compute (CPU) or GPU nodes directly; you need to use qsub -I***

***If you want X forwarding from the new interactive session, use qsub -IX***

To allow a program on the cluster to open a window on your local computer (e.g. MS Windows PC or Mac or Linux) you need 
to have an "X Window" (X11) server running on your local machine.
This is automatic if you use mobaxterm (PCs, https://mobaxterm.mobatek.net/) or Xquartz (Mac, https://www.xquartz.org/) terminals.

You can login to the head node from local desktops / laptops on the Duke-NUS network.

(You cannot ssh from PI's private servers due to current firewall settings.)

