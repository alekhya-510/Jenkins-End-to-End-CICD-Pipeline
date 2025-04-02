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

'''
git clone https://github.com/alekhya-510/Jenkins-End-to-End-CICD-Pipeline.git
cd java-maven-sonar-argocd-helm-k8s/sprint-boot-app
'''

The application is build using maven tool, install maven locally and once done,build using following command:

'''
mvn clean package
'''

Execute locally using java , access the application http://localhost:8080

'''
java -jar target/spring-boot-web.jar
'''
<img width="1728" alt="Screenshot 2025-04-02 at 15 43 11" src="https://github.com/user-attachments/assets/81ddcc18-9951-4b05-b3ba-2744eedf6075" />

Step 1: Creating EC2 instance
Since we are installing jenkins , docker and sonarqube it should be large instance.The specification is as below:
Instance type : t2.large
O.S : Ubuntu
Storage : 25Gb
Security group: we need to open ports for SSH,HTTP & HTTPS



