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

