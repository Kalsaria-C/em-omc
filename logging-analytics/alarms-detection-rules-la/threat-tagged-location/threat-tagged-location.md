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

## **Task 2:**  Create Source and add field enrichment

Logging Analytics provides automatic threat intelligence enrichment for your logs that can help identify public IP addresses which could have some level of threat associated with them. Learning about the possible threats early can help separate and mitigate them.

To enable the threat intelligence enrichment feature, Geolocation Field is needed.

1. Click on **Create Source**.
   ![](./images/source-create-01.png "UIdescription")

2. Specify the **Name** and **Description (optional)**. Select **File** as **Source Type** and **OCI Object Storage Bucket** at **Entity Types**.
   ![](./images/source-create-02.png "UIdescription")

3. Mark the **Specific parser(s)** option. Then, select **OCI Object Storage Access Log Format**.
   ![](./images/source-create-03.png "UIdescription")

4. Click on **Field Enrichment** and on **Add field enrichment**.
   ![](./images/source-create-04.png "UIdescription")

5. Select **Geolocation** in **Function**. Then, Select **Host IP Address (Client)** in **IP Address Field** and mark **Threat Intelligence enrichment**. Finally, click on **Add field enrichment**.
   ![](./images/source-create-05.png "UIdescription")

  The field enrichment is added successfully.
   ![](./images/source-create-06.png "UIdescription")

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

1. Click on **Create rule** inside **Detection Rules** page.
   ![](./images/detection-rules-create-01.png "UIdescription")

2. Click on **Ingest time detection rule**.
   ![](./images/detection-rules-create-02.png "UIdescription")

3. Specify the **Rule name**. Select **Sensitive Data Access from Threat Tagged Location** for **Label** and **Sensitive Data Access from Threat Tagged Location** for **Filter by log source**.
   ![](./images/detection-rules-create-03.png "UIdescription")

4. Select **Monitoring** for **Target Service**. Specify a **Metric Compartment**, **Metric Namespace** and **Metric Name**. Click on **Create detection rule**.
   ![](./images/detection-rules-create-04.png "UIdescription")

  The ingest time detection rule is saved successfully.
   ![](./images/detection-rules-create-05.png "UIdescription")

## **Task 6:**  Create alarm

1. Click on **Sensitive Data Access from Threat Tagged Location** which is the **Detection Rule** we created.
   ![](./images/create-alarm-01.png "UIdescription")

2. Click on **Create Alarm**.
   ![](./images/create-alarm-02.png "UIdescription")

3. Specify an **Alarm name** and **Alarm body (optional)**. Set **Critical** for **Alarm severity**.
   ![](./images/create-alarm-03.png "UIdescription")

4. Inside **Destination** click on **Create a topic**.
   ![](./images/create-alarm-04.png "UIdescription")

5. Specify a **Topic name** and **Topic description (optional)**. Select **Email** as **Subscription protocol** and specify a **Subscription Email**. Click on **Create topic and subscription**.
   ![](./images/create-alarm-05.png "UIdescription")

6. Click on **Save alarm**.
   ![](./images/create-alarm-06.png "UIdescription")

   The alarm is saved successfully.
   ![](./images/create-alarm-07.png "UIdescription")

## **Task 7:**  Navigate to Uploads

1. Click on the option **Uploads** inside **Resources** sidebar menu at the left.
   ![](./images/uploads-access.png "UIdescription")

  Now you are in **Uploads**.
   ![](./images/uploads-page.png "UIdescription")

## **Task 8:**  Upload logs file

1. Click on **Upload Files**.
   ![](./images/upload-logs-01.png "UIdescription")

2. Specify an **Upload Name** and **Log Group Compartment**. Select a **Log Group** or create a new one.
   ![](./images/upload-logs-02.png "UIdescription")

5. Download sample logs file for [Log Sample](./files/threat-tagged-location-logs.log)</br>
   Modify the file **threat-tagged-location-logs** so the date of each log is less than 1 hour before current UTC time.
   ![](./images/modify-logs.png "UIdescription")

6. Click on **Select Files** and select the **threat-tagged-location-logs.log** file.
   ![](./images/upload-logs-03.png "UIdescription")
   ![](./images/upload-logs-04.png "UIdescription")

6. Click on **Next**.
   ![](./images/upload-logs-05.png "UIdescription")

7. Click on **Set Properties**.
   ![](./images/upload-logs-06.png "UIdescription")

8. At **Source**, select **Copy of OCI Object Storage Access Logs** which is the source we created previously. Click on **Save Changes**.
   ![](./images/upload-logs-07.png "UIdescription")

9. Click on **Next**.
   ![](./images/upload-logs-08.png "UIdescription")

10. Click on **Upload**.
   ![](./images/upload-logs-09.png "UIdescription")

11. When the **Submission Status** is **Success**, click on **Close**.
   ![](./images/upload-logs-10.png "UIdescription")

   The logs file is uploaded successfully.
   ![](./images/upload-logs-11.png "UIdescription")

## **Task 9:**  See Detection Rules and Alarms results

1. Navigate to Detection rules **(see Task 4)** and click on **Sensitive Data Access from Threat Tagged Location** which is the **Detection Rule** we created.
   ![](./images/results-01.png "UIdescription")

2. At **Results** we can see there has been a **Sensitive Data Access from Threat Tagged Location**.
   ![](./images/results-02.png "UIdescription")

3. Click on **View In Metric Explorer**.
   ![](./images/results-03.png "UIdescription")

4. We can see the same result in the **Metrics Explorer** view.
   ![](./images/results-04.png "UIdescription")

5. Click on the **Navigation menu**.
   ![](./images/results-05.png "UIdescription")

6. Click on **Observability and Management**. Then, click on **Alarm Definitions** inside **Monitoring**.
   ![](./images/results-06.png "UIdescription")

7. Click on **Sensitive Data Access from Threat Tagged Location**.
   ![](./images/results-07.png "UIdescription")

8. We can see the alarm is **Firing**.
   ![](./images/results-08.png "UIdescription")


## Acknowledgements
* **Author** - Oswaldo Osuna, Logging Analytics Development Team
* **Contributors** -  Kumar Varun, Logging Analytics Product Management - Kiran Palukuri, Logging Analytics Product Management - Vikram Reddy, Logging Analytics Development Team 
* **Last Updated By/Date** - Oswaldo Osuna, Nov 3 2023
