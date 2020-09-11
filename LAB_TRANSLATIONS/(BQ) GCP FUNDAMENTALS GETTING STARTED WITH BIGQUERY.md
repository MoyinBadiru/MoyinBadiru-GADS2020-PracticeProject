

> # LAB: Google Cloud Fundamentals: Getting Started With Big Query
>

 ## OBJECTIVES:
 In this lab, you learn how to perform the following tasks:

-   Load data from Cloud Storage into BigQuery.

-   Perform a query on the data in BigQuery.  
 ## STEPS:

 ## TASK 1: Load data from Cloud Storage into BigQuery

1.  In the Cloud Console, on the  Navigation menu click  BigQuery.
2.  If prompted, click  Done.
3.  Create a new dataset within your project by selecting your project in the Resources section, then clicking on CREATE DATASET on the right.

4. In the Create Dataset dialog, for Dataset ID, type logdata.

5. For Data location, select the continent closest to the region your project was created in. click Create dataset.

    **COMMAND LINE:**
 
       bq --location=US mk --dataset logdata

6. Create a new table in the logdata to store the data from the CSV file.

7. Click on Create Table. On the Create Table page, in the Source section:

    - For Create table from, choose Google Cloud Storage, and in the field, type gs://cloud-training/gcpfci/access_log.csv

    - Verify File format is set to CSV

8. In the Destination section:

    -  For Dataset name, leave logdata selected.

    -  For Table name, type accesslog.

    -  For Table type, Native table should be selected

9. Under Schema section, for Auto detect check the Schema and input Parameters.

10. Accept the remaining default values and click Create Table

    **COMMAND LINE:**

        bq --location=US load --source_format=CSV --autodetect logdata.accesslog  gs://cloud-training/gcpfci/access_log.csv 

11. When the load job is complete, click logdata > accesslog.

12. On the table details page, click Details to view the table properties, and then click Preview to view the table data

    **COMMAND LINE:**

        bq show logdata.accesslog 

## TASK 2: Perform a query on the data using the BigQuery web UI

1. In the Query editor window, type the following query:

        select int64_field_6 as hour, count(*) as hitcount from logdata.accesslog group by hour order by hour

    **COMMAND LINE:**

       bq query --use_legacy_sql=false "select int64_field_6 as hour, count(*) as hitcount from logdata.accesslog group by hour order by hour"


## Task 3: Perform a query on the data using the bq command 

1. At the Cloud Shell prompt, enter this command:

        bq query "select string_field_10 as request, count(*) as requestcount from logdata.accesslog group by request order by requestcount desc"

    **COMMAND LINE:**
        
       bq query --use_legacy_sql=false "select string_field_10 as request, count(*) as requestcount from logdata.accesslog group by request order by requestcount desc"
