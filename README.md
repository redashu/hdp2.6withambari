# HDP 2.6 multinode setup using ambari on amazon ec2 ami 

## Need to done on each node 

### set hostname 

```
hostnamectl set-hostname  ec2-3-236-98-216.compute-1.amazonaws.com
```

### configure  local DNS 

```
[root@ec2-3-236-98-216 ~]# cat  /etc/hosts
127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
::1         localhost6 localhost6.localdomain6

172.31.66.4  ec2-3-236-98-216.compute-1.amazonaws.com
172.31.74.29  ec2-18-206-214-184.compute-1.amazonaws.com
172.31.71.69  ec2-3-236-78-59.compute-1.amazonaws.com

```

### disable firewalld and selinux 
```
setenfoce 0
systemctl disable --now firewalld
```

### installing NTP 
```
yum install -y ntp 
 systemctl enable --now ntpd
 
```
### Installing java jdk8 
```
yum install java-1.8.0-openjdk

```
### installing libtirpc

```
yum install libtirpc-devel

```

### install addition packages
```
yum install wget -y
yum install mysql-connector-java -y
yum install java-headless -y

```

### increase inode limit 
```
 ulimit  -n  10000
 
 ```
 ### setup ambari repo 
 ```
 wget -O  /etc/yum.repos.d/ambari.repo http://public-repo-1.hortonworks.com/ambari/centos7/2.x/updates/2.6.2.2/ambari.repo
 
 ```
 # Ambari Server setup  on Manager Node only 
 ```
 [root@ec2-3-236-98-216 ~]# yum  install ambari-server
 
 ```
 
## start ambari setup

```
 ambari-server setup 
 ```
 
 ## do one more step 
 ```
  ambari-server setup --jdbc-db=mysql --jdbc-driver=/usr/share/java/mysql-connector-java.jar
  ```
  
  ## start ambari
   
   ```
   ambari-server  start
   
   ```
   
