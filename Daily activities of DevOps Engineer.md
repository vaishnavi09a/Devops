##Daily Activities in Jenkins

Maintenance of pipeline: If we have created any pipeline, we have check daily if there is any build failure, or if any build is taking longer taker check why is it taking too much time. So, maintenance of pipeline is task we must do.
Monitoring of pipeline: If any Jenkins agents are running properly or not in Jenkins, is there any performance issue due to memory etc. Jenkins shared library is up to date or not, do they require any changes or not.
Maintaining Jenkins: Maintain Master node and Agent in Jenkins, if there is any memory issue, CPU issue, needs to restart Jenkins. 
Credentials and secret management:  secrets are not exposed; backups and plugins are workings are working fine. 
During deployment, whatever you have written in script deployment and creating infra on cloud are being executed or not. Collaborate with developer if there is any new change so that we can add those in our feature.
Code quality check: Check logs. Builds, automation we have written are working fine in prod the way client required. Compliance check, no sensitive data exposure. In organization audit occurs in 2-3 months, we need to make sure sensitive data is not exposed.

##Daily Activates in Docker##
In docker, we are creating images, so we start our day we should check if any build or image creation is failed or not. If everything is fine, then the containers which are running are healthy or not, check logs or monitoring tools. 
In meeting if there is sometime new, we must work on, we can keep docker file updated discuss with various team. Optimization, maintaining and creating new image. Discarding old containers/images, look after memory also if it is getting piling up it will increase memory usage, focus on cleaning docker image. Tagging is important and removing old images, keep latest image. How many pull push requests are there.

## Daily Activities in Kubernetes
Monitoring – All cluster are healthy; pod status is running. Watch status in monitoring tool, 
Automation – Replica count is maintaining. work on scaling, horizontal pod autoscaler is working. If there is any upgrade request, cluster must be upgraded, patch apply Application deploy has to be upgrade.
CI/CD Operation – deployments are happening properly, reviewing deployed applications that are deployed using pipeline. Helm charts are working properly. If there is any failure rollbacks are working fine and if rollbacks are not working fine, then plan on investigating issue how rollbacks can be done. 
Terraform – Updating infrastructure creation scripts, whatever cluster we creating using CloudFormation, terraform, ansible. 
Security – Kubernetes secret management are used, network policy everything should be in place. Collaborate with developer to debug deployment issues.

## Daily activities in GitHub
Collaborating with team where the code will be kept, Provision infrastructure (IAC Scripts), Ansible scripts, Jenkins pipeline shared library scripts on GitHub.
Review PR Requests: Open PR Requests should be reviewed; code quality checks have passed. How to manage secrets, env variable in gitHub. Webhook is working fine.
Branching stratgegies
Updating documentation of new feature implemented

Daily activities in Terraform & Ansible
Terraform: Whenever we have requirement to create resource using terraform script if script is already there well & good, do necessary changes in script.
Check if there is any drift between terraform script and actual infrastructure.
If we are using modules, check if they are updated. If we are using different environments, then for those environments scripts are running. Remote backend, TF state file is working properly. Integrate with pipeline, if there is any failure then plan to rollback, debug the issue.
Ansible
Configuration Management: We must write playbook, test it out, run it and maintain inventory (servers in which all servers we must run that playbook) those servers need to be updated.
We must integrate playbook with CI/CD Pipeline. So that whenever pipeline runs then that playbook should get executed.
