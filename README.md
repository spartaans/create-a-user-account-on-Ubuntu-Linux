# create-a-user-account-on-Ubuntu-Linux
Open the terminal application
Log in to remote box by running the ssh user@your-ubuntu-box-ip
To add a new user in Ubuntu run sudo adduser userNameHere
Enter password and other needed info to create a user account on Ubuntu server
New username would be added to /etc/passwd file, and encrypted password stored in the /etc/shadow file

add a new user in Ubuntu called bob
$ sudo adduser bob

Verification
$ cat /etc/passwd
$ grep '^vivek' /etc/passwd
bob:x:1001:1001:Bob Gite,,,:/home/bob:/bin/bash

How do I log in using ssh?
From your Windows (WSL) or macOS or Linux desktop, run:
$ ssh vivek@your-aws-ubuntu-server-ip
OR
$ ssh -i ~/.ssh/aws.pub.key vivek@your-aws-ubuntu-server-ip
Enter the password when prompted

Creating a user account using useradd command on Ubuntu
$ sudo useradd -s /path/to/shell -d /home/{dirname} -m -G {secondary-group} {username}
$ sudo passwd {username}

Let us create a new user named vivek using the useradd command on Ubuntu:
$ sudo useradd -s /bin/bash -d /home/vivek/ -m -G sudo vivek
$ sudo passwd vivek
Where,

-s /bin/bash – Set /bin/bash as login shell of the new account
-d /home/vivek/ – Set /home/vivek/ as home directory of the new Ubuntu account
-m – Create the user’s home directory
-G sudo – Make sure vivek user can sudo i.e. give admin access to the new account
I strongly recommend installing ssh keys while creating the new user account. You must have RSA/ed25519 key pair on your local desktop/laptop. Use the cat command to view your current RSA/ed25519 public key on the desktop:
$ cat ~/.ssh/id_ed25519.pub
$ cat ~/.ssh/id_rsa.pub

Run the following commands on your Ubuntu server to install above ~/.ssh/id_ed25519.pub key from your desktop:
$ sudo mkdir /home/vivek/.ssh/
$ sudo chmod 0700 /home/vivek/.ssh/
$ sudo -- sh -c "echo 'ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAILaLvLmaW9qIbUVo1aDHWZE9JewbNfIdTVif2aFGF0E0 vivek@nixcraft' > /home/vivek/.ssh/authorized_keys"
$ sudo chown -R vivek:vivek /home/vivek/.ssh/

Now you can log in with ssh keys:
$ ssh vivek@your-aws-server-ip-here

How to delete a user account

Use the userdel command as follows:
sudo userdel {userName}
sudo userdel vivek

To remove home directory and mail spool too, enter:
sudo userdel -r {user-name}
sudo userdel -r jerry

How to change Linux user password

Run the following passwd command:
sudo passwd {username}
sudo passwd tom

To change your own password, enter:
passwd

