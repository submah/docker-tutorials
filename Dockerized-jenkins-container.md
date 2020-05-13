<img src="images/c4logo.png">




In this module we are going to learn about how to dockerized a jenkins container.

## For this setup we need below files
  * Dockerfile
  * default-user.groovy
  * executors.groovy

### Code for Dockerfile
```dockerfile
FROM jenkins/jenkins:latest

RUN /usr/local/bin/install-plugins.sh git matrix-auth workflow-aggregator docker-workflow blueocean credentials-binding

ENV JENKINS_USER admin
ENV JENKINS_PASS admin

# Skip initial setup
ENV JAVA_OPTS -Djenkins.install.runSetupWizard=false

COPY executors.groovy /usr/share/jenkins/ref/init.groovy.d/
COPY default-user.groovy /usr/share/jenkins/ref/init.groovy.d/

VOLUME /var/jenkins_home
```

### Code for default-user.groovy
```groovy
import jenkins.model.*
import hudson.security.*

def env = System.getenv()

def jenkins = Jenkins.getInstance()
if(!(jenkins.getSecurityRealm() instanceof HudsonPrivateSecurityRealm))
    jenkins.setSecurityRealm(new HudsonPrivateSecurityRealm(false))

if(!(jenkins.getAuthorizationStrategy() instanceof GlobalMatrixAuthorizationStrategy))
    jenkins.setAuthorizationStrategy(new GlobalMatrixAuthorizationStrategy())

def user = jenkins.getSecurityRealm().createAccount(env.JENKINS_USER, env.JENKINS_PASS)
user.save()
jenkins.getAuthorizationStrategy().add(Jenkins.ADMINISTER, env.JENKINS_USER)

jenkins.save()
```

### Code for executors.groovy
```groovy
import jenkins.model.*
Jenkins.instance.setNumExecutors(10)
```

### To Build Images from the Dockerfile
```
docker build -t custom-jenkins .  # You can change the tag name of the jenkins Image

```

### To run the jenkins container and access from outside
```
docker run -it --rm -p 8080:8080 f21558459467   # Provide your custom-jenkins-image-id

```
### To Make your jenkins data persistent  create a volume and mount to jenkins home
```
docker run --rm -it -p 8080:8080 -p 50000:50000 -v jenkins-vol:/var/jenkins_home 1ce8a7d1aafc

```
