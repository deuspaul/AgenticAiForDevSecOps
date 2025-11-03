1)	In GitHub, create a new repository by clicking on ‘New repository’
    ![image](./images/lab2/lab2-1.png)

<br/>

2)	Name the repository ‘ado-ai’, 
keep it as a ‘public’ repository, 
check the ‘Add a README file’ checkbox
and click on ‘Create repository’
    ![image](./images/lab2/lab2-2.png)

<br/>

3)	Your new repository should look like the following screenshot:
    ![image](./images/lab2/lab2-3.png)

<br/>

4)	Next, click on the green ‘code’ button
click on the Codespaces tab
and click on ‘Create Codespaces on main’
    ![image](./images/lab2/lab2-4.png)

<br/>

5)	This should launch a Codespaces instance with VS Code and it should look like the following:
    ![image](./images/lab2/lab2-5.png)
📝 **Note:** This is basically a VM instance that has several tools installed such as git, python, copilot among others.

<br/>

6)	 Lets test out GitHub Copilot. Input the following prompt in the Copilot Chat window and hit enter (if it doesn’t appear, click on the icon within the red circle):
    I need to add a gitignore file for python. Create it in its own branch so that it can be reviewed
![image](./images/lab2/lab2-6.png)

<br/>

7)	This may ask us to set up copilot if not already set up in your account (click on ‘Set up Copilot’ if that’s the case):
![image](./images/lab2/lab2-7.png)

<br />

8) next click on enable:<br/>
![image](./images/lab2/lab2-8.png)

<br/>

9) It should create the file for you:<br/>
![image](./images/lab2/lab2-9.png)

<br />

10) ...but, it may not have created it in its own branch, so lets make sure we are on ‘agent’ mode instead of ‘ask’ and lets tell it to create the branch and create add the .gitignore file to it:
![image](./images/lab2/lab2-10.png)

<br />

11) Insert the following prompt: 
‘create a branch called 'adding-gitignore' and add the .gitignore file in that branch’
![image](./images/lab2/lab2-11.png)

<br />

12) Once you input the prompt it will reply with a to-do list with the tasks it will perform 
![image](./images/lab2/lab2-12.png)

<br />

13) Click on ‘Allow’ so that it can generate the branch
![image](./images/lab2/lab2-13.png)

<br />

14) So it has generated the branch, but our gitignore file is now empty (see screeshot from the previous step). 
    With these past steps we have experienced the importance of proper prompting.
	Lets change the model from gpt-5 mini to claude Sonnet 3.5 and continue:
    ![image](./images/lab2/lab2-14.png)

<br />

15) Now lets give it the following prompt:
Fill the existing empty .gitignore file with entries suitable for a standard Python project. Stage and commit the file to the Git repository with a clear commit message.
📝 **Note:** If it asks you to enable Claude Sonnet 3.5 for all clients, click on ‘Enable’<br/>
![image](./images/lab2/lab2-15.png)

<br />

16)	It should fill out the .gitignore file. 
Next click on Allow
![image](./images/lab2/lab2-16.png)

<br />

17) The file should have been successfully updated, and it will most probably ask you if you would like to open a pull request for these changes (tell it no)
![image](./images/lab2/lab2-17.png)

<br />

18)	Next, lets give it the following prompt:
Yes, open a pull request for these changes (if it asks you for permissions, click on ‘allow’)
![image](./images/lab2/lab2-18.png)

<br />

19)	Now let’s go back to our repository and look for the pull request and click on ‘merge pull request’ and leave the default comment. 
📝 **Note:** Don’t worry about pull requests at this point in time, we will dive deeper into these in the upcoming lessons. 
What’s important to note about the previous step is the ‘agents’ capability of leveraging the GitHub CLI to autonomously create this pull request for us.
![image](./images/lab2/lab2-19.png)

<br />

20)	Let’s go back to our Codespaces tab and switch to the main branch (First click on the current branch in the bottom left [red circle])
![image](./images/lab2/lab2-20.png)

<br />

21)	You will notice that the .gitignore file is not there. This is because we have not synchronized the latest changes that happened to our repository in GitHub.com through the previous pull request.
Hit the ‘refresh’ button to synchronize changes (bottom left):
Hit ‘Ok’ to allow it to synchronize changes. 
Once done, you should see the .gitignore file in the ‘Explorer’ pane.
![image](./images/lab2/lab2-21.png)

<br />

22)	Next, let’s input the following prompt into our Copilot Chat window:
Write a Python CLI app skeleton for a to-do list using argparse to handle commands (add, list) and JSON for task storage. 
Step 1: Create a new branch and save the generated code as src/todo.py and tasks.json
Step 2: Include a main function and basic file structure as well as the requirements.txt file
Step 3: update the readme.md file with a description of the repository <br/>
![image](./images/lab2/lab2-22.png)

<br />

23)	It will break down the task into steps and ask you for permission to run them (Click on ‘Allow’).
It should look something like the following 
![image](./images/lab2/lab2-23.png)

<br />

24)	This should have created a new branch with the full project structure (details in the chat response): 
![image](./images/lab2/lab2-24.png)

<br />

25)	Let’s check if our app is working as expected now. 
We could very well ask it to help us test the app, but we are in the free tier, so we have to be mindful of the amount of requests we make.
Also, it is a good practice to review the code that is written by AI, so lets have a look at the code to familizare ourselves.
Expand the ‘src’ folder and open the ‘todo.py’ file. Explore the functions inside of it (at least ‘add_task’ and ‘list_tasks’, look for tasks with similar names as AI could generate them differently)
![image](./images/lab2/lab2-25.png)

<br />

26)	To test the app, lets execute the ‘todo.py’ file:
In the terminal input:
python src/todo.py add "test the todo app"
It should reply with: “Added task: test the todo app”
Next, in the terminal type: python src/todo.py list
It should reply with the “test the todo app” item we just added
![image](./images/lab2/lab2-26.png)

<br />

27)	It may or may not have identified that tasks.json file should be added to the git ignore. 
If it did not do that, add it manually (to save on free tier requests) 
By editing the ‘.gitignore’ file, and adding the following lines of code at the end of the file:
```
# App specific
tasks.json
```
![image](./images/lab2/lab2-27.png)

<br />

28)	We are now ready to commit these changes and merge this feature branch to the main branch (we will omit the PR to save time).
Input the following prompt:
Commit the changes to this branch and merge the '<replace with your todo-cli branch name>' branch to the main branch and delete the '<replace with your todo-cli branch name>' branch
![image](./images/lab2/lab2-28.png)

<br />

29) As usual, it will ask for permissions, be sure to review the changes and click on ‘Allow’ if the changes look correct
![image](./images/lab2/lab2-29.png)<br />
📝 **Note:** Afterwards, it should checkout main and merge the feature branch (‘todo-cli-app’ in this guide) into main
and delete the feature branch (‘todo-cli-app’)

<br />

30) Next click on the ‘Sync Changes’ button to make sure our changes get pushed to the GitHub Repo
![image](./images/lab2/lab2-30.png)

<br />

31)	All of these changes should appear in our GitHub repo now:
![image](./images/lab2/lab2-31.png)