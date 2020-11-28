# MSDS498IndividualProject - Cloud Map Reduce with AWS’ Elastic Map Reduce (EMR)

## Inroduction

In the sixteenth chapter of the textbook *Python for Programmers*, the authors walk you through a number of exercises pertaining to Big Data utilizing Hadoop, Spark, NoSQL and IoT (**https://learning.oreilly.com/library/view/python-for-programmers/9780135231364/ch16.xhtml**).  In section 16.5 the exercise was to configure and run a MapReduce Cluster in Azure that could identify the length of each word in a text and count how many words had each length.  For this project, I wanted to get the same end result, but use a different cloud-based platform.  I chose **Amazon Web Services (AWS)** for this project utilizing their **Elastic Map Reduce (EMR)** program

This will host the source code and information pertaining to my MSDS 498 Individual Project.

## Romeo and Juliet Text
Originally, the Romeo and Juliet text was downloaded from this website: **https://www.gutenberg.org/ebooks/1513** <br /><br />
Since the text was uploaded to my local computer previously, I just had to select `Add file` and then `Upload file` within this repository to add the .txt to it.

## Mapper Code
The `mapper.py` code was sourced from Python for Programmers Chapter 16.5 (*citation below*).  This code asks the cluster to perform the mapping portion of the project by reading each line of text and for each word produce a key-value pair with the **word**, a **tab** and the number **1**.  

## Reducer Code
The `reducer.py` code was also sourced from the Python for Programmers text (*citation below*).  This code tasks the cluster with taking the mapped product (*above*) and counting the number of words of each length.  It should then produce new key-value pairs of the word legnth and the number of words in the text with that length.    
