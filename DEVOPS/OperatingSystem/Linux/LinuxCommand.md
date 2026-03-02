# Linux Command

1) sudo : super user
2) wget : download from internate
3) -O : on which path

```Bash
sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian/jenkins.io-2026.key
```

4) systemctl : system control who can start, stop and give status information
```BASH
systemctl status jenkins
```

5) sudo systemctl enable <Application name> : When we want start our application when the system get restart
```BASH
 
sudo systemctl enable jenkins
```

6) cat : to see the file content
```BASH
 
Syntax : sudo cat <filePath/fileName>
 
Example : sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```