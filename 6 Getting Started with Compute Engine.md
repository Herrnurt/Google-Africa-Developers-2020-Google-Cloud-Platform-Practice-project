## Course: Google Cloud Platform Fundamentals - Core Infrastructure

## Module:  Virtual Machines in the Cloud

### Lab: GCP Fundamentals: Getting Started with Compute Engine 

### Overview

In this lab, you will create virtual machines (VMs) and connect to them. You will
also create connections between the instances.
There are two integrated environments for CLI (command-line interface). They are Google Cloud Shell found on Google Cloud Platform website  and Google Cloud SDK shell,an Application used for interacting with GCP from users' Computers. Either of the Two will work perfectly.
### Objectives

In this lab, you will learn how to perform the following tasks:

• Create First Compute Engine virtual machine using the the gcloud command-line interface.Console.

• Create Second Compute Engine virtual machine using the gcloud command-line interface.

• Connect between the two instances.

### Task 1: Create a virtual machine using the Command Line instruction

1. for **Name**, put my-vm-1

2. For **Region** and **Zone**, select the region and zone as assigned by Qwiklabs.

3. For **Machine type**, use the default.

4. For **Boot disk**, use **Image** as **Debian GNU/Linux 9 (stretch)**

5. Use defaults for **Identity and API access** unmodified

6. For Firewall, use  **Allow HTTP traffic**.

###  Create first virtual machine using the gcloud command line

<div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;">gcloud cpmpute instances create my-vm-1 --machine-type=n1-standard-1 --image-project=debian-cloud --imagedebian-9-stretch-v20190213  -- subnets=default --tags=http</div>

### Create fire-wall rules using the gcloud command line

<div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;"> gcloud compute firewall rules create allow-http  --action=ALLLOW --destination=INGRESS --rules=http:80 --target-tag=http
</div>

Firewall rules need to be allowed in order for the two Vms to communicate with each other 

**Note**: The VM can take about two minutes to launch and be fully available for use.

###  Create second virtual machine using the gcloud command line

1. To display a list of all the zones in the region to which Qwiklabs assigned you, enter this partial command.
<div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;"> gcloud compute zones list | grep</div>

   Your completed command will look like this:
<div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;">gcloud compute zones list | grep us-central1</div>

2. Choose a zone from that list other than the zone to which Qwiklabs assigned you. For example, if Qwiklabs assigned you to region us-central1 and zone us-central1-a you might choose zone us-central1-b.

3. To set your default zone to the one you just chose, enter this partial command gcloud config set compute/zone followed by the zone youchose.

   Your completed command will look like this:
<div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;">gcloud config set compute/zone us-central1-b</div>

4.To create a VM instance called **my-vm-2** in that zone, execute this command:

<div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;">gcloud compute instances create "my-vm-2" --machine-type "n1-standard-1" --image-project "debian-cloud" --image "debian-9-stretch-v20190213" --subnet "default</div

**Note**: The VM can take about two minutes to launch and be fully available for
use.
    
5 . To close the Cloud Shell, execute the following command:
 <div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;">exit
</div>


### Task 2: Connect between VM instances

1. To view the two instances created using the gcloud command line

<div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;">gcloud compute instances list</div>

You will see the two VM instances you created, each in a different zone. 

Notice that the Internal IP addresses of these two instances share the first three bytes in common. They reside on the same subnet in their Google Cloud VPC even though they are in different zones.

2. To open a command prompt on the **my-vm-2** instance, click **SSH** in its row in the **VM instances** list.

3. Use the ping command to confirm that **my-vm-2** can reach **my-vm-1** over the network:

<div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;"> ping my-vm-1</div>

Notice that the output of the ping command reveals that the complete hostname of **my-vm-1 is my-vm-1.c.PROJECT_ID.internal**, where PROJECT_ID is the name of your Google Cloud Platform project. GCP automatically supplies Domain Name Service (DNS) resolution for the internal IP addresses of VM instances.

4. Press **Ctrl+C** to abort the ping command.

5. Use the **ssh** command to open a command prompt on **my-vm-1**:

<div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;">ssh my-vm-1</div>

If you are prompted about whether you want to continue connecting to a
host with unknown authenticity, enter **yes** to confirm that you do.


6. At the command prompt on **my-vm-1**, install the Nginx web server:

<div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;"> sudo apt-get install nginx-light -y</div>

7. Use the **nano** text editor to add a custom message to the home page of the web server:

<div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;">sudo nano /var/www/html/index.nginx-debian.html</div>

8. Use the arrow keys to move the cursor to the line just below the h1 header. Add text like this, and replace YOUR_NAME with your name:

<div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;">Hi from YOUR_NAME</div>

9. Press **Ctrl+O** and then press **Enter** to save your edited file, and then press **Ctrl+X** to exit the nano text editor.

10. Confirm that the web server is serving your new page. At the command prompt on **my-vm-1**, execute this command:

<div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;">curl http://localhost/</div>

The response will be the HTML source of the web server's home page, including your line of custom text.

11. To exit the command prompt on **my-vm-1**, execute this command:

<div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;">exit</div>

You will return to the command prompt on **my-vm-2**

12. To confirm that **my-vm-2** can reach the web server on **my-vm-1**, at the command prompt on **my-vm-2**, execute this command:

<div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;">curl http://my-vm-1/</div>

The response will again be the HTML source of the web server's home page, including your line of custom text.

13. Get the external Ip of my-vm-1 instance with gcloud command line

<div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;">gcloud compute instance list</div>

14. Copy the External IP address for **my-vm-1** and paste it into the address bar of a new browser tab. 

You will see your web server's home page, including your custom text.