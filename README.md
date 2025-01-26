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




