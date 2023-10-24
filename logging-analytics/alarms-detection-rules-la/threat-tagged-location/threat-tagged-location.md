# Sensitive Data Access from Threat Tagged Location

## Introduction

In this lab, you'll learn how to create multi-conditional labels for creating more sophisticated ingest time detection rules based on Threat Intelligence Enrichment.

Estimated Lab Time: 15 minutes


### Objectives

In this lab, you will:
* Extend/Customize Log Sources
* Object Storage bucket or access to a system, web-access from a location tagged by TISS risky
* Create alarms and verify

## **Task 1:**  Navigate to Sources

1. Click on the **Administration** option inside the drop-down menu to access to **Administration Overview**.
   ![](./images/admin-access.png "UIdescription")

2. Click on the option **Sources** inside **Resources** sidebar menu at the left.
   ![](./images/sources-access.png "UIdescription")

  Now you are in **Sources**.
   ![](./images/sources-page.png "UIdescription")

## **Task 2:**  Create Source from Oracle-defined and Add field enrichment

Logging Analytics provides automatic threat intelligence enrichment for your logs that can help identify public IP addresses which could have some level of threat associated with them. Learning about the possible threats early can help separate and mitigate them.

To enable the threat intelligence enrichment feature, Geolocation Field is needed.

1. Search for **OCI Object Storage Access Logs** and click on **Duplicate**.
   ![](./images/source-duplicate-01.png "UIdescription")

1. Click on **Field Enrichment** and on **Add field enrichment**.
   ![](./images/source-duplicate-02.png "UIdescription")

2. Select **Geolocation** in **Function**. Then, Select **Host IP Address (Client)** in **IP Address Field** and mark **Threat Intelligence enrichment**. Finally, click on **Add field enrichment**.
   ![](./images/source-duplicate-03.png "UIdescription")

  The field enrichment is added successfully.
   ![](./images/source-duplicate-04.png "UIdescription")

## **Task 3:**  Save User Defined Source

1. Click on **Create Source**.
   ![](./images/source-save-01.png "UIdescription")

  The source is created successfully.
   ![](./images/source-save-02.png "UIdescription")

## **Task 4:**  Navigate to Detection Rules

1. Click on the option **Detection Rules** inside **Resources** sidebar menu at the left.
   ![](./images/detection-rules-access.png "UIdescription")

  Now you are in **Detection Rules**.
   ![](./images/detection-rules.png "UIdescription")

## **Task 5:**  Create Ingest time detection rule

1. Click on **Create** inside **Detection Rules** page.
   ![](./images/detection-rules-create-01.png "UIdescription")

2. Click on **Ingest time detection rule**.
   ![](./images/detection-rules-create-02.png "UIdescription")

3. Specify the **Rule name**. Select **Action Failed** for **Label** and **Copy of OCI Object Storage Access Logs** for **Filter by log source**.
   ![](./images/detection-rules-create-03.png "UIdescription")

4. Select **Monitoring** for **Target Service**. Specify a **Metric Compartment**, **Metric Namespace** and **Metric Name**. Click on **Create detection rule**.
   ![](./images/detection-rules-create-04.png "UIdescription")

  The ingest time detection rule is saved successfully.
   ![](./images/detection-rules-create-05.png "UIdescription")


## Acknowledgements
* **Author** - Oswaldo Osuna, Logging Analytics Development Team
* **Contributors** -  Kumar Varun, Logging Analytics Product Management - Kiran Palukuri, Logging Analytics Product Management - Vikram Reddy, Logging Analytics Development Team 
* **Last Updated By/Date** - Oswaldo Osuna, Oct 24 2023
