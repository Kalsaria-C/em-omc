# Problem Labels for Custom Apps-Logs

## Introduction

In this lab, you'll learn best practices for proactively monitoring custom applications. You'll learn how to create custom problem labels, new fields (EFDs, query time).

Estimated Lab Time: 20 minutes


### Objectives

In this lab, you will:
* Extract new fields using eval, extract
* Create new labels & EFDs from log-explorer
* Create new labels, EFDs in a Log Source
* Create alarms on new labels and verify

## **Task 1:**  Navigate to Parsers

1. Click on the **Administration** option inside the drop-down menu to access to **Administration Overview**.
![](./images/admin-access.png "UIdescription") 

2. Click on the option **Parsers** inside **Resources** sidebar menu at the left.
   ![](./images/parsers-navigate-01.png "UIdescription")

  Now you are in **Parsers**.
   ![](./images/parsers-navigate-02.png "UIdescription")

## **Task 2:**  Create Parser

1. Click on **Create Parser** and select **Regex Type**.
   ![](./images/parsers-create-01.png "UIdescription")

2. Click on **Advanced**. Specify a **Name** and **Description (optional)**.
   ![](./images/parsers-create-02.png "UIdescription")

3. Download sample logs file for [Log Sample](./files/f5-firewall-logs.log)</br>
   Add the **f5-firewall-logs.log** we downloaded to **Example log content**.
   ![](./images/parsers-create-03.png "UIdescription")

4. Specify the following regular expression at **Parser regular expression**: **{TIMEDATE}\s+(.+)**
   ![](./images/parsers-create-04.png "UIdescription")

5. Select **Message** for the second field.
   ![](./images/parsers-create-05.png "UIdescription")

7. Click on **Parser Test** and on **Run Test**.
   ![](./images/parsers-create-06.png "UIdescription")

   We verify that the fields are matching with the example logs we provided.
   ![](./images/parsers-create-07.png "UIdescription")

8. Click on **Create Parser**.
   ![](./images/parsers-create-08.png "UIdescription")

9. The parser is saved successfully.
   ![](./images/parsers-create-09.png "UIdescription")

## **Task 3**  Navigate to Sources

1. Click on the option **Sources** inside **Resources** sidebar menu at the left.
   ![](./images/sources-access.png "UIdescription")

  Now you are in **Sources**.
   ![](./images/sources-page.png "UIdescription")

## **Task 4:**  Create User Defined Source

1. Click on **Create Source**.
   ![](./images/source-create-01.png "UIdescription")

2. Specify the **Name** and **Description (optional)**. Select **File** as **Source Type**. Select **Network Firewall** at **Entity Types**.
   ![](./images/source-create-02.png "UIdescription")

3. Mark the **Specific parser(s)** option. Then, select **F5 Firewall System Application**.
   ![](./images/source-create-03.png "UIdescription")

## **Task 5:**  Add Extended Fields

   We are able to create **Extended Fields** derived from existing **Base Fields**. In this case, we will create an **Extended Field** for the **Message** field we created previously in order to get the **Source IP**.

1. Click on **Extended Fields** and on **Add**.
   ![](./images/efd-create-01.png "UIdescription")

2. Download example base field content file for [Log Sample](./files/example-base-field-content.log)</br>
  Select **Message** as **Base Field**. Set the downloaded file content for **Example Base Field Content**. For **Extract Expression** set **source ip:?\s{Source IP:[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}}**.
   ![](./images/efd-create-02.png "UIdescription")

3. Click on **Test Definition** and see more details about test results to verify the match succeeded.
   ![](./images/efd-create-03.png "UIdescription")

4. Click on **Add**.
   ![](./images/efd-create-04.png "UIdescription")

5. The extended field definition is added successfully.
   ![](./images/efd-create-05.png "UIdescription")

## **Task 6:**  Add Labels

1. Click on **Labels** and on **Add conditional label**.
   ![](./images/labels-create-01.png "UIdescription")

