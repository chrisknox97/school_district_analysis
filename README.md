# PyCitySchools with Pandas

## Overview of School District Analysis 

After a local school board discovered irregularities in reading and math scores for ninth graders at Thomas High School; we must conduct an analysis using ``Pandas`` to uncover academic dishonesty for the sake of state-testing standards. 
  
## School District Analysis Results

* **Removing Dishonest Data**

To better represent the local school board's testing data, we first calculated the number of students in Thomas High School's ninth grade (the source of our acadmic dishonesty suspicons) and remove them from them from the total ``student_count``. The result removed test scores from 461 students to get a new count of 38,709 students. These calculations were performed by the following script: 

    # Specify "Thomas High School" from "School_Name" and "9th" Graders from "Grade
    
    dropped_scores = student_data_df.loc[(student_data_df["school_name"] == "Thomas High School") & 
    (student_data_df["grade"] == "9th")]

    dropped_score_count = dropped_scores["student_name"].count()
    
    --------------------------------------------------------------------------------------------------------------------------------------

    # Get the Total "Student_Count"

    student_count = school_data_complete_df["Student ID"].count()
    
    --------------------------------------------------------------------------------------------------------------------------------------
    
    # Subtract the "Dropped_Score_Count" from the "Student Count"

    new_count = student_count - dropped_score_count

* **District Summary**

Once we've established our ``new_count``, we are abble to calculate the new percentages of students passing math, reading, and both subjects by subtituting ``total_count`` with ``new_count``in the following scripts: 

    # New Student Count Passing Reading
    new_passing_reading_percentage = passing_reading_count / float(new_count) *100
    
    # New Student Count Passing Math
    new_passing_math_percentage = passing_math_count / float(new_count) *100
  
    # New Student Count Passing Math & Reading
    new_passing_overall_percentage = overall_passing_math_reading_count / float(new_count) *100

With these new scripts, we are able to assemble a new data frame and compare it against the previous data frame. As this removed only 461 students from a data set of 38,701; the overall district test scores' declines were relatively minimal, never exceeding 0.3%. 

    Prior to Removal of Academic Dishonesty

