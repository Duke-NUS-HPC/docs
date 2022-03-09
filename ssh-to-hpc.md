## ssh to the Duke-NUS Office of Research HPC cluster

9 March 2022

### Many people can use the browser-based dashboard

See https://docs.google.com/document/d/1N4ptdEcy8IWBbYXaNW8SQYdzMQ3GncfdETTuqGzbFGQ/edit.

### If you want to log in from an command shell

Or you can login from a command shell:

`ssh -X nusstf\\gmsfoo@172.25.138.10`

for staff and

`ssh -X nusstu\\e999999@172.25.138.10`

for students and

`ssh -X nusext\\gmv999@172.25.138.10`

for visitor accounts.

The `-X` is for X windows forwarding.

***Remember, you have to be on an NUS network, which can be the NUS VPN***

***Remember, you cannot ssh to compute (CPU) or GPU nodes directly; you need to use gsub -I***

You can login to the head node from local desktops / laptops on the Duke-NUS network or 
from the login nodes of the old HPC cluster.

(You cannot ssh from PI's private servers due to current firewall settings.)

