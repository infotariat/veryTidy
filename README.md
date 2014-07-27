veryTidy
========

My code for Coursera Getting and Cleaning Data course project assignment


README file for my course project

This code, named "run_analysis.R" creates the tidy data set required for the course project for the Coursera course "Getting and Cleaning Data."

To use this code, you must download a zip file containing the files used for the 

project.  The URL is:

https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip 

Once you have downloaded this file, unzip it into a folder named "UCIHAR" (create this 
folder within your R working directory first).  You will need to move the following files 
into the top level of this UCIHAR folder:

"subject_test.txt"
"X_test.txt"
"Y_test.txt"
"subject_train.txt"
"X-train.txt"
"Y-train.txt"
"features.txt"
"activity_labels.txt"

The code for "run_analysis.R":

*** The first block of code reads the data files into R using a series of read.table() 
commands.

*** The second block of code merges the training and test data sets into one data set 
using rbind() and cbind() commands.

*** You will see a rm() command which just does some housecleaning so that the user 
will not have so much drain on their RAM

*** The third block of code renames the column names for the data frame with names 
"subject," "activity," and the names in features.txt.  A full explanation of these feature 
names can be found in the folder you unzipped, in a file named "features_info.txt."  I 
have opted to keep these feature names (at least, the ones that were not trimmed 
later in the code) as the names for the columns.  They do the best job of describing 
the measurement while retaining some level of brevity.

*** The fourth block of code creates a new data frame with just the features of 
interest.  In other words, the measurement columns are reduced from 561 to 66.  
There are now a total of 68 columns when you count the 2 id columns.  The code 
manages to trim the columns almost perfectly on the first pass, but needs to revise the 
dataframe one last time to jettison the "meanFreq" columns.  We now have all of the 
means and standard deviations of the basic measurements as our measurement 
columns. A line of housecleaning for the user's benefit follows.

*** The fifth block of code creates "tidyframe," which is the data frame which will 
contain the final output of the analysis.  tidyframe is set up as an empty data frame, 
and then a loop is used to trim the rows of our data set from 10299 rows to 180 rows.
The 10299 rows are made up of the indivual instances of data produced by the 30 
subjects of the experiment as they perform 6 activities.  Each activity performed 
produces an average of 57.22 instances of data, hence 10299 rows (30x6x57.22).
tidyframe's rows are the unique combinations of subjects and activities, and the mean 
measurements of the instances of data produced by those subject-activity pairs for 
each column's feature measurement.


*** The sixth block of code renames the remaining columns again, as the names get lost 
in the mix when performing the loops. It then renames the activities from (1,2,3,4,5,6) 
to (walk, upstairswalk, downstairswalk, sit, stand, lay). Lastly, outputs the resulting 
dataframe to a text file named "Samsung_Data.txt".  This is the tidy data set requested 
by the course project guidelines - the end product of the data cleaning process for 
future analysis of the experiment.
