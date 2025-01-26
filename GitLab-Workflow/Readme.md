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
- 
  
