# G-CD_Project
Repo of my final project in Getting and cleaning data 

## Description of the code:

I think the code is self-explained but let's make a summary, 
we extract all the text files we need and the variables we are interested in those related with the mean and 
standrad deviation, then we merge them in a single data frame with the subject and the activity variable aswell
After that we group by subject and activity and obtain the mean of all variables store it in a new variable.
The final datat frame is a table with dimensions of 180x83.

## Codebook
In a general descrition of the variables we have:

"Subject": Each number belong to a certain person (there are 30 persons in total)

"Activity": Each number blong to a certain activity duning the medition of the rest of varibles
            -1. Walking
            -2. Walking upstairs
            -3. Walkig downstairs
            -4. Sitting
            -5. Standing
            -6. Laying

The rest of variables are means of diferent meditions related with means and standard deviations 
for each subject and activity such 
Triaxial acceleration from the accelerometer (total acceleration) and the estimated body acceleration and
Triaxial Angular velocity from the gyroscope. 
The results are normalized and bounded within [-1,1].
