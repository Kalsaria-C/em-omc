# DNS Exfiltration on Windows Systems

## Introduction

In this lab, you'll learn how to use problem labels and scheduled tasks together for creating more performant and sophisticated detection rules for alarms.

Log Name: Microsoft-Windows-DNS-Client/Operational
Event IDs: 3000 (Query), 3001 (Response)

Estimated Lab Time: 10 minutes


### Objectives

In this lab, you will:
* Label DNS query events in windows events
* Use query time lookup to verify DNS server by machines
* Create alarm per windows machine for DNS exfiltration

## **Task 1:**  Navigate to Log Explorer

1. Click on the **Log Explorer** option inside the drop-down menu.
   ![](./images/log-explorer-access.png "UIdescription")

2. Now you are in **Log Explorer**.
   ![](./images/log-explorer.png "UIdescription")

## **Task 2:**  Create a new Log Search

1. Type the following query in the text input: **'Entity Type' = 'Host (Windows)' and 'Log Source' = 'Windows System Events' | timestats count as logrecords by 'Log Source'**
   ![](./images/log-search-query.png "UIdescription")

2. Click on **Run** and see the results below.
   ![](./images/query-results.png "UIdescription")

## **Task 3:**  Save the Log Search

1. Specify the **Search Name** and the **Search Description (optional)**. Then, click on **Save** button.
   ![](./images/log-search-save.png "UIdescription")

  The log search is saved successfully.
   ![](./images/log-search-saved-successfully.png "UIdescription")

## **Task 4:**  Navigate to Detection Rules

1. Click on the **Administration** option inside the drop-down menu to access to **Administration Overview**.
   ![](./images/admin-access.png "UIdescription")

2. Click on the option **Detection Rules** inside **Resources** sidebar menu at the left.
   ![](./images/detection-rules-access.png "UIdescription")

  Now you are in **Detection Rules**.
   ![](./images/detection-rules.png "UIdescription")

## **Task 5:**  Create Scheduled search detection rule

1. In this lab you will use both **Scheduled search detection rule** and **Ingest time detection rule** for creating more performant and sophisticated detection rules for alarms.

  Click on **Create** inside **Detection Rules** page to start creating a new detection rule.
   ![](./images/detection-rules-create.png "UIdescription")

  First, we will create a **Scheduled search** type detection rule.
   ![](./images/scheduled-search-option.png "UIdescription")

2. Specify a **Rule name** and **Saved search compartment**. Then, select the **Saved search** we created for the scheduled task.
   ![](./images/specify-rule-name.png "UIdescription")

3. Select **Monitoring** as **Target Service**. Specify a **Metric Compartment**, **Metric Namespace** and **Metric Name**. Finally, set the **Interval** to **1 Hours** and click on **Create detection rule**.
   ![](./images/detection-rule-create.png "UIdescription")

4. The detection rule is saved successfully.
   ![](./images/detection-rule-saved-successfully.png "UIdescription")

## **Task 6:**  Navigate to Labels

1. Click on the option **Labels** inside **Resources** sidebar menu at the left.
   ![](./images/labels-access.png "UIdescription")

2. Click on **Create** inside **Labels** page to start creating a new label.
   ![](./images/labels-create.png "UIdescription")

## **Task 7:**  Create new Label

1. Specify the **Label** and **Description (optional)**.
   ![](./images/label-create-01.png "UIdescription")

2. Mark the **Use this label to indicate a problem** checkbox inside **Denotes Problem**. Then, select **High** for **Problem Priority**. Click on **Create**.
   ![](./images/label-create-02.png "UIdescription")

## **Task 8:**  Create Ingest time detection rule

1. Click on **Create** inside **Detection Rules** page.
   ![](./images/detection-rules-create.png "UIdescription")

2. Click on **Ingest time detection rule**.
   ![](./images/ingest-time-option.png "UIdescription")

3. Specify the **Rule name**. Select the **Label** we created and **Host (Windows)** for **Filter by entity type**.
   ![](./images/ingest-time-create-01.png "UIdescription")

4. Select **Monitoring** as **Target Service**. Specify a **Metric Compartment**, **Metric Namespace** and **Metric Name**. Finally, click on **Create detection rule**.
   ![](./images/ingest-time-create-02.png "UIdescription")

5. The detection rule is saved successfully.
   ![](./images/ingest-time-saved-successfully.png "UIdescription")
## Acknowledgements
* **Author** - Oswaldo Osuna, Logging Analytics Development Team
* **Contributors** -  Kumar Varun, Logging Analytics Product Management - Kiran Palukuri, Logging Analytics Product Management - Vikram Reddy, Logging Analytics Development Team 
* **Last Updated By/Date** - Oct 18 2023
