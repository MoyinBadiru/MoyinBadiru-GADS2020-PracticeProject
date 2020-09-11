

> # LAB: CREATING VIRTUAL MACHINES
>

 ## Task 1: Create a utility virtual machine



1.  In the Cloud Console, on the  Navigation menu , click  Compute Engine  >  VM instances.
2.  Click  Create.
3.  For  Name, type a name for your instance. Hover over the question mark icon for advice about what constitutes a properly formed name.
4.  For  Region  and  Zone select  us-central1  and  us-central1-c respectively.
5. For  Machine type,  click  n1-standard-1 (1 vCPUs, 3.75 GB memory).
6.  Click  Management, security, disks, networking, sole tenancy.
7.  Click  Networking.
8.  For  Network interfaces, click the  Edit  icon
9.  Select  None  for  External IP.
10.  Click  Done.

      **COMMAND LINE EQUIVALENT:**

         gcloud compute instances create instance-1 --zone=us-central1-c --machine-type=n1-standard-1 --no-address --image=debian-9-stretch-v20200902 --image-project=debian-cloud --boot-disk-size=10GB --boot-disk-type=pd-standard --boot-disk-device-name=instance-1 


## Task 2: Create a Windows virtual machine


1.  On the  Navigation menu, click  Compute Engine  >  VM instances.
2.  Click  Create instance.
3.  Specify the following, and leave the remaining settings as their defaults:
Name Type a name for your VM
Region europe-west2
Zone europe-west2-a
Machine type n1-standard-2(2 vCPUs, 7.5 GB memory)
Boot disk Change
Public Images > Operating system Windows Server
Version Windows Server 2016 Datacenter Core
Boot disk typeSSD persistent disk
Size (GB) 100
4. Click  Select.
5.  For  Firewall, enable  Allow HTTP traffic  and  Allow HTTPS traffic.
6.  Click  Create.

    **COMMAND LINE EQUIVALENT:**

        gcloud compute instances create instance-2 --zone=europe-west2-a --machine-type=n1-standard-2 --tags=http-server,https-server --image=windows-server-2016-dc-core-v20200813 --image-project=windows-cloud --boot-disk-size=100GB --boot-disk-type=pd-standard --boot-disk-device-name=instance-2


        gcloud compute firewall-rules create default-allow-http --direction=INGRESS --priority=1000 --network=default --action=ALLOW --rules=tcp:80 --source-ranges=0.0.0.0/0 --target-tags=http-server

        gcloud compute firewall-rules create default-allow-https --direction=INGRESS --priority=1000 --network=default --action=ALLOW --rules=tcp:443 --source-ranges=0.0.0.0/0 --target-tags=https-server


7.  Set the password for the VM
8. Click on the name of your Windows VM to access the  VM instance details.
9. You don't have a valid password for this Windows VM: you cannot log in to the Windows VM without a password. Click  Set Windows password.
10.  Click  Set.
11.  Copy the provided password, and click  CLOSE

       **COMMAND LINE EQUIVALENT:**

         gcloud compute reset-windows-password instance-2 --zone=europe-west2-a



## Task 3: Create a custom virtual machine


1.  On the  Navigation menu, click  Compute Engine  >  VM instances.
2.  Click  Create instance.
3.  Specify the following, and leave the remaining settings as their defaults: 
Name Type a name for your VM
Region us-west1
Zone us-west1-b
Machine type Custom
Cores 6 vCPU
Memory 32 GB
4. Click Create.

    **COMMAND LINE EQUIVALENT:**

       gcloud compute instances create instance-3 --zone=us-west1-b --machine-type=custom-6-32768
    
5.  Connect via SSH to your custom VM
6.  For the custom VM you just created, click SSH.

    **COMMAND LINE EQUIVALENT:**

        gcloud compute ssh instance-3 --zone=us-west1-b

7.  To see information about unused and used memory and swap space on your custom VM:

         free
8. To see details about the RAM installed on your VM: 

        sudo dmidecode -t 17
9. To verify the number of processors:

        nproc
10. To see details about the CPUs installed on your VM:

        lscpu
11. To exit the SSH terminal:  

         exit 