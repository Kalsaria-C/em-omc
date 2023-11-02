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

8. Click on **Create Parser**.
   ![](./images/parsers-save-01.png "UIdescription")

9. The parser is saved successfully.
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

## **Task 6:**  Save User Defined Source

1. Click on **Create Source**.
   ![](./images/sources-create-11.png "UIdescription")

   The source is saved successfully.
   ![](./images/sources-create-12.png "UIdescription")

## **Task 7:**  Navigate to Uploads

1. Click on the option **Uploads** inside **Resources** sidebar menu at the left.
   ![](./images/uploads-access.png "UIdescription")

  Now you are in **Uploads**.
   ![](./images/uploads-page.png "UIdescription")

## **Task 8:**  Upload logs file

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

7. Click on **Set Properties**.
   ![](./images/upload-logs-08.png "UIdescription")

8. At **Source**, select **DNS Exfiltration on Windows Systems** which is the source we created previously. Click on **Save Changes**.
   ![](./images/upload-logs-09.png "UIdescription")

9. Click on **Next**.
   ![](./images/upload-logs-10.png "UIdescription")

10. Click on **Upload**.
   ![](./images/upload-logs-11.png "UIdescription")

11. When the **Submission Status** is **Success**, click on **Close**.
   ![](./images/upload-logs-12.png "UIdescription")

   The logs file is uploaded successfully.
   ![](./images/upload-logs-13.png "UIdescription")

## **Task 9:**  Navigate to Log Explorer

1. Click on the **Log Explorer** option inside the drop-down menu.
   ![](./images/log-explorer-access.png "UIdescription")

2. Now you are in **Log Explorer**.
   ![](./images/log-explorer.png "UIdescription")

## **Task 10:**  Create a new Log Search

1. Type the following query in the text input **'Log Source' = 'DNS Exfiltration on Windows Systems' | timestats count as logrecords by 'Log Source'**
   ![](./images/log-search-create-01.png "UIdescription")

2. Open the **Time Range** drop-down and click on **Custom**.
   ![](./images/log-search-create-02.png "UIdescription")

3. Mark **Quick Select** and select **Last 8 Years**. Click on **Apply**.
   ![](./images/log-search-create-03.png "UIdescription")

4. Click on **Run** and see the results below.
   ![](./images/log-search-create-04.png "UIdescription")

## **Task 11:**  Save the Log Search

1. Open the **Actions** drop-down and click on **Save as...**.
   ![](./images/log-search-create-05.png "UIdescription")

1. Specify the **Search Name** and the **Search Description (optional)**. Then, click on **Save** button.
   ![](./images/log-search-create-06.png "UIdescription")

  The log search is saved successfully.
   ![](./images/log-search-create-07.png "UIdescription")

## **Task 12:**  Navigate to Detection Rules

1. Click on the option **Detection Rules** inside **Resources** sidebar menu at the left.
   ![](./images/detection-rules-access.png "UIdescription")

  Now you are in **Detection Rules**.
   ![](./images/detection-rules.png "UIdescription")

## **Task 13:**  Create Scheduled search detection rule

1. In this lab you will use both **Scheduled search detection rule** and **Ingest time detection rule** for creating more performant and sophisticated detection rules for alarms.

  Click on **Create** inside **Detection Rules** page to start creating a new detection rule.
   ![](./images/scheduled-search-create-01.png "UIdescription")

  First, we will create a **Scheduled search** type detection rule.
   ![](./images/scheduled-search-create-02.png "UIdescription")

2. Specify a **Rule name** and **Saved search compartment**. At **Saved search**, select **DNS Exfiltration on Windows Systems** which is the log search we created previously.
   ![](./images/scheduled-search-create-03.png "UIdescription")

3. Select **Monitoring** as **Target Service**. Specify a **Metric Compartment**, **Metric Namespace** and **Metric Name**. Finally, set the **Interval** to **30 Minutes** and click on **Create detection rule**.
   ![](./images/scheduled-search-create-04.png "UIdescription")
   
4. The detection rule is saved successfully.
   ![](./images/scheduled-search-create-05.png "UIdescription")

## **Task 14:**  See the results of Scheduled search detection rule

1. Click on **DNS Exfiltration on Windows Systems** scheduled search type detection rule.
   ![](./images/scheduled-search-results-01.png "UIdescription")

2. At **Results**, we can see there has been a DNS Exfiltration Attempt (change the **Quick Selects** if needed).
   ![](./images/scheduled-search-results-02.png "UIdescription")

3. Click on **View In Metric Explorer**.
   ![](./images/scheduled-search-results-03.png "UIdescription")

4. We can see the same result in the **Metrics Explorer** view.
   ![](./images/scheduled-search-results-04.png "UIdescription")

## **Task 15:**  Navigate to Labels

1. Click on the option **Labels** inside **Resources** sidebar menu at the left.
   ![](./images/labels-access.png "UIdescription")

2. Click on **Create** inside **Labels** page to start creating a new label.
   ![](./images/labels-create.png "UIdescription")

## **Task 16:**  Create new Label

1. Specify the **Label** and **Description (optional)**.
   ![](./images/label-create-01.png "UIdescription")

