1)	Click on ‘Project settings’ and next click on Agent Pools
    ![image](./images/lab4/lab4-1.png)

<br/>

2)	Next, click on ‘Add pool’
In pool to link select ‘New’ 
and select ‘Self-Hosted’
name it: ‘ado-ai’
and in ‘Pipeline permissions’ mark the ‘Grant access permissions to all pipelines’ checkbox
    ![image](./images/lab4/lab4-2.png)

<br/>

3)	Click on the ‘ado-ai’ agent pool,
and within it, click on ‘new agent’
    ![image](./images/lab4/lab4-3.png)

<br/>

4)	In the ‘Get the agent’ window, click on the ‘Linux’ tab
and click on the copy button for the ‘Download the agent’ section
    ![image](./images/lab4/lab4-4.png)

<br/>

5)	Before proceeding with the installation of the agent software in codespaces,
we will need to modify the gitignore file to add the directory where we will downloading the agent files to
so in the terminal, lets create a new branch with the following command:
git branch feature/git-ignore
then checkout the branch with the following command:
git switch feature/git-ignore
    ![image](./images/lab4/lab4-5.png)

<br/>

6)	Next, edit the .gitignore file, and add the following lines:
```
# Azure DevOps Agent
myagent/
```
![image](./images/lab4/lab4-6.png)

<br/>

7)	Commit these changes, and publish the branch to Azure DevOps
It will ask for the Access Token
![image](./images/lab4/lab4-7.png)

<br/>

8)	Create a pull request for this git-ignore branch:
![image](./images/lab4/lab4-8.png)

<br/>

9)	Be sure to select the main branch as the destination:
![image](./images/lab4/lab4-9.png)

<br/>

10)	Next, approve and merge it:
![image](./images/lab4/lab4-10.png)

<br/>

11)	Once done, head back to codespaces and switch to the main branch and pull the latest changes
(the ‘myagent/’ directory should now be part of the .gitignore file)
![image](./images/lab4/lab4-11.png)

<br/>

12)	 Run the following command in the terminal:
mkdir myagent && cd myagent
and type wget and paste the download file we copied from the agent pool which should still be available in the GitHub Chat input
it should be:
wget https://download.agent.dev.azure.com/agent/4.261.0/vsts-agent-linux-x64-4.261.0.tar.gz
![image](./images/lab4/lab4-12.png)

<br/>

13)	Next, lets uncompress the file with:
![image](./images/lab4/lab4-13.png)

<br/>

14)	Now we need to configure our agent, for this run:
./config.sh
![image](./images/lab4/lab4-14.png)

<br/>

15)	Enter the server url:
It should be https://dev.azure.com/<your azure devops collection name>
example: https://dev.azure.com/PaulFurlan0409
(note: its not the project)
In authentication type, press the ‘enter’ key (for personal access token)
and paste the Access token (you may need to paste it into the GitHub Copilot chat window and copy it from there, in case it doesn’t let you paste it directly in the terminal)
For agent pool, input: ado-ai
For agent name, add a descriptive name, such as: ado-ai-codespaces
In enter replace hit enter (for default setting)
and for the work folder, just press enter to leave the default.
![image](./images/lab4/lab4-15.png)

<br/>

16)	For agent name, add a descriptive name, such as: ado-ai-codespaces
In 'enter replace' hit enter (for default setting)
and for the work folder, just press enter to leave the default.
After the agent has been configured, type:
./run.sh
![image](./images/lab4/lab4-16.png)

<br/>

17)	 Upon refreshing the agents tab in the ‘ado-ai’ agent pool, our runner should now appear online:
![image](./images/lab4/lab4-17.png)

<br/>

18)	Now lets add some unit tests to our app
go back to codespaces
add a new terminal session with bash to prevent disruption the terminal session for our runner:
![image](./images/lab4/lab4-18.png)

<br/>

19)	Next, close all open files except ‘todo.py’
In copilot chat, input the following prompt:
As a Python testing expert, write unit tests for the to-do list CLI app’s add, list and complete functions using pytest in a new feature branch.
![image](./images/lab4/lab4-19.png)
![image](./images/lab4/lab4-19-2.png)

<br/>

20)	If everything work as expected, commit the changes and publish the branch
![image](./images/lab4/lab4-20.png)
Select the ado remote repo:
![image](./images/lab4/lab4-20-2.png)

<br/>

21)	Then lets create a pull request to merge these tests into the main branch:
![image](./images/lab4/lab4-21.png)
![image](./images/lab4/lab4-21-2.png)

<br/>

22)	Approve and complete the pull request:
![image](./images/lab4/lab4-22.png)

<br/>

23)	In codespaces, switch to the main branch and pull the changes
Don’t forget to give it a couple of seconds to update before moving on to the next steps (it may ask you for your token again)
![image](./images/lab4/lab4-23.png)

<br/>

