#README file

##Assumptions
These are the list of assumptions I am making for this assignment
1. I will try to download the zipped file from the URL given
   in the assignment in the function downloadUnzipFiles() if the zipped file is not already there. I check to see if 
   the root level directory exists for the zipped content.
2. I am also making an assumption that other directories underneath exist and previously unzipped

# How to run the file
Basically you need to call 'run_analysis()' without any argument after souring the file.
It calls a function to download the zipped file.

It then tries to take the training files and combine that with test files for each of the different files it has in the datasets. For example


   
        #Writing out tidy file
        write.table(mytidydf, file="tidyInitial.txt", row.names=F, col.names=T)
        
        #Trying to make the dataframe narrow using melt - all measurements
        #are in one column
        library(reshape2)
        library(plyr)
        mymelttidydf<-melt(mytidydf,id.vars=c("SubjectIdentifier","Activity"))
        
        #Attempting to order the dataset on SubjectIdentifier, Activity
        mymelttidyordereddf<-arrange(mymelttidydf, SubjectIdentifier, Activity)
        
        #now calculating averages overall activities/for each subject
        tidydf<-ddply(mymelttidyordereddf, .(SubjectIdentifier,Activity,variable), 
                  summarize, mean=mean(value))
        
        #arranging the calculations into columns as earlier
        finaltidydf1<-dcast(tidydf, SubjectIdentifier+Activity~variable, value.var="mean")
        
        #Putting a suffix as the data columns are now averages of earlier columns 
        suffixColNames<-names(finaltidydf1)
        prefix<-"Avg-"
        newnames<-paste(prefix, suffixColNames,sep="")
        newnames[1:2]<-c("SubjectIdentifier","Activity") #first two columns need not rename
        names(finaltidydf1)<-newnames
        
        #Writing the final tidy data set
        write.table(finaltidydf1, file="tidy.txt", row.names=F, col.names=T)

        
}
combineDatasets<-function(){
        #combining all X data from test and training datasets
        testXdata<-read.table("UCI HAR Dataset/test/X_test.txt")
        trainXdata<-read.table("UCI HAR Dataset/train/X_train.txt")
        allXdata<-rbind(testXdata,trainXdata)
        
        #reading feature names from features file and assigning column names
        #to the X data frame
        features<-read.table("UCI HAR Dataset/features.txt", stringsAsFactors=FALSE)    
        colnames(allXdata)<-gsub("[[:punct:]]", "",features[,2])
        
        #combining all Y data from test and training datasets
        testydata<-read.table("UCI HAR Dataset/test/y_test.txt")
        trainydata<-read.table("UCI HAR Dataset/train/y_train.txt")
        allydata<-rbind(testydata,trainydata)
        colnames(allydata)<-c("Activity")
        
        #reading labels for y data
        labels<-read.table("UCI HAR Dataset/activity_labels.txt")
        
        #assigning activity labels to numbers in y data file
        allydata[allydata$Activity==1,]<-as.character(labels[1,2])
        allydata[allydata$Activity==2,]<-as.character(labels[2,2])
        allydata[allydata$Activity==3,]<-as.character(labels[3,2])
        allydata[allydata$Activity==4,]<-as.character(labels[4,2])
        allydata[allydata$Activity==5,]<-as.character(labels[5,2])
        allydata[allydata$Activity==6,]<-as.character(labels[6,2])
        allydata$Activity=as.factor(allydata$Activity)
        
        #combining all Subject data from test and training datasets
        testsubjectdata<-read.table("UCI HAR Dataset/test/subject_test.txt")
        trainsubjectdata<-read.table("UCI HAR Dataset/train/subject_train.txt")
        
        allsubjectdata<-rbind(testsubjectdata,trainsubjectdata)
        colnames(allsubjectdata)<-c("SubjectIdentifier")
        
        #giving factor labels to subjects
        for(i in 1:30){
                allsubjectdata[allsubjectdata$SubjectIdentifier==i,]<-paste("subject-",i,sep="")
                i<-i+1
        }
        allsubjectdata$SubjectIdentifier=as.factor(allsubjectdata$SubjectIdentifier)
        
        #combining all X, Y and subject data in one data frame
        alldatadf<-cbind(allsubjectdata,allydata, allXdata)
        
        #trying to grab the mean and std columns from features 
        meancolumnsdf<-as.data.frame(features[grepl("mean\\(\\)" ,features[,2]),])
        stdcolumnsdf<-as.data.frame(features[grepl("std\\(\\)" ,features[,2]),])
        untidyXcolumns<-as.data.frame(rbind(meancolumnsdf,stdcolumnsdf))
        
        #removing special characters to get the columns of interest
        meanstdcolumns<-gsub("[[:punct:]]", "",untidyXcolumns[,2])
        
        #Creating tidy data set with first two columns (subject, activity)
        #and columns which match mean/std functions
        tidydf<-as.data.frame(cbind(alldatadf[,1:2],alldatadf[,meanstdcolumns]))
        
        #returning a tidy df
        return(tidydf)
      
}
