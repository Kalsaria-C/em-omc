# Problem Labels for Custom Apps-Logs

## Introduction

In this lab, you'll learn how to use a SQL query to pull data from DB Table and ingest each row as a log-record
"SELECT name,total_mb*1024*1024 as total,free_mb*1024*1024 as free FROM v$asm_diskgroup_stat where exists (select 1 from v$datafile where name like '+%')".

Estimated Lab Time: 10 minutes


### Objectives

In this lab, you will:
* Understand how DB Table Log Collection works (Study)
* Learn how to create a DB SQL Log Source for an existing DB Entity
* Create alarm if available free space is 30% or less

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

2. Specify the **Name** and **Description (optional)**. Select **Database** as **Source Type**. Set **MySQL Database Instance** as **Entity Types**.
   ![](./images/sources-create-01.png "UIdescription")

3. Click on **Database Queries** and add the following query: **SELECT name,total_mb*1024*1024 as total,free_mb*1024*1024 as free FROM v$asm_diskgroup_stat where exists (select 1 from v$datafile where name like '+%')**.
   ![](./images/sources-create-02.png "UIdescription")

## **Task 3:**  Configure Column Mapping

1. Click on **Configure**.
   ![](./images/sources-configure-mapping-01.png "UIdescription")

2. For the **name** column, click on **Create New Field** button.
   ![](./images/sources-configure-mapping-02.png "UIdescription")

3. Specify a **Name**, select **String** for **Data Type** and specify a **Description (optional)**. Click on **Create**.
   ![](./images/sources-configure-mapping-03.png "UIdescription")

4. Do the same as **Step 3** for **total** and **free** columns.
   ![](./images/sources-configure-mapping-04.png "UIdescription")

5. Click on **Done**.
   ![](./images/sources-configure-mapping-05.png "UIdescription")

## **Task 4:**  Save User Defined Source

1. Click on **Create Source**.
   ![](./images/sources-save-01.png "UIdescription")

   The source is saved successfully.
   ![](./images/sources-save-02.png "UIdescription")


## Acknowledgements
* **Author** - Oswaldo Osuna, Logging Analytics Development Team
* **Contributors** -  Kumar Varun, Logging Analytics Product Management - Kiran Palukuri, Logging Analytics Product Management - Vikram Reddy, Logging Analytics Development Team 
* **Last Updated By/Date** - Oct 18 2023
