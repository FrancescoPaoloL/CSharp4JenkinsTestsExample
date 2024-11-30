# CSharp4JenkinsTestsExample - Local Jenkins Docker Testing
This repository contains a simple C# console application used to demonstrate how to take the first steps in Jenkins.

For simplicity, this project is a "Hello World" example because our goal is to set up Jenkins. Additionally, for simplicity, we will use the official Docker image.

## Step 1: Pull the Jenkins Docker Image

    docker pull jenkins/jenkins

## Step 2: Run Jenkins in a Docker Container

    docker run -p 8080:8080 -p 50000:50000 --restart=on-failure jenkins/jenkins

## Step 3: Access the Jenkins Web Interface
Once Jenkins is running, navigate to: http://localhost:8080

## Step 4: Retrieve the Initial Admin Password
When Jenkins starts, you'll need to unlock it using an initial password. You'll see a log like the following:

> Jenkins initial setup is required. An admin user has been created, and a password has been generated.  
> Please use the following password to proceed with installation:
> 
> `<initial_admin_password>`
> 
> This may also be found at: /var/> jenkins_home/secrets/> initialAdminPassword
> 
> Copy the password provided and paste it into the Jenkins setup page to proceed with the installation.

## Step 5: Install Recommended Plugins
Jenkins will suggest installing popular plugins. You can proceed with the default installation of these plugins.

## Step 6: Create an Admin User
For simplicity, you can create an admin user with the following credentials:

    Username: admin  
    Password: admin

## Step 7: Configure the .NET SDK Plugin
After installing the plugin, go to Manage Jenkins > Global Tool Configuration.  
Add the latest .NET SDK version (e.g., .NET 8.0) and set the platform to linux-x64.

## Step 8: Add this repository in project
Dashboard --> select project --> Configure --> General --> Github Project --> write https://github.com/FrancescoPaoloL/CSharp4JenkinsTestsExample.git/

## Step 8: Build the Project
Create a new Jenkins job with a freestyle project.  
If you encounter the ICU Package error, use the following command to resolve it:

        sudo docker exec -it -u root <container_id> bash  
        apt-get install libicu-dev

## Step 9: Build Log Output
Here's an example of a successful build log:

    14:51:46 Started by user admin  
    14:51:46 Running as SYSTEM  
    14:51:46 Building in workspace /var/jenkins_home/workspace/CSharp4JenkinsTestsExample  
    14:51:46 [WS-CLEANUP] Deleting project workspace...  
    14:51:46 [WS-CLEANUP] Deferred wipeout is used...  
    14:51:46 [WS-CLEANUP] Done  
    14:51:46 The recommended git tool is: NONE  
    14:51:46 No credentials specified  
    14:51:46 Cloning the remote Git repository  
    14:51:46 Cloning repository https://github.com/FrancescoPaoloL/CSharp4JenkinsTestsExample.git/  
    14:51:46 Fetching upstream changes from https://github.com/FrancescoPaoloL/CSharp4JenkinsTestsExample.git/  
    14:51:46 Checking out Revision a8246c0e1ef7dbce1efa26b411ce1517d291e9d1 (refs/remotes/origin/main)  
    14:51:46 Commit message: "Implemented simple code"  
    14:51:46 [CSharp4JenkinsTestsExample] $ /var/jenkins_home/tools/io.jenkins.plugins.dotnet.DotNetSDK/NET/dotnet build CSharp4JenkinsTestsExample.csproj  
    14:51:47 Determining projects to restore...  
    14:51:47 Restored /var/jenkins_home/workspace/CSharp4JenkinsTestsExample/CSharp4JenkinsTestsExample.csproj (in 41 ms).  
    14:51:48 CSharp4JenkinsTestsExample -> /var/jenkins_home/workspace/CSharp4JenkinsTestsExample/bin/Debug/net8.0/CSharp4JenkinsTestsExample.dll  
    14:51:48  
    14:51:48 Build succeeded.  
    14:51:48 0 Warning(s)  
    14:51:48 0 Error(s)  
    14:51:48  
    14:51:48 Time Elapsed 00:00:01.73  
    14:51:48 .NET Command Completed - Exit Code: 0  
    14:51:49 Finished: SUCCESS

