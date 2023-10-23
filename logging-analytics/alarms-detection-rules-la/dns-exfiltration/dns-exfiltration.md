# DNS Exfiltration on Windows Systems

## Introduction

In this lab, you'll learn how to use problem labels and scheduled tasks together for creating more performant and sophisticated detection rules for alarms.

Log Name: Microsoft-Windows-DNS-Client/Operational
Event IDs: 3000 (Query), 3001 (Response)

Estimated Lab Time: 15 minutes


### Objectives

In this lab, you will:
* Label DNS query events in windows events
* Use query time lookup to verify DNS server by machines
* Create alarm per windows machine for DNS exfiltration


## **Task 1:**  Navigate to Parsers

1. Click on the **Administration** option inside the drop-down menu to access to **Administration Overview**.
![](./images/admin-access.png "UIdescription") 

2. Click on the option **Parsers** inside **Resources** sidebar menu at the left.
   ![](./images/parsers-navigate-01.png "UIdescription")

  Now you are in **Parsers**.
   ![](./images/parsers-navigate-02.png "UIdescription")

## **Task 2:**  Create Parser from Oracle-defined

1. Search for **Microsoft DNS**. In the **Oracle-defined** one, click on **Actions** button and then on **Duplicate**.
   ![](./images/parsers-create-01.png "UIdescription")

2. Specify a **Name** and **Description (optional)**.
   ![](./images/parsers-create-02.png "UIdescription")

3. Download sample logs file for [Log Sample](./files/microsoft-dns-logs.log)</br>
   Add the **microsoft-dns-logs.log** we downloaded to **Example log content**.
   ![](./images/parsers-create-03.png "UIdescription")

4. Specify the following regular expression at **Parser regular expression**: **{TIMEDATE}\s+(\S+)\s+(\S+)\s+(\S+)\s+(.+)**
   ![](./images/parsers-create-04.png "UIdescription")

   As we modified the **Parser regular expression** two more fields were added.
   ![](./images/parsers-create-05.png "UIdescription")

5. Select **Event** for the first field added.
   ![](./images/parsers-create-06.png "UIdescription")

6. Select **Destination IP** for the second field added.
   ![](./images/parsers-create-07.png "UIdescription")

7. Click on **Parser Test** and on **Run Test**.
   ![](./images/parsers-create-08.png "UIdescription")

   We verify that the fields are matching with the example logs we provided.
   ![](./images/parsers-create-09.png "UIdescription")

## **Task 2:**  Save Parser

1. Click on **Create Parser**.
   ![](./images/parsers-save-01.png "UIdescription")

2. The parser is saved successfully.
   ![](./images/parsers-save-02.png "UIdescription")


## **Task 3:**  Navigate to Sources

1. Click on the **Administration** option inside the drop-down menu to access to **Administration Overview**.
   ![](./images/admin-access.png "UIdescription")

2. Click on the option **Sources** inside **Resources** sidebar menu at the left.
   ![](./images/sources-access.png "UIdescription")

  Now you are in **Sources**.
   ![](./images/sources-page.png "UIdescription")

## **Task 4:**  Create User Defined Source

1. Click on **Create Source**.
   ![](./images/sources-create-01.png "UIdescription")

2. Specify the **Name** and **Description (optional)**. Select **File** as **Source Type** and **Microsoft DNS Server** at **Entity Types**.
   ![](./images/sources-create-02.png "UIdescription")

3. Mark the **Specific parser(s)** option. Then, select **DNS Exfiltration on Windows Systems** which is the parser we created previously.
   ![](./images/sources-create-03.png "UIdescription")

## **Task 5:**  Add Labels

1. Click on **Labels** and on **Add conditional field**.
   ![](./images/sources-create-04.png "UIdescription")

2. Select **Destination IP** as **Input Field** and **Not In** as **Operator**. Add the following IPv4 addresses to **Condition Value**: 192.168.1.10, 10.0.0.5, 192.168.2.20, 10.1.1.1
   ![](./images/sources-create-05.png "UIdescription")