![Dishonest_District](https://github.com/chrisknox97/school_district_analysis/blob/main/Resources/Dishonest_District.png)

    After Removal of Academic Dishonesty

![Revised_District](https://github.com/chrisknox97/school_district_analysis/blob/main/Resources/Revised_District.png)

**Please Note:** The ``new_count`` was added to this data frame for clarity, showing which data frame removed the dishonest students' test results. However in the future, we would continue to the old ``student_count`` as altering the total student data could affect calculations such as ``per_capita_spending``. 

* **School Summary**

For our school summary, we had to tabulate the new counts of: "Thomas High School" students in grades 10-12, "Thomas High School" students in grades 10-12 who passed their math test, "Thomas High School" students in grades 10-12 who passed their history test, and "Thomas High School" students in grades 10-12 who passed overall. The script to tabulate these new counts in listed below. 

    # Calculate The Number of Students in Grades 10-12 at "Thomas High School"

    thomas_tenth_graders = student_data_df.loc[(student_data_df["school_name"] == "Thomas High School") & 
    (student_data_df["grade"] == "10th")]
    thomas_eleventh_graders = student_data_df.loc[(student_data_df["school_name"] == "Thomas High School") &
    (student_data_df["grade"] == "11th")]
    thomas_twelfth_graders = student_data_df.loc[(student_data_df["school_name"] == "Thomas High School") & 
    (student_data_df["grade"] == "12th")]

    clean_thomas_score_count = thomas_tenth_graders["student_name"].count() + thomas_eleventh_graders["student_name"].count() +                   
    thomas_twelfth_graders["student_name"].count()
 
--------------------------------------------------------------------------------------------------------------------------------------

    # Calculate the Total Number of "Thomas High School" Students Who Passed Math

    thomas_passing_math_count = school_data_complete_df[(school_data_complete_df["school_name"] == "Thomas High School") &      
    (school_data_complete_df["math_score"] >= 70)].count()["student_name"]
    
    # Calculate the Total Number of "Thomas High School" Students Who Passed Reading

    thomas_passing_reading_count = school_data_complete_df[(school_data_complete_df["school_name"] == "Thomas High School") &  
    (school_data_complete_df["reading_score"] >= 70)].count()["student_name"]
    
    # Calculate the Total Number of "Thomas High School" Students Who Passed Overall

    thomas_passing_math_reading = school_data_complete_df[(school_data_complete_df["school_name"] == "Thomas High School") & 
    (school_data_complete_df["math_score"] >= 70) & (school_data_complete_df["reading_score"] >= 70)].count()["student_name"]

From here, the new counts can be used to calculate new percentages of students passing each respective subject; as well as subsituted these new variables into the ``per_school_summary`` data frame. The result is the following code: 
   
    # Calculate the Percentage of "Thomas High School" Students Who Passed Math
    clean_thomas_percentage_math = thomas_passing_math_count / float(clean_thomas_score_count) * 100

    # Calculate the Percentage of "Thomas High School" Students Who Passed Reading
    clean_thomas_percentage_reading = thomas_passing_reading_count / float(clean_thomas_score_count) * 100
    
    # Calculate the Percentage of "Thomas High School" Students Who Passed Overall
    clean_thomas_percentage = thomas_passing_math_reading / float(clean_thomas_score_count) * 100
    
    --------------------------------------------------------------------------------------------------------------------------------------
    
    # Substitute the Old Passing Math Percentage with An Updated One
    per_school_summary_df.loc[["Thomas High School"],["% Passing Math"]] = clean_thomas_percentage_math
    
    # Substitute the Old Passing Reading Percentage with An Updated One
    per_school_summary_df.loc[["Thomas High School"], ["% Passing Reading"]] = clean_thomas_percentage_reading
    
    # Substitute the Old Overall Passing Percentage with An Updated One
    per_school_summary_df.loc[["Thomas High School"], ["% Overall Passing"]] = clean_thomas_percentage
    
With these new calculations all three percentages tracked, ``per_school_passing_math``, ``per_school_passing_reading``, and ``per_overall_passing_percent`` all declined, with the later decreasing by approximately 0.3%. This drop was relatively similar to the one seen in ``new_overall_passing_percentage`` in our ``district_summary``. 
    
    Prior to Removal of Academic Dishonesty
    
![Dishonest_School](https://github.com/chrisknox97/school_district_analysis/blob/main/Resources/Dishonest_School.png) =250x250

    After Removal of Academic Dishonesty

![Revised_School](https://github.com/chrisknox97/school_district_analysis/blob/main/Resources/Revised_School.png)

* **Thomas High School Vs. Comparative High Schools**

After removing the academically dishonest test scores, we were concerned about how their new results would affect "Thomas High School"'s standing within the school district. Yet any worries were ultimately laid to rest when the high school retained its second-best ranking. The minimal declines can be seen below. 

    Prior to Removal of Academic Dishonesty
    
![Dishonest_Top5](https://github.com/chrisknox97/school_district_analysis/blob/main/Resources/Dishonest_Top5.png)

    After Removal of Academic Dishonesty
   
![Dishonest_Top5](https://github.com/chrisknox97/school_district_analysis/blob/main/Resources/Revised_Top5.png)

* **Thomas High School Student Grades**

Finally, we were also concerned about how the removal of the academically dishonest test scores would affect other parameters including: math and reading scores, scores by school spending, scores by school size, and scores by school type.
    
   * **Test Scores**
    
    Prior to Removal of Academic Dishonesty

![Dishonest_Math Scores](https://github.com/chrisknox97/school_district_analysis/blob/main/Resources/Dishonest_Math.png)
![Dishonest_Reading Scores](https://github.com/chrisknox97/school_district_analysis/blob/main/Resources/Dishonest_Reading.png)

    After Removal of Academic Dishonesty
    
![Revised_Math Scores](https://github.com/chrisknox97/school_district_analysis/blob/main/Resources/Revised_Math.png)
![Revised_Reading Scores](https://github.com/chrisknox97/school_district_analysis/blob/main/Resources/Revised_Reading.png)

hskdhs



 
     
     

     
    


    

   

