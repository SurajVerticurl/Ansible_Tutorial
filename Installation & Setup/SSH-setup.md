# Setup SSH 

- add a user (on BOTH)

        useradd -m -s /bin/bash surajk
        passwd surajk

password : `surajk`

- adding the user to Sudoers List 

        visudo
        surajk  ALL=(ALL)        NOPASSWD:ALL


        sudo usermod -aG sudo surajk
  
- Give Permission to the User for ssh folder on WORKER-NODE

        sudo su ansadmin
        cd 
        mkdir -p ~/.ssh
        touch ~/.ssh/authorized_keys

        chmod -R 700 ~/.ssh
        chmod 600 ~/.ssh/*

- Permitting Passwdless Login on WORKER-NODE

        # sudo is mandatory
		   sudo nano /etc/ssh/sshd_config

		# To disable tunneled clear text passwords, change to no here!
  
        PasswordAuthentication yes
        PermitRootLogin yes #(PermitRootLogin prohibit-password for ubuntu)
        ClientAliveInterval 1200
        ClientAliveCountMax 3

- Add Hosts in known hosts

        #add host to list
        X.X.X.X    surajk
  
        sudo systemctl restart sshd.service

- generate and Copy SSH key to other nodes (on MASTER)

        sudo su - surajk
        ssh-keygen -t rsa
        ls -a
        cd .ssh

        ssh-copy-id surajk@<ip>


        cat ~/.ssh/id_rsa.pub
            Copy it to the remote ~/.ssh/authorized_keys
            [cat ~/.ssh/id_rsa.pub | ssh surajk@master-node 'cat >> ~/.ssh/authorized_keys']

## Reference

	https://community.cloudera.com/t5/Support-Questions/how-to-create-password-less-ssh-between-two-AWS-EC2/td-p/109442
	https://www.cyberciti.biz/faq/how-to-disable-ssh-password-login-on-linux/
	https://sectigostore.com/blog/what-is-passwordless-ssh-a-look-at-ssh-passwordless-authentication/
	
 - To permit root login
   
	 https://docs.rackspace.com/support/how-to/enable-ssh-remote-root-login-on-centos-and-the-ubuntu-operating-system/

