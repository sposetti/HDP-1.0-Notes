

http://hortonworks.com/download/thankyou_hdp1a/

Supplimental Info for installing HDP 1.0 on Amazon EC2.


Launching an EC2 Instance
=======

1. Launch Instances 
2. Classic Wizard > Quick Start
3. Choose the "Red Hat Enterprise Linux 6.3" 64-bit AMI.
4. Select "Large" instance type
5. Launch


On the HMC Server
=======

1. Choose a machine to host the HMC Server
2. Login to machine as root
3. Create the SSH Private Key

     	ssh-keygen

4. Select default values. This creates <code>id_rsa</code> public and private keys in <code>/root/.ssh</code>
5. Copy the <code>id_rsa.pub</code> public key into the <code>authorized_keys</code> file to enable passwordless access

     	// change to the ssh directory created by the ssh-keygen
     	cd /root/.ssh

    	// concatenate the public key information into the authorized key file
    	// note: be sure not to overwrite the existing content of this authorized_keys file, only concatenate
    	cat id_rsa.pub >> authorized_keys

6. Test out you can ssh w/o getting prompted for a password

    	ssh root@localhost

    note: you might be prompted to enter "yes" the first time. On subsequent times, you'll login directly

7. You can also testing ssh w/o getting prompted for a password with the hostname

    	// this will get you the EC2 internal DNS hostname
    	hostname

    	ssh root@{hostname.from.above} 

On All Hosts (turn off SELinux and Firewall)
=======

1a. Disable SELinux from the command line:

    	setenforce 0

1b. (optional) disable SELinux by setting "disabled" in the config (from "enforcing") to stay disabled between restarts

    	vi /etc/selinux/config

2. Disable the iptables firewall

    	/etc/init.d/iptables stop


On All Hosts (password-less SSH)
=======

1. On each host, copy the <code>id_rsa.pub</code> key from the HMC server
2. Concatenate the contents of this file to <code>authorized_keys</code> file on each host.
3. From the HMC Server, test connecting SSH to each host


Two Files
=======

1. Get the id_rsa from the HMC Server. This is the *SSH Private Key* and you'll need this during the install.
2. Create a text file and list all the hosts (one per line). Use the internal Private DNS name for each host. This can be on the instance info from the EMC2 Management Console, or by running "hostname" on each host.


Run the Install
========

1. Login into the HMC Server
2. Follow the instructions here:

http://hortonworks.com/download/thankyou_hdp1a/#down-install

 

