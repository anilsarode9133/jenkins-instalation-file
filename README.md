# jenkins-instalation-file
urls
sudo apt-get update -y 
sudo apt-get install openjdk-11-jdk -y
sudo wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt-get update -y
sudo apt-get install jenkins -y
sudo systemctl status jenkins
----------------------------------------------------------------------------------------------------------------------------------------------------------------------
TOMCAT INSTALLATION
 sudo apt-get update -y
 wget [paste copied link]                       #copy tomcat8 tar file link from google
 tar -xvzf [tarfile]                            #need to untar tar file
 cd tomcat folder                               # we doo all setup in this folder 
 cd bin                                         #need to install java in this configuration folder
   sudo apt-get install openjdk-8*                
   ./shutdown.sh
   ./startup.sh                                   #need to restart service if any changes done
 now you copy ip and paste in browser:8080
 *to change port number
 cd conf                                         #To change port number 
 vi server.xml                                   #in this file change connector port number
 cd bin 
   ./sutdown.sh
   ./startup.sh                                  #service resstart
 *if you login through manager app shows 403 denied because in context .xml file have error
    find / -name context.xml                     #shows 4files path need to go inside and disable valve class name <!-- *** -- >
    ./sutdown.sh
    ./startup.sh                                 # restart service
 * To give credentials                              
 TOMCAT USERNAME AND ROLES CONFIGURATION         #copy text and past in cd conf tomcat-user.xml file
 <role rolename="manager-gui"/>
 <role rolename="manager-script"/>
 <role rolename="manager-jmx"/>
 <role rolename="managerstatus"/>
 <user username="admin" password="admin" roles="mager-gui, manager-script, manager-jmx, manager-status"/>
 <user username="deployer" password="deployer" roles="manager-srcipt"/>
 <user username="tomcat"  password="s3cret" roles="manager-gui"/>

cd conf
 vi tomcat-user.xml                             #paste that credentials and restart service in cd bin 

---------------------------------------------------------------------------------------------------------------------------------------------------------------------

jenkins slave (centos 7)

adduser anil
passwd anil
password:123
vi /etc/ssh/sshd_config           #give passwd authen permission
service sshd restart              #need to restart sshd file after changes done
vi /etc/sudoers                   #give root permisions to user :wq!
yum install java11-openjdk-devel  #need to install java to connect master
---------------------------------------------------------------------------------------------------------------------------------------------------------------------

ansible main setup     [amazzon-linux]

yum update -y
yum install python                #because ansible developed in python
sudo amazon-linux-extras install ansible2
cd .ssh                           #in this foleder need to generate public key copy and paste in client servers
     ssh-keygen                   #generated 2keys copy pub key
     
     
ansible client setup 

yum update
cd .ssh
vi authorized_keys                #in this text key copy public key from ansinle main by using cat pub :wq
vi /etc/ssh/sshd_config           #need to modiefied 1.permit root login 2.passwd auth YES :wq
service sshd restart              #need to restart service


NOW YOU CAN CHECK AUTHENTICATION

ansible main
(ccd .ssh )ssh root@3.144.181.42             # client public ip  yes then you will in client server
exit                                         #return back to main server
vi /etc/ansible/hosts                        #in this file need create group of client nodes and paste public ip of nodes
     [dev]
     private ip
     [qa]
     private ip
     [prod]
     private ip
ansible -m ping all (dev,qa,prod)            #before going to automation need to check by pinging all the client nodes

CREATING PLAYBOOK TO DEPLOY JAVA
 vi java.yml                                 #file name
   ---
    - hosts : all
      tasks :
      -name :install java 1.7
       yum : name=java-1.7.0-openjdk state=present   
 :wq

ansible-playbook java.yml --syntax-check      #before execute the playbook need to check playbook 
ansible-playbook java.yml                     #to execute[run] the playbook 






