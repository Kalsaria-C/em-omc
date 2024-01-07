# Unsuccessful Food Orders

## Introduction

In this lab, you will understand the concept of Parsers in Logging Analytics.

Estimated Time: 30 minutes.

### Objectives

In this lab you will:

* Create alarms for more than 30% unsuccessful orders in 15 mins
* Verify the alarm

### Prerequisites

This lab assumes you have:

* An Oracle Cloud Infrastructure account.

In this lab, you will create an alarm for real life based application. The API logs which we are using will be classified into **Livelab Passed API** and **Livelab Failed API**. In each 15 minutes interval if there are more than 30% of Livelab Failed APIs, an alarm will be triggered.

## Task 1: Create Labels

You will be creating two labels, one label as **Livelab Passed API** and other as **Livelab Failed API**, using these two labels, you will create a detection rule for each, from the two detection rule, you will create an alarm.

1. From **Navigation Menu** ![navigation-menu](images/navigation-menu.png) > **Observability & Management** > **Logging Analytics** > **Administration** > **Sources box**.
    ![administration-navigation](images/administration-navigation.png)
    ![sources-navigation](images/sources-navigation.png)

2. Search for **Livelab API Mushop Log Source**, which was created in [Lab 4: Create a Source](?lab=create-source). Click on it.

3. Click on **Edit** button.
    ![edit-source](images/edit-source.png)

4. Click on **Labels**, to add label. Cick on **Add conditional label**.
    ![labels](images/labels.png)

5. You will create label for Failed API. In the Conditions section:
    * Select the log field on which you want to apply the condition from the Input Field list. Select **Status** from dropdown list.
    * Select the operator from the Operator list. Select **Contains** or **Equals**. Both can be used in the given usecase.
    * In the Condition Value field, specify the value of the condition to be matched for applying the label. For failed APIs, values of Status can be **401, 400, 404, 406, 408** which we extracted using parsers from log records.
    * Under Actions, select from the already available Oracle-defined or user created labels. If required, you can create a new label by clicking **Create Label**.
    ![add-label-1](images/add-label-1.png)

6. **Create Label** dialog box will appear. Fill in the details:
    * **Label Name:** Enter the label name. For example, **Livelab Failed API**.
    * (Optional) **Description:**  Enter the details about the label.
    * Labels can be marked as being a problem with a priority to make those log entries more prominent in the Log Explorer. To assign priority to the label. Under Livelab Failed API select **Yes** check box.
    * In the Problem Priority field, click the down arrow and select a priority. For example, select **Medium**.
    * A log entry will be assigned a problem priority based on the labels that get attached to the log entry. In this case, if Livelab Failed API has a problem priority of Medium, any log entry that matches a condition such that it gets the Livelab Failed API label would have a problem priority of Medium.
    * In the **Related Terms** field, enter the terms that are related to the log entry.
    * Click on **Create**.
![add-label-2](images/add-label-2.png)

7. Similarly, add another label, named **Livelab API Passed**. Uncheck the **Use this label to indicate a problem**, as are not having any problem for passed APIs. For adding condition:
    * If the **Status** does not contain or not equal to **401, 400, 404, 406, 408**, the log record can be labelled as passed.
    * Select **Status** from dropdown list in Input Field List. Select **Not Contain** operator. Add **401** as condition value.
    * **Not Contain** operator only allows for one value, so add more conditions by clicking on the Add Condition icon, marked as 2 in below image.
    * Select the logical operation to apply on the multiple conditions. Select **AND**.
    * Similarly add other 4 conditions where Status does not contain **406,409,400,404**.
    * Click on **Add**.
![add-label-3](images/add-label-3.png)

8. In the **Edit Source**, you will be able to see the two condition with its associated label. Click on **Save Changes**.
    ![labels-added](images/labels-added.png)

## Task 2: Create Detection Rules

Create two ingest time detection rules, as discussed in [Lab 6](?lab=create-and-trigger-ingest-time-detection-rule).

1. One rule for detecting **Livelab API Passed** label. Fields to be filled in Create detection rule page:
    * **Rule name:** Livelab Detect Passed API.
    * **Metric Namespace:** livelabmetricnamespace.
    * **Metric Name:** livelab_name.
    ![detection-rule-1](images/detection-rule-1.png)
     * Click on **Create detection rule**.

2. Other rule for detecting **Livelab Detect Failed API**. Fields to be filled in Create detection rule page:
    * **Rule name:** Livelab Detect Failed API.
    * **Metric Namespace:** livelabmetricnamespace.
    * **Metric Name:** livelab_name.
![detection-rule-2](images/detection-rule-2.png)
     * Click on **Create detection rule**.

3. Make sure that Metric Namespace and Metric Name remains same throughout the task, or else results may not appear.

