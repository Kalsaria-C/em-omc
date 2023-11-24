# Create Sensitive Configuration and Privilege Escalation Scheduled Detection rules alarms

## Introduction

This lab will walk you through the steps to Create & verify Scheduled Detection rules alarms to detect **Sensitive Configuration and Privilege Escalation**.
This lab explains how to create and manage single and multi-conditional labels for ingest time detection rules.

Estimated Time: 20 minutes

### Objectives

In this lab, you will:

* Create single and multi-conditional labels.
* Create an alarm for the labels

### Prerequisites

This lab assumes you have:

* An Oracle Cloud Infrastructure account

## Task 1: Check the Policies

To create and manage Detection Rules and use them in the Monitoring Service, the correct policies need to be set:

  ```Policies
    allow group &lt;group name&gt; to manage loganalytics-ingesttime-rule in tenancy
    allow service loganalytics to use metrics in tenancy
  ```

Replace the group name with whatever group fills your needs, be sure that your user is part of that group.

To set the policies go to **"Identity & Security"** > **"Identity"** > **"Policies"**

![Figure 1: Navigate to policies Tab](images/go-to-policies-tab.png)

Here you can create a new policy or edit an existing one to contain the needed policies.

## Task 2: Ingest Database Audit Logs

Conditional Labels can be created via multiple ways. The most straight forward is by using the "Log Explorer". Let's ingest a log sample with the problem:

1. Step 1

  Generate the log file to upload by copying these logs into a file:

  ```Logs
    <copy>
      Thu Nov  16 14:36:23 2023 +01:00
      LENGTH : '157'
      ACTION :[67] 'ALTER PROFILE'
      DATABASE USER:[3] 'sys'
      PRIVILEGE :[6] 'SYSDBA'
      CLIENT USER:[8] 'user1'
      CLIENT TERMINAL:[0] ''
      STATUS:[1] '0'
      DBID:[9] '592398530'
    </copy>
  ```

  Edit the time from "Thu Nov  16 14:36:23 2023 +01:00" into a valid time within 3-5 upcoming minutes.
2. Step 2

  Go to **"Administration"** > **"Sources"** from the bottom left menu, look for the **"Database Audit Logs"** and select it.

  **P.S:** You can duplicate the log source, but this is not recommended because the duplicated source will not be able to get the latest Oracle Sources updates.
3. Step 3

  Click on "Upload Files", and fill the form:
  ![Figure 2: Open the upload file page from source](images/open-the-files-upload-page.png)
  ![Figure 3: Fill the File Upload info](images/fill-files-upload-info.png)

  Add the file(s) with your logs, and click on "Next" when over:
  ![Figure 4: Select Files to upload](images/select-files-to-upload.png)
  ![Figure 5: Check files to submit & click on next](images/check-files-to-submit-and-click-next.png)
4. Step 4

  In the second step, Click on "Next":
  ![Figure 6: Click On Next in the second step](images/select-next-in-file-upload-2nd-step.png)
5. Step 5

  Check your configuration, then click on "Upload", then click on "close":
  ![Figure 7: Check and Upload Files](images/check-upload-and-submit.png)

  You shall see your files state in the files page:
  ![Figure 8: Files upload state In Progress](images/check-files-upload-status-in-progress.png)
  ![Figure 9: Files upload state Complete](images/check-files-upload-status-completed.png)

Your logs should now appear in the Logs Explorer.

## Task 3: Create the conditional Label

To create a conditional Label out of the logs ingested:

1. Step 1

  Click on "View in Log Explorer":

  ![Figure 10: Open Log Explorer from file uploads](images/open-log-explorer-from-uploads.png)
2. Step 2

  Select your Log Set (we will use "*" to search over all the logs):

  ![Figure 11: Set log set to wildcard](images/set-log-set-to-wildcard.mov)
3. Step 3

  Go to one of the logs that should raise the label, click on the 3 dots at its far right and click on "Add conditional label":

  ![Figure 12: Open Conditional Label Creation Panel](images/open-conditional-label-creation-panel.png)
