# Application Express (APEX) Installation

![](images/200/lab200-intro.png)  
Updated: June 12, 2019

## Introduction

This lab walks you through the steps to install Application Express (APEX) onto the database instance that you provisioned in the previous lab. APEX is a low-code development platform that enables you to build stunning, scalable, secure apps, with world-class features, that can be deployed anywhere. By the end of this lab, you will have APEX installed in your database.

**_To log issues_**, click here to go to the [github oracle](https://github.com/oracle/learning-library/issues/new) repository issue submission form.

## Objectives
-   Learn how to use Secure Shell (SSH) to log into your database instance
-   Learn how to configure database instance
-   Learn how to install Application Express

## Required Artifacts
-   The following lab requires an Oracle Public Cloud account. You may use your own cloud account, a cloud account that you obtained through a trial, or a training account whose details were given to you by an Oracle instructor.

-   [PuTTY Program](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) for windows systems.

-   Oracle Application Apex 19.1 or later (see <a href="https://www.oracle.com/technetwork/developer-tools/apex/downloads/index.html" target="\_blank">Oracle Technology Network download site</a>)

# Application Express Installation

## Part 1. Obtaining APEX files 

### **STEP 1: Download Oracle Application Apex 19.1 (see <a href="https://www.oracle.com/technetwork/developer-tools/apex/downloads/index.html" target="\_blank">Oracle Technology Network download site</a>)**

-   Accept the license agreement and download the APEX zip file.

![](./images/200/lab200-1.png)

-   Compress the APEX file into a zip file if it is not already in zip format.

![](./images/200/lab200-2.png)

### **STEP 2: Copy or move APEX into your database**

-   Sign into [Oracle Cloud](http://cloud.oracle.com)

-   Open the dashboard and click on **Bare Metal, VM, and Exadata**.

![](./images/200/lab200-23.png)

-   Locate your database IP address in your cloud tenancy be navigating to your database instance.

![](./images/200/lab200-4.png)

-   Use the following command to copy APEX files into your database instance after navigating to the location of where your APEX files are located. Replace the zip file name and IP address with your own.

	-   For Windows use Command Prompt and PuTTY Program
	
	    Download [PuTTY Program](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)
	    
	    Open PuTTY and navigate to Auth page by scrolling down the menu. Browse for your Private Key.
	    
	    ![](./images/200/putty1.png)
	    ![](./images/200/putty2.png)
	    
	    Navigate back to session page and fill in your IP Address and click Open.
	    
	    ![](./images/200/putty3.png)
	    
	    Click Yes when prompted to create your connection.
	    
	    Login in as **opc** with your database password.
	    
	    ![](./images/200/putty5.png)
	    
	    Use the command prompt to execute the following command. Remember to use your own IP Address SSH key file path.

	    scp -i /Users/alawang/.ssh/DataMarketPlaceKey apex_19.1_en.zip opc@150.136.245.101:~/
	    
	    ![](./images/200/putty6.png)
	
	-   For Macs use Terminal

	    scp -i /Users/alawang/.ssh/DataMarketPlaceKey apex_19.1_en.zip opc@150.136.245.101:~/
	
	    ![](./images/200/lab200-3.png)

## Part 2. Using Secure Shell (SSH) to log into your database instance

### **STEP 1: Logging into your database**

-   Locate your database IP address in your cloud tenancy be navigating to your database instance.

![](./images/200/lab200-4.png)


-   Use windows PuTTY Program or mac Terminal to SSH into your instance.


-   SSH into your database instance with the following syntax for macs, use the file path of where your private SSH key resides and the IP address you found earlier. Replace the content and the brackets with your own file path and Database IP Address.

	```ssh -i <File Path To Private SSH Key> opc@<Your Database IP Address>```
  
![](./images/200/lab200-5.png)

## Part 3. Setting up Oracle environment

### **STEP 1: Oracle database configuration**

-   Change to the oracle user with the following command.

	```sudo su – oracle```

![](./images/200/lab200-6.png)

-   Find your ORACLE_SID and ORACLE_HOME file path with the command below and take note of it. You will need need these later on.

	```cat /etc/oratab```
  
![](./images/200/lab200-7.png)

-   Add ORACLE_SID and ORACLE_HOME to your .bash_profile.

	```vi ~/.bash_profile```
  
![](./images/200/lab200-8.png)

-   Press **i** to enter insert mode. Add environment variables below to the end of the file. Replace SID and HOME file path with your own.

	```export ORACLE_SID=APEXDB```
	
	```export ORACLE_HOME=/u01/app/oracle/product/12.1.0.2/dbhome_1```
	
	```export PATH=$ORACLE_HOME/bin:$PATH```
	
-  Press ```esc``` to exit insert mode. Type ```:wq!``` and hit return to save your environment variables.
  
![](./images/200/lab200-9.png)

-   Run source command.

	```source ~/.bash_profile```
  
![](./images/200/lab200-10.png)

## Part 4. APEX Installation


### **STEP 1: Installing APEX onto the database**

-   Navigate back to the opc user with the command ```exit```.

![](./images/200/lab200-11.png)

-   Use the following command to copy APEX files from your opc user over to the oracle user. Replace the zip file name with your own.
	
	-   For Windows

	    sudo copy apex_19.1_en.zip ../oracle

	-   For Macs

	    sudo scp apex_19.1_en.zip ../oracle
  

![](./images/200/lab200-12.png)

### **STEP 2: Changing to the Oracle user**

-   Change user with the following command.

	```sudo su – oracle```
  
![](./images/200/lab200-13.png)

### **STEP 3: Unzip your APEX files**

-   Use the following command to unzip your APEX files (Replace file name with your own)

	```unzip apex_19.1_en.zip```
  
![](./images/200/lab200-14.png)

### **STEP 4: APEX Configuration**

-   Change to the apex directory with the following command.

	```cd apex```
  
![](./images/200/lab200-15.png)

-   Start SQL Plus and ensure you are connecting to your PDB and not to the “root” of the container database. Run the commands below to login.

	sqlplus / as sysdba
	
	alter session set container=pdb1;
	
	@apexins sysaux sysaux temp /i/
	
  
![](./images/200/lab200-16.png)

-   Wait until you see sql prompt.

-   Unlock the APEX_PUBLIC_USER account and set the password.

	```alter user apex_public_user identified by BEstrO0ng_#11 account unlock;```
  
![](./images/200/lab200-18.png)


-   Create the APEX Instance Administration user and set the password. (Note: Copy and pasting this may result in a quotation mark format change which will cause errors.)
	
	```
	begin
	
	apex_util.set_security_group_id( 10 );
	
	apex_util.create_user(p_user_name => ‘ADMIN’,p_email_address =>
	
	‘Enter your Email id’,p_web_password => ‘BEstrO0ng_#11’,p_developer_privs => ’ADMIN’ );
	
	apex_util.set_security_group_id( null );
	
	commit;
	
	end;
	
	/
	```

![](./images/200/lab200-19.png)

-   Run APEX REST configuration, and set the passwords of APEX_REST_PUBLIC_USER and APEX_LISTENER.

	```@apex_rest_config_core.sql ./ BEstrO0ng_#11 BEstrO0ng_#11```
  
![](./images/200/lab200-20.png)

-   Create a network ACE for APEX. This is used when consuming Web services or sending outbound mail. (Note: Copy and pasting will likely result in quotes changing to a different format which causes errors. Manually type this in your terminal if you run into errors.)

	```
	declare
	
	l_acl_path varchar2(4000);
	
	l_apex_schema varchar2(100);
	
	begin
	
	for c1 in (select schema from sys.dba_registry where comp_id = ‘APEX’) loop
	
	l_apex_schema := c1.schema;
	
	end loop;
	
 	sys.dbms_network_acl_admin.append_host_ace(host => ‘*‘,ace => xs$ace_type(privilege_list => xs$name_list(‘connect’),principal_name => l_apex_schema,principal_type => xs_acl.ptype_db));
	 
	commit;
	
	end;
	
	/
	```
	
![](./images/200/lab200-21.png)

-   Exit SQL*Plus with ```exit``` command.

![](./images/200/lab200-22.png)


## Great Work - All Done with Lab200!
**You are ready to move on to the next lab. You may now close this tab.**
