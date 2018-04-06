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

 
