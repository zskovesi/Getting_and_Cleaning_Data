---
Subject: "Getting and Cleaning Data, Course Project"
author: "zskovesi"
date: "Friday, October 24, 2014"

---
---

### Introduction

One of the most exciting areas in all of data science right now is wearable computing - see for example this article . Companies like Fitbit, Nike, and Jawbone Up are racing to develop the most advanced algorithms to attract new users. The data linked to from the course website represent data collected from the accelerometers from the Samsung Galaxy S smartphone. A full description is available at the site where the data was obtained: 

#### Data can be dowloaded from here:

(https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip)

#### Data Set information

(http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones )

The experiments have been carried out with a group of 30 volunteers within an age bracket of 19-48 years. Each person performed six activities (WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING) wearing a smartphone (Samsung Galaxy S II) on the waist. Using its embedded accelerometer and gyroscope, we captured 3-axial linear acceleration and 3-axial angular velocity at a constant rate of 50Hz. The experiments have been video-recorded to label the data manually. The obtained dataset has been randomly partitioned into two sets, where 70% of the volunteers was selected for generating the training data and 30% the test data. 

#### Attribute Information

For each record in the dataset it is provided: 

- Triaxial acceleration from the accelerometer (total acceleration) and the estimated body acceleration. 
- Triaxial Angular velocity from the gyroscope. 
- A 561-feature vector with time and frequency domain variables. 
- Its activity label. 
- An identifier of the subject who carried out the experiment.

---------


### R script called `run_analysis.R` does the following: 

1. Merges the training and the test sets to create one data set.
2. Extracts only the measurements on the mean and standard deviation for each measurement. 
3. Uses descriptive activity names to name the activities in the data set
4. Appropriately labels the data set with descriptive variable names. 
5. From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each activity and each subject.

##### 1. Merge the training and the test sets to create one data set

- Set working directory to the location where the UCI HAR Dataset is planned to be unzipped, then download, extract, remove zip file

- Read in the data from files:

           features.txt
           activity_labels.txt
           .../train/subject_train.txt
           .../train/x_train.txt
           .../train/y_train.txt

- Assign column names **activityID**, **activityType**, **subjectID** and 561 features to the train data imported above

           1 WALKING
           2 WALKING_UPSTAIRS
           3 WALKING_DOWNSTAIRS
           4 SITTING
           5 STANDING
           6 LAYING


- Create the final training set by merging yTrain, subjectTrain, and xTrain

- Read the test data

           .../test/subject_test.txt
           .../test/x_test.txt
           .../test/y_test.txt

- Assign column names to the test data imported above
- Create the final test set by merging the xTest, yTest and subjectTest data
- Combine/merge training and test data to create a final data set
- Create a vector for the column names from the finalData, which will be used to select the mean() & stddev() columns

##### 2. Extract only the measurements on the mean and standard deviation for each measurement 

- Create a logicalVector that contains TRUE values for the ID, mean() & stddev() columns and FALSE for others
- Subset finalData table based on the logicalVector to keep only the required columns

##### 3. Use descriptive activity names to name the activities in the data

- Merge the finalData with the acitivityType table to include descriptive activity names
- Update the colNames vector to include the new column names after merge
 
##### 4. Appropriately label the data with descriptive activity names 

- Clean up the variable names by using gsub function for pattern replacement
- Reassigning the new descriptive column names to the finalData set

##### 5. Create a second, independent tidy data with the average of each variable for each activity and each subject 
- This second dataset has only average of each variable for each activity and subject
- Create a new table, finalDataNoActivityType without the activityType column
- Summarizing the finalDataNoActivityType table to include just the mean of each variable for each activity and each subject
- Merging the tidyData with activityType to include descriptive acitvity names
- Name tidyData and export the file