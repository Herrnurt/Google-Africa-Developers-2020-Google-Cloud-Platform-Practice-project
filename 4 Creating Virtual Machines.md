# Course:  Essential Google Cloud Infrastructure: Foundation
## Module: Virtual Machines
## Lab: Creating Virtual Machines

## Overview
In this lab, you will explore the Virtual Machine instance options and create several VMs with different characteristics.

## Objectives
In this lab, you explore the available options for VMs and see the differences between locations.
In this lab, you learn how to perform the following tasks:

• Create several standard VMs

• Create advanced VMs

## Task 1: Create a utility virtual machine

### Create a VM

1. For **Name**, Use a unique name for your instance. 
2. For Region and Zone select **us-central1** and **us-central1-c** respectively.
3. For **Machine type**, **use n1-standard-1 (1 vCPUs, 3.75 GB memory)**
4. Use this Gcloud command line codeto create the VM instance 
<div style = "background-color:black;color:white;text-align:left; font-family:CourierNewPSMT; vertical-align: middle; padding:5px 47px;">gcloud compute instances create   [Enter the Vm name here] -- machine-type "n1-standard-1" --region "us-central1" --zone "us-central1-c"
</div>

### Explore the VM details
1. Use this gcloud command line code to view the details of the VM instance created.
<div style = "background-color:black;color:white;text-align:left; font-family:CourierNewPSMT; vertical-align: middle; padding:5px 47px;">gcloud compute instances describe [Instance name here]
</div>

2. You can't change the machine type, the CPU platform, or the zone.

You can add network tags and allow specific network traffic from the internet through firewalls.

Some properties of a VM are integral to the VM, are established when the VM is created, and cannot be changed. Other properties can be edited. You can add
additional disks and you can also determine whether the boot disk is deleted when the instance is deleted. Normally the boot disk defaults to being deleted
automatically when the instance is deleted. But sometimes you will want to override this behavior. This feature is very important because you cannot create
an image from a boot disk when it is attached to a running instance. So you would need to disable **Delete boot disk when instance is deleted** to enable creating a system image from the boot disk.
3. **Availability policies**.

You can't convert a non-preemptible instance into a preemptible one. This choice must be made at VM creation. A preemptible instance can be interrupted at any time and is available at a lower cost.

If a VM is stopped for any reason, (for example an outage or a hardware failure)the automatic restart feature will start it back up. Is this the behavior you want?
Are your applications idempotent (written to handle a second startup properly)?

During host maintenance, the VM is set for live migration. However, you can have the VM terminated instead of migrated.

If you make changes, they can sometimes take several minutes to be implemented, especially if they involve networking changes like adding firewalls
or changing the external IP.

### Explore the VM logs
Use this gcloud command line explore the VM logs.
<div style = "background-color:black;color:white;text-align:left; font-family:CourierNewPSMT; vertical-align: middle; padding:5px 47px;">gcloud logging logs list
</div>

### Task 2: Create a Windows virtual machine

**Create a VM**
1. Specify the following, and leave the remaining settings as their defaults:


Property                         |  Value (type value or select option as specified)
---------------------------------|--------------------------------------------------
Name                             |  Type a name for your VM
Region                           |  europe-west2
Zone                             |  europe-west2-a
Machine type                     |  n1-standard-2(2 vCPUs, 7.5 GB memory)
Boot                             |  disk Change
Public Images > Operating system |  Windows Server
Version                          |  Windows Server 2016 Datacenter Core
Boot disk type                   |  SSD persistent disk
Size (GB)                        |  100

2. For **Firewall**,**Allow HTTP traffic** and **Allow HTTPS traffic**
3. RDP is the Remote Desktop Protocol. You would need the RDP client installed on your local machine to connect to the Windows desktop.

Instructions for connecting to Windows VMs are here:
https://cloud.google.com/compute/docs/instances/windows/connecting-to-windows-instance

Use this gcloud command line code to create a Windpws VM instance with Vm's name as **new-windows-vm** and boot disk name as **windows-vm-boot-disk**.

<div style = "background-color:black;color:white;text-align:left; font-family:CourierNewPSMT; vertical-align: middle; padding:5px 47px;">gcloud compute instances create new-windows-vm --region=europe-west2 --zone=europe-west2-a --machine-type=n1-standard-2 --subnet=default --network-tier=PREMIUM --maintenancepolicy=MIGRATE --tags=http-server,httpsserver --image=windows-server-2016-dc-core-v20200813 --image-project=windows-cloud --boot-disk-size=100GB --boot-disk-type=pd-ssd --boot-disk-device-name=windows-vm-boot-disk --no-shielded-secure-boot --shieldedvtpm --shielded-integrity-monitoring --reservation-affinity=any </div>