24)	And now we are ready to author our pipeline.
Start a new chat GitHub Copilot, and then input the following prompt:
As a Devops Expert who specializes in Azure Devops, please create a yaml pipeline to automate the build and test of a python application.
Step 1: Create this pipeline in a new feature branch called feature/azure-pipeline
Step 2: The pipeline must use  the ‘ado-ai’ agent pool
Step 3:  The pipeline must use pytest for the unit tests and it must publish the test results whether they succeed or fail
Step 4: The pipeline must publish code coverage results with cobertura
Step 5: The pipeline must use bandit to identify vulnerabilities and publish a report
Step 6: The pipeline must use trivy for dependency scanning and publish a report
![image](./images/lab4/lab4-24.png)
![image](./images/lab4/lab4-24-2.png)

<br/>

25)	If Copilot added a trigger for ‘-feature/*’ branches, comment it out from the azure-pipelines.yml file
Also, comment out the following lines as our Codespaces Agent already has Python installed:
```
#- task: UsePythonVersion@0
#  inputs:
#    versionSpec: '3.x'
#    addToPath: true
```
![image](./images/lab4/lab4-25.png)

<br/>

26)	Next, commit the changes, publish the branch, create a pull request, approve it and merge it with rebase and select delete branch.
![image](./images/lab4/lab4-26.png)
![image](./images/lab4/lab4-26-2.png)
![image](./images/lab4/lab4-26-3.png)
![image](./images/lab4/lab4-26-4.png)

<br/>

27)	Next we can create our pipeline, 
Click on pipelines and next on create pipeline
![image](./images/lab4/lab4-27.png)

<br/>

28)	Select ‘Azure Repos Git’
next select our ‘ado-ai’ repository
and it should automatically detect our pipeline.
Click on run
![image](./images/lab4/lab4-28.png)
![image](./images/lab4/lab4-28-2.png)

<br/>

29)	This should launch our pipeline:
![image](./images/lab4/lab4-29.png)

<br/>

30)	The pipeline failed as it was not able to find a package named ‘trivy-plugin’, so lets go back to codespaces and ask it to fix this issue:
![image](./images/lab4/lab4-30.png)

<br/>

31)	As usual, we have to change to the main branch and pull the latest updates.
Then lets give the following prompt to copilot chat:

The trivy-plugin appears to be unavailable or deprecated. Please create a new branch and update the pipeline to use an alternative method for installing Trivy, such as the official installation script or a supported package manager.
![image](./images/lab4/lab4-31.png)
![image](./images/lab4/lab4-31-2.png)

<br/>

32)	And now, lets add the trigger to allow this pipeline (or uncomment it if it is already there) to run on feature branches as well
![image](./images/lab4/lab4-32.png)

<br/>

33)	As usual, lets commit (if needed) and publish this branch
![image](./images/lab4/lab4-33.png)

<br/>

34)	This will run the pipeline for these changes to let us know if the issue has been resolved before we try and merge these to the main branch:
![image](./images/lab4/lab4-34.png)

<br/>

35)	And it looks like we have a couple of issues to iron out:
![image](./images/lab4/lab4-35.png)

<br/>

36)	The first one is an issue with pytest
And upon looking into the job it seems that it has an issue locating the ‘src’ module:
![image](./images/lab4/lab4-36.png)

<br/>

37)	Here we can troubleshoot the issue with the assistance from AI:
Give it the following prompt:
```
The ‘<failed step display name>’ is running into an error:
<error message>
```
Then it will fix and test the error:
![image](./images/lab4/lab4-37.png)

<br/>

38)	Lets tackle the second error: 
![image](./images/lab4/lab4-38.png)

<br/>

39)	Lets give copilot chat the following prompt:
```
The ‘<failed step display name>’ is running into an error:

<error message>
```
![image](./images/lab4/lab4-39.png)

<br/>

40)	This failure is due to some false positive statements, and after a couple of attempts it is finally able to figure it out.
![image](./images/lab4/lab4-40.png)

<br/>

41)	It seems it resolved these issues locally but not in the pipeline, so lets give it the following prompt:
Modify the azure-pipelines.yml file to include the fix for the ‘Run pytest with coverage’ and ‘Run Bandit security scan’ steps:
![image](./images/lab4/lab4-41.png)

<br/>

42)	Now lets commit and push our changes:
![image](./images/lab4/lab4-42.png)

<br/>

43)	Lets have a look at how our pipeline for this branch is doing now:
![image](./images/lab4/lab4-43.png)

<br/>

44)	If everything went fine, all the steps in the pipeline job will run successfully:
![image](./images/lab4/lab4-44.png)
![image](./images/lab4/lab4-44-2.png)

<br/>

45)	In the tests tab, you can find details about the unit tests:
![image](./images/lab4/lab4-45.png)

<br/>

46)	And there is a nice code coverage report in the corresponding tab:
![image](./images/lab4/lab4-46.png)

<br/>

47)	We can now proceed with merging this feature branch to the main branch.
![image](./images/lab4/lab4-47.png)
![image](./images/lab4/lab4-47-2.png)
<br/>