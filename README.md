### hdp-8-Nifi-installation

> Install prerequisites

```sh
# log as root
sudo su - root

# install packages
 yum -y install libffi-devel gmp-devel ant gcc gcc-c++ rsync krb5-devel openssl-devel \
 cyrus-sasl-devel cyrus-sasl-gssapi sqlite-devel openldap-devel libtidy libxml2-devel \
 libxslt-devel maven
 
 yum install cyrus-sasl-devel cyrus-sasl-gssapi cyrus-sasl-md5 cyrus-sasl-plain
 
 yum -y install mysql-devel mysql
 
 yum -y install python-devel python-simplejson python-setuptools
```

> Download and install HUE

```sh
# download 
wget http://gethue.com/downloads/releases/4.0.1/hue-4.0.1.tgz

# unpack package
tar -xzvf hue-4.0.1.tgz

# create hue directory
mkdir -p /usr/local/hue

# Copy untar binaries into the new folder
mv hue-4.0.0/* /usr/local/hue

# go to hue directory
cd /usr/local/hue

# Build the hue module
make apps


```

> Configure Hadoop cluster to accept connections from HUE:
- ensure WebHDFS is enabled
![MetaStore remote database](https://github.com/gamboabdoulraoufou/hdp-5-HUE-installation/blob/master/img/hue_web_hdfs2.png)
- proxy user hosts and groups for HUE
![MetaStore remote database](https://github.com/gamboabdoulraoufou/hdp-5-HUE-installation/blob/master/img/hue_proxy.png)
- enable HDFS file access control lists (FACLs) (optional)
![MetaStore remote database](https://github.com/gamboabdoulraoufou/hdp-5-HUE-installation/blob/master/img/hue_acl.png)



> Configure HUE to start after reboot
```sh
# edit crontab as root
crontab -e 

# add the following line
#### START ####
#start HUE
@reboot sleep 120; /usr/local/hue/build/env/bin/supervisor -d
#### END ####

```

> Go to http://IP:8888 or http:hostname:8888



