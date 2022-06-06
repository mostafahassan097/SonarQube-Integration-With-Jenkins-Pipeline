# SonarQube
## Install SonarQube Using Helm Chart
### Helm
- Add SonarQube Repository
```sh
helm repo add sonarqube https://SonarSource.github.io/helm-chart-sonarqube
helm repo update

```
- Create Namespace and install SonarQube with ingress from file values 
```sh
kubectl create namespace sonarqube
helm upgrade -f values.yaml  --install -n sonarqube sonarqube sonarqube/sonarqube
```

- Access SonarQube From The Browser
```sh 
kubectl port-forward  sonarqube-ingress-nginx-controller 8080:80 -n sonarqube  
```
![Build Status](https://github.com/mostafahassan097/SonarQube-Task/blob/master/Imgs/1.png)

![Build Status](https://github.com/mostafahassan097/SonarQube-Task/blob/master/Imgs/2.png)

![Build Status](https://github.com/mostafahassan097/SonarQube-Task/blob/master/Imgs/3-1.png)

### Steps To Install Jenknis and Intgrate with Sonar Qube:

- Apply jenkins resources
```sh
kubectl apply -f /apply-jenknis/jenkins
```
- Check Logs to get password of jenkins to configure
```sh
kubectl logs -f {POD_NAME} -n jenkins
```
- Create Key Pair for JENKINS 
```sh
ssh-keygen -t rsa -f {Name_OF_Key}

cat {Name_OF_Key}.pub

```
- Connect Slave to master
```sh
kubectl exec -it {POD_NAME_Slave} -n jenkins -- sh 
#Start SSH Service
service ssh start 
#enter any passwd
passwd jenkins
#switch to user jenkins
mkdir .ssh
echo "Public_Key_Content" > .ssh/authorized_keys
```

![Build Status](https://github.com/mostafahassan097/SonarQube-Task/blob/master/Imgs/3.png)
![Build Status](https://github.com/mostafahassan097/SonarQube-Task/blob/master/Imgs/4.png)
![Build Status](https://github.com/mostafahassan097/SonarQube-Task/blob/master/Imgs/5.png)
![Build Status](https://github.com/mostafahassan097/SonarQube-Task/blob/master/Imgs/6.png)
- Install SonarQube and NodeJS Plugins
![Build Status](https://github.com/mostafahassan097/SonarQube-Task/blob/master/Imgs/7.png)
- Create Token for Jenkins in SonarQube
![Build Status](https://github.com/mostafahassan097/SonarQube-Task/blob/master/Imgs/8.png)

- Configure SonarQube Plugin

1- Create Credentials for  SonarQube using token created above
![Build Status](https://github.com/mostafahassan097/SonarQube-Task/blob/master/Imgs/9.png)

2-  Configure Sonarqube Server Dashboard >> configuration
![Build Status](https://github.com/mostafahassan097/SonarQube-Task/blob/master/Imgs/11.png)
3- Configure SonarQube Scanner and NodeJS  From Dashboard >> Global tool configuration
![Build Status](https://github.com/mostafahassan097/SonarQube-Task/blob/master/Imgs/12.png)
![Build Status](https://github.com/mostafahassan097/SonarQube-Task/blob/master/Imgs/17.png)
3-  Create Pipeline to test code of this  [REPO](https://github.com/mostafahassan097/NodeJs-SonarQube) Using SonarQube
![Build Status](https://github.com/mostafahassan097/SonarQube-Task/blob/master/Imgs/13.png)
![Build Status](https://github.com/mostafahassan097/SonarQube-Task/blob/master/Imgs/14.png)
![Build Status](https://github.com/mostafahassan097/SonarQube-Task/blob/master/Imgs/15.png)
![Build Status](https://github.com/mostafahassan097/SonarQube-Task/blob/master/Imgs/16.png)


- Install Multi Branch Plugin


```sh
helm upgrade -f values.yaml  -n sonarqube sonarqube sonarqube/sonarqube \
 --set "plugins.install={https://github.com/mc1arke/sonarqube-community-branch-plugin/releases/download/1.11.0/sonarqube-community-branch-plugin-1.11.0.jar}" 
```

![Build Status](https://github.com/mostafahassan097/SonarQube-Task/blob/master/Imgs/18.png)
![Build Status](https://github.com/mostafahassan097/SonarQube-Task/blob/master/Imgs/19.png)
![Build Status](https://github.com/mostafahassan097/SonarQube-Task/blob/master/Imgs/20.png)
![Build Status](https://github.com/mostafahassan097/SonarQube-Task/blob/master/Imgs/21.png)
![Build Status](https://github.com/mostafahassan097/SonarQube-Task/blob/master/Imgs/22.png)
![Build Status](https://github.com/mostafahassan097/SonarQube-Task/blob/master/Imgs/23.png)

