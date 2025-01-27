# GITLAB

- GitLab is a tool which gives project management capabilities. GitLab has integrated CICD features
- If we make EC2 instance on AWS where we want to run GitHub for our organization, it is not free of cost. It needs GitHub enterprise edition. In short we cannot run Github on our own instances, we've to run it on cloud which is Github.com
- We can run GitLab on our instance, for our team. We can make our instance self hosted
  If we do docker run gitlab/github :- Here **we can run gitlab in docker container not github** , which makes GitLab open source whereas GitHub is run by microsoft.

  - We can run Gitlab on our own system
    > GitLab is specifically used for CICD, DevOps and DevSecOps
    > BitBucket is for project tracking and management
    > GitHub is for open source contributions

How to use GitLab?
-
- Suppose we've groups like DevOps, scripts, Docs in our organization. Group is a collection of team members and their projects. Members who are part of particular group will've access to that group.
- To give access to particular kind of projects, we can make separate group and provide access. However in GitHub we've repositories under our username (which is the only group).
  In **GitHub we call repositories and in GitLab we call it as project.**

- Syntax :- **https://gitlab.com/{group}/{project}**
  
- We can create group and projects under them as per requirement and add members if necessary granting them access. So when we invite members, invite will go to them and they will accept to checkout project.

- We need SSH key or SSO for push, pull or any other operations to perform on gitlab. If we want to use through HTTPS, we need personal access token. There is no password kind of thing in gitlab.

Steps to add SSH key
-
- Launch t2-micro/ubuntu EC2 instance in AWS with a key pair and allow HTTP/HTTPS traffic.
- When instance is ready, connect using SSH command inside of instance (take command like below)
 > ssh -i "key-pair" ubuntu@ip.region.compute.amazonaws.com
- Connect to the instance
- To connect this EC2 and our Gitlab server, run below
   **ssh-keygen --> enter --> enter --> key is ready (public+private)**
- Go to cd .ssh , here we can see 2 keys **id_ed###** and **id_ed###.pub**.
- To push/pull code from this EC2 to our Gitlab, private key will be on EC2 and public key will be on Gitlab. So copy the public key and add SSH key so that key gets registered with our Gitlab account.

- Now in project, we can go to code and clone it with SSH (Copy the link of project)
  Go to instance console, make one dir, and do git clone and connect. In this way we've cloned private repo via SSH
  Command :- **git clone git@gitlab.com/$group/$project**

Import Project
-
- To import from Github, choose "Repository by URL" and use any github repo
  Put the repo URL and choose group under which we've to copy. Create project.
- Just in case if anyone makes changes on our repo in Github and we want to replicate those changes automatically on Gitlab, we can use **"Mirror this Repository"**.

- In Github there is "Pull request" and in Gitlab there is "Merge request"

x
-
Creating Pipelines
-
- To create pipelines we dont need jenkins kind of tool. All features are there in gitlab.
- To create pipelines, create new file :- .gitlab-ci.yml. Here key-value pair is used.
- Gitlab CI works on 2 things :- stages and jobs. In CICD pipeline we've stages and inside stages we've jobs (In jenkins inside pipeline, there're stages and inside stages there're steps).
- Suppose we've 4 stages to perform :- build, test, push, deploy. We've to define those stages in gitlab yml file
  If we've build_job inside build stage and we've to run some script inside it.
- Using "script" keyword inside yml we can run shell scripts. Create jobs for stages in our pipeline as below and create file. As soon as we create yml file, our pipeline runs.

-**For gitlab yml keywords(cheat sheet) :- https://cheatography.com/violaken/cheat-sheets/gitlab-ci-cd-pipeline-configuration/
**  
-

