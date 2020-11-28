# MSDS498IndividualProject - Cloud Map Reduce with AWS’ Elastic Map Reduce (EMR)

## Inroduction

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
  * **Name:** Give your key pair a name that is is for you to identify
  * **File format:** I selected pem to use with OpenSSH, but this is not mandatory for the project
  * **All other fields:** Keep default
  * Click the `Create key pair` button at the bottom of the page.
  
  
