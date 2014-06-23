#Code Book

##tidy.txt columns

###There are 68 columns in the dataset, a text file which is delimited by 'space'


#### Simple description of the columns
1.	SubjectIdentifier  - This is a identifier for the subject whose data is being measured.
I have kept it simple and just prefixed the subject with 'Subject-'. For example the first
subject is named 'subject-1'
2.	Activity - This is the activity label instead of the numbers 1-6. For example instead of '1'
activity I have given it WALKING
3.	Avg-tBodyAccmeanX - Columns 3-68 are all average columns. These are the same original column names
from features file with some simple modifications. The first modification is that these are columns 
with std and or mean function in their names. Second modification is that all the special characters
i.e. the punctuations were removed so that I have no issue with R function
4. 	Avg-tBodyAccmeanY
5.	Avg-tBodyAccmeanZ
6.	Avg-tGravityAccmeanX
7.	Avg-tGravityAccmeanY
8.	Avg-tGravityAccmeanZ
9.	Avg-tBodyAccJerkmeanX
10.	Avg-tBodyAccJerkmeanY
11.	Avg-tBodyAccJerkmeanZ
12.	Avg-tBodyGyromeanX
13.	Avg-tBodyGyromeanY
14.	Avg-tBodyGyromeanZ
15.	Avg-tBodyGyroJerkmeanX
16.	Avg-tBodyGyroJerkmeanY
17.	Avg-tBodyGyroJerkmeanZ
18.	Avg-tBodyAccMagmean
19.	Avg-tGravityAccMagmean
20.	Avg-tBodyAccJerkMagmean
21.	Avg-tBodyGyroMagmean
22.	Avg-tBodyGyroJerkMagmean
23.	Avg-fBodyAccmeanX
24.	Avg-fBodyAccmeanY
25.	Avg-fBodyAccmeanZ
26.	Avg-fBodyAccJerkmeanX
27.	Avg-fBodyAccJerkmeanY
28.	Avg-fBodyAccJerkmeanZ
29.	Avg-fBodyGyromeanX
30.	Avg-fBodyGyromeanY
31.	Avg-fBodyGyromeanZ
32.	Avg-fBodyAccMagmean
33.	Avg-fBodyBodyAccJerkMagmean
34.	Avg-fBodyBodyGyroMagmean
35.	Avg-fBodyBodyGyroJerkMagmean
36.	Avg-tBodyAccstdX
37.	Avg-tBodyAccstdY
38.	Avg-tBodyAccstdZ
39.	Avg-tGravityAccstdX
40.	Avg-tGravityAccstdY
41.	Avg-tGravityAccstdZ
42.	Avg-tBodyAccJerkstdX
43.	Avg-tBodyAccJerkstdY
44.	Avg-tBodyAccJerkstdZ
45.	Avg-tBodyGyrostdX
46.	Avg-tBodyGyrostdY
47.	Avg-tBodyGyrostdZ
48.	Avg-tBodyGyroJerkstdX
49.	Avg-tBodyGyroJerkstdY
50.	Avg-tBodyGyroJerkstdZ
51.	Avg-tBodyAccMagstd
52.	Avg-tGravityAccMagstd
53.	Avg-tBodyAccJerkMagstd
54.	Avg-tBodyGyroMagstd
55.	Avg-tBodyGyroJerkMagstd
56.	Avg-fBodyAccstdX
57.	Avg-fBodyAccstdY
58.	Avg-fBodyAccstdZ
59.	Avg-fBodyAccJerkstdX
60.	Avg-fBodyAccJerkstdY
61.	Avg-fBodyAccJerkstdZ
62.	Avg-fBodyGyrostdX
63.	Avg-fBodyGyrostdY
64.	Avg-fBodyGyrostdZ
65.	Avg-fBodyAccMagstd
66.	Avg-fBodyBodyAccJerkMagstd
67.	Avg-fBodyBodyGyroMagstd
68.	Avg-fBodyBodyGyroJerkMagstd

#### Including the feature info so that you interstand the background of what the columns are
Feature Selection 
=================

The features selected for this database come from the accelerometer and gyroscope 3-axial raw signals tAcc-XYZ and tGyro-XYZ. These time domain signals (prefix 't' to denote time) were captured at a constant rate of 50 Hz. Then they were filtered using a median filter and a 3rd order low pass Butterworth filter with a corner frequency of 20 Hz to remove noise. Similarly, the acceleration signal was then separated into body and gravity acceleration signals (tBodyAcc-XYZ and tGravityAcc-XYZ) using another low pass Butterworth filter with a corner frequency of 0.3 Hz. 

Subsequently, the body linear acceleration and angular velocity were derived in time to obtain Jerk signals (tBodyAccJerk-XYZ and tBodyGyroJerk-XYZ). Also the magnitude of these three-dimensional signals were calculated using the Euclidean norm (tBodyAccMag, tGravityAccMag, tBodyAccJerkMag, tBodyGyroMag, tBodyGyroJerkMag). 

Finally a Fast Fourier Transform (FFT) was applied to some of these signals producing fBodyAcc-XYZ, fBodyAccJerk-XYZ, fBodyGyro-XYZ, fBodyAccJerkMag, fBodyGyroMag, fBodyGyroJerkMag. (Note the 'f' to indicate frequency domain signals). 

These signals were used to estimate variables of the feature vector for each pattern:  
'-XYZ' is used to denote 3-axial signals in the X, Y and Z directions.

tBodyAcc-XYZ
tGravityAcc-XYZ
tBodyAccJerk-XYZ
tBodyGyro-XYZ
tBodyGyroJerk-XYZ
tBodyAccMag
tGravityAccMag
tBodyAccJerkMag
tBodyGyroMag
tBodyGyroJerkMag
fBodyAcc-XYZ
fBodyAccJerk-XYZ
fBodyGyro-XYZ
fBodyAccMag
fBodyAccJerkMag
fBodyGyroMag
fBodyGyroJerkMag

The set of variables that were estimated from these signals are: 

mean(): Mean value
std(): Standard deviation
mad(): Median absolute deviation 
max(): Largest value in array
min(): Smallest value in array
sma(): Signal magnitude area
energy(): Energy measure. Sum of the squares divided by the number of values. 
iqr(): Interquartile range 
entropy(): Signal entropy
arCoeff(): Autorregresion coefficients with Burg order equal to 4
correlation(): correlation coefficient between two signals
maxInds(): index of the frequency component with largest magnitude
meanFreq(): Weighted average of the frequency components to obtain a mean frequency
skewness(): skewness of the frequency domain signal 
kurtosis(): kurtosis of the frequency domain signal 
bandsEnergy(): Energy of a frequency interval within the 64 bins of the FFT of each window.
angle(): Angle between to vectors.

Additional vectors obtained by averaging the signals in a signal window sample. These are used on the angle() variable:

gravityMean
tBodyAccMean
tBodyAccJerkMean
tBodyGyroMean
tBodyGyroJerkMean

The complete list of variables of each feature vector is available in 'features.txt'