3. Click on **Create New Field**.
   ![](./images/sources-create-06.png "UIdescription")

4. Specify a **Name**, **Data Type** and **Description (optional)**. Click on **Create**.
   ![](./images/sources-create-07.png "UIdescription")

   The field is added successfully.
   ![](./images/sources-create-08.png "UIdescription")

5. Specify an **Output Value**.
   ![](./images/sources-create-09.png "UIdescription")

6. Click on **Add**.
   ![](./images/sources-create-10.png "UIdescription")

## **Task 5:**  Save User Defined Source

1. Click on **Create Source**.
   ![](./images/sources-create-11.png "UIdescription")

   The source is saved successfully.
   ![](./images/sources-create-12.png "UIdescription")

## **Task 6:**  Navigate to Uploads

1. Click on the option **Uploads** inside **Resources** sidebar menu at the left.
   ![](./images/uploads-access.png "UIdescription")

  Now you are in **Uploads**.
   ![](./images/uploads-page.png "UIdescription")

## **Task 7:**  Upload logs file

1. Click on **Upload Files**.
   ![](./images/upload-logs-01.png "UIdescription")

2. Specify an **Upload Name** and **Log Group Compartment**.
   ![](./images/upload-logs-02.png "UIdescription")

3. Click on **Create Log Group**.
   ![](./images/upload-logs-03.png "UIdescription")

4. Specify a **Name** and **Description (optional)**. Click on **Create**.
   ![](./images/upload-logs-04.png "UIdescription")

5. Download sample logs file for [Log Sample](./files/microsoft-dns-logs.log)</br>
   Click on **Select Files** and select the **microsoft-dns-logs.log** file.
   ![](./images/upload-logs-05.png "UIdescription")
   ![](./images/upload-logs-06.png "UIdescription")

6. Click on **Next**.
   ![](./images/upload-logs-07.png "UIdescription")

## **Task 8:**  Navigate to Log Explorer

1. Click on the **Log Explorer** option inside the drop-down menu.
   ![](./images/log-explorer-access.png "UIdescription")

2. Now you are in **Log Explorer**.
   ![](./images/log-explorer.png "UIdescription")

## **Task 9:**  Create a new Log Search

1. Type the following query in the text input: **'Entity Type' = 'Host (Windows)' and 'Log Source' = 'Windows System Events' | timestats count as logrecords by 'Log Source'**
   ![](./images/log-search-query.png "UIdescription")

2. Click on **Run** and see the results below.
   ![](./images/query-results.png "UIdescription")

## **Task 10:**  Save the Log Search

1. Specify the **Search Name** and the **Search Description (optional)**. Then, click on **Save** button.
   ![](./images/log-search-save.png "UIdescription")

  The log search is saved successfully.
   ![](./images/log-search-saved-successfully.png "UIdescription")

## **Task 11:**  Navigate to Detection Rules

1. Click on the **Administration** option inside the drop-down menu to access to **Administration Overview**.
   ![](./images/admin-access.png "UIdescription")

2. Click on the option **Detection Rules** inside **Resources** sidebar menu at the left.
   ![](./images/detection-rules-access.png "UIdescription")

  Now you are in **Detection Rules**.
   ![](./images/detection-rules.png "UIdescription")

## **Task 12:**  Create Scheduled search detection rule

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

## **Task 13:**  Navigate to Labels

1. Click on the option **Labels** inside **Resources** sidebar menu at the left.
   ![](./images/labels-access.png "UIdescription")

2. Click on **Create** inside **Labels** page to start creating a new label.
   ![](./images/labels-create.png "UIdescription")

## **Task 14:**  Create new Label

1. Specify the **Label** and **Description (optional)**.
   ![](./images/label-create-01.png "UIdescription")

2. Mark the **Use this label to indicate a problem** checkbox inside **Denotes Problem**. Then, select **High** for **Problem Priority**. Click on **Create**.
   ![](./images/label-create-02.png "UIdescription")

## **Task 15:**  Create Ingest time detection rule

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
* **Last Updated By/Date** - Oswaldo Osuna, Oct 23 2023
