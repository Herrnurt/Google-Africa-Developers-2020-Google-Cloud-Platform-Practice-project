
# Course:   Essential Google Cloud Infrastructure: Foundation.
## Module: Introduction to Google Cloud.
## Lab: Console and Cloud Shell

## Overview
In this lab, you become familiar with the Google Cloud command Line.
They are Google Cloud Shell found on Google Cloud Platform website  and Google Cloud SDK shell,an application used for interacting with GCP from users' Computers. Either of the two will work perfectly.
## Objectives

In this lab, you learn how to perform the following tasks:

• Get access to Google Cloud.

• Create a Cloud Storage bucket (first) using the Cloud Command Line.

• Create a Cloud Storage bucket (second) using Cloud Cloud command Line.

• Become familiar with Cloud Shell features.

## Prerequisite
1. Google SDK Cloud shell will be used, so the environment is needed to be set up.
2. Google cloud account is needed to be able to connect to Google cloud platformn.

## Note
Cloud Storage is an object storage system, which means files that are stored in the system are treated as atomic units—that is, you cannot operate on part of the file, such as reading only a section of the file.

## Task 1: Create a bucket (First) Cloud Command Line.

To create a bucket, use the gsutil mb command; “mb” is short for “make bucket.”
<div style = "background-color:black;color:white;text-align:left; font-family:CourierNewPSMT; vertical-align: middle; padding:5px 47px;">gsutil mb gs://[BUCKET_NAME]/</div>


To create a bucket named
Cloud-track-bucket1, you would use the following command:
_gsutil mb gs://Cloud-track-bucket1/_

## Task 2: Access Google Cloud Shell
In this section, you explore Google Cloud Shell and some of its features.
You can use the Cloud Shell to manage projects and resources via command
line, having to install the Cloud SDK and other tools on your computer.
Cloud shell provides the following:

• Temporary Compute Engine VM,

• Command-line access to the instance via a browser,

• 5 GB of persistent disk storage ($HOME dir).

• Pre-installed Cloud SDK and other tools.

• gcloud: for working with Google Compute Engine and many Google Cloud services.

• gsutil: for working with Cloud Storage.

• kubectl: for working with Google Container Engine and Kubernetes.

• bq: for working with BigQuery.

• Language support for Java, Go, Python, Node.js, PHP, and Ruby.

• Web preview functionality.


## Task 3: Create a bucket using Cloud Command Line via Google Cloud Shell.

To create a bucket, use the gsutil mb command; “mb” is short for “make bucket.”

<div style = "background-color:black;color:white;text-align:left; font-family:CourierNewPSMT; vertical-align: middle; padding:5px 47px;">gsutil mb gs://[BUCKET_NAME]/</div>

To create a bucket named
Cloud-track-bucket2, you would use the following command:
gsutil mb gs://Cloud-track-bucket2/

## Task 4: Explore more Cloud Shell feature.
### Upload a file

To **upload** a file from your local device or a GCP virtual machine (VM), you can use the gsutil cp command to copy files. The command is as follows:

<div style = "background-color:black;color:white;text-align:left; font-family:CourierNewPSMT; vertical-align: middle; padding:5px 47px;">gsutil cp [LOCAL_OBJECT_LOCATION] gs://[DESTINATION_BUCKET_NAME]/</div>

For example, to copy a file called README.txt from /home/mydir to the bucket
cloud-track-bucket1, you’d execute the following command from your client device
command line:

<div style = "background-color:black;color:white;text-align:left; font-family:CourierNewPSMT; vertical-align: middle; padding:5px 47px;">gsutil cp /home/mydir/README.txt gs://cloud-track-bucket1/</div>


## Task 5: Create a persistent state in Cloud Shell.

In this section you will learn a best practice for using Cloud Shell. The gcloud command often requires specifying values such as **Region** or **Zone** or **Project ID**. Entering them repeatedly increases the chances of making typing errors. If you use Cloud Shell a lot, you may want to set common values in environment variables and use them instead of typing the actual values.

### Identify available regions.
1. Open Google Cloud Shell from the Cloud Console. Note that this allocates a new
VM for you.

2. To list available regions, execute the following command:

<div style = "background-color:black;color:white;text-align:left;font-family:CourierNewPSMT;font-size:15px;  vertical-align: middle; padding:5px 47px;">gcloud compute regions list.</div>

3. Select a region from the list and note the value in any text editor. This
region will now be referred to as [YOUR_REGION] in the remainder of the lab.

### Create and verify an environment variable.
1. Create an environment variable and replace [YOUR_REGION] with the region you selected in the previous step:

