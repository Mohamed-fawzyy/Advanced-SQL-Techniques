# Project Scenario 🎩
You have to analyze the following datasets for the city of Chicago, as available on the Chicago City data portal.
* Socioeconomic indicators in Chicago
* Chicago public schools
* Chicago crime data

Based on the information available in the different tables, you have to run specific queries using Advanced SQL techniques that generate the required result sets.

# Objectives📝
* After completing this project, you will be able to:
  * Use joins to query data from multiple tables
  * Create and query views
  * Write and run stored procedures
  * Use transactions

# Reach/Follow me on 🚀<br>
<p align="left">
  <a href="https://www.linkedin.com/in/mohamed-fawzy-936b661b8/" target="_blank" rel="noreferrer"> <img src="https://img.icons8.com/fluency/2x/linkedin.png" alt="linkedIn" width="50" height="50"/> </a>&nbsp&nbsp
  <a href="mailto:fwzymohamed90@gmail.com" target="_blank" rel="noreferrer"> <img src="https://img.icons8.com/fluency/2x/google-logo.png" alt="googleEmail" width="50" height="50"/> </a>&nbsp&nbsp
  <a href="https://www.facebook.com/mohamed.fwzy.14" target="_blank" rel="noreferrer"> <img src="https://cdn.iconscout.com/icon/free/png-256/facebook-262-721949.png" alt="facebook" width="50" height="50"/> </a>
</p>
<br>

# Prepare the lab environment 📦
* In this lab, you will use MySQL.
* <b> Database Used in this Lab</b>

<!-- Side Note: Additional Information -->
> Note: Here you will be creating and inserting data into the below mentioned 3 tables

* Here you will be using 3 dump files for this purpose. <br>

[chicago_public_schools](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork/labs/MySQL/week5/chicago_public_schools.sql)


[chicago_socioeconomic_data](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork/labs/MySQL/week5/chicago_crime.sql)


[chicago_crime](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-DB0201EN-SkillsNetwork/labs/MySQL/week5/chicago_socioeconomic_data.sql)

1. create a new empty database `Mysql_Learners`
2. Load the dump files one by one into the database `Mysql_learners` by clicking the Import tab and choose the file.

### Task 1 - Write and execute a SQL query to list the school names, community names and average attendance for communities with a hardship index of 98.
<img width="1103" alt="Exercise_1_Q1" src="https://github.com/Mohamed-fawzyy/Advanced-SQL-Techniques/assets/111665714/aa7535b6-32be-44d8-a392-4b99235dfba2">

### Task 2 - Write and execute a SQL query to list all crimes that took place at a school. Include case number, crime type and community name.
<img width="1078" alt="Exercise_1_Q2" src="https://github.com/Mohamed-fawzyy/Advanced-SQL-Techniques/assets/111665714/619a627d-b2c5-4d88-94b4-f537365cbcc2">

### Task 3 - Creating a View
1. Write and execute a SQL statement to create a view showing the columns listed in the following table, with new column names as shown in the second column.

|       Column name in <br> CHICAGO_PUBLIC_SCHOOLS    | 🔰 Column name in <br> view  
| --------------------------                          | :----------------:| 
| NAME_OF_SCHOOL	                          |              School_Name
| Safety_Icon	                             |              Safety_Rating
| Family_Involvement_Icon	                 |              Family_Rating
| Environment_Icon	                        |              Environment_Rating
| Instruction_Icon	                        |              Instruction_Rating
| Leaders_Icon	                            |              Leaders_Rating
| Teachers_Icon	                           |              Teachers_Rating

2. Write and execute a SQL statement that returns all of the columns from the view.
3.Write and execute a SQL statement that returns just the school name and leaders rating from the view.
```sql
CREATE VIEW PRIVATE_VIEW (School_Name, Safety_Rating, Family_Rating, Environment _Rating, Instruction_Rating, Leaders_Rating, Teachers _Rating)
AS SELECT NAME_OF_SCHOOL, Safety_Icon, Family_Involvement_Icon, Environment_Icon, Instruction_Icon, Leaders_Icon, Teachers_Icon
FROM CHICAGO_PUBLIC_SCHOOLS;

SELECT * FROM PRIVATE_ VIEW;
SELECT SCHOOL_NAME, Leaders_Rating FROM PRIVATE_VIEW
```

### Task 4 - Write the structure of a query to create or replace a stored procedure called UPDATE_LEADERS_SCORE that takes a in_School_ID parameter as an integer and a in_Leader_Score parameter as an integer.

