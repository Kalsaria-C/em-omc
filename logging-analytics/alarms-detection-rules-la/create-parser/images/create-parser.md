# Create a Parser

## Introduction

In this lab, you will understand the concept of Parsers in Logging Analytics.

Estimated Time: 10 minutes.

### Objectives

In this lab you will:

* Understand the meaning of Parser in Logging Analytics.
* Create a single-line Parser.

### Prerequisites

This lab assumes you have:

* An Oracle Cloud Infrastructure account.

## Task 1:  Understand Logging Analytics Parser

A Parser takes raw configuration data and parses it into a nested attribute structure. Each parser consists of a base parser and parser parameters. Some parsers also contain post-parsing rules. A base parser essentially is a category of parser capable of parsing data of a particular format. Parser parameters provide a way to tailor the base format to accommodate variations in data formatting.

Oracle Logging Analytics offers hundreds of Oracle-defined sources and parsers that you can directly use without creating custom ones. To collect logs of a format which doesn't have an Oracle-defined source or parser, you can create custom source or parser.

There are four varieties of base parser:

1. Regex
2. JSON
3. XML
4. Delimited

Regex parser can be of 2 types:

1. Single-line
2. Multi-line

## Task 2: Create a single-line Parser

1. From **Navigation Menu** ![navigation-menu](images/navigation-menu.png) > **Observability & Management** > **Logging Analytics** > **Administration**.
![administration-navigation](images/administration-navigation.png)

2. From **Administration Overview Page**, Click on **Create Parser** button. A dropdown will appear, showing four types of parsers available. As per our type of sample log you can select any. In this lab you will create a **Regex Type** parser. Click on **Regex Type**.
![parser-dialog-box](images/parser-dialog-box.png)

3. The **Create Parsers Page** page is displayed. In case of Regex Type, the Create Parser page opens in the **Guided** mode, by default. Continue in this mode if you want Logging Analytics to generate the regular expression to parse the logs after you select the fields. If you want to write regular expression for parsing, then switch to **Advanced** mode. You will go for **Guided** mode, as it is very easy method to create Parser, you don't need knowledge of regular expression.

4. This is the first step of parser creation.

    * In the **Name** field, enter the parser name. For example, enter **livelab\_mushop\_api\_logs**.
    * (Optional) Provide a suitable **description** to the parser for easy identification.
    * In the **Example Log Content field**, paste the contents from a log file that you want to parse, such as the following:
        ```
        <copy>::ffff:10.244.1.225 - livelab_user [06/Nov/2023:03:22:17 +0000] "POST /api/orders HTTP/1.1" 401 70 "-" "python-requests/2.25.1"
        ::ffff:10.244.1.42 - livelab_user [06/Nov/2023:21:00:35 +0000] "POST /api/orders HTTP/1.1" 503 86 "-" "python-requests/2.25.1"
        ::ffff:10.244.1.42 - livelab_user [06/Nov/2023:08:25:16 +0000] "POST /api/orders HTTP/1.1" 500 120 "-" "python-requests/2.25.1"
        ::ffff:10.244.0.104 - livelab_user [06/Nov/2023:02:51:18 +0000] "GET /api/orders HTTP/1.1" 200 719 "-" "python-requests/2.25.1"</copy>
        ```
    * This is a single-line log entry, as each record is of single line, as shown in the figure below.
        ![create-parser-page-1](images/create-parser-page-1.png)

    * Click on **Next** to go to second step of parser creation.

5. Select one of the log records, you want to extract the field from.
    ![create-parser-page-2](images/create-parser-page-2.png)
    Click on **Next** to go to third step of parser creation.

6. Select the exact content for the value of each field. For example select the **::ffff:10.244.0.14"** content from the shown log record, a dialog of **Extract field** will appear. Here you can see the text you want to extract as a field, there is option if you don't want to extract it as field, you can select the **as literal text** option. From the Field dropdown, select the existing **Field Name**, here it is **Host IP Address (Client)**. You can also create a custom field, if it is not present in the dropdown. The **Regular expression** for the selected text will be auto generated. Mark the **Optional field** button if you want to make the field as optional. Click on **Extract field** option to map the selected text to field.
    ![create-parser-page-3.1](images/create-parser-page-3.1.png)

7. Selected text has been mapped to the field, you can see the **Parser Test**, where **Host IP Address (Client)** has been extracted out of all the log records which were pasted in Step 4. **Parser expression** will also be auto generated. **Match Status** will show if we are successful in extracting the field from all the log records. Click on **Next** to select another content to log record to be extracted out.
    ![create-parser-page-3.2](images/create-parser-page-3.2.png)

8. Repeat the Step 7, by selecting other content of log i.e. **livelabuser01**. After clicking on **Next**, you will see other column of **User Name** field has been added to the table showing extracted user names from the log records. You will also see the **Parse expression** has been modified now.
    ![create-parser-page-3.3](images/create-parser-page-3.3.png)

9. Similarly, repeat the Step 7, until you extracted all the field from selected log record, you will see all the extracted field in the table, with its extracted value from the log records. Verify by observing all the extracted fields, if they seems fine. Click on **Next**.
    ![create-parser-page-3.4](images/create-parser-page-3.4.png)

10. This is the last step of parser creation. Verify the **Parser expression**, field name, parser regular expression, data type, description of each field and other fields. If you want to change something, you can go to **Previous** step, or else click on **Create Parser** to create parser.
    ![create-parser-page-4](images/create-parser-page-4.png)