2. Mark the **Use this label to indicate a problem** checkbox inside **Denotes Problem**. Then, select **High** for **Problem Priority**. Click on **Create**.
   ![](./images/label-create-02.png "UIdescription")

## **Task 17:**  Create Ingest time detection rule

1. Click on **Create** inside **Detection Rules** page.
   ![](./images/scheduled-search-create-01.png "UIdescription")

2. Click on **Ingest time detection rule**.
   ![](./images/ingest-time-option.png "UIdescription")

3. Specify the **Rule name**. For the **Label**, select **DNS Exfiltration Attempt****Label** which is the one we created previously and **DNS Exfiltration on Windows Systems** for **Filter by log source**.
   ![](./images/ingest-time-create-01.png "UIdescription")

4. Select **Monitoring** as **Target Service**. Specify a **Metric Compartment**, **Metric Namespace** and **Metric Name**. Finally, click on **Create detection rule**.
   ![](./images/ingest-time-create-02.png "UIdescription")

   The detection rule is saved successfully.
   ![](./images/ingest-time-create-03.png "UIdescription")

## **Task 18:**  Create alarm for Detection Rules

1. Navigate to **Detection Rules**.

2. Click on **DNS Exfiltration on Windows Systems** Scheduled search type.
   ![](./images/scheduled-search-alarm-01.png "UIdescription")

3. Click on **Create Alarm**.
   ![](./images/scheduled-search-alarm-02.png "UIdescription")

4. Specify an **Alarm name** and **Alarm body (optional)**. Set **Critical** for **Alarm severity**.
   ![](./images/scheduled-search-alarm-03.png "UIdescription")

5. Inside **Destination** click on **Create a topic**.
   ![](./images/scheduled-search-alarm-04.png "UIdescription")

6. Specify a **Topic name** and **Topic description (optional)**. Select **Email** as **Subscription protocol** and specify a **Subscription Email**. Click on **Create topic and subscription**.
   ![](./images/scheduled-search-alarm-05.png "UIdescription")

7. Click on **Save alarm**.
   ![](./images/scheduled-search-alarm-06.png "UIdescription")

   The alarm is saved successfully.
   ![](./images/scheduled-search-alarm-07.png "UIdescription")

8. Do the same process of **Create Alarm** for the **DNS Exfiltration on Windows Systems** Ingest time type.

## **Task 19:**  Upload logs file and see the results of Ingest time Detection Rule

1. Click on the option **Uploads** inside **Resources** sidebar menu at the left.
   ![](./images/uploads-access.png "UIdescription")

  Now you are in **Uploads**.
   ![](./images/uploads-page.png "UIdescription")

2. Click on the **Upload** we created for this live lab.
   ![](./images/ingest-time-results-01.png "UIdescription")

3. Modify the file **microsoft-dns-logs.log** so the date of each log is less than 12 hours before current UTC time.
   ![](./images/ingest-time-results-02.png "UIdescription")

4. Click on **Select Files** and open the logs file we modified.
   ![](./images/ingest-time-results-03.png "UIdescription")
   ![](./images/ingest-time-results-04.png "UIdescription")

5. Click on **Next**.
   ![](./images/ingest-time-results-05.png "UIdescription")

6. Click on **Set Properties**.
   ![](./images/ingest-time-results-06.png "UIdescription")

7. At **Source**, select **DNS Exfiltration on Windows Systems** which is the source we created previously. Click on **Save Changes**.
   ![](./images/ingest-time-results-07.png "UIdescription")

8. Click on **Next**.
   ![](./images/ingest-time-results-08.png "UIdescription")

9. Click on **Upload**.
   ![](./images/ingest-time-results-09.png "UIdescription")

10. When the **Submission Status** is **Success**, click on **Close**.
   ![](./images/ingest-time-results-10.png "UIdescription")

   The logs file is uploaded successfully.

11. Navigate to Detection Rules and select the **DNS Exfiltration on Windows Systems** ingest time type detection rule.
   ![](./images/ingest-time-results-11.png "UIdescription")

12. At **Results**, select **12 hours** for the **Quick Selects**. We can see there has been a DNS Exfiltration Attempt.
   ![](./images/ingest-time-results-12.png "UIdescription")

13. Click on **View In Metric Explorer**.
   ![](./images/ingest-time-results-13.png "UIdescription")

14. Select **12 hours** at **Quick selects**. We can see the same result in the **Metrics Explorer** view.
   ![](./images/ingest-time-results-14.png "UIdescription")

## **Task 20:**  See the Alarms results

1. Navigate to **Alarms**.

2. At **Alarm Definitions** click on the alarms we created.
   ![](./images/alarm-results-01.png "UIdescription")

3. We can see both alarms are **Firing**.
   ![](./images/alarm-results-02.png "UIdescription")
   ![](./images/alarm-results-03.png "UIdescription")


## Acknowledgements
* **Author** - Oswaldo Osuna, Logging Analytics Development Team
* **Contributors** -  Kumar Varun, Logging Analytics Product Management - Kiran Palukuri, Logging Analytics Product Management - Vikram Reddy, Logging Analytics Development Team 
* **Last Updated By/Date** - Oswaldo Osuna, Nov 2 2023
