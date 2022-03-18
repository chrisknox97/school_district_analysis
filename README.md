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
    
    -----------------------------------------------------------------------------------------------------------------------------

    Get the Total "Student_Count"

    student_count = school_data_complete_df["Student ID"].count()
    
    -----------------------------------------------------------------------------------------------------------------------------
    
    Subtract the "Dropped_Score_Count" from the "Student Count"

    new_count = student_count - dropped_score_count

* **District Summary**



      district_summary_df = pd.DataFrame(
        [{"Total Schools": school_count, 
        "Total Students": new_count, 
        "Total Budget": total_budget,
        "Average Math Score": average_math_score, 
        "Average Reading Score": average_reading_score,
        "% Passing Math": new_passing_math_percentage,
        "% Passing Reading": new_passing_reading_percentage,
        "% Overall Passing": new_passing_overall_percentage}])

