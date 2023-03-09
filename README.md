# Ansible
This repository consists of info about how to install Ansible and some playbook examples.

# How To Install Ansible --

Steps to install ansible and how to configure ansible nodes ---

1. For this take 2 ubuntu servers -- one for ansible-server other is node-1
2. Create one centos server which will work as node-2
3. Create one user named ansible (adduser ansible)
4. Set password for this user (passwd ansible --prompt will come provide your password)
5. Step 4 will be done on all 3 servers.  -- Install ansible only on ansible-server
6. Now change some configuration 
	    1. vi /etc/ansible/hosts  --(Only on ansible-server)
	       add private ip's of your other server's so that it will communicate.
	    2. vi /etc/ansible/ansible.cfg ---(Ansible will be installed only on server not on node)
	       Uncomment these lines --
	         1. hosts      2. user
    	3. Now to communicate with each other we need ssh keys to do this 
	       again change some configuration as --
		     vi /etc/ssh/sshd_config
		      Uncomment these lines
				1.Permit root login yes
				2.password authontication yes  --(Comment second password authontication)
				3.service ssh restart (on ubuntu server)
				4.systemctl sshd restart (on centos server)
				

  Now to check connection with other servers from ansible-server
	ssh private ip of other server -- it will prompt for password give the same passwd that you given before
	if the user changed then connection is success.

  Here it will always asks password to avoid this we have other method	as -
	On ansible-server be as ansible user as su - ansible
	ssh-keygen (give enter 2,3 times)
	then cd .ssh --> ls-a --> It will show some files as ssh_rsa like this
	Then perform 
	   1.ssh-copy-id ansible@ip of other server (node-1)
	   2.ssh-copy-id ansible@ip of other server (node-2)	
------------------------------------------------------------------------------	   
Now add nodes ip in servers /etc/ansible/hosts files
Here you can also create diff groups under that mention ip of that node-1
	example - [webserver] -- give any name in []
	            ip
			      [dbserver]
				      ip

Now to work with ansible we have some menthods --
  1.Ad-hoc commands
  2.Playbooks

Ad-hoc commands are single line linux commands which are used perform some action
Ad-hoc commands will not support Idempotence 

Q) What is Idempotence --
      Suppose once we create a file by touch command and now if we do this again the file will be overwritten
	    but in Ansible we have one powerfull feature called Idempotence which will not work if the
	    same work has done in previous steps.
  Ad-hoc commands not support Idempotence.
  Playbooks support Idempotence.

  In playbooks we use some modules which are nothing but some pre-deffined commands 
  which will give some boost to ansible to complete his work.

For Ansible we will write playbooks which are nothing but yaml files.
Yaml is a human readeble files which has key-pair values.             ------------- [https://youtu.be/GN6eMwsNkds]	-- To understand yaml file
We will study some modules -- 
You can find more modules in ansible-documentation (https://docs.ansible.com/ansible/2.9/modules/list_of_all_modules.html)
In playbooks the indentation is most importatnt.

