# git-jenk-dock
## Docker-based solution for GitLab and Jenkins

### Documentation for Installation and Integration

#### Requirement

- Docker (Installed)
- Docker-compose (Installed)

### Installation

```bash
sudo docker-compose -f docker-compose.yaml up
```

#### Urls

Browse to following Urls to verify successfull installation of Gitlab and Jenkins

- **Gitlab:** http://localhost:8081
- **Jenkins:** http://localhost:8081

#### Gitlab Configuration

- After browsing to above mentioned url of gitlab, initial registration page will show up. Set the new password for root user of Gitlab.

![root-password-set](images/git-config-1.png)

- Login with the newly created password

![root-login](images/git-config-2.png)

- Gitlab Homepage

![git-home](images/git-homepage.png)

#### Jenkins Configuration

- Browse to above mentioned url of jenkins and get the Administrator password from the mentioned path:

```bash
sudo docker exec -it jenkins cat /var/jenkins_home/secrets/initialAdminPassword
```

![jenkins-conf](images/jenkins-config-1.png)

- Select the "Install suggested plugins".

![jenkins-plugins](images/jenkins-config-2.png)

- Wait till all the plugins are installed.

![plugins-install](images/jenkins-config-3.png)

- Set Admin user and password.

![user-create](images/jenkins-config-4.png)

- Set the default url for jenkins for 3rd party access. For-example integration with gitlab and email configuration.

![instance-conf](images/jenkins-config-5.png)

- All set!

![jenkins-installed](images/jenkins-config-6.png)

- Jenkins Homepage

![jenkins-homepage](images/jenkins-config-7.png)
