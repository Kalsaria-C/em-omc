# Create detection rules

## Introduction

In this lab will walk you through the steps to create Detection Rules for **Oracle Database Abnormal Termination** incident

Estimated Time: 5 minutes

### Objectives

In this lab, you will:

* Create a Detection Rule with an Oracle predefined OOTB label.

### Prerequisites

This lab assumes you have:

* An Oracle Cloud Infrastructure account
* A running Oracle Database Instance

## Task 1: Navigate to Detection Rules Tab

Detection Rules can be found and defined in the Detection Rules Tab:

1. Step 1

  Open the ![Left Menu Icon](images/menu-icon.png) **Navigation Menu**
2. Step 2

  Open **"Observability & Management"** > In **"Logging Analytics"**, Click **"Administration"**.

  ![Figure 1: Open the Logging Analytics Administration board ](images/open-the-logging-analytics-administration-board.png)
3. Step 3

  In the Menu at bottom left, Click on "Detection Rules".

  ![Figure 2: Open "Detection Rules" Page](images/open-detection-rules-page.png)

## Task 2: Create Detection Rules

1. Step 1

  Click on **"Create rule"** button.

  ![Figure 3: Click on create rule button"](images/click-on-create-rule-button.png)
2. Step 2

  Select **"Ingest time detection rule"**.

  ![Figure 4: Select "Ingest Time Detection Rule"](images/select-ingest-time-detection-rule.png)
3. Step 3

  Insert a name in the **"Rule name"** field.

  ![Figure 5: Fill "Rule name" field](images/fill-rule-name-field.png)
4. Step 4

  Under **"Select a label"** section > in **"Label"** input, Select **"Abnormal Termination"** label.

  ![Figure 6: Fill "Label" field with "Abnormal Termination"](images/fill-label-field.png)
5. Step 5

  Fill "Metric Namespace" & "Metric Name" fields.

  ![Figure 7: Fill "Metric Namespace" and "Metric Name" fields](images/fill-metric-namespace-and-metric-name-fields.png)
6. Step 6

  Save & Create the Detection Rule.

  ![Figure 8: Save and create the Detection Rule](images/save-and-create-the-detection-rule.png)

The Detection Rules creation pane will close and an info confirmation message should appear on screen if the rule was created, Otherwise you will need to correct the error(s) before the rule will be created.

![Figure 9: Detection Rule creation Confirmation Message](images/detection-rule-creation-confirmation-message.png)

## Task 3: Create and verify alarms

Alarms let you generate an alert and notify the desired recipients when a predefined threshold is reached. The alarms can be found, created and edited in a separate service (OCI Monitoring service).

1. Step 1
Create the alarm

2. Step 2
Verify the alarm

## Learn More

* [Detect Predefined Events at Ingest Time](https://docs.oracle.com/en-us/iaas/logging-analytics/doc/detect-predefined-events-ingest-time.html#GUID-D28CF994-288F-48C3-8CE5-28CE29C3482C)

## Acknowledgements

* **Author:** Ayoub BELMEHDI, OCI Logging Analytics

* **Contributors:** Ashish GOR, Kiran PALUKURI, Vikram REDDY, Kumar Varun, OCI Logging Analytics

* **Last Updated By/Date:** Ayoub BELMEHDI, October 2023
