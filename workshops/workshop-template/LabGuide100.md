Getting Started with Database Systems
----------------------------------------------------------------------------

![](images/100/Picture100-lab.png)  
Updated: May 10, 2019

## **Introduction**

This lab walks you through the steps to get started with provisioning a Database system to run Application Express (APEX). In this lab, you will create a Virtual Cloud Network and related resources needed to provision a Database System on Oracle Cloud Infrastructure.

**_To log issues_**, click here to go to the [github oracle](https://github.com/oracle/learning-library/issues/new) repository issue submission form.

## Objectives
-   Learn how to create a Virtual Cloud Network and related resources
-   Learn how to provision a Database system
-   Learn how to access your Database system Secure Shell (SSH)


## Required Artifacts
-   The following lab requires an Oracle Public Cloud account. You may use your own cloud account, a cloud account that you obtained through a trial, or a training account whose details were given to you by an Oracle instructor.

# Provision Database system


## Part 1. Generating Secure Shell (SSH) keys

In this section you will create SSH keys to establish secure connections to your database system

### For Windows

### **STEP 1: Download PuTTY Key Generator**

-   Download [PuTTY Key Generator](https://www.putty.org/)

### **Generate SSH Keys using PuTTY Key Generator**

-   Find puttygen.exe in the PuTTY folder on your computer, for example, C:\Program Files (x86)\PuTTY. Double-click puttygen.exe to open it.

-   Accept the default key type, RSA.

-   Set the Number of bits in a generated key to 2048 bits, if it is not already set with that value.

-   Click Generate.

![](./images/100/lab100-1.png)

-   Move your mouse around the blank area to generate randomness to the key.

![](./images/100/lab100-2.png)

-   The generated key appears under Public key. Save the Public and Private keys as they will be used to provision your database instance.

![](./images/100/lab100-3.png)


### For Windows

### **STEP 1: Getting to the Command Line Interface**

-   Open your spotlight search by simultaneously clicking “CMD” and “spacebar”

-   Search for “Terminal” to open your command line interface (CLI)