2. Select **Source IP** as **Input Field** and **Not In** as **Operator**. Add the following IPv4 addresses to **Condition Value**: 192.168.1.101, 192.168.1.102, 192.168.1.103
   ![](./images/labels-create-02.png "UIdescription")

3. Select **Security Problem** label.
   ![](./images/labels-create-03.png "UIdescription")

5. Click on **Add**.
   ![](./images/labels-create-04.png "UIdescription")
   
  The conditional label is added successfully.
   ![](./images/labels-create-05.png "UIdescription")

## **Task 7:**  Save User Defined Source

1. Click on **Create Source**.
   ![](./images/source-save-01.png "UIdescription")
   
  The source is created successfully.
   ![](./images/source-save-02.png "UIdescription")

## **Task 8:**  Navigate to Uploads

1. Click on the option **Uploads** inside **Resources** sidebar menu at the left.
   ![](./images/uploads-access.png "UIdescription")

  Now you are in **Uploads**.
   ![](./images/uploads-page.png "UIdescription")

## **Task 9:**  Upload logs file

1. Click on **Upload Files**.
   ![](./images/upload-logs-01.png "UIdescription")

2. Specify an **Upload Name** and **Log Group Compartment**.
   ![](./images/upload-logs-02.png "UIdescription")

3. Select an existing **Log Group** or create a new one.
   ![](./images/upload-logs-03.png "UIdescription")

4. Download sample logs file for [Log Sample](./files/f5-firewall-logs.log)</br>
   Click on **Select Files** and select the **f5-firewall-logs.log** file.
   ![](./images/upload-logs-04.png "UIdescription")
   ![](./images/upload-logs-05.png "UIdescription")

6. Click on **Next**.
   ![](./images/upload-logs-06.png "UIdescription")

7. Click on **Set Properties**.
   ![](./images/upload-logs-07.png "UIdescription")

8. At **Source**, select **Problem Labels for Custom Apps-Logs** which is the source we created previously. Click on **Save Changes**.
   ![](./images/upload-logs-08.png "UIdescription")

9. Click on **Next**.
   ![](./images/upload-logs-09.png "UIdescription")

10. Click on **Upload**.
   ![](./images/upload-logs-10.png "UIdescription")

11. When the **Submission Status** is **Success**, click on **Close**.
   ![](./images/upload-logs-11.png "UIdescription")

   The logs file is uploaded successfully.
   ![](./images/upload-logs-12.png "UIdescription")

## **Task 10:**  Navigate to Log Explorer

1. Click on the **Log Explorer** option inside the drop-down menu.
   ![](./images/log-explorer-access.png "UIdescription")

2. Now you are in **Log Explorer**.
   ![](./images/log-explorer.png "UIdescription")

## **Task 11:**  Create a new Log Search

1. For this lab, we are going to save a query using **extract** command to add a new field from an existing one. In this case, we want to add a new field derived from the **Message** to obtain the **Destination IP**.
  Type the following query in the text input: **'Log Source' = 'Problem Labels for Custom Apps-Logs' | extract field = Message 'destination ip:?\s{Destination IP:[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}}' | timestats count as logrecords by 'Log Source'**
   ![](./images/log-search-create-01.png "UIdescription")

2. Open the **Time Range** drop-down and click on **Custom**.
   ![](./images/log-search-create-02.png "UIdescription")

3. Mark **Quick Select** and select **Last 90 Days**. Click on **Apply**.
   ![](./images/log-search-create-03.png "UIdescription")

3. Click on **Run** and see the results below.
   ![](./images/log-search-create-04.png "UIdescription")

4. Click on **Save as...** option inside **Actions** drop-down menu.
   ![](./images/log-search-create-05.png "UIdescription")

5. Select a **Saved Search Compartment**. Specify the **Search Name** and the **Search Description (optional)**. Then, click on **Save** button.
   ![](./images/log-search-create-06.png "UIdescription")

  The log search is saved successfully.
   ![](./images/log-search-create-07.png "UIdescription")

