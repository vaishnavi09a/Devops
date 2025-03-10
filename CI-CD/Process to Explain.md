# HOW TO ANSWER CICD PROCESS IN AN INTERVIEW| DEVOPS INTERVIEW QUESTIONS

We use GitHub as Version Control System and out target platform is Openshift

We make changes using Github creates a code commit, Raise PR and code is reviewed by code owner, then we use pipeline Orchestrature Jenkins for CI-CD Process.

(Reason: whenever there is code commit to Github repo git webhook triggers pipeline to jenkins).
In Continuos Integration, 

1.checkout code commit that user has made along with whole code, then check Naming convention of branch name is correct with valid JIRAID.

2.Then we perform build action(using MAVEN) along with unit testcase in code repo we use unit testing framework(with bad case and good case scenario).

3. As part of code scanning we use sonarqube to scan code for checking if there is any vulnernability and security check to ensure our code.

4. As part of Building image, OpenShift Container Platform uses Kubernetes by creating containers from build images and pushing them to a container image registry.
OpenShift Container Platform uses Buildah to build a container image from a Dockerfile.

5. Once to image is build, it is important to perform image scanning.In image scanning, we check the image we have created have some vulnerabilities.

6. Finally you push image to image registry. So image registry can be dockerHUb ECR in AWS.

These are above steps we persion in continous Integration. we use Scripted Jenkins Pipeline.

**Scripted Pipeline** is the original pipeline syntax for Jenkins, and it is based on Groovy scripting language. In Scripted Pipeline, the entire workflow is defined in a single file called a Jenkinsfile. The Jenkinsfile is written in Groovy and is executed by the Jenkins Pipeline plugin.

Then we use same jenkins pipeline and update this image in the k8 yaml manifest and you to again push this updated image to a helm chart(for storing your image manifest)

**A Helm chart** is a collection of files that define and manage Kubernetes applications. Charts are packages that contain all the resources needed to deploy an application to a Kubernetes cluster. 

7.Once the updated k8 image manifest pushed to gitHub repo then what we do as part of same pipeline using helm command we just push this new commit in git repo to k8 platform.
