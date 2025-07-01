## 1. How To Integrate Git With Jenkins?
To integrate Git with Jenkins:

Install the "Git Plugin" in Jenkins through the plugin manager.
Configure Git in the global tool configuration, ensuring automatic installation is enabled.
Create or configure a Jenkins job, selecting Git as the version control system.
Specify the Git repository URL and, if necessary, credentials for authentication.
Define the branches to monitor and build.
Set up build triggers as needed.
Save the job configuration and trigger builds manually or automatically based on your settings.
Monitor build progress and results in the Jenkins dashboard.

## 2.What Does "Poll SCM" Mean In Jenkins?
In Jenkins, "poll SCM" means periodically checking a version control system (e.g., Git) for changes. You can schedule how often Jenkins checks for updates. When changes are detected, Jenkins triggers a build, making it a key feature for continuous integration, scheduled tasks, and automated response to code changes.

## 3. How To Schedule Jenkins Build Periodically (hourly, daily, weekly)? Explain the Jenkins schedule format.
To schedule Jenkins builds periodically at specific intervals, you can use the built-in scheduling feature. Jenkins uses a cron-like syntax for scheduling, allowing you to specify when and how often your builds should run. Here's a detailed explanation of the Jenkins schedule format and how to schedule builds:

**1. Jenkins Schedule Format**
The Jenkins schedule format closely resembles the familiar cron syntax, with a few minor differences. A typical Jenkins schedule consists of five fields, representing minute, hour, day of the month, month, and day of the week, in that order:

Here's what each field means:

Minute (0 - 59): Specifies the minute of the hour when the build should run (e.g., 0 for the top of the hour, 30 for the half-hour).
Hour (0 - 23): Specifies the hour of the day when the build should run (e.g., 1 for 1 AM, 13 for 1 PM).
Day of the month (1 - 31): Specifies the day of the month when the build should run (e.g., 1 for the 1st day of the month, 15 for the 15th day).
Month (1 - 12): Specifies the month when the build should run (e.g., 1 for January, 12 for December).
Day of the week (0 - 7): Specifies the day of the week when the build should run (e.g., 0 or 7 for Sunday, 1 for Monday, and so on).

Scheduling Examples:
Now, let's look at some scheduling examples:

Cron Expression	      Description
0 0 * * *	            Schedules a build every day at midnight (00:00).
30 * * * *        	  Schedules a build every hour at the 30th minute (e.g., 1:30 AM, 2:30 AM).
0 15 * * 1          	Schedules a build every Monday at 3 PM.
0 8,20 * * *	        Schedules a build every day at 8 AM and 8 PM.
30 22 * * 5	          Schedules a build every Friday at 10:30 PM.

## 4. What Is A Jenkins Agent?
A Jenkins agent, also called a Jenkins slave or node, is a separate machine or resource that collaborates with a Jenkins master to execute jobs and build tasks. Agents enable parallel and distributed builds, scaling Jenkins' capacity.

They register with the master, get assigned jobs, execute them on their own hardware or VMs, and report back results. Agents can run on various platforms, making it possible to test and build in different environments.

## 5 . How To Restart Jenkins?
To restart Jenkins, you can follow these steps:

**Method 1.Using the Jenkins Web Interface (if available):**

Open a web browser and navigate to your Jenkins server's URL.
Log in to the Jenkins web interface if required.
In the top-right corner, you may see a "Restart" option. Click on it to initiate the restart process.
Jenkins will display a confirmation dialog. Confirm that you want to restart Jenkins.

**Method 2.Using Command Line (Linux/Unix):**

If you have SSH access to the server where Jenkins is installed, you can use the following commands:
Open a terminal or SSH into the Jenkins server.
Run the following command with superuser privileges (e.g., using sudo):
sudo systemctl restart jenkins
