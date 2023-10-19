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

## **Task 2:**  Create User Defined Source

1. Click on **Create Source**.
   ![](./images/source-create-button.png "UIdescription")

2. Specify the **Name** and **Description (optional)**. Select **File** as **Source Type**. Set **OCI Compute Instance** and **Apache HTTP Server** as **Entity Types**.
   ![](./images/source-create-01.png "UIdescription")

3. Mark the **Specific parser(s)** option. Then, select **Apache HTTP Access Log Format**.
   ![](./images/source-create-02.png "UIdescription")

## **Task 3:**  Add Field Enrichment

Logging Analytics provides automatic threat intelligence enrichment for your logs that can help identify public IP addresses which could have some level of threat associated with them. Learning about the possible threats early can help separate and mitigate them.

To enable the threat intelligence enrichment feature, Geolocation Field is needed.

1. Click on **Field Enrichment** and on **Add field enrichment**.
   ![](./images/field-enrichment-create-01.png "UIdescription")

2. Select **Geolocation** in **Function**. Then, Select **Host IP Address (Client)** in **IP Address Field** and mark **Threat Intelligence enrichment**. Finally, click on **Add field enrichment**.
   ![](./images/field-enrichment-create-02.png "UIdescription")

  The field enrichment is added successfully.
   ![](./images/field-enrichment-create-03.png "UIdescription")

## **Task 4:**  Create Multi-conditional label

1. Click on **Labels**, then on **Add conditional label**.
   ![](./images/conditional-label-create-01.png "UIdescription")

2. Select **Original Log Content** as **Input Field** and **Contains** as **Operator**. Add **threat** and **error** in **Condition Value**.
   ![](./images/conditional-label-create-02.png "UIdescription")

3. Click on the **Add a condition** button to make the label multi-conditional.
   ![](./images/conditional-label-create-03.png "UIdescription")

4. Select **Match all of the following conditions (AND)** in the drop-down above. Add the new condition with **Log Group** as **Input Field**, **Equal** as **Operator** and **live-labs** as the **Condition Value**.
   ![](./images/conditional-label-create-04.png "UIdescription")

5. Click on **Show Condition Summary** to check the multi-condition is correct.
   ![](./images/conditional-label-create-05.png "UIdescription")
   ![](./images/conditional-label-create-06.png "UIdescription")

6. Click on **Create Label**.
   ![](./images/conditional-label-create-07.png "UIdescription")

7. Specify a **Label** and **Description (optional)**. Mark the **Use this label to indicate a problem** checkbox inside **Denotes Problem**. Then, select **High** for **Problem Priority**. Click on **Create**.
   ![](./images/conditional-label-create-08.png "UIdescription")

  The label is created successfully.
   ![](./images/conditional-label-create-09.png "UIdescription")

8. Click on **Add**.
   ![](./images/conditional-label-create-10.png "UIdescription")

  The multi-conditional label is added successfully.
   ![](./images/conditional-label-create-11.png "UIdescription")

## **Task 5:**  Save User Defined Source
1. Click on **Create Source**.
   ![](./images/conditional-label-create-12.png "UIdescription")

  The source is created successfully.
   ![](./images/conditional-label-create-13.png "UIdescription")

## **Task 6:**  Navigate to Detection Rules

1. Click on the option **Detection Rules** inside **Resources** sidebar menu at the left.
   ![](./images/detection-rules-access.png "UIdescription")

  Now you are in **Detection Rules**.
   ![](./images/detection-rules.png "UIdescription")

## **Task 7:**  Create Ingest time detection rule

1. Click on **Create** inside **Detection Rules** page.
   ![](./images/detection-rules-create.png "UIdescription")

2. Click on **Ingest time detection rule**.
   ![](./images/ingest-time-option.png "UIdescription")

3. Specify the **Rule name**. Select the **Label** we created and **Monitoring** as **Target Service**.
   ![](./images/ingest-time-create-01.png "UIdescription")

4. Specify a **Metric Compartment**, **Metric Namespace** and **Metric Name**.
   ![](./images/ingest-time-create-02.png "UIdescription")

5. Click on **Create detection rule**.
   ![](./images/ingest-time-create-03.png "UIdescription")

  The ingest time detection rule is saved successfully.
   ![](./images/ingest-time-create-04.png "UIdescription")


## Acknowledgements
* **Author** - Oswaldo Osuna, Logging Analytics Development Team
* **Contributors** -  Kumar Varun, Logging Analytics Product Management - Kiran Palukuri, Logging Analytics Product Management - Vikram Reddy, Logging Analytics Development Team 
* **Last Updated By/Date** - Oct 12 2023
