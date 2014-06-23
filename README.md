#README file

These are the list of assumptions I am making for this assignment 

1. I will try to download the zipped file from the URL given in the assignment to the 
current working directory if there is no zipped file already present in the current directory.
2. I will see if the root level directory exists for the zipped content ('UCI HAR Dataset'). 
Again here I am assuming that the file was previously unzipped if I find this.
3. I am also making an assumption that other directories underneath exist and 
previously unzipped only if the root level directory exists for the data.


### How to run the file

Basically you need to call 'run_analysis()' without any argument after running source on the
file 'run_analysis.R'. 

### What it outputs

It writes a file 'tidy.txt' with 68 columns. The first column identifies the subject. The 
second column tells what activity the subject was doing. The remaining observations are
an average of all the observations taken for a given subject/activity.

#### What is the file doing

The main function calls downloadUnzipFiles() which tries to download the zipped files 
and unzip them.

Next it combines the test/training datasets by calling the function combineDatasets().
This function returns an initial tidy data frame which is later massaged much further.

##### combineDatasets() function logic
In the function combineDatasets() it tries to take the training files and combine that with 
test files for each of the different files it has in the datasets. For example its takes
all X data from test and training datasets from their respective folders and uses rbind
to combine into one data frame.

Once the data is combined, it nexts tries to give a header row by reading all column names from
the features file and later removing all special characters (punctuation) by using gsub()

For the Y data, the same process is followed except the Activity numbers 1-6 are replaced by
the actual labels. For example 'WALKING' is assigned to 1.

While dealing with subject data files, the numbers 1-30 which are different subjects are 
replaced by the following naming convention 'Subject-1' for subject 1.

Once the three dataframes are thus formed, they are combined into one dataframe using cbind.

Next the mean and std (standard deviation) columns are determined by examining feature names.
If the feature name has std() or mean() in them, I am assuming they are the columns of interest.
        
Once the mean/std columns are extracted and combined, they are used to subset the dataframe from
earlier. This will only have around 68 columns.      
        

##### remaining logic
The main function then writes the intial tidy data frame for any analysis (if needed).
This is only used for validation that everything looks good. This is however not needed as this
is not the final tidy data frame.

Next I try to make the dataframe narrow using melt (part of reshape2 library) - all measurements
are in one column. Then I order the dataset on SubjectIdentifier, Activity. Then I calculate
the averages of overall activities/for each subject using ddply (plyr library).

Once calculations are done, I use dcast to put the narrow dataframe into a wide data frame
with all columns back to how they were.

I then change the column names to prefix with Avg- to show the calculations are now averages
of all the observations for a given subject/activity for each type of observation.  
        
I finally write the table to a 'tidy.txt' file.
