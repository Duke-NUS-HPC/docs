## ssh to the Duke-NUS Office of Research HPC cluster using key pairs

9 March 2022

### Most people will not need this

Most people can just login in from the dashboard. 
See https://docs.google.com/document/d/1N4ptdEcy8IWBbYXaNW8SQYdzMQ3GncfdETTuqGzbFGQ/edit.

or from a command shell with password authentication

https://github.com/Duke-NUS-HPC/docs/blob/main/ssh-to-hpc.md

### If you really want to use Key pairs

It is hard to provide absolutely bullet-proof instructions for this because of variation
across different setups. If you have problems, contact Steve at gmssgr@nus.edu.sg.

These are the steps for ssh key-pair generation to log in to the Duke-NUS HPC cluster


### Steps

#### 1. Run `ssh-keygen` to generate a public/private key pair

At the command shell on your local desktop (for example, for a Windows desktop, a local shell from `mobaxterm`), generate ssh keys on your local desktop.

```
ssh-keygen -t rsa -b 5120
Output from ssh-keygen: Generating public/private rsa key pair.
Prompt from ssh-keygen and your input: Enter the  name of the file in which to save the key (/home/willie/.ssh/id_rsa): <hit return>
```

Enter a passphrase to prevent unauthorized users from accessing the HPC cluster using this key.

```
Prompt from ssh-keygen and your response: Enter passphrase (empty for no passphrase): mypassphrase
Enter same passphrase again: mypassphrase
```

There is more output from `ssh-keygen` that you do not need to worry about.

You need a unique name for the key pair to differentiate between the different keys you might have. Here I am using `hpc_rsa`.

```
cd .ssh
mv id_rsa hpc_rsa
mv id_rsa.pub hpc_rsa.pub
```

#### 2. Check the output from `ssh-keygen`

Check that your .`ssh` folder has the 2 generated key files. I named mine `hpc_rsa`. 
You need the name `hpc_rsa` for the config file on your local desktop,
and you need the contents of `hpc_rsa.pub` for the HPC.

```
ls -lh .ssh
-rw-------. 1 willie willie 4.2K Feb 24 16:27 hpc_rsa
-rw-r--r--. 1 willie willie  926 Feb 24 16:27 hpc_rsa.pub
```

#### 3. Edit the `.ssh/config` file on your desktop

I use `vim` but ok to use any text editor.

```
vim .ssh/config
```

In the editor input the following in the now opened config file, 
replacing the items in `<...>` as appropriate.
```
Host *
ServerAliveInterval 30
ServerAliveCountMax 5
TCPKeepAlive no

Host hpc    
HostName 172.25.138.10
User <your_NUS_ID>
ForwardX11 yes
IdentityFile /home/<your_local_user_id>/.ssh/hpc_rsa
```

#### 4. Put your public key on the HPC cluster

Open your generated `.pub` file (e.g. `.ssh/hpc_rsa.pub` using a text editor.

Copy ***EVERYTHING*** inside the `.pub` file to your clipboard.

Login to the HPC cluster via web dashboard (https://172.25.138.10:1111/pun/sys/dashboard).

From the web dashboard, click on the `DUKE-NUS HPC Shell Access` button.

In the now-opened shell/terminal, type 
```
vim .ssh/authorized_keys
```
In `vim`, type "i", start a new line and paste the contents of the .pub file you just copied using Ctl-v.

*Do not damage the existing key(s), and make sure your new key is all on one (new) line.*

After pasting, hit and release the "Esc" key to exit insert mode in `vim`,
and then type "ZZ" to save and exit.

#### 5. Test the connection

Now from the same local desktop command prompt type
```
ssh -X hpc
```

If the set up is correct `ssh` should 
prompt you to save the remote host signature, and 
then prompt
you to enter the passphrase for the key you have
generated above.  *This is not your NUS password, but the
passphrase that you associated with the key using `ssh-keygen`.*

After entering the passphrase 
you should be logged into the HPC cluster.

The `-X` enables X11 forwarding, i.e. allows the HPC cluster to pop up windows on 
your local desktop, *provided your local desktop is running an X11 server*.

#### 6. What can go wrong

If you have different command shells on the local desktop (e.g. `mobaxterm` and e.g. the terminal window
in `Rstudio`), they will probably have different locations for their respective `.ssh\` folders. If so, you need
make sure the private keys and `config` files are the same in the different `.ssh\` folder.

