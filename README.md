# Zabbix server

![artifactory](https://www.vm-hci.info/wp-content/uploads/2017/10/banner-zabbix.jpg)

## prerequisite

* Ansible
* Git
* Mysql server

### Installation of prerequisites

1. zabbix server

We have two methods:

- In CentOs server, follow these steps  
These installations will be done on the zabbix server. 
if you are on aws, use the second dot
   
   ```
   sudo yum install git -y
   sudo yum -y install epel-release 
   sudo yum install ansible -y
   sudo yum install wget -y
   wget http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm
   sudo rpm -ivh mysql-community-release-el7-5.noarch.rpm
   sudo yum update -y
   sudo yum install mysql-server -y
   sudo systemctl start mysqld
   ```
 - On aws, load the zabbix stack named zabbix.yml
   

2. Installing the zabbix agent on the servers to be supervised

NB: Installation of zabbix agent can be crossed because it does not enter the installation of zabbix server. the goal was to do a much more complete job, which is why this part was added

```
   sudo rpm -ivh https://repo.zabbix.com/zabbix/4.0/rhel/7/x86_64/zabbix-release-4.0-1.el7.noarch.rpm
   sudo yum install zabbix-agent
   sudo service zabbix-agent start
```


#### Configuring the mysql server on zabbix server

```
shell> mysql -uroot -p 
mysql> create database zabbix character set utf8 collate utf8_bin;
mysql> grant all privileges on zabbix.* to zabbix@localhost identified by '';
mysql> quit;
```

##### Download the playbook

1. Ansible
  * git clone https://github.com/franck-art/zabbix-server-playbook.git
  * cd zabbix-server-playbook/
  * Modify the host and zabbix_playbook.yml
  * ansible-playbook --private-key /path/of/your/private/key   zabbix_playbook.yml
2. Jenkins
  * git clone https://github.com/franck-art/zabbix-server-playbook.git
  * cd zabbix-server-playbook/
  * Modify the host and zabbix_playbook.yml
  * Push on github
  * Configure Pipeline and webhook in Jenkins and deploy Zabbix-server
  
NB: Make sure that jenkins is correctly configured

###### Connect to the zabbix web interface

To access the Zabbix home page, type the url in your browser:
`http://@ip/zabbix`


--> zabbix web interface connection:
* Username: Admin
* Password: zabbix

**NB**: Make sure that the listening port of the zabbix server and agents is open: **10050**

