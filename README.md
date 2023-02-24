# jenkins-instalation-file
urls
sudo apt-get update -y 
sudo apt-get install openjdk-11-jdk -y
sudo wget -q -O - https://pkg.jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt-get update -y
sudo apt-get install jenkins -y
sudo systemctl status jenkins
