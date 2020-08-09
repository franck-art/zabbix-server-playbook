# Zabbix server

![artifactory](https://www.vm-hci.info/wp-content/uploads/2017/10/banner-zabbix.jpg)

## prerequisite

* Ansible
* Git
* Mysql server

### Installation of prerequisites

1. On zabbix server
NB:  These installations will be done on the zabbix server
   
   ```
   sudo yum install git -y
   sudo yum -y install epel-release 
   sudo yum install ansible -y
   wget http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm
   sudo rpm -ivh mysql-community-release-el7-5.noarch.rpm
   sudo yum update -y
   sudo yum install mysql-server -y
   sudo systemctl start mysqld
   ```
   
   NB: Installation of zabbix agent can be crossed because it does not enter the installation of zabbix server. the goal was to do a much more complete job, which is why this part was added

2. Installing the zabbix agent on the servers to be supervised

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
  * Modify the host and main.yml files in the vars / directory
  * ansible-playbook zabbix_playbook.yml
2. Jenkins
  * git clone https://github.com/franck-art/zabbix-server-playbook.git
  * cd zabbix-server-playbook/
  * Modify the host and main.yml files in the vars / directory
  * Push on Jenkins
  
NB: Make sure that jenkins is correctly configured

###### Connect to the zabbix web interface

To access the Zabbix home page, type the url in your browser:
`http://@ip/zabbix`

