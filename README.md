![Pattern_Social_16x9](https://github.com/user-attachments/assets/74dc65b6-5208-47aa-a502-524a9d123e9f)

<div style='display:flex; align-items:center; gap: 30px;' align='center'>
<a href="https://www.credly.com/go/6C69ZOKh"><img src="https://github.com/akashdip2001/akashdip2001/raw/main/img/Badge/github-foundations.png" width="150px" height="150px" /></a>
<a href="https://www.linkedin.com/posts/akashdip2001_postman-api-certification-activity-7264947968200368128-MHWG"><img src="https://github.com/akashdip2001/akashdip2001/raw/main/img/Badge/Postman%20White%20badge.png" width="150px" height="150px" /></a>
<a href="https://www.credly.com/badges/998c7f5e-7081-4cd7-b8ee-153ece4d89f0/public_url"><img src="https://github.com/akashdip2001/akashdip2001/raw/main/img/Badge/aws-educate-introduction-to-cloud-101.png" width="150px" height="150px" /></a>
<a href="https://www.credly.com/badges/6ea09b08-c1f7-4035-ae3b-bf921004d224/public_url"><img src="https://github.com/akashdip2001/akashdip2001/raw/main/img/Badge/aws-educate-getting-started-with-security.png" width="150px" height="150px" /></a>
</div>


==============================
Linux with AWS Cloud Bootcamp
==============================

Duration : 2 to 3 weeks

Pre-Requisites : Your time + Concentration + Practice

Course Content : 


1) Windows Vs Linux
2) Linux History
3) Linux Distributions
4) Linux VM Setup
5) Working with Files & Directories
6) Working with text editors
7) User Management
8) File Permissions
9) Networking commands
10) Pacakge Managers


11) On-Prem Infrastructure
12) Cloud Computing
13) Cloud Providers (Amazon, MS, Google)
14) AWS Cloud Introduction
15) AWS Console tour
16) EC2 (Elastic Compute Cloud)
17) RDS (Relational Database service)
18) S3 (simple storage service)
19) Beanstack (web app deployment)
20) IAM (Identity & Access Mgmt)
21) Lambdas (Serverless computing)
22) Route 53 (DNS)


Frontend Technologies : Angular/React

Backend Technologies : Java Springboot MS

Databases : Oracle , Mysql + Mongo DB

DevOps tools : mvn, git, docker, jenkins, k8s

Operating Systems : linux

Cloud Services: Aws services


===========================
What is Operating System ?
===========================

=> OS is a software

=> OS act as a mediator between users and computers

=> Wihout OS we can't use computers

=> We have several Operating Systems in the market

 Ex : Windows, Linux, Mac, Solaris, Anroid, IOS
 
============ 
Windows OS  
============

=> Developed By Microsoft company

=> It is GUI based OS

=> It is licensed OS 

=> Single user based OS

=> Security features are less

Note: Anti Virus software we have to install.

=> Windows OS is recommended for personal use

Ex : watch movies, games, browsing, online classes

===========
Linux OS 
===========

=> Developed by Linus Torvalds

=> It is free and open source

=> Linux supports both GUI and CLI

=> Linux is multi user based OS

=> Linux is Virus free (security is very high)

=> It is highly recommended for business use cases

Ex : Database servers, app servers, k8s cluster, jenkins server, sonarqube server, docker server, nexus server, ELK, Log files... 

=================
Linux OS History
=================

1990

Unix -->  challenges

Minux

	(Li)nus + Mi(nux ) = Linux
	
====================
Linux Distributions	
====================

200+ distributions

amazon linux
ubuntu linux
cent os linux
kali linux
suse linux
fedora linux
red hat linux


AWS Account Setup : https://www.youtube.com/watch?v=xi-JDeceLeI

====================
Linux Machine Setup
====================

Approach-1 : Install Linux OS directley in PC

Approach-2 : Install Linux as Guest OS using Virtual Box

Approach-3 : Setup Linux VM in windows using Vagrant

Approach-4 : Take linux vm for rent in cloud platform (AWS)


EC2 service we can use to setup virtual machines in aws cloud.

AWS Free Tier account (1 year)

EC2 : To setup virtual machines 

Monthly : 750 hours free of cost

===============
Lab Practicals
===============

Step-1 : Login into aws account 

Step-2 : Go to EC2 service and launch new instance 

		AMI : amazon linux 
		
		instance type : t2.micro / t3.micro
		
		Keypair : Create new keypair (.pem)
		
Step-3 : Select machine and click on Connect (SSH Client)

Step-4 : Open gitbash from keypair location and execute commands (chmod and ssh)



## Connect with EC2 VM using MobaXterm: https://www.youtube.com/watch?v=uI2iDk8iTps&t=458s


## Connect with EC2 VM using GitBash: 
https://youtu.be/JMlQaTXvw5o?si=okXzG9jKkBn1xcMY				
			
## Connect with EC2 VM using Putty : https://www.youtube.com/watch?v=GXc_bxmP0AA

===================
Linux Architecture
===================

1) Apps / Commands

2) Shell

3) Kernel

4) Hardware components


=> Shell is responsible to validate command given by user and translate that into kernel understandable format.

=> Kernel is one of the core component in linux os. Kernel is responsible to give instructions to hardware to process command execution.

====================
Linux File System
=====================

=> In linux os everything will be represented as file only.

		/
		 /bin
		 /opt
		 /etc
		 /lib
		 /var
		 /mnt
		 /media
		 /home
		 
		 
Note: In Linux VM for every user one home directory will be available like below.

		 
	ec2-user : /home/ec2-user
	
	ashok   : /home/ashok
	
	sita : /home/sita

================	
Linux Commands 
================

pwd: display present working directory.

