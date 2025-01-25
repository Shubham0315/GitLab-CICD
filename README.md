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

GitLab Runner
-
- 


