# School District Analysis
## Overview of the Project
### Purpose
My client, Maria, is a chief data scientist for a city school district and needs assistance with analyzing data regarding the standardized test scores of students. She would like a high-level snapshot of the district's key metrics presented in a table format and an overview of the key metrics for each school presented in a table format. She also desires tables presenting each of the following metrics: top 5 and bottom 5 performing schools based on the overall passing rate, the average math score received by students in each grade level at each school, the average reading score received by students in each grade level at each school, school performance based on the budget per student, school performance based on the school size, and school performance based on the type of school. The board has also recently notified Maria that signs of academic dishonesty are present in the reading and math grades for Thomas High School ninth graders. Maria thereby needs these scores to be replaced with NaNs, while keeping the rest of the data intact. 
## Results
### Assessing the Data
Before analyzing the data, I imported pandas as a dependency and loaded the schools_complete.csv and students_complete.csv files into the Jupyter Notebook. To read and store the data into a Pandas DataFrame, I initialized the following: "school_data_df = pd.read_csv(school_data_to_load)" and "student_data_df = pd.read_csv(student_data_to_load)". To ensure the data was clean, I iterated through a list I created of prefixes and suffixes that were not related to a familial name and removed them. 
![image](https://user-images.githubusercontent.com/106560739/177842990-ec7f6359-7873-40f7-95b0-70672ed61749.png)
   Generating analysis on the data after signs of academic dishonesty were observed, required that I import numpy into the Jupyter Notebook. I utilized the loc[] method to select all the reading and math scores from the ninth graders at Thomas High School. Inside the loc[], I did the following: used a comparison operator to retrieve all rows with Thomas High School in the “school_name” column of the "student_data_df", used a comparison operator to retrieve all rows with the ninth grade in the “grade” column of the "student_data_df", used logical and comparison operators to retrieve all rows with the “reading_score” column for Thomas High School ninth graders from the "student_data_df", and used logical and comparison operators to retrieve all rows with the “math_score” column for Thomas High School ninth graders from the "student_data_df". All the reading and math scores for the ninth graders in Thomas High school were then replaced with NaN’s.
![image](https://user-images.githubusercontent.com/106560739/177843320-1b5c499c-8be1-4987-85bb-11cefcfa9163.png)
![image](https://user-images.githubusercontent.com/106560739/177843369-ff747f1e-6dc2-447a-81a2-cecc2b0a06be.png)
### Findings
* _How is the school district summary affected?_
To generate analysis on the district, I used the pd.merge() operator to combine the "student_data_df" and "school_data_df" into a single dataset, which I named "school_data_complete_df". I merged it by the left on the “school_name” column. I then calculated the total number of schools using the len() operation and unique() method on the "school_data_complete_df", which returned the unique items in the “school_name” column. I calculated the total number of students by initializing a variable, “student_count”, and utilized the count() method on the “Student ID” column in the "school_data_complete_df". To calculate the total budget, I used the sum() function on the “budget” column of the "school_data_complete_df". It was then necessary to calculate the total math and reading scores by utilizing the mean() operation. I initialized an “average_math_score” variable and set it equal to “school_data_complete_df["math_score"].mean()". I repurposed the code to generate reading scores by initializing an “average_reading_score” variable and setting it equal to “school_data_complete_df["reading_score"].mean()”. 
![image](https://user-images.githubusercontent.com/106560739/177844185-adceff83-ea5b-4589-89ef-53d2c939b270.png)
For the original script, I initialized a “passing_math” variable and filtered the “math_score” column in the "school_data_complete_df" to greater than or equal to 70. It is important to note that the district determined that a score of 70 or greater is considered passing. I then applied the count() method to the “student_name” column of the “passing_math” variable to get the total number of students who passed math. This produced a total count, which I named “passing_math_count”. I then repurposed the code to find the total number of students who passed reading. To get the percentage of students who passed math and reading, I divided the “passing_math_count” and the “passing_reading_count” by the total number of students (named “student_count”) and multiplied it by 100. Since I was calculating a percentage, I converted the “student_count” to a number with a decimal, or floating-point decimal, using float().
![image](https://user-images.githubusercontent.com/106560739/177844490-f2a20906-03e4-4912-bef6-e1df94238546.png)
To acquire the overall passing percentage, I first filtered the "school_data_complete_df" by adding the "school_data_complete_df["math_score"] >= 70" and "school_data_complete_df["reading_score"] >= 70" with the logical operator "&" within brackets. To get the total number of students who passed both math and reading, I applied the count() method to the "passing_math_reading". To calculate the percentage of students who passed both math and reading I divided the “overall_passing_math_reading_count” by the “student_count” and multiplied it by 100. 
![image](https://user-images.githubusercontent.com/106560739/177844660-94c9b40b-ec39-4648-9d6a-4bb9fefbcea4.png)
I then created a "district_summary_df" using the pd.DataFrame() operator and inserted a list of dictionaries where the keys represented column names and the values were the metrics I calculated. I formatted the DataFrame using the map() function so that dollar amounts had two decimal places, grade average values had one decimal place, and percentages had one decimal place. 
![image](https://user-images.githubusercontent.com/106560739/177844793-cd5863a2-6eb5-4c5a-8cc2-6937ca5f37dc.png)
![image](https://user-images.githubusercontent.com/106560739/177844848-8c2a35ee-3d84-4796-8af2-5f67bcc92ed7.png)
For the script written after signs of academic dishonesty were noted, I made several alterations to the orginal script. I first changed the original code by using the loc[] method with logical and comparison operators to retrieve the student count for Thomas High School ninth graders (named "ninth_count") in the "school_data_complete_df". I then subtracted the number of students I retrieved from the "student_count" to get the "new_total_student_count". I calculated math and reading passing percentages based on the "new_total_student_count". Then I calculated the overall passing percentage using the "new_total_student_count".
![image](https://user-images.githubusercontent.com/106560739/177845553-3dcb311c-be16-49cb-be22-e0b359b3111b.png)
![image](https://user-images.githubusercontent.com/106560739/177845580-fd08c896-6589-4a11-904b-309f516fe73e.png)
I used the new calculations to create a DataFrame, which I named "district_summary_df" and formatted it similar to the original one. 
![image](https://user-images.githubusercontent.com/106560739/177845851-917fe453-7175-4e25-864e-662a8dcb558d.png)
![image](https://user-images.githubusercontent.com/106560739/177845904-91500727-d417-46a0-9605-1356067a2515.png)
The school district summary is marginally affected by the updated changes to the dataset after Thomas High School 9th grade scores were removed and set to NaN's. The average math score in the original code was 79.0, whereas the average math scores in the script written due to academic dishonesty was 78.9. This thereby changed the percentage of students passing math in the district. In the original script, the percentage of students passing math was 75.0, whereas in the updated script the percentage was 74.8. Similar changes were seen in the average reading scores and percentage of students passing reading. The main discrepency lies in the percentage of overall passing students in the district. In the original script, the overall passing percentage was 65.2, whereas the updated script shows an overall passing percentage of 64.9. Overall, the district summary is not greatly affected by the changes made to the original code.
* _How is the school summary affected?_
To generate a summary for each school in the district, I needed to create a new DataFrame that would allow me to acquire statistics on unique schools. I utilized "school_data_df" because the "school_name" and "type" columns were both series. I set the index to the “school_name” column with the set_index() method, which returned “School Type” as the first column. I then created the new DataFrame by setting "df" equal to “pd.DataFrame(per_school_types)”. To calculate the number of students per school, I initialized a variable "per_school_counts" and used the "school_data_complete_df" to apply the value_counts() method. This counted the number of times a high school appeared on the “school_name” column. To find the budget per student for each school, I divided the budget for each school by the number of students at each school. I used the "school_data_df" to set the index to “school_name” and called on the “budget” column. I named these results "per_school_budget" and divided it by "per_school_counts" to get "per_school_capita". 
![determine school type](https://user-images.githubusercontent.com/106560739/177917957-c19982d6-e1f4-4365-acd1-6bb1f9679005.png)
For the original script, I initialized "per_school_math" and "per_school_reading" variables. I then utilized the Pandas groupby() function and the mean() method on the "school_data_complete_df" to get the grade averages for each column. I did ensure that the “math_score” and “reading_score” columns were applied at the end of their respective variables.
![image](https://user-images.githubusercontent.com/106560739/177847917-b41b331b-029a-470a-841b-f1e70355dace.png)
To get the number of students who passed math and reading at each school, I initialized "per_school_passing_math" and "per_school_passing_reading" variables. I first filtered the “math_score” column in the "school_data_complete_df" to greater than or equal to 70. However, I needed to index the data by "school_name" and thereby used the grouby([“school_name”]) on the "per_passing_math". Then I applied a mathematical operation, in this case the count() method, on the "student_name" column, which was within the groupby() object. I repurposed this code to generate results for the "per_school_passing_reading". To determine the percentage of students passing math and reading, I divided "per_school_passing_math" and "per_school_passing_reading" by the "per_school_counts", and then multiplied each one by 100.
![image](https://user-images.githubusercontent.com/106560739/177849334-b62d4197-2c02-4f0d-9d48-2bf735bca614.png)
To get the overall passing percentage for all students at each school, I first initialized a "per_passing_math_reading" variable and set the index to "school_name". I then used the count() method for the "student_name" to calculate the number of students who passed both exams. I calculated the overall percentage by dividing the "per_passing_math_reading" by "per_school_counts" and then multiplying it by 100. 
![image](https://user-images.githubusercontent.com/106560739/177849921-a81d0010-61f8-4dd7-826c-8e18c68408f8.png)
I then created a "per_school_summary_df" using the pd.DataFrame() operator and inserted a list of dictionaries where the keys were column names and the values represented the metrics I calculated. I formatted the DataFrame using the map() function so that the “Total School Budget” and “Per Student Budget” columns had a dollar sign, two decimal places, and a thousands separator. 
![image](https://user-images.githubusercontent.com/106560739/177850192-81e4cfa0-1061-4d6e-8e6d-ecd6a05c49be.png)
![image](https://user-images.githubusercontent.com/106560739/177850215-0dd5dc21-f216-4b45-b712-9bd7b013b24d.png)
![image](https://user-images.githubusercontent.com/106560739/177850244-5a280e68-85d0-4a5d-9009-0fe89752d993.png)
For the script written after signs of academic dishonesty were noted, I made several alterations to the original script. I first initialized a variable "ten_twelve_count" and used the loc[] method and count() operator on the "student_data_df" to get the number of 10th-12th graders at Thomas High School. For this, I made sure to set the "school_name" in the "student_data_df" to "Thomas High School" and the "grade" column not equal to "9th". I similarly used the loc[] method and count() operator on the "student_data_df" to create a new DataFrame that held the total number of students passing math (named "passing_math") and the total number of students passing reading (named "passing_reading") from Thomas High School. I also utilized the loc[] method and count() operator to create a new DataFrame that held all the students who passed both math and reading exams (named "passing_math_reading") from Thomas High School. I then calculated the percentage of 10th-12th grade students passing math from Thomas High School using the loc[] method and count() operator on the "student_data_df". For this, I made sure to set the "school_name" to "Thomas High School", the "grade" column not equal to "9th", and divide the equation by the "ten_twelve_count". I repurposed the code to calculate the percentage of 10th-12th grade students passing reading from Thomas High School. Next, I calculated the overall passing percentage of 10th-12th grade students (named ten_twelve_overall_passing_percentage") from Thomas High School. For this, I made sure to set the "school_name" to "Thomas High School", the "grade" column not equal to "9th", and divide the equation by the "ten_twelve_count".I then utilized the loc[] method to replace the “% Passing Math” score for Thomas High School with the "ten_twelve_passing_math_percentage". I also used the loc[] method to replace the “% Passing Reading” score for Thomas High School with the "ten_twelve_passing_reading_percentage". I utilized the loc[] method once again to replace the “% Overall Passing” score for Thomas High School with the "ten_twelve_overall_passing_percentage".
![image](https://user-images.githubusercontent.com/106560739/177856833-bf8fd7bc-b5fd-4652-9c22-328824cd9e99.png)
![image](https://user-images.githubusercontent.com/106560739/177856863-4eab695b-f2ed-4c7c-a8c0-aab9580eae5d.png)
I used the new calculations to create a DataFrame, which I named "per_school_summary_df" and formatted it similar to the original one. 
![image](https://user-images.githubusercontent.com/106560739/177857045-95232d35-656c-4a19-b060-16704c8796bc.png)
![image](https://user-images.githubusercontent.com/106560739/177857071-f1bc19fb-465d-4a27-a997-bfb1ad948f7e.png)
![image](https://user-images.githubusercontent.com/106560739/177857096-f1081c6b-cb76-4ca6-a625-ee33ba558ea1.png)
The school summary is slighlty affected by the updated changes to the dataset after Thomas High School 9th grade scores were removed and set to NaN's. The school summary remained the same for other schools within the district. The only changes observed were with Thomas High School testing scores. In the original script, the average math score was 83.418349, whereas in the updated code the score was 83.350937. This in turn led to slight decimal point changes between the original and updated code regarding the percentage of students passing math at Thomas High School. In the original code, the average reading score was 83.848930, whereas in the new script there was an average reading score of 83.896082. This similarly led to small changes between the original and updated script regarding the percentage of students passing reading at Thomas High School. The percentage of overall students passing both math and reading at Thomas High School also experienced slight decimal point changes between the original and updated script. The original had an overall passing percentage of 90.948012 while the updated was 90.630324. Therefore, the school summary was only marginally affected by altering the original code. 
* _How does replacing the ninth graders’ math and reading scores affect Thomas High School’s performance relative to the other schools?_
For the original script, I determined which schools were the highest performing based on the overall percentage of passing students by sorting the "per_school_summary_df" on the “% Overall Passing” column. I used the Pandas sort_values() function and set ascending to False to generate the highest to lowest overall passing percentage. To find the lowest performing schools, I reused this code but set ascending to True.
![image](https://user-images.githubusercontent.com/106560739/177857306-6cb7078a-b5be-410c-9e79-f155aca78070.png)
![image](https://user-images.githubusercontent.com/106560739/177857323-a8fbddbb-372a-44aa-8114-b2bfd05116e8.png)
For the script written after signs of academic dishonesty were noted, I utilized the same code structure as the original script to determine the top 5 and bottom 5 performing schools.
![image](https://user-images.githubusercontent.com/106560739/177857483-6ac7966a-44cf-4679-acf9-967efae90025.png)
![image](https://user-images.githubusercontent.com/106560739/177857509-64a08f26-0bbd-4bcf-871e-e25356bdfbd4.png)
Replacing the ninth graders’ math and reading scores did not affect Thomas High School’s performance relative to the other schools. Schools were ranked based on their average math scores, reading scores, percentage of students passing math, percentage of students passing reading, and the overall passing percentage. In both the original and updated script, Thomas High School ranked second in the district. The top ranking school was Cabrera High School and the bottom ranking school was Rodriguez High School.
* _How does replacing the ninth-grade scores affect the following:_
  * _Math and reading scores by grade:_ Prior to the analysis of math and reading scores by grade, I needed to create a grade-level DataFrame that was grouped by the name of the school. To get each grade as a series, I filtered "school_data_complete_df". I initialized a variable, “ninth_graders”, and set it equal to “school_data_complete_df["grade"] == "9th"”. I then repurposed this code by replacing “9th” with each grade. I made sure to assign a grade-level variable to each grade-level series. To get the average math scores for each grade level, I used the groupby() function on the “school_name” column and applied the mean() on the “math_score” column. For this code, the index was the “school_name”. I repurposed this code to find the average reading scores for each grade level by replacing “math_score” with “reading_score”. Once I performed these calculations, I then combined each grade level series for average math scores by school into a single DataFrame, which I named "math_scores_by_grade", using the pd.DataFrame() operator. I repurposed this same code to add the reading scores for each grade level to a new DataFrame, which I named "reading_scores_by_grade".
![image](https://user-images.githubusercontent.com/106560739/177858297-c7465911-d39b-4ea0-b4a1-39f04941e4fb.png)
![image](https://user-images.githubusercontent.com/106560739/177858328-c74a9b50-1fa9-4143-b9d5-b354841b0624.png)
For reporting purposes, I formatted the grade-level averages for both math and reading to one decimal place and removed the name of the index column, “school_name” using the map() function. 
![image](https://user-images.githubusercontent.com/106560739/177858423-6c206e99-cf10-4bee-9a16-5d891848fc92.png)
![image](https://user-images.githubusercontent.com/106560739/177858450-d18a4b1b-2b35-47c8-b946-c7f3e5ac7bee.png)
![image](https://user-images.githubusercontent.com/106560739/177858488-f2f14ec0-6911-4b3b-b24e-88f46c15a5cd.png)
![ths module reading](https://user-images.githubusercontent.com/106560739/177916876-e7b7f663-ebe9-45e8-91a2-c22b914521d6.png)
For the script written after signs of academic dishonesty were noted, I utilized the same code structure as the original script to determine the average math and reading score for all grade levels from each school. The average math scores for all grade levels from each school are as follows.
![math challenge](https://user-images.githubusercontent.com/106560739/177917028-2fc3e9f6-b829-4adb-90be-c374229c85bf.png)
The average reading scores for all grade levels from each school are as follows.
![reading challenge](https://user-images.githubusercontent.com/106560739/177917046-f81feb05-8285-4ee8-9ebb-8349010cb0d9.png)
The math and reading scores by grade were greatly affected when the ninth grade scores for Thomas High School were replaced with NaN's. In the original script, Thomas High School had math score values for all grade levels. However, when the script was updated, Thomas High School no longer had math score values for 9th graders but instead had a NaN. The same trend was observed in Thomas High School reading score values. In the original script, Thomas High School had reading score values for all grade levels. However, when the script was updated, Thomas High School no longer had reading score values for 9th graders but instead had a NaN. All other schools were not affected by updating the code. 
  * _Scores by school spending:_ 
Prior to the analysis of scores by school spending, I needed to sort the school spending per student into four spending bins, or ranges. To determine the bins to use, I used the describe() method on "per_school_capita". I found that the four bins were dollar amounts that ranged from the lowest amount ($578) to the highest amount ($655) a school spends on a student. Since the standard deviation was approximately 30, I increased the bins by $30 dollars. Therefore, the four bins were: $585, $630, $645, and $675. In Pandas, I wrote the ranges for the bins and grouped the spending ranges using the cut() function on the "per_school_capita". To determine how many schools were in each range, I used the count() method on the groupby() operator in relation to the "per_school_capita" series. I then named each range using a list of string values. After establishing the bin ranges, I created a new column in the "per_school_summary_df" and assigned the spending bins from the "per_school_capita" series. To do this I used the cut() function on the "per_school_capita" series and added the "spending_bins" and labels for the bins using “labels=group_names”. To see how school spending affected score averages and passing rates, I used the groupby() function on the "Spending Ranges (Per Student)" column. For each series, I used the mean() method to get the averages of the “Average Math Score” column, “Average Reading Score” column, “% Passing Math” column, and the  “% Passing Reading” column. For the average "% Overall Passing," I added the "% Passing Math" and "% Passing Reading" columns and then divided by 2. 
![image](https://user-images.githubusercontent.com/106560739/177859568-b04e3012-f9b6-4b3f-8344-66b9db53df05.png)
![image](https://user-images.githubusercontent.com/106560739/177859614-f1a6f668-5068-40f0-a3b4-fed3348113ae.png)
![image](https://user-images.githubusercontent.com/106560739/177859639-9817c3e1-be95-46a7-99cb-2194933a4507.png)
After obtaining these calculations, I added them to a new DataFrame, named "spending_summary_df", by using the pd.DataFrame() function. To ensure that the DataFrame adhered to grade-reporting standards, I formatted the average math and reading scores to one decimal place, formatted the passing percent for math and reading to a whole number, and formatted the overall passing percentage to a whole number. I utilized the map() method to format my calculations.
![image](https://user-images.githubusercontent.com/106560739/177859775-c9582ef7-d895-41c5-bde9-c0e4dd393b64.png)
![image](https://user-images.githubusercontent.com/106560739/177859799-efcb403c-1e98-49ff-bdf0-c974a83a444f.png)
For the script written after signs of academic dishonesty were noted, I utilized the same code structure as the original script to determine the average scores and passing percentages based on school spending. The results are as follows. 
![image](https://user-images.githubusercontent.com/106560739/177859860-acde541c-2c72-4e76-89ba-7e8259b4bbdb.png)
The scores by school spending were not affected by removing Thomas High School 9th grade scores and setting them to NaN's. All values remained the same in both the original and updated script.
  * _Scores by school size:_ 
Prior to the analysis of scores by school size, I needed to create three bins: small, medium, and large. To determine these bins, I looked at the "per_school_counts", or total students from each school, in the "per_school_summary_df". Since the highest student population was 4,976, the upper edge was set to 5,000. I grouped small schools as having fewer than 1,000 students, medium schools as having 1,000 to 1,999 students, and large schools as having 2,000-5,000 students. After I established the bins and group names, I created a new column in the "per_school_summary_df" where I grouped the school sizes. I used the cut() function on the "per_school_summary_df" column “Total Students” and grouped the student size in the "size_bins" and added “labels=group_names”. Upon grouping the schools based on size, I used the groupby() function on the “School Size” column. The data for each column was calculated by using the mean() method, which retrieved the averages of the following columns: “Average Math Score”, “Average Reading Score”, “% Passing Math”, and “% Passing Reading”. For the average "% Overall Passing," I added the “% Passing Math” and “% Passing Reading” columns, and then divided it by 2. 
![image](https://user-images.githubusercontent.com/106560739/177860796-a6e7c071-a540-43e0-b09d-2d55dd1529d1.png)
![image](https://user-images.githubusercontent.com/106560739/177860841-29043204-e7d3-4d3e-bfd3-66ebdb019487.png)
I then assembled my calculations into a DataFrame, named "size_summary_df", using the pd.DataFrame() function. I also ensured that I applied proper formatting to the average math and reading scores, the percentage of students passing math and reading, and the overall passing percentage. To format these calculations, I utilized the map() operator. 
![image](https://user-images.githubusercontent.com/106560739/177861078-9ec0f757-4224-4e65-9f9e-9ed20a522d94.png)
![image](https://user-images.githubusercontent.com/106560739/177861111-c6031556-ee9e-49b3-91e9-637e1f5b4fc0.png)
For the script written after signs of academic dishonesty were noted, I utilized the same code structure as the original script to determine the average scores and passing percentages based on school size. The results are as follows.
![image](https://user-images.githubusercontent.com/106560739/177861170-727286c2-e7f9-4e11-a1cb-e59ace66636d.png)
The scores by school size were not affected by removing Thomas High School 9th grade scores and setting them to NaN's. All values remained the same in both the original and updated script.
  * _Scores by school type_ To analyze scores by school type, I determined which schools were district or charter. I used the groupby() function to group the data on the “School Type” and used the mean() method to get the averages for the following columns: “Average Math Score”, “Average Reading Score”, “% Passing Math”, and “% Passing Reading”. For the average "% Overall Passing," I added the “% Passing Math” and “% Passing Reading” columns, and then divided it by 2. 
![image](https://user-images.githubusercontent.com/106560739/177861400-b179e9f3-8f57-47ee-a157-b07431da855a.png)
I then assembled my calculations in a new DataFrame, named "type_summary_df" using the pd.DataFrame() operator. This DataFrame needed to adhere to reporting standards and so I used the map() function to format the average math and reading scores to one decimal place, the percentage of students passing math and reading to a whole number, and the overall passing percentage to a whole number. 
![image](https://user-images.githubusercontent.com/106560739/177861492-18e17ce2-1384-4ee1-81b4-9e5ddcf3b3ce.png)
![image](https://user-images.githubusercontent.com/106560739/177861512-7f423bd8-8598-4a6a-a55e-b732bfab2108.png)
For the script written after signs of academic dishonesty were noted, I utilized the same code structure as the original script to determine the average scores and passing percentages based on school type. The results are as follows.
![image](https://user-images.githubusercontent.com/106560739/177861570-ecb6d3c1-2192-4e36-8d35-ca09f610816b.png)
The scores by school type were not affected by removing Thomas High School 9th grade scores and setting them to NaN's. All values remained the same in both the original and updated script.
## Summary
### Changes Observed
There were four changes observed in the school district analysis after reading and math scores for the ninth grade at Thomas High School were replaced with NaN's. Firstly, the school district summary DataFrame was affected marginally. In the original code, the average math score was 79.0; however, in the updated script the average math score was 78.9. This updated average caused changes to be observed in the percentage of students passing math in the district. In the original script, the percentage of students passing math was 75.0, whereas in the updated script the percentage was 74.8. Similar changes were observed in the average reading scores and percentage of students passing reading. Furthermore, the overall passing percentage of the original sciprt differed slighlty from the overall passing percentage of the updated script. In the original script, the overall passing percentage was 65.2, whereas the updated script shows an overall passing percentage of 64.9. Secondly, the school summary DataFrame was also affected slightly by the changes made to the original script. When Thomas High School 9th grade scores were removed and set to NaN's, the metrics for the school altered. In the original script, the average math score was 83.418349, whereas in the updated code the score was 83.350937. This caused decimal point changes between the values outputted by the original and updated code regarding the percentage of students passing math at Thomas High School. Furthermore, in the original code, the average reading score was 83.848930, whereas in the new script there was an average reading score of 83.896082. This similarly led to small changes between the original and updated script regarding the percentage of students passing reading at Thomas High School. The percentage of overall students passing both math and reading at Thomas High School also experienced slight decimal point changes between the original and updated script. The original had an overall passing percentage of 90.948012 while the updated was 90.630324. Thirdly, the math scores by grade DataFrame was greatly affected when the ninth grade scores for Thomas High School were replaced with NaN's. In the original script, Thomas High School had math score values for all grade levels. However, when the script was updated, Thomas High School no longer had math score values for 9th graders but instead had a NaN. Fourthly, the reading scores by grade were greatly affected when the ninth grade scores for Thomas High School were replaced with NaN's. In the original script, Thomas High School had reading score values for all grade levels. However, when the script was updated, Thomas High School no longer had reading score values for 9th graders but instead had a NaN.
