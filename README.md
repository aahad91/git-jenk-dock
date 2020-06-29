![Docker-compose CI](https://github.com/aahad91/git-jenk-dock/workflows/Docker-compose%20CI/badge.svg?branch=master)
# git-jenk-dock
## Docker-based solution for GitLab, GitLab Runner, Jenkins and SonarQube

### Documentation for Installation, Integration, Plugins Installation and Pipeline Testing

#### Requirement

- Docker (Installed)
- Docker-compose (Installed)

### Installation

```bash
sudo docker-compose -f docker-compose.yaml up

#New terminal
sudo docker exec -it -u root jenkins chmod 777 /var/run/docker.sock
```

#### URLs

Browse to following Urls to verify successful installation of Gitlab, Jenkins and SonarQube.

- **Gitlab:** http://localhost:8081
- **Jenkins:** http://localhost:8095
- **SonarQube:** http://localhost:9000
  - **Login:** admin
  - **Password:** admin 

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

- Select the "Select plugins to Install" and enable gitlab.

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

#### Installing OWASP Dependency Checker for Jenkins

- Navigate to **_Manage Jenkins_** > **_Manage Plugins_**. Click on ***Available*** tab and search for OWASP Dependency-Check and click on Download now and install after restart.

![](images/jenkins-plugin-install-5.png)

![](images/jenkins-plugin-install-6.png)

- Verify the successfull installation of OWASP Dependency-Check plugin by navigating to **_Manage Jenkins_** > **_Manage Plugins_** and click on ***installed*** tab.

![](images/jenkins-plugin-install-7.png) 

### Integration of Gitlab and Jenkins

Sample [Jenkinsfile](https://github.com/aahad91/git-jenk-dock/blob/master/Jenkinsfile) for pipeline testing.

#### Gitlab

- Generate authentication token. *Navigate to **Settings** > **Access Token***. Do as follow:

![git-token](images/git-inti-1.png)

#### Jenkins

- Add connection to Gitlab from jenkins. *Navigate to **Manage Jenkins** > **Configure System***. Search for Gitlab tab. Add Name, Url of gitlab, token and test the connection as follow.

![add-conn](images/jenkins-inti-1.png)

![add-token](images/jenkins-inti-2.png)

### Test Pipeline

#### Gitlab

- Click on "Create a Project".

![git-pipline1](images/git-pipeline-1.png)

- Click on "Import Project", after that "Repo by URL" and paste the repo: **https://github.com/aahad91/git-jenk-dock.git**. Set project to public and finally click on Create project.

![git-add-project](images/git-pipeline-2.png)

#### Jenkins

- From Home page click on "New Item". Add the name for pipeline and select pipeline.

![create-pipeline](images/jenkins-pipeline-1.png)

- In pipeline section, select "Pipeline script from SCM" and set SCM to "Git". Afterwards add URL of the git repo.

![pipeline-config](images/jenkins-pipeline-2.png)

- Click on Build now to test the pipeline.

![run-pipeline](images/jenkins-pipeline-3.png)

- Verfiy the pipeline is executed successfully.

![](images/jenkins-pipeline-4.png)

### Gitlab Runner Integration

#### Gitlab

- Navigate to ***Admin Area*** > ***Runners*** and copy the ***Registration Token***.

![gitlab-runner1](images/gitlab-runner-1.png)

#### Gitlab Runner

```bash
# Command to register runner with gitlab
gitlab-runner register -n --url http://<gitlab-ip>:80/ --registration-token {token from gitlab} --clone-url http://<gitlab-ip>:80/ --executor docker --docker-image "docker:latest" --docker-privileged

# Execute
sudo docker exec -it gitlab-runner gitlab-runner register -n --url http://172.22.0.3:80/ --registration-token F8BoGetFnszYx91FT2ro --clone-url http://172.22.0.3:80/ --executor docker --docker-image "docker:latest" --docker-privileged
```

- Verify the added runner.

![gitlab-runner2](images/gitlab-runner-2.png)

### SonarQube

- Browse ot Url http://localhost:9000 

![](images/sonarqube-1.png)

- Click on login and enter the credentials:
  - Username: admin
  - Password: admin

![](images/sonarqube-2.png)

![](images/sonarqube-3.png)

#### Installing OWASP Dependency Checker for SonarQube

- Click on ***Administration*** -> ***Marketplace***. Type dependency-check in search bar and click install. 

![](images/sonarqube-4.png)

- Click on ***Restart Server*** on the top to proceed the installation.

![](images/sonarqube-5.png)

- Verify the successfull installation of OWASP Dependency Checker plugin. Navigate to ***Administration*** > ***Marketplace***, and click on Plugins installed.

![](images/sonarqube-6.png)

 