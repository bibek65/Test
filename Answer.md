1.  _Repository Setup:_

- Fork the provided repository on Git Classroom.

  ![Screenshot](materials/1.png)
  As forking is not available so I have created a repository on my own.

- Clone the forked repository to your local machine.

  One way to clone the repo is by copying the ssh url

  ![Screenshot](materials/2.png)

  To clone a repository on local machine we can use the below command

> **git clone git@github.com:bibek65/My-Git-Flow.git**

    ![Screenshot](materials/3.png)

- Set up a remote named upstream pointing to the original repository.

  For this we can use the below command

> **git remote set-url origin [url]**

- url to the original repository

2.  _Branching and Workflow:_(CLI is recommended. Do try in UI also.)

- Implement a Git branching strategy using Gitflow:

- Create a develop branch.

Initialize Gitflow:

![Screenshot](materials/4.png)

By initializing git flow develop and main branches are created

- Implement a feature (a simple script) in a branch named feature/add-advanced-functionality.

In gitflow we can implement a feature branch as

![Screenshot](materials/5.png)

- Merge the feature branch into the develop branch.

Merging the feature branch into develop branch can be done as

![Screenshot](materials/6.png)

- Create a release branch named release/v1.0 from the develop branch.

Release branch can be created as

![Screenshot](materials/7.png)

- Tag the release branch with version v1.0.

Tag is created automatically when you finish the release

![Screenshot](materials/8.png)

- Merge the release branch into both main and develop branches.

When we finish the release it will be merged into main and develop

Branches as shown below :

![Screenshot](materials/9.png)

I have push the changes to the remote repo as well :

![Screenshot](materials/10.png)

3.  _Conflict Resolution:_

- Introduce a deliberate conflict in the feature/add-advanced-functionality branch.

To introduce conflict in the feature/add-advanced-functionality I have added a echo statement in example.sh file which I created earlier as shown below

![Screenshot](materials/11.png)

Then I have created another branch feature/add-simple-functionality

And add echo statement in the same line as shown below

![Screenshot](materials/12.png)

Now I have merged feature/add-simple-functionality into feature/add-advanced-functionality now conflict is occurred as shown below

![Screenshot](materials/13.png)

- Resolve the conflict using Git and document the resolution steps.

You can resolve the conflict using VS Code by choosing one of the actions provided by VS. In my case I have chosen accept both changes to resolve the issue and continue the merge process.

![Screenshot](materials/14.png)

4. _Git Submodules:_

- Add a submodule pointing to another public GitHub repository of your choice within the project.

To demonstrate git submodule I have taken a temp repo which I created in my github account . Now to add a submodule we can do this by

![Screenshot](materials/15.png)

- Update the README to include instructions on how to initialize and update the submodule.

![Screenshot](materials/16.png)

To show git submodule init I have just clone the repo . At first we couldnot see the files of submodules. So to do that we have to use initialize and update the submodule that can be done as shown below

![Screenshot](materials/17.png)

5.  _Hooks and Custom Scripts:_

- Implement a custom Git post-merge hook that triggers a script (post-merge-script.sh) whenever a merge occurs in the repository.

Navigate to .git/hooks/

Create a file post-merge that will trigger the script post-merge-script.sh whenever a merge occurs

![Screenshot](materials/18.png)

post-merge-script.sh

![Screenshot](materials/19.png)

- Ensure the script is executable and prints a message indicating a successful merge.

To make the script executable . Below is the command

![Screenshot](materials/20.png)

![Screenshot](materials/21.png)

Message "Merge Successful" is shown as below

![Screenshot](materials/22.png)

6.  _Interactive Rebase:_

- Perform an interactive rebase on the develop branch to squash three consecutive commits into a single commit.

To demonstrate this I have done 4 commits Now to squash the 3 consecutive commits

We can use interactive rebase as shown below

![Screenshot](materials/23.png)

![Screenshot](materials/24.png)

![Screenshot](materials/25.png)

Here commit A is picked and 3 commits are squashed into one.

![Screenshot](materials/26.png)
