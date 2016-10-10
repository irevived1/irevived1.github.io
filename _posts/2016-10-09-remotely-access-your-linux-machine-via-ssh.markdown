---
layout: post
title:  "Remotely Access your Linux Machine via SSH"
date:   2016-10-09 11:00:00 -0400
---

10.09.16

Remotely Access your Linux Machine via SSH

If you have an old desktop machine sitting somewhere accumulating dust, here is your chance to turn your monitorless desktop into a personal Linux machine where you can remotely access it anywhere in the world!  Only if internet is available.  

Installing the Operating System on your ancient device.

Wipe out the old harddrive, get an .iso of your flavor, could be Ubuntu, Debian, or even Red Hat and install on it.  

Installing SSHD onto your newly installed Linux machine

Depending on which LInux Distribution you chose, the command to install SSHD will be different.  Please check the documentation of your distro.  I chose Ubuntu and `sudo apt-get install` will be my primary command to install anything.

Installation of the OpenSSH client and server applications is simple. To install the OpenSSH client applications on your Ubuntu system, use this command at a terminal prompt:

`sudo apt install openssh-client`
To install the OpenSSH server application, and related support files, use this command at a terminal prompt:

`sudo apt install openssh-server`
The openssh-server package can also be selected to install during the Server Edition installation process.

Once that’s done, find out your private IP address by entering `ifconfig` in your terminal and test to see if the SSHD is working properly.  Usually the private IP is something ilke 10.0.x.x or 192.168.x.x.  Make sure you use another device that is within the local network.  Simply open your terminal and prompt in:

`ssh your_user_name@server_ip_address`

You may wish to add the -p flag for custom port number, in this case, the default will be 22.

You now should be able to access your linux server within your local network.  Before we open up to the public network for remote access, it is very important to add some form of security to our server.  We would want to have a strong password for our server but we do not want to remember it at the same time.  This is where RSA kicks in for the rescue.  On your local computer, prompt in `ssh-keygen`,(inputs/passphrase is optional).  This generates a public and private key in your .ssh directory located in your home directory.  Remember the private key should not be shared with anyone unless you want them to access your server.  Use your favorite editor and open .ssh/id_rsa.pub, then copy what’s in there on the clipboard and let’s go to the server for a moment.  

On your server’s home directory, make a directory called .ssh and restrict the permission by prompting `chmod 700 .ssh`.  The number 700 grants full permission for the root user but no read, write and execute for any other users.  

Now, create a file called `authorized_keys` in your .ssh folder and paste the id_rsa.pub from your local machine to the server.  

If you attempt to reconnect to your server, you should be able to login without entering any password thanks to RSA.  We are almost done, now we’ll have to visit `/etc/ssh/sshd_config` and modify some settings.  It is important to prevent anyone to login with a password.  So we will have to look for `PasswordAuthentication` and uncomment the line.  Then change from `yes` to `no` to disable password authentication.  We should also disable root login.  We can disable root login by searching for `PermitRootLogin` and change that from `yes` to `no` once again.  It is optional to modify your port number as well.

Finally, restart your sshd to take effect by running the following command:

`sudo service ssh restart`

To enable access from the open network, you will have to configure your router in the port forwarding section.  Different router have different ways to configure, but they pretty much works the same.  You will have to forward your chosen port number and direct UDP/TCP packets to your server’s private IP address.  If you are using the default setting, again, you should forward it to port 22.  Otherwise, just change 22 to some any other port number you wish.  Please consult with the router’s user menu.

Lastly, you will have to check the connectivity of your setup by typing:

`ssh your_user_name@your_public_ip_address -p your_custom_port_number`

Enjoy!
irevievd1

Source: [https://help.ubuntu.com/lts/serverguide/openssh-server.html](https://help.ubuntu.com/lts/serverguide/openssh-server.html)
[https://www.youtube.com/watch?v=EuIYabZS3ow](https://www.youtube.com/watch?v=EuIYabZS3ow)