### To allow Fire wall rules use this command line code

***For http-server***
<div style = "background-color:black;color:white;text-align:left; font-family:CourierNewPSMT; vertical-align: middle; padding:5px 47px;">gcloud compute firewall-rules create default-allow-http --direction=INGRESS --priority=1000 --network=default --action=ALLOW --rules=tcp:80 --source-ranges=0.0.0.0/0 --target-tags=http-server</div>

***For httpsserver***
<div style = "background-color:black;color:white;text-align:left; font-family:CourierNewPSMT; vertical-align: middle; padding:5px 47px;">gcloud compute firewall-rules create default-allow-https --direction=INGRESS --priority=1000 --network=default --action=ALLOW --rules=tcp:443 --source-ranges=0.0.0.0/0 --target-tags=https-server</div>

### Set the password for the VM

1. Use the gcloud compute reset-windows-password command to create a new account and password or reset the existing account password for the logged in user.
2. Use this gcloud command line code toset the password for the VM.
<div style = "background-color:black;color:white;text-align:left; font-family:CourierNewPSMT; vertical-align: middle; padding:5px 47px;">gcloud compute reset-windows-password [INSTANCE NAME here]</div>

3. you will be presented with a confirmation prompt; this will need to beaccepted by entering **Y** and/or pressing **Enter**. it can be rejected by entering **N**, then pressing **Enter**.
4. Once confirmed, confirmation of password reset will look as follows.

 output looks like this(**do not copy**)
 
Resetting and retrieving password for [username] on [INSTANCE NAME]    
updated [https;//www.googleapis.com/compute/v1/projects/project-name/zones/zone/instances/instance-name]
**ip_address: ip-address**

**password:   password**

**username:   username**

3. Copy the provided password
You will not connect to the Windows VM during this lab. However, the process would look something like the following (depending on the RDP client you installed). 

The RDP client shown can be installed for Chrome here:
https://chrome.google.com/webstore/detail/chrome-rdp-for-googleclo/mpbbnannobiobpnfblimoapbephgifkm?hl=en-US
On the VM instances page, you would click RDP for your Windows VM and connect with the password copied earlier.

### Task 3: Create a custom virtual machine

**Create a VM**

1. Specify the following, and leave the remaining settings as their defaults:

Property Value    |  (type value or select option as specified)
------------------|--------------------------------------------
Name              |   Type a name for your VM
Region            |   us-west1
Zone              |   us-west1-b
Machine           |   type Custom
Cores             |   6 vCPU
Memory            |   32 GB

2. Use this gcloud command line code to create the VM instance with 
<div style = "background-color:black;color:white;text-align:left;font-family:calibri;font-size:15px;  vertical-align: middle; padding:10px 47px;">gcloud beta compute instances create [Enter Instance Name here] --zone=us-west1-b --machine-type=custom-6-32768 --subnet=default --networktier=PREMIUM --maintenance-policy=MIGRATE  --image=debian-9-stretch-v20200805 --image-project=debian-cloud --boot-disk-size=10GB --boot-disk-type=pd-standard --bootdisk-device-name=instance-us-west --reservation-affinity=any</div>

### Connect via SSH to your custom VM
1. Use this command line code to **SSH** into the custom Vm.
<div style = "background-color:black;color:white;text-align:left; font-family:CourierNewPSMT; vertical-align: middle; padding:5px 47px;">gloud compute ssh [stance Name]</div>

2. To see information about unused and used memory and swap space on ur custom VM, run the following command: 
<div style = "background-color:black;color:white;text-align:left; font-family:CourierNewPSMT; vertical-align: middle; padding:5px 47px;">free</div>
3. To see details about the RAM installed on your VM, run the following
command:
<div style = "background-color:black;color:white;text-align:left; font-family:CourierNewPSMT; vertical-align: middle; padding:5px 47px;">sudo dmidecode -t 17</div>
4. To verify the number of processors, run the following command:
<div style = "background-color:black;color:white;text-align:left; font-family:CourierNewPSMT; vertical-align: middle; padding:5px 47px;">nproc</div>
5. To see details about the CPUs installed on your VM, run the following
command:
<div style = "background-color:black;color:white;text-align:left; font-family:CourierNewPSMT; vertical-align: middle; padding:5px 47px;">lscpu</div>
6. To exit the SSH terminal, run the following command:
<div style = "background-color:black;color:white;text-align:left; font-family:CourierNewPSMT; vertical-align: middle; padding:5px 47px;">exit
</div>

### Task 4: Review

In this lab, you created several virtual machine instances of different types with
different characteristics. One was a small utility VM for administration purposes.
You also created a standard VM and a custom VM. You launched both Windows
and Linux VMs and deleted VMs.

