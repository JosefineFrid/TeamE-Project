# TeamE-Project

Our workplan is to create graph 3.2 and 3.4. The temperature for every day of the year and the mean temperature of each year. Our "own" graph will be the mean temperature of each month in a year. We have decided to use the weather data from Lund.

The logic behind 3.2 and our own is to run the data and for the dates of the year we are checking we collect. Then we split the data up so that it will be printed out in order starting with january 1th and ending with december 31th. To do this sorting we can for example perhaps sort each date into every month and then in every month we have a loop that orders them from 1-highest date. Or maybe a loop that can order in months and dates all together. To get the mean value of every month we will have to split the dates into months and then divide by how many dates. The logic behind 3.4 is to collect all the temperatures for each day of that year and split them by 365. If we have time we could check for leap year. 

The plan is to focus on one graph each but help eachother out when we need help.

Ilayda: 3.2
Josefine: "Own" graph
Hristiana: 3.4

Due to that we are now only two people we will make our own graph and 3.2.
We are looking at using librarys for the data.

This is what I've done until now:
I am trying to clean up the data by doing the case study from tutorial 3. This is how far I've gotten:

#!/bin/bash

###### Functions #######################################################

## usage
# this function takes no parameters and prints an error with the 
# information on how to run this script.
usage(){
	echo "----"
	echo -e "  To call this script please use"
	echo -e "   $0 '<path>'"
	echo -e "  Example:"
    echo -e "   $0 '/tutorial3/casestudy/data/smhi-opendata_1_52240_20200905_163726.csv'"
	echo "----"
}

###### Functions END =##################################################


# T1 Get the first parameter from the command line:
# (see Tutorial 3 slides 39,40)
# and put it in the variable SMHIINPUT
SHMIINPUT=$#

# T2 Input parameter validation:
# Check that the variable SMHIINPUT is defined, if not, 
# inform the user, show the script usage by calling the usage() 
# function in the library above and exit with error
# See Tutorial3 Slide 47 and exercises 3.14, 3.15
if  [[ $# -le 1 ]];  then
    echo "Missing input file parameter, exiting";
    exit 1;
else
    # echo "Argument good."
    exit 0;
fi

# T3 Extract filename:
# Extract the name of the file using the "basename" command 
# basename examples: https://www.geeksforgeeks.org/basename-command-in-linux-with-examples/
# then store it in a variable DATAFILE
DATAFILE= basename smhi-opendata_1_52230_20210906_212532.csv

# T4 Analyze the input parameter and copy:

# T4.1 If $SMHIINPUT not empty
if [[ “x$SMHIINPUT” != “x” ]]
   # T4.2 check if the file is a directory, it should not be!
   # exit with error in case.
   if [[ -d "$SMHIINPUT" ]]
      echo -e "This script requires a data file and not a directory, exiting..."     
      exit 1;
   fi
   # T4.3 Copy the file in the current directory as
   #    original_$DATAFILE
   # use the -a option to preserve filesystem information (permissions etc)
   echo "Copying input file $SMHIINPUT to original_$DATAFILE"
   YOUR_CODE_HERE
fi 

# T5 Check that the input file has been copied with no errors:
# Write an IF statement that does the following:
# If any of the previous commands failed, exit with error 
# and tell the user what happened.
# remind the user of the syntax by calling the usage() function defined
# in the libraries section above.
# test the $? variable, Tutorial 3 slides 41, 42 
# and previous years exercises (Tutorial 3 slide 15)
if YOUR_CODE_HERE
   echo "Error downloading or copying file, maybe wrong command syntax? exiting...."
   YOUR_CODE_HERE
fi

# If we got here without errors, we can start cleaning up!

# T6 Identify the data starting line:
# Looking at the SHMI data, it seems that the line that contains the
# string "Datum" is the beginning of data.
# Find what line contains the string "Datum" using grep
# put the value in a variable called STARTLINE
# - use the grep option -n  and cut to take just the number.
# - use the cut command to select field 1 using ':' as separator
# - Use the pipe | to pass the output of grep to cut
# Examples about the above can be found in Tutorial 3 slide 84 and 
# some on Tutorial 2
# read also:
# https://stackoverflow.com/questions/6958841/use-grep-to-report-back-only-line-numbers
echo "Finding the first line containing 'Datum'..."
STARTLINE=YOUR_CODE_HERE

# T7 skip one more header line:
# Use arithmetic expansion to add a line, since the actual 
# data starts at the STARTLINE + 1 line, so to remove the header
# where Datum;... is contained
# See Slides 86, 90
STARTLINE=YOUR_CODE_HERE

# T8 Remove unnecessary lines at the top of the datafile:
# Strip away the top STARTLINE lines (the value of $STARTLINE) using 
# the tail command and write the result 
# to as file called clean1_$DATAFILE using the > operator to 
# redirect the standard output.
# how to exclude n lines with tail : http://heyrod.com/snippets/skip-n-lines.html
# For the use of the > operator, see Tutorial 2
# Redirecting output: https://thoughtbot.com/blog/input-output-redirection-in-the-shell#redirecting-output
# You can verify the generated file against the same file in tutorial3/casestudy/result
echo "Removing the first $STARTLINE lines, result in clean1_${DATAFILE}"
YOUR_CODE_HERE

# T9 Fix format for the strange lines with comments:
# consider only the relevant columns (1,2,3,4,5) using cut
# this will clean up the lines at the beginning of the data 
# that are not consistent with the format, so that we can use the data 
# these lines contain without discarding them.
# Write the result to a file called clean2_${DATAFILE} using the > operator
# see cut examples at the link in Tutorial 3 slide 85, in particular
#       "5. Select Multiple Fields from a File"
# You can verify the generated file against the same file in tutorial3/casestudy/result
echo "Selecting only relevant columns, result in clean2_${DATAFILE}"
YOUR_CODE_HERE

# T10 Convert format to C++ readable with spaces instead of commas:
# Change semicolons to singe spaces using sed and 
# write out the result to a file called rawdata_${DATAFILE}
# TODO read about sed at the links in Tutorial 3 slide 84,
# and here: https://linuxize.com/post/how-to-use-sed-to-find-and-replace-string-in-files/
# You can verify the generated file against the same file in tutorial3/casestudy/result
echo "Substituting the ; with spaces, result in rawdata_${DATAFILE}"
YOUR_CODE_HERE

# initialize empty report file
# here I use the special device /dev/null so that if there is already
# an existing file it will be cleaned
cat /dev/null > report_${DATAFILE}

# T11 Print sizes of generated .csv files in a report file:
# Using a for, scan all the .csv files in the folder and write out a
# report of their size in report_<filename>
# cycle the files with a variable csvfile
# Save the size of each file in variable SIZE using the "stat" command
# see: https://www.howtogeek.com/451022/how-to-use-the-stat-command-on-linux/
# to verify the results: compare your output with the script_output file
# in the tutorial3/casestudy/result folder
echo "Writing filesizes summary to report_${DATAFILE}"
for YOUR_CODE_HERE
done
