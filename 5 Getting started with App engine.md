# Course:   Google Cloud Platform Fundamentals - Core Infrastructure
## Module: Applications in the Cloud.
## Lab: GCP Fundamentals: Getting Started with App Engine
## Overview

In this lab, you create and deploy a simple App Engine application using a virtual
environment in the Google Cloud Shell.

## Objectives

In this lab, you learn how to perform the following tasks:

• Initialize App Engine.

• Preview an App Engine application running locally in Cloud Shell.

• Deploy an App Engine application, so that others can reach it.

• Disable an App Engine application, when you no longer want it to be visible.

### Task 1: Initialize App Engine

1. Initialize your App Engine app with your project and choose its region:

<div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;">gcloud app create --project=$DEVSHELL_PROJECT_ID </div>

When prompted, select the region where you want your App Engine application located.

2. Clone the source code repository for a sample application in the **hello_world** directory:

<div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;">git clone https://github.com/GoogleCloudPlatform/python-docs-samples </div>

3. Navigate to the source directory:

<div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;">cd python-docs-samples/appengine/standard_python3/hello_world </div>

###   Task 2: Run Hello World application locally

In this task, you run the Hello World application in a local, virtual environment in Cloud Shell.

Ensure that you are at the Cloud Shell command prompt.

1. Execute the following command to download and update the packages list.

<div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;">sudo apt-get update</div>

2. Set up a virtual environment in which you will run your application. Python virtual environments are used to isolate package installations from the system.

<div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;">sudo apt-get install virtualenv</div>

If prompted [Y/n], press Y and then Enter.

<div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;">virtualenv -p python3 venv</div>

3. Activate the virtual environment.

<div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;">source venv/bin/activate</div>

4. Navigate to your project directory and install dependencies.

<div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;">pip install -r requirements.txt</div>

5. Run the application:

<div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;">python main.py</div>

    Please ignore the warning if any.
    
 6. In **Cloud Shell**, click **Web preview**> **Preview** on **port 8080** to preview the application.
 
To access the **Web preview** icon, you may need to collapse the **Navigation menu**.

Alternatively 

Use the gcloud command line code to view the app deployed

<div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;">gcloud app browse</div>

7. To end the test, return to Cloud Shell and press Ctrl+C to abort the deployed service.

8. Using the Cloud shell, verify that the app is not deployed with this code.

<div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;">gcloud app browse </div>

       Notice that no resources are deployed.
       
### Task 3: Deploy and run Hello World on App Engine

To deploy your application to the App Engine Standard environment:

1. Navigate to the source directory:

<div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;">cd ~/python-docs-samples/appengine/standard_python3/hello_world</div>

2. Deploy your Hello World application.

<div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;">gcloud app deploy</div>

If prompted "Do you want to continue (Y/n)?", press Y and then Enter.


This **app deploy** command uses the app.yaml file to identify project configuration.

3. Launch your browser to view the app at http://YOUR_PROJECT_ID.appspot.com

<div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;">gcloud app browse</div>

Copy and paste the URL into a new browser window.

Congratulations! You created your first application using App Engine.


### Task 4: Disable the application


App Engine offers no option to Undeploy an application. After an application is deployed, it remains deployed, although you could instead replace the application with a simple page that says something like "not in service."

However, you can disable the application, which causes it to no longer be accessible to users.

Use the gcloud command line to stop the App deployed.

<div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;">gcloud app versions stop</div>
