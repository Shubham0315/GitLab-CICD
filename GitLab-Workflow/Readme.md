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
  > ssh-keygen --> enter --> enter --> key is ready (public+private)
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
- To create pipelines, create new file :- .gitlab-ci.yml. Here key-value 
  