![image](https://github.com/user-attachments/assets/eaa2e0b6-6a7b-4718-a26b-9b6b767178ff)

![image](https://github.com/user-attachments/assets/49761f45-a458-4dcd-b296-5d0adddd0755)


- Once we commit this gitlab-ci.yml file in our project, Build option gets unlocked for ur in the left console where we can make pipelines, check jobs, check pipeline syntax using pipeline editor. Check below SS:-

![image](https://github.com/user-attachments/assets/7613d964-5341-4393-8477-40eac2399879)

- In jenkins we dont deploy/execute jobs on master node. Here in Gitlab we havent created/added agents like slaves so how this is getting deployed here??
  Go to Settings --> CICD --> Runners
  So here in Gitlab we've runners to run jobs unlike agents in jenkins. Runners are processes that pick up and execute CICD jobs for gitlab

- Here are 2 types:-
  - Project runners :- self hosted we can setup own runner creating EC2
  - Instance runners :- all over world where we can deploy our projects freely. Only requirement is runner should be in active state.
- So we can make our own runners as well as use Gitlab runners.

![image](https://github.com/user-attachments/assets/9053b4d8-bd86-415e-85a1-2640f889f113)

- We can edit CI files in various ways :-
  - pipeline editor - to highlight syntax errors
  - Web IDE - We can make GITLAB IDE for our project and manage our project there. Commit files and apply.
  
![image](https://github.com/user-attachments/assets/d4d8eac0-ff09-4701-a6c6-efe4cd6ebacc)

  Here we can have multiple jobs running in one stage in parallel. Just give stage name like below in IDE and commit the changes. (Suppose we've to test in prod, dev and test parallely)

![image](https://github.com/user-attachments/assets/db1d2fd6-9404-4a6b-a973-e489685f793d)

  Now when we go to pipeline, we can see our pipeline is triggered automatically and also check how parallel builds are executed. 
  
![image](https://github.com/user-attachments/assets/151c2518-958f-4f21-a421-9ec1b7ebc795)

![image](https://github.com/user-attachments/assets/73d4b496-dac2-4b4d-9223-e4785c2aa6bf)

 In the logs we can also check which runner is being used by particular job.

<img width="831" alt="image" src="https://github.com/user-attachments/assets/95ad04e0-8ed0-443f-a162-246c7dcafd74" />

Variable
-
- To use passwords, secrets go to IDE. In build_job we have to pass project name in echo command. There are some inbuilt variables like $CI_PROJECT_NAME, $CI_COMMIT_AUTHOR. We can also define variable on own (user defined variables). For that refer below SS :-

![image](https://github.com/user-attachments/assets/eba58c64-278e-46cf-873f-66af544c6ef9)

- Here - is NA as we're creating variable objects not list of variables just like we do in docker compose for env.
- Output for above variables is as given below:-

![image](https://github.com/user-attachments/assets/4330da28-ca3b-41dd-9cbf-8b4dc9a285c1)

![image](https://github.com/user-attachments/assets/9d9c2a05-f3d4-49f4-919b-5bc09e0b666c)

![image](https://github.com/user-attachments/assets/9f13f5fe-766a-48a5-bcc1-c18f83ccd93f)
  
![image](https://github.com/user-attachments/assets/00e2777e-41b3-47b5-85ea-c27736e342d5)

![image](https://github.com/user-attachments/assets/5f4af1de-c726-494e-833e-f83a2bcb620c)

Secrets
-
- Go to CICD --> Variables
  To add variable we need to provide type, environment, description, visibility, etc. We can do like below for our dockerhub credentials. Keeping them masked.
  Protected variable :- to use variable for specific branches only.

![image](https://github.com/user-attachments/assets/03b6880f-843a-41ee-96d4-b8831e252636)

![image](https://github.com/user-attachments/assets/0a05dd04-53e0-421b-bd39-365143a579f7)

 For password variable create Personal Access Token in DockerHub
 Go to Account --> Settings --> Personal Access Token --> Generate new token --> Copy the token --> Add to variable as password for dockerhub

![image](https://github.com/user-attachments/assets/5887ee3e-920c-4a1e-9961-ef44cede3743)

<img width="939" alt="image" src="https://github.com/user-attachments/assets/e53eba2e-8392-452a-ad6b-abe828de9e32" />

![image](https://github.com/user-attachments/assets/94683357-347c-4389-95b9-2817067682da)

Now we've below 2 variables which are not visible to anyone as they're masked

![image](https://github.com/user-attachments/assets/bf4078ac-fedd-4968-b66d-423a89710c3c)

- To use these custom variables, go to IDE and edit the yml. We can see our username is masked.

![image](https://github.com/user-attachments/assets/1fa551f0-5b8f-4863-9913-bb147795bfb3)

![image](https://github.com/user-attachments/assets/cc939a91-f087-4f6c-b581-5e22c1c95dde)

Artifacts
-
- Suppose, we've run some test cases and it generated logs or reports which we want to be downloaded in a file.
  So the things which we can collect from the pipelines to share with others are called as **Artifacts**
- In short artifacts means we've to store logs of pipeline at some place.

- Go to CICD --> Artifacts --> Keep artifacts from most recent successful jobs
- Now we've to use those artifacts in our pipeline

![image](https://github.com/user-attachments/assets/6cba8f08-b76a-4e2d-8050-ee2c54237eb9)

- Now go to IDE and lets say we need artifacts of test_job and we've to store logs in **app.log** file. But we've to tell our job where is artifactory of this (mention path). app.log is a file which we're preserving from script/job.
- Here we're creating one folder called "**logs**" which is artifact folder for logs. We can also set expiry for logs using **"expire_in:"**
- Here we need to create directory as well when we need to create folder of our name. 

![image](https://github.com/user-attachments/assets/daa8d6ff-fba7-413f-aad4-48672d23c825)

- Now we can go to artifacts we can see 2 type of files generated under "deploy_job" and "test_job"

![image](https://github.com/user-attachments/assets/5da06704-6de3-45d8-b6fc-8456a1bca739)

 Download those files, we can see the logs in downlaoded files.

Runners
-
- 2 types of runners :- Self hosted and SaaS(Instance)
- Instance runners have Gitlab software installed and they run our pipelines. If we go to our pipeline, we can see on which runner the job was run.

<img width="831" alt="image" src="https://github.com/user-attachments/assets/7783ccc4-cc00-4935-aa29-cc6f501482ef" />

- If we want the pipeline to run on our runner/platform, go to CICD --> Runners --> New project runner
  Specify tags like dev,prod, staging so that jobs get assigned to these runners (In jenkins runners mean agents).

![image](https://github.com/user-attachments/assets/4b9a97b7-0afc-44b7-95c2-84f05f345b36)

- When we create runner, we can have docker container, k8s as runner or linux instance as runner. Only condition is Gitlab runner must be installed before we register a runner.

![image](https://github.com/user-attachments/assets/d5c54cba-6bf2-4c3a-89ac-938173d1636e)