```sql
--#SET TERMINATOR 0
CREATE OR REPLACE PROCEDURE
UPDATE LEADERS SCORE (IN in School ID INTEGER, IN in Leader Score INTEGER)
LANGUAGE SOL
BEGIN
END@
```

### Task 5 - Inside your stored procedure, write a SQL statement to update the Leaders_Score field in the CHICAGO_PUBLIC_SCHOOLS table for the school identified by in_School_ID to the value in the in_Leader_Score parameter.

```sql
CREATE OR REPLACE PROCEDURE
UPDATE_LEADERS_SCORE (IN in_School_ID INTEGER, IN in_Leader_Score INTEGER)
LANGUAGE SOL
BEGIN
UPDATE CHICAGO PUBLIC SCHOOLS
SET "Leaders Score" = in Leader Score
WHERE "School_ID" = in_School_ID;
END@
```

### Task 6 - Inside your stored procedure, write a SQL IF statement to update the Leaders_Icon field in the CHICAGO_PUBLIC_SCHOOLS table for the school identified by in_School_ID using the following information.



|       Score lower limit	    | Score upper limit |      Icon        |
| --------------------------  | ------------------| ----------------| 
|  80	                        |      99	          |        Very strong |
|  60	                        |      79	          |        Strong |
|  40	                        |      59	          |        Average |
|  20	                        |      39	          |        Weak |
|  0	                         |      19	          |        Very weak |

```sql
IF in Leader Score >
© AND in_Leader_Score < 20 THEN
UPDATE chicago_public_schools
SET Safety_Icon
= 'VERY WEEK
WHERE in School ID = in School ID:
ELSEIF in Leader Score
< 40 THEN
UPDATE chicago_public_schools
SET Safety_Icon
'WEEK
WHERE in School ID = in School ID;
ELSEIF in Leader Score
< 60 THEN
UPDATE chicago_public_schools
SET Safety_Icon = 'AVERAGE'
WHERE in School ID = in School ID;
ELSEIF in Leader Score
< 80 THEN
UPDATE chicago_public_schools
SET Safety_Icon
'STRONG'
WHERE in School ID = in School ID:
ELSEIF in Leader Score
< 100 THEN
UPDATE chicago_public_schools
SET Safety_Icon =
'VERY STRONG'
WHERE in School ID = in School ID;
```

### Task 7 - Write a query to call the stored procedure, passing a valid school ID and a leader score of 50, to check that the procedure works as expected.
* Run your code to create the stored procedure.
```sql
CREATE OR REPLACE PROCEDURE UPDATE_LEADERS_SCORE (IN in_School_ID INTEGER, IN in_Leader_Score INTEGER)
LANGUAGE SQL
BEGIN
UPDATE CHICAGO_ PUBLIC_SCHOOLS
SET "Leaders_Score" = in_Leader_Score
WHERE "School_ID" = in_School_ID;

IF in_Leader_Score > 0 AND in_Leader_Score <20 THEN
    UPDATE CHICAGO_PUBLIC_SCHOOLS
    SET "Leaders icon" = 'Very weak';

ELSEIF in Leader Score < 40 THEN
    UPDATE CHICAGO_PUBLIC_SCHOOLS
    SET "Leaders icon" = 'Weak';

ELSEIF in Leader Score < 60 THEN
    UPDATE CHICAGO_PUBLIC SCHOOLS
    SET "Leaders_icon" = 'Average';

ELSEIF in Leader Score < 80 THEN
    UPDATE CHICAGO_PUBLIC_SCHOOLS
    SET "Leaders_icon" = 'Strong';

ELSEIF in Leader Score < 100 THEN
    UPDATE CHICAGO_PUBLIC_SCHOOLS
    SET "Leaders_icon" = 'Very Strong';
END IF;
END@
```

### Task 8 - Update your stored procedure definition. Add a generic ELSE clause to the IF statement that rolls back the current work if the score did not fit any of the preceding categories.

```sql
ELSE
   ROLLBACK;
-- UPDATE chicago_public_schools
-- SET Safety_Icon = Safety_Icon
-- WHERE in_School_ID = School_ID:
END IF:
END@
```

### Task 9 - Update your stored procedure definition again. Add a statement to commit the current unit of work at the end of the procedure.

```sql
END IF:
COMMIT:
END
@
```

# Contributing 📝
Contributions are welcome! Please open an issue or pull request for any changes or improvements.














