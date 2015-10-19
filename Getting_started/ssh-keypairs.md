---
title: SSH keypairs
meta_desc: How to import or create an SSH keypair and use it to connect to your Exoscale vitual machine instance through SSH
date: 2015-10-09 18:40 +01:00
category: Getting started
tags: security, ssh
---
SSH keypairs are a way to authenticate to your linux virtual machine without using a password with the added security of [SSH Public-Key authentication](https://en.wikipedia.org/wiki/Public-key_cryptography).

Public-Key authentication is both:

* **Secure**: breaking an SSH key requires so much time and computational power that these sorts of attacks are not practical in the real world. SSH keys are much, much secure than even very strong passwords.

* **Convenient**: instead of managing per-machine passwords or sharing them across your company, every physical person who needs access to your servers give you their public key. You can then setup granular access control by adding those keys only to the relevant machines. If you need to revoke someone's access, simply revoking his key prevents him from logging in without altering other people's workflow.

Exoscale allows you to automatically provision linux machines with SSH public keys to use for Public-Key authentication with SSHv2.

Note that while you can have multiple keypairs in your account, the instance creation dialog only allows you to select one keypair. Once the instance is created, you may allow additional public keys and set up more detailed access control using traditional means.

keypairs can be imported or created through the [keypairs view](https://portal.exoscale.ch/compute/keypairs).


## Import an existing public key

Enter the [New SSH keypair](https://portal.exoscale.ch/compute/keypairs/add) screen and choose *IMPORT*. You can then paste in the content of your **public key**.

## Create a new SSH keypair

If you dont't have an SSH keypair you can choose to either create one through a simple command on your linux machine or to create one through the Exoscale console.

### Create a new SSH keypair on your machine
You can create a new SSH keypair with the following command:

<pre>
ssh-keygen -t rsa -b 4096 -C 'a-comment-to-identify-your-key'
</pre>

You will be asked for a name and location to save your new keypair (keyairs are usually stored in `~/.ssh`) and for a password to protect it. You can then copy and paste the content of your freshly created **public key** in the import text field of the [New SSH keypair](https://portal.exoscale.ch/compute/keypairs/add) screen.

### Create a new SSH keypair through the Exoscale console

Access the [New SSH keypair](https://portal.exoscale.ch/compute/keypairs/add) screen and choose *CREATE*. through this screen you will create a new SSH keypair: the public key will be available through the interface to provision your instances, while the private key will be displayed to you at the end of the process.

**Save the private key on you computer**. To do so copy the content of the private key and paste it in a text file called with the bare name of your key.

SSH keys are usually stored in the `~/.ssh/` folder on your linux machine. If you wish you may extract the public key from the private key using the `ssh-keygen -y` command. The full process may be as following:

<pre>
touch /desired/destination/to/your/public/key
chmod u=rw,go-rwx /desired/destination/to/your/public/key
ssh-keygen -y > /desired/destination/to/your/public/key
	Enter file in which the key is (/home/user/.ssh/id_rsa): /path/to/your/private/key
</pre>

## Provision an instance with a keypair

When creating a new virtual machine, simply select the keypair you want to be associated to that instance and the person holding the corresponding private key will be able to log in via password-less SSH.

**Plese be aware that deleting a public key in the Exoscale console does not automatically remove the authorized public key from an already created instance.** If you want to completely revoke a key, you need to do so manually by deleting the key on every instance holding it.

## Connect to your newly created instance

Once your new instance has started and is running, you can connect to it via SSH. How to use SSH is out of the scope of this documentation, but assuming the following conditions:
	
* You have SSH installed on your machine
* Your private key is stored in `~/.ssh/id_rsa`
* Permissions of the `~/.ssh` folder (700) and of your private key (600) are correct
* You opened TCP port 22 in your machine's [securty groups](https://community.exoscale.ch/tutorial/introduction-to-security-groups/)

you should then be able to connect to your machine simply with:

<pre>
ssh root@ip-address-of-your-instance
</pre>

You may be asked the **password of your private key** if set (**not the password of your instance**).

You may also see a warning about the remote host identification: this is to be expected **on a first connection** and you can trust the remote.