## **Task 12:**  Navigate to Detection Rules

1. Click on the **Administration** option inside the drop-down menu to access to **Administration Overview**.
   ![](./images/admin-access.png "UIdescription")

2. Click on the option **Detection Rules** inside **Resources** sidebar menu at the left.
   ![](./images/detection-rules-access.png "UIdescription")

  Now you are in **Detection Rules**.
   ![](./images/detection-rules.png "UIdescription")

## **Task 13:**  Create Scheduled search detection rule

1. Click on **Create** inside **Detection Rules** page to start creating a new detection rule.
   ![](./images/scheduled-search-create-01.png "UIdescription")

  We will create a **Scheduled search** type detection rule.
   ![](./images/scheduled-search-create-02.png "UIdescription")

2. Specify a **Rule name** and **Saved search compartment**. Then, select **Problem Labels for Custom Apps-Logs** as **Saved search** which is the one we created previously.
   ![](./images/scheduled-search-create-03.png "UIdescription")

3. Select **Monitoring** as **Target Service**. Specify a **Metric Compartment**, **Metric Namespace** and **Metric Name**. Finally, set the **Interval** to **30 Minutes** and click on **Create detection rule**.
   ![](./images/scheduled-search-create-04.png "UIdescription")

  The detection rule is saved successfully.
   ![](./images/scheduled-search-create-05.png "UIdescription")

## **Task 14:**  Create Alarm

1. Click on **Problem Labels for Custom Apps-Logs** Scheduled search type.
   ![](./images/scheduled-search-alarm-01.png "UIdescription")

2. Click on **Create Alarm**.
   ![](./images/scheduled-search-alarm-02.png "UIdescription")

3. Specify an **Alarm name** and **Alarm body (optional)**. Set **Critical** for **Alarm severity**.
   ![](./images/scheduled-search-alarm-03.png "UIdescription")

4. Inside **Destination** click on **Create a topic**.
   ![](./images/scheduled-search-alarm-04.png "UIdescription")

5. Specify a **Topic name** and **Topic description (optional)**. Select **Email** as **Subscription protocol** and specify a **Subscription Email**. Click on **Create topic and subscription**.
   ![](./images/scheduled-search-alarm-05.png "UIdescription")

6. Click on **Save alarm**.
   ![](./images/scheduled-search-alarm-06.png "UIdescription")

   The alarm is saved successfully.
   ![](./images/scheduled-search-alarm-07.png "UIdescription")

## **Task 15:**  See Detection Rules and Alarms results

1. Navigate to Detection rules **(see Task 12)** and click on **Problem Labels for Custom Apps-Logs** which is the **Detection Rule** we created.
   ![](./images/results-01.png "UIdescription")

2. At **Results** we can see there has been a **Security Problem**.
   ![](./images/results-02.png "UIdescription")

3. Click on **View In Metric Explorer**.
   ![](./images/results-03.png "UIdescription")

4. We can see the same result in the **Metrics Explorer** view.
   ![](./images/results-04.png "UIdescription")

5. Click on the **Navigation menu**.
   ![](./images/results-05.png "UIdescription")

6. Click on **Observability and Management**. Then, click on **Alarm Definitions** inside **Monitoring**.
   ![](./images/results-06.png "UIdescription")

7. Click on **Problem Labels for Custom Apps-Logs**.
   ![](./images/results-07.png "UIdescription")

8. We can see the alarm is **Firing**.
   ![](./images/results-08.png "UIdescription")


## Acknowledgements
* **Author** - Oswaldo Osuna, Logging Analytics Development Team
* **Contributors** -  Kumar Varun, Logging Analytics Product Management - Kiran Palukuri, Logging Analytics Product Management - Vikram Reddy, Logging Analytics Development Team 
* **Last Updated By/Date** - Oswaldo Osuna, Nov 6 2023