4. Step 4

  Fill the label's conditions fields:
  ![Figure 13: Fill the Label's fields](images/set-conditions-for-conditional-label.png)

  **Explanation:**
    1. Change "Original Log Content" to "Action"
    2. Change "equal" to "In"
    3. The condition value field should be populated with 'ALTER PROFILE', add these value one by one (These are the privileges names of database actions), hit enter after you enter each one in the field:
      - ALTER USER
      - CREATE PROFILE
      - CREATE USER
      - DROP PROFILE
      - DROP USER
5. Step 5

  Create a label in the Actions select labels field (You can use an existing label):
  ![Figure 14: Open the label creation panel](images/open-label-creation-panel.png)
  ![Figure 15: Fill the label information & click on "create"](images/create-label.png)
  ![Figure 16: Check the Conditional Label & Create](images/check-conditional-label-and-create.png)
  **Explanation:**
    1. Open the label creation panel
    2. Fill the label fields
    3. Save the label
    4. Save the conditional Label

Your new label should now be ready to be used in other Monitoring services.

## Task 4: Create Detection Rule

To create a detection rule from the Label:

1. Step 1

  Go to **"Administration"** > **"Label"** > Select the Label you just created for the Conditional Label.
2. Step 2

  Click on "Ingest time detection rule" to move to the Detection Rules tab, click on "Create rule":
  ![Figure 17: Click on "Ingest time detection rule"](images/click-on-ingest-tab.png)
3. Step 3

  Fill the fields to create the Detection Rule:
  ![Figure 18: Fill the Detection Rule creation fields](images/create-detection-rule.png)

  **Explanation:**
    1. Fill the name, log source, Metric Namespace & Name.
    2. Click on "Create Detection Rule".
4. Step 4

  Trigger the Detection Rule by re-uploading your logs (Follow *2. Task 2*). When done you should expect a result similar to this figure:
  ![Figure 19: Detection Rule triggered](images/detection-rule-triggered.png)

The Detection Rule should be up and ready to be used in other Monitoring services.

## Task 5: Create & Verify Alarm

To create an alarm from the Detection Rule:

1. Step 1

  Go to **"Administration"** > **"Detection"** > Select the Detection Rule you just created for the Label (you can use the breadcrumb).
2. Step 2

  Click on Create Alarm to open the alarm creation page:

  ![Figure 20: Open the alarm creation panel](images/open-alarm-creation-panel.png)
3. Step 3

  Fill the Alarm Form:
  ![Figure 21: Fill the Alarm Form general info & metrics](images/alarm-info-fill-general-field-and-metrics.png)
  ![Figure 22: Fill the Alarm Form trigger rule & metric dimensions](images/alarm-info-fill-trigger-rule-and-metric-dimension.png)
  ![Figure 23: Fill the Alarm Form topic & save](images/alarm-info-fill-topic-and-save.png)

  **Explanation:**
    1. Fill the name, body and severity of the alarm.
    2. Fill the metrics fields for your alarm (Choose the ones you created in the Detection Rule).
    3. Choose a topic or create and select a new one if you still have not done so.
    4. Hit the "Save alarm" button.
4. Step 4

  To verify the alarm, upload logs that triggers the "Database User Permission Change" Label, it should appear in the Log Explorer and you should receive a notification.

## Learn More

* [Detect Predefined Events at Ingest Time](https://docs.oracle.com/en-us/iaas/logging-analytics/doc/detect-predefined-events-ingest-time.html#GUID-D28CF994-288F-48C3-8CE5-28CE29C3482C)
* [Create Alarm from a Detection Rule](https://docs.oracle.com/en-us/iaas/logging-analytics/doc/create-alerts-detected-events.html)

## Acknowledgements

* **Author:** Ayoub BELMEHDI, OCI Logging Analytics

* **Contributors:** Ashish GOR, Kiran PALUKURI, Vikram REDDY, Kumar Varun, OCI Logging Analytics

* **Last Updated By/Date:** Ayoub BELMEHDI, October 2023
