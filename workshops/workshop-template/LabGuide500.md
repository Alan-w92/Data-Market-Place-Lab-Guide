# Getting Started with Data Marketplace

![](images/500/lab500-intro.png)  
Updated: June 4, 2019

## Introduction

This lab walks your company through the steps to set up and configure Data Marketplace for use. Data Marketplace is a pre-built centralized workspace where your admins can catalog data sets and give quick access to data scientists through an approval process. By the end of this lab, you will have access to the data sets through Data Marketplace.


**_To log issues_**, click here to go to the [github oracle](https://github.com/oracle/learning-library/issues/new) repository issue submission form.

## Objectives
-   Learn how to import APEX applications
-   Learn load data sets through SQL Developer
-   Learn how to set up Data Marketplace

## Required Artifacts
-   The following lab requires an Oracle Public Cloud account. You may use your own cloud account, a cloud account that you obtained through a trial, or a training account whose details were given to you by an Oracle instructor.

-   Oracle SQL Developer 18.3 or later (see <a href="http://www.oracle.com/technetwork/developer-tools/sql-developer/downloads/index.html" target="\_blank">Oracle Technology Network download site</a>)

-   [Data Marketplace Files 19.1.zip](./Files/Data_Marketplace_Files_19.1.zip)

-   [Data Marketplace Data Set.zip](./Files/Data_Marketplace_Data_Set.zip)

## Part 1. Importing Data Marketplace application

### **STEP 1: Download the required files and prepare data files**

-   Download these two files.

[Data Marketplace Files 19.1.zip](./Files/Data_Marketplace_Files_19.1.zip)

[Data Marketplace Data Set.zip](./Files/Data_Marketplace_Data_Set.zip)

-   Unzip Data Marketplace Files 19.1 and open Data Marketplace SQL File and Data Marketplace Administration SQL File in any text editor.

-   Search and replace the following IP address with your own IP address and save it.

    150.136.245.101 (Note: Use Ctrl + F or CMD + F to bring up the search option in your editor)
    
![](./images/500/lab500-1.png)

-   Open Database SQL 19.1.sql and replace **Your Database IP Address** at line 1 with your IP Address and save it.

![](./images/500/lab500-71.png)

### **STEP 2: Logging into APEX workspace**

-   Open windows PuTTY program or mac Terminal.

-   SSH into your database instance with the following syntax, use the file path of where your private SSH key resides and your IP address.

    ```ssh -i <File Path To Private SSH Key> opc@<Your Database IP Address>```
    
![](./images/500/lab500-2.png)

-   Change to Oracle user with the following command.

    ```sudo su – oracle```
   
![](./images/500/lab500-3.png)

-   Change to ords directory with the following command.

    ```cd ords```
    
![](./images/500/lab500-4.png) 

-   Start ORDS with the following command.

    ```java -Dconfig.dir=/home/oracle/ords -jar ords.war install simple –preserveParamFile```
    
![](./images/500/lab500-5.png)  

-   Go to APEX url (Replace the brackets and content with your own Database IP address).

    ```http://<Your Database IP Address>:8080/ords```
    
![](./images/500/lab500-6.png) 

-   Sign into the APEX workspace that you created in lab 400.

![](./images/500/lab500-7.png)

### **STEP 3: Importing APEX applications**

-   Click on **Import**.

![](./images/500/lab500-8.png)

-   Find your Data Marketplace SQL File and click **Next**.

![](./images/500/lab500-9.png)

-   Click **Next** to confirm your import.

![](./images/500/lab500-10.png)

-   Install the application with ID 100 by clicking **Reuse Application ID 100** and then click **Install Application**.

![](./images/500/lab500-11.png)

-   Click on **Import**.

![](./images/500/lab500-12.png)

-   Find your Data Marketplace Administration SQL File and click **Next**.

![](./images/500/lab500-13.png)

-   Click **Next** to confirm your import.

![](./images/500/lab500-14.png)

-   Install the application with ID 101 by clicking **Reuse Application ID 101** and then click **Install Application**.

![](./images/500/lab500-15.png)

### **STEP 4: Allow user access to imported applications**

-   Click on **Data Marketplace application** (ID 100)

![](./images/500/lab500-16.png)

-   Click on **Shared Components**.

![](./images/500/lab500-17.png)

-   Click on **Application Access Control**.

![](./images/500/lab500-18.png)

-   Click on **Add User Role Assignment**.

![](./images/500/lab500-19.png)

-   Add your APEX workspace user (The email you used to create the workspace), check all three roles and click on **Create Assignment**.

![](./images/500/lab500-20.png)

-   Click on **App Builder** to navigate back to the main page.

![](./images/500/lab500-21.png)

-   Click on **Data Marketplace Administration application** (ID 101)

![](./images/500/lab500-22.png)

-   Click on **Shared Components**.

![](./images/500/lab500-23.png)

-   Click on Application **Access Control**.

![](./images/500/lab500-24.png)

-   Click on **Add User Role Assignment**.

![](./images/500/lab500-25.png)

-   Add your APEX workspace user (The email you used to create the workspace), check all three roles and click on **Create Assignment**.

![](./images/500/lab500-26.png)

-   Click on **App Builder** to navigate back to the main page.

![](./images/500/lab500-65.png)

-   Click on **Data Marketplace Administration application** (ID 101)

![](./images/500/lab500-22.png)

-   Click on **1 - Data Market Place Administration**.

![](./images/500/lab500-66.png)

-   Click on **Processin tab**. Click on **Save Interactive Grid Data**. 

![](./images/500/lab500-67.png)

-   Click on the Code Editor.

![](./images/500/lab500-68.png)

-   Navigate down to line 34 and change the pluggable database servicename to your own servicename.

-   Navigate down to line 38 and change the IP address to your own IP address. Click on **OK**.

![](./images/500/lab500-69.png)

-   Click on **Save**.

![](./images/500/lab500-70.png)

## Part 2. Load data sets through SQL Developer

### **STEP 1: Download [SQL Developer](https://www.oracle.com/technetwork/developer-tools/sql-developer/downloads/index.html)**

-   Accept the license agreement and click **Download**.

![](./images/500/lab500-27.png)

### **STEP 2: Connecting to your database with SQL Developer**

-   Click on the **Green Plus Icon** to start a new connection.

![](./images/500/lab500-28.png)

-   Create database connection with the following. Click **Connect** when done.

```
Connection Name:		DataMarketPlace
Username:			sys
Password:			Use your own Database Password
Role:				SYSDBA
Hostname:			Your Database IP Address
Service Name:			Your database service name can be found by using SSH to log into your database and running the command lsnrctl status
```

![](./images/500/lab500-29.png)

### **STEP 3: Load data sets into database**

-   Open Database Schema Creation File, Data Marketplace Tables File, and Data Marketplace Data Set File. Unzip the Data Marketplace Data Set File for all the excel data files.

-   Copy the SQL statements from Database Schema Creation File and paste them into SQL Developer worksheet. Run the SQL statements to create a schema for each data set in your pluggable database (pdb1)

![](./images/500/lab500-30.png)

-   Expand the options for your database, scroll down to Other Users and expand the tab to find all the schemas.

![](./images/500/lab500-31.png)

![](./images/500/lab500-32.png)

-   Find the schema called **WORLD_STOCK_MARKET_AND_INDUSTRY_PROD** and expand the options.

![](./images/500/lab500-33.png)

-   Right click **Tables (Filtered)** and click **Import Data**.

![](./images/500/lab500-34.png)

-   Click on **Browse** and open the WORLD_STOCK_MARKET_AND_INDUSTRY_PROD excel file.

![](./images/500/lab500-35.png)

-   Click on **Next**.

![](./images/500/lab500-36.png)

-   From Data Marketplace Tables File find all the table names, use WORLD_STOCK_MARKET_AND_INDUSTRY_PROD_DATA for the Table Name. Click **Next**.

![](./images/500/lab500-37.png)

-   Click on **Next**.

![](./images/500/lab500-38.png)

-   Columns with an invalid name will appear with red bubbled exclamation mark. Change Name to something different that doesn’t violate rules such as keywords like date or symbols like **/**, **-**, or **( )**. In this example we will change DATE to DAY and WEIGHTED_STOCK_MKT_INDEX_(XGDP) to WEIGHTED_STOCK_MKT_INDEX_XGDP.

![](./images/500/lab500-39.png)

![](./images/500/lab500-40.png)

![](./images/500/lab500-41.png)

-   Click on **Next**.

![](./images/500/lab500-42.png)

-   Click on **Finish**.

![](./images/500/lab500-43.png)

-   Locate the next schema WORLD_MTCO2_EMISSION_AND_POPULATION and expand the options.

![](./images/500/lab500-44.png)

-   Import data and use WORLD_MTCO2_EMISSION_AND_POPULATION_DATA for the table name.

![](./images/500/lab500-45.png)

-   There are no invalid column names in this table. Click **Next** and proceed to click **Finish** to import the table.

![](./images/500/lab500-46.png)

-   Locate the next schema WORLD_HYBRID_CARS_FUEL and expand the options.

![](./images/500/lab500-47.png)

-   Import data and use WORLD_HYBRID_CARS_FUEL_DATA for the table name.

![](./images/500/lab500-48.png)

-   There is one invalid column name in this table. Delete the **( )** and replace the **/** with underscores ( _ ) for better readability. 

        ACCELRATE_RATE_KM_HOUR_SECOND
        
![](./images/500/lab500-49.png)

-   Click **Next** and proceed to click **Finish** to import the table. (Note: You will get a message for some rows that don't contain values. You can click **ok** for the missing data.)

![](./images/500/lab500-50.png)

(Note: There are a total of 16 data sets. You may continue uploading the rest of the tables or proceed with less data in Data Marketplace. You may follow the table names in the Data Marketplace Tables File for the remaining data sets.)

## Part 3. Setting up Data Marketplace application

### **STEP 1: Configurations for Data Marketplace**

-   Download Database SQL File.

-   Start SQL Developer and open your DataMarketPlace connection by double clicking the connection name.

![](./images/500/lab500-51.png)

-   Fill in **sys** for the username and your database password to log in.

![](./images/500/lab500-52.png)

-   Clear your SQL worksheet if there are any SQL statements in it.

![](./images/500/lab500-53.png)

-   Download Database SQL File and copy and paste the SQL statements into your worksheet. Run the Statements by clicking the **Run Script** button.

![](./images/500/lab500-54.png)

## Part 4. Starting Data Marketplace application

### **STEP 1: Start Oracle Rest Data Services**

-   Open windows PuTTY program or mac Terminal.

-   SSH into your database instance with the following syntax, use the file path of where your private SSH key resides and your database IP address.

	```ssh -i <File Path To Private SSH Key> opc@<Your Database IP Address>```
    
![](./images/500/lab500-55.png) 

-   Change to Oracle user with the following command.

	```sudo su – oracle```
	
![](./images/500/lab500-56.png)

-   Change to ords directory with the following command. 

	```cd ords```
    
![](./images/500/lab500-57.png) 

-   Start ORDS with the following command.

	```java -Dconfig.dir=/home/oracle/ords -jar ords.war install simple –preserveParamFile```
    
![](./images/500/lab500-58.png) 

### **STEP 2: Start Data Marketplace application**

-   Go to the APEX url (Replace the brackets and content with your own Database IP address)

   ``` http://<Your Database IP Address>:8080/ords```
    
![](./images/500/lab500-59.png)

-   Sign into the APEX workspace that you created in lab 400.

![](./images/500/lab500-60.png)

-   Click on the **Data Marketplace application** (ID 100)

![](./images/500/lab500-61.png)

-   Click on **Run Application**.

![](./images/500/lab500-62.png)

-   Use the email and password you used to create your workspace to log into Data Marketplace.

![](./images/500/lab500-63.png)

-   Installation complete. You can now start exploring Data Marketplace.

![](./images/500/lab500-64.png)



## Great Work - All Done with Lab500!
**Congrats! You are all done. You may now close this tab.**
