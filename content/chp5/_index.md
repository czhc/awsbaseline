
---
title: "Disaster Recovery"
date: 2020-06-13T05:37:25+08:00
weight: 5
chapter: true
pre: "<b>Chp 5. </b>"

---

### Chapter 5

# Disaster Recovery

The Octank marketplace is alive and hitting 100 MAUs and they are no longer recording order placements on paper!

Their data in production is important and they cannot afford losing customers for a few hours like they used to. Help them understand what is disaster recovery, and how to prepare themselves for the unlikely event of failure.



### Everything fails all the time! Understanding RTO and RPO for your Business

**What are RTO and RPO?**

Recovery time objective (RTO) and recovery point objective (RPO) are two key metrics to consider when developing a DR plan. 

1. **RTO (Recovery Time Objective)** represents the time it takes after a disruption to restore a business process to its service level, as defined by the operational level agreement (OLA). For example, if a disaster occurs at 12:00 PM (noon) and the RTO is eight hours, the DR process should restore the business process to the acceptable service level by 8:00 PM.

2. **RPO (Recovery Point Objective)**, which is also expressed in hours, represents how much data you could lose when a disaster happens. For example, if a disaster occurs at 12:00 PM (noon) and the RPO is one hour, the system should recover all data that was in the system before 11:00 AM. Data loss will span only one hour, between 11:00 AM and 12:00 PM (noon).

You have to decide on an acceptable RTO and RPO based on the financial impact to the business when systems are unavailable. You have to determine the financial impact by considering many factors, such as the loss of business and damage to your reputation due to downtime and the lack of systems availability.

