# Setting up Visual Studio Code Remote-SSH

Here are the steps to setup a Windows desktop running  (local VSCode) and connecting SSH to a remote Ubuntu server for software development.

## Pre-requisites

- A remote Ubuntu server
- A local Windows desktop with VS Code installed
- Set up key authentication for SSH

# Edit VS Remote-SSH Settings 

## Export your SSH key to SSH-1 (RSA format)

On the Windows desktop, you need to have an SSH key in SSH-1 (RSA) format.

- From PuTTYKeyGenerator, load your private key file
- Select the SSH-1 (RSA) format
- Export OpenSSH Key (force new file format)

The key file should look like:

```
Host coder003
    HostName 20.96.121.234
    User dliu
    IdentityFile ~/.ssh/id_coder003kkkk

-----BEGIN RSA PRIVATE KEY-----
...
...
...
-----END RSA PRIVATE KEY-----
```

- Edit your VSCode SSH Setting File (`C:\Users\<userid>\.ssh\config`) to contain an entry like this:

```
Host <hostname>
    HostName <ip addr>
    User <userid>
    IdentityFile ~/.ssh/<keyfilename>
```

## Add SSH to remote Ubuntu

You need to save the SSH public key to the remote Ubuntu under:

`~/.ssh/authorized_keys` with permissions set to 600, e.g.,

```
$ ls -l authorized_keys
-rw------- 1 dliu dliu 398 May 26 09:43 authorized_keys
```

# Launch VS Code (runas Administrator) on Windows

Once VS Code is running, you can presss CTRL-SHIFT-P to launch Command Palette.
Then run `Remote-SSH: Connect to Host...` 
You will see that VS Code is trying to setup (VS Code Server), this is why you may need to initially launch VS Code runas Administrator.

If everything is correct, you should see a new VS Code window connecting to the remote SSH server. 

# Setting Up git & github

[How to Setup Git and Github in Ubuntu 20.04](https://cis106.com/guides/Ubuntu%20Github%20Setup/)