## Task 3: Create an Alarm

1. Navigate to **Create Alarm page** as discussed in Option 1 of [Lab 8: Task 3](?lab=create-and-verify-alarm#Task3:CreateanAlarm)

2. Provide alarm name as **Livelab Failed APIs more than 30%**. Click on **Switch to Advanced Mode**, as a complex query will be required which will be using two labels from detection rule to create this alarm.
    ![alarm-adv-mode](images/alarm-adv-mode.png)

3. Make sure that the compartment and Metric Name is same as given for detection rules. Inside query editor, paste this query:
    ```
    <copy>livelab_name[15m]{label = "Livelab API Failed"}.grouping().sum() / (livelab_name[15m]{label = "Livelab API Passed"}.grouping().sum() + livelab_name[15m]{label = "Livelab API Failed"}.grouping().sum()) > 0.3</copy>
    ```
    This query  is the condition, when the alarm will trigger. Query implies, if the total no of log records with failed labels divide by total no of log records (failed labels and passed labels) is greater than 0.3 i.e. more than 30%, then the alarm will trigger.

    ![alarm-query](images/alarm-query.png)

    Currently, there is not data uploaded after creating alarm, so you see the graph is empty. You can have a table view by clicking on **Show Data Table**.

4. Now, **Define alarm notification**, select the **Destination service**, **compartment** and **Topic**, if there are no existing topic, you can create a new one just by clicking on **Create a topic**. For more information regarding these options, you can refer [Lab 2: Task 5](?lab=alarms-detection-rules#Task5:CreateAlarmsandNotifications)
    ![alarm-end](images/alarm-end.png)

5. Click on **Save alarm**. **Alarm Definitions page** will show up, providing the details of alarm, with a **Ok** mark.
    ![alarm-before-triggering](images/alarm-before-triggering.png)

6. Now, your alarm is ready. To test it, you will have to give some log records.

## Task 4: Verify an Alarm

1. A **python script** is attached with this lab. Download it, run it. A file named **logrecords\_for\_livelab.txt** will be created at the location, where this script is executed. These file will contains 1000 random log records, generated in interval of your current UTC time and 2 hours before your current UTC time.

    >**NOTE :** Alarm only works if the logs are not more than 2 hours older.

2. Refer to [Lab 5](?lab=upload-log-file), for uploading the local file to console. Once the file is uploaded and processed, you will see **Processing Status** as Successful, as shown in below image.
    ![file-uploaded](images/file-uploaded.png)

3. As the file is processed, the log records will also be parsed with the provided parser. All logs will be labelled as **Livelab Failed API** or **Livelab Passed API**. The alarm will check all the logs in interval of 15mins, runs it query, and will be triggered as soon as the queries satisfies.

4. Open **Navigation Menu** ![navigation-menu](images/navigation-menu.png) > **Observability & Management** > **Monitoring** > **Alarm Definitions** > **Livelab Failed APIs more than 30%** alarm. You will notice, the alarm has changed its state from **Ok** to **Firing**. A graph can be seen under **Alarm data** as shown in image. Click on **Show Data Table**
    ![alarm-triggered-graph](images/alarm-triggered-graph.png)

5. From data table, you can clearly observe, the alarm has been triggered 5 times, in interval of 15 minutes, in last hour. Click on **Quick selects** dropdown, and change time to **Last 6 hours**. By observing the table, it can be observed that for the uploaded logs, the alarm triggered 9 times, and sent a notification to selected destination.
    ![alarm-triggered-table](images/alarm-triggered-table.png)

    You can also observe, that the alarm was initially in **Ok** state, then it went to **Firing** state, after some time, it will go to **Reset** state, waiting to go to **Firing** state again.

You may now **proceed to the next lab**.

## Learn More

For further reading please refer to the resources.

[Create a Parser] (<https://docs.oracle.com/en-us/iaas/logging-analytics/doc/create-parser.html>)

[How to use a RegEx Parser Builder?] (<https://www.youtube.com/watch?v=EoBJkaq9Png>)

[Create a Source] (<https://docs.oracle.com/en-us/iaas/logging-analytics/doc/create-log-source.html>)

[Upload Logs on Demand] (<https://docs.oracle.com/en-us/iaas/logging-analytics/doc/upload-logs-demand.html>)

[Managing Alarms] (<https://docs.oracle.com/en-us/iaas/Content/Monitoring/Tasks/managingalarms.htm>)

## Acknowledgements

* **Author** - Chintan Kalsaria, OCI Logging Analytics
* **Contributors** -  Chintan Kalsaria, Kiran Palukuri, Ashish Gor, Kumar Varun, OCI Logging Analytics
* **Last Updated By/Date** - Chintan Kalsaria, Dec, 2023