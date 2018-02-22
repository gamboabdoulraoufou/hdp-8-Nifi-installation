### hdp-8-Nifi-installation

> Install Nifi

```sh
# log as root
sudo su - root

# download 
wget http://public-repo-1.hortonworks.com/HDF/3.1.0.0/nifi-1.5.0.3.1.0.0-564-bin.tar.gz

# unpack package
tar -xzvf nifi-1.5.0.3.1.0.0-564-bin.tar.gz

# create hue directory
mkdir -p /usr/local/nifi

# Copy untar binaries into the new folder
mv nifi-1.5.0.3.1.0.0-564/* /usr/local/nifi

# go to hue directory
cd /usr/local/nifi
```



> Configure Hadoop cluster to accept connections from HUE:
- ensure WebHDFS is enabled
![MetaStore remote database](https://github.com/gamboabdoulraoufou/hdp-5-HUE-installation/blob/master/img/hue_web_hdfs2.png)
- proxy user hosts and groups for HUE
![MetaStore remote database](https://github.com/gamboabdoulraoufou/hdp-5-HUE-installation/blob/master/img/hue_proxy.png)
- enable HDFS file access control lists (FACLs) (optional)
![MetaStore remote database](https://github.com/gamboabdoulraoufou/hdp-5-HUE-installation/blob/master/img/hue_acl.png)


> Start Nifi
```sh
/usr/local/nifi/bin/nifi.sh run
 ```
 
 > Stop Nifi
```sh
/usr/local/nifi/bin/nifi.sh stop
 ```
 
 
> Configure Nifi to start after reboot
```sh
# edit crontab as root
crontab -e 

# add the following line
#### START ####
#start Nifi
@reboot sleep 120; /usr/local/nifi/bin/nifi.sh run
#### END ####

```

> Go to http://IP:8888 or http:hostname:8888