<div style = "background-color:black;color:white;text-align:left;font-family:CourierNewPSMT;font-size:15px;  vertical-align: middle; padding:5px 47px;"> INFRACLASS_REGION=[YOUR_REGION]</div>


2. Verify it with echo:

<div style = "background-color:black;color:white;text-align:left;font-family:CourierNewPSMT;font-size:15px;  vertical-align: middle; padding:5px 47px;">  echo $INFRACLASS_REGION</div>

You can use environment variables like this in gcloud commands to reduce the
opportunities for typos, and so that you won't have to remember a lot of detailed
information.

Every time you close Google  Cloud Shell and reopen it, a new VM is allocated, and the environment variable you just set disappears. In the next steps, you create a file to set the value so that you won't have to enter the command each time Cloud
Shell is cycled.

### Append the environment variable to a file.
1. Create a subdirectory for materials used in this class:

<div style = "background-color:black;color:white;text-align:left;font-family:CourierNewPSMT;font-size:15px;  vertical-align: middle; padding:5px 47px;">mkdir infraclass</div>
 
2. Create a file called config in the infraclass directory

<div style = "background-color:black;color:white;text-align:left;font-family:CourierNewPSMT;font-size:15px;  vertical-align: middle; padding:5px 47px;"> touch infraclass/config</div>
  
3. Append the value of your Region environment variable to the config file:
 
<div style = "background-color:black;color:white;text-align:left;font-family:CourierNewPSMT;font-size:15px;  vertical-align: middle; padding:5px 47px;"> echo INFRACLASS_REGION=$INFRACLASS_REGION >> ~/infraclass/config.
 </div>
 
4. Create a second environment variable for your Project ID, replacing
[YOUR_PROJECT_ID] with your Project ID. You can find the project ID on
the Cloud Console Home page.

<div style = "background-color:black;color:white;text-align:left;font-family:CourierNewPSMT;font-size:15px;  vertical-align: middle; padding:5px 47px;"> INFRACLASS_PROJECT_ID=[YOUR_PROJECT_ID]
  </div>
  
5. Append the value of your Project ID environment variable to the config file:

<div style = "background-color:black;color:white;text-align:left;font-family:CourierNewPSMT;font-size:15px;  vertical-align: middle; padding:5px 47px;">  echo INFRACLASS_PROJECT_ID=$INFRACLASS_PROJECT_ID >> ~/infraclass/config.
  </div>
 

6. Use the source command to set the environment variables, and use the echo command to verify that the project variable was set:

<div style = "background-color:black;color:white;text-align:left;font-family:CourierNewPSMT;font-size:15px;  vertical-align: middle; padding:5px 47px;">source infraclass/config 

echo $INFRACLASS_PROJECT_ID </div>
  
This gives you a method to create environment variables and to easily recreate
them if the Google Cloud Shell is cycled. However, you will still need to remember to
issue the source command each time Cloud Shell is opened.
In the next step you will modify the .profile file so that the source command is
issued automatically any time a terminal to Cloud Shell is opened.

7. Close and re-open Cloud Shell. Then issue the echo command again:

<div style = "background-color:black;color:white;text-align:left;font-family:CourierNewPSMT;font-size:15px;  vertical-align: middle; padding:5px 47px;">   echo $INFRACLASS_PROJECT_ID.</div>
  
There will be no output because the environment variable no longer exists.

### Modify the bash profile and create persistence.

1. Edit the shell profile with the following command:

<div style = "background-color:black;color:white;text-align:left;font-family:CourierNewPSMT;font-size:15px;  vertical-align: middle; padding:5px 47px;">    nano .profile</div>
  
2. Add the following line to the end of the file:

<div style = "background-color:black;color:white;text-align:left;font-family:CourierNewPSMT;font-size:15px;  vertical-align: middle; padding:5px 47px;">    source infraclass/config</div>
   

3. Press **Ctrl+O**, **ENTER** to save the file, and then press **Ctrl+X** to exit nano.

4. Close and then re-open Cloud Shell to cycle the VM.

5. Use the echo command to verify that the variable is still set:

<div style = "background-color:black;color:white;text-align:left;font-family:CourierNewPSMT;font-size:15px;  vertical-align: middle; padding:5px 47px;">    echo $INFRACLASS_PROJECT_ID</div>
  

   You should now see the expected value that you set in the config file.

   If you ever find your Cloud Shell environment corrupted, you can find instructions on resetting it here:

### Resetting Cloud Shell
This will cause everything in your Cloud Shell environment to be set back to its
original default state.