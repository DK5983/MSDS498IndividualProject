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
For this project you will be creating ***three*** S3 buckets.  The first of which will hold the `RomeoAndJuliet.txt`. <br /><br />

To create an AWS S3 bucket complete the following:
* From your AWS Management Console select `S3` from the services. 
* In **S3** select the `Create Bucket` tab
  * **Name:** Give your bucket a unique name with lowercase letters and no spaces (you can use numbers)
  * **Region:** Select region that is closest to you
  * **All other fields:** Keep default
  * Select the `Create Bucket` tab at the bottom of the page.


#### Uploading to S3
 



## Mapper Code
The `mapper.py` code was sourced from Python for Programmers Chapter 16.5 (*citation below*).  This code asks the cluster to perform the mapping portion of the project by reading each line of text and for each word produce a key-value pair with the **word**, a **tab** and the number **1**.  

## Reducer Code
The `reducer.py` code was also sourced from the Python for Programmers text (*citation below*).  This code tasks the cluster with taking the mapped product (*above*) and counting the number of words of each length.  It should then produce new key-value pairs of the word legnth and the number of words in the text with that length.    
