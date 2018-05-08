# Elastic Compute Cloud

EC2 is Web service that provides resizable compute capacity in the cloud.

EC2 reduces time required to obtain server instances to minutes, allowing to scale cpacity up and down as soon as requirements change.

VM in the cloud.

Huge budget to start experimenting is not required anymore. It makes a new range of business of Start up.

## EC2 options

* On demand : fixed rate by the hour or by the second (for Linux instances only). No long term commitment.
    * Use case : Workload is unpredictable and can't be interrupted. 
* Reserved : capacity reservation in advance (1 or 3 years terms). Provides savings if capacity requirement is well known in advance. Users able to make upfront payment. Predictable usage. 4 types : Standard RI, convertible RI, scheduled.
    
* Spot : bid price for instance capacity. Provides great saving if application has flexible start and end times.
    * Applications that are only feasible at very low computing prices. Example : for big data processing.
    * Pay for the started hour if you terminate the instance
    * If AWS terminates the instance, you get the started hour for free
* Dedicated hosts : physical servers dedicated. Example : when licenses or legal constraints apply, which does not support multi-tenant virtualization.
    * Can be purchased on demand
    * Can be purchased as a reservation

## EC2 Instance types

* D2 : Dense storage - file servers, data warehousing ... - Density
* R4 : Memory Optimized - memory intensive - RAM
* M4 : General purpose - application servers - Main choice
* C4 : Compute optimized - CPU intensive - Compute
* G2 : Graphics intensive - Video encoding, Streaming - Graphics
* I2 : High Speed Storage - Databases - IOPS
* F1 : Change the physical hardware FPGA - hardware acceleration for code - FPGA
* T2 : Low cost general purpose - web servers, small database - T Cheap
* P2 : GPU / Graphics - Bitcoins mining - graPhics
* X1 : Extreme Memory

DR Mc GIFT PX

# EBS : Elastic Block Storage

Block Based Storage : can be used to install OS or Database (as opposed to S3).
EBS volumes are places in a specific Availability Zone and automatically replicated to protect from the failure of a storage array (within a single Availability Zone).

EBS volume types :

*  General Purpose SSD (GP2)
    * 3 IOPS per GB up to 10 000 IOPS
    
* Provisioned IOPS SSD (IO1)
    * Intensive applications such as relational DB or NoSQL
    * If more than 10 000 IOPS is needed
    * 20 000 IOPS per volume
    
* Throughput Optimized HDD (ST1)
    * Big data
    * Log processing
    * Magnetic
    * Can't boot
    
* Cold HDD (SC1)
    * Less frequently accessed
    * File server
    * Low cost storage
    * Magnetic
    * Can't boot
    
* Magnetic (Standard) 
    * Low cost per GB
    * Bootable

Note : IOPS - IO Operations Per Second - the number of operations the storage system can perform per second

1 EBS volume can't be mounted on multiple EC2 instances.
If such a setup is needed, use EFS.

1 Subnet 1 one availability zone (Subnet can't cross multiple availability zones).
Volume is a virtual hard disk.

## EC2 lab - 1 

* Termination protection is turned off by default
* The default action for the root volume is to be deleted when the instance is terminated
* EBS root volume can't be encrypted by default, but can be encrypted with third party tool such as bitlocker or in the AWS console using the API
* Additional volumes can be encrypted

## EC2 lab - 2 : Security Groups

Security group is a virtual firewall


* Rules are only *allowing* traffic. Rules are not **denying** traffic.
* All inbound traffic is blocked by default
* All outbound traffic is allowed automatically by default
* Any rule applied to a security group applies immediately. Changes take effect immediately
* Any number of EC2 oinstances can be attached to a security group
* Multiple security groups can be attached to an EC2 instance
* Security groups are *Stateful* : any inbound round allowing traffic is automatically associated to a rule allowing traffic out
* You can't block specific IP adresses with security groups. Instead use NACL
 
## EC2 lab - 3 : EBS volumes

* Volumes are virtual hard disks

**Snapshots**
* Snapshots are point in time copy of the volumes
* Snapshots are existing on S3
* Snapshots are incremental. Only the blocks that are changed since the last snapshot are moved to S3.
* In order to take a snapshot of a root volume, one should stop the instance. However it is possible to take a snapshot while the instance is running
* Snapshots can be made public

**Images**
* AMI can be created from both snapshots and volumes

**Volumes**
* EBS volume size can be changed on the fly
* EBS volume type can be modified on the fly (while being used) except Standard volumes (Magnetic) which can't be modified

* EBS volumes of an EC2 instance **are ALWAYS in the same availability zone** as the EC2 instance AZ
* In order to move a volume to a new availability zone, one should first create a snapshot (or an image of the EC2 instance). 
The snapshot (or the image) can then be copied to another AZ/region with the copy action.

**Encryption**
* Snapshots of encrypted volumes are encrypted automatically
* Volumes restored from encrypted snapshots are encrypted automatically
* Snapshots can be shared only if they are unencrypted.


## EC2 - Creating a Windows EC2 instance and RAID groups

### RAID, volumes and snapshots

RAID = Redundant Array of Independant Disks

* RAID 0 : no redundancy, striped, good performance
* RAID 1 : mirrored 1 <-> 1
* RAID 5 : 3 disks or more, AWS does not recommend RAID 5 on EBS. Write parity using checksum. 
* RAID 10 : combination of RAID 1 and RAID 0 - good performance and redundancy

Striping : segmenting logically sequential data so that consecutive segments are stored on different physical storage devices 

RAID is used when you don't get the required disks I/O.
Solution : add more volumes and put them together in a RAID array.
Ex : database which is not supported by AWS such as Cassandra

### Lab : creation of a RAID 0 array on a W2012 server

Create striped volume in from disk management console.

![RAID 0 on Windows 2012 server](RAID%200%20W2012.png)

### Taking a snapshot of RAID array 

A snapshot of a RAID array excludes data held in OS and application cache.

It doesn't matter on a single volume, but it is a problem on a RAID array due to interdependencies of disks in the array.

Solution : 

1. Stop the application writing to the disks
2. Flush all caches to the disk

How ?
Either 
- Freeze the file system
- Unmount the RAID array
- or shut down the associated EC2 instance 

### EC2 - Create an AMI 

* To create a snapshot of an EBS volume that serves as a root device, one should stop the instance first 
* Snapshots of encrypted volumes are encrypted automatically
* Volumes restored from encrypted snapshots are encrypted automatically
* You can share snapshots only if they are unencrypted (because the encryption key is tied to the AWS account)

### EC2 - AMI EBS root volume VS instance store

### EC2 - ELB & Health checks

* Classic ELB and Application ELB (operates at level 7)
* Instances monitored by ELB are reported as In service or Out of service
* Health check check the instance by talking to it. It is done through HTTP or HTTPS.
* ELB has its own DNS name. Public Ip address is not given.

**READ the ELB FAQ (classic)** for the exam.

### EC2 - CloudWatch

* Standard monitoring : 5 minutes
* Detailed monitoring : 1 minute


* Dashboard
* Alarms
* Events : helps to respond to changes
* Logs :aggregate, monitor and store logs

Do not confuse Cloud trail (auditing )with Cloud watch (monitoring)

### EC2 - The AWS CLI


