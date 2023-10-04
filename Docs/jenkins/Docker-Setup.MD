## Install Docker
```sh
yum install docker
systemctl start docker
systemctl enable docker
systemctl enable docker.service
chkconfig docker on

```

## provide permissions to jenkins user in jenkins server to access docker
```sh
  sudo groupadd docker
  sudo usermod -aG docker jenkins
  sudo chmod 777 /var/run/docker.sock
```
## Add Jenkins user into sudoers file to get sudo access
```sh
   vi /etc/sudoers
   jenkins ALL=(ALL) NOPASSWD: ALL
```   
   
## Sudo Access
<a href="https://ibb.co/94pQLQK"><img src="https://i.ibb.co/jw8n2n0/sudo.jpg" alt="sudo" border="0"></a><br /><a target='_blank' href='https://imgbb.com/'>where to upload images</a><br />

