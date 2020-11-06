# MSDS498IndividualProject
This will host the source code and information pertaining to my MSDS 498 Individual Project.

## Romeo and Juliet Text
Originally, the Romeo and Juliet text was downloaded from this website: **https://www.gutenberg.org/ebooks/1513** <br /><br />
Since the text was uploaded to my local computer previously, I just had to select `Add file` and then `Upload file` within this repository to add the .txt to it.

## Mapper Code
The `mapper.py` code was sourced from Python for Programmers Chapter 16.5 (*citation below*).  This code asks the cluster to perform the mapping portion of the project by reading each line of text and for each word produce a key-value pair with the **word**, a **tab** and the number **1**.  

## Reducer Code
The `reducer.py` code was also sourced from the Python for Programmers text (*citation below*).  This code tasks the cluster with taking the mapped product (*above*) and counting the number of words of each length.  It should then produce new key-value pairs of the word legnth and the number of words in the text with that length.    
