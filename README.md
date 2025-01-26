# GitLab-CICD

- GitLab is web(cloud) based devops lifecycle tool which we can access by cloud and perform devops actions.
- It provides features like
  > CICD Pipeline features
  > Collaboration on code and project management
  > Monitoring and security
  > To automate various parts of software development :- Building, Testing, Deploy

CI/CD
- 
- It is method of ferquently delivering apps to customers by introducing automation into the satges of app development

Set Up GitLab
-
- Using GitHub credentials we can sign in to GitLab otherwise create new account

![image](https://github.com/user-attachments/assets/05b180de-c685-4fad-8df5-dc1ddc094d76)

![image](https://github.com/user-attachments/assets/9c617d3f-1941-43e5-b96e-0562f5d00124)

![image](https://github.com/user-attachments/assets/12f6a848-2044-441e-a050-1820b3a92de8)

- After this we can see below GitLab dashboard

![image](https://github.com/user-attachments/assets/a72dc2b9-7338-49ba-8935-9768b70b6163)

Creating First Pipeline
-
- Create a new file named ".gitlab-ci.yml" based on yaml syntax
- Add the steps as required and commit the changes

![image](https://github.com/user-attachments/assets/df607ed2-a542-47e6-ab71-a76d842b75b6)

- But here we get error "This GitLab config is invalid". After editing in "Edit pipeline" we get message that "Pipeline syntax is correct"

![image](https://github.com/user-attachments/assets/0017ae76-f9d3-4902-92d0-260fd1365d20)

- When we create file and commit the required changes, the file/pipeline will run automatically. We can see what execution is being done on pipeline in the background in terms of logs just like console output in Jenkins
- Here we can see GitLab runner gets assigned to pipeline to run. This runner will "prepare dcoker-machine executor" means it will take docker container which is lightweight and ran our pipeline in it. So docker container acts as env for our pipeline to run. Changes in our git repo is taken by runner and it executes in container.

![image](https://github.com/user-attachments/assets/ee295796-b2c7-4bc0-8225-5ca2b6991482)

Multiple Jobs
- 
- Make 3 jobs :- build, test and deploy in our yml file. When we commit changes, pipeline will auto-run.

![image](https://github.com/user-attachments/assets/f90a13ed-9597-401f-82bb-13baa39e0df2)

![image](https://github.com/user-attachments/assets/c6d15e93-b63b-4b00-8758-62b5e551c45c)

- Here all jobs are running parallely. But we want step by step execution
  For this, we can provide stages section in our pipeline and then pipeline will execute in sequence of the stages written.
  But for runner to understand which is build stege or any other, we can provide stages name inside jobs
  Also we can see all 3 jobs are connected. We can also see logs related to specific job.

![image](https://github.com/user-attachments/assets/a17a2070-2493-445d-84bd-e7212d07ceee)

![image](https://github.com/user-attachments/assets/7351dcf3-2917-47ec-bae6-4d3e7a337b5f)

- Here for pipeline to run, it take more time compared to jenkins as iyt is shared platform, free, online tool. Also gitlab runners for running pipelines are shared, so execution is slow

-  What if our "build" step is unsuccessful. Make spelling mistake for echo as "echos"
  This step will fail and subsequent stages of test and deploy will not run, they will get skipped. Even if build is not success we've to run test or deploy we can run them manually
  Here GitLab manages failure cases.

![image](https://github.com/user-attachments/assets/6b144d09-6c6a-43dc-9ea4-124562aefa09)

- In pipelines section we can check overall status of all builds.

![image](https://github.com/user-attachments/assets/15beee12-e11b-409b-8803-0b05357f4aa5)

Before and After Script
-
- If we define before/after script outside job, it is applicable for all 3 jobs. We can also define this inside specific job so that it will be applicable for only that job.
- Whatever we need to perform before/after script, this section will handle.
- Before script is done when we need to check if the env is proper before build, dependencies are available or not or updating app.
- After script is done when we have performed many operations and we've to cleanup the things

![image](https://github.com/user-attachments/assets/c6adb5f3-373b-4576-b7ab-ce6d795e4374)

- We can see the logs of build stage to cjheck the same

Running BASH Script
-
- Write a script to create a file and then append it with some text. Commit the changes.

![image](https://github.com/user-attachments/assets/b9ba7ee0-ff35-4a90-ad7d-58d885cefa79)

- Now to run this bash script go to gitlab.yml file and edit.

![image](https://github.com/user-attachments/assets/545bb4ef-21a7-4f91-b7ae-ebd246370bb3)

- We can see logs of the same. Here we're not just printing on console, we're also making file. But this file will get vanished once we execute the pipeline. To preserve the file we can use GitLab artifacts.

GitLab Artifacts
-
- In the existing gitlab.yml file, add mkdir, create a newfile. To save this, use artifacts.
  In artifacts we can use "paths" to preserve specific file/location

![image](https://github.com/user-attachments/assets/3a71551c-e7e7-4e9a-a473-9944cf47c922)

- To preserve artifacts mean we can preserve files getting created inside our job
- After committing, we can see our job getting failed

![image](https://github.com/user-attachments/assets/31fdfe5e-a530-457a-ba17-dfbb0f9fb777)

For this go to our GitLab.yml file as this is conceptual error, not syntax error. So do as per below ss to fix (copy the bash file in our folder created)

![image](https://github.com/user-attachments/assets/c047979a-e50b-4e98-84d1-6feb425b70d7)

- So after the pipeline is run, we can see "JOB ARTIFACTS" at the right side with options "Keep/Download/Browse"

![image](https://github.com/user-attachments/assets/45047e26-6eac-43c5-8e73-6e0f1e3ecb8c)

- If we click on "Browse" we can see our folder created and files inside it.

Pipeline Auto Run
-
- Even if we do changes in our script file, our pipeline will run automatically. And we can see our added content in logs as well.

Environment Variables
-
- Go to Settings --> CICD --> Variables --> Add
  Define type and environment. Provide "Key" and "Value" (Lets say Key and value :- Name and Gitlab

![image](https://github.com/user-attachments/assets/218a760d-5bde-4b5d-8487-114f9d6bc483)

![image](https://github.com/user-attachments/assets/034d3f75-1f8d-44d1-97c8-e5cf456c9fb3)

- Create another variable using "masked" visibility

![image](https://github.com/user-attachments/assets/bf267b68-5e89-4942-82ba-6d166e2da026)

- Now go to repo yml file and add variables here (pass the variables in script). Inside logs we can see values of both key variables

![image](https://github.com/user-attachments/assets/dad61da7-90d2-4bb9-9a36-b342b2160659)

![image](https://github.com/user-attachments/assets/99e0263e-8f65-4f38-ba3e-d04f88d4fcf9)

Email Notification
-
- Lets edit the yml file and make mistake. We'll get notified that our pipeline is failed through email. If we correct the error we get mail as pipeline is fixed


Schedule Jobs using CRON
-
- Usually when we do changes in file, our pipeline gets run. But we want to run the pipeline at desired time without manual need. This will help run pipelines periodically when we're not on screen.
- Go to Build --> Pipeline Schedules --> Create a new pipeline schedule --> Select timezone, pattern and create pipeline
- Creating this will also give us "Next run timings"

![image](https://github.com/user-attachments/assets/663d5d10-63f0-486a-9dc2-5ddd57c5dd2d)

![image](https://github.com/user-attachments/assets/1d7154f7-77ae-4b1c-a2f8-b35f73cb890e)

Manual Deployment
-
- Add when: clasue in script as below.

![image](https://github.com/user-attachments/assets/83b7ad13-221c-4e77-89ec-528707539d7d)

- When we commit changes, our build and test stages get executed but deploy stage will wait for our manual instruction. So we can press play button here to run the stage

![image](https://github.com/user-attachments/assets/d2cb8b41-62cf-4f95-836c-98ea6061b61f)

Pre-defined Variables
-
- We can use those variables in scripts without defining them. Used for logging purpose
- One of them is :- CI_COMMIT_AUTHOR, expmple of use case is below. We can see author name(username and email) in logs as well.

![image](https://github.com/user-attachments/assets/51e21299-e0e7-42ba-9f2a-e7ab5eb4f151)

![image](https://github.com/user-attachments/assets/c4af457b-8bfd-4fed-ab78-733b02ba0da6)

Working with GIT:- Import GitHub project
-
- Now we've to use the imported GitHub project in pipeline
- Create new project in GitLab. Here we can see option of "Import Project" --> select GitHub --> Authorize using GitHub

![image](https://github.com/user-attachments/assets/cf42013a-4bfa-43d4-9ac0-8536951b83cc)

![image](https://github.com/user-attachments/assets/d1eeb690-2f39-42d2-bbc4-35e8df845e0b)

![image](https://github.com/user-attachments/assets/ee781437-81cf-4700-bf21-284f8754cace)

- Once this is done, we get below page where we can see GitHub repos inside our GitLab console and we can select "Import" option for the repo we want.

![image](https://github.com/user-attachments/assets/23cac856-87f1-47f5-a8f0-b8c742cef4a4)

![image](https://github.com/user-attachments/assets/85cd4661-a09d-444b-9844-62d8cc69cfd0)

![image](https://github.com/user-attachments/assets/768b32be-db93-4cfb-a786-c64fd654a481)

- By default, ruby image is used for GitLab CICD. We can change that. To run our code using custom images, we can use like below

![image](https://github.com/user-attachments/assets/e855c7bb-6e61-4646-9b9c-3a252fb92c34)



