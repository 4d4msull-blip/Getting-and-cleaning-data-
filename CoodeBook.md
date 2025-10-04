install.packages('dplyr')
library(dplyr)
library(dplyr)
tidy_data = unzip(getdata_projectfiles_UCI HAR Dataset)
library(dplyr)
tidy_data = "final_project.zip"
download.file(fileURL,tidy_data,method = "curl")}
if (!file.exists(tidy_data)){fileURL = "https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip"
download.file(fileURL,tidy_data,method = "curl")
}
if (!file.exists("UCI HAR Dataset")){unzip(tidy_data)
}
head(tidy_data)
features = read.table("UCI HAR Dataset/features.txt",col.names = c("index","feature"))
features
activity_labels = read.table("UCI HAR Dataset/activity_labels.txt",col.names = c("code","activity"))
subject_train = read.table("UCI HAR Dataset/train/subject_train.txt",col.names = "subject")
x_train = read.table("UCI HAR Dataset/train/x_train.txt",col.names = features$feature)
x_train
y_train = read.table("UCI HAR Dataset/train/y_train.txt",col.names = "code")
subject_test = read.table("UCI HAR Dataset/test/subject_test.txt",col.names = "subject")
x_test = read.table("UCI HAR Dataset/test/X_test.txt",col.names = features$feature)
y_test = read.table("UCI HAR Dataset/test/y_test.txt",col.names = "code")
data = rbind(train,test)
data = rbind(train, test)
X = rbind(x_train,x_test)
Y = rbind(y_train,y_test)
subject = rbind(subject_train,subject_test)
merged_data = cbind(subject,Y,X)
merged_data
Data = merged_data %>% select(subject,code,contains("mean"),contains("std"))
Data
Data$code = activity_labels[Data$code, 2]
names(Data)[2] = "activity"
names(Data) = gsub("Acc","Asselerometer",names(Data))
names(Data) = gsub("Gyro","Gyroscope",names(Data))
names(Data) = gsub("BodyBody","Body",names(Data))
names(Data) = gsub("Mag","Magnitude",names(Data))
names(Data) = gsub("^t","Time",names(Data))
names(Data) = gsub("^f","Frequency",names(Data))
names(Data) = gsub("tBody","TimeBody",names(Data))
names(Data) = gsub("-mea()","mean",names(Data),ignore.case = TRUE)
names(Data) = gsub("-std()","std",names(Data),ignore.case = TRUE)
names(Data) = gsub("-freq()","Frequency",names(Data),ignore.case = TRUE)
FData = Data %>% group_by(subject,activity) %>% summarise_all(mean)
FData
write.table(FData,"FinalData.txt",row.name = FALSE)