cd : change directory 

touch : create empty files 

ls : listing the data of pwd

ls -l : long listing with alphabetical order

ls -lr : display files in reverse of alphabetical

ls -lt : display latest files on top

ls -ltr : display old files on top

ls -la : show hidden files also

mkdir : create new directory

rmdir : remove empty directory

rm : remove file 

rm -rf : remove non-empty directories

cat : create file with data + append data + print data

		cat > abc.txt
		
		cat >> abc.txt
		
		cat abc.txt
		
		cat -n abc.txt
		
tac : print data from bottom to top

cp : copy one file to another file

mv : rename + move 

history : display user activities in linux

head : display first 10 lines of the file.

			head f1.txt 
			
			head -n 5 f1.txt 
			
			head -n 100 f1.txt

tail : display last 10 lines of the file.

			tail f1.txt 
			
			tail -n 15 f1.txt
			
			tail -n 50 app.log
			
			tail -f app.log

=========================================
grep : global regular expression print
=========================================

=> It is used for searching data in the file

# print lines which contains ashokit keyword
grep 'ashokit' app.log

# print lines which contains ashokit keyword along with line numbers and ignore case sentivie

grep -n -i 'exception' app.log

# print lines which doesn't contains ashokit keyword

grep -v 'ashokit' app.log

# search for ashokit keyword in last 10 lines
tail app.log | grep 'ashokit'


# search for exception keyword in last 100 lines
tail -n 100 app.log | grep -n -i 'exception'


==========
vi editor 
==========

=> It is used to edit the files in linux os

=> Using vi we can open existing files and we can create new files also.

$ vi java.txt

=> vi command works based on 3 modes

	1) command mode (read data)
	
	2) insert mode (press i in keyword)
	
	3) esc mode (press esc key)
	
	=> save and close (:wq + Enter)
	
	=> close without saving (:q! + Enter)
	
=====================
Networking Commands
=====================

ifconfig : To check IP address of our machine

ping: To check connectivity

		ping www.google.com
		
		ping www.facebook.com 
		
		ping 172.31.4.278

wget: To download files from internet

	wget <url>
	

curl: To send Http request to server 

	curl https://reqres.in/api/users
	
================
User Management	
================

-> Linux OS is a multi user based OS

-> Multiple Users can connect with linux vm at a time.

Note: When we create linux vm using "Amazon Linux" AMI we will get 'ec2-user' as a default user with sudo priviliges.

SUDO : Super user doing operation


# check users available
cat /etc/passwd

# create new user 

Syntax : sudo useradd <username>

Ex : sudo useradd john

# set password for user 

Syntax : sudo passwd <username>

Ex : sudo passwd john

================================
What is sudoers file in linux ?
================================

Note: To give sudo priviliges for the users we need to add them in sudoers file.

# open sudoers file
sudo visudo

Note: Configure user like below (just below root user)

john    ALL=(ALL)       ALL
smith   ALL=(ALL)		ALL

Note: After adding user,  close that file using "CTRL + X + Y + Enter"

===================================================
How to enable password based authentication in linux ?
===================================================

=> In Linux VM by default PasswordAuthentication is disabled.

=> If we want to connect with Linux vm using  username and password we need to enable that.

# open sshd_config file
sudo vi /etc/ssh/sshd_config

=> Find the Line containing â€˜PasswordAuthenticationâ€™ parameter and change its value from â€˜noâ€™ to â€˜yesâ€™

Note: save that file and close it using :wq + Enter

# restart sshd service 
sudo service sshd restart

# exit from the machine 
exit

# connect with linux vm usng john user 
# open gitbash 

# execute ssh command
ssh john@public-ip

==================
File Permissions 
==================

=> File permissions are divided into 3 types 

		a) read (r)
		b) write (w)
		c) execute (x)
		
=> File permissions will be represented like below

	Ex : -rwxrwxrwx f1.txt
	     drwxrwxrwx ashokit
	
=> First 3 characters will represent owner permissions (the user who created that file)

=> Middle 3 characters will represent group permissions.

=> Last 3 characters will represent other users permissions.	


Ex:

-rw-r-xr-x f1.txt 

owner => read + write 
group => read + execute 
others => read + execute 

-rwx------ f2.txt 

owner : read + write + execute 
group : Nothing
Others: Nothing


=> To add or remove file permissions we will use 'chmod' command.

# add execute permission for user(owner)
chmod u+x f1.txt 

# remove write permission for user(owner)
chmod u-w f1.txt 

# add write and execute permissions for group
chmod g+wx f1.txt

# remove read permission for others
chmod o-r f1.txt

=> We can represent file permissions using numeric numbers also.

0 => No Permissions 

1 => Execute

2 => Write

3 => (2+1) => Write + Execute 

4 => Read 

5 => (4+1) => Read + Execute 

6 => (4+2) => Read + Write 

7 => (4+2+1) => Read + Write + Execute

# user-read, group-write, others- r+e
chmod 425 f1.txt

# u+rw, g+w, o+we
chmod 623 f1.txt

#u-rwx, g-rwx , o+rwx
chmod 7 f1.txt 

#u-rwx, g+rwx , o+rwx
chmod 77 f1.txt 

======================================
How to change ownership of the file ?
======================================

=> using chown command we can change ownership 

$ sudo chown ashok f1.txt


==================
Package Managers
==================

Package : A software 

=> Package managers are used to manage softwares installation in linux machines.

=> Package Managers are specific to linux distribution.

yum : amazon linux, cent os 

apt : ubuntu , debian

rpm : red hat


# install git 
sudo yum install git -y 
git --version
whereis git

# install java 
sudo yum install java -y
java -version
whereis java

# install maven 
sudo yum install maven -y
maven -version
whereis maven
