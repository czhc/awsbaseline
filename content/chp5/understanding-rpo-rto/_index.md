---
title: "Understanding RTO and RPO"
date: 2020-06-13T05:37:25+08:00
weight: 5

---


### Everything fails all the time! Understanding RTO and RPO for your Business

**What are RTO and RPO?**

Recovery time objective (RTO) and recovery point objective (RPO) are two key metrics to consider when developing a DR plan. 

1. **RTO (Recovery Time Objective)** represents the time it takes after a disruption to restore a business process to its service level, as defined by the operational level agreement (OLA). For example, if a disaster occurs at 12:00 PM (noon) and the RTO is eight hours, the DR process should restore the business process to the acceptable service level by 8:00 PM.

2. **RPO (Recovery Point Objective)**, which is also expressed in hours, represents how much data you could lose when a disaster happens. For example, if a disaster occurs at 12:00 PM (noon) and the RPO is one hour, the system should recover all data that was in the system before 11:00 AM. Data loss will span only one hour, between 11:00 AM and 12:00 PM (noon).

You have to decide on an acceptable RTO and RPO based on the financial impact to the business when systems are unavailable. You have to determine the financial impact by considering many factors, such as the loss of business and damage to your reputation due to downtime and the lack of systems availability.

Octank CTO decided RTO and RPO details
Sample DR plan [here](https://d1.awsstatic.com/products/CloudEndure/The_Disaster_Recovery_Plan_Checklist.pdf)
