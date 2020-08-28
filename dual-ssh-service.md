## Make more than one Instances of openssh-server on single machine  



#### Make a copy of the sshd_config  

`cp /etc/ssh/sshd_config /etc/ssh/sshd_new_config`  



#### Edit sshd-second_config to assign a different port number  

###### Uncomment Port and add a custom port

`Port 2022`

#### Make a copy of the systemd unit file for the sshd service.  

###### For Ubuntu :  

`cp /etc/systemd/system/sshd.service /etc/systemd/system/sshd_new.service`  

###### For CentOS :  

`cp /usr/lib/systemd/system/sshd.service  /etc/systemd/system/sshd_new.service`

#### Alter /etc/systemd/system/sshd_new.service file

###### Add the -f /etc/ssh/sshd_new_config option to sshd, so that the alternative configuration file is used  

    Description=OpenSSH server second instance daemon
 
    ExecStart=/usr/sbin/sshd -D -f /etc/ssh/sshd_new_config $OPTIONS

#### Start the Service :  

`systemctl daemon-reload`  

`systemctl start sshd_new`
