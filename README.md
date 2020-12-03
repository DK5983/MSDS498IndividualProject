# MSDS498IndividualProject - Cloud Map Reduce with AWS’ Elastic Map Reduce (EMR)

## Introduction

In the sixteenth chapter of the textbook *Python for Programmers*, the authors walk you through a number of exercises pertaining to Big Data utilizing Hadoop, Spark, NoSQL and IoT (**https://learning.oreilly.com/library/view/python-for-programmers/9780135231364/ch16.xhtml**).  In section 16.5 the exercise was to configure and run a MapReduce Cluster in Azure that could identify the length of each word in a text and count how many words had each length.  For this project, I wanted to get the same end result, but use a different cloud-based platform.  I chose **Amazon Web Services (AWS)** for this project utilizing their **Elastic Map Reduce (EMR)** program.  This README will walk you through the entire process including introducing the architecture of the project, uploading the documents into *GitHub* and *AWS*, configuirng the EMR cluster, adding the Mapper/Reducer step to run the cluster and obtaining the readable output.  <br /><br />
*This repository contains the source code and information pertaining to the project which was initially downloaded from the **Python for Programmers** text*

## Files
This project requires ***three*** files:
* Romeo and Juliet text file `RomeoAndJuliet.txt`
* Mapper python file `length_mapper.py`
* Reducer python file `length_reducer.py`
<br />
The Romeo and Juliet text can be downloaded from this website: https://www.gutenberg.org/ebooks/1513 (it is also in this repository)<br /><br />

The two python files were originally downloaded using the examples in the ***Python for Programmers*** text (they are both in this repository)

## Uploading Files to GitHub
The `RomeoAndJuliet.txt` was uploaded directly into the repository. <br />
This was accomplished by: 
* Clicking on the `Add File` tab
* Selecting `Upload Files`
* Choosing the file from your local computer
* Clicking on the `Commit Changes` button at the bottom of the page

The two python files were placed into the ***Mapper-ReducerCode*** folder. <br />
The folder was developed by:
* Clicking on the `Add File` tab
* Selecting `Create New File`
* In the top section there is a place to `Name Your File`
  * Type a new folder name (for this project it was `Mapper-ReducerCoder`
  * Then type `/`
  * Then enter the name of the python code (`length_mapper.py`) and enter python code (***copied from code obtained in text***)

You can then add the `length_reducer.py` file into the same folder by:
* Going into the `Mapper-ReducerCode` folder
* Clicking on the `Add File` tab
* Selecting `Upload Files`
* Choosing the reducer file from your local computer
* Clicking on the `Commit Changes` button at the bottom of the page

## Uploading Files into AWS S3
### *Creating A Bucket*
For this project you will be creating ***three*** S3 buckets.  The first two of which will hold the ***Romeo and Juliet text*** and the ***Mapper and Reducer Python files***. <br />

To create an AWS S3 bucket complete the following:
* From your AWS Management Console select `S3` from the services. 
* In **S3** select the `Create Bucket` tab
  * **Name:** Give your bucket a unique name with lowercase letters and no spaces (you can use numbers)
  * **Region:** Select region that is closest to you
  * **All other fields:** Keep default
  * Select the `Create Bucket` tab at the bottom of the page.

### Uploading RomeoAndJuliet.txt into S3 Bucket
The first bucket you create should be named in a way that it identifies you will have .txt files in it. ***mine was named `textfilesjp`*** <br /><br />
After the bucket is created complete the following:
* Select the bucket you are using for the .txt file
* In the bucket click on the `Upload` tab
* Click on the `Add Files` tab
* Select the `RomeoAndJuliet.txt` file from your computer
* Click the `Upload` tab at the bottom of the page

### Uploading Mapper and Reducer Python Files into S3 Bucket
The second bucket you create should be named in a way that it identifies you will have the mapper and reducer python files in it. ***mine was named `mapperreducercode`*** <br /><br />
After the bucket is created complete the following:
* Select the bucket you are using for the python files
* In the bucket click on the `Upload` tab
* Click on the `Add Files` tab
* Select both the `length_mapper.py` and `length_reducer.py` files from your computer
* Click the `Upload` tab at the bottom of the page

### Setting Up the Output Bucket
The final bucket you create should be named in a way that it identifies you will have the output files in it. ***mine was named `outputformapreduce`*** <br /><br />
Unlike the previous two buckets, this bucket will not intitally have any files in it.

## Configuring the Cluster
### Part 1: Create Key Pair
In order to authenticate to Amazon EMR cluster you will need specify the "Amazon EC2 key pair that will be used for SSH connections to all cluster instances" (***https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan-access-ssh.html***).  This is a very easy process. <br /><br />
To create a key pair:
* From your AWS Management Console select `EC2` from the services. 
* In **EC2** select the item that says `Key pairs`
* Click on the `Creat key pair` button
  * **Name:** Give your key pair a name that is easy for you to identify
  * **File format:** I selected pem to use with OpenSSH, but this is not mandatory for the project
  * **All other fields:** Keep default
  * Click the `Create key pair` button at the bottom of the page.
  
### Part 2: Create Cluster
Now that your key value pair and buckets are all set up it is now time to create the cluster! <br /><br />
To create the cluster:
* From your AWS Management Console select `EMR` from the services. 
* In **EMR** click the `Create cluster` button
  * In the **General Configuration** section
    * **Cluster Name:** Give your cluster a name that is easy for you to identify
    * **Logging:** Keep the logging box checked and the default S3 bucket as-is
    * **Launch Mode:** Keep default (you could add a step directly to the cluster by selecting `Step execution` but for this project, we will be doing the step after the cluster has been created 
  * In the **Software Configuration** section
    * **Release:** Keep the default release version
    * **Applications:** Keep default: Core Hadoop
  * In the **Hardware Configuration** section
    * **Instance type:** Keep default (this is a small project and does not require anything more than the default)
    * **Number of instances:** Keep default as 3 (1 master and 2 core nodes).  This project does not require anything more than that.
    * **Cluster scaling:** Keep unchecked
   * In the **Security and Access** section
     * **EC2 key pair:** Select the key pair you created from the drop-down menu
     * **Permissions:** Keep as default
 * Click the `Create cluster` button
 
 ### Part 3: Security
 The cluster will take a few minutes to get up and running.  After it is ready to use, you have the ability to adjust security settings.  This is done by completing the following steps:
 * Click on your new cluster.  This will bring you to a face page that provides information about that specific cluster.
 * At the bottom portion of that page there is a section called `Security and access`
 * Click on the link for the ***Security groups for Master***
 * Select the Master Security Group ID.  This will bring you to a page where you can see the Inbound rules, Outbound rules and Tags.
 * Click on the `Edit inbound rules` button in the right corner.
   * Scan the inbound rules to see ***if*** there is any rule type **SSH** with port range of **22**
     * If there is **delete** that rule.
   * Click the `Add Rule` button at bottom of page
     * **Type:** select **SSH**
     * **Port Range:** select **My IP**
     * All other fields will be automatically filled in
   * Save the new rule and complete the same steps for the Slave Group ID
   
   ## Adding a Step
    Now that the cluster is up and running, the MapReduce step needs to be ran through the cluster.  To provde the cluster with the necessary .txt and .py files the following should be done:
   * Within your cluster, select the `Step` tab
   * Click on the `Add step` button
   * An window will pop up asking for specific information:
     * **Step type:** Select `Streaming program` from the dropdown menu
     * **Name:** Give this step a name that indicates what the step is doing
     * **Mapper:** Select the S3 bucket and file that contains your `length_mapper.py`
     * **Reducer:** Select the S3 bucket and file that contains your `length_reducer.py`
     * **Input S3 location:** Select the S3 bucket and file that contains the `RomeoAndJuliet.txt` file
     * **Output S3 location:** Select the S3 bucket that you set up for output and then add a ***new*** file name for that specific output
     * **Arguments:** leave blank
     * **Action on failute:** Keep as `Continue`
     * Select the `Add` button
   
   Once you select `Add` the cluster will begin working through the step!
  
  ## Retrieving the Ouput
  ### Part 1: Downloading Files to Local Drive
  Once the step has completed (hopefully with no errors), your output material will be automatically sent to the S3 output bucket you created and will be inside the output file you identified in the step.  To retrieve the files:
  * Log into **S3**
  * Go into the output bucket you created (for my example it was: `outputformapreduce`)
  * Go into the folders you designated the output files to go into
  * There should be 3 "part" files (part-00000, part-00001 and part-00002)
    * The three files are from the 3 nodes that worked on the project and each have a portion of the output
  * Select each file and click on the `Actions` tab
  * Select `Download` from the tab and save it to a local folder with a ***.txt*** extension
  
  ### Part 2: Merging and Sorting Files via Command Line
  Now that you have the `.txt` files on your local computer, you will want to get the data sorted so it is readable and in one file.  To do this you will need to open the command prompt within the folder that your `.txt` files are located.  <br/><br />
  
  Once in the command prompt type: ***Get-Content * .txt | Sort-Object { [double]$_.split()[-0] } | Set-Content sortedfile.txt*** <br /><br />
  
  * The `Get-Content` command retrieves all files in the folder with a ***.txt*** extension
  * The `Sort-Object` command sorts objects in all files by (in this case) the first column
  * The `Set-Content` command allows for the new sorted data to be written as one new .txt file
  <br /><br />
  
  There you have it!  A .txt file that identifies word length and the count of each length in the Romeo and Juliet text!  
  
  
  
  
    
  
