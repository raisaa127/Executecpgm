Hello_Jenkins
This simple exercise is designed to introduce you to Jenkins and continuous integration. This was originally written as an exercise for California State University, Chico. I have since modified it to be a simple exercise for anyone to use.

Overview
Fork the repo.
Set up job in Jenkins to connect to your repository and build C++ hello.cpp.
Set up build status badge.
Set up second job to run the program after build completes.
Prerequisites
A Jenkins server is needed in order to complete the exercise. One option is local virtualization using Docker or a virtual machine. Another is installing Jenkins on a cloud platform like AWS. A t2.micro would be more than enough for this particular exercise.

You should fork this repository and set up to run on your own. This will allow you to change and experiment to your heart's desire.

Setting up a Job in Jenkins
Jenkins Landing Page

Navtigate to Jenkins server.
Click New Item.
Enter a name for your project, click Freestyle Project, then OK.
Note: Please do not include a space.
Name this something unique so there are no collisions.
Set up Source Code Management.
Select git.
Enter the URL to your git repository
Setting up Build Triggers
Select Poll SCM.
Set up cron job by putting in H/2 * * * *.
Set up Build.
Add build step Execute Shell.
Enter make (This will run the Makefile).
Click Save.
If you want a bit more of a challenge consider setting up Webhooks as opposed to polling. A fun Jenkins exercise that can get you thinking.

Set up Embeddable Build Status for Repo
Build status badge

The build status symbol often seen on a Github repository is normally connected to TravisCI or JenkinsCI. We are using JenkinsCI which requires a plugin called Embeddable Build Status. I have already installed it for you. You just need to add the proper information into your README.md file.

Open the README file in a text editor.
Go to the Embeddable Build Status page. The link is found on the main page of the job.
Select the Markdown (with View) protected link and paste it in your README.
Commit your README changes and push to Github.
The change should automatically cause the job to build and after you can go to Github and check your repo. You should see the build status there
Because we selected With View you will be able to click the build status icon which will take you to the Job in Jenkins.

Set up Second Job to Run the Compiled Program
The final step to this demo is to set up a second job that automatically runs after the project builds. This is different than the other job because this will not have a git repository - it doesn't even build anything.

Just a note: In a real-life scenario you wouldn't run a program through a build job just like this because I/O is not possible via this console. There are other tools people use at this step like SeleniumHQ, SonarQube, or a Deployment. The point of this is to show downstream/upstream job relationships.

Create a new Job in Jenkins
Click New Item.
Enter a name for your second job, click Freestyle Project, then OK.
Go immediately to build step and select Execute Shell.
Enter the following Command /var/lib/jenkins/workspace/<the name of your first project>/output file
Save
Set your first job to call the second
Go to your first job and open the Configure page.
Scroll to bottom and add a Post-Build Action. Select Build other projects.
Enter the name of your second job.
Save
Run your first job
Do this by clicking build now on the main page.
After that successfully builds go and check your second job.
You should see it successfully run.
Select a Build Job from History and go to the console log to see your program output. If you program has run there then you successfully set up a basic pipeline. Job history
