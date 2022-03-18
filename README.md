# PyCitySchools with Pandas

## Overview of School District Analysis 

After a local school board discovered irregularities in reading and math scores for ninth graders at Thomas High School; we must conduct an analysis using ``Pandas`` to uncover academic dishonesty for the sake of state-testing standards. 
  
## School District Analysis Results

* **Removing Dishonest Data**

To better represent the local school board's testing data, we first calculated the number of students in Thomas High School's ninth grade (the source of our acadmic dishonesty suspicons) and remove them from them from the total ``student_count``. The result removed test scores from 461 students to get a new count of 38,709 students. These calculations were performed by the following script: 

    Specify "Thomas High School" from "School_Name" and "9th" Graders from "Grade
    
    dropped_scores = student_data_df.loc[(student_data_df["school_name"] == "Thomas High School") & 
    (student_data_df["grade"] == "9th")]

    dropped_score_count = dropped_scores["student_name"].count()
    
    --------------------------------------------------------------------------------------------------------------------------------------------------------------

    Get the Total "Student_Count"

    student_count = school_data_complete_df["Student ID"].count()
    
    --------------------------------------------------------------------------------------------------------------------------------------------------------------
    
    Subtract the "Dropped_Score_Count" from the "Student Count"

    new_count = student_count - dropped_score_count

* **District Summary**

Once we've established our ``new_count``, we are abble to calculate the new percentages of students passing math, reading, and both subjects by subtituting ``total_count`` with ``new_count``in the following scripts: 

    New Student Count Passing Reading
    new_passing_reading_percentage = passing_reading_count / float(new_count) *100
    
    New Student Count Passing Math
    new_passing_math_percentage = passing_math_count / float(new_count) *100
  
    New Student Count Passing Math & Reading
    new_passing_overall_percentage = overall_passing_math_reading_count / float(new_count) *100

With these new scripts, we are able to assemble a new data frame and compare it against the previous data frame. As this removed only 461 students from a data set of 38,701; the overall district test scores' declines were relatively minimal, never exceeding 0.3%. 

    Prior to Removal of Academic Dishonesty

![Dishonest_District](https://github.com/chrisknox97/school_district_analysis/blob/main/Resources/Dishonest_District.png)

    After Removal of Academic Dishonesty

![Revised_District](https://github.com/chrisknox97/school_district_analysis/blob/main/Resources/Revised_District.png)
    

   