Octank CTO decided RTO and RPO details
Sample DR plan [here](https://d1.awsstatic.com/products/CloudEndure/The_Disaster_Recovery_Plan_Checklist.pdf)

### Simple Disaster Recovery Using Backup + Restore

This section provides an overview of backup, restore and disaster recovery in AWS, along with a comprehensive list of requirements that you must consider before configuring your architecture.

You can watch the [video] (https://www.youtube.com/watch?v=cBh_Tlg-2yM&list=PLhr1KZpdzukf2K67aldy_A1pAC-SkpPWz&index=8&t=34s) below to understand more.
{{< youtube id="cBh_Tlg-2yM&list=PLhr1KZpdzukf2K67aldy_A1pAC-SkpPWz&index=8&t=0s" >}}

#### Case 1: Storage and Archiving

The most basic services you can use for backup and archival are [Amazon S3] (https://aws.amazon.com/s3/) and [Amazon Glacier] (https://aws.amazon.com/glacier/). They both offer unlimited capacity and require no volume or media management as backup data sets grow. The  pay-for-whatyou-use model and low cost per GB/month make these services a good fit for data protection use cases.

***Amazon S3***

You can use Amazon S3 to store and retrieve any amount of data, at any time, from anywhere on the web. Amazon S3 offers a range of storage classes designed for different use cases. These include:
- Amazon S3 Standard for general-purpose storage of frequently
accessed data.
- Amazon S3 Standard for infrequent Access for long-lived, but less
frequently accessed data.
- Amazon Glacier for long-term archive

When choosing the Amazon S3 tier that will best suit you, some of the factors to consider are:

* Access frequency (how often do you need to read/write objects)
* Durability and Availability of objects
* Pricing (such as min capacity charge, min storage duration charge, retrieval fee)

You can view details of the different [storage classes] (https://aws.amazon.com/s3/storage-classes/), which can help you decide in setting up your architecture.

***Amazon Glacier***

Amazon Glacier is an extremely low-cost, cloud archive storage service that provides secure and durable storage for data archiving and online backup. To keep costs low, Amazon Glacier is optimized for data that is infrequently accessed and for which retrieval times of several hours are acceptable. 

You can view a [detailed pricing comparison] ((https://aws.amazon.com/s3/pricing/)) of Amazon S3 classes and Amazon Glacier.

***AWS Backup***

[AWS Backup] (https://aws.amazon.com/backup/) is a fully managed backup service that makes it easy to centralize and automate the backup of data across AWS services in the cloud and on premises. AWS Backup automates and consolidates backup tasks that were previously performed service-by-service, and removes the need to create custom scripts and manual processes. 

AWS Backup support backup and restore for: [Amazon EFS] (https://aws.amazon.com/efs/), [DynamoDB] (https://aws.amazon.com/dynamodb/), [Amazon EC2] (https://aws.amazon.com/ec2/), [Amazon EBS] (https://aws.amazon.com/ebs/), [Amazon RDS] (https://aws.amazon.com/rds/), [Amazon Aurora] (https://aws.amazon.com/rds/aurora/) and [AWS Storage Gateway] (https://aws.amazon.com/storagegateway/). If you are interested to understand how AWS Backup integrated with these services, visit this [documentation] (https://docs.aws.amazon.com/aws-backup/latest/devguide/working-with-other-services.html).

You can watch the [video] (https://www.youtube.com/watch?v=QDiXzFx2iMU&t=34s) below to have an overview of AWS Backup

{{< youtube id="QDiXzFx2iMU&t=34s" >}}

#### Case 2: Backing Up EC2 with EBS Snapshots

[Amazon EBS] (https://aws.amazon.com/ebs/) provides the ability to create snapshots (backups) of any Amazon EBS volume. It takes a copy of the volume and places it in Amazon S3, where it is stored redundantly in multiple Availability Zones. The first snapshot is a full copy of the volume; ongoing snapshots store incremental block-level changes only.

You can watch the [video] (https://www.youtube.com/watch?v=TKEUrhhEy34) below to understand more about EBS, how to create EBS snapshot, monitoring of snapshot costs and automating snapshot management.

{{< youtube id="TKEUrhhEy34" >}}

You can check these documentations for some key actions you can do with EBS: [create snapshot] (https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-creating-snapshot.html), [delete snapshot] (https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-deleting-snapshot.html), [copy snapshot] (https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-copy-snapshot.html), [share snapshot] (https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-modifying-snapshot-permissions.html) and [automate snapshot] (https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/snapshot-lifecycle.html).

#### Case 3: Backing up RDS

Amazon RDS includes features for automating database backups. Amazon RDS creates a storage volume snapshot of your database instance, backing up the entire DB instance, not just individual databases. 

DB snapshots are user-initiated backups that enable you to back up your DB instance to a known state as frequently as you like, and then restore to that state at any time. The steps are easy and you can find them [here] (https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_CreateSnapshot.html).


#### Labs and Hands-on Resources

Looks like you are all set! To help you implement, here are some labs that we recommend you can practice on.

1. Creating Periodic Backup of AWS Resources [here] (https://wellarchitectedlabs.com/reliability/200_labs/200_testing_backup_and_restore_of_data/) 

2. Creating asynchronous backup of data in S3 [here] (https://wellarchitectedlabs.com/reliability/200_labs/200_bidirectional_replication_for_s3/) 

3. Creating EBS Backup for EC2 Instance[here] (https://aws.amazon.com/premiumsupport/knowledge-center/back-up-instance-store-ebs/) 

4. Creating DB Snapshot for Relational Database Service [here] (https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_CreateSnapshot.html) 

5. Restoring Data from DB Snapshot of Relational Database Service [here] (https://aws.amazon.com/premiumsupport/knowledge-center/restore-rds-instance-from-snapshot/) 

6. Backing Up and Restoring with AWS Backup [here] (https://docs.aws.amazon.com/aws-backup/latest/devguide/getting-started.html)


### Automating Failure Detection and Recovery Using Cloudwatch and Lambda 

With Amazon CloudWatch, you can monitor your application workloads, create alarms, set thresholds for alarms, and even create self-mitigating responses or send notifications in near-real time to your operations team.

You can watch the video below for a quick overview of Amazon Cloudwatch.

{{< youtube id="a4dhoTQCyRA" >}}

#### Failure Detection with Amazon Cloudwatch 

Failure detection is important in maintaining the reliability, availability, and performance of your AWS solutions. You should collect data from all of the parts in your infrastructure so that you can more easily debug a multi-point failure if one occurs.

***Choose Metrics to Monitor***

To establish a baseline, you need to understand what metrics you can monitor, and decide within your organization how detailed you want to monitor. 

You can find the detailed metrics for EC2, Application Load Balancer (ALB) and RDS in the documentations:

   1. [EC2] (https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/viewing_metrics_with_cloudwatch.html) metrics: including instance (CPU utilization, byte read/write etc) and CPU credits.
   2. [Application Load Balancer] (https://docs.aws.amazon.com/elasticloadbalancing/latest/application/load-balancer-cloudwatch-metrics.html) metrics: including Active connection count, condumed LCUs and healthy host count.
   3. [RDS] (https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/MonitoringOverview.html) metrics: including etwork throughput, client connections, I/O for read, write, or metadata operations, and burst credit balances.




***Set Alarms and Thresholds***

A CloudWatch Alarm is always in one of three states: OK, ALARM, or INSUFFICIENT_DATA. When the metric is within the range that you have defined as acceptable, the Monitor is in the OK state. When it breaches a threshold it transitions to the ALARM state. If the data needed to make the decision is missing or incomplete, the monitor transitions to the INSUFFICIENT_DATA state.


***Actions Based on Alarm State***

Alarms watch metrics and execute actions by:

1. Publishing notifications to [Amazon SNS] (https://aws.amazon.com/sns/?whats-new-cards.sort-by=item.additionalFields.postDateTime&whats-new-cards.sort-order=desc) topics or by 
2. Initiating Auto Scaling actions with AWS Lambda

SNS can deliver notifications using HTTP, HTTPS, Email, or an [Amazon SQS] (https://aws.amazon.com/sqs/) queue. Your application can receive these notifications and then act on them in any desired way.

**Email Notifications**

You can set the alarm to send a notification to an Amazon Simple Notification Service (Amazon SNS) topic. This allows you to create subscriptions based on the topic. For this use case, I trigger an alarm and send an informational email any time the message queue has over 1 million visible messages. The following screenshot shows the configuration of this notification.

Follow the steps in this [documentation] (https://docs.aws.amazon.com/codepipeline/latest/userguide/tutorials-cloudwatch-sns-notifications.html)

Watch the seamless integration of AWS Cloudwatch and SNS (Email) in the tutorial below.

{{< youtube id="YC-sVSbeowA" >}}

**SMS Text Notifications**

To send a text message, create an SNS topic. Then create a subscription and for Protocol, choose SMS and enter the phone number to text. Make sure the SMS is available in your Region and be aware that you may need to request a raise in SMS limits.

ADD PHOTO

#### Automating with AWS Lambda

AWS Lambda is a great way to remediate incidents that occur based on your alarms. AWS Lambda is a serverless compute service that runs your code in response to events and automatically manages the underlying compute resources for you.

You can watch the [video] (https://www.youtube.com/watch?v=eOBq__h4OJ4) below to have an overview of AWS Lambda

{{< youtube id="eOBq__h4OJ4" >}}

In this example, you’re monitoring your microservices API that is behind an Application Load Balancer, traffic can’t reach the microservice, so it times out. You could have an alarm triggered to send an SNS notification to a topic to which a Lambda function is subscribed so it runs a describe-security-groups —group-namemicroserviceXYZ command to validate that the ports are still open for the load balancer. 

ADD PHOTO

You can set up an alarm configured which will trigger a notification to SNS. This invokes a Lambda function which in-turn makes changes to the security group in question.

You can read more [here] (https://aws.amazon.com/blogs/mt/alarms-incident-management-and-remediation-in-the-cloud-with-amazon-cloudwatch/)


***Create a Dashboard***

Once you determine the metrics you want to monitor and the baseline performance you are comfortable with, you can consolidate them in a dashboard for easier tracking. 

Amazon CloudWatch dashboards are customizable home pages in the CloudWatch console that you can use to monitor your resources in a single view, even those resources that are spread across different Regions. 

You can use CloudWatch dashboards to create customized views of the metrics and alarms for your AWS resources. You can follow this [tutorial] (https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/create_dashboard.html) on how to setup a basic dashboard.

Watch the video below to have a visual understanding to monitor multiple resources at once, view automatic dashboards that can be dynamically filtered, or create your own custom dashboards.

{{< youtube id="I7EFLChc07M" >}}

After creating your dashboard, you can have simple edits such as [adding/removing graphs] (https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/add_remove_graph_dashboard.html), [resizing graphs] (https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/move_resize_graph_dashboard.html) graphs, [editing graphs] (https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/edit_graph_dashboard.html)  and setting up [cross-account cross-region dashboards] (https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_xaxr_dashboard.html).


#### Labs and Hands-on Resources

1. Monitoring Your Resources with AWS Cloudwatch
with this [lab] (https://wellarchitectedlabs.com/performance-efficiency/100_labs/100_monitoring_with_cloudwatch_dashboards/) 

2. Enable or Disable detailed Monitoring for Your Instances with this [documentation] (https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-cloudwatch-new.html) 

3. Creating Notifications When Resource Changes are Made with Amazon Cloudwatch with this [lab] (https://aws.amazon.com/premiumsupport/knowledge-center/iam-cloudwatch-sns-rule/) 

4. Setting Enhanced Monitoring for Your RDS Application with this [documentation] (https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_Monitoring.OS.html) 


Resources

https://aws.amazon.com/blogs/mt/how-to-set-up-cloudwatch-anomaly-detection-to-set-dynamic-alarms-automate-actions-and-drive-online-sales/


