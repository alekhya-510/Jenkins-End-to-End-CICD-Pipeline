# Jenkins-End-to-end-CICD-Pipeline
In this project we will deploy a java spring boot application to a EKS cluster

We are going to deploy a java spring boot application to Kubernetes EKS cluster, during the process we will use following tools:
In this process CI and CD implemented separately:
**Continuous Integration(CI):**
Git: For source code we will be using git.
Maven: To build the java application we have used maven
SonarQube: Once the code is build, test the using SonarQube.
Docker: After building and static code analysis we need to containerize, this will be achieved by using docker. Docker image will be build and pushed to dockerhub.
Jenkins: For Continuous integration , we are using Jenkins.
Image Updating : In this pipeline , using shell script we have updated the image and build no.
 
**Continuous Deployment(CD):**
AWS EKS : To create the Kubernetes cluster , we have  used AWS EKS.
ArgoCD :  This is Gitops based, continuous delivery tool kit for Kubernetes. For this we will install argo cd operator in Kubernetes cluster and access the argocd ui and integrate git repository and Kubernetes cluster for deployment. 
Finally we deployed the java springboot application in EKS cluster.

**Deploying the application locally and accessing through your browser:**
Before deploying to EKS cluster , we can check locally that how the application is working.
Clone the git repo and move to the directory :

```
git clone https://github.com/alekhya-510/Jenkins-End-to-End-CICD-Pipeline.git
cd java-maven-sonar-argocd-helm-k8s/sprint-boot-app
```

The application is build using maven tool, install maven locally and once done,build using following command:

```
mvn clean package
```

Execute locally using java , access the application http://localhost:8080

```
java -jar target/spring-boot-web.jar
```

Using Docker , application can be accessed as below:

```
docker build -t jenkins-cicd:v1 .
```
```
docker run -d -p 8010:8080 -t jenkins-cicd:v1
```


<img width="1728" alt="Screenshot 2025-04-02 at 15 47 02" src="https://github.com/user-attachments/assets/e4fd2c47-2c7d-46cf-ae6f-c18cca59d2ac" />

Hurray!! We are able to access the application.


**Step 1: Creating EC2 instance**

Since we are installing jenkins , docker and sonarqube it should be large instance.The specification is as below:
**Instance type** : t2.large 
**O.S** : Ubuntu 
**Storage**: 25Gb 
**Security group**: we need to open ports for SSH,HTTP & HTTPS

<img width="1457" alt="Screenshot 2025-04-02 at 15 51 20" src="https://github.com/user-attachments/assets/bc768207-a078-4682-bdbe-b211734c1e44" />

**Step 2: Installing Jenkins**

ssh to the instance and install the jenkins as below:

ssh -i <pvt.key> user@<public-ip>

Install java:

```
sudo apt update
sudo apt install openjdk-17-jre
```

Install Jenkins:

```
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins

```

Jenkins Login Page:

<img width="1725" alt="Screenshot 2025-04-02 at 16 44 27" src="https://github.com/user-attachments/assets/b80056f1-23fc-41e9-9ada-f4006e9960b4" />



