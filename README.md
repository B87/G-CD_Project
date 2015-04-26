# G-CD_Project
Repo of my final project in Getting and cleaning data 

##Let's extract first the variables we're interested in from the features file.

setwd("C:/Users/Bernat/Desktop/MOOCS/getting and cleaning data/project_data/UCI HAR Dataset")
      features<-read.table("features.txt")
            features<-features[,2]
                  meanfeatures<-grep("mean",features)
                        stdfeatures<-grep("std",features)
                              feature_indexes<-sort(append(meanfeatures,stdfeatures))
                                    rm(meanfeatures,stdfeatures)

## Now we import test data filtering it by indexes in order to work with less data before
## binding it into one data frame and change the names of the variables. 

setwd("C:/Users/Bernat/Desktop/MOOCS/getting and cleaning data/project_data/UCI HAR Dataset/test")
xtest<-read.table("X_test.txt")
xtest<-xtest[,feature_indexes]
colnames(xtest)<-features[feature_indexes]
ytest<-read.table("y_test.txt")
subject_test<-read.table("subject_test.txt")
test<-cbind(subject_test,ytest,xtest)
names(test)[1]<-"Subject"
names(test)[2]<-"Activity"
rm(ytest,xtest,subject_test)

## Now we do the same as above using the train data instead

setwd("C:/Users/Bernat/Desktop/MOOCS/getting and cleaning data/project_data/UCI HAR Dataset/train")
xtrain<-read.table("X_train.txt")
xtrain<-xtrain[,feature_indexes]
colnames(xtrain)<-features[feature_indexes]
ytrain<-read.table("y_train.txt")
subject_train<-read.table("subject_train.txt")
train<-cbind(subject_train,ytrain,xtrain)
names(train)[1]<-"Subject"
names(train)[2]<-"Activity"
rm(ytrain,xtrain,subject_train)

## We merge now both data sets 
data<-rbind(test,train)
rm(test,train,features,feature_indexes)

## Now we will use the dplyr package to get the final data frame. 

library(dplyr)

data<-tbl_df(data)

x<-data %>% 
      group_by(Subject,Activity) %>% 
            summarise_each(funs(mean(., na.rm = TRUE)), matches("mean"))

y<-data %>% 
      group_by(Subject,Activity) %>% 
            summarise_each(funs(mean(., na.rm = TRUE)), matches("std"))

final<-cbind(x,y)

rm(x,y)
