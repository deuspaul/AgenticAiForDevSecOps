1)	For this lab, we will need to make sure the build service will have permissions to interact with the git repository
Click on project settings > repositories > security
Select the ado-ai Build Service user and make sure the following are set to allow:
bypass policies when pushing: Allow
Contribute: Allow
Create branch: Allow
Create tag: Allow
Read: allow
![image](./images/lab5/lab5-1.png)

<br/>

2)	Go back to GitHub Codespaces, and make sure you are on the main branch and pull changes

<br/>

3)	Input the following prompt in GitHub Copilot:

As a highly experienced release manager, help us release this application and add release notes, avoid using powershell.
Step 1: create a new branch for these changes
Step 2:  add a step in the azure devops pipeline to create the git tag for this release using semantic versioning 
Step 3: add a step in the azure devops pipeline to create the release notes in a changelog file
Step 4: add a step in the azure devops pipeline to zip the application and publish it as an artifact
![image](./images/lab5/lab5-3.png)
![image](./images/lab5/lab5-3-2.png)
<br/>

4)	Next, publish the branch (or commit changes if needed)
![image](./images/lab5/lab5-4.png)

<br/>

5)	Next, review the pipeline to make sure everything looks good:
![image](./images/lab5/lab5-5.png)

<br/>

6)	And merge it to the main branch by creating a pull request:
![image](./images/lab5/lab5-6.png)
![image](./images/lab5/lab5-6-2.png)
![image](./images/lab5/lab5-6-3.png)
<br/>






7)	 After If the pipeline succeded you should be able to see a tag with the version specified in the azure-pipeline.yml file
As well as the artifacts which contain the changelog file
![image](./images/lab5/lab5-7.png)

<br/>


