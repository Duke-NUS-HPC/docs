## ssh to the Duke-NUS Office of Reearch HPC cluster using key pairs

26 February 2022

These are the steps for ssh key-pair generation to log in to the Duke-NUS HPC cluster

Currently, login to the head node is enabled from local desktops within the Duke-NUS nextwork or the 
the login nodes of the old HPC cluster.

You cannot ssh from PI's private servers due to current firewall settings.

### Steps

#### 1. Run ssh-keygen

At the command shell, generate ssh keys on your local desktop

```
ssh-keygen -t rsa -b 5120
Output from ssh-keygen: Generating public/private rsa key pair.
```

You need a unique name for the key pair to differentiate between the different keys you might have

```
Prompt from ssh-keygen and your input: Enter the  name of the file in which to save the key (/home/willie/.ssh/id_rsa): /home/willie/.ssh/hpc_rsa
```

Enter a passphrase to prevent unauthorized users to access the hpc cluster freely using this key

```
Prompt from ssh-keygen and your response: Enter passphrase (empty for no passphrase): mypassphrase#!#
Enter same passphrase again: mypassphrasee#!#
```

There is more output ssh-keygen output you do not need to worry about.

#### 2. Check the output from ssh-keygen

Look in you .ssh folder and you should see your two generated key files. I named mine `hpc_rsa`. 
You need `hpc_rsa` for the config file on your local desktop,
and `hpc_rsa.pub` for the HPC.

```
ls -lh .ssh
-rw-------. 1 willie willie 4.2K Feb 24 16:27 hpc_rsa
-rw-r--r--. 1 willie willie  926 Feb 24 16:27 hpc_rsa.pub
```

#### 3. Edit the .ssh/config file on your desktop

I use vim but ok to use any text editor.

```
vim .ssh/config
```

In the editor innput the following in the now opened config file
```
Host *
ServerAliveInterval 30
ServerAliveCountMax 5
TCPKeepAlive no

Host hpc    
HostName 172.25.138.10
User <YOUR_NUS_ID>
ForwardX11 yes
IdentityFile /home/willie/.ssh/test
```

#### 4. Put your public key on the HPC cluster

Open your generated .pub file (e.g. `.ssh/hpc_rsa.pub` using a text editor.

Copy ***EVERYTHING*** inside the .pub file you just opened into your clipboard.

Login to the HPC clsuter via web dashboard (https://172.25.138.10:1111/pun/sys/dashboard).

Once you are logged in, click on the DUKE-NUS HPC Shell access button.

In the now opened shell/terminal, type 
```
vim .ssh/authorized_keys
```
In `vim`, type "i", start a new line and paste the contents of the .pub file you just copied.

Once the paste is successful, type hit "Esc" key and type "ZZ" to save and exit `vim`.

#### 5. Test the connection

Now from your local desktop command prompt type
```
ssh -X hpc
```

If setup properly there should be
prompts to save the remote host signature and a prompt
for you to enter the password for the key you have
generated above. Once you have entered the password 
you should be logged into the HPC cluster.

The `-X` enables X11 forwarding, i.e. allows the HPC cluster to pop up windows on 
your local desktop, *provided your local desktop is running an X11 server*.
