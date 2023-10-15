Business Intelligence Project
================
<Champions>
\<15/10/2023\>

- [Student Details](#student-details)
- [Setup Chunk](#setup-chunk)
- [Understanding the Dataset (Explanatory Data Analysis
  (EDA))](#understanding-the-dataset-explanatory-data-analysis-eda)
  - [Loading the Dataset](#loading-the-dataset)
    - [Source:](#source)
    - [Reference:](#reference)
- [Applying the Center Data
  Transform](#applying-the-center-data-transform)
- [Normalized the Dataset ensuring the numerical values between 0 and
  1](#normalized-the-dataset-ensuring-the-numerical-values-between-0-and-1)
- [Applying the Box Cox Data
  Transform](#applying-the-box-cox-data-transform)

# Student Details

|                                              |                  |
|----------------------------------------------|------------------|
| **Student ID Number**                        | 126761           |
|                                              | 134111           |
|                                              | 133996           |
|                                              | 127707           |
|                                              | 135859           |
| **Student Name**                             | Virginia Wanjiru |
|                                              | Immaculate Haayo |
|                                              | Trevor Ngugi     |
|                                              | Clarice Muthoni  |
|                                              | Pauline Wairimu  |
| **BBIT 4.2 Group**                           | B                |
| **BI Project Group Name/ID (if applicable)** | Champions        |

# Setup Chunk

**Note:** the following KnitR options have been set as the global
defaults: <BR>
`knitr::opts_chunk$set(echo = TRUE, warning = FALSE, eval = TRUE, collapse = FALSE, tidy = TRUE)`.

More KnitR options are documented here
<https://bookdown.org/yihui/rmarkdown-cookbook/chunk-options.html> and
here <https://yihui.org/knitr/options/>.

# Understanding the Dataset (Explanatory Data Analysis (EDA))

## Loading the Dataset

### Source:

The dataset that was used can be downloaded here:
<https://drive.google.com/drive/folders/1-BGEhfOwquXF6KKXwcvrx7WuZXuqmW9q?usp=sharing>

### Reference:

*  
Refer to the APA 7th edition manual for rules on how to cite datasets:
<https://apastyle.apa.org/style-grammar-guidelines/references/examples/data-set-references>*

``` r
library(readr)
StudentPerformanceDataset <- read_csv("../markdown/StudentPerformanceDataset.csv")
```

    ## Rows: 101 Columns: 100
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr  (4): class_group, D - 1. Write two things you like about the teaching a...
    ## dbl (96): gender, YOB, regret_choosing_bi, drop_bi_now, motivator, read_cont...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

\# Applying the Scale Data Transform

``` r
# We use the "preProcess()" function in the caret package

### The Scale Basic Transform on the Student Performance Dataset ----
# BEFORE
class(StudentPerformanceDataset)
```

    ## [1] "spec_tbl_df" "tbl_df"      "tbl"         "data.frame"

``` r
summary(StudentPerformanceDataset)
```

    ##  class_group            gender            YOB       regret_choosing_bi
    ##  Length:101         Min.   :0.0000   Min.   :1998   Min.   :0.0000    
    ##  Class :character   1st Qu.:0.0000   1st Qu.:2000   1st Qu.:0.0000    
    ##  Mode  :character   Median :1.0000   Median :2001   Median :0.0000    
    ##                     Mean   :0.5743   Mean   :2001   Mean   :0.0198    
    ##                     3rd Qu.:1.0000   3rd Qu.:2002   3rd Qu.:0.0000    
    ##                     Max.   :1.0000   Max.   :2003   Max.   :1.0000    
    ##                                                                       
    ##   drop_bi_now       motivator      read_content_before_lecture
    ##  Min.   :0.0000   Min.   :0.0000   Min.   :1.000              
    ##  1st Qu.:0.0000   1st Qu.:1.0000   1st Qu.:2.000              
    ##  Median :0.0000   Median :1.0000   Median :3.000              
    ##  Mean   :0.0198   Mean   :0.7525   Mean   :2.752              
    ##  3rd Qu.:0.0000   3rd Qu.:1.0000   3rd Qu.:3.000              
    ##  Max.   :1.0000   Max.   :1.0000   Max.   :5.000              
    ##                                                               
    ##  anticipate_test_questions answer_rhetorical_questions find_terms_I_do_not_know
    ##  Min.   :1.000             Min.   :1.000               Min.   :1.000           
    ##  1st Qu.:3.000             1st Qu.:3.000               1st Qu.:3.000           
    ##  Median :4.000             Median :4.000               Median :4.000           
    ##  Mean   :3.584             Mean   :3.426               Mean   :3.743           
    ##  3rd Qu.:4.000             3rd Qu.:4.000               3rd Qu.:5.000           
    ##  Max.   :5.000             Max.   :5.000               Max.   :5.000           
    ##                                                                                
    ##  copy_new_terms_in_reading_notebook take_quizzes_and_use_results
    ##  Min.   :1.000                      Min.   :1.000               
    ##  1st Qu.:3.000                      1st Qu.:3.000               
    ##  Median :4.000                      Median :4.000               
    ##  Mean   :3.663                      Mean   :3.941               
    ##  3rd Qu.:4.000                      3rd Qu.:5.000               
    ##  Max.   :5.000                      Max.   :5.000               
    ##                                                                 
    ##  reorganise_course_outline write_down_important_points space_out_revision
    ##  Min.   :1.000             Min.   :1.000               Min.   :1.000     
    ##  1st Qu.:3.000             1st Qu.:3.000               1st Qu.:3.000     
    ##  Median :3.000             Median :4.000               Median :3.000     
    ##  Mean   :3.376             Mean   :3.832               Mean   :3.228     
    ##  3rd Qu.:4.000             3rd Qu.:5.000               3rd Qu.:4.000     
    ##  Max.   :5.000             Max.   :5.000               Max.   :5.000     
    ##                                                                          
    ##  studying_in_study_group schedule_appointments goal_oriented  
    ##  Min.   :1.000           Min.   :1.000         Min.   :0.000  
    ##  1st Qu.:1.000           1st Qu.:1.000         1st Qu.:0.000  
    ##  Median :2.000           Median :2.000         Median :0.000  
    ##  Mean   :2.455           Mean   :1.931         Mean   :0.198  
    ##  3rd Qu.:3.000           3rd Qu.:2.000         3rd Qu.:0.000  
    ##  Max.   :5.000           Max.   :5.000         Max.   :1.000  
    ##                                                               
    ##  spaced_repetition testing_and_active_recall  interleaving    categorizing  
    ##  Min.   :1.000     Min.   :1.000             Min.   :1.000   Min.   :1.000  
    ##  1st Qu.:2.000     1st Qu.:3.000             1st Qu.:2.000   1st Qu.:2.000  
    ##  Median :3.000     Median :3.000             Median :2.000   Median :3.000  
    ##  Mean   :2.554     Mean   :3.059             Mean   :2.257   Mean   :2.713  
    ##  3rd Qu.:3.000     3rd Qu.:4.000             3rd Qu.:3.000   3rd Qu.:3.000  
    ##  Max.   :4.000     Max.   :4.000             Max.   :4.000   Max.   :4.000  
    ##                                                                             
    ##  retrospective_timetable cornell_notes        sq3r          commute    
    ##  Min.   :1.000           Min.   :1.000   Min.   :1.000   Min.   :1.00  
    ##  1st Qu.:2.000           1st Qu.:2.000   1st Qu.:2.000   1st Qu.:2.00  
    ##  Median :2.000           Median :3.000   Median :3.000   Median :3.00  
    ##  Mean   :2.406           Mean   :2.545   Mean   :2.614   Mean   :2.73  
    ##  3rd Qu.:3.000           3rd Qu.:3.000   3rd Qu.:3.000   3rd Qu.:4.00  
    ##  Max.   :4.000           Max.   :4.000   Max.   :4.000   Max.   :4.00  
    ##                                                          NA's   :1     
    ##    study_time   repeats_since_Y1  paid_tuition   free_tuition  extra_curricular
    ##  Min.   :1.00   Min.   : 0.00    Min.   :0.00   Min.   :0.00   Min.   :0.00    
    ##  1st Qu.:1.00   1st Qu.: 0.00    1st Qu.:0.00   1st Qu.:0.00   1st Qu.:0.00    
    ##  Median :2.00   Median : 2.00    Median :0.00   Median :0.00   Median :1.00    
    ##  Mean   :1.75   Mean   : 2.05    Mean   :0.11   Mean   :0.27   Mean   :0.53    
    ##  3rd Qu.:2.00   3rd Qu.: 3.00    3rd Qu.:0.00   3rd Qu.:1.00   3rd Qu.:1.00    
    ##  Max.   :4.00   Max.   :10.00    Max.   :1.00   Max.   :1.00   Max.   :1.00    
    ##  NA's   :1      NA's   :1        NA's   :1      NA's   :1      NA's   :1       
    ##  sports_extra_curricular exercise_per_week    meditate         pray     
    ##  Min.   :0.00            Min.   :0.0       Min.   :0.00   Min.   :0.00  
    ##  1st Qu.:0.00            1st Qu.:1.0       1st Qu.:0.00   1st Qu.:1.00  
    ##  Median :0.00            Median :1.0       Median :1.00   Median :2.00  
    ##  Mean   :0.36            Mean   :1.1       Mean   :0.76   Mean   :2.09  
    ##  3rd Qu.:1.00            3rd Qu.:2.0       3rd Qu.:1.00   3rd Qu.:3.00  
    ##  Max.   :1.00            Max.   :3.0       Max.   :3.00   Max.   :3.00  
    ##  NA's   :1               NA's   :1         NA's   :1      NA's   :1     
    ##     internet        laptop  family_relationships  friendships  
    ##  Min.   :0.00   Min.   :1   Min.   :2.00         Min.   :2.00  
    ##  1st Qu.:1.00   1st Qu.:1   1st Qu.:4.00         1st Qu.:4.00  
    ##  Median :1.00   Median :1   Median :4.00         Median :4.00  
    ##  Mean   :0.87   Mean   :1   Mean   :4.19         Mean   :4.01  
    ##  3rd Qu.:1.00   3rd Qu.:1   3rd Qu.:5.00         3rd Qu.:4.00  
    ##  Max.   :1.00   Max.   :1   Max.   :5.00         Max.   :5.00  
    ##  NA's   :1      NA's   :1   NA's   :1            NA's   :1     
    ##  romantic_relationships spiritual_wellnes financial_wellness     health    
    ##  Min.   :0.00           Min.   :1.00      Min.   :1.00       Min.   :1.00  
    ##  1st Qu.:0.00           1st Qu.:3.00      1st Qu.:2.00       1st Qu.:3.00  
    ##  Median :0.00           Median :4.00      Median :3.00       Median :4.00  
    ##  Mean   :1.37           Mean   :3.65      Mean   :3.03       Mean   :4.04  
    ##  3rd Qu.:3.00           3rd Qu.:4.00      3rd Qu.:4.00       3rd Qu.:5.00  
    ##  Max.   :4.00           Max.   :5.00      Max.   :5.00       Max.   :5.00  
    ##  NA's   :1              NA's   :1         NA's   :1          NA's   :1     
    ##     day_out      night_out    alcohol_or_narcotics     mentor    
    ##  Min.   :0.0   Min.   :0.00   Min.   :0.00         Min.   :0.00  
    ##  1st Qu.:0.0   1st Qu.:0.00   1st Qu.:0.00         1st Qu.:0.00  
    ##  Median :1.0   Median :0.00   Median :0.00         Median :0.00  
    ##  Mean   :0.8   Mean   :0.51   Mean   :0.35         Mean   :0.41  
    ##  3rd Qu.:1.0   3rd Qu.:1.00   3rd Qu.:1.00         3rd Qu.:1.00  
    ##  Max.   :3.0   Max.   :3.00   Max.   :3.00         Max.   :1.00  
    ##  NA's   :1     NA's   :1      NA's   :1            NA's   :1     
    ##  mentor_meetings A - 1. I am enjoying the subject
    ##  Min.   :0.00    Min.   :3.00                    
    ##  1st Qu.:0.00    1st Qu.:4.00                    
    ##  Median :0.00    Median :5.00                    
    ##  Mean   :0.68    Mean   :4.49                    
    ##  3rd Qu.:1.00    3rd Qu.:5.00                    
    ##  Max.   :3.00    Max.   :5.00                    
    ##  NA's   :1       NA's   :1                       
    ##  A - 2. Classes start and end on time
    ##  Min.   :3.00                        
    ##  1st Qu.:4.00                        
    ##  Median :5.00                        
    ##  Mean   :4.68                        
    ##  3rd Qu.:5.00                        
    ##  Max.   :5.00                        
    ##  NA's   :1                           
    ##  A - 3. The learning environment is participative, involves learning by doing and is group-based
    ##  Min.   :3.00                                                                                   
    ##  1st Qu.:4.00                                                                                   
    ##  Median :4.00                                                                                   
    ##  Mean   :4.35                                                                                   
    ##  3rd Qu.:5.00                                                                                   
    ##  Max.   :5.00                                                                                   
    ##  NA's   :1                                                                                      
    ##  A - 4. The subject content is delivered according to the course outline and meets my expectations
    ##  Min.   :3.00                                                                                     
    ##  1st Qu.:4.75                                                                                     
    ##  Median :5.00                                                                                     
    ##  Mean   :4.74                                                                                     
    ##  3rd Qu.:5.00                                                                                     
    ##  Max.   :5.00                                                                                     
    ##  NA's   :1                                                                                        
    ##  A - 5. The topics are clear and logically developed
    ##  Min.   :2.00                                       
    ##  1st Qu.:4.00                                       
    ##  Median :5.00                                       
    ##  Mean   :4.65                                       
    ##  3rd Qu.:5.00                                       
    ##  Max.   :5.00                                       
    ##  NA's   :1                                          
    ##  A - 6. I am developing my oral and writing skills
    ##  Min.   :1.00                                     
    ##  1st Qu.:4.00                                     
    ##  Median :4.00                                     
    ##  Mean   :4.11                                     
    ##  3rd Qu.:5.00                                     
    ##  Max.   :5.00                                     
    ##  NA's   :1                                        
    ##  A - 7. I am developing my reflective and critical reasoning skills
    ##  Min.   :2.00                                                      
    ##  1st Qu.:4.00                                                      
    ##  Median :4.00                                                      
    ##  Mean   :4.38                                                      
    ##  3rd Qu.:5.00                                                      
    ##  Max.   :5.00                                                      
    ##  NA's   :1                                                         
    ##  A - 8. The assessment methods are assisting me to learn
    ##  Min.   :1.00                                           
    ##  1st Qu.:4.00                                           
    ##  Median :5.00                                           
    ##  Mean   :4.61                                           
    ##  3rd Qu.:5.00                                           
    ##  Max.   :5.00                                           
    ##  NA's   :1                                              
    ##  A - 9. I receive relevant feedback
    ##  Min.   :3.00                      
    ##  1st Qu.:4.00                      
    ##  Median :5.00                      
    ##  Mean   :4.58                      
    ##  3rd Qu.:5.00                      
    ##  Max.   :5.00                      
    ##  NA's   :1                         
    ##  A - 10. I read the recommended readings and notes
    ##  Min.   :3.00                                     
    ##  1st Qu.:4.00                                     
    ##  Median :5.00                                     
    ##  Mean   :4.55                                     
    ##  3rd Qu.:5.00                                     
    ##  Max.   :5.00                                     
    ##  NA's   :1                                        
    ##  A - 11. I use the eLearning material posted
    ##  Min.   :3.0                                
    ##  1st Qu.:4.0                                
    ##  Median :5.0                                
    ##  Mean   :4.7                                
    ##  3rd Qu.:5.0                                
    ##  Max.   :5.0                                
    ##  NA's   :1                                  
    ##  B - 1. Concept 1 of 6: Principles of Business Intelligence and the DataOps Philosophy
    ##  Min.   :1.00                                                                         
    ##  1st Qu.:4.00                                                                         
    ##  Median :4.00                                                                         
    ##  Mean   :4.25                                                                         
    ##  3rd Qu.:5.00                                                                         
    ##  Max.   :5.00                                                                         
    ##  NA's   :1                                                                            
    ##  B - 2. Concept 3 of 6: Linear Algorithms for Predictive Analytics
    ##  Min.   :2.00                                                     
    ##  1st Qu.:3.00                                                     
    ##  Median :4.00                                                     
    ##  Mean   :3.94                                                     
    ##  3rd Qu.:5.00                                                     
    ##  Max.   :5.00                                                     
    ##  NA's   :1                                                        
    ##  C - 2. Quizzes at the end of each concept
    ##  Min.   :2.00                             
    ##  1st Qu.:4.00                             
    ##  Median :5.00                             
    ##  Mean   :4.59                             
    ##  3rd Qu.:5.00                             
    ##  Max.   :5.00                             
    ##  NA's   :1                                
    ##  C - 3. Lab manuals that outline the steps to follow during the labs
    ##  Min.   :3.00                                                       
    ##  1st Qu.:4.00                                                       
    ##  Median :5.00                                                       
    ##  Mean   :4.61                                                       
    ##  3rd Qu.:5.00                                                       
    ##  Max.   :5.00                                                       
    ##  NA's   :1                                                          
    ##  C - 4. Required lab work submissions at the end of each lab manual that outline the activity to be done on your own
    ##  Min.   :3.00                                                                                                       
    ##  1st Qu.:4.00                                                                                                       
    ##  Median :5.00                                                                                                       
    ##  Mean   :4.55                                                                                                       
    ##  3rd Qu.:5.00                                                                                                       
    ##  Max.   :5.00                                                                                                       
    ##  NA's   :1                                                                                                          
    ##  C - 5. Supplementary videos to watch
    ##  Min.   :1.00                        
    ##  1st Qu.:4.00                        
    ##  Median :4.00                        
    ##  Mean   :4.19                        
    ##  3rd Qu.:5.00                        
    ##  Max.   :5.00                        
    ##  NA's   :1                           
    ##  C - 6. Supplementary podcasts to listen to
    ##  Min.   :1.00                              
    ##  1st Qu.:4.00                              
    ##  Median :4.00                              
    ##  Mean   :4.08                              
    ##  3rd Qu.:5.00                              
    ##  Max.   :5.00                              
    ##  NA's   :1                                 
    ##  C - 7. Supplementary content to read C - 8. Lectures slides
    ##  Min.   :1.00                         Min.   :2.0           
    ##  1st Qu.:4.00                         1st Qu.:4.0           
    ##  Median :4.00                         Median :5.0           
    ##  Mean   :4.17                         Mean   :4.6           
    ##  3rd Qu.:5.00                         3rd Qu.:5.0           
    ##  Max.   :5.00                         Max.   :5.0           
    ##  NA's   :1                            NA's   :1             
    ##  C - 9. Lecture notes on some of the lecture slides
    ##  Min.   :2.0                                       
    ##  1st Qu.:4.0                                       
    ##  Median :5.0                                       
    ##  Mean   :4.6                                       
    ##  3rd Qu.:5.0                                       
    ##  Max.   :5.0                                       
    ##  NA's   :1                                         
    ##  C - 10. The quality of the lectures given (quality measured by the breadth (the full span of knowledge of a subject) and depth (the extent to which specific topics are focused upon, amplified, and explored) of learning - NOT quality measured by how fun/comical/lively the lectures are)
    ##  Min.   :2.00                                                                                                                                                                                                                                                                                 
    ##  1st Qu.:4.00                                                                                                                                                                                                                                                                                 
    ##  Median :5.00                                                                                                                                                                                                                                                                                 
    ##  Mean   :4.54                                                                                                                                                                                                                                                                                 
    ##  3rd Qu.:5.00                                                                                                                                                                                                                                                                                 
    ##  Max.   :5.00                                                                                                                                                                                                                                                                                 
    ##  NA's   :1                                                                                                                                                                                                                                                                                    
    ##  C - 11. The division of theory and practice such that most of the theory is done during the recorded online classes and most of the practice is done during the physical classes
    ##  Min.   :2.00                                                                                                                                                                    
    ##  1st Qu.:4.00                                                                                                                                                                    
    ##  Median :5.00                                                                                                                                                                    
    ##  Mean   :4.49                                                                                                                                                                    
    ##  3rd Qu.:5.00                                                                                                                                                                    
    ##  Max.   :5.00                                                                                                                                                                    
    ##  NA's   :1                                                                                                                                                                       
    ##  C - 12. The recordings of online classes
    ##  Min.   :2.00                            
    ##  1st Qu.:4.00                            
    ##  Median :5.00                            
    ##  Mean   :4.33                            
    ##  3rd Qu.:5.00                            
    ##  Max.   :5.00                            
    ##  NA's   :1                               
    ##  D - 1. Write two things you like about the teaching and learning in this unit so far.
    ##  Length:101                                                                           
    ##  Class :character                                                                     
    ##  Mode  :character                                                                     
    ##                                                                                       
    ##                                                                                       
    ##                                                                                       
    ##                                                                                       
    ##  D - 2. Write at least one recommendation to improve the teaching and learning in this unit (for the remaining weeks in the semester)
    ##  Length:101                                                                                                                          
    ##  Class :character                                                                                                                    
    ##  Mode  :character                                                                                                                    
    ##                                                                                                                                      
    ##                                                                                                                                      
    ##                                                                                                                                      
    ##                                                                                                                                      
    ##  Average Course Evaluation Rating Average Level of Learning Attained Rating
    ##  Min.   :2.909                    Min.   :2.000                            
    ##  1st Qu.:4.273                    1st Qu.:3.500                            
    ##  Median :4.545                    Median :4.000                            
    ##  Mean   :4.531                    Mean   :4.095                            
    ##  3rd Qu.:4.909                    3rd Qu.:4.500                            
    ##  Max.   :5.000                    Max.   :5.000                            
    ##  NA's   :1                        NA's   :1                                
    ##  Average Pedagogical Strategy Effectiveness Rating
    ##  Min.   :3.182                                    
    ##  1st Qu.:4.068                                    
    ##  Median :4.545                                    
    ##  Mean   :4.432                                    
    ##  3rd Qu.:4.909                                    
    ##  Max.   :5.000                                    
    ##  NA's   :1                                        
    ##  Project: Section 1-4: (20%) x/10 Project: Section 5-11: (50%) x/10
    ##  Min.   : 0.000                   Min.   : 0.000                   
    ##  1st Qu.: 7.400                   1st Qu.: 6.000                   
    ##  Median : 8.500                   Median : 7.800                   
    ##  Mean   : 8.011                   Mean   : 6.582                   
    ##  3rd Qu.: 9.000                   3rd Qu.: 8.300                   
    ##  Max.   :10.000                   Max.   :10.000                   
    ##                                                                    
    ##  Project: Section 12: (30%) x/5 Project: (10%): x/30 x 100 TOTAL
    ##  Min.   :0.000                  Min.   :  0.00                  
    ##  1st Qu.:0.000                  1st Qu.: 56.00                  
    ##  Median :0.000                  Median : 66.40                  
    ##  Mean   :1.015                  Mean   : 62.39                  
    ##  3rd Qu.:1.250                  3rd Qu.: 71.60                  
    ##  Max.   :5.000                  Max.   :100.00                  
    ##  NA's   :1                                                      
    ##  Quiz 1 on Concept 1 (Introduction) x/32 Quiz 3 on Concept 3 (Linear) x/15
    ##  Min.   : 4.75                           Min.   : 3.00                    
    ##  1st Qu.:11.53                           1st Qu.: 7.00                    
    ##  Median :15.33                           Median : 9.00                    
    ##  Mean   :16.36                           Mean   : 9.53                    
    ##  3rd Qu.:19.63                           3rd Qu.:12.00                    
    ##  Max.   :31.25                           Max.   :15.00                    
    ##                                          NA's   :2                        
    ##  Quiz 4 on Concept 4 (Non-Linear) x/22 Quiz 5 on Concept 5 (Dashboarding) x/10
    ##  Min.   : 3.00                         Min.   : 0.000                         
    ##  1st Qu.:10.91                         1st Qu.: 5.000                         
    ##  Median :13.50                         Median : 6.330                         
    ##  Mean   :13.94                         Mean   : 6.367                         
    ##  3rd Qu.:17.50                         3rd Qu.: 8.000                         
    ##  Max.   :22.00                         Max.   :12.670                         
    ##  NA's   :6                             NA's   :12                             
    ##  Quizzes and  Bonus Marks (7%): x/79 x 100 TOTAL
    ##  Min.   :26.26                                  
    ##  1st Qu.:43.82                                  
    ##  Median :55.31                                  
    ##  Mean   :56.22                                  
    ##  3rd Qu.:65.16                                  
    ##  Max.   :95.25                                  
    ##                                                 
    ##  Lab 1 - 2.c. - (Simple Linear Regression) x/5
    ##  Min.   :3.000                                
    ##  1st Qu.:5.000                                
    ##  Median :5.000                                
    ##  Mean   :4.898                                
    ##  3rd Qu.:5.000                                
    ##  Max.   :5.000                                
    ##  NA's   :3                                    
    ##  Lab 2 - 2.e. -  (Linear Regression using Gradient Descent) x/5
    ##  Min.   :2.150                                                 
    ##  1st Qu.:3.150                                                 
    ##  Median :4.850                                                 
    ##  Mean   :4.166                                                 
    ##  3rd Qu.:5.000                                                 
    ##  Max.   :5.000                                                 
    ##  NA's   :6                                                     
    ##  Lab 3 - 2.g. - (Logistic Regression using Gradient Descent) x/5
    ##  Min.   :2.85                                                   
    ##  1st Qu.:4.85                                                   
    ##  Median :4.85                                                   
    ##  Mean   :4.63                                                   
    ##  3rd Qu.:4.85                                                   
    ##  Max.   :5.00                                                   
    ##  NA's   :9                                                      
    ##  Lab 4 - 2.h. - (Linear Discriminant Analysis) x/5
    ##  Min.   :1.850                                    
    ##  1st Qu.:4.100                                    
    ##  Median :4.850                                    
    ##  Mean   :4.425                                    
    ##  3rd Qu.:5.000                                    
    ##  Max.   :5.000                                    
    ##  NA's   :18                                       
    ##  Lab 5 - Chart JS Dashboard Setup x/5 Lab Work (7%) x/25 x 100
    ##  Min.   :0.000                        Min.   : 17.80          
    ##  1st Qu.:0.000                        1st Qu.: 70.80          
    ##  Median :5.000                        Median : 80.00          
    ##  Mean   :3.404                        Mean   : 79.72          
    ##  3rd Qu.:5.000                        3rd Qu.: 97.20          
    ##  Max.   :5.000                        Max.   :100.00          
    ##                                                               
    ##  CAT 1 (8%): x/38 x 100 CAT 2 (8%): x/100 x 100
    ##  Min.   :32.89          Min.   :  0.00         
    ##  1st Qu.:59.21          1st Qu.: 51.00         
    ##  Median :69.73          Median : 63.50         
    ##  Mean   :69.39          Mean   : 62.13         
    ##  3rd Qu.:82.89          3rd Qu.: 81.75         
    ##  Max.   :97.36          Max.   :100.00         
    ##  NA's   :4              NA's   :31             
    ##  Attendance Waiver Granted: 1 = Yes, 0 = No Absenteeism Percentage
    ##  Min.   :0.00000                            Min.   : 0.00         
    ##  1st Qu.:0.00000                            1st Qu.: 7.41         
    ##  Median :0.00000                            Median :14.81         
    ##  Mean   :0.04951                            Mean   :15.42         
    ##  3rd Qu.:0.00000                            3rd Qu.:22.22         
    ##  Max.   :1.00000                            Max.   :51.85         
    ##                                                                   
    ##  Coursework TOTAL: x/40 (40%) EXAM: x/60 (60%)
    ##  Min.   : 7.47                Min.   : 5.00   
    ##  1st Qu.:20.44                1st Qu.:26.00   
    ##  Median :24.58                Median :34.00   
    ##  Mean   :24.53                Mean   :33.94   
    ##  3rd Qu.:29.31                3rd Qu.:42.00   
    ##  Max.   :35.08                Max.   :56.00   
    ##                               NA's   :4       
    ##  TOTAL = Coursework TOTAL + EXAM (100%)    GRADE          
    ##  Min.   : 7.47                          Length:101        
    ##  1st Qu.:45.54                          Class :character  
    ##  Median :58.69                          Mode  :character  
    ##  Mean   :57.12                                            
    ##  3rd Qu.:68.83                                            
    ##  Max.   :87.72                                            
    ## 

``` r
colnames(StudentPerformanceDataset)
```

    ##   [1] "class_group"                                                                                                                                                                                                                                                                                  
    ##   [2] "gender"                                                                                                                                                                                                                                                                                       
    ##   [3] "YOB"                                                                                                                                                                                                                                                                                          
    ##   [4] "regret_choosing_bi"                                                                                                                                                                                                                                                                           
    ##   [5] "drop_bi_now"                                                                                                                                                                                                                                                                                  
    ##   [6] "motivator"                                                                                                                                                                                                                                                                                    
    ##   [7] "read_content_before_lecture"                                                                                                                                                                                                                                                                  
    ##   [8] "anticipate_test_questions"                                                                                                                                                                                                                                                                    
    ##   [9] "answer_rhetorical_questions"                                                                                                                                                                                                                                                                  
    ##  [10] "find_terms_I_do_not_know"                                                                                                                                                                                                                                                                     
    ##  [11] "copy_new_terms_in_reading_notebook"                                                                                                                                                                                                                                                           
    ##  [12] "take_quizzes_and_use_results"                                                                                                                                                                                                                                                                 
    ##  [13] "reorganise_course_outline"                                                                                                                                                                                                                                                                    
    ##  [14] "write_down_important_points"                                                                                                                                                                                                                                                                  
    ##  [15] "space_out_revision"                                                                                                                                                                                                                                                                           
    ##  [16] "studying_in_study_group"                                                                                                                                                                                                                                                                      
    ##  [17] "schedule_appointments"                                                                                                                                                                                                                                                                        
    ##  [18] "goal_oriented"                                                                                                                                                                                                                                                                                
    ##  [19] "spaced_repetition"                                                                                                                                                                                                                                                                            
    ##  [20] "testing_and_active_recall"                                                                                                                                                                                                                                                                    
    ##  [21] "interleaving"                                                                                                                                                                                                                                                                                 
    ##  [22] "categorizing"                                                                                                                                                                                                                                                                                 
    ##  [23] "retrospective_timetable"                                                                                                                                                                                                                                                                      
    ##  [24] "cornell_notes"                                                                                                                                                                                                                                                                                
    ##  [25] "sq3r"                                                                                                                                                                                                                                                                                         
    ##  [26] "commute"                                                                                                                                                                                                                                                                                      
    ##  [27] "study_time"                                                                                                                                                                                                                                                                                   
    ##  [28] "repeats_since_Y1"                                                                                                                                                                                                                                                                             
    ##  [29] "paid_tuition"                                                                                                                                                                                                                                                                                 
    ##  [30] "free_tuition"                                                                                                                                                                                                                                                                                 
    ##  [31] "extra_curricular"                                                                                                                                                                                                                                                                             
    ##  [32] "sports_extra_curricular"                                                                                                                                                                                                                                                                      
    ##  [33] "exercise_per_week"                                                                                                                                                                                                                                                                            
    ##  [34] "meditate"                                                                                                                                                                                                                                                                                     
    ##  [35] "pray"                                                                                                                                                                                                                                                                                         
    ##  [36] "internet"                                                                                                                                                                                                                                                                                     
    ##  [37] "laptop"                                                                                                                                                                                                                                                                                       
    ##  [38] "family_relationships"                                                                                                                                                                                                                                                                         
    ##  [39] "friendships"                                                                                                                                                                                                                                                                                  
    ##  [40] "romantic_relationships"                                                                                                                                                                                                                                                                       
    ##  [41] "spiritual_wellnes"                                                                                                                                                                                                                                                                            
    ##  [42] "financial_wellness"                                                                                                                                                                                                                                                                           
    ##  [43] "health"                                                                                                                                                                                                                                                                                       
    ##  [44] "day_out"                                                                                                                                                                                                                                                                                      
    ##  [45] "night_out"                                                                                                                                                                                                                                                                                    
    ##  [46] "alcohol_or_narcotics"                                                                                                                                                                                                                                                                         
    ##  [47] "mentor"                                                                                                                                                                                                                                                                                       
    ##  [48] "mentor_meetings"                                                                                                                                                                                                                                                                              
    ##  [49] "A - 1. I am enjoying the subject"                                                                                                                                                                                                                                                             
    ##  [50] "A - 2. Classes start and end on time"                                                                                                                                                                                                                                                         
    ##  [51] "A - 3. The learning environment is participative, involves learning by doing and is group-based"                                                                                                                                                                                              
    ##  [52] "A - 4. The subject content is delivered according to the course outline and meets my expectations"                                                                                                                                                                                            
    ##  [53] "A - 5. The topics are clear and logically developed"                                                                                                                                                                                                                                          
    ##  [54] "A - 6. I am developing my oral and writing skills"                                                                                                                                                                                                                                            
    ##  [55] "A - 7. I am developing my reflective and critical reasoning skills"                                                                                                                                                                                                                           
    ##  [56] "A - 8. The assessment methods are assisting me to learn"                                                                                                                                                                                                                                      
    ##  [57] "A - 9. I receive relevant feedback"                                                                                                                                                                                                                                                           
    ##  [58] "A - 10. I read the recommended readings and notes"                                                                                                                                                                                                                                            
    ##  [59] "A - 11. I use the eLearning material posted"                                                                                                                                                                                                                                                  
    ##  [60] "B - 1. Concept 1 of 6: Principles of Business Intelligence and the DataOps Philosophy"                                                                                                                                                                                                        
    ##  [61] "B - 2. Concept 3 of 6: Linear Algorithms for Predictive Analytics"                                                                                                                                                                                                                            
    ##  [62] "C - 2. Quizzes at the end of each concept"                                                                                                                                                                                                                                                    
    ##  [63] "C - 3. Lab manuals that outline the steps to follow during the labs"                                                                                                                                                                                                                          
    ##  [64] "C - 4. Required lab work submissions at the end of each lab manual that outline the activity to be done on your own"                                                                                                                                                                          
    ##  [65] "C - 5. Supplementary videos to watch"                                                                                                                                                                                                                                                         
    ##  [66] "C - 6. Supplementary podcasts to listen to"                                                                                                                                                                                                                                                   
    ##  [67] "C - 7. Supplementary content to read"                                                                                                                                                                                                                                                         
    ##  [68] "C - 8. Lectures slides"                                                                                                                                                                                                                                                                       
    ##  [69] "C - 9. Lecture notes on some of the lecture slides"                                                                                                                                                                                                                                           
    ##  [70] "C - 10. The quality of the lectures given (quality measured by the breadth (the full span of knowledge of a subject) and depth (the extent to which specific topics are focused upon, amplified, and explored) of learning - NOT quality measured by how fun/comical/lively the lectures are)"
    ##  [71] "C - 11. The division of theory and practice such that most of the theory is done during the recorded online classes and most of the practice is done during the physical classes"                                                                                                             
    ##  [72] "C - 12. The recordings of online classes"                                                                                                                                                                                                                                                     
    ##  [73] "D - 1. Write two things you like about the teaching and learning in this unit so far."                                                                                                                                                                                                        
    ##  [74] "D - 2. Write at least one recommendation to improve the teaching and learning in this unit (for the remaining weeks in the semester)"                                                                                                                                                         
    ##  [75] "Average Course Evaluation Rating"                                                                                                                                                                                                                                                             
    ##  [76] "Average Level of Learning Attained Rating"                                                                                                                                                                                                                                                    
    ##  [77] "Average Pedagogical Strategy Effectiveness Rating"                                                                                                                                                                                                                                            
    ##  [78] "Project: Section 1-4: (20%) x/10"                                                                                                                                                                                                                                                             
    ##  [79] "Project: Section 5-11: (50%) x/10"                                                                                                                                                                                                                                                            
    ##  [80] "Project: Section 12: (30%) x/5"                                                                                                                                                                                                                                                               
    ##  [81] "Project: (10%): x/30 x 100 TOTAL"                                                                                                                                                                                                                                                             
    ##  [82] "Quiz 1 on Concept 1 (Introduction) x/32"                                                                                                                                                                                                                                                      
    ##  [83] "Quiz 3 on Concept 3 (Linear) x/15"                                                                                                                                                                                                                                                            
    ##  [84] "Quiz 4 on Concept 4 (Non-Linear) x/22"                                                                                                                                                                                                                                                        
    ##  [85] "Quiz 5 on Concept 5 (Dashboarding) x/10"                                                                                                                                                                                                                                                      
    ##  [86] "Quizzes and  Bonus Marks (7%): x/79 x 100 TOTAL"                                                                                                                                                                                                                                              
    ##  [87] "Lab 1 - 2.c. - (Simple Linear Regression) x/5"                                                                                                                                                                                                                                                
    ##  [88] "Lab 2 - 2.e. -  (Linear Regression using Gradient Descent) x/5"                                                                                                                                                                                                                               
    ##  [89] "Lab 3 - 2.g. - (Logistic Regression using Gradient Descent) x/5"                                                                                                                                                                                                                              
    ##  [90] "Lab 4 - 2.h. - (Linear Discriminant Analysis) x/5"                                                                                                                                                                                                                                            
    ##  [91] "Lab 5 - Chart JS Dashboard Setup x/5"                                                                                                                                                                                                                                                         
    ##  [92] "Lab Work (7%) x/25 x 100"                                                                                                                                                                                                                                                                     
    ##  [93] "CAT 1 (8%): x/38 x 100"                                                                                                                                                                                                                                                                       
    ##  [94] "CAT 2 (8%): x/100 x 100"                                                                                                                                                                                                                                                                      
    ##  [95] "Attendance Waiver Granted: 1 = Yes, 0 = No"                                                                                                                                                                                                                                                   
    ##  [96] "Absenteeism Percentage"                                                                                                                                                                                                                                                                       
    ##  [97] "Coursework TOTAL: x/40 (40%)"                                                                                                                                                                                                                                                                 
    ##  [98] "EXAM: x/60 (60%)"                                                                                                                                                                                                                                                                             
    ##  [99] "TOTAL = Coursework TOTAL + EXAM (100%)"                                                                                                                                                                                                                                                       
    ## [100] "GRADE"

``` r
StudentPerformanceDataset <- as.data.frame(StudentPerformanceDataset)


hist(StudentPerformanceDataset[,2], main = names(StudentPerformanceDataset)[2])
```

![](BIProject-Template_files/figure-gfm/Apply%20Scale%20Data%20Transform-1.png)<!-- -->

``` r
hist(StudentPerformanceDataset[,3], main = names(StudentPerformanceDataset)[3])
```

![](BIProject-Template_files/figure-gfm/Apply%20Scale%20Data%20Transform-2.png)<!-- -->

``` r
hist(StudentPerformanceDataset[,4], main = names(StudentPerformanceDataset)[5])
```

![](BIProject-Template_files/figure-gfm/Apply%20Scale%20Data%20Transform-3.png)<!-- -->

``` r
hist(StudentPerformanceDataset[,5], main = names(StudentPerformanceDataset)[6])
```

![](BIProject-Template_files/figure-gfm/Apply%20Scale%20Data%20Transform-4.png)<!-- -->

``` r
hist(StudentPerformanceDataset[,6], main = names(StudentPerformanceDataset)[7])
```

![](BIProject-Template_files/figure-gfm/Apply%20Scale%20Data%20Transform-5.png)<!-- -->

``` r
hist(StudentPerformanceDataset[,7], main = names(StudentPerformanceDataset)[8])
```

![](BIProject-Template_files/figure-gfm/Apply%20Scale%20Data%20Transform-6.png)<!-- -->

``` r
hist(StudentPerformanceDataset[,8], main = names(StudentPerformanceDataset)[9])
```

![](BIProject-Template_files/figure-gfm/Apply%20Scale%20Data%20Transform-7.png)<!-- -->

``` r
hist(StudentPerformanceDataset[,9], main = names(StudentPerformanceDataset)[10])
```

![](BIProject-Template_files/figure-gfm/Apply%20Scale%20Data%20Transform-8.png)<!-- -->

``` r
hist(StudentPerformanceDataset[,10], main = names(StudentPerformanceDataset)[11])
```

![](BIProject-Template_files/figure-gfm/Apply%20Scale%20Data%20Transform-9.png)<!-- -->

``` r
hist(StudentPerformanceDataset[,11], main = names(StudentPerformanceDataset)[12])
```

![](BIProject-Template_files/figure-gfm/Apply%20Scale%20Data%20Transform-10.png)<!-- -->

``` r
hist(StudentPerformanceDataset[,12], main = names(StudentPerformanceDataset)[13])
```

![](BIProject-Template_files/figure-gfm/Apply%20Scale%20Data%20Transform-11.png)<!-- -->

``` r
hist(StudentPerformanceDataset[,13], main = names(StudentPerformanceDataset)[14])
```

![](BIProject-Template_files/figure-gfm/Apply%20Scale%20Data%20Transform-12.png)<!-- -->

``` r
student_performance_scale_transform <- as.data.frame(StudentPerformanceDataset)  # Convert to data frame if needed
preprocessed_data <- preProcess(StudentPerformanceDataset)

model_of_the_transform <- preProcess(StudentPerformanceDataset, method = c("scale"))
print(model_of_the_transform)
```

    ## Created from 51 samples and 100 variables
    ## 
    ## Pre-processing:
    ##   - ignored (4)
    ##   - scaled (96)

``` r
student_performance_scale_transform <- predict(model_of_the_transform,
                                               StudentPerformanceDataset)
# AFTER
summary(student_performance_scale_transform)
```

    ##  class_group            gender           YOB       regret_choosing_bi
    ##  Length:101         Min.   :0.000   Min.   :2008   Min.   :0.0000    
    ##  Class :character   1st Qu.:0.000   1st Qu.:2010   1st Qu.:0.0000    
    ##  Mode  :character   Median :2.012   Median :2011   Median :0.0000    
    ##                     Mean   :1.156   Mean   :2011   Mean   :0.1414    
    ##                     3rd Qu.:2.012   3rd Qu.:2012   3rd Qu.:0.0000    
    ##                     Max.   :2.012   Max.   :2013   Max.   :7.1421    
    ##                                                                      
    ##   drop_bi_now       motivator     read_content_before_lecture
    ##  Min.   :0.0000   Min.   :0.000   Min.   :1.038              
    ##  1st Qu.:0.0000   1st Qu.:2.306   1st Qu.:2.076              
    ##  Median :0.0000   Median :2.306   Median :3.114              
    ##  Mean   :0.1414   Mean   :1.735   Mean   :2.857              
    ##  3rd Qu.:0.0000   3rd Qu.:2.306   3rd Qu.:3.114              
    ##  Max.   :7.1421   Max.   :2.306   Max.   :5.190              
    ##                                                              
    ##  anticipate_test_questions answer_rhetorical_questions find_terms_I_do_not_know
    ##  Min.   :1.007             Min.   :1.007               Min.   :0.9478          
    ##  1st Qu.:3.022             1st Qu.:3.020               1st Qu.:2.8435          
    ##  Median :4.030             Median :4.026               Median :3.7914          
    ##  Mean   :3.611             Mean   :3.448               Mean   :3.5474          
    ##  3rd Qu.:4.030             3rd Qu.:4.026               3rd Qu.:4.7392          
    ##  Max.   :5.037             Max.   :5.033               Max.   :4.7392          
    ##                                                                                
    ##  copy_new_terms_in_reading_notebook take_quizzes_and_use_results
    ##  Min.   :0.9033                     Min.   :0.9299              
    ##  1st Qu.:2.7099                     1st Qu.:2.7897              
    ##  Median :3.6132                     Median :3.7196              
    ##  Mean   :3.3091                     Mean   :3.6644              
    ##  3rd Qu.:3.6132                     3rd Qu.:4.6495              
    ##  Max.   :4.5165                     Max.   :4.6495              
    ##                                                                 
    ##  reorganise_course_outline write_down_important_points space_out_revision
    ##  Min.   :0.8648            Min.   :0.9279              Min.   :0.8847    
    ##  1st Qu.:2.5945            1st Qu.:2.7838              1st Qu.:2.6541    
    ##  Median :2.5945            Median :3.7117              Median :2.6541    
    ##  Mean   :2.9199            Mean   :3.5555              Mean   :2.8556    
    ##  3rd Qu.:3.4593            3rd Qu.:4.6396              3rd Qu.:3.5388    
    ##  Max.   :4.3241            Max.   :4.6396              Max.   :4.4235    
    ##                                                                          
    ##  studying_in_study_group schedule_appointments goal_oriented   
    ##  Min.   :0.7473          Min.   :0.9782        Min.   :0.0000  
    ##  1st Qu.:0.7473          1st Qu.:0.9782        1st Qu.:0.0000  
    ##  Median :1.4947          Median :1.9563        Median :0.0000  
    ##  Mean   :1.8350          Mean   :1.8885        Mean   :0.4944  
    ##  3rd Qu.:2.2420          3rd Qu.:1.9563        3rd Qu.:0.0000  
    ##  Max.   :3.7367          Max.   :4.8908        Max.   :2.4969  
    ##                                                                
    ##  spaced_repetition testing_and_active_recall  interleaving    categorizing  
    ##  Min.   :1.204     Min.   :1.392             Min.   :1.345   Min.   :1.352  
    ##  1st Qu.:2.409     1st Qu.:4.175             1st Qu.:2.689   1st Qu.:2.705  
    ##  Median :3.613     Median :4.175             Median :2.689   Median :4.057  
    ##  Mean   :3.076     Mean   :4.257             Mean   :3.035   Mean   :3.669  
    ##  3rd Qu.:3.613     3rd Qu.:5.566             3rd Qu.:4.034   3rd Qu.:4.057  
    ##  Max.   :4.817     Max.   :5.566             Max.   :5.379   Max.   :5.410  
    ##                                                                             
    ##  retrospective_timetable cornell_notes        sq3r           commute      
    ##  Min.   :1.130           Min.   :1.005   Min.   :0.9537   Min.   :0.9587  
    ##  1st Qu.:2.259           1st Qu.:2.010   1st Qu.:1.9074   1st Qu.:1.9174  
    ##  Median :2.259           Median :3.014   Median :2.8612   Median :2.8761  
    ##  Mean   :2.718           Mean   :2.557   Mean   :2.4929   Mean   :2.6173  
    ##  3rd Qu.:3.389           3rd Qu.:3.014   3rd Qu.:2.8612   3rd Qu.:3.8349  
    ##  Max.   :4.519           Max.   :4.019   Max.   :3.8149   Max.   :3.8349  
    ##                                                           NA's   :1       
    ##    study_time    repeats_since_Y1  paid_tuition     free_tuition   
    ##  Min.   :1.218   Min.   :0.0000   Min.   :0.0000   Min.   :0.0000  
    ##  1st Qu.:1.218   1st Qu.:0.0000   1st Qu.:0.0000   1st Qu.:0.0000  
    ##  Median :2.436   Median :0.9479   Median :0.0000   Median :0.0000  
    ##  Mean   :2.131   Mean   :0.9716   Mean   :0.3498   Mean   :0.6051  
    ##  3rd Qu.:2.436   3rd Qu.:1.4218   3rd Qu.:0.0000   3rd Qu.:2.2412  
    ##  Max.   :4.871   Max.   :4.7394   Max.   :3.1800   Max.   :2.2412  
    ##  NA's   :1       NA's   :1        NA's   :1        NA's   :1       
    ##  extra_curricular sports_extra_curricular exercise_per_week    meditate     
    ##  Min.   :0.000    Min.   :0.0000          Min.   :0.000     Min.   :0.0000  
    ##  1st Qu.:0.000    1st Qu.:0.0000          1st Qu.:1.234     1st Qu.:0.0000  
    ##  Median :1.994    Median :0.0000          Median :1.234     Median :1.0714  
    ##  Mean   :1.057    Mean   :0.7462          Mean   :1.358     Mean   :0.8143  
    ##  3rd Qu.:1.994    3rd Qu.:2.0729          3rd Qu.:2.468     3rd Qu.:1.0714  
    ##  Max.   :1.994    Max.   :2.0729          Max.   :3.702     Max.   :3.2143  
    ##  NA's   :1        NA's   :1               NA's   :1         NA's   :1       
    ##       pray           internet         laptop  family_relationships
    ##  Min.   :0.0000   Min.   :0.000   Min.   :1   Min.   :2.499       
    ##  1st Qu.:0.9748   1st Qu.:2.959   1st Qu.:1   1st Qu.:4.999       
    ##  Median :1.9496   Median :2.959   Median :1   Median :4.999       
    ##  Mean   :2.0373   Mean   :2.574   Mean   :1   Mean   :5.236       
    ##  3rd Qu.:2.9243   3rd Qu.:2.959   3rd Qu.:1   3rd Qu.:6.249       
    ##  Max.   :2.9243   Max.   :2.959   Max.   :1   Max.   :6.249       
    ##  NA's   :1        NA's   :1       NA's   :1   NA's   :1           
    ##   friendships    romantic_relationships spiritual_wellnes financial_wellness
    ##  Min.   :2.734   Min.   :0.0000         Min.   :1.068     Min.   :0.9124    
    ##  1st Qu.:5.467   1st Qu.:0.0000         1st Qu.:3.205     1st Qu.:1.8249    
    ##  Median :5.467   Median :0.0000         Median :4.273     Median :2.7373    
    ##  Mean   :5.481   Mean   :0.8531         Mean   :3.899     Mean   :2.7647    
    ##  3rd Qu.:5.467   3rd Qu.:1.8681         3rd Qu.:4.273     3rd Qu.:3.6498    
    ##  Max.   :6.834   Max.   :2.4908         Max.   :5.341     Max.   :4.5622    
    ##  NA's   :1       NA's   :1              NA's   :1         NA's   :1         
    ##      health         day_out        night_out      alcohol_or_narcotics
    ##  Min.   :1.050   Min.   :0.000   Min.   :0.0000   Min.   :0.000       
    ##  1st Qu.:3.149   1st Qu.:0.000   1st Qu.:0.0000   1st Qu.:0.000       
    ##  Median :4.199   Median :1.759   Median :0.0000   Median :0.000       
    ##  Mean   :4.241   Mean   :1.407   Mean   :0.7926   Mean   :0.628       
    ##  3rd Qu.:5.249   3rd Qu.:1.759   3rd Qu.:1.5541   3rd Qu.:1.794       
    ##  Max.   :5.249   Max.   :5.277   Max.   :4.6623   Max.   :5.383       
    ##  NA's   :1       NA's   :1       NA's   :1        NA's   :1           
    ##      mentor       mentor_meetings  A - 1. I am enjoying the subject
    ##  Min.   :0.0000   Min.   :0.0000   Min.   :5.046                   
    ##  1st Qu.:0.0000   1st Qu.:0.0000   1st Qu.:6.728                   
    ##  Median :0.0000   Median :0.0000   Median :8.410                   
    ##  Mean   :0.8294   Mean   :0.8101   Mean   :7.553                   
    ##  3rd Qu.:2.0230   3rd Qu.:1.1913   3rd Qu.:8.410                   
    ##  Max.   :2.0230   Max.   :3.5738   Max.   :8.410                   
    ##  NA's   :1        NA's   :1        NA's   :1                       
    ##  A - 2. Classes start and end on time
    ##  Min.   : 6.124                      
    ##  1st Qu.: 8.165                      
    ##  Median :10.206                      
    ##  Mean   : 9.553                      
    ##  3rd Qu.:10.206                      
    ##  Max.   :10.206                      
    ##  NA's   :1                           
    ##  A - 3. The learning environment is participative, involves learning by doing and is group-based
    ##  Min.   :4.565                                                                                  
    ##  1st Qu.:6.087                                                                                  
    ##  Median :6.087                                                                                  
    ##  Mean   :6.620                                                                                  
    ##  3rd Qu.:7.609                                                                                  
    ##  Max.   :7.609                                                                                  
    ##  NA's   :1                                                                                      
    ##  A - 4. The subject content is delivered according to the course outline and meets my expectations
    ##  Min.   : 6.477                                                                                   
    ##  1st Qu.:10.255                                                                                   
    ##  Median :10.795                                                                                   
    ##  Mean   :10.233                                                                                   
    ##  3rd Qu.:10.795                                                                                   
    ##  Max.   :10.795                                                                                   
    ##  NA's   :1                                                                                        
    ##  A - 5. The topics are clear and logically developed
    ##  Min.   :3.477                                      
    ##  1st Qu.:6.955                                      
    ##  Median :8.693                                      
    ##  Mean   :8.085                                      
    ##  3rd Qu.:8.693                                      
    ##  Max.   :8.693                                      
    ##  NA's   :1                                          
    ##  A - 6. I am developing my oral and writing skills
    ##  Min.   :1.143                                    
    ##  1st Qu.:4.572                                    
    ##  Median :4.572                                    
    ##  Mean   :4.697                                    
    ##  3rd Qu.:5.715                                    
    ##  Max.   :5.715                                    
    ##  NA's   :1                                        
    ##  A - 7. I am developing my reflective and critical reasoning skills
    ##  Min.   :2.886                                                     
    ##  1st Qu.:5.771                                                     
    ##  Median :5.771                                                     
    ##  Mean   :6.319                                                     
    ##  3rd Qu.:7.214                                                     
    ##  Max.   :7.214                                                     
    ##  NA's   :1                                                         
    ##  A - 8. The assessment methods are assisting me to learn
    ##  Min.   :1.539                                          
    ##  1st Qu.:6.157                                          
    ##  Median :7.696                                          
    ##  Mean   :7.095                                          
    ##  3rd Qu.:7.696                                          
    ##  Max.   :7.696                                          
    ##  NA's   :1                                              
    ##  A - 9. I receive relevant feedback
    ##  Min.   :5.417                     
    ##  1st Qu.:7.223                     
    ##  Median :9.029                     
    ##  Mean   :8.271                     
    ##  3rd Qu.:9.029                     
    ##  Max.   :9.029                     
    ##  NA's   :1                         
    ##  A - 10. I read the recommended readings and notes
    ##  Min.   :4.795                                    
    ##  1st Qu.:6.394                                    
    ##  Median :7.992                                    
    ##  Mean   :7.273                                    
    ##  3rd Qu.:7.992                                    
    ##  Max.   :7.992                                    
    ##  NA's   :1                                        
    ##  A - 11. I use the eLearning material posted
    ##  Min.   :5.745                              
    ##  1st Qu.:7.659                              
    ##  Median :9.574                              
    ##  Mean   :9.000                              
    ##  3rd Qu.:9.574                              
    ##  Max.   :9.574                              
    ##  NA's   :1                                  
    ##  B - 1. Concept 1 of 6: Principles of Business Intelligence and the DataOps Philosophy
    ##  Min.   :1.277                                                                        
    ##  1st Qu.:5.106                                                                        
    ##  Median :5.106                                                                        
    ##  Mean   :5.425                                                                        
    ##  3rd Qu.:6.383                                                                        
    ##  Max.   :6.383                                                                        
    ##  NA's   :1                                                                            
    ##  B - 2. Concept 3 of 6: Linear Algorithms for Predictive Analytics
    ##  Min.   :2.319                                                    
    ##  1st Qu.:3.478                                                    
    ##  Median :4.638                                                    
    ##  Mean   :4.568                                                    
    ##  3rd Qu.:5.797                                                    
    ##  Max.   :5.797                                                    
    ##  NA's   :1                                                        
    ##  C - 2. Quizzes at the end of each concept
    ##  Min.   :3.22                             
    ##  1st Qu.:6.44                             
    ##  Median :8.05                             
    ##  Mean   :7.39                             
    ##  3rd Qu.:8.05                             
    ##  Max.   :8.05                             
    ##  NA's   :1                                
    ##  C - 3. Lab manuals that outline the steps to follow during the labs
    ##  Min.   :4.990                                                      
    ##  1st Qu.:6.653                                                      
    ##  Median :8.316                                                      
    ##  Mean   :7.667                                                      
    ##  3rd Qu.:8.316                                                      
    ##  Max.   :8.316                                                      
    ##  NA's   :1                                                          
    ##  C - 4. Required lab work submissions at the end of each lab manual that outline the activity to be done on your own
    ##  Min.   :4.924                                                                                                      
    ##  1st Qu.:6.565                                                                                                      
    ##  Median :8.207                                                                                                      
    ##  Mean   :7.468                                                                                                      
    ##  3rd Qu.:8.207                                                                                                      
    ##  Max.   :8.207                                                                                                      
    ##  NA's   :1                                                                                                          
    ##  C - 5. Supplementary videos to watch
    ##  Min.   :1.131                       
    ##  1st Qu.:4.524                       
    ##  Median :4.524                       
    ##  Mean   :4.739                       
    ##  3rd Qu.:5.655                       
    ##  Max.   :5.655                       
    ##  NA's   :1                           
    ##  C - 6. Supplementary podcasts to listen to
    ##  Min.   :1.008                             
    ##  1st Qu.:4.034                             
    ##  Median :4.034                             
    ##  Mean   :4.114                             
    ##  3rd Qu.:5.042                             
    ##  Max.   :5.042                             
    ##  NA's   :1                                 
    ##  C - 7. Supplementary content to read C - 8. Lectures slides
    ##  Min.   :1.037                        Min.   :2.760         
    ##  1st Qu.:4.147                        1st Qu.:5.519         
    ##  Median :4.147                        Median :6.899         
    ##  Mean   :4.323                        Mean   :6.347         
    ##  3rd Qu.:5.184                        3rd Qu.:6.899         
    ##  Max.   :5.184                        Max.   :6.899         
    ##  NA's   :1                            NA's   :1             
    ##  C - 9. Lecture notes on some of the lecture slides
    ##  Min.   :3.146                                     
    ##  1st Qu.:6.293                                     
    ##  Median :7.866                                     
    ##  Mean   :7.237                                     
    ##  3rd Qu.:7.866                                     
    ##  Max.   :7.866                                     
    ##  NA's   :1                                         
    ##  C - 10. The quality of the lectures given (quality measured by the breadth (the full span of knowledge of a subject) and depth (the extent to which specific topics are focused upon, amplified, and explored) of learning - NOT quality measured by how fun/comical/lively the lectures are)
    ##  Min.   :3.040                                                                                                                                                                                                                                                                                
    ##  1st Qu.:6.081                                                                                                                                                                                                                                                                                
    ##  Median :7.601                                                                                                                                                                                                                                                                                
    ##  Mean   :6.902                                                                                                                                                                                                                                                                                
    ##  3rd Qu.:7.601                                                                                                                                                                                                                                                                                
    ##  Max.   :7.601                                                                                                                                                                                                                                                                                
    ##  NA's   :1                                                                                                                                                                                                                                                                                    
    ##  C - 11. The division of theory and practice such that most of the theory is done during the recorded online classes and most of the practice is done during the physical classes
    ##  Min.   :2.903                                                                                                                                                                   
    ##  1st Qu.:5.806                                                                                                                                                                   
    ##  Median :7.257                                                                                                                                                                   
    ##  Mean   :6.517                                                                                                                                                                   
    ##  3rd Qu.:7.257                                                                                                                                                                   
    ##  Max.   :7.257                                                                                                                                                                   
    ##  NA's   :1                                                                                                                                                                       
    ##  C - 12. The recordings of online classes
    ##  Min.   :2.343                           
    ##  1st Qu.:4.687                           
    ##  Median :5.859                           
    ##  Mean   :5.074                           
    ##  3rd Qu.:5.859                           
    ##  Max.   :5.859                           
    ##  NA's   :1                               
    ##  D - 1. Write two things you like about the teaching and learning in this unit so far.
    ##  Length:101                                                                           
    ##  Class :character                                                                     
    ##  Mode  :character                                                                     
    ##                                                                                       
    ##                                                                                       
    ##                                                                                       
    ##                                                                                       
    ##  D - 2. Write at least one recommendation to improve the teaching and learning in this unit (for the remaining weeks in the semester)
    ##  Length:101                                                                                                                          
    ##  Class :character                                                                                                                    
    ##  Mode  :character                                                                                                                    
    ##                                                                                                                                      
    ##                                                                                                                                      
    ##                                                                                                                                      
    ##                                                                                                                                      
    ##  Average Course Evaluation Rating Average Level of Learning Attained Rating
    ##  Min.   : 7.267                   Min.   :2.833                            
    ##  1st Qu.:10.674                   1st Qu.:4.957                            
    ##  Median :11.355                   Median :5.666                            
    ##  Mean   :11.319                   Mean   :5.800                            
    ##  3rd Qu.:12.264                   3rd Qu.:6.374                            
    ##  Max.   :12.491                   Max.   :7.082                            
    ##  NA's   :1                        NA's   :1                                
    ##  Average Pedagogical Strategy Effectiveness Rating
    ##  Min.   :6.297                                    
    ##  1st Qu.:8.051                                    
    ##  Median :8.995                                    
    ##  Mean   :8.770                                    
    ##  3rd Qu.:9.715                                    
    ##  Max.   :9.895                                    
    ##  NA's   :1                                        
    ##  Project: Section 1-4: (20%) x/10 Project: Section 5-11: (50%) x/10
    ##  Min.   :0.000                    Min.   :0.000                    
    ##  1st Qu.:3.521                    1st Qu.:2.151                    
    ##  Median :4.044                    Median :2.797                    
    ##  Mean   :3.811                    Mean   :2.360                    
    ##  3rd Qu.:4.282                    3rd Qu.:2.976                    
    ##  Max.   :4.758                    Max.   :3.585                    
    ##                                                                    
    ##  Project: Section 12: (30%) x/5 Project: (10%): x/30 x 100 TOTAL
    ##  Min.   :0.0000                 Min.   :0.000                   
    ##  1st Qu.:0.0000                 1st Qu.:2.779                   
    ##  Median :0.0000                 Median :3.295                   
    ##  Mean   :0.5683                 Mean   :3.096                   
    ##  3rd Qu.:0.6998                 3rd Qu.:3.553                   
    ##  Max.   :2.7993                 Max.   :4.962                   
    ##  NA's   :1                                                      
    ##  Quiz 1 on Concept 1 (Introduction) x/32 Quiz 3 on Concept 3 (Linear) x/15
    ##  Min.   :0.7302                          Min.   :0.9661                   
    ##  1st Qu.:1.7724                          1st Qu.:2.2543                   
    ##  Median :2.3565                          Median :2.8984                   
    ##  Mean   :2.5144                          Mean   :3.0692                   
    ##  3rd Qu.:3.0175                          3rd Qu.:3.8646                   
    ##  Max.   :4.8038                          Max.   :4.8307                   
    ##                                          NA's   :2                        
    ##  Quiz 4 on Concept 4 (Non-Linear) x/22 Quiz 5 on Concept 5 (Dashboarding) x/10
    ##  Min.   :0.6769                        Min.   :0.000                          
    ##  1st Qu.:2.4628                        1st Qu.:2.381                          
    ##  Median :3.0461                        Median :3.014                          
    ##  Mean   :3.1444                        Mean   :3.032                          
    ##  3rd Qu.:3.9486                        3rd Qu.:3.809                          
    ##  Max.   :4.9640                        Max.   :6.033                          
    ##  NA's   :6                             NA's   :12                             
    ##  Quizzes and  Bonus Marks (7%): x/79 x 100 TOTAL
    ##  Min.   :1.592                                  
    ##  1st Qu.:2.657                                  
    ##  Median :3.353                                  
    ##  Mean   :3.408                                  
    ##  3rd Qu.:3.951                                  
    ##  Max.   :5.775                                  
    ##                                                 
    ##  Lab 1 - 2.c. - (Simple Linear Regression) x/5
    ##  Min.   : 7.634                               
    ##  1st Qu.:12.723                               
    ##  Median :12.723                               
    ##  Mean   :12.464                               
    ##  3rd Qu.:12.723                               
    ##  Max.   :12.723                               
    ##  NA's   :3                                    
    ##  Lab 2 - 2.e. -  (Linear Regression using Gradient Descent) x/5
    ##  Min.   :2.078                                                 
    ##  1st Qu.:3.044                                                 
    ##  Median :4.687                                                 
    ##  Mean   :4.026                                                 
    ##  3rd Qu.:4.832                                                 
    ##  Max.   :4.832                                                 
    ##  NA's   :6                                                     
    ##  Lab 3 - 2.g. - (Logistic Regression using Gradient Descent) x/5
    ##  Min.   :4.450                                                  
    ##  1st Qu.:7.572                                                  
    ##  Median :7.572                                                  
    ##  Mean   :7.229                                                  
    ##  3rd Qu.:7.572                                                  
    ##  Max.   :7.806                                                  
    ##  NA's   :9                                                      
    ##  Lab 4 - 2.h. - (Linear Discriminant Analysis) x/5
    ##  Min.   :2.054                                    
    ##  1st Qu.:4.552                                    
    ##  Median :5.385                                    
    ##  Mean   :4.913                                    
    ##  3rd Qu.:5.551                                    
    ##  Max.   :5.551                                    
    ##  NA's   :18                                       
    ##  Lab 5 - Chart JS Dashboard Setup x/5 Lab Work (7%) x/25 x 100
    ##  Min.   :0.000                        Min.   :0.9221          
    ##  1st Qu.:0.000                        1st Qu.:3.6678          
    ##  Median :2.143                        Median :4.1444          
    ##  Mean   :1.459                        Mean   :4.1297          
    ##  3rd Qu.:2.143                        3rd Qu.:5.0355          
    ##  Max.   :2.143                        Max.   :5.1805          
    ##                                                               
    ##  CAT 1 (8%): x/38 x 100 CAT 2 (8%): x/100 x 100
    ##  Min.   :2.175          Min.   :0.000          
    ##  1st Qu.:3.915          1st Qu.:2.067          
    ##  Median :4.610          Median :2.574          
    ##  Mean   :4.588          Mean   :2.518          
    ##  3rd Qu.:5.480          3rd Qu.:3.314          
    ##  Max.   :6.437          Max.   :4.053          
    ##  NA's   :4              NA's   :31             
    ##  Attendance Waiver Granted: 1 = Yes, 0 = No Absenteeism Percentage
    ##  Min.   :0.0000                             Min.   :0.0000        
    ##  1st Qu.:0.0000                             1st Qu.:0.8153        
    ##  Median :0.0000                             Median :1.6295        
    ##  Mean   :0.2271                             Mean   :1.6961        
    ##  3rd Qu.:0.0000                             3rd Qu.:2.4448        
    ##  Max.   :4.5871                             Max.   :5.7049        
    ##                                                                   
    ##  Coursework TOTAL: x/40 (40%) EXAM: x/60 (60%)
    ##  Min.   :1.200                Min.   :0.4441  
    ##  1st Qu.:3.284                1st Qu.:2.3094  
    ##  Median :3.949                Median :3.0200  
    ##  Mean   :3.941                Mean   :3.0145  
    ##  3rd Qu.:4.709                3rd Qu.:3.7306  
    ##  Max.   :5.636                Max.   :4.9742  
    ##                               NA's   :4       
    ##  TOTAL = Coursework TOTAL + EXAM (100%)    GRADE          
    ##  Min.   :0.475                          Length:101        
    ##  1st Qu.:2.896                          Class :character  
    ##  Median :3.732                          Mode  :character  
    ##  Mean   :3.632                                            
    ##  3rd Qu.:4.377                                            
    ##  Max.   :5.578                                            
    ## 

``` r
student_performance_scale_transform <- as.data.frame(student_performance_scale_transform)  # Convert to data frame if needed
preprocessed_data <- preProcess(student_performance_scale_transform)



hist(student_performance_scale_transform[,2],
     main = names(student_performance_scale_transform)[2])
```

![](BIProject-Template_files/figure-gfm/Apply%20Scale%20Data%20Transform-13.png)<!-- -->

``` r
hist(student_performance_scale_transform[,3],
     main = names(student_performance_scale_transform)[3])
```

![](BIProject-Template_files/figure-gfm/Apply%20Scale%20Data%20Transform-14.png)<!-- -->

``` r
hist(student_performance_scale_transform[,5],
     main = names(student_performance_scale_transform)[5])
```

![](BIProject-Template_files/figure-gfm/Apply%20Scale%20Data%20Transform-15.png)<!-- -->

``` r
hist(student_performance_scale_transform[,6],
     main = names(student_performance_scale_transform)[6])
```

![](BIProject-Template_files/figure-gfm/Apply%20Scale%20Data%20Transform-16.png)<!-- -->

``` r
hist(student_performance_scale_transform[,7],
     main = names(student_performance_scale_transform)[7])
```

![](BIProject-Template_files/figure-gfm/Apply%20Scale%20Data%20Transform-17.png)<!-- -->

``` r
hist(student_performance_scale_transform[,8],
     main = names(student_performance_scale_transform)[8])
```

![](BIProject-Template_files/figure-gfm/Apply%20Scale%20Data%20Transform-18.png)<!-- -->

``` r
hist(student_performance_scale_transform[,9],
     main = names(student_performance_scale_transform)[9])
```

![](BIProject-Template_files/figure-gfm/Apply%20Scale%20Data%20Transform-19.png)<!-- -->

``` r
hist(student_performance_scale_transform[,10],
     main = names(student_performance_scale_transform)[10])
```

![](BIProject-Template_files/figure-gfm/Apply%20Scale%20Data%20Transform-20.png)<!-- -->

``` r
hist(student_performance_scale_transform[,11],
     main = names(student_performance_scale_transform)[11])
```

![](BIProject-Template_files/figure-gfm/Apply%20Scale%20Data%20Transform-21.png)<!-- -->

``` r
hist(student_performance_scale_transform[,12],
     main = names(student_performance_scale_transform)[12])
```

![](BIProject-Template_files/figure-gfm/Apply%20Scale%20Data%20Transform-22.png)<!-- -->

``` r
hist(student_performance_scale_transform[,13],
     main = names(student_performance_scale_transform)[13])
```

![](BIProject-Template_files/figure-gfm/Apply%20Scale%20Data%20Transform-23.png)<!-- -->

``` r
hist(student_performance_scale_transform[,14],
     main = names(student_performance_scale_transform)[14])
```

![](BIProject-Template_files/figure-gfm/Apply%20Scale%20Data%20Transform-24.png)<!-- -->

# Applying the Center Data Transform

``` r
### The Centre Basic Transform on the Student Performance Dataset ----
# BEFORE
summary(StudentPerformanceDataset)
```

    ##  class_group            gender            YOB       regret_choosing_bi
    ##  Length:101         Min.   :0.0000   Min.   :1998   Min.   :0.0000    
    ##  Class :character   1st Qu.:0.0000   1st Qu.:2000   1st Qu.:0.0000    
    ##  Mode  :character   Median :1.0000   Median :2001   Median :0.0000    
    ##                     Mean   :0.5743   Mean   :2001   Mean   :0.0198    
    ##                     3rd Qu.:1.0000   3rd Qu.:2002   3rd Qu.:0.0000    
    ##                     Max.   :1.0000   Max.   :2003   Max.   :1.0000    
    ##                                                                       
    ##   drop_bi_now       motivator      read_content_before_lecture
    ##  Min.   :0.0000   Min.   :0.0000   Min.   :1.000              
    ##  1st Qu.:0.0000   1st Qu.:1.0000   1st Qu.:2.000              
    ##  Median :0.0000   Median :1.0000   Median :3.000              
    ##  Mean   :0.0198   Mean   :0.7525   Mean   :2.752              
    ##  3rd Qu.:0.0000   3rd Qu.:1.0000   3rd Qu.:3.000              
    ##  Max.   :1.0000   Max.   :1.0000   Max.   :5.000              
    ##                                                               
    ##  anticipate_test_questions answer_rhetorical_questions find_terms_I_do_not_know
    ##  Min.   :1.000             Min.   :1.000               Min.   :1.000           
    ##  1st Qu.:3.000             1st Qu.:3.000               1st Qu.:3.000           
    ##  Median :4.000             Median :4.000               Median :4.000           
    ##  Mean   :3.584             Mean   :3.426               Mean   :3.743           
    ##  3rd Qu.:4.000             3rd Qu.:4.000               3rd Qu.:5.000           
    ##  Max.   :5.000             Max.   :5.000               Max.   :5.000           
    ##                                                                                
    ##  copy_new_terms_in_reading_notebook take_quizzes_and_use_results
    ##  Min.   :1.000                      Min.   :1.000               
    ##  1st Qu.:3.000                      1st Qu.:3.000               
    ##  Median :4.000                      Median :4.000               
    ##  Mean   :3.663                      Mean   :3.941               
    ##  3rd Qu.:4.000                      3rd Qu.:5.000               
    ##  Max.   :5.000                      Max.   :5.000               
    ##                                                                 
    ##  reorganise_course_outline write_down_important_points space_out_revision
    ##  Min.   :1.000             Min.   :1.000               Min.   :1.000     
    ##  1st Qu.:3.000             1st Qu.:3.000               1st Qu.:3.000     
    ##  Median :3.000             Median :4.000               Median :3.000     
    ##  Mean   :3.376             Mean   :3.832               Mean   :3.228     
    ##  3rd Qu.:4.000             3rd Qu.:5.000               3rd Qu.:4.000     
    ##  Max.   :5.000             Max.   :5.000               Max.   :5.000     
    ##                                                                          
    ##  studying_in_study_group schedule_appointments goal_oriented  
    ##  Min.   :1.000           Min.   :1.000         Min.   :0.000  
    ##  1st Qu.:1.000           1st Qu.:1.000         1st Qu.:0.000  
    ##  Median :2.000           Median :2.000         Median :0.000  
    ##  Mean   :2.455           Mean   :1.931         Mean   :0.198  
    ##  3rd Qu.:3.000           3rd Qu.:2.000         3rd Qu.:0.000  
    ##  Max.   :5.000           Max.   :5.000         Max.   :1.000  
    ##                                                               
    ##  spaced_repetition testing_and_active_recall  interleaving    categorizing  
    ##  Min.   :1.000     Min.   :1.000             Min.   :1.000   Min.   :1.000  
    ##  1st Qu.:2.000     1st Qu.:3.000             1st Qu.:2.000   1st Qu.:2.000  
    ##  Median :3.000     Median :3.000             Median :2.000   Median :3.000  
    ##  Mean   :2.554     Mean   :3.059             Mean   :2.257   Mean   :2.713  
    ##  3rd Qu.:3.000     3rd Qu.:4.000             3rd Qu.:3.000   3rd Qu.:3.000  
    ##  Max.   :4.000     Max.   :4.000             Max.   :4.000   Max.   :4.000  
    ##                                                                             
    ##  retrospective_timetable cornell_notes        sq3r          commute    
    ##  Min.   :1.000           Min.   :1.000   Min.   :1.000   Min.   :1.00  
    ##  1st Qu.:2.000           1st Qu.:2.000   1st Qu.:2.000   1st Qu.:2.00  
    ##  Median :2.000           Median :3.000   Median :3.000   Median :3.00  
    ##  Mean   :2.406           Mean   :2.545   Mean   :2.614   Mean   :2.73  
    ##  3rd Qu.:3.000           3rd Qu.:3.000   3rd Qu.:3.000   3rd Qu.:4.00  
    ##  Max.   :4.000           Max.   :4.000   Max.   :4.000   Max.   :4.00  
    ##                                                          NA's   :1     
    ##    study_time   repeats_since_Y1  paid_tuition   free_tuition  extra_curricular
    ##  Min.   :1.00   Min.   : 0.00    Min.   :0.00   Min.   :0.00   Min.   :0.00    
    ##  1st Qu.:1.00   1st Qu.: 0.00    1st Qu.:0.00   1st Qu.:0.00   1st Qu.:0.00    
    ##  Median :2.00   Median : 2.00    Median :0.00   Median :0.00   Median :1.00    
    ##  Mean   :1.75   Mean   : 2.05    Mean   :0.11   Mean   :0.27   Mean   :0.53    
    ##  3rd Qu.:2.00   3rd Qu.: 3.00    3rd Qu.:0.00   3rd Qu.:1.00   3rd Qu.:1.00    
    ##  Max.   :4.00   Max.   :10.00    Max.   :1.00   Max.   :1.00   Max.   :1.00    
    ##  NA's   :1      NA's   :1        NA's   :1      NA's   :1      NA's   :1       
    ##  sports_extra_curricular exercise_per_week    meditate         pray     
    ##  Min.   :0.00            Min.   :0.0       Min.   :0.00   Min.   :0.00  
    ##  1st Qu.:0.00            1st Qu.:1.0       1st Qu.:0.00   1st Qu.:1.00  
    ##  Median :0.00            Median :1.0       Median :1.00   Median :2.00  
    ##  Mean   :0.36            Mean   :1.1       Mean   :0.76   Mean   :2.09  
    ##  3rd Qu.:1.00            3rd Qu.:2.0       3rd Qu.:1.00   3rd Qu.:3.00  
    ##  Max.   :1.00            Max.   :3.0       Max.   :3.00   Max.   :3.00  
    ##  NA's   :1               NA's   :1         NA's   :1      NA's   :1     
    ##     internet        laptop  family_relationships  friendships  
    ##  Min.   :0.00   Min.   :1   Min.   :2.00         Min.   :2.00  
    ##  1st Qu.:1.00   1st Qu.:1   1st Qu.:4.00         1st Qu.:4.00  
    ##  Median :1.00   Median :1   Median :4.00         Median :4.00  
    ##  Mean   :0.87   Mean   :1   Mean   :4.19         Mean   :4.01  
    ##  3rd Qu.:1.00   3rd Qu.:1   3rd Qu.:5.00         3rd Qu.:4.00  
    ##  Max.   :1.00   Max.   :1   Max.   :5.00         Max.   :5.00  
    ##  NA's   :1      NA's   :1   NA's   :1            NA's   :1     
    ##  romantic_relationships spiritual_wellnes financial_wellness     health    
    ##  Min.   :0.00           Min.   :1.00      Min.   :1.00       Min.   :1.00  
    ##  1st Qu.:0.00           1st Qu.:3.00      1st Qu.:2.00       1st Qu.:3.00  
    ##  Median :0.00           Median :4.00      Median :3.00       Median :4.00  
    ##  Mean   :1.37           Mean   :3.65      Mean   :3.03       Mean   :4.04  
    ##  3rd Qu.:3.00           3rd Qu.:4.00      3rd Qu.:4.00       3rd Qu.:5.00  
    ##  Max.   :4.00           Max.   :5.00      Max.   :5.00       Max.   :5.00  
    ##  NA's   :1              NA's   :1         NA's   :1          NA's   :1     
    ##     day_out      night_out    alcohol_or_narcotics     mentor    
    ##  Min.   :0.0   Min.   :0.00   Min.   :0.00         Min.   :0.00  
    ##  1st Qu.:0.0   1st Qu.:0.00   1st Qu.:0.00         1st Qu.:0.00  
    ##  Median :1.0   Median :0.00   Median :0.00         Median :0.00  
    ##  Mean   :0.8   Mean   :0.51   Mean   :0.35         Mean   :0.41  
    ##  3rd Qu.:1.0   3rd Qu.:1.00   3rd Qu.:1.00         3rd Qu.:1.00  
    ##  Max.   :3.0   Max.   :3.00   Max.   :3.00         Max.   :1.00  
    ##  NA's   :1     NA's   :1      NA's   :1            NA's   :1     
    ##  mentor_meetings A - 1. I am enjoying the subject
    ##  Min.   :0.00    Min.   :3.00                    
    ##  1st Qu.:0.00    1st Qu.:4.00                    
    ##  Median :0.00    Median :5.00                    
    ##  Mean   :0.68    Mean   :4.49                    
    ##  3rd Qu.:1.00    3rd Qu.:5.00                    
    ##  Max.   :3.00    Max.   :5.00                    
    ##  NA's   :1       NA's   :1                       
    ##  A - 2. Classes start and end on time
    ##  Min.   :3.00                        
    ##  1st Qu.:4.00                        
    ##  Median :5.00                        
    ##  Mean   :4.68                        
    ##  3rd Qu.:5.00                        
    ##  Max.   :5.00                        
    ##  NA's   :1                           
    ##  A - 3. The learning environment is participative, involves learning by doing and is group-based
    ##  Min.   :3.00                                                                                   
    ##  1st Qu.:4.00                                                                                   
    ##  Median :4.00                                                                                   
    ##  Mean   :4.35                                                                                   
    ##  3rd Qu.:5.00                                                                                   
    ##  Max.   :5.00                                                                                   
    ##  NA's   :1                                                                                      
    ##  A - 4. The subject content is delivered according to the course outline and meets my expectations
    ##  Min.   :3.00                                                                                     
    ##  1st Qu.:4.75                                                                                     
    ##  Median :5.00                                                                                     
    ##  Mean   :4.74                                                                                     
    ##  3rd Qu.:5.00                                                                                     
    ##  Max.   :5.00                                                                                     
    ##  NA's   :1                                                                                        
    ##  A - 5. The topics are clear and logically developed
    ##  Min.   :2.00                                       
    ##  1st Qu.:4.00                                       
    ##  Median :5.00                                       
    ##  Mean   :4.65                                       
    ##  3rd Qu.:5.00                                       
    ##  Max.   :5.00                                       
    ##  NA's   :1                                          
    ##  A - 6. I am developing my oral and writing skills
    ##  Min.   :1.00                                     
    ##  1st Qu.:4.00                                     
    ##  Median :4.00                                     
    ##  Mean   :4.11                                     
    ##  3rd Qu.:5.00                                     
    ##  Max.   :5.00                                     
    ##  NA's   :1                                        
    ##  A - 7. I am developing my reflective and critical reasoning skills
    ##  Min.   :2.00                                                      
    ##  1st Qu.:4.00                                                      
    ##  Median :4.00                                                      
    ##  Mean   :4.38                                                      
    ##  3rd Qu.:5.00                                                      
    ##  Max.   :5.00                                                      
    ##  NA's   :1                                                         
    ##  A - 8. The assessment methods are assisting me to learn
    ##  Min.   :1.00                                           
    ##  1st Qu.:4.00                                           
    ##  Median :5.00                                           
    ##  Mean   :4.61                                           
    ##  3rd Qu.:5.00                                           
    ##  Max.   :5.00                                           
    ##  NA's   :1                                              
    ##  A - 9. I receive relevant feedback
    ##  Min.   :3.00                      
    ##  1st Qu.:4.00                      
    ##  Median :5.00                      
    ##  Mean   :4.58                      
    ##  3rd Qu.:5.00                      
    ##  Max.   :5.00                      
    ##  NA's   :1                         
    ##  A - 10. I read the recommended readings and notes
    ##  Min.   :3.00                                     
    ##  1st Qu.:4.00                                     
    ##  Median :5.00                                     
    ##  Mean   :4.55                                     
    ##  3rd Qu.:5.00                                     
    ##  Max.   :5.00                                     
    ##  NA's   :1                                        
    ##  A - 11. I use the eLearning material posted
    ##  Min.   :3.0                                
    ##  1st Qu.:4.0                                
    ##  Median :5.0                                
    ##  Mean   :4.7                                
    ##  3rd Qu.:5.0                                
    ##  Max.   :5.0                                
    ##  NA's   :1                                  
    ##  B - 1. Concept 1 of 6: Principles of Business Intelligence and the DataOps Philosophy
    ##  Min.   :1.00                                                                         
    ##  1st Qu.:4.00                                                                         
    ##  Median :4.00                                                                         
    ##  Mean   :4.25                                                                         
    ##  3rd Qu.:5.00                                                                         
    ##  Max.   :5.00                                                                         
    ##  NA's   :1                                                                            
    ##  B - 2. Concept 3 of 6: Linear Algorithms for Predictive Analytics
    ##  Min.   :2.00                                                     
    ##  1st Qu.:3.00                                                     
    ##  Median :4.00                                                     
    ##  Mean   :3.94                                                     
    ##  3rd Qu.:5.00                                                     
    ##  Max.   :5.00                                                     
    ##  NA's   :1                                                        
    ##  C - 2. Quizzes at the end of each concept
    ##  Min.   :2.00                             
    ##  1st Qu.:4.00                             
    ##  Median :5.00                             
    ##  Mean   :4.59                             
    ##  3rd Qu.:5.00                             
    ##  Max.   :5.00                             
    ##  NA's   :1                                
    ##  C - 3. Lab manuals that outline the steps to follow during the labs
    ##  Min.   :3.00                                                       
    ##  1st Qu.:4.00                                                       
    ##  Median :5.00                                                       
    ##  Mean   :4.61                                                       
    ##  3rd Qu.:5.00                                                       
    ##  Max.   :5.00                                                       
    ##  NA's   :1                                                          
    ##  C - 4. Required lab work submissions at the end of each lab manual that outline the activity to be done on your own
    ##  Min.   :3.00                                                                                                       
    ##  1st Qu.:4.00                                                                                                       
    ##  Median :5.00                                                                                                       
    ##  Mean   :4.55                                                                                                       
    ##  3rd Qu.:5.00                                                                                                       
    ##  Max.   :5.00                                                                                                       
    ##  NA's   :1                                                                                                          
    ##  C - 5. Supplementary videos to watch
    ##  Min.   :1.00                        
    ##  1st Qu.:4.00                        
    ##  Median :4.00                        
    ##  Mean   :4.19                        
    ##  3rd Qu.:5.00                        
    ##  Max.   :5.00                        
    ##  NA's   :1                           
    ##  C - 6. Supplementary podcasts to listen to
    ##  Min.   :1.00                              
    ##  1st Qu.:4.00                              
    ##  Median :4.00                              
    ##  Mean   :4.08                              
    ##  3rd Qu.:5.00                              
    ##  Max.   :5.00                              
    ##  NA's   :1                                 
    ##  C - 7. Supplementary content to read C - 8. Lectures slides
    ##  Min.   :1.00                         Min.   :2.0           
    ##  1st Qu.:4.00                         1st Qu.:4.0           
    ##  Median :4.00                         Median :5.0           
    ##  Mean   :4.17                         Mean   :4.6           
    ##  3rd Qu.:5.00                         3rd Qu.:5.0           
    ##  Max.   :5.00                         Max.   :5.0           
    ##  NA's   :1                            NA's   :1             
    ##  C - 9. Lecture notes on some of the lecture slides
    ##  Min.   :2.0                                       
    ##  1st Qu.:4.0                                       
    ##  Median :5.0                                       
    ##  Mean   :4.6                                       
    ##  3rd Qu.:5.0                                       
    ##  Max.   :5.0                                       
    ##  NA's   :1                                         
    ##  C - 10. The quality of the lectures given (quality measured by the breadth (the full span of knowledge of a subject) and depth (the extent to which specific topics are focused upon, amplified, and explored) of learning - NOT quality measured by how fun/comical/lively the lectures are)
    ##  Min.   :2.00                                                                                                                                                                                                                                                                                 
    ##  1st Qu.:4.00                                                                                                                                                                                                                                                                                 
    ##  Median :5.00                                                                                                                                                                                                                                                                                 
    ##  Mean   :4.54                                                                                                                                                                                                                                                                                 
    ##  3rd Qu.:5.00                                                                                                                                                                                                                                                                                 
    ##  Max.   :5.00                                                                                                                                                                                                                                                                                 
    ##  NA's   :1                                                                                                                                                                                                                                                                                    
    ##  C - 11. The division of theory and practice such that most of the theory is done during the recorded online classes and most of the practice is done during the physical classes
    ##  Min.   :2.00                                                                                                                                                                    
    ##  1st Qu.:4.00                                                                                                                                                                    
    ##  Median :5.00                                                                                                                                                                    
    ##  Mean   :4.49                                                                                                                                                                    
    ##  3rd Qu.:5.00                                                                                                                                                                    
    ##  Max.   :5.00                                                                                                                                                                    
    ##  NA's   :1                                                                                                                                                                       
    ##  C - 12. The recordings of online classes
    ##  Min.   :2.00                            
    ##  1st Qu.:4.00                            
    ##  Median :5.00                            
    ##  Mean   :4.33                            
    ##  3rd Qu.:5.00                            
    ##  Max.   :5.00                            
    ##  NA's   :1                               
    ##  D - 1. Write two things you like about the teaching and learning in this unit so far.
    ##  Length:101                                                                           
    ##  Class :character                                                                     
    ##  Mode  :character                                                                     
    ##                                                                                       
    ##                                                                                       
    ##                                                                                       
    ##                                                                                       
    ##  D - 2. Write at least one recommendation to improve the teaching and learning in this unit (for the remaining weeks in the semester)
    ##  Length:101                                                                                                                          
    ##  Class :character                                                                                                                    
    ##  Mode  :character                                                                                                                    
    ##                                                                                                                                      
    ##                                                                                                                                      
    ##                                                                                                                                      
    ##                                                                                                                                      
    ##  Average Course Evaluation Rating Average Level of Learning Attained Rating
    ##  Min.   :2.909                    Min.   :2.000                            
    ##  1st Qu.:4.273                    1st Qu.:3.500                            
    ##  Median :4.545                    Median :4.000                            
    ##  Mean   :4.531                    Mean   :4.095                            
    ##  3rd Qu.:4.909                    3rd Qu.:4.500                            
    ##  Max.   :5.000                    Max.   :5.000                            
    ##  NA's   :1                        NA's   :1                                
    ##  Average Pedagogical Strategy Effectiveness Rating
    ##  Min.   :3.182                                    
    ##  1st Qu.:4.068                                    
    ##  Median :4.545                                    
    ##  Mean   :4.432                                    
    ##  3rd Qu.:4.909                                    
    ##  Max.   :5.000                                    
    ##  NA's   :1                                        
    ##  Project: Section 1-4: (20%) x/10 Project: Section 5-11: (50%) x/10
    ##  Min.   : 0.000                   Min.   : 0.000                   
    ##  1st Qu.: 7.400                   1st Qu.: 6.000                   
    ##  Median : 8.500                   Median : 7.800                   
    ##  Mean   : 8.011                   Mean   : 6.582                   
    ##  3rd Qu.: 9.000                   3rd Qu.: 8.300                   
    ##  Max.   :10.000                   Max.   :10.000                   
    ##                                                                    
    ##  Project: Section 12: (30%) x/5 Project: (10%): x/30 x 100 TOTAL
    ##  Min.   :0.000                  Min.   :  0.00                  
    ##  1st Qu.:0.000                  1st Qu.: 56.00                  
    ##  Median :0.000                  Median : 66.40                  
    ##  Mean   :1.015                  Mean   : 62.39                  
    ##  3rd Qu.:1.250                  3rd Qu.: 71.60                  
    ##  Max.   :5.000                  Max.   :100.00                  
    ##  NA's   :1                                                      
    ##  Quiz 1 on Concept 1 (Introduction) x/32 Quiz 3 on Concept 3 (Linear) x/15
    ##  Min.   : 4.75                           Min.   : 3.00                    
    ##  1st Qu.:11.53                           1st Qu.: 7.00                    
    ##  Median :15.33                           Median : 9.00                    
    ##  Mean   :16.36                           Mean   : 9.53                    
    ##  3rd Qu.:19.63                           3rd Qu.:12.00                    
    ##  Max.   :31.25                           Max.   :15.00                    
    ##                                          NA's   :2                        
    ##  Quiz 4 on Concept 4 (Non-Linear) x/22 Quiz 5 on Concept 5 (Dashboarding) x/10
    ##  Min.   : 3.00                         Min.   : 0.000                         
    ##  1st Qu.:10.91                         1st Qu.: 5.000                         
    ##  Median :13.50                         Median : 6.330                         
    ##  Mean   :13.94                         Mean   : 6.367                         
    ##  3rd Qu.:17.50                         3rd Qu.: 8.000                         
    ##  Max.   :22.00                         Max.   :12.670                         
    ##  NA's   :6                             NA's   :12                             
    ##  Quizzes and  Bonus Marks (7%): x/79 x 100 TOTAL
    ##  Min.   :26.26                                  
    ##  1st Qu.:43.82                                  
    ##  Median :55.31                                  
    ##  Mean   :56.22                                  
    ##  3rd Qu.:65.16                                  
    ##  Max.   :95.25                                  
    ##                                                 
    ##  Lab 1 - 2.c. - (Simple Linear Regression) x/5
    ##  Min.   :3.000                                
    ##  1st Qu.:5.000                                
    ##  Median :5.000                                
    ##  Mean   :4.898                                
    ##  3rd Qu.:5.000                                
    ##  Max.   :5.000                                
    ##  NA's   :3                                    
    ##  Lab 2 - 2.e. -  (Linear Regression using Gradient Descent) x/5
    ##  Min.   :2.150                                                 
    ##  1st Qu.:3.150                                                 
    ##  Median :4.850                                                 
    ##  Mean   :4.166                                                 
    ##  3rd Qu.:5.000                                                 
    ##  Max.   :5.000                                                 
    ##  NA's   :6                                                     
    ##  Lab 3 - 2.g. - (Logistic Regression using Gradient Descent) x/5
    ##  Min.   :2.85                                                   
    ##  1st Qu.:4.85                                                   
    ##  Median :4.85                                                   
    ##  Mean   :4.63                                                   
    ##  3rd Qu.:4.85                                                   
    ##  Max.   :5.00                                                   
    ##  NA's   :9                                                      
    ##  Lab 4 - 2.h. - (Linear Discriminant Analysis) x/5
    ##  Min.   :1.850                                    
    ##  1st Qu.:4.100                                    
    ##  Median :4.850                                    
    ##  Mean   :4.425                                    
    ##  3rd Qu.:5.000                                    
    ##  Max.   :5.000                                    
    ##  NA's   :18                                       
    ##  Lab 5 - Chart JS Dashboard Setup x/5 Lab Work (7%) x/25 x 100
    ##  Min.   :0.000                        Min.   : 17.80          
    ##  1st Qu.:0.000                        1st Qu.: 70.80          
    ##  Median :5.000                        Median : 80.00          
    ##  Mean   :3.404                        Mean   : 79.72          
    ##  3rd Qu.:5.000                        3rd Qu.: 97.20          
    ##  Max.   :5.000                        Max.   :100.00          
    ##                                                               
    ##  CAT 1 (8%): x/38 x 100 CAT 2 (8%): x/100 x 100
    ##  Min.   :32.89          Min.   :  0.00         
    ##  1st Qu.:59.21          1st Qu.: 51.00         
    ##  Median :69.73          Median : 63.50         
    ##  Mean   :69.39          Mean   : 62.13         
    ##  3rd Qu.:82.89          3rd Qu.: 81.75         
    ##  Max.   :97.36          Max.   :100.00         
    ##  NA's   :4              NA's   :31             
    ##  Attendance Waiver Granted: 1 = Yes, 0 = No Absenteeism Percentage
    ##  Min.   :0.00000                            Min.   : 0.00         
    ##  1st Qu.:0.00000                            1st Qu.: 7.41         
    ##  Median :0.00000                            Median :14.81         
    ##  Mean   :0.04951                            Mean   :15.42         
    ##  3rd Qu.:0.00000                            3rd Qu.:22.22         
    ##  Max.   :1.00000                            Max.   :51.85         
    ##                                                                   
    ##  Coursework TOTAL: x/40 (40%) EXAM: x/60 (60%)
    ##  Min.   : 7.47                Min.   : 5.00   
    ##  1st Qu.:20.44                1st Qu.:26.00   
    ##  Median :24.58                Median :34.00   
    ##  Mean   :24.53                Mean   :33.94   
    ##  3rd Qu.:29.31                3rd Qu.:42.00   
    ##  Max.   :35.08                Max.   :56.00   
    ##                               NA's   :4       
    ##  TOTAL = Coursework TOTAL + EXAM (100%)    GRADE          
    ##  Min.   : 7.47                          Length:101        
    ##  1st Qu.:45.54                          Class :character  
    ##  Median :58.69                          Mode  :character  
    ##  Mean   :57.12                                            
    ##  3rd Qu.:68.83                                            
    ##  Max.   :87.72                                            
    ## 

``` r
boxplot(StudentPerformanceDataset[,2], main = names(StudentPerformanceDataset)[2])
```

![](BIProject-Template_files/figure-gfm/Apply%20Center%20Data%20Transform-1.png)<!-- -->

``` r
boxplot(StudentPerformanceDataset[,4], main = names(StudentPerformanceDataset)[3])
```

![](BIProject-Template_files/figure-gfm/Apply%20Center%20Data%20Transform-2.png)<!-- -->

``` r
boxplot(StudentPerformanceDataset[,5], main = names(StudentPerformanceDataset)[5])
```

![](BIProject-Template_files/figure-gfm/Apply%20Center%20Data%20Transform-3.png)<!-- -->

``` r
boxplot(StudentPerformanceDataset[,6], main = names(StudentPerformanceDataset)[6])
```

![](BIProject-Template_files/figure-gfm/Apply%20Center%20Data%20Transform-4.png)<!-- -->

``` r
boxplot(StudentPerformanceDataset[,7], main = names(StudentPerformanceDataset)[7])
```

![](BIProject-Template_files/figure-gfm/Apply%20Center%20Data%20Transform-5.png)<!-- -->

``` r
boxplot(StudentPerformanceDataset[,8], main = names(StudentPerformanceDataset)[8])
```

![](BIProject-Template_files/figure-gfm/Apply%20Center%20Data%20Transform-6.png)<!-- -->

``` r
boxplot(StudentPerformanceDataset[,9], main = names(StudentPerformanceDataset)[9])
```

![](BIProject-Template_files/figure-gfm/Apply%20Center%20Data%20Transform-7.png)<!-- -->

``` r
boxplot(StudentPerformanceDataset[,10], main = names(StudentPerformanceDataset)[10])
```

![](BIProject-Template_files/figure-gfm/Apply%20Center%20Data%20Transform-8.png)<!-- -->

``` r
boxplot(StudentPerformanceDataset[,11], main = names(StudentPerformanceDataset)[11])
```

![](BIProject-Template_files/figure-gfm/Apply%20Center%20Data%20Transform-9.png)<!-- -->

``` r
boxplot(StudentPerformanceDataset[,12], main = names(StudentPerformanceDataset)[12])
```

![](BIProject-Template_files/figure-gfm/Apply%20Center%20Data%20Transform-10.png)<!-- -->

``` r
boxplot(StudentPerformanceDataset[,13], main = names(StudentPerformanceDataset)[13])
```

![](BIProject-Template_files/figure-gfm/Apply%20Center%20Data%20Transform-11.png)<!-- -->

``` r
boxplot(StudentPerformanceDataset[,14], main = names(StudentPerformanceDataset)[14])
```

![](BIProject-Template_files/figure-gfm/Apply%20Center%20Data%20Transform-12.png)<!-- -->

``` r
model_of_the_transform <- preProcess(StudentPerformanceDataset, method = c("center"))
print(model_of_the_transform)
```

    ## Created from 51 samples and 100 variables
    ## 
    ## Pre-processing:
    ##   - centered (96)
    ##   - ignored (4)

``` r
student_performance_center_transform <- predict(model_of_the_transform, # nolint
                                                StudentPerformanceDataset)

# AFTER
summary(student_performance_center_transform)
```

    ##  class_group            gender             YOB           regret_choosing_bi
    ##  Length:101         Min.   :-0.5743   Min.   :-2.90099   Min.   :-0.0198   
    ##  Class :character   1st Qu.:-0.5743   1st Qu.:-0.90099   1st Qu.:-0.0198   
    ##  Mode  :character   Median : 0.4257   Median : 0.09901   Median :-0.0198   
    ##                     Mean   : 0.0000   Mean   : 0.00000   Mean   : 0.0000   
    ##                     3rd Qu.: 0.4257   3rd Qu.: 1.09901   3rd Qu.:-0.0198   
    ##                     Max.   : 0.4257   Max.   : 2.09901   Max.   : 0.9802   
    ##                                                                            
    ##   drop_bi_now        motivator       read_content_before_lecture
    ##  Min.   :-0.0198   Min.   :-0.7525   Min.   :-1.7525            
    ##  1st Qu.:-0.0198   1st Qu.: 0.2475   1st Qu.:-0.7525            
    ##  Median :-0.0198   Median : 0.2475   Median : 0.2475            
    ##  Mean   : 0.0000   Mean   : 0.0000   Mean   : 0.0000            
    ##  3rd Qu.:-0.0198   3rd Qu.: 0.2475   3rd Qu.: 0.2475            
    ##  Max.   : 0.9802   Max.   : 0.2475   Max.   : 2.2475            
    ##                                                                 
    ##  anticipate_test_questions answer_rhetorical_questions find_terms_I_do_not_know
    ##  Min.   :-2.5842           Min.   :-2.4257             Min.   :-2.7426         
    ##  1st Qu.:-0.5842           1st Qu.:-0.4257             1st Qu.:-0.7426         
    ##  Median : 0.4158           Median : 0.5743             Median : 0.2574         
    ##  Mean   : 0.0000           Mean   : 0.0000             Mean   : 0.0000         
    ##  3rd Qu.: 0.4158           3rd Qu.: 0.5743             3rd Qu.: 1.2574         
    ##  Max.   : 1.4158           Max.   : 1.5743             Max.   : 1.2574         
    ##                                                                                
    ##  copy_new_terms_in_reading_notebook take_quizzes_and_use_results
    ##  Min.   :-2.6634                    Min.   :-2.94059            
    ##  1st Qu.:-0.6634                    1st Qu.:-0.94059            
    ##  Median : 0.3366                    Median : 0.05941            
    ##  Mean   : 0.0000                    Mean   : 0.00000            
    ##  3rd Qu.: 0.3366                    3rd Qu.: 1.05941            
    ##  Max.   : 1.3366                    Max.   : 1.05941            
    ##                                                                 
    ##  reorganise_course_outline write_down_important_points space_out_revision
    ##  Min.   :-2.3762           Min.   :-2.8317             Min.   :-2.2277   
    ##  1st Qu.:-0.3762           1st Qu.:-0.8317             1st Qu.:-0.2277   
    ##  Median :-0.3762           Median : 0.1683             Median :-0.2277   
    ##  Mean   : 0.0000           Mean   : 0.0000             Mean   : 0.0000   
    ##  3rd Qu.: 0.6238           3rd Qu.: 1.1683             3rd Qu.: 0.7723   
    ##  Max.   : 1.6238           Max.   : 1.1683             Max.   : 1.7723   
    ##                                                                          
    ##  studying_in_study_group schedule_appointments goal_oriented   
    ##  Min.   :-1.4554         Min.   :-0.93069      Min.   :-0.198  
    ##  1st Qu.:-1.4554         1st Qu.:-0.93069      1st Qu.:-0.198  
    ##  Median :-0.4554         Median : 0.06931      Median :-0.198  
    ##  Mean   : 0.0000         Mean   : 0.00000      Mean   : 0.000  
    ##  3rd Qu.: 0.5446         3rd Qu.: 0.06931      3rd Qu.:-0.198  
    ##  Max.   : 2.5446         Max.   : 3.06931      Max.   : 0.802  
    ##                                                                
    ##  spaced_repetition testing_and_active_recall  interleaving    
    ##  Min.   :-1.5545   Min.   :-2.05941          Min.   :-1.2574  
    ##  1st Qu.:-0.5545   1st Qu.:-0.05941          1st Qu.:-0.2574  
    ##  Median : 0.4455   Median :-0.05941          Median :-0.2574  
    ##  Mean   : 0.0000   Mean   : 0.00000          Mean   : 0.0000  
    ##  3rd Qu.: 0.4455   3rd Qu.: 0.94059          3rd Qu.: 0.7426  
    ##  Max.   : 1.4455   Max.   : 0.94059          Max.   : 1.7426  
    ##                                                               
    ##   categorizing     retrospective_timetable cornell_notes          sq3r        
    ##  Min.   :-1.7129   Min.   :-1.4059         Min.   :-1.5446   Min.   :-1.6139  
    ##  1st Qu.:-0.7129   1st Qu.:-0.4059         1st Qu.:-0.5446   1st Qu.:-0.6139  
    ##  Median : 0.2871   Median :-0.4059         Median : 0.4554   Median : 0.3861  
    ##  Mean   : 0.0000   Mean   : 0.0000         Mean   : 0.0000   Mean   : 0.0000  
    ##  3rd Qu.: 0.2871   3rd Qu.: 0.5941         3rd Qu.: 0.4554   3rd Qu.: 0.3861  
    ##  Max.   : 1.2871   Max.   : 1.5941         Max.   : 1.4554   Max.   : 1.3861  
    ##                                                                               
    ##     commute        study_time    repeats_since_Y1  paid_tuition  
    ##  Min.   :-1.73   Min.   :-0.75   Min.   :-2.05    Min.   :-0.11  
    ##  1st Qu.:-0.73   1st Qu.:-0.75   1st Qu.:-2.05    1st Qu.:-0.11  
    ##  Median : 0.27   Median : 0.25   Median :-0.05    Median :-0.11  
    ##  Mean   : 0.00   Mean   : 0.00   Mean   : 0.00    Mean   : 0.00  
    ##  3rd Qu.: 1.27   3rd Qu.: 0.25   3rd Qu.: 0.95    3rd Qu.:-0.11  
    ##  Max.   : 1.27   Max.   : 2.25   Max.   : 7.95    Max.   : 0.89  
    ##  NA's   :1       NA's   :1       NA's   :1        NA's   :1      
    ##   free_tuition   extra_curricular sports_extra_curricular exercise_per_week
    ##  Min.   :-0.27   Min.   :-0.53    Min.   :-0.36           Min.   :-1.1     
    ##  1st Qu.:-0.27   1st Qu.:-0.53    1st Qu.:-0.36           1st Qu.:-0.1     
    ##  Median :-0.27   Median : 0.47    Median :-0.36           Median :-0.1     
    ##  Mean   : 0.00   Mean   : 0.00    Mean   : 0.00           Mean   : 0.0     
    ##  3rd Qu.: 0.73   3rd Qu.: 0.47    3rd Qu.: 0.64           3rd Qu.: 0.9     
    ##  Max.   : 0.73   Max.   : 0.47    Max.   : 0.64           Max.   : 1.9     
    ##  NA's   :1       NA's   :1        NA's   :1               NA's   :1        
    ##     meditate          pray          internet         laptop 
    ##  Min.   :-0.76   Min.   :-2.09   Min.   :-0.87   Min.   :0  
    ##  1st Qu.:-0.76   1st Qu.:-1.09   1st Qu.: 0.13   1st Qu.:0  
    ##  Median : 0.24   Median :-0.09   Median : 0.13   Median :0  
    ##  Mean   : 0.00   Mean   : 0.00   Mean   : 0.00   Mean   :0  
    ##  3rd Qu.: 0.24   3rd Qu.: 0.91   3rd Qu.: 0.13   3rd Qu.:0  
    ##  Max.   : 2.24   Max.   : 0.91   Max.   : 0.13   Max.   :0  
    ##  NA's   :1       NA's   :1       NA's   :1       NA's   :1  
    ##  family_relationships  friendships    romantic_relationships spiritual_wellnes
    ##  Min.   :-2.19        Min.   :-2.01   Min.   :-1.37          Min.   :-2.65    
    ##  1st Qu.:-0.19        1st Qu.:-0.01   1st Qu.:-1.37          1st Qu.:-0.65    
    ##  Median :-0.19        Median :-0.01   Median :-1.37          Median : 0.35    
    ##  Mean   : 0.00        Mean   : 0.00   Mean   : 0.00          Mean   : 0.00    
    ##  3rd Qu.: 0.81        3rd Qu.:-0.01   3rd Qu.: 1.63          3rd Qu.: 0.35    
    ##  Max.   : 0.81        Max.   : 0.99   Max.   : 2.63          Max.   : 1.35    
    ##  NA's   :1            NA's   :1       NA's   :1              NA's   :1        
    ##  financial_wellness     health         day_out       night_out    
    ##  Min.   :-2.03      Min.   :-3.04   Min.   :-0.8   Min.   :-0.51  
    ##  1st Qu.:-1.03      1st Qu.:-1.04   1st Qu.:-0.8   1st Qu.:-0.51  
    ##  Median :-0.03      Median :-0.04   Median : 0.2   Median :-0.51  
    ##  Mean   : 0.00      Mean   : 0.00   Mean   : 0.0   Mean   : 0.00  
    ##  3rd Qu.: 0.97      3rd Qu.: 0.96   3rd Qu.: 0.2   3rd Qu.: 0.49  
    ##  Max.   : 1.97      Max.   : 0.96   Max.   : 2.2   Max.   : 2.49  
    ##  NA's   :1          NA's   :1       NA's   :1      NA's   :1      
    ##  alcohol_or_narcotics     mentor      mentor_meetings
    ##  Min.   :-0.35        Min.   :-0.41   Min.   :-0.68  
    ##  1st Qu.:-0.35        1st Qu.:-0.41   1st Qu.:-0.68  
    ##  Median :-0.35        Median :-0.41   Median :-0.68  
    ##  Mean   : 0.00        Mean   : 0.00   Mean   : 0.00  
    ##  3rd Qu.: 0.65        3rd Qu.: 0.59   3rd Qu.: 0.32  
    ##  Max.   : 2.65        Max.   : 0.59   Max.   : 2.32  
    ##  NA's   :1            NA's   :1       NA's   :1      
    ##  A - 1. I am enjoying the subject A - 2. Classes start and end on time
    ##  Min.   :-1.49                    Min.   :-1.68                       
    ##  1st Qu.:-0.49                    1st Qu.:-0.68                       
    ##  Median : 0.51                    Median : 0.32                       
    ##  Mean   : 0.00                    Mean   : 0.00                       
    ##  3rd Qu.: 0.51                    3rd Qu.: 0.32                       
    ##  Max.   : 0.51                    Max.   : 0.32                       
    ##  NA's   :1                        NA's   :1                           
    ##  A - 3. The learning environment is participative, involves learning by doing and is group-based
    ##  Min.   :-1.35                                                                                  
    ##  1st Qu.:-0.35                                                                                  
    ##  Median :-0.35                                                                                  
    ##  Mean   : 0.00                                                                                  
    ##  3rd Qu.: 0.65                                                                                  
    ##  Max.   : 0.65                                                                                  
    ##  NA's   :1                                                                                      
    ##  A - 4. The subject content is delivered according to the course outline and meets my expectations
    ##  Min.   :-1.74                                                                                    
    ##  1st Qu.: 0.01                                                                                    
    ##  Median : 0.26                                                                                    
    ##  Mean   : 0.00                                                                                    
    ##  3rd Qu.: 0.26                                                                                    
    ##  Max.   : 0.26                                                                                    
    ##  NA's   :1                                                                                        
    ##  A - 5. The topics are clear and logically developed
    ##  Min.   :-2.65                                      
    ##  1st Qu.:-0.65                                      
    ##  Median : 0.35                                      
    ##  Mean   : 0.00                                      
    ##  3rd Qu.: 0.35                                      
    ##  Max.   : 0.35                                      
    ##  NA's   :1                                          
    ##  A - 6. I am developing my oral and writing skills
    ##  Min.   :-3.11                                    
    ##  1st Qu.:-0.11                                    
    ##  Median :-0.11                                    
    ##  Mean   : 0.00                                    
    ##  3rd Qu.: 0.89                                    
    ##  Max.   : 0.89                                    
    ##  NA's   :1                                        
    ##  A - 7. I am developing my reflective and critical reasoning skills
    ##  Min.   :-2.38                                                     
    ##  1st Qu.:-0.38                                                     
    ##  Median :-0.38                                                     
    ##  Mean   : 0.00                                                     
    ##  3rd Qu.: 0.62                                                     
    ##  Max.   : 0.62                                                     
    ##  NA's   :1                                                         
    ##  A - 8. The assessment methods are assisting me to learn
    ##  Min.   :-3.61                                          
    ##  1st Qu.:-0.61                                          
    ##  Median : 0.39                                          
    ##  Mean   : 0.00                                          
    ##  3rd Qu.: 0.39                                          
    ##  Max.   : 0.39                                          
    ##  NA's   :1                                              
    ##  A - 9. I receive relevant feedback
    ##  Min.   :-1.58                     
    ##  1st Qu.:-0.58                     
    ##  Median : 0.42                     
    ##  Mean   : 0.00                     
    ##  3rd Qu.: 0.42                     
    ##  Max.   : 0.42                     
    ##  NA's   :1                         
    ##  A - 10. I read the recommended readings and notes
    ##  Min.   :-1.55                                    
    ##  1st Qu.:-0.55                                    
    ##  Median : 0.45                                    
    ##  Mean   : 0.00                                    
    ##  3rd Qu.: 0.45                                    
    ##  Max.   : 0.45                                    
    ##  NA's   :1                                        
    ##  A - 11. I use the eLearning material posted
    ##  Min.   :-1.7                               
    ##  1st Qu.:-0.7                               
    ##  Median : 0.3                               
    ##  Mean   : 0.0                               
    ##  3rd Qu.: 0.3                               
    ##  Max.   : 0.3                               
    ##  NA's   :1                                  
    ##  B - 1. Concept 1 of 6: Principles of Business Intelligence and the DataOps Philosophy
    ##  Min.   :-3.25                                                                        
    ##  1st Qu.:-0.25                                                                        
    ##  Median :-0.25                                                                        
    ##  Mean   : 0.00                                                                        
    ##  3rd Qu.: 0.75                                                                        
    ##  Max.   : 0.75                                                                        
    ##  NA's   :1                                                                            
    ##  B - 2. Concept 3 of 6: Linear Algorithms for Predictive Analytics
    ##  Min.   :-1.94                                                    
    ##  1st Qu.:-0.94                                                    
    ##  Median : 0.06                                                    
    ##  Mean   : 0.00                                                    
    ##  3rd Qu.: 1.06                                                    
    ##  Max.   : 1.06                                                    
    ##  NA's   :1                                                        
    ##  C - 2. Quizzes at the end of each concept
    ##  Min.   :-2.59                            
    ##  1st Qu.:-0.59                            
    ##  Median : 0.41                            
    ##  Mean   : 0.00                            
    ##  3rd Qu.: 0.41                            
    ##  Max.   : 0.41                            
    ##  NA's   :1                                
    ##  C - 3. Lab manuals that outline the steps to follow during the labs
    ##  Min.   :-1.61                                                      
    ##  1st Qu.:-0.61                                                      
    ##  Median : 0.39                                                      
    ##  Mean   : 0.00                                                      
    ##  3rd Qu.: 0.39                                                      
    ##  Max.   : 0.39                                                      
    ##  NA's   :1                                                          
    ##  C - 4. Required lab work submissions at the end of each lab manual that outline the activity to be done on your own
    ##  Min.   :-1.55                                                                                                      
    ##  1st Qu.:-0.55                                                                                                      
    ##  Median : 0.45                                                                                                      
    ##  Mean   : 0.00                                                                                                      
    ##  3rd Qu.: 0.45                                                                                                      
    ##  Max.   : 0.45                                                                                                      
    ##  NA's   :1                                                                                                          
    ##  C - 5. Supplementary videos to watch
    ##  Min.   :-3.19                       
    ##  1st Qu.:-0.19                       
    ##  Median :-0.19                       
    ##  Mean   : 0.00                       
    ##  3rd Qu.: 0.81                       
    ##  Max.   : 0.81                       
    ##  NA's   :1                           
    ##  C - 6. Supplementary podcasts to listen to
    ##  Min.   :-3.08                             
    ##  1st Qu.:-0.08                             
    ##  Median :-0.08                             
    ##  Mean   : 0.00                             
    ##  3rd Qu.: 0.92                             
    ##  Max.   : 0.92                             
    ##  NA's   :1                                 
    ##  C - 7. Supplementary content to read C - 8. Lectures slides
    ##  Min.   :-3.17                        Min.   :-2.6          
    ##  1st Qu.:-0.17                        1st Qu.:-0.6          
    ##  Median :-0.17                        Median : 0.4          
    ##  Mean   : 0.00                        Mean   : 0.0          
    ##  3rd Qu.: 0.83                        3rd Qu.: 0.4          
    ##  Max.   : 0.83                        Max.   : 0.4          
    ##  NA's   :1                            NA's   :1             
    ##  C - 9. Lecture notes on some of the lecture slides
    ##  Min.   :-2.6                                      
    ##  1st Qu.:-0.6                                      
    ##  Median : 0.4                                      
    ##  Mean   : 0.0                                      
    ##  3rd Qu.: 0.4                                      
    ##  Max.   : 0.4                                      
    ##  NA's   :1                                         
    ##  C - 10. The quality of the lectures given (quality measured by the breadth (the full span of knowledge of a subject) and depth (the extent to which specific topics are focused upon, amplified, and explored) of learning - NOT quality measured by how fun/comical/lively the lectures are)
    ##  Min.   :-2.54                                                                                                                                                                                                                                                                                
    ##  1st Qu.:-0.54                                                                                                                                                                                                                                                                                
    ##  Median : 0.46                                                                                                                                                                                                                                                                                
    ##  Mean   : 0.00                                                                                                                                                                                                                                                                                
    ##  3rd Qu.: 0.46                                                                                                                                                                                                                                                                                
    ##  Max.   : 0.46                                                                                                                                                                                                                                                                                
    ##  NA's   :1                                                                                                                                                                                                                                                                                    
    ##  C - 11. The division of theory and practice such that most of the theory is done during the recorded online classes and most of the practice is done during the physical classes
    ##  Min.   :-2.49                                                                                                                                                                   
    ##  1st Qu.:-0.49                                                                                                                                                                   
    ##  Median : 0.51                                                                                                                                                                   
    ##  Mean   : 0.00                                                                                                                                                                   
    ##  3rd Qu.: 0.51                                                                                                                                                                   
    ##  Max.   : 0.51                                                                                                                                                                   
    ##  NA's   :1                                                                                                                                                                       
    ##  C - 12. The recordings of online classes
    ##  Min.   :-2.33                           
    ##  1st Qu.:-0.33                           
    ##  Median : 0.67                           
    ##  Mean   : 0.00                           
    ##  3rd Qu.: 0.67                           
    ##  Max.   : 0.67                           
    ##  NA's   :1                               
    ##  D - 1. Write two things you like about the teaching and learning in this unit so far.
    ##  Length:101                                                                           
    ##  Class :character                                                                     
    ##  Mode  :character                                                                     
    ##                                                                                       
    ##                                                                                       
    ##                                                                                       
    ##                                                                                       
    ##  D - 2. Write at least one recommendation to improve the teaching and learning in this unit (for the remaining weeks in the semester)
    ##  Length:101                                                                                                                          
    ##  Class :character                                                                                                                    
    ##  Mode  :character                                                                                                                    
    ##                                                                                                                                      
    ##                                                                                                                                      
    ##                                                                                                                                      
    ##                                                                                                                                      
    ##  Average Course Evaluation Rating Average Level of Learning Attained Rating
    ##  Min.   :-1.62181                 Min.   :-2.095                           
    ##  1st Qu.:-0.25821                 1st Qu.:-0.595                           
    ##  Median : 0.01459                 Median :-0.095                           
    ##  Mean   : 0.00000                 Mean   : 0.000                           
    ##  3rd Qu.: 0.37819                 3rd Qu.: 0.405                           
    ##  Max.   : 0.46909                 Max.   : 0.905                           
    ##  NA's   :1                        NA's   :1                                
    ##  Average Pedagogical Strategy Effectiveness Rating
    ##  Min.   :-1.2500                                  
    ##  1st Qu.:-0.3636                                  
    ##  Median : 0.1137                                  
    ##  Mean   : 0.0000                                  
    ##  3rd Qu.: 0.4773                                  
    ##  Max.   : 0.5682                                  
    ##  NA's   :1                                        
    ##  Project: Section 1-4: (20%) x/10 Project: Section 5-11: (50%) x/10
    ##  Min.   :-8.0109                  Min.   :-6.5822                  
    ##  1st Qu.:-0.6109                  1st Qu.:-0.5822                  
    ##  Median : 0.4891                  Median : 1.2178                  
    ##  Mean   : 0.0000                  Mean   : 0.0000                  
    ##  3rd Qu.: 0.9891                  3rd Qu.: 1.7178                  
    ##  Max.   : 1.9891                  Max.   : 3.4178                  
    ##                                                                    
    ##  Project: Section 12: (30%) x/5 Project: (10%): x/30 x 100 TOTAL
    ##  Min.   :-1.015                 Min.   :-62.392                 
    ##  1st Qu.:-1.015                 1st Qu.: -6.392                 
    ##  Median :-1.015                 Median :  4.008                 
    ##  Mean   : 0.000                 Mean   :  0.000                 
    ##  3rd Qu.: 0.235                 3rd Qu.:  9.208                 
    ##  Max.   : 3.985                 Max.   : 37.608                 
    ##  NA's   :1                                                      
    ##  Quiz 1 on Concept 1 (Introduction) x/32 Quiz 3 on Concept 3 (Linear) x/15
    ##  Min.   :-11.607                         Min.   :-6.5303                  
    ##  1st Qu.: -4.827                         1st Qu.:-2.5303                  
    ##  Median : -1.027                         Median :-0.5303                  
    ##  Mean   :  0.000                         Mean   : 0.0000                  
    ##  3rd Qu.:  3.273                         3rd Qu.: 2.4697                  
    ##  Max.   : 14.893                         Max.   : 5.4697                  
    ##                                          NA's   :2                        
    ##  Quiz 4 on Concept 4 (Non-Linear) x/22 Quiz 5 on Concept 5 (Dashboarding) x/10
    ##  Min.   :-10.9357                      Min.   :-6.36742                       
    ##  1st Qu.: -3.0207                      1st Qu.:-1.36742                       
    ##  Median : -0.4357                      Median :-0.03742                       
    ##  Mean   :  0.0000                      Mean   : 0.00000                       
    ##  3rd Qu.:  3.5643                      3rd Qu.: 1.63258                       
    ##  Max.   :  8.0643                      Max.   : 6.30258                       
    ##  NA's   :6                             NA's   :12                             
    ##  Quizzes and  Bonus Marks (7%): x/79 x 100 TOTAL
    ##  Min.   :-29.9592                               
    ##  1st Qu.:-12.3992                               
    ##  Median : -0.9092                               
    ##  Mean   :  0.0000                               
    ##  3rd Qu.:  8.9408                               
    ##  Max.   : 39.0308                               
    ##                                                 
    ##  Lab 1 - 2.c. - (Simple Linear Regression) x/5
    ##  Min.   :-1.898                               
    ##  1st Qu.: 0.102                               
    ##  Median : 0.102                               
    ##  Mean   : 0.000                               
    ##  3rd Qu.: 0.102                               
    ##  Max.   : 0.102                               
    ##  NA's   :3                                    
    ##  Lab 2 - 2.e. -  (Linear Regression using Gradient Descent) x/5
    ##  Min.   :-2.0163                                               
    ##  1st Qu.:-1.0163                                               
    ##  Median : 0.6837                                               
    ##  Mean   : 0.0000                                               
    ##  3rd Qu.: 0.8337                                               
    ##  Max.   : 0.8337                                               
    ##  NA's   :6                                                     
    ##  Lab 3 - 2.g. - (Logistic Regression using Gradient Descent) x/5
    ##  Min.   :-1.7802                                                
    ##  1st Qu.: 0.2198                                                
    ##  Median : 0.2198                                                
    ##  Mean   : 0.0000                                                
    ##  3rd Qu.: 0.2198                                                
    ##  Max.   : 0.3698                                                
    ##  NA's   :9                                                      
    ##  Lab 4 - 2.h. - (Linear Discriminant Analysis) x/5
    ##  Min.   :-2.5747                                  
    ##  1st Qu.:-0.3247                                  
    ##  Median : 0.4253                                  
    ##  Mean   : 0.0000                                  
    ##  3rd Qu.: 0.5753                                  
    ##  Max.   : 0.5753                                  
    ##  NA's   :18                                       
    ##  Lab 5 - Chart JS Dashboard Setup x/5 Lab Work (7%) x/25 x 100
    ##  Min.   :-3.404                       Min.   :-61.916         
    ##  1st Qu.:-3.404                       1st Qu.: -8.916         
    ##  Median : 1.596                       Median :  0.284         
    ##  Mean   : 0.000                       Mean   :  0.000         
    ##  3rd Qu.: 1.596                       3rd Qu.: 17.484         
    ##  Max.   : 1.596                       Max.   : 20.284         
    ##                                                               
    ##  CAT 1 (8%): x/38 x 100 CAT 2 (8%): x/100 x 100
    ##  Min.   :-36.5033       Min.   :-62.129        
    ##  1st Qu.:-10.1833       1st Qu.:-11.129        
    ##  Median :  0.3367       Median :  1.371        
    ##  Mean   :  0.0000       Mean   :  0.000        
    ##  3rd Qu.: 13.4967       3rd Qu.: 19.621        
    ##  Max.   : 27.9667       Max.   : 37.871        
    ##  NA's   :4              NA's   :31             
    ##  Attendance Waiver Granted: 1 = Yes, 0 = No Absenteeism Percentage
    ##  Min.   :-0.04951                           Min.   :-15.4155      
    ##  1st Qu.:-0.04951                           1st Qu.: -8.0055      
    ##  Median :-0.04951                           Median : -0.6055      
    ##  Mean   : 0.00000                           Mean   :  0.0000      
    ##  3rd Qu.:-0.04951                           3rd Qu.:  6.8045      
    ##  Max.   : 0.95049                           Max.   : 36.4345      
    ##                                                                   
    ##  Coursework TOTAL: x/40 (40%) EXAM: x/60 (60%)   
    ##  Min.   :-17.05604            Min.   :-28.93814  
    ##  1st Qu.: -4.08604            1st Qu.: -7.93814  
    ##  Median :  0.05396            Median :  0.06186  
    ##  Mean   :  0.00000            Mean   :  0.00000  
    ##  3rd Qu.:  4.78396            3rd Qu.:  8.06186  
    ##  Max.   : 10.55396            Max.   : 22.06186  
    ##                               NA's   :4          
    ##  TOTAL = Coursework TOTAL + EXAM (100%)    GRADE          
    ##  Min.   :-49.65                         Length:101        
    ##  1st Qu.:-11.58                         Class :character  
    ##  Median :  1.57                         Mode  :character  
    ##  Mean   :  0.00                                           
    ##  3rd Qu.: 11.71                                           
    ##  Max.   : 30.60                                           
    ## 

``` r
boxplot(student_performance_center_transform[,2],
        main = names(student_performance_center_transform)[2])
```

![](BIProject-Template_files/figure-gfm/Apply%20Center%20Data%20Transform-13.png)<!-- -->

``` r
boxplot(student_performance_center_transform[,3],
        main = names(student_performance_center_transform)[3])
```

![](BIProject-Template_files/figure-gfm/Apply%20Center%20Data%20Transform-14.png)<!-- -->

``` r
boxplot(student_performance_center_transform[,5],
        main = names(student_performance_center_transform)[5])
```

![](BIProject-Template_files/figure-gfm/Apply%20Center%20Data%20Transform-15.png)<!-- -->

``` r
boxplot(student_performance_center_transform[,6],
        main = names(student_performance_center_transform)[6])
```

![](BIProject-Template_files/figure-gfm/Apply%20Center%20Data%20Transform-16.png)<!-- -->

``` r
boxplot(student_performance_center_transform[,7],
        main = names(student_performance_center_transform)[7])
```

![](BIProject-Template_files/figure-gfm/Apply%20Center%20Data%20Transform-17.png)<!-- -->

``` r
boxplot(student_performance_center_transform[,8],
        main = names(student_performance_center_transform)[8])
```

![](BIProject-Template_files/figure-gfm/Apply%20Center%20Data%20Transform-18.png)<!-- -->

``` r
boxplot(student_performance_center_transform[,9],
        main = names(student_performance_center_transform)[9])
```

![](BIProject-Template_files/figure-gfm/Apply%20Center%20Data%20Transform-19.png)<!-- -->

``` r
boxplot(student_performance_center_transform[,10],
        main = names(student_performance_center_transform)[10])
```

![](BIProject-Template_files/figure-gfm/Apply%20Center%20Data%20Transform-20.png)<!-- -->

``` r
boxplot(student_performance_center_transform[,11],
        main = names(student_performance_center_transform)[11])
```

![](BIProject-Template_files/figure-gfm/Apply%20Center%20Data%20Transform-21.png)<!-- -->

``` r
boxplot(student_performance_center_transform[,12],
        main = names(student_performance_center_transform)[12])
```

![](BIProject-Template_files/figure-gfm/Apply%20Center%20Data%20Transform-22.png)<!-- -->

``` r
boxplot(student_performance_center_transform[,13],
        main = names(student_performance_center_transform)[13])
```

![](BIProject-Template_files/figure-gfm/Apply%20Center%20Data%20Transform-23.png)<!-- -->

``` r
boxplot(student_performance_center_transform[,14],
        main = names(student_performance_center_transform)[14])
```

![](BIProject-Template_files/figure-gfm/Apply%20Center%20Data%20Transform-24.png)<!-- -->
\# Standardization of the Student Performance Dataset

``` r
### The Standardize Basic Transform on the Student Performance Dataset ----
# BEFORE
summary(StudentPerformanceDataset)
```

    ##  class_group            gender            YOB       regret_choosing_bi
    ##  Length:101         Min.   :0.0000   Min.   :1998   Min.   :0.0000    
    ##  Class :character   1st Qu.:0.0000   1st Qu.:2000   1st Qu.:0.0000    
    ##  Mode  :character   Median :1.0000   Median :2001   Median :0.0000    
    ##                     Mean   :0.5743   Mean   :2001   Mean   :0.0198    
    ##                     3rd Qu.:1.0000   3rd Qu.:2002   3rd Qu.:0.0000    
    ##                     Max.   :1.0000   Max.   :2003   Max.   :1.0000    
    ##                                                                       
    ##   drop_bi_now       motivator      read_content_before_lecture
    ##  Min.   :0.0000   Min.   :0.0000   Min.   :1.000              
    ##  1st Qu.:0.0000   1st Qu.:1.0000   1st Qu.:2.000              
    ##  Median :0.0000   Median :1.0000   Median :3.000              
    ##  Mean   :0.0198   Mean   :0.7525   Mean   :2.752              
    ##  3rd Qu.:0.0000   3rd Qu.:1.0000   3rd Qu.:3.000              
    ##  Max.   :1.0000   Max.   :1.0000   Max.   :5.000              
    ##                                                               
    ##  anticipate_test_questions answer_rhetorical_questions find_terms_I_do_not_know
    ##  Min.   :1.000             Min.   :1.000               Min.   :1.000           
    ##  1st Qu.:3.000             1st Qu.:3.000               1st Qu.:3.000           
    ##  Median :4.000             Median :4.000               Median :4.000           
    ##  Mean   :3.584             Mean   :3.426               Mean   :3.743           
    ##  3rd Qu.:4.000             3rd Qu.:4.000               3rd Qu.:5.000           
    ##  Max.   :5.000             Max.   :5.000               Max.   :5.000           
    ##                                                                                
    ##  copy_new_terms_in_reading_notebook take_quizzes_and_use_results
    ##  Min.   :1.000                      Min.   :1.000               
    ##  1st Qu.:3.000                      1st Qu.:3.000               
    ##  Median :4.000                      Median :4.000               
    ##  Mean   :3.663                      Mean   :3.941               
    ##  3rd Qu.:4.000                      3rd Qu.:5.000               
    ##  Max.   :5.000                      Max.   :5.000               
    ##                                                                 
    ##  reorganise_course_outline write_down_important_points space_out_revision
    ##  Min.   :1.000             Min.   :1.000               Min.   :1.000     
    ##  1st Qu.:3.000             1st Qu.:3.000               1st Qu.:3.000     
    ##  Median :3.000             Median :4.000               Median :3.000     
    ##  Mean   :3.376             Mean   :3.832               Mean   :3.228     
    ##  3rd Qu.:4.000             3rd Qu.:5.000               3rd Qu.:4.000     
    ##  Max.   :5.000             Max.   :5.000               Max.   :5.000     
    ##                                                                          
    ##  studying_in_study_group schedule_appointments goal_oriented  
    ##  Min.   :1.000           Min.   :1.000         Min.   :0.000  
    ##  1st Qu.:1.000           1st Qu.:1.000         1st Qu.:0.000  
    ##  Median :2.000           Median :2.000         Median :0.000  
    ##  Mean   :2.455           Mean   :1.931         Mean   :0.198  
    ##  3rd Qu.:3.000           3rd Qu.:2.000         3rd Qu.:0.000  
    ##  Max.   :5.000           Max.   :5.000         Max.   :1.000  
    ##                                                               
    ##  spaced_repetition testing_and_active_recall  interleaving    categorizing  
    ##  Min.   :1.000     Min.   :1.000             Min.   :1.000   Min.   :1.000  
    ##  1st Qu.:2.000     1st Qu.:3.000             1st Qu.:2.000   1st Qu.:2.000  
    ##  Median :3.000     Median :3.000             Median :2.000   Median :3.000  
    ##  Mean   :2.554     Mean   :3.059             Mean   :2.257   Mean   :2.713  
    ##  3rd Qu.:3.000     3rd Qu.:4.000             3rd Qu.:3.000   3rd Qu.:3.000  
    ##  Max.   :4.000     Max.   :4.000             Max.   :4.000   Max.   :4.000  
    ##                                                                             
    ##  retrospective_timetable cornell_notes        sq3r          commute    
    ##  Min.   :1.000           Min.   :1.000   Min.   :1.000   Min.   :1.00  
    ##  1st Qu.:2.000           1st Qu.:2.000   1st Qu.:2.000   1st Qu.:2.00  
    ##  Median :2.000           Median :3.000   Median :3.000   Median :3.00  
    ##  Mean   :2.406           Mean   :2.545   Mean   :2.614   Mean   :2.73  
    ##  3rd Qu.:3.000           3rd Qu.:3.000   3rd Qu.:3.000   3rd Qu.:4.00  
    ##  Max.   :4.000           Max.   :4.000   Max.   :4.000   Max.   :4.00  
    ##                                                          NA's   :1     
    ##    study_time   repeats_since_Y1  paid_tuition   free_tuition  extra_curricular
    ##  Min.   :1.00   Min.   : 0.00    Min.   :0.00   Min.   :0.00   Min.   :0.00    
    ##  1st Qu.:1.00   1st Qu.: 0.00    1st Qu.:0.00   1st Qu.:0.00   1st Qu.:0.00    
    ##  Median :2.00   Median : 2.00    Median :0.00   Median :0.00   Median :1.00    
    ##  Mean   :1.75   Mean   : 2.05    Mean   :0.11   Mean   :0.27   Mean   :0.53    
    ##  3rd Qu.:2.00   3rd Qu.: 3.00    3rd Qu.:0.00   3rd Qu.:1.00   3rd Qu.:1.00    
    ##  Max.   :4.00   Max.   :10.00    Max.   :1.00   Max.   :1.00   Max.   :1.00    
    ##  NA's   :1      NA's   :1        NA's   :1      NA's   :1      NA's   :1       
    ##  sports_extra_curricular exercise_per_week    meditate         pray     
    ##  Min.   :0.00            Min.   :0.0       Min.   :0.00   Min.   :0.00  
    ##  1st Qu.:0.00            1st Qu.:1.0       1st Qu.:0.00   1st Qu.:1.00  
    ##  Median :0.00            Median :1.0       Median :1.00   Median :2.00  
    ##  Mean   :0.36            Mean   :1.1       Mean   :0.76   Mean   :2.09  
    ##  3rd Qu.:1.00            3rd Qu.:2.0       3rd Qu.:1.00   3rd Qu.:3.00  
    ##  Max.   :1.00            Max.   :3.0       Max.   :3.00   Max.   :3.00  
    ##  NA's   :1               NA's   :1         NA's   :1      NA's   :1     
    ##     internet        laptop  family_relationships  friendships  
    ##  Min.   :0.00   Min.   :1   Min.   :2.00         Min.   :2.00  
    ##  1st Qu.:1.00   1st Qu.:1   1st Qu.:4.00         1st Qu.:4.00  
    ##  Median :1.00   Median :1   Median :4.00         Median :4.00  
    ##  Mean   :0.87   Mean   :1   Mean   :4.19         Mean   :4.01  
    ##  3rd Qu.:1.00   3rd Qu.:1   3rd Qu.:5.00         3rd Qu.:4.00  
    ##  Max.   :1.00   Max.   :1   Max.   :5.00         Max.   :5.00  
    ##  NA's   :1      NA's   :1   NA's   :1            NA's   :1     
    ##  romantic_relationships spiritual_wellnes financial_wellness     health    
    ##  Min.   :0.00           Min.   :1.00      Min.   :1.00       Min.   :1.00  
    ##  1st Qu.:0.00           1st Qu.:3.00      1st Qu.:2.00       1st Qu.:3.00  
    ##  Median :0.00           Median :4.00      Median :3.00       Median :4.00  
    ##  Mean   :1.37           Mean   :3.65      Mean   :3.03       Mean   :4.04  
    ##  3rd Qu.:3.00           3rd Qu.:4.00      3rd Qu.:4.00       3rd Qu.:5.00  
    ##  Max.   :4.00           Max.   :5.00      Max.   :5.00       Max.   :5.00  
    ##  NA's   :1              NA's   :1         NA's   :1          NA's   :1     
    ##     day_out      night_out    alcohol_or_narcotics     mentor    
    ##  Min.   :0.0   Min.   :0.00   Min.   :0.00         Min.   :0.00  
    ##  1st Qu.:0.0   1st Qu.:0.00   1st Qu.:0.00         1st Qu.:0.00  
    ##  Median :1.0   Median :0.00   Median :0.00         Median :0.00  
    ##  Mean   :0.8   Mean   :0.51   Mean   :0.35         Mean   :0.41  
    ##  3rd Qu.:1.0   3rd Qu.:1.00   3rd Qu.:1.00         3rd Qu.:1.00  
    ##  Max.   :3.0   Max.   :3.00   Max.   :3.00         Max.   :1.00  
    ##  NA's   :1     NA's   :1      NA's   :1            NA's   :1     
    ##  mentor_meetings A - 1. I am enjoying the subject
    ##  Min.   :0.00    Min.   :3.00                    
    ##  1st Qu.:0.00    1st Qu.:4.00                    
    ##  Median :0.00    Median :5.00                    
    ##  Mean   :0.68    Mean   :4.49                    
    ##  3rd Qu.:1.00    3rd Qu.:5.00                    
    ##  Max.   :3.00    Max.   :5.00                    
    ##  NA's   :1       NA's   :1                       
    ##  A - 2. Classes start and end on time
    ##  Min.   :3.00                        
    ##  1st Qu.:4.00                        
    ##  Median :5.00                        
    ##  Mean   :4.68                        
    ##  3rd Qu.:5.00                        
    ##  Max.   :5.00                        
    ##  NA's   :1                           
    ##  A - 3. The learning environment is participative, involves learning by doing and is group-based
    ##  Min.   :3.00                                                                                   
    ##  1st Qu.:4.00                                                                                   
    ##  Median :4.00                                                                                   
    ##  Mean   :4.35                                                                                   
    ##  3rd Qu.:5.00                                                                                   
    ##  Max.   :5.00                                                                                   
    ##  NA's   :1                                                                                      
    ##  A - 4. The subject content is delivered according to the course outline and meets my expectations
    ##  Min.   :3.00                                                                                     
    ##  1st Qu.:4.75                                                                                     
    ##  Median :5.00                                                                                     
    ##  Mean   :4.74                                                                                     
    ##  3rd Qu.:5.00                                                                                     
    ##  Max.   :5.00                                                                                     
    ##  NA's   :1                                                                                        
    ##  A - 5. The topics are clear and logically developed
    ##  Min.   :2.00                                       
    ##  1st Qu.:4.00                                       
    ##  Median :5.00                                       
    ##  Mean   :4.65                                       
    ##  3rd Qu.:5.00                                       
    ##  Max.   :5.00                                       
    ##  NA's   :1                                          
    ##  A - 6. I am developing my oral and writing skills
    ##  Min.   :1.00                                     
    ##  1st Qu.:4.00                                     
    ##  Median :4.00                                     
    ##  Mean   :4.11                                     
    ##  3rd Qu.:5.00                                     
    ##  Max.   :5.00                                     
    ##  NA's   :1                                        
    ##  A - 7. I am developing my reflective and critical reasoning skills
    ##  Min.   :2.00                                                      
    ##  1st Qu.:4.00                                                      
    ##  Median :4.00                                                      
    ##  Mean   :4.38                                                      
    ##  3rd Qu.:5.00                                                      
    ##  Max.   :5.00                                                      
    ##  NA's   :1                                                         
    ##  A - 8. The assessment methods are assisting me to learn
    ##  Min.   :1.00                                           
    ##  1st Qu.:4.00                                           
    ##  Median :5.00                                           
    ##  Mean   :4.61                                           
    ##  3rd Qu.:5.00                                           
    ##  Max.   :5.00                                           
    ##  NA's   :1                                              
    ##  A - 9. I receive relevant feedback
    ##  Min.   :3.00                      
    ##  1st Qu.:4.00                      
    ##  Median :5.00                      
    ##  Mean   :4.58                      
    ##  3rd Qu.:5.00                      
    ##  Max.   :5.00                      
    ##  NA's   :1                         
    ##  A - 10. I read the recommended readings and notes
    ##  Min.   :3.00                                     
    ##  1st Qu.:4.00                                     
    ##  Median :5.00                                     
    ##  Mean   :4.55                                     
    ##  3rd Qu.:5.00                                     
    ##  Max.   :5.00                                     
    ##  NA's   :1                                        
    ##  A - 11. I use the eLearning material posted
    ##  Min.   :3.0                                
    ##  1st Qu.:4.0                                
    ##  Median :5.0                                
    ##  Mean   :4.7                                
    ##  3rd Qu.:5.0                                
    ##  Max.   :5.0                                
    ##  NA's   :1                                  
    ##  B - 1. Concept 1 of 6: Principles of Business Intelligence and the DataOps Philosophy
    ##  Min.   :1.00                                                                         
    ##  1st Qu.:4.00                                                                         
    ##  Median :4.00                                                                         
    ##  Mean   :4.25                                                                         
    ##  3rd Qu.:5.00                                                                         
    ##  Max.   :5.00                                                                         
    ##  NA's   :1                                                                            
    ##  B - 2. Concept 3 of 6: Linear Algorithms for Predictive Analytics
    ##  Min.   :2.00                                                     
    ##  1st Qu.:3.00                                                     
    ##  Median :4.00                                                     
    ##  Mean   :3.94                                                     
    ##  3rd Qu.:5.00                                                     
    ##  Max.   :5.00                                                     
    ##  NA's   :1                                                        
    ##  C - 2. Quizzes at the end of each concept
    ##  Min.   :2.00                             
    ##  1st Qu.:4.00                             
    ##  Median :5.00                             
    ##  Mean   :4.59                             
    ##  3rd Qu.:5.00                             
    ##  Max.   :5.00                             
    ##  NA's   :1                                
    ##  C - 3. Lab manuals that outline the steps to follow during the labs
    ##  Min.   :3.00                                                       
    ##  1st Qu.:4.00                                                       
    ##  Median :5.00                                                       
    ##  Mean   :4.61                                                       
    ##  3rd Qu.:5.00                                                       
    ##  Max.   :5.00                                                       
    ##  NA's   :1                                                          
    ##  C - 4. Required lab work submissions at the end of each lab manual that outline the activity to be done on your own
    ##  Min.   :3.00                                                                                                       
    ##  1st Qu.:4.00                                                                                                       
    ##  Median :5.00                                                                                                       
    ##  Mean   :4.55                                                                                                       
    ##  3rd Qu.:5.00                                                                                                       
    ##  Max.   :5.00                                                                                                       
    ##  NA's   :1                                                                                                          
    ##  C - 5. Supplementary videos to watch
    ##  Min.   :1.00                        
    ##  1st Qu.:4.00                        
    ##  Median :4.00                        
    ##  Mean   :4.19                        
    ##  3rd Qu.:5.00                        
    ##  Max.   :5.00                        
    ##  NA's   :1                           
    ##  C - 6. Supplementary podcasts to listen to
    ##  Min.   :1.00                              
    ##  1st Qu.:4.00                              
    ##  Median :4.00                              
    ##  Mean   :4.08                              
    ##  3rd Qu.:5.00                              
    ##  Max.   :5.00                              
    ##  NA's   :1                                 
    ##  C - 7. Supplementary content to read C - 8. Lectures slides
    ##  Min.   :1.00                         Min.   :2.0           
    ##  1st Qu.:4.00                         1st Qu.:4.0           
    ##  Median :4.00                         Median :5.0           
    ##  Mean   :4.17                         Mean   :4.6           
    ##  3rd Qu.:5.00                         3rd Qu.:5.0           
    ##  Max.   :5.00                         Max.   :5.0           
    ##  NA's   :1                            NA's   :1             
    ##  C - 9. Lecture notes on some of the lecture slides
    ##  Min.   :2.0                                       
    ##  1st Qu.:4.0                                       
    ##  Median :5.0                                       
    ##  Mean   :4.6                                       
    ##  3rd Qu.:5.0                                       
    ##  Max.   :5.0                                       
    ##  NA's   :1                                         
    ##  C - 10. The quality of the lectures given (quality measured by the breadth (the full span of knowledge of a subject) and depth (the extent to which specific topics are focused upon, amplified, and explored) of learning - NOT quality measured by how fun/comical/lively the lectures are)
    ##  Min.   :2.00                                                                                                                                                                                                                                                                                 
    ##  1st Qu.:4.00                                                                                                                                                                                                                                                                                 
    ##  Median :5.00                                                                                                                                                                                                                                                                                 
    ##  Mean   :4.54                                                                                                                                                                                                                                                                                 
    ##  3rd Qu.:5.00                                                                                                                                                                                                                                                                                 
    ##  Max.   :5.00                                                                                                                                                                                                                                                                                 
    ##  NA's   :1                                                                                                                                                                                                                                                                                    
    ##  C - 11. The division of theory and practice such that most of the theory is done during the recorded online classes and most of the practice is done during the physical classes
    ##  Min.   :2.00                                                                                                                                                                    
    ##  1st Qu.:4.00                                                                                                                                                                    
    ##  Median :5.00                                                                                                                                                                    
    ##  Mean   :4.49                                                                                                                                                                    
    ##  3rd Qu.:5.00                                                                                                                                                                    
    ##  Max.   :5.00                                                                                                                                                                    
    ##  NA's   :1                                                                                                                                                                       
    ##  C - 12. The recordings of online classes
    ##  Min.   :2.00                            
    ##  1st Qu.:4.00                            
    ##  Median :5.00                            
    ##  Mean   :4.33                            
    ##  3rd Qu.:5.00                            
    ##  Max.   :5.00                            
    ##  NA's   :1                               
    ##  D - 1. Write two things you like about the teaching and learning in this unit so far.
    ##  Length:101                                                                           
    ##  Class :character                                                                     
    ##  Mode  :character                                                                     
    ##                                                                                       
    ##                                                                                       
    ##                                                                                       
    ##                                                                                       
    ##  D - 2. Write at least one recommendation to improve the teaching and learning in this unit (for the remaining weeks in the semester)
    ##  Length:101                                                                                                                          
    ##  Class :character                                                                                                                    
    ##  Mode  :character                                                                                                                    
    ##                                                                                                                                      
    ##                                                                                                                                      
    ##                                                                                                                                      
    ##                                                                                                                                      
    ##  Average Course Evaluation Rating Average Level of Learning Attained Rating
    ##  Min.   :2.909                    Min.   :2.000                            
    ##  1st Qu.:4.273                    1st Qu.:3.500                            
    ##  Median :4.545                    Median :4.000                            
    ##  Mean   :4.531                    Mean   :4.095                            
    ##  3rd Qu.:4.909                    3rd Qu.:4.500                            
    ##  Max.   :5.000                    Max.   :5.000                            
    ##  NA's   :1                        NA's   :1                                
    ##  Average Pedagogical Strategy Effectiveness Rating
    ##  Min.   :3.182                                    
    ##  1st Qu.:4.068                                    
    ##  Median :4.545                                    
    ##  Mean   :4.432                                    
    ##  3rd Qu.:4.909                                    
    ##  Max.   :5.000                                    
    ##  NA's   :1                                        
    ##  Project: Section 1-4: (20%) x/10 Project: Section 5-11: (50%) x/10
    ##  Min.   : 0.000                   Min.   : 0.000                   
    ##  1st Qu.: 7.400                   1st Qu.: 6.000                   
    ##  Median : 8.500                   Median : 7.800                   
    ##  Mean   : 8.011                   Mean   : 6.582                   
    ##  3rd Qu.: 9.000                   3rd Qu.: 8.300                   
    ##  Max.   :10.000                   Max.   :10.000                   
    ##                                                                    
    ##  Project: Section 12: (30%) x/5 Project: (10%): x/30 x 100 TOTAL
    ##  Min.   :0.000                  Min.   :  0.00                  
    ##  1st Qu.:0.000                  1st Qu.: 56.00                  
    ##  Median :0.000                  Median : 66.40                  
    ##  Mean   :1.015                  Mean   : 62.39                  
    ##  3rd Qu.:1.250                  3rd Qu.: 71.60                  
    ##  Max.   :5.000                  Max.   :100.00                  
    ##  NA's   :1                                                      
    ##  Quiz 1 on Concept 1 (Introduction) x/32 Quiz 3 on Concept 3 (Linear) x/15
    ##  Min.   : 4.75                           Min.   : 3.00                    
    ##  1st Qu.:11.53                           1st Qu.: 7.00                    
    ##  Median :15.33                           Median : 9.00                    
    ##  Mean   :16.36                           Mean   : 9.53                    
    ##  3rd Qu.:19.63                           3rd Qu.:12.00                    
    ##  Max.   :31.25                           Max.   :15.00                    
    ##                                          NA's   :2                        
    ##  Quiz 4 on Concept 4 (Non-Linear) x/22 Quiz 5 on Concept 5 (Dashboarding) x/10
    ##  Min.   : 3.00                         Min.   : 0.000                         
    ##  1st Qu.:10.91                         1st Qu.: 5.000                         
    ##  Median :13.50                         Median : 6.330                         
    ##  Mean   :13.94                         Mean   : 6.367                         
    ##  3rd Qu.:17.50                         3rd Qu.: 8.000                         
    ##  Max.   :22.00                         Max.   :12.670                         
    ##  NA's   :6                             NA's   :12                             
    ##  Quizzes and  Bonus Marks (7%): x/79 x 100 TOTAL
    ##  Min.   :26.26                                  
    ##  1st Qu.:43.82                                  
    ##  Median :55.31                                  
    ##  Mean   :56.22                                  
    ##  3rd Qu.:65.16                                  
    ##  Max.   :95.25                                  
    ##                                                 
    ##  Lab 1 - 2.c. - (Simple Linear Regression) x/5
    ##  Min.   :3.000                                
    ##  1st Qu.:5.000                                
    ##  Median :5.000                                
    ##  Mean   :4.898                                
    ##  3rd Qu.:5.000                                
    ##  Max.   :5.000                                
    ##  NA's   :3                                    
    ##  Lab 2 - 2.e. -  (Linear Regression using Gradient Descent) x/5
    ##  Min.   :2.150                                                 
    ##  1st Qu.:3.150                                                 
    ##  Median :4.850                                                 
    ##  Mean   :4.166                                                 
    ##  3rd Qu.:5.000                                                 
    ##  Max.   :5.000                                                 
    ##  NA's   :6                                                     
    ##  Lab 3 - 2.g. - (Logistic Regression using Gradient Descent) x/5
    ##  Min.   :2.85                                                   
    ##  1st Qu.:4.85                                                   
    ##  Median :4.85                                                   
    ##  Mean   :4.63                                                   
    ##  3rd Qu.:4.85                                                   
    ##  Max.   :5.00                                                   
    ##  NA's   :9                                                      
    ##  Lab 4 - 2.h. - (Linear Discriminant Analysis) x/5
    ##  Min.   :1.850                                    
    ##  1st Qu.:4.100                                    
    ##  Median :4.850                                    
    ##  Mean   :4.425                                    
    ##  3rd Qu.:5.000                                    
    ##  Max.   :5.000                                    
    ##  NA's   :18                                       
    ##  Lab 5 - Chart JS Dashboard Setup x/5 Lab Work (7%) x/25 x 100
    ##  Min.   :0.000                        Min.   : 17.80          
    ##  1st Qu.:0.000                        1st Qu.: 70.80          
    ##  Median :5.000                        Median : 80.00          
    ##  Mean   :3.404                        Mean   : 79.72          
    ##  3rd Qu.:5.000                        3rd Qu.: 97.20          
    ##  Max.   :5.000                        Max.   :100.00          
    ##                                                               
    ##  CAT 1 (8%): x/38 x 100 CAT 2 (8%): x/100 x 100
    ##  Min.   :32.89          Min.   :  0.00         
    ##  1st Qu.:59.21          1st Qu.: 51.00         
    ##  Median :69.73          Median : 63.50         
    ##  Mean   :69.39          Mean   : 62.13         
    ##  3rd Qu.:82.89          3rd Qu.: 81.75         
    ##  Max.   :97.36          Max.   :100.00         
    ##  NA's   :4              NA's   :31             
    ##  Attendance Waiver Granted: 1 = Yes, 0 = No Absenteeism Percentage
    ##  Min.   :0.00000                            Min.   : 0.00         
    ##  1st Qu.:0.00000                            1st Qu.: 7.41         
    ##  Median :0.00000                            Median :14.81         
    ##  Mean   :0.04951                            Mean   :15.42         
    ##  3rd Qu.:0.00000                            3rd Qu.:22.22         
    ##  Max.   :1.00000                            Max.   :51.85         
    ##                                                                   
    ##  Coursework TOTAL: x/40 (40%) EXAM: x/60 (60%)
    ##  Min.   : 7.47                Min.   : 5.00   
    ##  1st Qu.:20.44                1st Qu.:26.00   
    ##  Median :24.58                Median :34.00   
    ##  Mean   :24.53                Mean   :33.94   
    ##  3rd Qu.:29.31                3rd Qu.:42.00   
    ##  Max.   :35.08                Max.   :56.00   
    ##                               NA's   :4       
    ##  TOTAL = Coursework TOTAL + EXAM (100%)    GRADE          
    ##  Min.   : 7.47                          Length:101        
    ##  1st Qu.:45.54                          Class :character  
    ##  Median :58.69                          Mode  :character  
    ##  Mean   :57.12                                            
    ##  3rd Qu.:68.83                                            
    ##  Max.   :87.72                                            
    ## 

``` r
model_of_the_transform <- preProcess(StudentPerformanceDataset,
                                     method = c("scale", "center"))
print(model_of_the_transform)
```

    ## Created from 51 samples and 100 variables
    ## 
    ## Pre-processing:
    ##   - centered (96)
    ##   - ignored (4)
    ##   - scaled (96)

``` r
student_performance_standardize_transform <- predict(model_of_the_transform, # nolint
                                                StudentPerformanceDataset)

# AFTER
summary(student_performance_standardize_transform)
```

    ##  class_group            gender             YOB          regret_choosing_bi
    ##  Length:101         Min.   :-1.1556   Min.   :-2.9155   Min.   :-0.1414   
    ##  Class :character   1st Qu.:-1.1556   1st Qu.:-0.9055   1st Qu.:-0.1414   
    ##  Mode  :character   Median : 0.8568   Median : 0.0995   Median :-0.1414   
    ##                     Mean   : 0.0000   Mean   : 0.0000   Mean   : 0.0000   
    ##                     3rd Qu.: 0.8568   3rd Qu.: 1.1045   3rd Qu.:-0.1414   
    ##                     Max.   : 0.8568   Max.   : 2.1095   Max.   : 7.0007   
    ##                                                                           
    ##   drop_bi_now        motivator       read_content_before_lecture
    ##  Min.   :-0.1414   Min.   :-1.7349   Min.   :-1.8191            
    ##  1st Qu.:-0.1414   1st Qu.: 0.5707   1st Qu.:-0.7811            
    ##  Median :-0.1414   Median : 0.5707   Median : 0.2569            
    ##  Mean   : 0.0000   Mean   : 0.0000   Mean   : 0.0000            
    ##  3rd Qu.:-0.1414   3rd Qu.: 0.5707   3rd Qu.: 0.2569            
    ##  Max.   : 7.0007   Max.   : 0.5707   Max.   : 2.3329            
    ##                                                                 
    ##  anticipate_test_questions answer_rhetorical_questions find_terms_I_do_not_know
    ##  Min.   :-2.6033           Min.   :-2.4418             Min.   :-2.5995         
    ##  1st Qu.:-0.5885           1st Qu.:-0.4286             1st Qu.:-0.7038         
    ##  Median : 0.4189           Median : 0.5780             Median : 0.2440         
    ##  Mean   : 0.0000           Mean   : 0.0000             Mean   : 0.0000         
    ##  3rd Qu.: 0.4189           3rd Qu.: 0.5780             3rd Qu.: 1.1918         
    ##  Max.   : 1.4263           Max.   : 1.5846             Max.   : 1.1918         
    ##                                                                                
    ##  copy_new_terms_in_reading_notebook take_quizzes_and_use_results
    ##  Min.   :-2.4058                    Min.   :-2.73448            
    ##  1st Qu.:-0.5992                    1st Qu.:-0.87466            
    ##  Median : 0.3041                    Median : 0.05524            
    ##  Mean   : 0.0000                    Mean   : 0.00000            
    ##  3rd Qu.: 0.3041                    3rd Qu.: 0.98515            
    ##  Max.   : 1.2074                    Max.   : 0.98515            
    ##                                                                 
    ##  reorganise_course_outline write_down_important_points space_out_revision
    ##  Min.   :-2.0550           Min.   :-2.6276             Min.   :-1.9709   
    ##  1st Qu.:-0.3254           1st Qu.:-0.7717             1st Qu.:-0.2015   
    ##  Median :-0.3254           Median : 0.1562             Median :-0.2015   
    ##  Mean   : 0.0000           Mean   : 0.0000             Mean   : 0.0000   
    ##  3rd Qu.: 0.5394           3rd Qu.: 1.0841             3rd Qu.: 0.6832   
    ##  Max.   : 1.4043           Max.   : 1.0841             Max.   : 1.5679   
    ##                                                                          
    ##  studying_in_study_group schedule_appointments goal_oriented    
    ##  Min.   :-1.0877         Min.   :-0.91037      Min.   :-0.4944  
    ##  1st Qu.:-1.0877         1st Qu.:-0.91037      1st Qu.:-0.4944  
    ##  Median :-0.3404         Median : 0.06779      Median :-0.4944  
    ##  Mean   : 0.0000         Mean   : 0.00000      Mean   : 0.0000  
    ##  3rd Qu.: 0.4070         3rd Qu.: 0.06779      3rd Qu.:-0.4944  
    ##  Max.   : 1.9016         Max.   : 3.00228      Max.   : 2.0025  
    ##                                                                 
    ##  spaced_repetition testing_and_active_recall  interleaving    
    ##  Min.   :-1.8720   Min.   :-2.86572          Min.   :-1.6908  
    ##  1st Qu.:-0.6677   1st Qu.:-0.08267          1st Qu.:-0.3461  
    ##  Median : 0.5366   Median :-0.08267          Median :-0.3461  
    ##  Mean   : 0.0000   Mean   : 0.00000          Mean   : 0.0000  
    ##  3rd Qu.: 0.5366   3rd Qu.: 1.30886          3rd Qu.: 0.9985  
    ##  Max.   : 1.7409   Max.   : 1.30886          Max.   : 2.3432  
    ##                                                               
    ##   categorizing     retrospective_timetable cornell_notes          sq3r        
    ##  Min.   :-2.3165   Min.   :-1.5883         Min.   :-1.5519   Min.   :-1.5392  
    ##  1st Qu.:-0.9641   1st Qu.:-0.4586         1st Qu.:-0.5472   1st Qu.:-0.5855  
    ##  Median : 0.3883   Median :-0.4586         Median : 0.4576   Median : 0.3683  
    ##  Mean   : 0.0000   Mean   : 0.0000         Mean   : 0.0000   Mean   : 0.0000  
    ##  3rd Qu.: 0.3883   3rd Qu.: 0.6711         3rd Qu.: 0.4576   3rd Qu.: 0.3683  
    ##  Max.   : 1.7407   Max.   : 1.8008         Max.   : 1.4624   Max.   : 1.3220  
    ##                                                                               
    ##     commute          study_time      repeats_since_Y1   paid_tuition    
    ##  Min.   :-1.6586   Min.   :-0.9134   Min.   :-0.9716   Min.   :-0.3498  
    ##  1st Qu.:-0.6999   1st Qu.:-0.9134   1st Qu.:-0.9716   1st Qu.:-0.3498  
    ##  Median : 0.2589   Median : 0.3045   Median :-0.0237   Median :-0.3498  
    ##  Mean   : 0.0000   Mean   : 0.0000   Mean   : 0.0000   Mean   : 0.0000  
    ##  3rd Qu.: 1.2176   3rd Qu.: 0.3045   3rd Qu.: 0.4502   3rd Qu.:-0.3498  
    ##  Max.   : 1.2176   Max.   : 2.7402   Max.   : 3.7678   Max.   : 2.8302  
    ##  NA's   :1         NA's   :1         NA's   :1         NA's   :1        
    ##   free_tuition     extra_curricular sports_extra_curricular exercise_per_week
    ##  Min.   :-0.6051   Min.   :-1.057   Min.   :-0.7462         Min.   :-1.3575  
    ##  1st Qu.:-0.6051   1st Qu.:-1.057   1st Qu.:-0.7462         1st Qu.:-0.1234  
    ##  Median :-0.6051   Median : 0.937   Median :-0.7462         Median :-0.1234  
    ##  Mean   : 0.0000   Mean   : 0.000   Mean   : 0.0000         Mean   : 0.0000  
    ##  3rd Qu.: 1.6361   3rd Qu.: 0.937   3rd Qu.: 1.3266         3rd Qu.: 1.1107  
    ##  Max.   : 1.6361   Max.   : 0.937   Max.   : 1.3266         Max.   : 2.3448  
    ##  NA's   :1         NA's   :1        NA's   :1               NA's   :1        
    ##     meditate            pray             internet           laptop 
    ##  Min.   :-0.8143   Min.   :-2.03728   Min.   :-2.5740   Min.   :0  
    ##  1st Qu.:-0.8143   1st Qu.:-1.06251   1st Qu.: 0.3846   1st Qu.:0  
    ##  Median : 0.2571   Median :-0.08773   Median : 0.3846   Median :0  
    ##  Mean   : 0.0000   Mean   : 0.00000   Mean   : 0.0000   Mean   :0  
    ##  3rd Qu.: 0.2571   3rd Qu.: 0.88705   3rd Qu.: 0.3846   3rd Qu.:0  
    ##  Max.   : 2.4000   Max.   : 0.88705   Max.   : 0.3846   Max.   :0  
    ##  NA's   :1         NA's   :1          NA's   :1         NA's   :1  
    ##  family_relationships  friendships       romantic_relationships
    ##  Min.   :-2.7369      Min.   :-2.74737   Min.   :-0.8531       
    ##  1st Qu.:-0.2374      1st Qu.:-0.01367   1st Qu.:-0.8531       
    ##  Median :-0.2374      Median :-0.01367   Median :-0.8531       
    ##  Mean   : 0.0000      Mean   : 0.00000   Mean   : 0.0000       
    ##  3rd Qu.: 1.0123      3rd Qu.:-0.01367   3rd Qu.: 1.0150       
    ##  Max.   : 1.0123      Max.   : 1.35318   Max.   : 1.6377       
    ##  NA's   :1            NA's   :1          NA's   :1             
    ##  spiritual_wellnes financial_wellness     health            day_out       
    ##  Min.   :-2.8309   Min.   :-1.85227   Min.   :-3.19122   Min.   :-1.4071  
    ##  1st Qu.:-0.6944   1st Qu.:-0.93982   1st Qu.:-1.09173   1st Qu.:-1.4071  
    ##  Median : 0.3739   Median :-0.02737   Median :-0.04199   Median : 0.3518  
    ##  Mean   : 0.0000   Mean   : 0.00000   Mean   : 0.00000   Mean   : 0.0000  
    ##  3rd Qu.: 0.3739   3rd Qu.: 0.88508   3rd Qu.: 1.00775   3rd Qu.: 0.3518  
    ##  Max.   : 1.4422   Max.   : 1.79752   Max.   : 1.00775   Max.   : 3.8696  
    ##  NA's   :1         NA's   :1          NA's   :1          NA's   :1        
    ##    night_out       alcohol_or_narcotics     mentor        mentor_meetings  
    ##  Min.   :-0.7926   Min.   :-0.628       Min.   :-0.8294   Min.   :-0.8101  
    ##  1st Qu.:-0.7926   1st Qu.:-0.628       1st Qu.:-0.8294   1st Qu.:-0.8101  
    ##  Median :-0.7926   Median :-0.628       Median :-0.8294   Median :-0.8101  
    ##  Mean   : 0.0000   Mean   : 0.000       Mean   : 0.0000   Mean   : 0.0000  
    ##  3rd Qu.: 0.7615   3rd Qu.: 1.166       3rd Qu.: 1.1936   3rd Qu.: 0.3812  
    ##  Max.   : 3.8697   Max.   : 4.755       Max.   : 1.1936   Max.   : 2.7638  
    ##  NA's   :1         NA's   :1            NA's   :1         NA's   :1        
    ##  A - 1. I am enjoying the subject A - 2. Classes start and end on time
    ##  Min.   :-2.5063                  Min.   :-3.4293                     
    ##  1st Qu.:-0.8242                  1st Qu.:-1.3880                     
    ##  Median : 0.8579                  Median : 0.6532                     
    ##  Mean   : 0.0000                  Mean   : 0.0000                     
    ##  3rd Qu.: 0.8579                  3rd Qu.: 0.6532                     
    ##  Max.   : 0.8579                  Max.   : 0.6532                     
    ##  NA's   :1                        NA's   :1                           
    ##  A - 3. The learning environment is participative, involves learning by doing and is group-based
    ##  Min.   :-2.0544                                                                                
    ##  1st Qu.:-0.5326                                                                                
    ##  Median :-0.5326                                                                                
    ##  Mean   : 0.0000                                                                                
    ##  3rd Qu.: 0.9892                                                                                
    ##  Max.   : 0.9892                                                                                
    ##  NA's   :1                                                                                      
    ##  A - 4. The subject content is delivered according to the course outline and meets my expectations
    ##  Min.   :-3.75655                                                                                 
    ##  1st Qu.: 0.02159                                                                                 
    ##  Median : 0.56132                                                                                 
    ##  Mean   : 0.00000                                                                                 
    ##  3rd Qu.: 0.56132                                                                                 
    ##  Max.   : 0.56132                                                                                 
    ##  NA's   :1                                                                                        
    ##  A - 5. The topics are clear and logically developed
    ##  Min.   :-4.6074                                    
    ##  1st Qu.:-1.1301                                    
    ##  Median : 0.6085                                    
    ##  Mean   : 0.0000                                    
    ##  3rd Qu.: 0.6085                                    
    ##  Max.   : 0.6085                                    
    ##  NA's   :1                                          
    ##  A - 6. I am developing my oral and writing skills
    ##  Min.   :-3.5544                                  
    ##  1st Qu.:-0.1257                                  
    ##  Median :-0.1257                                  
    ##  Mean   : 0.0000                                  
    ##  3rd Qu.: 1.0172                                  
    ##  Max.   : 1.0172                                  
    ##  NA's   :1                                        
    ##  A - 7. I am developing my reflective and critical reasoning skills
    ##  Min.   :-3.4338                                                   
    ##  1st Qu.:-0.5483                                                   
    ##  Median :-0.5483                                                   
    ##  Mean   : 0.0000                                                   
    ##  3rd Qu.: 0.8945                                                   
    ##  Max.   : 0.8945                                                   
    ##  NA's   :1                                                         
    ##  A - 8. The assessment methods are assisting me to learn
    ##  Min.   :-5.5563                                        
    ##  1st Qu.:-0.9389                                        
    ##  Median : 0.6003                                        
    ##  Mean   : 0.0000                                        
    ##  3rd Qu.: 0.6003                                        
    ##  Max.   : 0.6003                                        
    ##  NA's   :1                                              
    ##  A - 9. I receive relevant feedback
    ##  Min.   :-2.8531                   
    ##  1st Qu.:-1.0474                   
    ##  Median : 0.7584                   
    ##  Mean   : 0.0000                   
    ##  3rd Qu.: 0.7584                   
    ##  Max.   : 0.7584                   
    ##  NA's   :1                         
    ##  A - 10. I read the recommended readings and notes
    ##  Min.   :-2.4775                                  
    ##  1st Qu.:-0.8791                                  
    ##  Median : 0.7193                                  
    ##  Mean   : 0.0000                                  
    ##  3rd Qu.: 0.7193                                  
    ##  Max.   : 0.7193                                  
    ##  NA's   :1                                        
    ##  A - 11. I use the eLearning material posted
    ##  Min.   :-3.2553                            
    ##  1st Qu.:-1.3404                            
    ##  Median : 0.5745                            
    ##  Mean   : 0.0000                            
    ##  3rd Qu.: 0.5745                            
    ##  Max.   : 0.5745                            
    ##  NA's   :1                                  
    ##  B - 1. Concept 1 of 6: Principles of Business Intelligence and the DataOps Philosophy
    ##  Min.   :-4.1489                                                                      
    ##  1st Qu.:-0.3191                                                                      
    ##  Median :-0.3191                                                                      
    ##  Mean   : 0.0000                                                                      
    ##  3rd Qu.: 0.9574                                                                      
    ##  Max.   : 0.9574                                                                      
    ##  NA's   :1                                                                            
    ##  B - 2. Concept 3 of 6: Linear Algorithms for Predictive Analytics
    ##  Min.   :-2.24938                                                 
    ##  1st Qu.:-1.08990                                                 
    ##  Median : 0.06957                                                 
    ##  Mean   : 0.00000                                                 
    ##  3rd Qu.: 1.22904                                                 
    ##  Max.   : 1.22904                                                 
    ##  NA's   :1                                                        
    ##  C - 2. Quizzes at the end of each concept
    ##  Min.   :-4.1701                          
    ##  1st Qu.:-0.9499                          
    ##  Median : 0.6601                          
    ##  Mean   : 0.0000                          
    ##  3rd Qu.: 0.6601                          
    ##  Max.   : 0.6601                          
    ##  NA's   :1                                
    ##  C - 3. Lab manuals that outline the steps to follow during the labs
    ##  Min.   :-2.6777                                                    
    ##  1st Qu.:-1.0145                                                    
    ##  Median : 0.6486                                                    
    ##  Mean   : 0.0000                                                    
    ##  3rd Qu.: 0.6486                                                    
    ##  Max.   : 0.6486                                                    
    ##  NA's   :1                                                          
    ##  C - 4. Required lab work submissions at the end of each lab manual that outline the activity to be done on your own
    ##  Min.   :-2.5440                                                                                                    
    ##  1st Qu.:-0.9027                                                                                                    
    ##  Median : 0.7386                                                                                                    
    ##  Mean   : 0.0000                                                                                                    
    ##  3rd Qu.: 0.7386                                                                                                    
    ##  Max.   : 0.7386                                                                                                    
    ##  NA's   :1                                                                                                          
    ##  C - 5. Supplementary videos to watch
    ##  Min.   :-3.6080                     
    ##  1st Qu.:-0.2149                     
    ##  Median :-0.2149                     
    ##  Mean   : 0.0000                     
    ##  3rd Qu.: 0.9161                     
    ##  Max.   : 0.9161                     
    ##  NA's   :1                           
    ##  C - 6. Supplementary podcasts to listen to
    ##  Min.   :-3.10583                          
    ##  1st Qu.:-0.08067                          
    ##  Median :-0.08067                          
    ##  Mean   : 0.00000                          
    ##  3rd Qu.: 0.92772                          
    ##  Max.   : 0.92772                          
    ##  NA's   :1                                 
    ##  C - 7. Supplementary content to read C - 8. Lectures slides
    ##  Min.   :-3.2864                      Min.   :-3.5875       
    ##  1st Qu.:-0.1762                      1st Qu.:-0.8279       
    ##  Median :-0.1762                      Median : 0.5519       
    ##  Mean   : 0.0000                      Mean   : 0.0000       
    ##  3rd Qu.: 0.8605                      3rd Qu.: 0.5519       
    ##  Max.   : 0.8605                      Max.   : 0.5519       
    ##  NA's   :1                            NA's   :1             
    ##  C - 9. Lecture notes on some of the lecture slides
    ##  Min.   :-4.0904                                   
    ##  1st Qu.:-0.9439                                   
    ##  Median : 0.6293                                   
    ##  Mean   : 0.0000                                   
    ##  3rd Qu.: 0.6293                                   
    ##  Max.   : 0.6293                                   
    ##  NA's   :1                                         
    ##  C - 10. The quality of the lectures given (quality measured by the breadth (the full span of knowledge of a subject) and depth (the extent to which specific topics are focused upon, amplified, and explored) of learning - NOT quality measured by how fun/comical/lively the lectures are)
    ##  Min.   :-3.8612                                                                                                                                                                                                                                                                              
    ##  1st Qu.:-0.8209                                                                                                                                                                                                                                                                              
    ##  Median : 0.6993                                                                                                                                                                                                                                                                              
    ##  Mean   : 0.0000                                                                                                                                                                                                                                                                              
    ##  3rd Qu.: 0.6993                                                                                                                                                                                                                                                                              
    ##  Max.   : 0.6993                                                                                                                                                                                                                                                                              
    ##  NA's   :1                                                                                                                                                                                                                                                                                    
    ##  C - 11. The division of theory and practice such that most of the theory is done during the recorded online classes and most of the practice is done during the physical classes
    ##  Min.   :-3.6142                                                                                                                                                                 
    ##  1st Qu.:-0.7112                                                                                                                                                                 
    ##  Median : 0.7403                                                                                                                                                                 
    ##  Mean   : 0.0000                                                                                                                                                                 
    ##  3rd Qu.: 0.7403                                                                                                                                                                 
    ##  Max.   : 0.7403                                                                                                                                                                 
    ##  NA's   :1                                                                                                                                                                       
    ##  C - 12. The recordings of online classes
    ##  Min.   :-2.7301                         
    ##  1st Qu.:-0.3867                         
    ##  Median : 0.7850                         
    ##  Mean   : 0.0000                         
    ##  3rd Qu.: 0.7850                         
    ##  Max.   : 0.7850                         
    ##  NA's   :1                               
    ##  D - 1. Write two things you like about the teaching and learning in this unit so far.
    ##  Length:101                                                                           
    ##  Class :character                                                                     
    ##  Mode  :character                                                                     
    ##                                                                                       
    ##                                                                                       
    ##                                                                                       
    ##                                                                                       
    ##  D - 2. Write at least one recommendation to improve the teaching and learning in this unit (for the remaining weeks in the semester)
    ##  Length:101                                                                                                                          
    ##  Class :character                                                                                                                    
    ##  Mode  :character                                                                                                                    
    ##                                                                                                                                      
    ##                                                                                                                                      
    ##                                                                                                                                      
    ##                                                                                                                                      
    ##  Average Course Evaluation Rating Average Level of Learning Attained Rating
    ##  Min.   :-4.05150                 Min.   :-2.9674                          
    ##  1st Qu.:-0.64504                 1st Qu.:-0.8428                          
    ##  Median : 0.03645                 Median :-0.1346                          
    ##  Mean   : 0.00000                 Mean   : 0.0000                          
    ##  3rd Qu.: 0.94477                 3rd Qu.: 0.5736                          
    ##  Max.   : 1.17185                 Max.   : 1.2818                          
    ##  NA's   :1                        NA's   :1                                
    ##  Average Pedagogical Strategy Effectiveness Rating
    ##  Min.   :-2.4737                                  
    ##  1st Qu.:-0.7196                                  
    ##  Median : 0.2250                                  
    ##  Mean   : 0.0000                                  
    ##  3rd Qu.: 0.9445                                  
    ##  Max.   : 1.1244                                  
    ##  NA's   :1                                        
    ##  Project: Section 1-4: (20%) x/10 Project: Section 5-11: (50%) x/10
    ##  Min.   :-3.8114                  Min.   :-2.3600                  
    ##  1st Qu.:-0.2907                  1st Qu.:-0.2087                  
    ##  Median : 0.2327                  Median : 0.4366                  
    ##  Mean   : 0.0000                  Mean   : 0.0000                  
    ##  3rd Qu.: 0.4706                  3rd Qu.: 0.6159                  
    ##  Max.   : 0.9464                  Max.   : 1.2255                  
    ##                                                                    
    ##  Project: Section 12: (30%) x/5 Project: (10%): x/30 x 100 TOTAL
    ##  Min.   :-0.5683                Min.   :-3.0961                 
    ##  1st Qu.:-0.5683                1st Qu.:-0.3172                 
    ##  Median :-0.5683                Median : 0.1989                 
    ##  Mean   : 0.0000                Mean   : 0.0000                 
    ##  3rd Qu.: 0.1316                3rd Qu.: 0.4569                 
    ##  Max.   : 2.2310                Max.   : 1.8662                 
    ##  NA's   :1                                                      
    ##  Quiz 1 on Concept 1 (Introduction) x/32 Quiz 3 on Concept 3 (Linear) x/15
    ##  Min.   :-1.7842                         Min.   :-2.1031                  
    ##  1st Qu.:-0.7420                         1st Qu.:-0.8149                  
    ##  Median :-0.1578                         Median :-0.1708                  
    ##  Mean   : 0.0000                         Mean   : 0.0000                  
    ##  3rd Qu.: 0.5032                         3rd Qu.: 0.7954                  
    ##  Max.   : 2.2894                         Max.   : 1.7615                  
    ##                                          NA's   :2                        
    ##  Quiz 4 on Concept 4 (Non-Linear) x/22 Quiz 5 on Concept 5 (Dashboarding) x/10
    ##  Min.   :-2.46748                      Min.   :-3.03179                       
    ##  1st Qu.:-0.68157                      1st Qu.:-0.65108                       
    ##  Median :-0.09831                      Median :-0.01782                       
    ##  Mean   : 0.00000                      Mean   : 0.00000                       
    ##  3rd Qu.: 0.80424                      3rd Qu.: 0.77734                       
    ##  Max.   : 1.81960                      Max.   : 3.00092                       
    ##  NA's   :6                             NA's   :12                             
    ##  Quizzes and  Bonus Marks (7%): x/79 x 100 TOTAL
    ##  Min.   :-1.81638                               
    ##  1st Qu.:-0.75175                               
    ##  Median :-0.05512                               
    ##  Mean   : 0.00000                               
    ##  3rd Qu.: 0.54207                               
    ##  Max.   : 2.36638                               
    ##                                                 
    ##  Lab 1 - 2.c. - (Simple Linear Regression) x/5
    ##  Min.   :-4.8297                              
    ##  1st Qu.: 0.2597                              
    ##  Median : 0.2597                              
    ##  Mean   : 0.0000                              
    ##  3rd Qu.: 0.2597                              
    ##  Max.   : 0.2597                              
    ##  NA's   :3                                    
    ##  Lab 2 - 2.e. -  (Linear Regression using Gradient Descent) x/5
    ##  Min.   :-1.9485                                               
    ##  1st Qu.:-0.9821                                               
    ##  Median : 0.6607                                               
    ##  Mean   : 0.0000                                               
    ##  3rd Qu.: 0.8056                                               
    ##  Max.   : 0.8056                                               
    ##  NA's   :6                                                     
    ##  Lab 3 - 2.g. - (Logistic Regression using Gradient Descent) x/5
    ##  Min.   :-2.7794                                                
    ##  1st Qu.: 0.3431                                                
    ##  Median : 0.3431                                                
    ##  Mean   : 0.0000                                                
    ##  3rd Qu.: 0.3431                                                
    ##  Max.   : 0.5773                                                
    ##  NA's   :9                                                      
    ##  Lab 4 - 2.h. - (Linear Discriminant Analysis) x/5
    ##  Min.   :-2.8586                                  
    ##  1st Qu.:-0.3605                                  
    ##  Median : 0.4722                                  
    ##  Mean   : 0.0000                                  
    ##  3rd Qu.: 0.6387                                  
    ##  Max.   : 0.6387                                  
    ##  NA's   :18                                       
    ##  Lab 5 - Chart JS Dashboard Setup x/5 Lab Work (7%) x/25 x 100
    ##  Min.   :-1.4592                      Min.   :-3.20757        
    ##  1st Qu.:-1.4592                      1st Qu.:-0.46190        
    ##  Median : 0.6842                      Median : 0.01471        
    ##  Mean   : 0.0000                      Mean   : 0.00000        
    ##  3rd Qu.: 0.6842                      3rd Qu.: 0.90576        
    ##  Max.   : 0.6842                      Max.   : 1.05081        
    ##                                                               
    ##  CAT 1 (8%): x/38 x 100 CAT 2 (8%): x/100 x 100
    ##  Min.   :-2.41349       Min.   :-2.51821       
    ##  1st Qu.:-0.67329       1st Qu.:-0.45107       
    ##  Median : 0.02226       Median : 0.05559       
    ##  Mean   : 0.00000       Mean   : 0.00000       
    ##  3rd Qu.: 0.89236       3rd Qu.: 0.79530       
    ##  Max.   : 1.84908       Max.   : 1.53501       
    ##  NA's   :4              NA's   :31             
    ##  Attendance Waiver Granted: 1 = Yes, 0 = No Absenteeism Percentage
    ##  Min.   :-0.2271                            Min.   :-1.69613      
    ##  1st Qu.:-0.2271                            1st Qu.:-0.88083      
    ##  Median :-0.2271                            Median :-0.06663      
    ##  Mean   : 0.0000                            Mean   : 0.00000      
    ##  3rd Qu.:-0.2271                            3rd Qu.: 0.74867      
    ##  Max.   : 4.3600                            Max.   : 4.00877      
    ##                                                                   
    ##  Coursework TOTAL: x/40 (40%) EXAM: x/60 (60%)   
    ##  Min.   :-2.74036             Min.   :-2.570415  
    ##  1st Qu.:-0.65650             1st Qu.:-0.705101  
    ##  Median : 0.00867             Median : 0.005494  
    ##  Mean   : 0.00000             Mean   : 0.000000  
    ##  3rd Qu.: 0.76863             3rd Qu.: 0.716090  
    ##  Max.   : 1.69569             Max.   : 1.959633  
    ##                               NA's   :4          
    ##  TOTAL = Coursework TOTAL + EXAM (100%)    GRADE          
    ##  Min.   :-3.15733                       Length:101        
    ##  1st Qu.:-0.73640                       Class :character  
    ##  Median : 0.09983                       Mode  :character  
    ##  Mean   : 0.00000                                         
    ##  3rd Qu.: 0.74465                                         
    ##  Max.   : 1.94590                                         
    ## 

``` r
sapply(student_performance_standardize_transform, sd)
```

    ##                                                                                                                                                                                                                                                                                   class_group 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                                                                        gender 
    ##                                                                                                                                                                                                                                                                                             1 
    ##                                                                                                                                                                                                                                                                                           YOB 
    ##                                                                                                                                                                                                                                                                                             1 
    ##                                                                                                                                                                                                                                                                            regret_choosing_bi 
    ##                                                                                                                                                                                                                                                                                             1 
    ##                                                                                                                                                                                                                                                                                   drop_bi_now 
    ##                                                                                                                                                                                                                                                                                             1 
    ##                                                                                                                                                                                                                                                                                     motivator 
    ##                                                                                                                                                                                                                                                                                             1 
    ##                                                                                                                                                                                                                                                                   read_content_before_lecture 
    ##                                                                                                                                                                                                                                                                                             1 
    ##                                                                                                                                                                                                                                                                     anticipate_test_questions 
    ##                                                                                                                                                                                                                                                                                             1 
    ##                                                                                                                                                                                                                                                                   answer_rhetorical_questions 
    ##                                                                                                                                                                                                                                                                                             1 
    ##                                                                                                                                                                                                                                                                      find_terms_I_do_not_know 
    ##                                                                                                                                                                                                                                                                                             1 
    ##                                                                                                                                                                                                                                                            copy_new_terms_in_reading_notebook 
    ##                                                                                                                                                                                                                                                                                             1 
    ##                                                                                                                                                                                                                                                                  take_quizzes_and_use_results 
    ##                                                                                                                                                                                                                                                                                             1 
    ##                                                                                                                                                                                                                                                                     reorganise_course_outline 
    ##                                                                                                                                                                                                                                                                                             1 
    ##                                                                                                                                                                                                                                                                   write_down_important_points 
    ##                                                                                                                                                                                                                                                                                             1 
    ##                                                                                                                                                                                                                                                                            space_out_revision 
    ##                                                                                                                                                                                                                                                                                             1 
    ##                                                                                                                                                                                                                                                                       studying_in_study_group 
    ##                                                                                                                                                                                                                                                                                             1 
    ##                                                                                                                                                                                                                                                                         schedule_appointments 
    ##                                                                                                                                                                                                                                                                                             1 
    ##                                                                                                                                                                                                                                                                                 goal_oriented 
    ##                                                                                                                                                                                                                                                                                             1 
    ##                                                                                                                                                                                                                                                                             spaced_repetition 
    ##                                                                                                                                                                                                                                                                                             1 
    ##                                                                                                                                                                                                                                                                     testing_and_active_recall 
    ##                                                                                                                                                                                                                                                                                             1 
    ##                                                                                                                                                                                                                                                                                  interleaving 
    ##                                                                                                                                                                                                                                                                                             1 
    ##                                                                                                                                                                                                                                                                                  categorizing 
    ##                                                                                                                                                                                                                                                                                             1 
    ##                                                                                                                                                                                                                                                                       retrospective_timetable 
    ##                                                                                                                                                                                                                                                                                             1 
    ##                                                                                                                                                                                                                                                                                 cornell_notes 
    ##                                                                                                                                                                                                                                                                                             1 
    ##                                                                                                                                                                                                                                                                                          sq3r 
    ##                                                                                                                                                                                                                                                                                             1 
    ##                                                                                                                                                                                                                                                                                       commute 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                                                                    study_time 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                                                              repeats_since_Y1 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                                                                  paid_tuition 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                                                                  free_tuition 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                                                              extra_curricular 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                                                       sports_extra_curricular 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                                                             exercise_per_week 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                                                                      meditate 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                                                                          pray 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                                                                      internet 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                                                                        laptop 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                                                          family_relationships 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                                                                   friendships 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                                                        romantic_relationships 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                                                             spiritual_wellnes 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                                                            financial_wellness 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                                                                        health 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                                                                       day_out 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                                                                     night_out 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                                                          alcohol_or_narcotics 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                                                                        mentor 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                                                               mentor_meetings 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                                              A - 1. I am enjoying the subject 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                                          A - 2. Classes start and end on time 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                               A - 3. The learning environment is participative, involves learning by doing and is group-based 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                             A - 4. The subject content is delivered according to the course outline and meets my expectations 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                           A - 5. The topics are clear and logically developed 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                             A - 6. I am developing my oral and writing skills 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                            A - 7. I am developing my reflective and critical reasoning skills 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                       A - 8. The assessment methods are assisting me to learn 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                                            A - 9. I receive relevant feedback 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                             A - 10. I read the recommended readings and notes 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                                   A - 11. I use the eLearning material posted 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                         B - 1. Concept 1 of 6: Principles of Business Intelligence and the DataOps Philosophy 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                             B - 2. Concept 3 of 6: Linear Algorithms for Predictive Analytics 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                                     C - 2. Quizzes at the end of each concept 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                           C - 3. Lab manuals that outline the steps to follow during the labs 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                           C - 4. Required lab work submissions at the end of each lab manual that outline the activity to be done on your own 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                                          C - 5. Supplementary videos to watch 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                                    C - 6. Supplementary podcasts to listen to 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                                          C - 7. Supplementary content to read 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                                                        C - 8. Lectures slides 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                            C - 9. Lecture notes on some of the lecture slides 
    ##                                                                                                                                                                                                                                                                                            NA 
    ## C - 10. The quality of the lectures given (quality measured by the breadth (the full span of knowledge of a subject) and depth (the extent to which specific topics are focused upon, amplified, and explored) of learning - NOT quality measured by how fun/comical/lively the lectures are) 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                              C - 11. The division of theory and practice such that most of the theory is done during the recorded online classes and most of the practice is done during the physical classes 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                                      C - 12. The recordings of online classes 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                         D - 1. Write two things you like about the teaching and learning in this unit so far. 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                          D - 2. Write at least one recommendation to improve the teaching and learning in this unit (for the remaining weeks in the semester) 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                                              Average Course Evaluation Rating 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                                     Average Level of Learning Attained Rating 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                             Average Pedagogical Strategy Effectiveness Rating 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                                              Project: Section 1-4: (20%) x/10 
    ##                                                                                                                                                                                                                                                                                             1 
    ##                                                                                                                                                                                                                                                             Project: Section 5-11: (50%) x/10 
    ##                                                                                                                                                                                                                                                                                             1 
    ##                                                                                                                                                                                                                                                                Project: Section 12: (30%) x/5 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                                              Project: (10%): x/30 x 100 TOTAL 
    ##                                                                                                                                                                                                                                                                                             1 
    ##                                                                                                                                                                                                                                                       Quiz 1 on Concept 1 (Introduction) x/32 
    ##                                                                                                                                                                                                                                                                                             1 
    ##                                                                                                                                                                                                                                                             Quiz 3 on Concept 3 (Linear) x/15 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                                         Quiz 4 on Concept 4 (Non-Linear) x/22 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                                       Quiz 5 on Concept 5 (Dashboarding) x/10 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                               Quizzes and  Bonus Marks (7%): x/79 x 100 TOTAL 
    ##                                                                                                                                                                                                                                                                                             1 
    ##                                                                                                                                                                                                                                                 Lab 1 - 2.c. - (Simple Linear Regression) x/5 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                Lab 2 - 2.e. -  (Linear Regression using Gradient Descent) x/5 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                               Lab 3 - 2.g. - (Logistic Regression using Gradient Descent) x/5 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                             Lab 4 - 2.h. - (Linear Discriminant Analysis) x/5 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                                          Lab 5 - Chart JS Dashboard Setup x/5 
    ##                                                                                                                                                                                                                                                                                             1 
    ##                                                                                                                                                                                                                                                                      Lab Work (7%) x/25 x 100 
    ##                                                                                                                                                                                                                                                                                             1 
    ##                                                                                                                                                                                                                                                                        CAT 1 (8%): x/38 x 100 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                                                       CAT 2 (8%): x/100 x 100 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                                    Attendance Waiver Granted: 1 = Yes, 0 = No 
    ##                                                                                                                                                                                                                                                                                             1 
    ##                                                                                                                                                                                                                                                                        Absenteeism Percentage 
    ##                                                                                                                                                                                                                                                                                             1 
    ##                                                                                                                                                                                                                                                                  Coursework TOTAL: x/40 (40%) 
    ##                                                                                                                                                                                                                                                                                             1 
    ##                                                                                                                                                                                                                                                                              EXAM: x/60 (60%) 
    ##                                                                                                                                                                                                                                                                                            NA 
    ##                                                                                                                                                                                                                                                        TOTAL = Coursework TOTAL + EXAM (100%) 
    ##                                                                                                                                                                                                                                                                                             1 
    ##                                                                                                                                                                                                                                                                                         GRADE 
    ##                                                                                                                                                                                                                                                                                            NA

# Normalized the Dataset ensuring the numerical values between 0 and 1

``` r
# Normalizing a dataset implies ensuring the numerical data are
# between [0, 1] (inclusive).

### The Normalize Transform on the Student Performance Dataset ----
summary(StudentPerformanceDataset)
```

    ##  class_group            gender            YOB       regret_choosing_bi
    ##  Length:101         Min.   :0.0000   Min.   :1998   Min.   :0.0000    
    ##  Class :character   1st Qu.:0.0000   1st Qu.:2000   1st Qu.:0.0000    
    ##  Mode  :character   Median :1.0000   Median :2001   Median :0.0000    
    ##                     Mean   :0.5743   Mean   :2001   Mean   :0.0198    
    ##                     3rd Qu.:1.0000   3rd Qu.:2002   3rd Qu.:0.0000    
    ##                     Max.   :1.0000   Max.   :2003   Max.   :1.0000    
    ##                                                                       
    ##   drop_bi_now       motivator      read_content_before_lecture
    ##  Min.   :0.0000   Min.   :0.0000   Min.   :1.000              
    ##  1st Qu.:0.0000   1st Qu.:1.0000   1st Qu.:2.000              
    ##  Median :0.0000   Median :1.0000   Median :3.000              
    ##  Mean   :0.0198   Mean   :0.7525   Mean   :2.752              
    ##  3rd Qu.:0.0000   3rd Qu.:1.0000   3rd Qu.:3.000              
    ##  Max.   :1.0000   Max.   :1.0000   Max.   :5.000              
    ##                                                               
    ##  anticipate_test_questions answer_rhetorical_questions find_terms_I_do_not_know
    ##  Min.   :1.000             Min.   :1.000               Min.   :1.000           
    ##  1st Qu.:3.000             1st Qu.:3.000               1st Qu.:3.000           
    ##  Median :4.000             Median :4.000               Median :4.000           
    ##  Mean   :3.584             Mean   :3.426               Mean   :3.743           
    ##  3rd Qu.:4.000             3rd Qu.:4.000               3rd Qu.:5.000           
    ##  Max.   :5.000             Max.   :5.000               Max.   :5.000           
    ##                                                                                
    ##  copy_new_terms_in_reading_notebook take_quizzes_and_use_results
    ##  Min.   :1.000                      Min.   :1.000               
    ##  1st Qu.:3.000                      1st Qu.:3.000               
    ##  Median :4.000                      Median :4.000               
    ##  Mean   :3.663                      Mean   :3.941               
    ##  3rd Qu.:4.000                      3rd Qu.:5.000               
    ##  Max.   :5.000                      Max.   :5.000               
    ##                                                                 
    ##  reorganise_course_outline write_down_important_points space_out_revision
    ##  Min.   :1.000             Min.   :1.000               Min.   :1.000     
    ##  1st Qu.:3.000             1st Qu.:3.000               1st Qu.:3.000     
    ##  Median :3.000             Median :4.000               Median :3.000     
    ##  Mean   :3.376             Mean   :3.832               Mean   :3.228     
    ##  3rd Qu.:4.000             3rd Qu.:5.000               3rd Qu.:4.000     
    ##  Max.   :5.000             Max.   :5.000               Max.   :5.000     
    ##                                                                          
    ##  studying_in_study_group schedule_appointments goal_oriented  
    ##  Min.   :1.000           Min.   :1.000         Min.   :0.000  
    ##  1st Qu.:1.000           1st Qu.:1.000         1st Qu.:0.000  
    ##  Median :2.000           Median :2.000         Median :0.000  
    ##  Mean   :2.455           Mean   :1.931         Mean   :0.198  
    ##  3rd Qu.:3.000           3rd Qu.:2.000         3rd Qu.:0.000  
    ##  Max.   :5.000           Max.   :5.000         Max.   :1.000  
    ##                                                               
    ##  spaced_repetition testing_and_active_recall  interleaving    categorizing  
    ##  Min.   :1.000     Min.   :1.000             Min.   :1.000   Min.   :1.000  
    ##  1st Qu.:2.000     1st Qu.:3.000             1st Qu.:2.000   1st Qu.:2.000  
    ##  Median :3.000     Median :3.000             Median :2.000   Median :3.000  
    ##  Mean   :2.554     Mean   :3.059             Mean   :2.257   Mean   :2.713  
    ##  3rd Qu.:3.000     3rd Qu.:4.000             3rd Qu.:3.000   3rd Qu.:3.000  
    ##  Max.   :4.000     Max.   :4.000             Max.   :4.000   Max.   :4.000  
    ##                                                                             
    ##  retrospective_timetable cornell_notes        sq3r          commute    
    ##  Min.   :1.000           Min.   :1.000   Min.   :1.000   Min.   :1.00  
    ##  1st Qu.:2.000           1st Qu.:2.000   1st Qu.:2.000   1st Qu.:2.00  
    ##  Median :2.000           Median :3.000   Median :3.000   Median :3.00  
    ##  Mean   :2.406           Mean   :2.545   Mean   :2.614   Mean   :2.73  
    ##  3rd Qu.:3.000           3rd Qu.:3.000   3rd Qu.:3.000   3rd Qu.:4.00  
    ##  Max.   :4.000           Max.   :4.000   Max.   :4.000   Max.   :4.00  
    ##                                                          NA's   :1     
    ##    study_time   repeats_since_Y1  paid_tuition   free_tuition  extra_curricular
    ##  Min.   :1.00   Min.   : 0.00    Min.   :0.00   Min.   :0.00   Min.   :0.00    
    ##  1st Qu.:1.00   1st Qu.: 0.00    1st Qu.:0.00   1st Qu.:0.00   1st Qu.:0.00    
    ##  Median :2.00   Median : 2.00    Median :0.00   Median :0.00   Median :1.00    
    ##  Mean   :1.75   Mean   : 2.05    Mean   :0.11   Mean   :0.27   Mean   :0.53    
    ##  3rd Qu.:2.00   3rd Qu.: 3.00    3rd Qu.:0.00   3rd Qu.:1.00   3rd Qu.:1.00    
    ##  Max.   :4.00   Max.   :10.00    Max.   :1.00   Max.   :1.00   Max.   :1.00    
    ##  NA's   :1      NA's   :1        NA's   :1      NA's   :1      NA's   :1       
    ##  sports_extra_curricular exercise_per_week    meditate         pray     
    ##  Min.   :0.00            Min.   :0.0       Min.   :0.00   Min.   :0.00  
    ##  1st Qu.:0.00            1st Qu.:1.0       1st Qu.:0.00   1st Qu.:1.00  
    ##  Median :0.00            Median :1.0       Median :1.00   Median :2.00  
    ##  Mean   :0.36            Mean   :1.1       Mean   :0.76   Mean   :2.09  
    ##  3rd Qu.:1.00            3rd Qu.:2.0       3rd Qu.:1.00   3rd Qu.:3.00  
    ##  Max.   :1.00            Max.   :3.0       Max.   :3.00   Max.   :3.00  
    ##  NA's   :1               NA's   :1         NA's   :1      NA's   :1     
    ##     internet        laptop  family_relationships  friendships  
    ##  Min.   :0.00   Min.   :1   Min.   :2.00         Min.   :2.00  
    ##  1st Qu.:1.00   1st Qu.:1   1st Qu.:4.00         1st Qu.:4.00  
    ##  Median :1.00   Median :1   Median :4.00         Median :4.00  
    ##  Mean   :0.87   Mean   :1   Mean   :4.19         Mean   :4.01  
    ##  3rd Qu.:1.00   3rd Qu.:1   3rd Qu.:5.00         3rd Qu.:4.00  
    ##  Max.   :1.00   Max.   :1   Max.   :5.00         Max.   :5.00  
    ##  NA's   :1      NA's   :1   NA's   :1            NA's   :1     
    ##  romantic_relationships spiritual_wellnes financial_wellness     health    
    ##  Min.   :0.00           Min.   :1.00      Min.   :1.00       Min.   :1.00  
    ##  1st Qu.:0.00           1st Qu.:3.00      1st Qu.:2.00       1st Qu.:3.00  
    ##  Median :0.00           Median :4.00      Median :3.00       Median :4.00  
    ##  Mean   :1.37           Mean   :3.65      Mean   :3.03       Mean   :4.04  
    ##  3rd Qu.:3.00           3rd Qu.:4.00      3rd Qu.:4.00       3rd Qu.:5.00  
    ##  Max.   :4.00           Max.   :5.00      Max.   :5.00       Max.   :5.00  
    ##  NA's   :1              NA's   :1         NA's   :1          NA's   :1     
    ##     day_out      night_out    alcohol_or_narcotics     mentor    
    ##  Min.   :0.0   Min.   :0.00   Min.   :0.00         Min.   :0.00  
    ##  1st Qu.:0.0   1st Qu.:0.00   1st Qu.:0.00         1st Qu.:0.00  
    ##  Median :1.0   Median :0.00   Median :0.00         Median :0.00  
    ##  Mean   :0.8   Mean   :0.51   Mean   :0.35         Mean   :0.41  
    ##  3rd Qu.:1.0   3rd Qu.:1.00   3rd Qu.:1.00         3rd Qu.:1.00  
    ##  Max.   :3.0   Max.   :3.00   Max.   :3.00         Max.   :1.00  
    ##  NA's   :1     NA's   :1      NA's   :1            NA's   :1     
    ##  mentor_meetings A - 1. I am enjoying the subject
    ##  Min.   :0.00    Min.   :3.00                    
    ##  1st Qu.:0.00    1st Qu.:4.00                    
    ##  Median :0.00    Median :5.00                    
    ##  Mean   :0.68    Mean   :4.49                    
    ##  3rd Qu.:1.00    3rd Qu.:5.00                    
    ##  Max.   :3.00    Max.   :5.00                    
    ##  NA's   :1       NA's   :1                       
    ##  A - 2. Classes start and end on time
    ##  Min.   :3.00                        
    ##  1st Qu.:4.00                        
    ##  Median :5.00                        
    ##  Mean   :4.68                        
    ##  3rd Qu.:5.00                        
    ##  Max.   :5.00                        
    ##  NA's   :1                           
    ##  A - 3. The learning environment is participative, involves learning by doing and is group-based
    ##  Min.   :3.00                                                                                   
    ##  1st Qu.:4.00                                                                                   
    ##  Median :4.00                                                                                   
    ##  Mean   :4.35                                                                                   
    ##  3rd Qu.:5.00                                                                                   
    ##  Max.   :5.00                                                                                   
    ##  NA's   :1                                                                                      
    ##  A - 4. The subject content is delivered according to the course outline and meets my expectations
    ##  Min.   :3.00                                                                                     
    ##  1st Qu.:4.75                                                                                     
    ##  Median :5.00                                                                                     
    ##  Mean   :4.74                                                                                     
    ##  3rd Qu.:5.00                                                                                     
    ##  Max.   :5.00                                                                                     
    ##  NA's   :1                                                                                        
    ##  A - 5. The topics are clear and logically developed
    ##  Min.   :2.00                                       
    ##  1st Qu.:4.00                                       
    ##  Median :5.00                                       
    ##  Mean   :4.65                                       
    ##  3rd Qu.:5.00                                       
    ##  Max.   :5.00                                       
    ##  NA's   :1                                          
    ##  A - 6. I am developing my oral and writing skills
    ##  Min.   :1.00                                     
    ##  1st Qu.:4.00                                     
    ##  Median :4.00                                     
    ##  Mean   :4.11                                     
    ##  3rd Qu.:5.00                                     
    ##  Max.   :5.00                                     
    ##  NA's   :1                                        
    ##  A - 7. I am developing my reflective and critical reasoning skills
    ##  Min.   :2.00                                                      
    ##  1st Qu.:4.00                                                      
    ##  Median :4.00                                                      
    ##  Mean   :4.38                                                      
    ##  3rd Qu.:5.00                                                      
    ##  Max.   :5.00                                                      
    ##  NA's   :1                                                         
    ##  A - 8. The assessment methods are assisting me to learn
    ##  Min.   :1.00                                           
    ##  1st Qu.:4.00                                           
    ##  Median :5.00                                           
    ##  Mean   :4.61                                           
    ##  3rd Qu.:5.00                                           
    ##  Max.   :5.00                                           
    ##  NA's   :1                                              
    ##  A - 9. I receive relevant feedback
    ##  Min.   :3.00                      
    ##  1st Qu.:4.00                      
    ##  Median :5.00                      
    ##  Mean   :4.58                      
    ##  3rd Qu.:5.00                      
    ##  Max.   :5.00                      
    ##  NA's   :1                         
    ##  A - 10. I read the recommended readings and notes
    ##  Min.   :3.00                                     
    ##  1st Qu.:4.00                                     
    ##  Median :5.00                                     
    ##  Mean   :4.55                                     
    ##  3rd Qu.:5.00                                     
    ##  Max.   :5.00                                     
    ##  NA's   :1                                        
    ##  A - 11. I use the eLearning material posted
    ##  Min.   :3.0                                
    ##  1st Qu.:4.0                                
    ##  Median :5.0                                
    ##  Mean   :4.7                                
    ##  3rd Qu.:5.0                                
    ##  Max.   :5.0                                
    ##  NA's   :1                                  
    ##  B - 1. Concept 1 of 6: Principles of Business Intelligence and the DataOps Philosophy
    ##  Min.   :1.00                                                                         
    ##  1st Qu.:4.00                                                                         
    ##  Median :4.00                                                                         
    ##  Mean   :4.25                                                                         
    ##  3rd Qu.:5.00                                                                         
    ##  Max.   :5.00                                                                         
    ##  NA's   :1                                                                            
    ##  B - 2. Concept 3 of 6: Linear Algorithms for Predictive Analytics
    ##  Min.   :2.00                                                     
    ##  1st Qu.:3.00                                                     
    ##  Median :4.00                                                     
    ##  Mean   :3.94                                                     
    ##  3rd Qu.:5.00                                                     
    ##  Max.   :5.00                                                     
    ##  NA's   :1                                                        
    ##  C - 2. Quizzes at the end of each concept
    ##  Min.   :2.00                             
    ##  1st Qu.:4.00                             
    ##  Median :5.00                             
    ##  Mean   :4.59                             
    ##  3rd Qu.:5.00                             
    ##  Max.   :5.00                             
    ##  NA's   :1                                
    ##  C - 3. Lab manuals that outline the steps to follow during the labs
    ##  Min.   :3.00                                                       
    ##  1st Qu.:4.00                                                       
    ##  Median :5.00                                                       
    ##  Mean   :4.61                                                       
    ##  3rd Qu.:5.00                                                       
    ##  Max.   :5.00                                                       
    ##  NA's   :1                                                          
    ##  C - 4. Required lab work submissions at the end of each lab manual that outline the activity to be done on your own
    ##  Min.   :3.00                                                                                                       
    ##  1st Qu.:4.00                                                                                                       
    ##  Median :5.00                                                                                                       
    ##  Mean   :4.55                                                                                                       
    ##  3rd Qu.:5.00                                                                                                       
    ##  Max.   :5.00                                                                                                       
    ##  NA's   :1                                                                                                          
    ##  C - 5. Supplementary videos to watch
    ##  Min.   :1.00                        
    ##  1st Qu.:4.00                        
    ##  Median :4.00                        
    ##  Mean   :4.19                        
    ##  3rd Qu.:5.00                        
    ##  Max.   :5.00                        
    ##  NA's   :1                           
    ##  C - 6. Supplementary podcasts to listen to
    ##  Min.   :1.00                              
    ##  1st Qu.:4.00                              
    ##  Median :4.00                              
    ##  Mean   :4.08                              
    ##  3rd Qu.:5.00                              
    ##  Max.   :5.00                              
    ##  NA's   :1                                 
    ##  C - 7. Supplementary content to read C - 8. Lectures slides
    ##  Min.   :1.00                         Min.   :2.0           
    ##  1st Qu.:4.00                         1st Qu.:4.0           
    ##  Median :4.00                         Median :5.0           
    ##  Mean   :4.17                         Mean   :4.6           
    ##  3rd Qu.:5.00                         3rd Qu.:5.0           
    ##  Max.   :5.00                         Max.   :5.0           
    ##  NA's   :1                            NA's   :1             
    ##  C - 9. Lecture notes on some of the lecture slides
    ##  Min.   :2.0                                       
    ##  1st Qu.:4.0                                       
    ##  Median :5.0                                       
    ##  Mean   :4.6                                       
    ##  3rd Qu.:5.0                                       
    ##  Max.   :5.0                                       
    ##  NA's   :1                                         
    ##  C - 10. The quality of the lectures given (quality measured by the breadth (the full span of knowledge of a subject) and depth (the extent to which specific topics are focused upon, amplified, and explored) of learning - NOT quality measured by how fun/comical/lively the lectures are)
    ##  Min.   :2.00                                                                                                                                                                                                                                                                                 
    ##  1st Qu.:4.00                                                                                                                                                                                                                                                                                 
    ##  Median :5.00                                                                                                                                                                                                                                                                                 
    ##  Mean   :4.54                                                                                                                                                                                                                                                                                 
    ##  3rd Qu.:5.00                                                                                                                                                                                                                                                                                 
    ##  Max.   :5.00                                                                                                                                                                                                                                                                                 
    ##  NA's   :1                                                                                                                                                                                                                                                                                    
    ##  C - 11. The division of theory and practice such that most of the theory is done during the recorded online classes and most of the practice is done during the physical classes
    ##  Min.   :2.00                                                                                                                                                                    
    ##  1st Qu.:4.00                                                                                                                                                                    
    ##  Median :5.00                                                                                                                                                                    
    ##  Mean   :4.49                                                                                                                                                                    
    ##  3rd Qu.:5.00                                                                                                                                                                    
    ##  Max.   :5.00                                                                                                                                                                    
    ##  NA's   :1                                                                                                                                                                       
    ##  C - 12. The recordings of online classes
    ##  Min.   :2.00                            
    ##  1st Qu.:4.00                            
    ##  Median :5.00                            
    ##  Mean   :4.33                            
    ##  3rd Qu.:5.00                            
    ##  Max.   :5.00                            
    ##  NA's   :1                               
    ##  D - 1. Write two things you like about the teaching and learning in this unit so far.
    ##  Length:101                                                                           
    ##  Class :character                                                                     
    ##  Mode  :character                                                                     
    ##                                                                                       
    ##                                                                                       
    ##                                                                                       
    ##                                                                                       
    ##  D - 2. Write at least one recommendation to improve the teaching and learning in this unit (for the remaining weeks in the semester)
    ##  Length:101                                                                                                                          
    ##  Class :character                                                                                                                    
    ##  Mode  :character                                                                                                                    
    ##                                                                                                                                      
    ##                                                                                                                                      
    ##                                                                                                                                      
    ##                                                                                                                                      
    ##  Average Course Evaluation Rating Average Level of Learning Attained Rating
    ##  Min.   :2.909                    Min.   :2.000                            
    ##  1st Qu.:4.273                    1st Qu.:3.500                            
    ##  Median :4.545                    Median :4.000                            
    ##  Mean   :4.531                    Mean   :4.095                            
    ##  3rd Qu.:4.909                    3rd Qu.:4.500                            
    ##  Max.   :5.000                    Max.   :5.000                            
    ##  NA's   :1                        NA's   :1                                
    ##  Average Pedagogical Strategy Effectiveness Rating
    ##  Min.   :3.182                                    
    ##  1st Qu.:4.068                                    
    ##  Median :4.545                                    
    ##  Mean   :4.432                                    
    ##  3rd Qu.:4.909                                    
    ##  Max.   :5.000                                    
    ##  NA's   :1                                        
    ##  Project: Section 1-4: (20%) x/10 Project: Section 5-11: (50%) x/10
    ##  Min.   : 0.000                   Min.   : 0.000                   
    ##  1st Qu.: 7.400                   1st Qu.: 6.000                   
    ##  Median : 8.500                   Median : 7.800                   
    ##  Mean   : 8.011                   Mean   : 6.582                   
    ##  3rd Qu.: 9.000                   3rd Qu.: 8.300                   
    ##  Max.   :10.000                   Max.   :10.000                   
    ##                                                                    
    ##  Project: Section 12: (30%) x/5 Project: (10%): x/30 x 100 TOTAL
    ##  Min.   :0.000                  Min.   :  0.00                  
    ##  1st Qu.:0.000                  1st Qu.: 56.00                  
    ##  Median :0.000                  Median : 66.40                  
    ##  Mean   :1.015                  Mean   : 62.39                  
    ##  3rd Qu.:1.250                  3rd Qu.: 71.60                  
    ##  Max.   :5.000                  Max.   :100.00                  
    ##  NA's   :1                                                      
    ##  Quiz 1 on Concept 1 (Introduction) x/32 Quiz 3 on Concept 3 (Linear) x/15
    ##  Min.   : 4.75                           Min.   : 3.00                    
    ##  1st Qu.:11.53                           1st Qu.: 7.00                    
    ##  Median :15.33                           Median : 9.00                    
    ##  Mean   :16.36                           Mean   : 9.53                    
    ##  3rd Qu.:19.63                           3rd Qu.:12.00                    
    ##  Max.   :31.25                           Max.   :15.00                    
    ##                                          NA's   :2                        
    ##  Quiz 4 on Concept 4 (Non-Linear) x/22 Quiz 5 on Concept 5 (Dashboarding) x/10
    ##  Min.   : 3.00                         Min.   : 0.000                         
    ##  1st Qu.:10.91                         1st Qu.: 5.000                         
    ##  Median :13.50                         Median : 6.330                         
    ##  Mean   :13.94                         Mean   : 6.367                         
    ##  3rd Qu.:17.50                         3rd Qu.: 8.000                         
    ##  Max.   :22.00                         Max.   :12.670                         
    ##  NA's   :6                             NA's   :12                             
    ##  Quizzes and  Bonus Marks (7%): x/79 x 100 TOTAL
    ##  Min.   :26.26                                  
    ##  1st Qu.:43.82                                  
    ##  Median :55.31                                  
    ##  Mean   :56.22                                  
    ##  3rd Qu.:65.16                                  
    ##  Max.   :95.25                                  
    ##                                                 
    ##  Lab 1 - 2.c. - (Simple Linear Regression) x/5
    ##  Min.   :3.000                                
    ##  1st Qu.:5.000                                
    ##  Median :5.000                                
    ##  Mean   :4.898                                
    ##  3rd Qu.:5.000                                
    ##  Max.   :5.000                                
    ##  NA's   :3                                    
    ##  Lab 2 - 2.e. -  (Linear Regression using Gradient Descent) x/5
    ##  Min.   :2.150                                                 
    ##  1st Qu.:3.150                                                 
    ##  Median :4.850                                                 
    ##  Mean   :4.166                                                 
    ##  3rd Qu.:5.000                                                 
    ##  Max.   :5.000                                                 
    ##  NA's   :6                                                     
    ##  Lab 3 - 2.g. - (Logistic Regression using Gradient Descent) x/5
    ##  Min.   :2.85                                                   
    ##  1st Qu.:4.85                                                   
    ##  Median :4.85                                                   
    ##  Mean   :4.63                                                   
    ##  3rd Qu.:4.85                                                   
    ##  Max.   :5.00                                                   
    ##  NA's   :9                                                      
    ##  Lab 4 - 2.h. - (Linear Discriminant Analysis) x/5
    ##  Min.   :1.850                                    
    ##  1st Qu.:4.100                                    
    ##  Median :4.850                                    
    ##  Mean   :4.425                                    
    ##  3rd Qu.:5.000                                    
    ##  Max.   :5.000                                    
    ##  NA's   :18                                       
    ##  Lab 5 - Chart JS Dashboard Setup x/5 Lab Work (7%) x/25 x 100
    ##  Min.   :0.000                        Min.   : 17.80          
    ##  1st Qu.:0.000                        1st Qu.: 70.80          
    ##  Median :5.000                        Median : 80.00          
    ##  Mean   :3.404                        Mean   : 79.72          
    ##  3rd Qu.:5.000                        3rd Qu.: 97.20          
    ##  Max.   :5.000                        Max.   :100.00          
    ##                                                               
    ##  CAT 1 (8%): x/38 x 100 CAT 2 (8%): x/100 x 100
    ##  Min.   :32.89          Min.   :  0.00         
    ##  1st Qu.:59.21          1st Qu.: 51.00         
    ##  Median :69.73          Median : 63.50         
    ##  Mean   :69.39          Mean   : 62.13         
    ##  3rd Qu.:82.89          3rd Qu.: 81.75         
    ##  Max.   :97.36          Max.   :100.00         
    ##  NA's   :4              NA's   :31             
    ##  Attendance Waiver Granted: 1 = Yes, 0 = No Absenteeism Percentage
    ##  Min.   :0.00000                            Min.   : 0.00         
    ##  1st Qu.:0.00000                            1st Qu.: 7.41         
    ##  Median :0.00000                            Median :14.81         
    ##  Mean   :0.04951                            Mean   :15.42         
    ##  3rd Qu.:0.00000                            3rd Qu.:22.22         
    ##  Max.   :1.00000                            Max.   :51.85         
    ##                                                                   
    ##  Coursework TOTAL: x/40 (40%) EXAM: x/60 (60%)
    ##  Min.   : 7.47                Min.   : 5.00   
    ##  1st Qu.:20.44                1st Qu.:26.00   
    ##  Median :24.58                Median :34.00   
    ##  Mean   :24.53                Mean   :33.94   
    ##  3rd Qu.:29.31                3rd Qu.:42.00   
    ##  Max.   :35.08                Max.   :56.00   
    ##                               NA's   :4       
    ##  TOTAL = Coursework TOTAL + EXAM (100%)    GRADE          
    ##  Min.   : 7.47                          Length:101        
    ##  1st Qu.:45.54                          Class :character  
    ##  Median :58.69                          Mode  :character  
    ##  Mean   :57.12                                            
    ##  3rd Qu.:68.83                                            
    ##  Max.   :87.72                                            
    ## 

``` r
model_of_the_transform <- preProcess(StudentPerformanceDataset, method = c("range"))
print(model_of_the_transform)
```

    ## Created from 51 samples and 99 variables
    ## 
    ## Pre-processing:
    ##   - ignored (4)
    ##   - re-scaling to [0, 1] (95)

``` r
student_performance_normalize_transform <- predict(model_of_the_transform, # nolint
                                                   StudentPerformanceDataset)
summary(student_performance_normalize_transform)
```

    ##  class_group            gender            YOB         regret_choosing_bi
    ##  Length:101         Min.   :0.0000   Min.   :0.0000   Min.   :0.0000    
    ##  Class :character   1st Qu.:0.0000   1st Qu.:0.4000   1st Qu.:0.0000    
    ##  Mode  :character   Median :1.0000   Median :0.6000   Median :0.0000    
    ##                     Mean   :0.5743   Mean   :0.5802   Mean   :0.0198    
    ##                     3rd Qu.:1.0000   3rd Qu.:0.8000   3rd Qu.:0.0000    
    ##                     Max.   :1.0000   Max.   :1.0000   Max.   :1.0000    
    ##                                                                         
    ##   drop_bi_now       motivator      read_content_before_lecture
    ##  Min.   :0.0000   Min.   :0.0000   Min.   :0.0000             
    ##  1st Qu.:0.0000   1st Qu.:1.0000   1st Qu.:0.2500             
    ##  Median :0.0000   Median :1.0000   Median :0.5000             
    ##  Mean   :0.0198   Mean   :0.7525   Mean   :0.4381             
    ##  3rd Qu.:0.0000   3rd Qu.:1.0000   3rd Qu.:0.5000             
    ##  Max.   :1.0000   Max.   :1.0000   Max.   :1.0000             
    ##                                                               
    ##  anticipate_test_questions answer_rhetorical_questions find_terms_I_do_not_know
    ##  Min.   :0.000             Min.   :0.0000              Min.   :0.0000          
    ##  1st Qu.:0.500             1st Qu.:0.5000              1st Qu.:0.5000          
    ##  Median :0.750             Median :0.7500              Median :0.7500          
    ##  Mean   :0.646             Mean   :0.6064              Mean   :0.6856          
    ##  3rd Qu.:0.750             3rd Qu.:0.7500              3rd Qu.:1.0000          
    ##  Max.   :1.000             Max.   :1.0000              Max.   :1.0000          
    ##                                                                                
    ##  copy_new_terms_in_reading_notebook take_quizzes_and_use_results
    ##  Min.   :0.0000                     Min.   :0.0000              
    ##  1st Qu.:0.5000                     1st Qu.:0.5000              
    ##  Median :0.7500                     Median :0.7500              
    ##  Mean   :0.6658                     Mean   :0.7351              
    ##  3rd Qu.:0.7500                     3rd Qu.:1.0000              
    ##  Max.   :1.0000                     Max.   :1.0000              
    ##                                                                 
    ##  reorganise_course_outline write_down_important_points space_out_revision
    ##  Min.   :0.0000            Min.   :0.0000              Min.   :0.0000    
    ##  1st Qu.:0.5000            1st Qu.:0.5000              1st Qu.:0.5000    
    ##  Median :0.5000            Median :0.7500              Median :0.5000    
    ##  Mean   :0.5941            Mean   :0.7079              Mean   :0.5569    
    ##  3rd Qu.:0.7500            3rd Qu.:1.0000              3rd Qu.:0.7500    
    ##  Max.   :1.0000            Max.   :1.0000              Max.   :1.0000    
    ##                                                                          
    ##  studying_in_study_group schedule_appointments goal_oriented  
    ##  Min.   :0.0000          Min.   :0.0000        Min.   :0.000  
    ##  1st Qu.:0.0000          1st Qu.:0.0000        1st Qu.:0.000  
    ##  Median :0.2500          Median :0.2500        Median :0.000  
    ##  Mean   :0.3639          Mean   :0.2327        Mean   :0.198  
    ##  3rd Qu.:0.5000          3rd Qu.:0.2500        3rd Qu.:0.000  
    ##  Max.   :1.0000          Max.   :1.0000        Max.   :1.000  
    ##                                                               
    ##  spaced_repetition testing_and_active_recall  interleaving     categorizing   
    ##  Min.   :0.0000    Min.   :0.0000            Min.   :0.0000   Min.   :0.0000  
    ##  1st Qu.:0.3333    1st Qu.:0.6667            1st Qu.:0.3333   1st Qu.:0.3333  
    ##  Median :0.6667    Median :0.6667            Median :0.3333   Median :0.6667  
    ##  Mean   :0.5182    Mean   :0.6865            Mean   :0.4191   Mean   :0.5710  
    ##  3rd Qu.:0.6667    3rd Qu.:1.0000            3rd Qu.:0.6667   3rd Qu.:0.6667  
    ##  Max.   :1.0000    Max.   :1.0000            Max.   :1.0000   Max.   :1.0000  
    ##                                                                               
    ##  retrospective_timetable cornell_notes         sq3r           commute      
    ##  Min.   :0.0000          Min.   :0.0000   Min.   :0.0000   Min.   :0.0000  
    ##  1st Qu.:0.3333          1st Qu.:0.3333   1st Qu.:0.3333   1st Qu.:0.3333  
    ##  Median :0.3333          Median :0.6667   Median :0.6667   Median :0.6667  
    ##  Mean   :0.4686          Mean   :0.5149   Mean   :0.5380   Mean   :0.5767  
    ##  3rd Qu.:0.6667          3rd Qu.:0.6667   3rd Qu.:0.6667   3rd Qu.:1.0000  
    ##  Max.   :1.0000          Max.   :1.0000   Max.   :1.0000   Max.   :1.0000  
    ##                                                            NA's   :1       
    ##    study_time     repeats_since_Y1  paid_tuition   free_tuition 
    ##  Min.   :0.0000   Min.   :0.000    Min.   :0.00   Min.   :0.00  
    ##  1st Qu.:0.0000   1st Qu.:0.000    1st Qu.:0.00   1st Qu.:0.00  
    ##  Median :0.3333   Median :0.200    Median :0.00   Median :0.00  
    ##  Mean   :0.2500   Mean   :0.205    Mean   :0.11   Mean   :0.27  
    ##  3rd Qu.:0.3333   3rd Qu.:0.300    3rd Qu.:0.00   3rd Qu.:1.00  
    ##  Max.   :1.0000   Max.   :1.000    Max.   :1.00   Max.   :1.00  
    ##  NA's   :1        NA's   :1        NA's   :1      NA's   :1     
    ##  extra_curricular sports_extra_curricular exercise_per_week    meditate     
    ##  Min.   :0.00     Min.   :0.00            Min.   :0.0000    Min.   :0.0000  
    ##  1st Qu.:0.00     1st Qu.:0.00            1st Qu.:0.3333    1st Qu.:0.0000  
    ##  Median :1.00     Median :0.00            Median :0.3333    Median :0.3333  
    ##  Mean   :0.53     Mean   :0.36            Mean   :0.3667    Mean   :0.2533  
    ##  3rd Qu.:1.00     3rd Qu.:1.00            3rd Qu.:0.6667    3rd Qu.:0.3333  
    ##  Max.   :1.00     Max.   :1.00            Max.   :1.0000    Max.   :1.0000  
    ##  NA's   :1        NA's   :1               NA's   :1         NA's   :1       
    ##       pray           internet        laptop  family_relationships
    ##  Min.   :0.0000   Min.   :0.00   Min.   :1   Min.   :0.0000      
    ##  1st Qu.:0.3333   1st Qu.:1.00   1st Qu.:1   1st Qu.:0.6667      
    ##  Median :0.6667   Median :1.00   Median :1   Median :0.6667      
    ##  Mean   :0.6967   Mean   :0.87   Mean   :1   Mean   :0.7300      
    ##  3rd Qu.:1.0000   3rd Qu.:1.00   3rd Qu.:1   3rd Qu.:1.0000      
    ##  Max.   :1.0000   Max.   :1.00   Max.   :1   Max.   :1.0000      
    ##  NA's   :1        NA's   :1      NA's   :1   NA's   :1           
    ##   friendships     romantic_relationships spiritual_wellnes financial_wellness
    ##  Min.   :0.0000   Min.   :0.0000         Min.   :0.0000    Min.   :0.0000    
    ##  1st Qu.:0.6667   1st Qu.:0.0000         1st Qu.:0.5000    1st Qu.:0.2500    
    ##  Median :0.6667   Median :0.0000         Median :0.7500    Median :0.5000    
    ##  Mean   :0.6700   Mean   :0.3425         Mean   :0.6625    Mean   :0.5075    
    ##  3rd Qu.:0.6667   3rd Qu.:0.7500         3rd Qu.:0.7500    3rd Qu.:0.7500    
    ##  Max.   :1.0000   Max.   :1.0000         Max.   :1.0000    Max.   :1.0000    
    ##  NA's   :1        NA's   :1              NA's   :1         NA's   :1         
    ##      health        day_out         night_out      alcohol_or_narcotics
    ##  Min.   :0.00   Min.   :0.0000   Min.   :0.0000   Min.   :0.0000      
    ##  1st Qu.:0.50   1st Qu.:0.0000   1st Qu.:0.0000   1st Qu.:0.0000      
    ##  Median :0.75   Median :0.3333   Median :0.0000   Median :0.0000      
    ##  Mean   :0.76   Mean   :0.2667   Mean   :0.1700   Mean   :0.1167      
    ##  3rd Qu.:1.00   3rd Qu.:0.3333   3rd Qu.:0.3333   3rd Qu.:0.3333      
    ##  Max.   :1.00   Max.   :1.0000   Max.   :1.0000   Max.   :1.0000      
    ##  NA's   :1      NA's   :1        NA's   :1        NA's   :1           
    ##      mentor     mentor_meetings  A - 1. I am enjoying the subject
    ##  Min.   :0.00   Min.   :0.0000   Min.   :0.000                   
    ##  1st Qu.:0.00   1st Qu.:0.0000   1st Qu.:0.500                   
    ##  Median :0.00   Median :0.0000   Median :1.000                   
    ##  Mean   :0.41   Mean   :0.2267   Mean   :0.745                   
    ##  3rd Qu.:1.00   3rd Qu.:0.3333   3rd Qu.:1.000                   
    ##  Max.   :1.00   Max.   :1.0000   Max.   :1.000                   
    ##  NA's   :1      NA's   :1        NA's   :1                       
    ##  A - 2. Classes start and end on time
    ##  Min.   :0.00                        
    ##  1st Qu.:0.50                        
    ##  Median :1.00                        
    ##  Mean   :0.84                        
    ##  3rd Qu.:1.00                        
    ##  Max.   :1.00                        
    ##  NA's   :1                           
    ##  A - 3. The learning environment is participative, involves learning by doing and is group-based
    ##  Min.   :0.000                                                                                  
    ##  1st Qu.:0.500                                                                                  
    ##  Median :0.500                                                                                  
    ##  Mean   :0.675                                                                                  
    ##  3rd Qu.:1.000                                                                                  
    ##  Max.   :1.000                                                                                  
    ##  NA's   :1                                                                                      
    ##  A - 4. The subject content is delivered according to the course outline and meets my expectations
    ##  Min.   :0.000                                                                                    
    ##  1st Qu.:0.875                                                                                    
    ##  Median :1.000                                                                                    
    ##  Mean   :0.870                                                                                    
    ##  3rd Qu.:1.000                                                                                    
    ##  Max.   :1.000                                                                                    
    ##  NA's   :1                                                                                        
    ##  A - 5. The topics are clear and logically developed
    ##  Min.   :0.0000                                     
    ##  1st Qu.:0.6667                                     
    ##  Median :1.0000                                     
    ##  Mean   :0.8833                                     
    ##  3rd Qu.:1.0000                                     
    ##  Max.   :1.0000                                     
    ##  NA's   :1                                          
    ##  A - 6. I am developing my oral and writing skills
    ##  Min.   :0.0000                                   
    ##  1st Qu.:0.7500                                   
    ##  Median :0.7500                                   
    ##  Mean   :0.7775                                   
    ##  3rd Qu.:1.0000                                   
    ##  Max.   :1.0000                                   
    ##  NA's   :1                                        
    ##  A - 7. I am developing my reflective and critical reasoning skills
    ##  Min.   :0.0000                                                    
    ##  1st Qu.:0.6667                                                    
    ##  Median :0.6667                                                    
    ##  Mean   :0.7933                                                    
    ##  3rd Qu.:1.0000                                                    
    ##  Max.   :1.0000                                                    
    ##  NA's   :1                                                         
    ##  A - 8. The assessment methods are assisting me to learn
    ##  Min.   :0.0000                                         
    ##  1st Qu.:0.7500                                         
    ##  Median :1.0000                                         
    ##  Mean   :0.9025                                         
    ##  3rd Qu.:1.0000                                         
    ##  Max.   :1.0000                                         
    ##  NA's   :1                                              
    ##  A - 9. I receive relevant feedback
    ##  Min.   :0.00                      
    ##  1st Qu.:0.50                      
    ##  Median :1.00                      
    ##  Mean   :0.79                      
    ##  3rd Qu.:1.00                      
    ##  Max.   :1.00                      
    ##  NA's   :1                         
    ##  A - 10. I read the recommended readings and notes
    ##  Min.   :0.000                                    
    ##  1st Qu.:0.500                                    
    ##  Median :1.000                                    
    ##  Mean   :0.775                                    
    ##  3rd Qu.:1.000                                    
    ##  Max.   :1.000                                    
    ##  NA's   :1                                        
    ##  A - 11. I use the eLearning material posted
    ##  Min.   :0.00                               
    ##  1st Qu.:0.50                               
    ##  Median :1.00                               
    ##  Mean   :0.85                               
    ##  3rd Qu.:1.00                               
    ##  Max.   :1.00                               
    ##  NA's   :1                                  
    ##  B - 1. Concept 1 of 6: Principles of Business Intelligence and the DataOps Philosophy
    ##  Min.   :0.0000                                                                       
    ##  1st Qu.:0.7500                                                                       
    ##  Median :0.7500                                                                       
    ##  Mean   :0.8125                                                                       
    ##  3rd Qu.:1.0000                                                                       
    ##  Max.   :1.0000                                                                       
    ##  NA's   :1                                                                            
    ##  B - 2. Concept 3 of 6: Linear Algorithms for Predictive Analytics
    ##  Min.   :0.0000                                                   
    ##  1st Qu.:0.3333                                                   
    ##  Median :0.6667                                                   
    ##  Mean   :0.6467                                                   
    ##  3rd Qu.:1.0000                                                   
    ##  Max.   :1.0000                                                   
    ##  NA's   :1                                                        
    ##  C - 2. Quizzes at the end of each concept
    ##  Min.   :0.0000                           
    ##  1st Qu.:0.6667                           
    ##  Median :1.0000                           
    ##  Mean   :0.8633                           
    ##  3rd Qu.:1.0000                           
    ##  Max.   :1.0000                           
    ##  NA's   :1                                
    ##  C - 3. Lab manuals that outline the steps to follow during the labs
    ##  Min.   :0.000                                                      
    ##  1st Qu.:0.500                                                      
    ##  Median :1.000                                                      
    ##  Mean   :0.805                                                      
    ##  3rd Qu.:1.000                                                      
    ##  Max.   :1.000                                                      
    ##  NA's   :1                                                          
    ##  C - 4. Required lab work submissions at the end of each lab manual that outline the activity to be done on your own
    ##  Min.   :0.000                                                                                                      
    ##  1st Qu.:0.500                                                                                                      
    ##  Median :1.000                                                                                                      
    ##  Mean   :0.775                                                                                                      
    ##  3rd Qu.:1.000                                                                                                      
    ##  Max.   :1.000                                                                                                      
    ##  NA's   :1                                                                                                          
    ##  C - 5. Supplementary videos to watch
    ##  Min.   :0.0000                      
    ##  1st Qu.:0.7500                      
    ##  Median :0.7500                      
    ##  Mean   :0.7975                      
    ##  3rd Qu.:1.0000                      
    ##  Max.   :1.0000                      
    ##  NA's   :1                           
    ##  C - 6. Supplementary podcasts to listen to
    ##  Min.   :0.00                              
    ##  1st Qu.:0.75                              
    ##  Median :0.75                              
    ##  Mean   :0.77                              
    ##  3rd Qu.:1.00                              
    ##  Max.   :1.00                              
    ##  NA's   :1                                 
    ##  C - 7. Supplementary content to read C - 8. Lectures slides
    ##  Min.   :0.0000                       Min.   :0.0000        
    ##  1st Qu.:0.7500                       1st Qu.:0.6667        
    ##  Median :0.7500                       Median :1.0000        
    ##  Mean   :0.7925                       Mean   :0.8667        
    ##  3rd Qu.:1.0000                       3rd Qu.:1.0000        
    ##  Max.   :1.0000                       Max.   :1.0000        
    ##  NA's   :1                            NA's   :1             
    ##  C - 9. Lecture notes on some of the lecture slides
    ##  Min.   :0.0000                                    
    ##  1st Qu.:0.6667                                    
    ##  Median :1.0000                                    
    ##  Mean   :0.8667                                    
    ##  3rd Qu.:1.0000                                    
    ##  Max.   :1.0000                                    
    ##  NA's   :1                                         
    ##  C - 10. The quality of the lectures given (quality measured by the breadth (the full span of knowledge of a subject) and depth (the extent to which specific topics are focused upon, amplified, and explored) of learning - NOT quality measured by how fun/comical/lively the lectures are)
    ##  Min.   :0.0000                                                                                                                                                                                                                                                                               
    ##  1st Qu.:0.6667                                                                                                                                                                                                                                                                               
    ##  Median :1.0000                                                                                                                                                                                                                                                                               
    ##  Mean   :0.8467                                                                                                                                                                                                                                                                               
    ##  3rd Qu.:1.0000                                                                                                                                                                                                                                                                               
    ##  Max.   :1.0000                                                                                                                                                                                                                                                                               
    ##  NA's   :1                                                                                                                                                                                                                                                                                    
    ##  C - 11. The division of theory and practice such that most of the theory is done during the recorded online classes and most of the practice is done during the physical classes
    ##  Min.   :0.0000                                                                                                                                                                  
    ##  1st Qu.:0.6667                                                                                                                                                                  
    ##  Median :1.0000                                                                                                                                                                  
    ##  Mean   :0.8300                                                                                                                                                                  
    ##  3rd Qu.:1.0000                                                                                                                                                                  
    ##  Max.   :1.0000                                                                                                                                                                  
    ##  NA's   :1                                                                                                                                                                       
    ##  C - 12. The recordings of online classes
    ##  Min.   :0.0000                          
    ##  1st Qu.:0.6667                          
    ##  Median :1.0000                          
    ##  Mean   :0.7767                          
    ##  3rd Qu.:1.0000                          
    ##  Max.   :1.0000                          
    ##  NA's   :1                               
    ##  D - 1. Write two things you like about the teaching and learning in this unit so far.
    ##  Length:101                                                                           
    ##  Class :character                                                                     
    ##  Mode  :character                                                                     
    ##                                                                                       
    ##                                                                                       
    ##                                                                                       
    ##                                                                                       
    ##  D - 2. Write at least one recommendation to improve the teaching and learning in this unit (for the remaining weeks in the semester)
    ##  Length:101                                                                                                                          
    ##  Class :character                                                                                                                    
    ##  Mode  :character                                                                                                                    
    ##                                                                                                                                      
    ##                                                                                                                                      
    ##                                                                                                                                      
    ##                                                                                                                                      
    ##  Average Course Evaluation Rating Average Level of Learning Attained Rating
    ##  Min.   :0.0000                   Min.   :0.0000                           
    ##  1st Qu.:0.6522                   1st Qu.:0.5000                           
    ##  Median :0.7826                   Median :0.6667                           
    ##  Mean   :0.7757                   Mean   :0.6983                           
    ##  3rd Qu.:0.9565                   3rd Qu.:0.8333                           
    ##  Max.   :1.0000                   Max.   :1.0000                           
    ##  NA's   :1                        NA's   :1                                
    ##  Average Pedagogical Strategy Effectiveness Rating
    ##  Min.   :0.0000                                   
    ##  1st Qu.:0.4875                                   
    ##  Median :0.7500                                   
    ##  Mean   :0.6875                                   
    ##  3rd Qu.:0.9500                                   
    ##  Max.   :1.0000                                   
    ##  NA's   :1                                        
    ##  Project: Section 1-4: (20%) x/10 Project: Section 5-11: (50%) x/10
    ##  Min.   :0.0000                   Min.   :0.0000                   
    ##  1st Qu.:0.7400                   1st Qu.:0.6000                   
    ##  Median :0.8500                   Median :0.7800                   
    ##  Mean   :0.8011                   Mean   :0.6582                   
    ##  3rd Qu.:0.9000                   3rd Qu.:0.8300                   
    ##  Max.   :1.0000                   Max.   :1.0000                   
    ##                                                                    
    ##  Project: Section 12: (30%) x/5 Project: (10%): x/30 x 100 TOTAL
    ##  Min.   :0.000                  Min.   :0.0000                  
    ##  1st Qu.:0.000                  1st Qu.:0.5600                  
    ##  Median :0.000                  Median :0.6640                  
    ##  Mean   :0.203                  Mean   :0.6239                  
    ##  3rd Qu.:0.250                  3rd Qu.:0.7160                  
    ##  Max.   :1.000                  Max.   :1.0000                  
    ##  NA's   :1                                                      
    ##  Quiz 1 on Concept 1 (Introduction) x/32 Quiz 3 on Concept 3 (Linear) x/15
    ##  Min.   :0.0000                          Min.   :0.0000                   
    ##  1st Qu.:0.2558                          1st Qu.:0.3333                   
    ##  Median :0.3992                          Median :0.5000                   
    ##  Mean   :0.4380                          Mean   :0.5442                   
    ##  3rd Qu.:0.5615                          3rd Qu.:0.7500                   
    ##  Max.   :1.0000                          Max.   :1.0000                   
    ##                                          NA's   :2                        
    ##  Quiz 4 on Concept 4 (Non-Linear) x/22 Quiz 5 on Concept 5 (Dashboarding) x/10
    ##  Min.   :0.0000                        Min.   :0.0000                         
    ##  1st Qu.:0.4166                        1st Qu.:0.3946                         
    ##  Median :0.5526                        Median :0.4996                         
    ##  Mean   :0.5756                        Mean   :0.5026                         
    ##  3rd Qu.:0.7632                        3rd Qu.:0.6314                         
    ##  Max.   :1.0000                        Max.   :1.0000                         
    ##  NA's   :6                             NA's   :12                             
    ##  Quizzes and  Bonus Marks (7%): x/79 x 100 TOTAL
    ##  Min.   :0.0000                                 
    ##  1st Qu.:0.2545                                 
    ##  Median :0.4211                                 
    ##  Mean   :0.4343                                 
    ##  3rd Qu.:0.5638                                 
    ##  Max.   :1.0000                                 
    ##                                                 
    ##  Lab 1 - 2.c. - (Simple Linear Regression) x/5
    ##  Min.   :0.000                                
    ##  1st Qu.:1.000                                
    ##  Median :1.000                                
    ##  Mean   :0.949                                
    ##  3rd Qu.:1.000                                
    ##  Max.   :1.000                                
    ##  NA's   :3                                    
    ##  Lab 2 - 2.e. -  (Linear Regression using Gradient Descent) x/5
    ##  Min.   :0.0000                                                
    ##  1st Qu.:0.3509                                                
    ##  Median :0.9474                                                
    ##  Mean   :0.7075                                                
    ##  3rd Qu.:1.0000                                                
    ##  Max.   :1.0000                                                
    ##  NA's   :6                                                     
    ##  Lab 3 - 2.g. - (Logistic Regression using Gradient Descent) x/5
    ##  Min.   :0.0000                                                 
    ##  1st Qu.:0.9302                                                 
    ##  Median :0.9302                                                 
    ##  Mean   :0.8280                                                 
    ##  3rd Qu.:0.9302                                                 
    ##  Max.   :1.0000                                                 
    ##  NA's   :9                                                      
    ##  Lab 4 - 2.h. - (Linear Discriminant Analysis) x/5
    ##  Min.   :0.0000                                   
    ##  1st Qu.:0.7143                                   
    ##  Median :0.9524                                   
    ##  Mean   :0.8174                                   
    ##  3rd Qu.:1.0000                                   
    ##  Max.   :1.0000                                   
    ##  NA's   :18                                       
    ##  Lab 5 - Chart JS Dashboard Setup x/5 Lab Work (7%) x/25 x 100
    ##  Min.   :0.0000                       Min.   :0.0000          
    ##  1st Qu.:0.0000                       1st Qu.:0.6448          
    ##  Median :1.0000                       Median :0.7567          
    ##  Mean   :0.6808                       Mean   :0.7532          
    ##  3rd Qu.:1.0000                       3rd Qu.:0.9659          
    ##  Max.   :1.0000                       Max.   :1.0000          
    ##                                                               
    ##  CAT 1 (8%): x/38 x 100 CAT 2 (8%): x/100 x 100
    ##  Min.   :0.0000         Min.   :0.0000         
    ##  1st Qu.:0.4083         1st Qu.:0.5100         
    ##  Median :0.5714         Median :0.6350         
    ##  Mean   :0.5662         Mean   :0.6213         
    ##  3rd Qu.:0.7756         3rd Qu.:0.8175         
    ##  Max.   :1.0000         Max.   :1.0000         
    ##  NA's   :4              NA's   :31             
    ##  Attendance Waiver Granted: 1 = Yes, 0 = No Absenteeism Percentage
    ##  Min.   :0.00000                            Min.   :0.0000        
    ##  1st Qu.:0.00000                            1st Qu.:0.1429        
    ##  Median :0.00000                            Median :0.2856        
    ##  Mean   :0.04951                            Mean   :0.2973        
    ##  3rd Qu.:0.00000                            3rd Qu.:0.4285        
    ##  Max.   :1.00000                            Max.   :1.0000        
    ##                                                                   
    ##  Coursework TOTAL: x/40 (40%) EXAM: x/60 (60%)
    ##  Min.   :0.0000               Min.   :0.0000  
    ##  1st Qu.:0.4698               1st Qu.:0.4118  
    ##  Median :0.6197               Median :0.5686  
    ##  Mean   :0.6177               Mean   :0.5674  
    ##  3rd Qu.:0.7910               3rd Qu.:0.7255  
    ##  Max.   :1.0000               Max.   :1.0000  
    ##                               NA's   :4       
    ##  TOTAL = Coursework TOTAL + EXAM (100%)    GRADE          
    ##  Min.   :0.0000                         Length:101        
    ##  1st Qu.:0.4744                         Class :character  
    ##  Median :0.6383                         Mode  :character  
    ##  Mean   :0.6187                                           
    ##  3rd Qu.:0.7646                                           
    ##  Max.   :1.0000                                           
    ## 

# Applying the Box Cox Data Transform

``` r
### Box-Cox Power Transform on the Student Performance Dataset ----
# BEFORE
summary(StudentPerformanceDataset)
```

    ##  class_group            gender            YOB       regret_choosing_bi
    ##  Length:101         Min.   :0.0000   Min.   :1998   Min.   :0.0000    
    ##  Class :character   1st Qu.:0.0000   1st Qu.:2000   1st Qu.:0.0000    
    ##  Mode  :character   Median :1.0000   Median :2001   Median :0.0000    
    ##                     Mean   :0.5743   Mean   :2001   Mean   :0.0198    
    ##                     3rd Qu.:1.0000   3rd Qu.:2002   3rd Qu.:0.0000    
    ##                     Max.   :1.0000   Max.   :2003   Max.   :1.0000    
    ##                                                                       
    ##   drop_bi_now       motivator      read_content_before_lecture
    ##  Min.   :0.0000   Min.   :0.0000   Min.   :1.000              
    ##  1st Qu.:0.0000   1st Qu.:1.0000   1st Qu.:2.000              
    ##  Median :0.0000   Median :1.0000   Median :3.000              
    ##  Mean   :0.0198   Mean   :0.7525   Mean   :2.752              
    ##  3rd Qu.:0.0000   3rd Qu.:1.0000   3rd Qu.:3.000              
    ##  Max.   :1.0000   Max.   :1.0000   Max.   :5.000              
    ##                                                               
    ##  anticipate_test_questions answer_rhetorical_questions find_terms_I_do_not_know
    ##  Min.   :1.000             Min.   :1.000               Min.   :1.000           
    ##  1st Qu.:3.000             1st Qu.:3.000               1st Qu.:3.000           
    ##  Median :4.000             Median :4.000               Median :4.000           
    ##  Mean   :3.584             Mean   :3.426               Mean   :3.743           
    ##  3rd Qu.:4.000             3rd Qu.:4.000               3rd Qu.:5.000           
    ##  Max.   :5.000             Max.   :5.000               Max.   :5.000           
    ##                                                                                
    ##  copy_new_terms_in_reading_notebook take_quizzes_and_use_results
    ##  Min.   :1.000                      Min.   :1.000               
    ##  1st Qu.:3.000                      1st Qu.:3.000               
    ##  Median :4.000                      Median :4.000               
    ##  Mean   :3.663                      Mean   :3.941               
    ##  3rd Qu.:4.000                      3rd Qu.:5.000               
    ##  Max.   :5.000                      Max.   :5.000               
    ##                                                                 
    ##  reorganise_course_outline write_down_important_points space_out_revision
    ##  Min.   :1.000             Min.   :1.000               Min.   :1.000     
    ##  1st Qu.:3.000             1st Qu.:3.000               1st Qu.:3.000     
    ##  Median :3.000             Median :4.000               Median :3.000     
    ##  Mean   :3.376             Mean   :3.832               Mean   :3.228     
    ##  3rd Qu.:4.000             3rd Qu.:5.000               3rd Qu.:4.000     
    ##  Max.   :5.000             Max.   :5.000               Max.   :5.000     
    ##                                                                          
    ##  studying_in_study_group schedule_appointments goal_oriented  
    ##  Min.   :1.000           Min.   :1.000         Min.   :0.000  
    ##  1st Qu.:1.000           1st Qu.:1.000         1st Qu.:0.000  
    ##  Median :2.000           Median :2.000         Median :0.000  
    ##  Mean   :2.455           Mean   :1.931         Mean   :0.198  
    ##  3rd Qu.:3.000           3rd Qu.:2.000         3rd Qu.:0.000  
    ##  Max.   :5.000           Max.   :5.000         Max.   :1.000  
    ##                                                               
    ##  spaced_repetition testing_and_active_recall  interleaving    categorizing  
    ##  Min.   :1.000     Min.   :1.000             Min.   :1.000   Min.   :1.000  
    ##  1st Qu.:2.000     1st Qu.:3.000             1st Qu.:2.000   1st Qu.:2.000  
    ##  Median :3.000     Median :3.000             Median :2.000   Median :3.000  
    ##  Mean   :2.554     Mean   :3.059             Mean   :2.257   Mean   :2.713  
    ##  3rd Qu.:3.000     3rd Qu.:4.000             3rd Qu.:3.000   3rd Qu.:3.000  
    ##  Max.   :4.000     Max.   :4.000             Max.   :4.000   Max.   :4.000  
    ##                                                                             
    ##  retrospective_timetable cornell_notes        sq3r          commute    
    ##  Min.   :1.000           Min.   :1.000   Min.   :1.000   Min.   :1.00  
    ##  1st Qu.:2.000           1st Qu.:2.000   1st Qu.:2.000   1st Qu.:2.00  
    ##  Median :2.000           Median :3.000   Median :3.000   Median :3.00  
    ##  Mean   :2.406           Mean   :2.545   Mean   :2.614   Mean   :2.73  
    ##  3rd Qu.:3.000           3rd Qu.:3.000   3rd Qu.:3.000   3rd Qu.:4.00  
    ##  Max.   :4.000           Max.   :4.000   Max.   :4.000   Max.   :4.00  
    ##                                                          NA's   :1     
    ##    study_time   repeats_since_Y1  paid_tuition   free_tuition  extra_curricular
    ##  Min.   :1.00   Min.   : 0.00    Min.   :0.00   Min.   :0.00   Min.   :0.00    
    ##  1st Qu.:1.00   1st Qu.: 0.00    1st Qu.:0.00   1st Qu.:0.00   1st Qu.:0.00    
    ##  Median :2.00   Median : 2.00    Median :0.00   Median :0.00   Median :1.00    
    ##  Mean   :1.75   Mean   : 2.05    Mean   :0.11   Mean   :0.27   Mean   :0.53    
    ##  3rd Qu.:2.00   3rd Qu.: 3.00    3rd Qu.:0.00   3rd Qu.:1.00   3rd Qu.:1.00    
    ##  Max.   :4.00   Max.   :10.00    Max.   :1.00   Max.   :1.00   Max.   :1.00    
    ##  NA's   :1      NA's   :1        NA's   :1      NA's   :1      NA's   :1       
    ##  sports_extra_curricular exercise_per_week    meditate         pray     
    ##  Min.   :0.00            Min.   :0.0       Min.   :0.00   Min.   :0.00  
    ##  1st Qu.:0.00            1st Qu.:1.0       1st Qu.:0.00   1st Qu.:1.00  
    ##  Median :0.00            Median :1.0       Median :1.00   Median :2.00  
    ##  Mean   :0.36            Mean   :1.1       Mean   :0.76   Mean   :2.09  
    ##  3rd Qu.:1.00            3rd Qu.:2.0       3rd Qu.:1.00   3rd Qu.:3.00  
    ##  Max.   :1.00            Max.   :3.0       Max.   :3.00   Max.   :3.00  
    ##  NA's   :1               NA's   :1         NA's   :1      NA's   :1     
    ##     internet        laptop  family_relationships  friendships  
    ##  Min.   :0.00   Min.   :1   Min.   :2.00         Min.   :2.00  
    ##  1st Qu.:1.00   1st Qu.:1   1st Qu.:4.00         1st Qu.:4.00  
    ##  Median :1.00   Median :1   Median :4.00         Median :4.00  
    ##  Mean   :0.87   Mean   :1   Mean   :4.19         Mean   :4.01  
    ##  3rd Qu.:1.00   3rd Qu.:1   3rd Qu.:5.00         3rd Qu.:4.00  
    ##  Max.   :1.00   Max.   :1   Max.   :5.00         Max.   :5.00  
    ##  NA's   :1      NA's   :1   NA's   :1            NA's   :1     
    ##  romantic_relationships spiritual_wellnes financial_wellness     health    
    ##  Min.   :0.00           Min.   :1.00      Min.   :1.00       Min.   :1.00  
    ##  1st Qu.:0.00           1st Qu.:3.00      1st Qu.:2.00       1st Qu.:3.00  
    ##  Median :0.00           Median :4.00      Median :3.00       Median :4.00  
    ##  Mean   :1.37           Mean   :3.65      Mean   :3.03       Mean   :4.04  
    ##  3rd Qu.:3.00           3rd Qu.:4.00      3rd Qu.:4.00       3rd Qu.:5.00  
    ##  Max.   :4.00           Max.   :5.00      Max.   :5.00       Max.   :5.00  
    ##  NA's   :1              NA's   :1         NA's   :1          NA's   :1     
    ##     day_out      night_out    alcohol_or_narcotics     mentor    
    ##  Min.   :0.0   Min.   :0.00   Min.   :0.00         Min.   :0.00  
    ##  1st Qu.:0.0   1st Qu.:0.00   1st Qu.:0.00         1st Qu.:0.00  
    ##  Median :1.0   Median :0.00   Median :0.00         Median :0.00  
    ##  Mean   :0.8   Mean   :0.51   Mean   :0.35         Mean   :0.41  
    ##  3rd Qu.:1.0   3rd Qu.:1.00   3rd Qu.:1.00         3rd Qu.:1.00  
    ##  Max.   :3.0   Max.   :3.00   Max.   :3.00         Max.   :1.00  
    ##  NA's   :1     NA's   :1      NA's   :1            NA's   :1     
    ##  mentor_meetings A - 1. I am enjoying the subject
    ##  Min.   :0.00    Min.   :3.00                    
    ##  1st Qu.:0.00    1st Qu.:4.00                    
    ##  Median :0.00    Median :5.00                    
    ##  Mean   :0.68    Mean   :4.49                    
    ##  3rd Qu.:1.00    3rd Qu.:5.00                    
    ##  Max.   :3.00    Max.   :5.00                    
    ##  NA's   :1       NA's   :1                       
    ##  A - 2. Classes start and end on time
    ##  Min.   :3.00                        
    ##  1st Qu.:4.00                        
    ##  Median :5.00                        
    ##  Mean   :4.68                        
    ##  3rd Qu.:5.00                        
    ##  Max.   :5.00                        
    ##  NA's   :1                           
    ##  A - 3. The learning environment is participative, involves learning by doing and is group-based
    ##  Min.   :3.00                                                                                   
    ##  1st Qu.:4.00                                                                                   
    ##  Median :4.00                                                                                   
    ##  Mean   :4.35                                                                                   
    ##  3rd Qu.:5.00                                                                                   
    ##  Max.   :5.00                                                                                   
    ##  NA's   :1                                                                                      
    ##  A - 4. The subject content is delivered according to the course outline and meets my expectations
    ##  Min.   :3.00                                                                                     
    ##  1st Qu.:4.75                                                                                     
    ##  Median :5.00                                                                                     
    ##  Mean   :4.74                                                                                     
    ##  3rd Qu.:5.00                                                                                     
    ##  Max.   :5.00                                                                                     
    ##  NA's   :1                                                                                        
    ##  A - 5. The topics are clear and logically developed
    ##  Min.   :2.00                                       
    ##  1st Qu.:4.00                                       
    ##  Median :5.00                                       
    ##  Mean   :4.65                                       
    ##  3rd Qu.:5.00                                       
    ##  Max.   :5.00                                       
    ##  NA's   :1                                          
    ##  A - 6. I am developing my oral and writing skills
    ##  Min.   :1.00                                     
    ##  1st Qu.:4.00                                     
    ##  Median :4.00                                     
    ##  Mean   :4.11                                     
    ##  3rd Qu.:5.00                                     
    ##  Max.   :5.00                                     
    ##  NA's   :1                                        
    ##  A - 7. I am developing my reflective and critical reasoning skills
    ##  Min.   :2.00                                                      
    ##  1st Qu.:4.00                                                      
    ##  Median :4.00                                                      
    ##  Mean   :4.38                                                      
    ##  3rd Qu.:5.00                                                      
    ##  Max.   :5.00                                                      
    ##  NA's   :1                                                         
    ##  A - 8. The assessment methods are assisting me to learn
    ##  Min.   :1.00                                           
    ##  1st Qu.:4.00                                           
    ##  Median :5.00                                           
    ##  Mean   :4.61                                           
    ##  3rd Qu.:5.00                                           
    ##  Max.   :5.00                                           
    ##  NA's   :1                                              
    ##  A - 9. I receive relevant feedback
    ##  Min.   :3.00                      
    ##  1st Qu.:4.00                      
    ##  Median :5.00                      
    ##  Mean   :4.58                      
    ##  3rd Qu.:5.00                      
    ##  Max.   :5.00                      
    ##  NA's   :1                         
    ##  A - 10. I read the recommended readings and notes
    ##  Min.   :3.00                                     
    ##  1st Qu.:4.00                                     
    ##  Median :5.00                                     
    ##  Mean   :4.55                                     
    ##  3rd Qu.:5.00                                     
    ##  Max.   :5.00                                     
    ##  NA's   :1                                        
    ##  A - 11. I use the eLearning material posted
    ##  Min.   :3.0                                
    ##  1st Qu.:4.0                                
    ##  Median :5.0                                
    ##  Mean   :4.7                                
    ##  3rd Qu.:5.0                                
    ##  Max.   :5.0                                
    ##  NA's   :1                                  
    ##  B - 1. Concept 1 of 6: Principles of Business Intelligence and the DataOps Philosophy
    ##  Min.   :1.00                                                                         
    ##  1st Qu.:4.00                                                                         
    ##  Median :4.00                                                                         
    ##  Mean   :4.25                                                                         
    ##  3rd Qu.:5.00                                                                         
    ##  Max.   :5.00                                                                         
    ##  NA's   :1                                                                            
    ##  B - 2. Concept 3 of 6: Linear Algorithms for Predictive Analytics
    ##  Min.   :2.00                                                     
    ##  1st Qu.:3.00                                                     
    ##  Median :4.00                                                     
    ##  Mean   :3.94                                                     
    ##  3rd Qu.:5.00                                                     
    ##  Max.   :5.00                                                     
    ##  NA's   :1                                                        
    ##  C - 2. Quizzes at the end of each concept
    ##  Min.   :2.00                             
    ##  1st Qu.:4.00                             
    ##  Median :5.00                             
    ##  Mean   :4.59                             
    ##  3rd Qu.:5.00                             
    ##  Max.   :5.00                             
    ##  NA's   :1                                
    ##  C - 3. Lab manuals that outline the steps to follow during the labs
    ##  Min.   :3.00                                                       
    ##  1st Qu.:4.00                                                       
    ##  Median :5.00                                                       
    ##  Mean   :4.61                                                       
    ##  3rd Qu.:5.00                                                       
    ##  Max.   :5.00                                                       
    ##  NA's   :1                                                          
    ##  C - 4. Required lab work submissions at the end of each lab manual that outline the activity to be done on your own
    ##  Min.   :3.00                                                                                                       
    ##  1st Qu.:4.00                                                                                                       
    ##  Median :5.00                                                                                                       
    ##  Mean   :4.55                                                                                                       
    ##  3rd Qu.:5.00                                                                                                       
    ##  Max.   :5.00                                                                                                       
    ##  NA's   :1                                                                                                          
    ##  C - 5. Supplementary videos to watch
    ##  Min.   :1.00                        
    ##  1st Qu.:4.00                        
    ##  Median :4.00                        
    ##  Mean   :4.19                        
    ##  3rd Qu.:5.00                        
    ##  Max.   :5.00                        
    ##  NA's   :1                           
    ##  C - 6. Supplementary podcasts to listen to
    ##  Min.   :1.00                              
    ##  1st Qu.:4.00                              
    ##  Median :4.00                              
    ##  Mean   :4.08                              
    ##  3rd Qu.:5.00                              
    ##  Max.   :5.00                              
    ##  NA's   :1                                 
    ##  C - 7. Supplementary content to read C - 8. Lectures slides
    ##  Min.   :1.00                         Min.   :2.0           
    ##  1st Qu.:4.00                         1st Qu.:4.0           
    ##  Median :4.00                         Median :5.0           
    ##  Mean   :4.17                         Mean   :4.6           
    ##  3rd Qu.:5.00                         3rd Qu.:5.0           
    ##  Max.   :5.00                         Max.   :5.0           
    ##  NA's   :1                            NA's   :1             
    ##  C - 9. Lecture notes on some of the lecture slides
    ##  Min.   :2.0                                       
    ##  1st Qu.:4.0                                       
    ##  Median :5.0                                       
    ##  Mean   :4.6                                       
    ##  3rd Qu.:5.0                                       
    ##  Max.   :5.0                                       
    ##  NA's   :1                                         
    ##  C - 10. The quality of the lectures given (quality measured by the breadth (the full span of knowledge of a subject) and depth (the extent to which specific topics are focused upon, amplified, and explored) of learning - NOT quality measured by how fun/comical/lively the lectures are)
    ##  Min.   :2.00                                                                                                                                                                                                                                                                                 
    ##  1st Qu.:4.00                                                                                                                                                                                                                                                                                 
    ##  Median :5.00                                                                                                                                                                                                                                                                                 
    ##  Mean   :4.54                                                                                                                                                                                                                                                                                 
    ##  3rd Qu.:5.00                                                                                                                                                                                                                                                                                 
    ##  Max.   :5.00                                                                                                                                                                                                                                                                                 
    ##  NA's   :1                                                                                                                                                                                                                                                                                    
    ##  C - 11. The division of theory and practice such that most of the theory is done during the recorded online classes and most of the practice is done during the physical classes
    ##  Min.   :2.00                                                                                                                                                                    
    ##  1st Qu.:4.00                                                                                                                                                                    
    ##  Median :5.00                                                                                                                                                                    
    ##  Mean   :4.49                                                                                                                                                                    
    ##  3rd Qu.:5.00                                                                                                                                                                    
    ##  Max.   :5.00                                                                                                                                                                    
    ##  NA's   :1                                                                                                                                                                       
    ##  C - 12. The recordings of online classes
    ##  Min.   :2.00                            
    ##  1st Qu.:4.00                            
    ##  Median :5.00                            
    ##  Mean   :4.33                            
    ##  3rd Qu.:5.00                            
    ##  Max.   :5.00                            
    ##  NA's   :1                               
    ##  D - 1. Write two things you like about the teaching and learning in this unit so far.
    ##  Length:101                                                                           
    ##  Class :character                                                                     
    ##  Mode  :character                                                                     
    ##                                                                                       
    ##                                                                                       
    ##                                                                                       
    ##                                                                                       
    ##  D - 2. Write at least one recommendation to improve the teaching and learning in this unit (for the remaining weeks in the semester)
    ##  Length:101                                                                                                                          
    ##  Class :character                                                                                                                    
    ##  Mode  :character                                                                                                                    
    ##                                                                                                                                      
    ##                                                                                                                                      
    ##                                                                                                                                      
    ##                                                                                                                                      
    ##  Average Course Evaluation Rating Average Level of Learning Attained Rating
    ##  Min.   :2.909                    Min.   :2.000                            
    ##  1st Qu.:4.273                    1st Qu.:3.500                            
    ##  Median :4.545                    Median :4.000                            
    ##  Mean   :4.531                    Mean   :4.095                            
    ##  3rd Qu.:4.909                    3rd Qu.:4.500                            
    ##  Max.   :5.000                    Max.   :5.000                            
    ##  NA's   :1                        NA's   :1                                
    ##  Average Pedagogical Strategy Effectiveness Rating
    ##  Min.   :3.182                                    
    ##  1st Qu.:4.068                                    
    ##  Median :4.545                                    
    ##  Mean   :4.432                                    
    ##  3rd Qu.:4.909                                    
    ##  Max.   :5.000                                    
    ##  NA's   :1                                        
    ##  Project: Section 1-4: (20%) x/10 Project: Section 5-11: (50%) x/10
    ##  Min.   : 0.000                   Min.   : 0.000                   
    ##  1st Qu.: 7.400                   1st Qu.: 6.000                   
    ##  Median : 8.500                   Median : 7.800                   
    ##  Mean   : 8.011                   Mean   : 6.582                   
    ##  3rd Qu.: 9.000                   3rd Qu.: 8.300                   
    ##  Max.   :10.000                   Max.   :10.000                   
    ##                                                                    
    ##  Project: Section 12: (30%) x/5 Project: (10%): x/30 x 100 TOTAL
    ##  Min.   :0.000                  Min.   :  0.00                  
    ##  1st Qu.:0.000                  1st Qu.: 56.00                  
    ##  Median :0.000                  Median : 66.40                  
    ##  Mean   :1.015                  Mean   : 62.39                  
    ##  3rd Qu.:1.250                  3rd Qu.: 71.60                  
    ##  Max.   :5.000                  Max.   :100.00                  
    ##  NA's   :1                                                      
    ##  Quiz 1 on Concept 1 (Introduction) x/32 Quiz 3 on Concept 3 (Linear) x/15
    ##  Min.   : 4.75                           Min.   : 3.00                    
    ##  1st Qu.:11.53                           1st Qu.: 7.00                    
    ##  Median :15.33                           Median : 9.00                    
    ##  Mean   :16.36                           Mean   : 9.53                    
    ##  3rd Qu.:19.63                           3rd Qu.:12.00                    
    ##  Max.   :31.25                           Max.   :15.00                    
    ##                                          NA's   :2                        
    ##  Quiz 4 on Concept 4 (Non-Linear) x/22 Quiz 5 on Concept 5 (Dashboarding) x/10
    ##  Min.   : 3.00                         Min.   : 0.000                         
    ##  1st Qu.:10.91                         1st Qu.: 5.000                         
    ##  Median :13.50                         Median : 6.330                         
    ##  Mean   :13.94                         Mean   : 6.367                         
    ##  3rd Qu.:17.50                         3rd Qu.: 8.000                         
    ##  Max.   :22.00                         Max.   :12.670                         
    ##  NA's   :6                             NA's   :12                             
    ##  Quizzes and  Bonus Marks (7%): x/79 x 100 TOTAL
    ##  Min.   :26.26                                  
    ##  1st Qu.:43.82                                  
    ##  Median :55.31                                  
    ##  Mean   :56.22                                  
    ##  3rd Qu.:65.16                                  
    ##  Max.   :95.25                                  
    ##                                                 
    ##  Lab 1 - 2.c. - (Simple Linear Regression) x/5
    ##  Min.   :3.000                                
    ##  1st Qu.:5.000                                
    ##  Median :5.000                                
    ##  Mean   :4.898                                
    ##  3rd Qu.:5.000                                
    ##  Max.   :5.000                                
    ##  NA's   :3                                    
    ##  Lab 2 - 2.e. -  (Linear Regression using Gradient Descent) x/5
    ##  Min.   :2.150                                                 
    ##  1st Qu.:3.150                                                 
    ##  Median :4.850                                                 
    ##  Mean   :4.166                                                 
    ##  3rd Qu.:5.000                                                 
    ##  Max.   :5.000                                                 
    ##  NA's   :6                                                     
    ##  Lab 3 - 2.g. - (Logistic Regression using Gradient Descent) x/5
    ##  Min.   :2.85                                                   
    ##  1st Qu.:4.85                                                   
    ##  Median :4.85                                                   
    ##  Mean   :4.63                                                   
    ##  3rd Qu.:4.85                                                   
    ##  Max.   :5.00                                                   
    ##  NA's   :9                                                      
    ##  Lab 4 - 2.h. - (Linear Discriminant Analysis) x/5
    ##  Min.   :1.850                                    
    ##  1st Qu.:4.100                                    
    ##  Median :4.850                                    
    ##  Mean   :4.425                                    
    ##  3rd Qu.:5.000                                    
    ##  Max.   :5.000                                    
    ##  NA's   :18                                       
    ##  Lab 5 - Chart JS Dashboard Setup x/5 Lab Work (7%) x/25 x 100
    ##  Min.   :0.000                        Min.   : 17.80          
    ##  1st Qu.:0.000                        1st Qu.: 70.80          
    ##  Median :5.000                        Median : 80.00          
    ##  Mean   :3.404                        Mean   : 79.72          
    ##  3rd Qu.:5.000                        3rd Qu.: 97.20          
    ##  Max.   :5.000                        Max.   :100.00          
    ##                                                               
    ##  CAT 1 (8%): x/38 x 100 CAT 2 (8%): x/100 x 100
    ##  Min.   :32.89          Min.   :  0.00         
    ##  1st Qu.:59.21          1st Qu.: 51.00         
    ##  Median :69.73          Median : 63.50         
    ##  Mean   :69.39          Mean   : 62.13         
    ##  3rd Qu.:82.89          3rd Qu.: 81.75         
    ##  Max.   :97.36          Max.   :100.00         
    ##  NA's   :4              NA's   :31             
    ##  Attendance Waiver Granted: 1 = Yes, 0 = No Absenteeism Percentage
    ##  Min.   :0.00000                            Min.   : 0.00         
    ##  1st Qu.:0.00000                            1st Qu.: 7.41         
    ##  Median :0.00000                            Median :14.81         
    ##  Mean   :0.04951                            Mean   :15.42         
    ##  3rd Qu.:0.00000                            3rd Qu.:22.22         
    ##  Max.   :1.00000                            Max.   :51.85         
    ##                                                                   
    ##  Coursework TOTAL: x/40 (40%) EXAM: x/60 (60%)
    ##  Min.   : 7.47                Min.   : 5.00   
    ##  1st Qu.:20.44                1st Qu.:26.00   
    ##  Median :24.58                Median :34.00   
    ##  Mean   :24.53                Mean   :33.94   
    ##  3rd Qu.:29.31                3rd Qu.:42.00   
    ##  Max.   :35.08                Max.   :56.00   
    ##                               NA's   :4       
    ##  TOTAL = Coursework TOTAL + EXAM (100%)    GRADE          
    ##  Min.   : 7.47                          Length:101        
    ##  1st Qu.:45.54                          Class :character  
    ##  Median :58.69                          Mode  :character  
    ##  Mean   :57.12                                            
    ##  3rd Qu.:68.83                                            
    ##  Max.   :87.72                                            
    ## 

``` r
StudentPerformanceDataset <- as.data.frame(StudentPerformanceDataset)


#Calculate the skewness before the Box-Cox transform

sapply(StudentPerformanceDataset[, 7:13], skewness, type = 2)
```

    ##        read_content_before_lecture          anticipate_test_questions 
    ##                         0.03938034                        -0.70731706 
    ##        answer_rhetorical_questions           find_terms_I_do_not_know 
    ##                        -0.32097933                        -0.81939607 
    ## copy_new_terms_in_reading_notebook       take_quizzes_and_use_results 
    ##                        -0.64953356                        -0.91362634 
    ##          reorganise_course_outline 
    ##                        -0.34506777

``` r
#Plot a histogram to view the skewness before the Box-Cox transform


hist(StudentPerformanceDataset[, 7], main = names(StudentPerformanceDataset)[7])
```

![](BIProject-Template_files/figure-gfm/Applying%20Box%20Cox%20Data%20Transform-1.png)<!-- -->

``` r
hist(StudentPerformanceDataset[, 8], main = names(StudentPerformanceDataset)[8])
```

![](BIProject-Template_files/figure-gfm/Applying%20Box%20Cox%20Data%20Transform-2.png)<!-- -->

``` r
hist(StudentPerformanceDataset[, 9], main = names(StudentPerformanceDataset)[9])
```

![](BIProject-Template_files/figure-gfm/Applying%20Box%20Cox%20Data%20Transform-3.png)<!-- -->

``` r
hist(StudentPerformanceDataset[, 10], main = names(StudentPerformanceDataset)[10])
```

![](BIProject-Template_files/figure-gfm/Applying%20Box%20Cox%20Data%20Transform-4.png)<!-- -->

``` r
hist(StudentPerformanceDataset[, 11], main = names(StudentPerformanceDataset)[11])
```

![](BIProject-Template_files/figure-gfm/Applying%20Box%20Cox%20Data%20Transform-5.png)<!-- -->

``` r
hist(StudentPerformanceDataset[, 12], main = names(StudentPerformanceDataset)[12])
```

![](BIProject-Template_files/figure-gfm/Applying%20Box%20Cox%20Data%20Transform-6.png)<!-- -->

``` r
hist(StudentPerformanceDataset[, 13], main = names(StudentPerformanceDataset)[13])
```

![](BIProject-Template_files/figure-gfm/Applying%20Box%20Cox%20Data%20Transform-7.png)<!-- -->

``` r
StudentPerformanceDataset <- as.data.frame(StudentPerformanceDataset)  # Convert to data frame if needed
preprocessed_data <- preProcess(StudentPerformanceDataset)

model_of_the_transform <- preProcess(StudentPerformanceDataset, method = c("BoxCox"))
print(model_of_the_transform)
```

    ## Created from 51 samples and 70 variables
    ## 
    ## Pre-processing:
    ##   - Box-Cox transformation (66)
    ##   - ignored (4)
    ## 
    ## Lambda estimates for Box-Cox transformation:
    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##  -0.500   1.125   2.000   1.552   2.000   2.000

``` r
student_performance_box_cox_transform <- predict(model_of_the_transform, # nolint
                                            StudentPerformanceDataset)

# AFTER
summary(student_performance_box_cox_transform)
```

    ##  class_group            gender            YOB          regret_choosing_bi
    ##  Length:101         Min.   :0.0000   Min.   :1996002   Min.   :0.0000    
    ##  Class :character   1st Qu.:0.0000   1st Qu.:2000000   1st Qu.:0.0000    
    ##  Mode  :character   Median :1.0000   Median :2002000   Median :0.0000    
    ##                     Mean   :0.5743   Mean   :2001802   Mean   :0.0198    
    ##                     3rd Qu.:1.0000   3rd Qu.:2004002   3rd Qu.:0.0000    
    ##                     Max.   :1.0000   Max.   :2006004   Max.   :1.0000    
    ##                                                                          
    ##   drop_bi_now       motivator      read_content_before_lecture
    ##  Min.   :0.0000   Min.   :0.0000   Min.   :1.000              
    ##  1st Qu.:0.0000   1st Qu.:1.0000   1st Qu.:2.000              
    ##  Median :0.0000   Median :1.0000   Median :3.000              
    ##  Mean   :0.0198   Mean   :0.7525   Mean   :2.752              
    ##  3rd Qu.:0.0000   3rd Qu.:1.0000   3rd Qu.:3.000              
    ##  Max.   :1.0000   Max.   :1.0000   Max.   :5.000              
    ##                                                               
    ##  anticipate_test_questions answer_rhetorical_questions find_terms_I_do_not_know
    ##  Min.   :0.000             Min.   :0.000               Min.   :0.000           
    ##  1st Qu.:3.219             1st Qu.:2.439               1st Qu.:3.219           
    ##  Median :5.621             Median :3.895               Median :5.621           
    ##  Mean   :4.804             Mean   :3.108               Mean   :5.226           
    ##  3rd Qu.:5.621             3rd Qu.:3.895               3rd Qu.:8.486           
    ##  Max.   :8.486             Max.   :5.464               Max.   :8.486           
    ##                                                                                
    ##  copy_new_terms_in_reading_notebook take_quizzes_and_use_results
    ##  Min.   :0.000                      Min.   : 0.000              
    ##  1st Qu.:3.000                      1st Qu.: 4.000              
    ##  Median :5.118                      Median : 7.500              
    ##  Mean   :4.591                      Mean   : 7.837              
    ##  3rd Qu.:5.118                      3rd Qu.:12.000              
    ##  Max.   :7.583                      Max.   :12.000              
    ##                                                                 
    ##  reorganise_course_outline write_down_important_points space_out_revision
    ##  Min.   :0.000             Min.   : 0.000              Min.   :1.000     
    ##  1st Qu.:2.281             1st Qu.: 3.718              1st Qu.:3.000     
    ##  Median :2.281             Median : 6.805              Median :3.000     
    ##  Mean   :2.809             Mean   : 6.687              Mean   :3.228     
    ##  3rd Qu.:3.565             3rd Qu.:10.676              3rd Qu.:4.000     
    ##  Max.   :4.916             Max.   :10.676              Max.   :5.000     
    ##                                                                          
    ##  studying_in_study_group schedule_appointments goal_oriented  
    ##  Min.   :0.0000          Min.   :0.0000        Min.   :0.000  
    ##  1st Qu.:0.0000          1st Qu.:0.0000        1st Qu.:0.000  
    ##  Median :0.6931          Median :0.6054        Median :0.000  
    ##  Mean   :0.7356          Mean   :0.4385        Mean   :0.198  
    ##  3rd Qu.:1.0986          3rd Qu.:0.6054        3rd Qu.:0.000  
    ##  Max.   :1.6094          Max.   :1.1867        Max.   :1.000  
    ##                                                               
    ##  spaced_repetition testing_and_active_recall  interleaving    categorizing  
    ##  Min.   :0.000     Min.   :0.000             Min.   :1.000   Min.   :0.000  
    ##  1st Qu.:1.081     1st Qu.:2.797             1st Qu.:2.000   1st Qu.:1.171  
    ##  Median :2.281     Median :2.797             Median :2.000   Median :2.611  
    ##  Mean   :1.769     Mean   :2.976             Mean   :2.257   Mean   :2.236  
    ##  3rd Qu.:2.281     3rd Qu.:4.667             3rd Qu.:3.000   3rd Qu.:2.611  
    ##  Max.   :3.565     Max.   :4.667             Max.   :4.000   Max.   :4.260  
    ##                                                                             
    ##  retrospective_timetable cornell_notes        sq3r          commute    
    ##  Min.   :1.000           Min.   :1.000   Min.   :1.000   Min.   :1.00  
    ##  1st Qu.:2.000           1st Qu.:2.000   1st Qu.:2.000   1st Qu.:2.00  
    ##  Median :2.000           Median :3.000   Median :3.000   Median :3.00  
    ##  Mean   :2.406           Mean   :2.545   Mean   :2.614   Mean   :2.73  
    ##  3rd Qu.:3.000           3rd Qu.:3.000   3rd Qu.:3.000   3rd Qu.:4.00  
    ##  Max.   :4.000           Max.   :4.000   Max.   :4.000   Max.   :4.00  
    ##                                                          NA's   :1     
    ##    study_time     repeats_since_Y1  paid_tuition   free_tuition 
    ##  Min.   :0.0000   Min.   : 0.00    Min.   :0.00   Min.   :0.00  
    ##  1st Qu.:0.0000   1st Qu.: 0.00    1st Qu.:0.00   1st Qu.:0.00  
    ##  Median :0.5858   Median : 2.00    Median :0.00   Median :0.00  
    ##  Mean   :0.3699   Mean   : 2.05    Mean   :0.11   Mean   :0.27  
    ##  3rd Qu.:0.5858   3rd Qu.: 3.00    3rd Qu.:0.00   3rd Qu.:1.00  
    ##  Max.   :1.0000   Max.   :10.00    Max.   :1.00   Max.   :1.00  
    ##  NA's   :1        NA's   :1        NA's   :1      NA's   :1     
    ##  extra_curricular sports_extra_curricular exercise_per_week    meditate   
    ##  Min.   :0.00     Min.   :0.00            Min.   :0.0       Min.   :0.00  
    ##  1st Qu.:0.00     1st Qu.:0.00            1st Qu.:1.0       1st Qu.:0.00  
    ##  Median :1.00     Median :0.00            Median :1.0       Median :1.00  
    ##  Mean   :0.53     Mean   :0.36            Mean   :1.1       Mean   :0.76  
    ##  3rd Qu.:1.00     3rd Qu.:1.00            3rd Qu.:2.0       3rd Qu.:1.00  
    ##  Max.   :1.00     Max.   :1.00            Max.   :3.0       Max.   :3.00  
    ##  NA's   :1        NA's   :1               NA's   :1         NA's   :1     
    ##       pray         internet        laptop  family_relationships  friendships   
    ##  Min.   :0.00   Min.   :0.00   Min.   :1   Min.   : 1.500       Min.   :1.379  
    ##  1st Qu.:1.00   1st Qu.:1.00   1st Qu.:1   1st Qu.: 7.500       1st Qu.:6.181  
    ##  Median :2.00   Median :1.00   Median :1   Median : 7.500       Median :6.181  
    ##  Mean   :2.09   Mean   :0.87   Mean   :1   Mean   : 8.595       Mean   :6.373  
    ##  3rd Qu.:3.00   3rd Qu.:1.00   3rd Qu.:1   3rd Qu.:12.000       3rd Qu.:6.181  
    ##  Max.   :3.00   Max.   :1.00   Max.   :1   Max.   :12.000       Max.   :9.511  
    ##  NA's   :1      NA's   :1      NA's   :1   NA's   :1            NA's   :1      
    ##  romantic_relationships spiritual_wellnes financial_wellness     health     
    ##  Min.   :0.00           Min.   :1.00      Min.   :1.00       Min.   : 0.00  
    ##  1st Qu.:0.00           1st Qu.:3.00      1st Qu.:2.00       1st Qu.: 4.00  
    ##  Median :0.00           Median :4.00      Median :3.00       Median : 7.50  
    ##  Mean   :1.37           Mean   :3.65      Mean   :3.03       Mean   : 8.11  
    ##  3rd Qu.:3.00           3rd Qu.:4.00      3rd Qu.:4.00       3rd Qu.:12.00  
    ##  Max.   :4.00           Max.   :5.00      Max.   :5.00       Max.   :12.00  
    ##  NA's   :1              NA's   :1         NA's   :1          NA's   :1      
    ##     day_out      night_out    alcohol_or_narcotics     mentor    
    ##  Min.   :0.0   Min.   :0.00   Min.   :0.00         Min.   :0.00  
    ##  1st Qu.:0.0   1st Qu.:0.00   1st Qu.:0.00         1st Qu.:0.00  
    ##  Median :1.0   Median :0.00   Median :0.00         Median :0.00  
    ##  Mean   :0.8   Mean   :0.51   Mean   :0.35         Mean   :0.41  
    ##  3rd Qu.:1.0   3rd Qu.:1.00   3rd Qu.:1.00         3rd Qu.:1.00  
    ##  Max.   :3.0   Max.   :3.00   Max.   :3.00         Max.   :1.00  
    ##  NA's   :1     NA's   :1      NA's   :1            NA's   :1     
    ##  mentor_meetings A - 1. I am enjoying the subject
    ##  Min.   :0.00    Min.   : 4.000                  
    ##  1st Qu.:0.00    1st Qu.: 7.500                  
    ##  Median :0.00    Median :12.000                  
    ##  Mean   :0.68    Mean   : 9.755                  
    ##  3rd Qu.:1.00    3rd Qu.:12.000                  
    ##  Max.   :3.00    Max.   :12.000                  
    ##  NA's   :1       NA's   :1                       
    ##  A - 2. Classes start and end on time
    ##  Min.   : 4.00                       
    ##  1st Qu.: 7.50                       
    ##  Median :12.00                       
    ##  Mean   :10.57                       
    ##  3rd Qu.:12.00                       
    ##  Max.   :12.00                       
    ##  NA's   :1                           
    ##  A - 3. The learning environment is participative, involves learning by doing and is group-based
    ##  Min.   : 4.000                                                                                 
    ##  1st Qu.: 7.500                                                                                 
    ##  Median : 7.500                                                                                 
    ##  Mean   : 9.175                                                                                 
    ##  3rd Qu.:12.000                                                                                 
    ##  Max.   :12.000                                                                                 
    ##  NA's   :1                                                                                      
    ##  A - 4. The subject content is delivered according to the course outline and meets my expectations
    ##  Min.   : 4.00                                                                                    
    ##  1st Qu.:10.88                                                                                    
    ##  Median :12.00                                                                                    
    ##  Mean   :10.84                                                                                    
    ##  3rd Qu.:12.00                                                                                    
    ##  Max.   :12.00                                                                                    
    ##  NA's   :1                                                                                        
    ##  A - 5. The topics are clear and logically developed
    ##  Min.   : 1.50                                      
    ##  1st Qu.: 7.50                                      
    ##  Median :12.00                                      
    ##  Mean   :10.47                                      
    ##  3rd Qu.:12.00                                      
    ##  Max.   :12.00                                      
    ##  NA's   :1                                          
    ##  A - 6. I am developing my oral and writing skills
    ##  Min.   : 0.000                                   
    ##  1st Qu.: 7.500                                   
    ##  Median : 7.500                                   
    ##  Mean   : 8.325                                   
    ##  3rd Qu.:12.000                                   
    ##  Max.   :12.000                                   
    ##  NA's   :1                                        
    ##  A - 7. I am developing my reflective and critical reasoning skills
    ##  Min.   : 1.50                                                     
    ##  1st Qu.: 7.50                                                     
    ##  Median : 7.50                                                     
    ##  Mean   : 9.33                                                     
    ##  3rd Qu.:12.00                                                     
    ##  Max.   :12.00                                                     
    ##  NA's   :1                                                         
    ##  A - 8. The assessment methods are assisting me to learn
    ##  Min.   : 0.00                                          
    ##  1st Qu.: 7.50                                          
    ##  Median :12.00                                          
    ##  Mean   :10.34                                          
    ##  3rd Qu.:12.00                                          
    ##  Max.   :12.00                                          
    ##  NA's   :1                                              
    ##  A - 9. I receive relevant feedback
    ##  Min.   : 4.00                     
    ##  1st Qu.: 7.50                     
    ##  Median :12.00                     
    ##  Mean   :10.14                     
    ##  3rd Qu.:12.00                     
    ##  Max.   :12.00                     
    ##  NA's   :1                         
    ##  A - 10. I read the recommended readings and notes
    ##  Min.   : 4.00                                    
    ##  1st Qu.: 7.50                                    
    ##  Median :12.00                                    
    ##  Mean   :10.04                                    
    ##  3rd Qu.:12.00                                    
    ##  Max.   :12.00                                    
    ##  NA's   :1                                        
    ##  A - 11. I use the eLearning material posted
    ##  Min.   : 4.00                              
    ##  1st Qu.: 7.50                              
    ##  Median :12.00                              
    ##  Mean   :10.68                              
    ##  3rd Qu.:12.00                              
    ##  Max.   :12.00                              
    ##  NA's   :1                                  
    ##  B - 1. Concept 1 of 6: Principles of Business Intelligence and the DataOps Philosophy
    ##  Min.   : 0.000                                                                       
    ##  1st Qu.: 7.500                                                                       
    ##  Median : 7.500                                                                       
    ##  Mean   : 8.835                                                                       
    ##  3rd Qu.:12.000                                                                       
    ##  Max.   :12.000                                                                       
    ##  NA's   :1                                                                            
    ##  B - 2. Concept 3 of 6: Linear Algorithms for Predictive Analytics
    ##  Min.   :1.270                                                    
    ##  1st Qu.:3.000                                                    
    ##  Median :5.118                                                    
    ##  Mean   :5.111                                                    
    ##  3rd Qu.:7.583                                                    
    ##  Max.   :7.583                                                    
    ##  NA's   :1                                                        
    ##  C - 2. Quizzes at the end of each concept
    ##  Min.   : 1.50                            
    ##  1st Qu.: 7.50                            
    ##  Median :12.00                            
    ##  Mean   :10.22                            
    ##  3rd Qu.:12.00                            
    ##  Max.   :12.00                            
    ##  NA's   :1                                
    ##  C - 3. Lab manuals that outline the steps to follow during the labs
    ##  Min.   : 4.0                                                       
    ##  1st Qu.: 7.5                                                       
    ##  Median :12.0                                                       
    ##  Mean   :10.3                                                       
    ##  3rd Qu.:12.0                                                       
    ##  Max.   :12.0                                                       
    ##  NA's   :1                                                          
    ##  C - 4. Required lab work submissions at the end of each lab manual that outline the activity to be done on your own
    ##  Min.   : 4.00                                                                                                      
    ##  1st Qu.: 7.50                                                                                                      
    ##  Median :12.00                                                                                                      
    ##  Mean   :10.04                                                                                                      
    ##  3rd Qu.:12.00                                                                                                      
    ##  Max.   :12.00                                                                                                      
    ##  NA's   :1                                                                                                          
    ##  C - 5. Supplementary videos to watch
    ##  Min.   : 0.000                      
    ##  1st Qu.: 7.500                      
    ##  Median : 7.500                      
    ##  Mean   : 8.665                      
    ##  3rd Qu.:12.000                      
    ##  Max.   :12.000                      
    ##  NA's   :1                           
    ##  C - 6. Supplementary podcasts to listen to
    ##  Min.   : 0.00                             
    ##  1st Qu.: 7.50                             
    ##  Median : 7.50                             
    ##  Mean   : 8.31                             
    ##  3rd Qu.:12.00                             
    ##  Max.   :12.00                             
    ##  NA's   :1                                 
    ##  C - 7. Supplementary content to read C - 8. Lectures slides
    ##  Min.   : 0.000                       Min.   : 1.50         
    ##  1st Qu.: 7.500                       1st Qu.: 7.50         
    ##  Median : 7.500                       Median :12.00         
    ##  Mean   : 8.655                       Mean   :10.34         
    ##  3rd Qu.:12.000                       3rd Qu.:12.00         
    ##  Max.   :12.000                       Max.   :12.00         
    ##  NA's   :1                            NA's   :1             
    ##  C - 9. Lecture notes on some of the lecture slides
    ##  Min.   : 1.50                                     
    ##  1st Qu.: 7.50                                     
    ##  Median :12.00                                     
    ##  Mean   :10.28                                     
    ##  3rd Qu.:12.00                                     
    ##  Max.   :12.00                                     
    ##  NA's   :1                                         
    ##  C - 10. The quality of the lectures given (quality measured by the breadth (the full span of knowledge of a subject) and depth (the extent to which specific topics are focused upon, amplified, and explored) of learning - NOT quality measured by how fun/comical/lively the lectures are)
    ##  Min.   : 1.50                                                                                                                                                                                                                                                                                
    ##  1st Qu.: 7.50                                                                                                                                                                                                                                                                                
    ##  Median :12.00                                                                                                                                                                                                                                                                                
    ##  Mean   :10.02                                                                                                                                                                                                                                                                                
    ##  3rd Qu.:12.00                                                                                                                                                                                                                                                                                
    ##  Max.   :12.00                                                                                                                                                                                                                                                                                
    ##  NA's   :1                                                                                                                                                                                                                                                                                    
    ##  C - 11. The division of theory and practice such that most of the theory is done during the recorded online classes and most of the practice is done during the physical classes
    ##  Min.   : 1.500                                                                                                                                                                  
    ##  1st Qu.: 7.500                                                                                                                                                                  
    ##  Median :12.000                                                                                                                                                                  
    ##  Mean   : 9.815                                                                                                                                                                  
    ##  3rd Qu.:12.000                                                                                                                                                                  
    ##  Max.   :12.000                                                                                                                                                                  
    ##  NA's   :1                                                                                                                                                                       
    ##  C - 12. The recordings of online classes
    ##  Min.   : 1.500                          
    ##  1st Qu.: 7.500                          
    ##  Median :12.000                          
    ##  Mean   : 9.235                          
    ##  3rd Qu.:12.000                          
    ##  Max.   :12.000                          
    ##  NA's   :1                               
    ##  D - 1. Write two things you like about the teaching and learning in this unit so far.
    ##  Length:101                                                                           
    ##  Class :character                                                                     
    ##  Mode  :character                                                                     
    ##                                                                                       
    ##                                                                                       
    ##                                                                                       
    ##                                                                                       
    ##  D - 2. Write at least one recommendation to improve the teaching and learning in this unit (for the remaining weeks in the semester)
    ##  Length:101                                                                                                                          
    ##  Class :character                                                                                                                    
    ##  Mode  :character                                                                                                                    
    ##                                                                                                                                      
    ##                                                                                                                                      
    ##                                                                                                                                      
    ##                                                                                                                                      
    ##  Average Course Evaluation Rating Average Level of Learning Attained Rating
    ##  Min.   : 3.731                   Min.   : 1.438                           
    ##  1st Qu.: 8.628                   1st Qu.: 5.162                           
    ##  Median : 9.831                   Median : 6.805                           
    ##  Mean   : 9.844                   Mean   : 7.332                           
    ##  3rd Qu.:11.550                   3rd Qu.: 8.643                           
    ##  Max.   :12.000                   Max.   :10.676                           
    ##  NA's   :1                        NA's   :1                                
    ##  Average Pedagogical Strategy Effectiveness Rating
    ##  Min.   : 4.562                                   
    ##  1st Qu.: 7.776                                   
    ##  Median : 9.831                                   
    ##  Mean   : 9.447                                   
    ##  3rd Qu.:11.550                                   
    ##  Max.   :12.000                                   
    ##  NA's   :1                                        
    ##  Project: Section 1-4: (20%) x/10 Project: Section 5-11: (50%) x/10
    ##  Min.   : 0.000                   Min.   : 0.000                   
    ##  1st Qu.: 7.400                   1st Qu.: 6.000                   
    ##  Median : 8.500                   Median : 7.800                   
    ##  Mean   : 8.011                   Mean   : 6.582                   
    ##  3rd Qu.: 9.000                   3rd Qu.: 8.300                   
    ##  Max.   :10.000                   Max.   :10.000                   
    ##                                                                    
    ##  Project: Section 12: (30%) x/5 Project: (10%): x/30 x 100 TOTAL
    ##  Min.   :0.000                  Min.   :  0.00                  
    ##  1st Qu.:0.000                  1st Qu.: 56.00                  
    ##  Median :0.000                  Median : 66.40                  
    ##  Mean   :1.015                  Mean   : 62.39                  
    ##  3rd Qu.:1.250                  3rd Qu.: 71.60                  
    ##  Max.   :5.000                  Max.   :100.00                  
    ##  NA's   :1                                                      
    ##  Quiz 1 on Concept 1 (Introduction) x/32 Quiz 3 on Concept 3 (Linear) x/15
    ##  Min.   :1.828                           Min.   :1.654                    
    ##  1st Qu.:3.153                           1st Qu.:4.149                    
    ##  Median :3.631                           Median :5.222                    
    ##  Mean   :3.635                           Mean   :5.414                    
    ##  3rd Qu.:4.069                           3rd Qu.:6.706                    
    ##  Max.   :4.953                           Max.   :8.081                    
    ##                                          NA's   :2                        
    ##  Quiz 4 on Concept 4 (Non-Linear) x/22 Quiz 5 on Concept 5 (Dashboarding) x/10
    ##  Min.   : 3.00                         Min.   : 0.000                         
    ##  1st Qu.:10.91                         1st Qu.: 5.000                         
    ##  Median :13.50                         Median : 6.330                         
    ##  Mean   :13.94                         Mean   : 6.367                         
    ##  3rd Qu.:17.50                         3rd Qu.: 8.000                         
    ##  Max.   :22.00                         Max.   :12.670                         
    ##  NA's   :6                             NA's   :12                             
    ##  Quizzes and  Bonus Marks (7%): x/79 x 100 TOTAL
    ##  Min.   :5.552                                  
    ##  1st Qu.:7.027                                  
    ##  Median :7.777                                  
    ##  Mean   :7.730                                  
    ##  3rd Qu.:8.337                                  
    ##  Max.   :9.745                                  
    ##                                                 
    ##  Lab 1 - 2.c. - (Simple Linear Regression) x/5
    ##  Min.   : 4.00                                
    ##  1st Qu.:12.00                                
    ##  Median :12.00                                
    ##  Mean   :11.57                                
    ##  3rd Qu.:12.00                                
    ##  Max.   :12.00                                
    ##  NA's   :3                                    
    ##  Lab 2 - 2.e. -  (Linear Regression using Gradient Descent) x/5
    ##  Min.   : 1.811                                                
    ##  1st Qu.: 4.461                                                
    ##  Median :11.261                                                
    ##  Mean   : 8.709                                                
    ##  3rd Qu.:12.000                                                
    ##  Max.   :12.000                                                
    ##  NA's   :6                                                     
    ##  Lab 3 - 2.g. - (Logistic Regression using Gradient Descent) x/5
    ##  Min.   : 3.561                                                 
    ##  1st Qu.:11.261                                                 
    ##  Median :11.261                                                 
    ##  Mean   :10.422                                                 
    ##  3rd Qu.:11.261                                                 
    ##  Max.   :12.000                                                 
    ##  NA's   :9                                                      
    ##  Lab 4 - 2.h. - (Linear Discriminant Analysis) x/5
    ##  Min.   : 1.211                                   
    ##  1st Qu.: 7.936                                   
    ##  Median :11.261                                   
    ##  Mean   : 9.690                                   
    ##  3rd Qu.:12.000                                   
    ##  Max.   :12.000                                   
    ##  NA's   :18                                       
    ##  Lab 5 - Chart JS Dashboard Setup x/5 Lab Work (7%) x/25 x 100
    ##  Min.   :0.000                        Min.   : 157.9          
    ##  1st Qu.:0.000                        1st Qu.:2505.8          
    ##  Median :5.000                        Median :3199.5          
    ##  Mean   :3.404                        Mean   :3361.3          
    ##  3rd Qu.:5.000                        3rd Qu.:4723.4          
    ##  Max.   :5.000                        Max.   :4999.5          
    ##                                                               
    ##  CAT 1 (8%): x/38 x 100 CAT 2 (8%): x/100 x 100
    ##  Min.   : 94.29         Min.   :  0.00         
    ##  1st Qu.:215.67         1st Qu.: 51.00         
    ##  Median :271.34         Median : 63.50         
    ##  Mean   :273.13         Mean   : 62.13         
    ##  3rd Qu.:345.84         3rd Qu.: 81.75         
    ##  Max.   :433.40         Max.   :100.00         
    ##  NA's   :4              NA's   :31             
    ##  Attendance Waiver Granted: 1 = Yes, 0 = No Absenteeism Percentage
    ##  Min.   :0.00000                            Min.   : 0.00         
    ##  1st Qu.:0.00000                            1st Qu.: 7.41         
    ##  Median :0.00000                            Median :14.81         
    ##  Mean   :0.04951                            Mean   :15.42         
    ##  3rd Qu.:0.00000                            3rd Qu.:22.22         
    ##  Max.   :1.00000                            Max.   :51.85         
    ##                                                                   
    ##  Coursework TOTAL: x/40 (40%) EXAM: x/60 (60%)
    ##  Min.   : 12.94               Min.   : 5.00   
    ##  1st Qu.: 60.94               1st Qu.:26.00   
    ##  Median : 80.58               Median :34.00   
    ##  Mean   : 82.31               Mean   :33.94   
    ##  3rd Qu.:105.12               3rd Qu.:42.00   
    ##  Max.   :137.85               Max.   :56.00   
    ##                               NA's   :4       
    ##  TOTAL = Coursework TOTAL + EXAM (100%)    GRADE          
    ##  Min.   : 11.21                         Length:101        
    ##  1st Qu.:149.12                         Class :character  
    ##  Median :213.01                         Mode  :character  
    ##  Mean   :209.61                                           
    ##  3rd Qu.:266.44                                           
    ##  Max.   :374.44                                           
    ## 

``` r
StudentPerformanceDataset <- as.data.frame(StudentPerformanceDataset)


# Calculate the skewness after the Box-Cox transform
sapply(student_performance_box_cox_transform[, 7:13],  skewness, type = 2)
```

    ##        read_content_before_lecture          anticipate_test_questions 
    ##                         0.03938034                        -0.09618519 
    ##        answer_rhetorical_questions           find_terms_I_do_not_know 
    ##                        -0.10403885                        -0.22025676 
    ## copy_new_terms_in_reading_notebook       take_quizzes_and_use_results 
    ##                        -0.23989873                        -0.31960114 
    ##          reorganise_course_outline 
    ##                        -0.20205241

``` r
#Plot a histogram to view the skewness after the Box-Cox transform


hist(student_performance_box_cox_transform[, 7],
     main = names(student_performance_box_cox_transform)[7])
```

![](BIProject-Template_files/figure-gfm/Applying%20Box%20Cox%20Data%20Transform-8.png)<!-- -->

``` r
hist(student_performance_box_cox_transform[,8],
     main = names(student_performance_box_cox_transform)[8])
```

![](BIProject-Template_files/figure-gfm/Applying%20Box%20Cox%20Data%20Transform-9.png)<!-- -->

``` r
hist(student_performance_box_cox_transform[,9],
     main = names(student_performance_box_cox_transform)[9])
```

![](BIProject-Template_files/figure-gfm/Applying%20Box%20Cox%20Data%20Transform-10.png)<!-- -->

``` r
hist(student_performance_box_cox_transform[,10],
     main = names(student_performance_box_cox_transform)[10])
```

![](BIProject-Template_files/figure-gfm/Applying%20Box%20Cox%20Data%20Transform-11.png)<!-- -->

``` r
hist(student_performance_box_cox_transform[,11],
     main = names(student_performance_box_cox_transform)[11])
```

![](BIProject-Template_files/figure-gfm/Applying%20Box%20Cox%20Data%20Transform-12.png)<!-- -->

``` r
hist(student_performance_box_cox_transform[,12],
     main = names(student_performance_box_cox_transform)[12])
```

![](BIProject-Template_files/figure-gfm/Applying%20Box%20Cox%20Data%20Transform-13.png)<!-- -->

``` r
hist(student_performance_box_cox_transform[,13],
     main = names(student_performance_box_cox_transform)[13])
```

![](BIProject-Template_files/figure-gfm/Applying%20Box%20Cox%20Data%20Transform-14.png)<!-- -->
\# We also tried applying the Yeo Johnson Power Transform on the Dataset

``` r
### Yeo-Johnson Power Transform on the Boston Housing Dataset ----
# BEFORE
summary(StudentPerformanceDataset)
```

    ##  class_group            gender            YOB       regret_choosing_bi
    ##  Length:101         Min.   :0.0000   Min.   :1998   Min.   :0.0000    
    ##  Class :character   1st Qu.:0.0000   1st Qu.:2000   1st Qu.:0.0000    
    ##  Mode  :character   Median :1.0000   Median :2001   Median :0.0000    
    ##                     Mean   :0.5743   Mean   :2001   Mean   :0.0198    
    ##                     3rd Qu.:1.0000   3rd Qu.:2002   3rd Qu.:0.0000    
    ##                     Max.   :1.0000   Max.   :2003   Max.   :1.0000    
    ##                                                                       
    ##   drop_bi_now       motivator      read_content_before_lecture
    ##  Min.   :0.0000   Min.   :0.0000   Min.   :1.000              
    ##  1st Qu.:0.0000   1st Qu.:1.0000   1st Qu.:2.000              
    ##  Median :0.0000   Median :1.0000   Median :3.000              
    ##  Mean   :0.0198   Mean   :0.7525   Mean   :2.752              
    ##  3rd Qu.:0.0000   3rd Qu.:1.0000   3rd Qu.:3.000              
    ##  Max.   :1.0000   Max.   :1.0000   Max.   :5.000              
    ##                                                               
    ##  anticipate_test_questions answer_rhetorical_questions find_terms_I_do_not_know
    ##  Min.   :1.000             Min.   :1.000               Min.   :1.000           
    ##  1st Qu.:3.000             1st Qu.:3.000               1st Qu.:3.000           
    ##  Median :4.000             Median :4.000               Median :4.000           
    ##  Mean   :3.584             Mean   :3.426               Mean   :3.743           
    ##  3rd Qu.:4.000             3rd Qu.:4.000               3rd Qu.:5.000           
    ##  Max.   :5.000             Max.   :5.000               Max.   :5.000           
    ##                                                                                
    ##  copy_new_terms_in_reading_notebook take_quizzes_and_use_results
    ##  Min.   :1.000                      Min.   :1.000               
    ##  1st Qu.:3.000                      1st Qu.:3.000               
    ##  Median :4.000                      Median :4.000               
    ##  Mean   :3.663                      Mean   :3.941               
    ##  3rd Qu.:4.000                      3rd Qu.:5.000               
    ##  Max.   :5.000                      Max.   :5.000               
    ##                                                                 
    ##  reorganise_course_outline write_down_important_points space_out_revision
    ##  Min.   :1.000             Min.   :1.000               Min.   :1.000     
    ##  1st Qu.:3.000             1st Qu.:3.000               1st Qu.:3.000     
    ##  Median :3.000             Median :4.000               Median :3.000     
    ##  Mean   :3.376             Mean   :3.832               Mean   :3.228     
    ##  3rd Qu.:4.000             3rd Qu.:5.000               3rd Qu.:4.000     
    ##  Max.   :5.000             Max.   :5.000               Max.   :5.000     
    ##                                                                          
    ##  studying_in_study_group schedule_appointments goal_oriented  
    ##  Min.   :1.000           Min.   :1.000         Min.   :0.000  
    ##  1st Qu.:1.000           1st Qu.:1.000         1st Qu.:0.000  
    ##  Median :2.000           Median :2.000         Median :0.000  
    ##  Mean   :2.455           Mean   :1.931         Mean   :0.198  
    ##  3rd Qu.:3.000           3rd Qu.:2.000         3rd Qu.:0.000  
    ##  Max.   :5.000           Max.   :5.000         Max.   :1.000  
    ##                                                               
    ##  spaced_repetition testing_and_active_recall  interleaving    categorizing  
    ##  Min.   :1.000     Min.   :1.000             Min.   :1.000   Min.   :1.000  
    ##  1st Qu.:2.000     1st Qu.:3.000             1st Qu.:2.000   1st Qu.:2.000  
    ##  Median :3.000     Median :3.000             Median :2.000   Median :3.000  
    ##  Mean   :2.554     Mean   :3.059             Mean   :2.257   Mean   :2.713  
    ##  3rd Qu.:3.000     3rd Qu.:4.000             3rd Qu.:3.000   3rd Qu.:3.000  
    ##  Max.   :4.000     Max.   :4.000             Max.   :4.000   Max.   :4.000  
    ##                                                                             
    ##  retrospective_timetable cornell_notes        sq3r          commute    
    ##  Min.   :1.000           Min.   :1.000   Min.   :1.000   Min.   :1.00  
    ##  1st Qu.:2.000           1st Qu.:2.000   1st Qu.:2.000   1st Qu.:2.00  
    ##  Median :2.000           Median :3.000   Median :3.000   Median :3.00  
    ##  Mean   :2.406           Mean   :2.545   Mean   :2.614   Mean   :2.73  
    ##  3rd Qu.:3.000           3rd Qu.:3.000   3rd Qu.:3.000   3rd Qu.:4.00  
    ##  Max.   :4.000           Max.   :4.000   Max.   :4.000   Max.   :4.00  
    ##                                                          NA's   :1     
    ##    study_time   repeats_since_Y1  paid_tuition   free_tuition  extra_curricular
    ##  Min.   :1.00   Min.   : 0.00    Min.   :0.00   Min.   :0.00   Min.   :0.00    
    ##  1st Qu.:1.00   1st Qu.: 0.00    1st Qu.:0.00   1st Qu.:0.00   1st Qu.:0.00    
    ##  Median :2.00   Median : 2.00    Median :0.00   Median :0.00   Median :1.00    
    ##  Mean   :1.75   Mean   : 2.05    Mean   :0.11   Mean   :0.27   Mean   :0.53    
    ##  3rd Qu.:2.00   3rd Qu.: 3.00    3rd Qu.:0.00   3rd Qu.:1.00   3rd Qu.:1.00    
    ##  Max.   :4.00   Max.   :10.00    Max.   :1.00   Max.   :1.00   Max.   :1.00    
    ##  NA's   :1      NA's   :1        NA's   :1      NA's   :1      NA's   :1       
    ##  sports_extra_curricular exercise_per_week    meditate         pray     
    ##  Min.   :0.00            Min.   :0.0       Min.   :0.00   Min.   :0.00  
    ##  1st Qu.:0.00            1st Qu.:1.0       1st Qu.:0.00   1st Qu.:1.00  
    ##  Median :0.00            Median :1.0       Median :1.00   Median :2.00  
    ##  Mean   :0.36            Mean   :1.1       Mean   :0.76   Mean   :2.09  
    ##  3rd Qu.:1.00            3rd Qu.:2.0       3rd Qu.:1.00   3rd Qu.:3.00  
    ##  Max.   :1.00            Max.   :3.0       Max.   :3.00   Max.   :3.00  
    ##  NA's   :1               NA's   :1         NA's   :1      NA's   :1     
    ##     internet        laptop  family_relationships  friendships  
    ##  Min.   :0.00   Min.   :1   Min.   :2.00         Min.   :2.00  
    ##  1st Qu.:1.00   1st Qu.:1   1st Qu.:4.00         1st Qu.:4.00  
    ##  Median :1.00   Median :1   Median :4.00         Median :4.00  
    ##  Mean   :0.87   Mean   :1   Mean   :4.19         Mean   :4.01  
    ##  3rd Qu.:1.00   3rd Qu.:1   3rd Qu.:5.00         3rd Qu.:4.00  
    ##  Max.   :1.00   Max.   :1   Max.   :5.00         Max.   :5.00  
    ##  NA's   :1      NA's   :1   NA's   :1            NA's   :1     
    ##  romantic_relationships spiritual_wellnes financial_wellness     health    
    ##  Min.   :0.00           Min.   :1.00      Min.   :1.00       Min.   :1.00  
    ##  1st Qu.:0.00           1st Qu.:3.00      1st Qu.:2.00       1st Qu.:3.00  
    ##  Median :0.00           Median :4.00      Median :3.00       Median :4.00  
    ##  Mean   :1.37           Mean   :3.65      Mean   :3.03       Mean   :4.04  
    ##  3rd Qu.:3.00           3rd Qu.:4.00      3rd Qu.:4.00       3rd Qu.:5.00  
    ##  Max.   :4.00           Max.   :5.00      Max.   :5.00       Max.   :5.00  
    ##  NA's   :1              NA's   :1         NA's   :1          NA's   :1     
    ##     day_out      night_out    alcohol_or_narcotics     mentor    
    ##  Min.   :0.0   Min.   :0.00   Min.   :0.00         Min.   :0.00  
    ##  1st Qu.:0.0   1st Qu.:0.00   1st Qu.:0.00         1st Qu.:0.00  
    ##  Median :1.0   Median :0.00   Median :0.00         Median :0.00  
    ##  Mean   :0.8   Mean   :0.51   Mean   :0.35         Mean   :0.41  
    ##  3rd Qu.:1.0   3rd Qu.:1.00   3rd Qu.:1.00         3rd Qu.:1.00  
    ##  Max.   :3.0   Max.   :3.00   Max.   :3.00         Max.   :1.00  
    ##  NA's   :1     NA's   :1      NA's   :1            NA's   :1     
    ##  mentor_meetings A - 1. I am enjoying the subject
    ##  Min.   :0.00    Min.   :3.00                    
    ##  1st Qu.:0.00    1st Qu.:4.00                    
    ##  Median :0.00    Median :5.00                    
    ##  Mean   :0.68    Mean   :4.49                    
    ##  3rd Qu.:1.00    3rd Qu.:5.00                    
    ##  Max.   :3.00    Max.   :5.00                    
    ##  NA's   :1       NA's   :1                       
    ##  A - 2. Classes start and end on time
    ##  Min.   :3.00                        
    ##  1st Qu.:4.00                        
    ##  Median :5.00                        
    ##  Mean   :4.68                        
    ##  3rd Qu.:5.00                        
    ##  Max.   :5.00                        
    ##  NA's   :1                           
    ##  A - 3. The learning environment is participative, involves learning by doing and is group-based
    ##  Min.   :3.00                                                                                   
    ##  1st Qu.:4.00                                                                                   
    ##  Median :4.00                                                                                   
    ##  Mean   :4.35                                                                                   
    ##  3rd Qu.:5.00                                                                                   
    ##  Max.   :5.00                                                                                   
    ##  NA's   :1                                                                                      
    ##  A - 4. The subject content is delivered according to the course outline and meets my expectations
    ##  Min.   :3.00                                                                                     
    ##  1st Qu.:4.75                                                                                     
    ##  Median :5.00                                                                                     
    ##  Mean   :4.74                                                                                     
    ##  3rd Qu.:5.00                                                                                     
    ##  Max.   :5.00                                                                                     
    ##  NA's   :1                                                                                        
    ##  A - 5. The topics are clear and logically developed
    ##  Min.   :2.00                                       
    ##  1st Qu.:4.00                                       
    ##  Median :5.00                                       
    ##  Mean   :4.65                                       
    ##  3rd Qu.:5.00                                       
    ##  Max.   :5.00                                       
    ##  NA's   :1                                          
    ##  A - 6. I am developing my oral and writing skills
    ##  Min.   :1.00                                     
    ##  1st Qu.:4.00                                     
    ##  Median :4.00                                     
    ##  Mean   :4.11                                     
    ##  3rd Qu.:5.00                                     
    ##  Max.   :5.00                                     
    ##  NA's   :1                                        
    ##  A - 7. I am developing my reflective and critical reasoning skills
    ##  Min.   :2.00                                                      
    ##  1st Qu.:4.00                                                      
    ##  Median :4.00                                                      
    ##  Mean   :4.38                                                      
    ##  3rd Qu.:5.00                                                      
    ##  Max.   :5.00                                                      
    ##  NA's   :1                                                         
    ##  A - 8. The assessment methods are assisting me to learn
    ##  Min.   :1.00                                           
    ##  1st Qu.:4.00                                           
    ##  Median :5.00                                           
    ##  Mean   :4.61                                           
    ##  3rd Qu.:5.00                                           
    ##  Max.   :5.00                                           
    ##  NA's   :1                                              
    ##  A - 9. I receive relevant feedback
    ##  Min.   :3.00                      
    ##  1st Qu.:4.00                      
    ##  Median :5.00                      
    ##  Mean   :4.58                      
    ##  3rd Qu.:5.00                      
    ##  Max.   :5.00                      
    ##  NA's   :1                         
    ##  A - 10. I read the recommended readings and notes
    ##  Min.   :3.00                                     
    ##  1st Qu.:4.00                                     
    ##  Median :5.00                                     
    ##  Mean   :4.55                                     
    ##  3rd Qu.:5.00                                     
    ##  Max.   :5.00                                     
    ##  NA's   :1                                        
    ##  A - 11. I use the eLearning material posted
    ##  Min.   :3.0                                
    ##  1st Qu.:4.0                                
    ##  Median :5.0                                
    ##  Mean   :4.7                                
    ##  3rd Qu.:5.0                                
    ##  Max.   :5.0                                
    ##  NA's   :1                                  
    ##  B - 1. Concept 1 of 6: Principles of Business Intelligence and the DataOps Philosophy
    ##  Min.   :1.00                                                                         
    ##  1st Qu.:4.00                                                                         
    ##  Median :4.00                                                                         
    ##  Mean   :4.25                                                                         
    ##  3rd Qu.:5.00                                                                         
    ##  Max.   :5.00                                                                         
    ##  NA's   :1                                                                            
    ##  B - 2. Concept 3 of 6: Linear Algorithms for Predictive Analytics
    ##  Min.   :2.00                                                     
    ##  1st Qu.:3.00                                                     
    ##  Median :4.00                                                     
    ##  Mean   :3.94                                                     
    ##  3rd Qu.:5.00                                                     
    ##  Max.   :5.00                                                     
    ##  NA's   :1                                                        
    ##  C - 2. Quizzes at the end of each concept
    ##  Min.   :2.00                             
    ##  1st Qu.:4.00                             
    ##  Median :5.00                             
    ##  Mean   :4.59                             
    ##  3rd Qu.:5.00                             
    ##  Max.   :5.00                             
    ##  NA's   :1                                
    ##  C - 3. Lab manuals that outline the steps to follow during the labs
    ##  Min.   :3.00                                                       
    ##  1st Qu.:4.00                                                       
    ##  Median :5.00                                                       
    ##  Mean   :4.61                                                       
    ##  3rd Qu.:5.00                                                       
    ##  Max.   :5.00                                                       
    ##  NA's   :1                                                          
    ##  C - 4. Required lab work submissions at the end of each lab manual that outline the activity to be done on your own
    ##  Min.   :3.00                                                                                                       
    ##  1st Qu.:4.00                                                                                                       
    ##  Median :5.00                                                                                                       
    ##  Mean   :4.55                                                                                                       
    ##  3rd Qu.:5.00                                                                                                       
    ##  Max.   :5.00                                                                                                       
    ##  NA's   :1                                                                                                          
    ##  C - 5. Supplementary videos to watch
    ##  Min.   :1.00                        
    ##  1st Qu.:4.00                        
    ##  Median :4.00                        
    ##  Mean   :4.19                        
    ##  3rd Qu.:5.00                        
    ##  Max.   :5.00                        
    ##  NA's   :1                           
    ##  C - 6. Supplementary podcasts to listen to
    ##  Min.   :1.00                              
    ##  1st Qu.:4.00                              
    ##  Median :4.00                              
    ##  Mean   :4.08                              
    ##  3rd Qu.:5.00                              
    ##  Max.   :5.00                              
    ##  NA's   :1                                 
    ##  C - 7. Supplementary content to read C - 8. Lectures slides
    ##  Min.   :1.00                         Min.   :2.0           
    ##  1st Qu.:4.00                         1st Qu.:4.0           
    ##  Median :4.00                         Median :5.0           
    ##  Mean   :4.17                         Mean   :4.6           
    ##  3rd Qu.:5.00                         3rd Qu.:5.0           
    ##  Max.   :5.00                         Max.   :5.0           
    ##  NA's   :1                            NA's   :1             
    ##  C - 9. Lecture notes on some of the lecture slides
    ##  Min.   :2.0                                       
    ##  1st Qu.:4.0                                       
    ##  Median :5.0                                       
    ##  Mean   :4.6                                       
    ##  3rd Qu.:5.0                                       
    ##  Max.   :5.0                                       
    ##  NA's   :1                                         
    ##  C - 10. The quality of the lectures given (quality measured by the breadth (the full span of knowledge of a subject) and depth (the extent to which specific topics are focused upon, amplified, and explored) of learning - NOT quality measured by how fun/comical/lively the lectures are)
    ##  Min.   :2.00                                                                                                                                                                                                                                                                                 
    ##  1st Qu.:4.00                                                                                                                                                                                                                                                                                 
    ##  Median :5.00                                                                                                                                                                                                                                                                                 
    ##  Mean   :4.54                                                                                                                                                                                                                                                                                 
    ##  3rd Qu.:5.00                                                                                                                                                                                                                                                                                 
    ##  Max.   :5.00                                                                                                                                                                                                                                                                                 
    ##  NA's   :1                                                                                                                                                                                                                                                                                    
    ##  C - 11. The division of theory and practice such that most of the theory is done during the recorded online classes and most of the practice is done during the physical classes
    ##  Min.   :2.00                                                                                                                                                                    
    ##  1st Qu.:4.00                                                                                                                                                                    
    ##  Median :5.00                                                                                                                                                                    
    ##  Mean   :4.49                                                                                                                                                                    
    ##  3rd Qu.:5.00                                                                                                                                                                    
    ##  Max.   :5.00                                                                                                                                                                    
    ##  NA's   :1                                                                                                                                                                       
    ##  C - 12. The recordings of online classes
    ##  Min.   :2.00                            
    ##  1st Qu.:4.00                            
    ##  Median :5.00                            
    ##  Mean   :4.33                            
    ##  3rd Qu.:5.00                            
    ##  Max.   :5.00                            
    ##  NA's   :1                               
    ##  D - 1. Write two things you like about the teaching and learning in this unit so far.
    ##  Length:101                                                                           
    ##  Class :character                                                                     
    ##  Mode  :character                                                                     
    ##                                                                                       
    ##                                                                                       
    ##                                                                                       
    ##                                                                                       
    ##  D - 2. Write at least one recommendation to improve the teaching and learning in this unit (for the remaining weeks in the semester)
    ##  Length:101                                                                                                                          
    ##  Class :character                                                                                                                    
    ##  Mode  :character                                                                                                                    
    ##                                                                                                                                      
    ##                                                                                                                                      
    ##                                                                                                                                      
    ##                                                                                                                                      
    ##  Average Course Evaluation Rating Average Level of Learning Attained Rating
    ##  Min.   :2.909                    Min.   :2.000                            
    ##  1st Qu.:4.273                    1st Qu.:3.500                            
    ##  Median :4.545                    Median :4.000                            
    ##  Mean   :4.531                    Mean   :4.095                            
    ##  3rd Qu.:4.909                    3rd Qu.:4.500                            
    ##  Max.   :5.000                    Max.   :5.000                            
    ##  NA's   :1                        NA's   :1                                
    ##  Average Pedagogical Strategy Effectiveness Rating
    ##  Min.   :3.182                                    
    ##  1st Qu.:4.068                                    
    ##  Median :4.545                                    
    ##  Mean   :4.432                                    
    ##  3rd Qu.:4.909                                    
    ##  Max.   :5.000                                    
    ##  NA's   :1                                        
    ##  Project: Section 1-4: (20%) x/10 Project: Section 5-11: (50%) x/10
    ##  Min.   : 0.000                   Min.   : 0.000                   
    ##  1st Qu.: 7.400                   1st Qu.: 6.000                   
    ##  Median : 8.500                   Median : 7.800                   
    ##  Mean   : 8.011                   Mean   : 6.582                   
    ##  3rd Qu.: 9.000                   3rd Qu.: 8.300                   
    ##  Max.   :10.000                   Max.   :10.000                   
    ##                                                                    
    ##  Project: Section 12: (30%) x/5 Project: (10%): x/30 x 100 TOTAL
    ##  Min.   :0.000                  Min.   :  0.00                  
    ##  1st Qu.:0.000                  1st Qu.: 56.00                  
    ##  Median :0.000                  Median : 66.40                  
    ##  Mean   :1.015                  Mean   : 62.39                  
    ##  3rd Qu.:1.250                  3rd Qu.: 71.60                  
    ##  Max.   :5.000                  Max.   :100.00                  
    ##  NA's   :1                                                      
    ##  Quiz 1 on Concept 1 (Introduction) x/32 Quiz 3 on Concept 3 (Linear) x/15
    ##  Min.   : 4.75                           Min.   : 3.00                    
    ##  1st Qu.:11.53                           1st Qu.: 7.00                    
    ##  Median :15.33                           Median : 9.00                    
    ##  Mean   :16.36                           Mean   : 9.53                    
    ##  3rd Qu.:19.63                           3rd Qu.:12.00                    
    ##  Max.   :31.25                           Max.   :15.00                    
    ##                                          NA's   :2                        
    ##  Quiz 4 on Concept 4 (Non-Linear) x/22 Quiz 5 on Concept 5 (Dashboarding) x/10
    ##  Min.   : 3.00                         Min.   : 0.000                         
    ##  1st Qu.:10.91                         1st Qu.: 5.000                         
    ##  Median :13.50                         Median : 6.330                         
    ##  Mean   :13.94                         Mean   : 6.367                         
    ##  3rd Qu.:17.50                         3rd Qu.: 8.000                         
    ##  Max.   :22.00                         Max.   :12.670                         
    ##  NA's   :6                             NA's   :12                             
    ##  Quizzes and  Bonus Marks (7%): x/79 x 100 TOTAL
    ##  Min.   :26.26                                  
    ##  1st Qu.:43.82                                  
    ##  Median :55.31                                  
    ##  Mean   :56.22                                  
    ##  3rd Qu.:65.16                                  
    ##  Max.   :95.25                                  
    ##                                                 
    ##  Lab 1 - 2.c. - (Simple Linear Regression) x/5
    ##  Min.   :3.000                                
    ##  1st Qu.:5.000                                
    ##  Median :5.000                                
    ##  Mean   :4.898                                
    ##  3rd Qu.:5.000                                
    ##  Max.   :5.000                                
    ##  NA's   :3                                    
    ##  Lab 2 - 2.e. -  (Linear Regression using Gradient Descent) x/5
    ##  Min.   :2.150                                                 
    ##  1st Qu.:3.150                                                 
    ##  Median :4.850                                                 
    ##  Mean   :4.166                                                 
    ##  3rd Qu.:5.000                                                 
    ##  Max.   :5.000                                                 
    ##  NA's   :6                                                     
    ##  Lab 3 - 2.g. - (Logistic Regression using Gradient Descent) x/5
    ##  Min.   :2.85                                                   
    ##  1st Qu.:4.85                                                   
    ##  Median :4.85                                                   
    ##  Mean   :4.63                                                   
    ##  3rd Qu.:4.85                                                   
    ##  Max.   :5.00                                                   
    ##  NA's   :9                                                      
    ##  Lab 4 - 2.h. - (Linear Discriminant Analysis) x/5
    ##  Min.   :1.850                                    
    ##  1st Qu.:4.100                                    
    ##  Median :4.850                                    
    ##  Mean   :4.425                                    
    ##  3rd Qu.:5.000                                    
    ##  Max.   :5.000                                    
    ##  NA's   :18                                       
    ##  Lab 5 - Chart JS Dashboard Setup x/5 Lab Work (7%) x/25 x 100
    ##  Min.   :0.000                        Min.   : 17.80          
    ##  1st Qu.:0.000                        1st Qu.: 70.80          
    ##  Median :5.000                        Median : 80.00          
    ##  Mean   :3.404                        Mean   : 79.72          
    ##  3rd Qu.:5.000                        3rd Qu.: 97.20          
    ##  Max.   :5.000                        Max.   :100.00          
    ##                                                               
    ##  CAT 1 (8%): x/38 x 100 CAT 2 (8%): x/100 x 100
    ##  Min.   :32.89          Min.   :  0.00         
    ##  1st Qu.:59.21          1st Qu.: 51.00         
    ##  Median :69.73          Median : 63.50         
    ##  Mean   :69.39          Mean   : 62.13         
    ##  3rd Qu.:82.89          3rd Qu.: 81.75         
    ##  Max.   :97.36          Max.   :100.00         
    ##  NA's   :4              NA's   :31             
    ##  Attendance Waiver Granted: 1 = Yes, 0 = No Absenteeism Percentage
    ##  Min.   :0.00000                            Min.   : 0.00         
    ##  1st Qu.:0.00000                            1st Qu.: 7.41         
    ##  Median :0.00000                            Median :14.81         
    ##  Mean   :0.04951                            Mean   :15.42         
    ##  3rd Qu.:0.00000                            3rd Qu.:22.22         
    ##  Max.   :1.00000                            Max.   :51.85         
    ##                                                                   
    ##  Coursework TOTAL: x/40 (40%) EXAM: x/60 (60%)
    ##  Min.   : 7.47                Min.   : 5.00   
    ##  1st Qu.:20.44                1st Qu.:26.00   
    ##  Median :24.58                Median :34.00   
    ##  Mean   :24.53                Mean   :33.94   
    ##  3rd Qu.:29.31                3rd Qu.:42.00   
    ##  Max.   :35.08                Max.   :56.00   
    ##                               NA's   :4       
    ##  TOTAL = Coursework TOTAL + EXAM (100%)    GRADE          
    ##  Min.   : 7.47                          Length:101        
    ##  1st Qu.:45.54                          Class :character  
    ##  Median :58.69                          Mode  :character  
    ##  Mean   :57.12                                            
    ##  3rd Qu.:68.83                                            
    ##  Max.   :87.72                                            
    ## 

``` r
# Calculate the skewness before the Yeo-Johnson transform
sapply(StudentPerformanceDataset [,7:13],  skewness, type = 2)
```

    ##        read_content_before_lecture          anticipate_test_questions 
    ##                         0.03938034                        -0.70731706 
    ##        answer_rhetorical_questions           find_terms_I_do_not_know 
    ##                        -0.32097933                        -0.81939607 
    ## copy_new_terms_in_reading_notebook       take_quizzes_and_use_results 
    ##                        -0.64953356                        -0.91362634 
    ##          reorganise_course_outline 
    ##                        -0.34506777

``` r
StudentPerformanceDataset <- as.data.frame(StudentPerformanceDataset)  # Convert to data frame if needed
preprocessed_data <- preProcess(StudentPerformanceDataset)

# Plot a histogram to view the skewness before the Box-Cox transform
hist(StudentPerformanceDataset[,7], main = names(StudentPerformanceDataset)[7])
```

![](BIProject-Template_files/figure-gfm/Applying%20Yeo%20Johnson%20Power%20Transform-1.png)<!-- -->

``` r
hist(StudentPerformanceDataset[,8], main = names(StudentPerformanceDataset)[8])
```

![](BIProject-Template_files/figure-gfm/Applying%20Yeo%20Johnson%20Power%20Transform-2.png)<!-- -->

``` r
hist(StudentPerformanceDataset[,9], main = names(StudentPerformanceDataset)[9])
```

![](BIProject-Template_files/figure-gfm/Applying%20Yeo%20Johnson%20Power%20Transform-3.png)<!-- -->

``` r
hist(StudentPerformanceDataset[,10], main = names(StudentPerformanceDataset)[10])
```

![](BIProject-Template_files/figure-gfm/Applying%20Yeo%20Johnson%20Power%20Transform-4.png)<!-- -->

``` r
hist(StudentPerformanceDataset[,11], main = names(StudentPerformanceDataset)[11])
```

![](BIProject-Template_files/figure-gfm/Applying%20Yeo%20Johnson%20Power%20Transform-5.png)<!-- -->

``` r
hist(StudentPerformanceDataset[,12], main = names(StudentPerformanceDataset)[12])
```

![](BIProject-Template_files/figure-gfm/Applying%20Yeo%20Johnson%20Power%20Transform-6.png)<!-- -->

``` r
hist(StudentPerformanceDataset[,13], main = names(StudentPerformanceDataset)[13])
```

![](BIProject-Template_files/figure-gfm/Applying%20Yeo%20Johnson%20Power%20Transform-7.png)<!-- -->

``` r
model_of_the_transform <- preProcess(StudentPerformanceDataset, method = c("YeoJohnson"))
print(model_of_the_transform)
```

    ## Created from 51 samples and 58 variables
    ## 
    ## Pre-processing:
    ##   - ignored (4)
    ##   - Yeo-Johnson transformation (54)
    ## 
    ## Lambda estimates for Yeo-Johnson transformation:
    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ## -2.0257  0.7083  1.2680  1.1256  1.8699  2.9682

``` r
student_performance_yeo_johnson_transform <- predict(model_of_the_transform, # nolint
                                                     StudentPerformanceDataset  )

# AFTER
summary(student_performance_yeo_johnson_transform, is.numeric)
```

    ##  class_group            gender            YOB       regret_choosing_bi
    ##  Length:101         Min.   :0.0000   Min.   :1998   Min.   :0.0000    
    ##  Class :character   1st Qu.:0.0000   1st Qu.:2000   1st Qu.:0.0000    
    ##  Mode  :character   Median :1.0000   Median :2001   Median :0.0000    
    ##                     Mean   :0.5743   Mean   :2001   Mean   :0.0198    
    ##                     3rd Qu.:1.0000   3rd Qu.:2002   3rd Qu.:0.0000    
    ##                     Max.   :1.0000   Max.   :2003   Max.   :1.0000    
    ##                                                                       
    ##   drop_bi_now       motivator      read_content_before_lecture
    ##  Min.   :0.0000   Min.   :0.0000   Min.   :0.9688             
    ##  1st Qu.:0.0000   1st Qu.:1.0000   1st Qu.:1.8967             
    ##  Median :0.0000   Median :1.0000   Median :2.7990             
    ##  Mean   :0.0198   Mean   :0.7525   Mean   :2.5682             
    ##  3rd Qu.:0.0000   3rd Qu.:1.0000   3rd Qu.:2.7990             
    ##  Max.   :1.0000   Max.   :1.0000   Max.   :4.5518             
    ##                                                               
    ##  anticipate_test_questions answer_rhetorical_questions find_terms_I_do_not_know
    ##  Min.   : 1.470            Min.   :1.197               Min.   : 1.559          
    ##  1st Qu.: 7.163            1st Qu.:4.477               1st Qu.: 8.199          
    ##  Median :11.355            Median :6.457               Median :13.357          
    ##  Mean   : 9.938            Mean   :5.396               Mean   :12.597          
    ##  3rd Qu.:11.355            3rd Qu.:6.457               3rd Qu.:19.776          
    ##  Max.   :16.431            Max.   :8.626               Max.   :19.776          
    ##                                                                                
    ##  copy_new_terms_in_reading_notebook take_quizzes_and_use_results
    ##  Min.   : 1.464                     Min.   : 1.851              
    ##  1st Qu.: 7.095                     1st Qu.:12.221              
    ##  Median :11.226                     Median :21.581              
    ##  Mean   :10.265                     Mean   :22.721              
    ##  3rd Qu.:11.226                     3rd Qu.:34.187              
    ##  Max.   :16.217                     Max.   :34.187              
    ##                                                                 
    ##  reorganise_course_outline write_down_important_points space_out_revision
    ##  Min.   :1.177             Min.   : 1.708              Min.   :1.083     
    ##  1st Qu.:4.315             1st Qu.:10.128              1st Qu.:3.575     
    ##  Median :4.315             Median :17.219              Median :3.575     
    ##  Mean   :5.114             Mean   :17.059              Mean   :3.921     
    ##  3rd Qu.:6.178             3rd Qu.:26.424              3rd Qu.:4.932     
    ##  Max.   :8.202             Max.   :26.424              Max.   :6.346     
    ##                                                                          
    ##  studying_in_study_group schedule_appointments goal_oriented  
    ##  Min.   :0.6719          Min.   :0.5085        Min.   :0.000  
    ##  1st Qu.:0.6719          1st Qu.:0.5085        1st Qu.:0.000  
    ##  Median :1.0459          Median :0.6834        Median :0.000  
    ##  Mean   :1.0993          Mean   :0.6372        Mean   :0.198  
    ##  3rd Qu.:1.3030          3rd Qu.:0.6834        3rd Qu.:0.000  
    ##  Max.   :1.6543          Max.   :0.8634        Max.   :1.000  
    ##                                                               
    ##  spaced_repetition testing_and_active_recall  interleaving     categorizing  
    ##  Min.   :1.163     Min.   :1.353             Min.   :0.9012   Min.   :1.273  
    ##  1st Qu.:2.581     1st Qu.:5.920             1st Qu.:1.6817   1st Qu.:3.014  
    ##  Median :4.195     Median :5.920             Median :1.6817   Median :5.151  
    ##  Mean   :3.515     Mean   :6.228             Mean   :1.8532   Mean   :4.599  
    ##  3rd Qu.:4.195     3rd Qu.:9.030             3rd Qu.:2.3928   3rd Qu.:5.151  
    ##  Max.   :5.973     Max.   :9.030             Max.   :3.0565   Max.   :7.640  
    ##                                                                              
    ##  retrospective_timetable cornell_notes        sq3r           commute     
    ##  Min.   :0.9607          Min.   :1.031   Min.   :0.9953   Min.   :1.146  
    ##  1st Qu.:1.8703          1st Qu.:2.104   1st Qu.:1.9842   1st Qu.:2.520  
    ##  Median :1.8703          Median :3.207   Median :2.9689   Median :4.064  
    ##  Mean   :2.2190          Mean   :2.714   Mean   :2.5872   Mean   :3.714  
    ##  3rd Qu.:2.7481          3rd Qu.:3.207   3rd Qu.:2.9689   3rd Qu.:5.751  
    ##  Max.   :3.6031          Max.   :4.331   Max.   :3.9507   Max.   :5.751  
    ##                                                           NA's   :1      
    ##    study_time     repeats_since_Y1  paid_tuition   free_tuition 
    ##  Min.   :0.4900   Min.   :0.0000   Min.   :0.00   Min.   :0.00  
    ##  1st Qu.:0.4900   1st Qu.:0.0000   1st Qu.:0.00   1st Qu.:0.00  
    ##  Median :0.6473   Median :1.0756   Median :0.00   Median :0.00  
    ##  Mean   :0.5906   Mean   :0.8515   Mean   :0.11   Mean   :0.27  
    ##  3rd Qu.:0.6473   3rd Qu.:1.3498   3rd Qu.:0.00   3rd Qu.:1.00  
    ##  Max.   :0.7694   Max.   :2.2900   Max.   :1.00   Max.   :1.00  
    ##  NA's   :1        NA's   :1        NA's   :1      NA's   :1     
    ##  extra_curricular sports_extra_curricular exercise_per_week    meditate     
    ##  Min.   :0.00     Min.   :0.00            Min.   :0.0000    Min.   :0.0000  
    ##  1st Qu.:0.00     1st Qu.:0.00            1st Qu.:0.8204    1st Qu.:0.0000  
    ##  Median :1.00     Median :0.00            Median :0.8204    Median :0.5304  
    ##  Mean   :0.53     Mean   :0.36            Mean   :0.8315    Mean   :0.3115  
    ##  3rd Qu.:1.00     3rd Qu.:1.00            3rd Qu.:1.4411    3rd Qu.:0.5304  
    ##  Max.   :1.00     Max.   :1.00            Max.   :1.9596    Max.   :0.8329  
    ##  NA's   :1        NA's   :1               NA's   :1         NA's   :1       
    ##       pray          internet        laptop  family_relationships
    ##  Min.   :0.000   Min.   :0.00   Min.   :1   Min.   : 7.08       
    ##  1st Qu.:1.344   1st Qu.:1.00   1st Qu.:1   1st Qu.:29.92       
    ##  Median :3.309   Median :1.00   Median :1   Median :29.92       
    ##  Mean   :3.807   Mean   :0.87   Mean   :1   Mean   :35.04       
    ##  3rd Qu.:5.829   3rd Qu.:1.00   3rd Qu.:1   3rd Qu.:49.61       
    ##  Max.   :5.829   Max.   :1.00   Max.   :1   Max.   :49.61       
    ##  NA's   :1       NA's   :1      NA's   :1   NA's   :1           
    ##   friendships     romantic_relationships spiritual_wellnes financial_wellness
    ##  Min.   : 4.188   Min.   :0.0000         Min.   :1.084     Min.   :1.003     
    ##  1st Qu.:12.915   1st Qu.:0.0000         1st Qu.:3.583     1st Qu.:2.011     
    ##  Median :12.915   Median :0.0000         Median :4.945     Median :3.023     
    ##  Mean   :13.280   Mean   :0.4209         Mean   :4.488     Mean   :3.054     
    ##  3rd Qu.:12.915   3rd Qu.:0.9523         3rd Qu.:4.945     3rd Qu.:4.036     
    ##  Max.   :19.030   Max.   :1.0459         Max.   :6.365     Max.   :5.051     
    ##  NA's   :1        NA's   :1              NA's   :1         NA's   :1         
    ##      health          day_out         night_out      alcohol_or_narcotics
    ##  Min.   : 1.921   Min.   :0.0000   Min.   :0.0000   Min.   :0.00        
    ##  1st Qu.:13.332   1st Qu.:0.0000   1st Qu.:0.0000   1st Qu.:0.00        
    ##  Median :23.959   Median :0.8992   Median :0.0000   Median :0.00        
    ##  Mean   :26.177   Mean   :0.7100   Mean   :0.2212   Mean   :0.35        
    ##  3rd Qu.:38.512   3rd Qu.:0.8992   3rd Qu.:0.4757   3rd Qu.:1.00        
    ##  Max.   :38.512   Max.   :2.3812   Max.   :0.6879   Max.   :3.00        
    ##  NA's   :1        NA's   :1        NA's   :1        NA's   :1           
    ##      mentor     mentor_meetings  A - 1. I am enjoying the subject
    ##  Min.   :0.00   Min.   :0.0000   Min.   :3.00                    
    ##  1st Qu.:0.00   1st Qu.:0.0000   1st Qu.:4.00                    
    ##  Median :0.00   Median :0.0000   Median :5.00                    
    ##  Mean   :0.41   Mean   :0.2705   Mean   :4.49                    
    ##  3rd Qu.:1.00   3rd Qu.:0.5045   3rd Qu.:5.00                    
    ##  Max.   :1.00   Max.   :0.7618   Max.   :5.00                    
    ##  NA's   :1      NA's   :1        NA's   :1                       
    ##  A - 2. Classes start and end on time
    ##  Min.   :3.00                        
    ##  1st Qu.:4.00                        
    ##  Median :5.00                        
    ##  Mean   :4.68                        
    ##  3rd Qu.:5.00                        
    ##  Max.   :5.00                        
    ##  NA's   :1                           
    ##  A - 3. The learning environment is participative, involves learning by doing and is group-based
    ##  Min.   :3.00                                                                                   
    ##  1st Qu.:4.00                                                                                   
    ##  Median :4.00                                                                                   
    ##  Mean   :4.35                                                                                   
    ##  3rd Qu.:5.00                                                                                   
    ##  Max.   :5.00                                                                                   
    ##  NA's   :1                                                                                      
    ##  A - 4. The subject content is delivered according to the course outline and meets my expectations
    ##  Min.   :3.00                                                                                     
    ##  1st Qu.:4.75                                                                                     
    ##  Median :5.00                                                                                     
    ##  Mean   :4.74                                                                                     
    ##  3rd Qu.:5.00                                                                                     
    ##  Max.   :5.00                                                                                     
    ##  NA's   :1                                                                                        
    ##  A - 5. The topics are clear and logically developed
    ##  Min.   :2.00                                       
    ##  1st Qu.:4.00                                       
    ##  Median :5.00                                       
    ##  Mean   :4.65                                       
    ##  3rd Qu.:5.00                                       
    ##  Max.   :5.00                                       
    ##  NA's   :1                                          
    ##  A - 6. I am developing my oral and writing skills
    ##  Min.   : 2.30                                    
    ##  1st Qu.:39.67                                    
    ##  Median :39.67                                    
    ##  Mean   :45.72                                    
    ##  3rd Qu.:68.40                                    
    ##  Max.   :68.40                                    
    ##  NA's   :1                                        
    ##  A - 7. I am developing my reflective and critical reasoning skills
    ##  Min.   :2.00                                                      
    ##  1st Qu.:4.00                                                      
    ##  Median :4.00                                                      
    ##  Mean   :4.38                                                      
    ##  3rd Qu.:5.00                                                      
    ##  Max.   :5.00                                                      
    ##  NA's   :1                                                         
    ##  A - 8. The assessment methods are assisting me to learn
    ##  Min.   :1.00                                           
    ##  1st Qu.:4.00                                           
    ##  Median :5.00                                           
    ##  Mean   :4.61                                           
    ##  3rd Qu.:5.00                                           
    ##  Max.   :5.00                                           
    ##  NA's   :1                                              
    ##  A - 9. I receive relevant feedback
    ##  Min.   :3.00                      
    ##  1st Qu.:4.00                      
    ##  Median :5.00                      
    ##  Mean   :4.58                      
    ##  3rd Qu.:5.00                      
    ##  Max.   :5.00                      
    ##  NA's   :1                         
    ##  A - 10. I read the recommended readings and notes
    ##  Min.   :3.00                                     
    ##  1st Qu.:4.00                                     
    ##  Median :5.00                                     
    ##  Mean   :4.55                                     
    ##  3rd Qu.:5.00                                     
    ##  Max.   :5.00                                     
    ##  NA's   :1                                        
    ##  A - 11. I use the eLearning material posted
    ##  Min.   :3.0                                
    ##  1st Qu.:4.0                                
    ##  Median :5.0                                
    ##  Mean   :4.7                                
    ##  3rd Qu.:5.0                                
    ##  Max.   :5.0                                
    ##  NA's   :1                                  
    ##  B - 1. Concept 1 of 6: Principles of Business Intelligence and the DataOps Philosophy
    ##  Min.   :1.00                                                                         
    ##  1st Qu.:4.00                                                                         
    ##  Median :4.00                                                                         
    ##  Mean   :4.25                                                                         
    ##  3rd Qu.:5.00                                                                         
    ##  Max.   :5.00                                                                         
    ##  NA's   :1                                                                            
    ##  B - 2. Concept 3 of 6: Linear Algorithms for Predictive Analytics
    ##  Min.   : 3.476                                                   
    ##  1st Qu.: 6.222                                                   
    ##  Median : 9.588                                                   
    ##  Mean   : 9.588                                                   
    ##  3rd Qu.:13.545                                                   
    ##  Max.   :13.545                                                   
    ##  NA's   :1                                                        
    ##  C - 2. Quizzes at the end of each concept
    ##  Min.   :2.00                             
    ##  1st Qu.:4.00                             
    ##  Median :5.00                             
    ##  Mean   :4.59                             
    ##  3rd Qu.:5.00                             
    ##  Max.   :5.00                             
    ##  NA's   :1                                
    ##  C - 3. Lab manuals that outline the steps to follow during the labs
    ##  Min.   :3.00                                                       
    ##  1st Qu.:4.00                                                       
    ##  Median :5.00                                                       
    ##  Mean   :4.61                                                       
    ##  3rd Qu.:5.00                                                       
    ##  Max.   :5.00                                                       
    ##  NA's   :1                                                          
    ##  C - 4. Required lab work submissions at the end of each lab manual that outline the activity to be done on your own
    ##  Min.   :3.00                                                                                                       
    ##  1st Qu.:4.00                                                                                                       
    ##  Median :5.00                                                                                                       
    ##  Mean   :4.55                                                                                                       
    ##  3rd Qu.:5.00                                                                                                       
    ##  Max.   :5.00                                                                                                       
    ##  NA's   :1                                                                                                          
    ##  C - 5. Supplementary videos to watch
    ##  Min.   :1.00                        
    ##  1st Qu.:4.00                        
    ##  Median :4.00                        
    ##  Mean   :4.19                        
    ##  3rd Qu.:5.00                        
    ##  Max.   :5.00                        
    ##  NA's   :1                           
    ##  C - 6. Supplementary podcasts to listen to
    ##  Min.   : 2.241                            
    ##  1st Qu.:36.899                            
    ##  Median :36.899                            
    ##  Mean   :42.486                            
    ##  3rd Qu.:62.983                            
    ##  Max.   :62.983                            
    ##  NA's   :1                                 
    ##  C - 7. Supplementary content to read C - 8. Lectures slides
    ##  Min.   :1.00                         Min.   :2.0           
    ##  1st Qu.:4.00                         1st Qu.:4.0           
    ##  Median :4.00                         Median :5.0           
    ##  Mean   :4.17                         Mean   :4.6           
    ##  3rd Qu.:5.00                         3rd Qu.:5.0           
    ##  Max.   :5.00                         Max.   :5.0           
    ##  NA's   :1                            NA's   :1             
    ##  C - 9. Lecture notes on some of the lecture slides
    ##  Min.   :2.0                                       
    ##  1st Qu.:4.0                                       
    ##  Median :5.0                                       
    ##  Mean   :4.6                                       
    ##  3rd Qu.:5.0                                       
    ##  Max.   :5.0                                       
    ##  NA's   :1                                         
    ##  C - 10. The quality of the lectures given (quality measured by the breadth (the full span of knowledge of a subject) and depth (the extent to which specific topics are focused upon, amplified, and explored) of learning - NOT quality measured by how fun/comical/lively the lectures are)
    ##  Min.   :2.00                                                                                                                                                                                                                                                                                 
    ##  1st Qu.:4.00                                                                                                                                                                                                                                                                                 
    ##  Median :5.00                                                                                                                                                                                                                                                                                 
    ##  Mean   :4.54                                                                                                                                                                                                                                                                                 
    ##  3rd Qu.:5.00                                                                                                                                                                                                                                                                                 
    ##  Max.   :5.00                                                                                                                                                                                                                                                                                 
    ##  NA's   :1                                                                                                                                                                                                                                                                                    
    ##  C - 11. The division of theory and practice such that most of the theory is done during the recorded online classes and most of the practice is done during the physical classes
    ##  Min.   :2.00                                                                                                                                                                    
    ##  1st Qu.:4.00                                                                                                                                                                    
    ##  Median :5.00                                                                                                                                                                    
    ##  Mean   :4.49                                                                                                                                                                    
    ##  3rd Qu.:5.00                                                                                                                                                                    
    ##  Max.   :5.00                                                                                                                                                                    
    ##  NA's   :1                                                                                                                                                                       
    ##  C - 12. The recordings of online classes
    ##  Min.   :2.00                            
    ##  1st Qu.:4.00                            
    ##  Median :5.00                            
    ##  Mean   :4.33                            
    ##  3rd Qu.:5.00                            
    ##  Max.   :5.00                            
    ##  NA's   :1                               
    ##  D - 1. Write two things you like about the teaching and learning in this unit so far.
    ##  Length:101                                                                           
    ##  Class :character                                                                     
    ##  Mode  :character                                                                     
    ##                                                                                       
    ##                                                                                       
    ##                                                                                       
    ##                                                                                       
    ##  D - 2. Write at least one recommendation to improve the teaching and learning in this unit (for the remaining weeks in the semester)
    ##  Length:101                                                                                                                          
    ##  Class :character                                                                                                                    
    ##  Mode  :character                                                                                                                    
    ##                                                                                                                                      
    ##                                                                                                                                      
    ##                                                                                                                                      
    ##                                                                                                                                      
    ##  Average Course Evaluation Rating Average Level of Learning Attained Rating
    ##  Min.   :2.909                    Min.   : 4.545                           
    ##  1st Qu.:4.273                    1st Qu.:11.616                           
    ##  Median :4.545                    Median :14.722                           
    ##  Mean   :4.531                    Mean   :15.736                           
    ##  3rd Qu.:4.909                    3rd Qu.:18.214                           
    ##  Max.   :5.000                    Max.   :22.098                           
    ##  NA's   :1                        NA's   :1                                
    ##  Average Pedagogical Strategy Effectiveness Rating
    ##  Min.   :3.182                                    
    ##  1st Qu.:4.068                                    
    ##  Median :4.545                                    
    ##  Mean   :4.432                                    
    ##  3rd Qu.:4.909                                    
    ##  Max.   :5.000                                    
    ##  NA's   :1                                        
    ##  Project: Section 1-4: (20%) x/10 Project: Section 5-11: (50%) x/10
    ##  Min.   :  0.0                    Min.   : 0.00                    
    ##  1st Qu.:169.8                    1st Qu.:20.43                    
    ##  Median :243.2                    Median :31.77                    
    ##  Mean   :234.3                    Mean   :26.66                    
    ##  3rd Qu.:282.5                    3rd Qu.:35.33                    
    ##  Max.   :373.1                    Max.   :48.73                    
    ##                                                                    
    ##  Project: Section 12: (30%) x/5 Project: (10%): x/30 x 100 TOTAL
    ##  Min.   :0.0000                 Min.   :  0.0                   
    ##  1st Qu.:0.0000                 1st Qu.:269.9                   
    ##  Median :0.0000                 Median :346.2                   
    ##  Mean   :0.1288                 Mean   :329.0                   
    ##  3rd Qu.:0.3894                 3rd Qu.:386.6                   
    ##  Max.   :0.4806                 Max.   :631.1                   
    ##  NA's   :1                                                      
    ##  Quiz 1 on Concept 1 (Introduction) x/32 Quiz 3 on Concept 3 (Linear) x/15
    ##  Min.   :1.972                           Min.   :2.349                    
    ##  1st Qu.:3.010                           1st Qu.:4.721                    
    ##  Median :3.389                           Median :5.766                    
    ##  Mean   :3.391                           Mean   :5.963                    
    ##  3rd Qu.:3.735                           3rd Qu.:7.224                    
    ##  Max.   :4.426                           Max.   :8.585                    
    ##                                          NA's   :2                        
    ##  Quiz 4 on Concept 4 (Non-Linear) x/22 Quiz 5 on Concept 5 (Dashboarding) x/10
    ##  Min.   : 3.018                        Min.   : 0.000                         
    ##  1st Qu.:11.045                        1st Qu.: 5.672                         
    ##  Median :13.677                        Median : 7.306                         
    ##  Mean   :14.126                        Mean   : 7.395                         
    ##  3rd Qu.:17.755                        3rd Qu.: 9.403                         
    ##  Max.   :22.351                        Max.   :15.477                         
    ##  NA's   :6                             NA's   :12                             
    ##  Quizzes and  Bonus Marks (7%): x/79 x 100 TOTAL
    ##  Min.   : 5.998                                 
    ##  1st Qu.: 7.611                                 
    ##  Median : 8.444                                 
    ##  Mean   : 8.399                                 
    ##  3rd Qu.: 9.072                                 
    ##  Max.   :10.669                                 
    ##                                                 
    ##  Lab 1 - 2.c. - (Simple Linear Regression) x/5
    ##  Min.   :3.000                                
    ##  1st Qu.:5.000                                
    ##  Median :5.000                                
    ##  Mean   :4.898                                
    ##  3rd Qu.:5.000                                
    ##  Max.   :5.000                                
    ##  NA's   :3                                    
    ##  Lab 2 - 2.e. -  (Linear Regression using Gradient Descent) x/5
    ##  Min.   :2.150                                                 
    ##  1st Qu.:3.150                                                 
    ##  Median :4.850                                                 
    ##  Mean   :4.166                                                 
    ##  3rd Qu.:5.000                                                 
    ##  Max.   :5.000                                                 
    ##  NA's   :6                                                     
    ##  Lab 3 - 2.g. - (Logistic Regression using Gradient Descent) x/5
    ##  Min.   :2.85                                                   
    ##  1st Qu.:4.85                                                   
    ##  Median :4.85                                                   
    ##  Mean   :4.63                                                   
    ##  3rd Qu.:4.85                                                   
    ##  Max.   :5.00                                                   
    ##  NA's   :9                                                      
    ##  Lab 4 - 2.h. - (Linear Discriminant Analysis) x/5
    ##  Min.   :1.850                                    
    ##  1st Qu.:4.100                                    
    ##  Median :4.850                                    
    ##  Mean   :4.425                                    
    ##  3rd Qu.:5.000                                    
    ##  Max.   :5.000                                    
    ##  NA's   :18                                       
    ##  Lab 5 - Chart JS Dashboard Setup x/5 Lab Work (7%) x/25 x 100
    ##  Min.   :0.000                        Min.   :  487.6         
    ##  1st Qu.:0.000                        1st Qu.:12326.1         
    ##  Median :7.400                        Median :16481.8         
    ##  Mean   :5.035                        Mean   :17845.7         
    ##  3rd Qu.:7.400                        3rd Qu.:26213.8         
    ##  Max.   :7.400                        Max.   :28051.3         
    ##                                                               
    ##  CAT 1 (8%): x/38 x 100 CAT 2 (8%): x/100 x 100
    ##  Min.   : 89.36         Min.   :  0.00         
    ##  1st Qu.:196.81         1st Qu.: 77.21         
    ##  Median :245.41         Median : 98.84         
    ##  Mean   :246.66         Mean   : 97.83         
    ##  3rd Qu.:310.02         3rd Qu.:131.42         
    ##  Max.   :385.48         Max.   :165.00         
    ##  NA's   :4              NA's   :31             
    ##  Attendance Waiver Granted: 1 = Yes, 0 = No Absenteeism Percentage
    ##  Min.   :0.00000                            Min.   : 0.000        
    ##  1st Qu.:0.00000                            1st Qu.: 4.668        
    ##  Median :0.00000                            Median : 7.867        
    ##  Mean   :0.04951                            Mean   : 7.726        
    ##  3rd Qu.:0.00000                            3rd Qu.:10.580        
    ##  Max.   :1.00000                            Max.   :19.312        
    ##                                                                   
    ##  Coursework TOTAL: x/40 (40%) EXAM: x/60 (60%)
    ##  Min.   : 17.21               Min.   : 5.473  
    ##  1st Qu.: 75.11               1st Qu.:31.465  
    ##  Median : 99.06               Median :41.922  
    ##  Mean   :101.33               Mean   :42.037  
    ##  3rd Qu.:129.18               3rd Qu.:52.569  
    ##  Max.   :169.62               Max.   :71.564  
    ##                               NA's   :4       
    ##  TOTAL = Coursework TOTAL + EXAM (100%)    GRADE          
    ##  Min.   : 14.21                         Length:101        
    ##  1st Qu.:170.57                         Class :character  
    ##  Median :243.94                         Mode  :character  
    ##  Mean   :240.33                                           
    ##  3rd Qu.:305.62                                           
    ##  Max.   :430.99                                           
    ## 

``` r
# Calculate the skewness after the Yeo-Johnson transform
sapply(student_performance_yeo_johnson_transform[,7:13] ,skewness, type = 2)
```

    ##        read_content_before_lecture          anticipate_test_questions 
    ##                        -0.02202912                        -0.08806466 
    ##        answer_rhetorical_questions           find_terms_I_do_not_know 
    ##                        -0.07841231                        -0.14603821 
    ## copy_new_terms_in_reading_notebook       take_quizzes_and_use_results 
    ##                        -0.17895513                        -0.26899345 
    ##          reorganise_course_outline 
    ##                        -0.13223830

``` r
# Plot a histogram to view the skewness after the Box-Cox transform
hist(student_performance_yeo_johnson_transform[,7],
     main = names(student_performance_yeo_johnson_transform)[7])
```

![](BIProject-Template_files/figure-gfm/Applying%20Yeo%20Johnson%20Power%20Transform-8.png)<!-- -->

``` r
hist(student_performance_yeo_johnson_transform[,8],
     main = names(student_performance_yeo_johnson_transform)[8])
```

![](BIProject-Template_files/figure-gfm/Applying%20Yeo%20Johnson%20Power%20Transform-9.png)<!-- -->

``` r
hist(student_performance_yeo_johnson_transform[,9],
     main = names(student_performance_yeo_johnson_transform)[9])
```

![](BIProject-Template_files/figure-gfm/Applying%20Yeo%20Johnson%20Power%20Transform-10.png)<!-- -->

``` r
hist(student_performance_yeo_johnson_transform[,10],
     main = names(student_performance_yeo_johnson_transform)[10])
```

![](BIProject-Template_files/figure-gfm/Applying%20Yeo%20Johnson%20Power%20Transform-11.png)<!-- -->

``` r
hist(student_performance_yeo_johnson_transform[,11],
     main = names(student_performance_yeo_johnson_transform)[11])
```

![](BIProject-Template_files/figure-gfm/Applying%20Yeo%20Johnson%20Power%20Transform-12.png)<!-- -->

``` r
hist(student_performance_yeo_johnson_transform[,12],
     main = names(student_performance_yeo_johnson_transform)[12])
```

![](BIProject-Template_files/figure-gfm/Applying%20Yeo%20Johnson%20Power%20Transform-13.png)<!-- -->

``` r
hist(student_performance_yeo_johnson_transform[,13],
     main = names(student_performance_yeo_johnson_transform)[13])
```

![](BIProject-Template_files/figure-gfm/Applying%20Yeo%20Johnson%20Power%20Transform-14.png)<!-- -->

``` r
### Yeo-Johnson Power Transform on the Student Performance ----
# BEFORE
summary(student_performance_yeo_johnson_transform)
```

    ##  class_group            gender            YOB       regret_choosing_bi
    ##  Length:101         Min.   :0.0000   Min.   :1998   Min.   :0.0000    
    ##  Class :character   1st Qu.:0.0000   1st Qu.:2000   1st Qu.:0.0000    
    ##  Mode  :character   Median :1.0000   Median :2001   Median :0.0000    
    ##                     Mean   :0.5743   Mean   :2001   Mean   :0.0198    
    ##                     3rd Qu.:1.0000   3rd Qu.:2002   3rd Qu.:0.0000    
    ##                     Max.   :1.0000   Max.   :2003   Max.   :1.0000    
    ##                                                                       
    ##   drop_bi_now       motivator      read_content_before_lecture
    ##  Min.   :0.0000   Min.   :0.0000   Min.   :0.9688             
    ##  1st Qu.:0.0000   1st Qu.:1.0000   1st Qu.:1.8967             
    ##  Median :0.0000   Median :1.0000   Median :2.7990             
    ##  Mean   :0.0198   Mean   :0.7525   Mean   :2.5682             
    ##  3rd Qu.:0.0000   3rd Qu.:1.0000   3rd Qu.:2.7990             
    ##  Max.   :1.0000   Max.   :1.0000   Max.   :4.5518             
    ##                                                               
    ##  anticipate_test_questions answer_rhetorical_questions find_terms_I_do_not_know
    ##  Min.   : 1.470            Min.   :1.197               Min.   : 1.559          
    ##  1st Qu.: 7.163            1st Qu.:4.477               1st Qu.: 8.199          
    ##  Median :11.355            Median :6.457               Median :13.357          
    ##  Mean   : 9.938            Mean   :5.396               Mean   :12.597          
    ##  3rd Qu.:11.355            3rd Qu.:6.457               3rd Qu.:19.776          
    ##  Max.   :16.431            Max.   :8.626               Max.   :19.776          
    ##                                                                                
    ##  copy_new_terms_in_reading_notebook take_quizzes_and_use_results
    ##  Min.   : 1.464                     Min.   : 1.851              
    ##  1st Qu.: 7.095                     1st Qu.:12.221              
    ##  Median :11.226                     Median :21.581              
    ##  Mean   :10.265                     Mean   :22.721              
    ##  3rd Qu.:11.226                     3rd Qu.:34.187              
    ##  Max.   :16.217                     Max.   :34.187              
    ##                                                                 
    ##  reorganise_course_outline write_down_important_points space_out_revision
    ##  Min.   :1.177             Min.   : 1.708              Min.   :1.083     
    ##  1st Qu.:4.315             1st Qu.:10.128              1st Qu.:3.575     
    ##  Median :4.315             Median :17.219              Median :3.575     
    ##  Mean   :5.114             Mean   :17.059              Mean   :3.921     
    ##  3rd Qu.:6.178             3rd Qu.:26.424              3rd Qu.:4.932     
    ##  Max.   :8.202             Max.   :26.424              Max.   :6.346     
    ##                                                                          
    ##  studying_in_study_group schedule_appointments goal_oriented  
    ##  Min.   :0.6719          Min.   :0.5085        Min.   :0.000  
    ##  1st Qu.:0.6719          1st Qu.:0.5085        1st Qu.:0.000  
    ##  Median :1.0459          Median :0.6834        Median :0.000  
    ##  Mean   :1.0993          Mean   :0.6372        Mean   :0.198  
    ##  3rd Qu.:1.3030          3rd Qu.:0.6834        3rd Qu.:0.000  
    ##  Max.   :1.6543          Max.   :0.8634        Max.   :1.000  
    ##                                                               
    ##  spaced_repetition testing_and_active_recall  interleaving     categorizing  
    ##  Min.   :1.163     Min.   :1.353             Min.   :0.9012   Min.   :1.273  
    ##  1st Qu.:2.581     1st Qu.:5.920             1st Qu.:1.6817   1st Qu.:3.014  
    ##  Median :4.195     Median :5.920             Median :1.6817   Median :5.151  
    ##  Mean   :3.515     Mean   :6.228             Mean   :1.8532   Mean   :4.599  
    ##  3rd Qu.:4.195     3rd Qu.:9.030             3rd Qu.:2.3928   3rd Qu.:5.151  
    ##  Max.   :5.973     Max.   :9.030             Max.   :3.0565   Max.   :7.640  
    ##                                                                              
    ##  retrospective_timetable cornell_notes        sq3r           commute     
    ##  Min.   :0.9607          Min.   :1.031   Min.   :0.9953   Min.   :1.146  
    ##  1st Qu.:1.8703          1st Qu.:2.104   1st Qu.:1.9842   1st Qu.:2.520  
    ##  Median :1.8703          Median :3.207   Median :2.9689   Median :4.064  
    ##  Mean   :2.2190          Mean   :2.714   Mean   :2.5872   Mean   :3.714  
    ##  3rd Qu.:2.7481          3rd Qu.:3.207   3rd Qu.:2.9689   3rd Qu.:5.751  
    ##  Max.   :3.6031          Max.   :4.331   Max.   :3.9507   Max.   :5.751  
    ##                                                           NA's   :1      
    ##    study_time     repeats_since_Y1  paid_tuition   free_tuition 
    ##  Min.   :0.4900   Min.   :0.0000   Min.   :0.00   Min.   :0.00  
    ##  1st Qu.:0.4900   1st Qu.:0.0000   1st Qu.:0.00   1st Qu.:0.00  
    ##  Median :0.6473   Median :1.0756   Median :0.00   Median :0.00  
    ##  Mean   :0.5906   Mean   :0.8515   Mean   :0.11   Mean   :0.27  
    ##  3rd Qu.:0.6473   3rd Qu.:1.3498   3rd Qu.:0.00   3rd Qu.:1.00  
    ##  Max.   :0.7694   Max.   :2.2900   Max.   :1.00   Max.   :1.00  
    ##  NA's   :1        NA's   :1        NA's   :1      NA's   :1     
    ##  extra_curricular sports_extra_curricular exercise_per_week    meditate     
    ##  Min.   :0.00     Min.   :0.00            Min.   :0.0000    Min.   :0.0000  
    ##  1st Qu.:0.00     1st Qu.:0.00            1st Qu.:0.8204    1st Qu.:0.0000  
    ##  Median :1.00     Median :0.00            Median :0.8204    Median :0.5304  
    ##  Mean   :0.53     Mean   :0.36            Mean   :0.8315    Mean   :0.3115  
    ##  3rd Qu.:1.00     3rd Qu.:1.00            3rd Qu.:1.4411    3rd Qu.:0.5304  
    ##  Max.   :1.00     Max.   :1.00            Max.   :1.9596    Max.   :0.8329  
    ##  NA's   :1        NA's   :1               NA's   :1         NA's   :1       
    ##       pray          internet        laptop  family_relationships
    ##  Min.   :0.000   Min.   :0.00   Min.   :1   Min.   : 7.08       
    ##  1st Qu.:1.344   1st Qu.:1.00   1st Qu.:1   1st Qu.:29.92       
    ##  Median :3.309   Median :1.00   Median :1   Median :29.92       
    ##  Mean   :3.807   Mean   :0.87   Mean   :1   Mean   :35.04       
    ##  3rd Qu.:5.829   3rd Qu.:1.00   3rd Qu.:1   3rd Qu.:49.61       
    ##  Max.   :5.829   Max.   :1.00   Max.   :1   Max.   :49.61       
    ##  NA's   :1       NA's   :1      NA's   :1   NA's   :1           
    ##   friendships     romantic_relationships spiritual_wellnes financial_wellness
    ##  Min.   : 4.188   Min.   :0.0000         Min.   :1.084     Min.   :1.003     
    ##  1st Qu.:12.915   1st Qu.:0.0000         1st Qu.:3.583     1st Qu.:2.011     
    ##  Median :12.915   Median :0.0000         Median :4.945     Median :3.023     
    ##  Mean   :13.280   Mean   :0.4209         Mean   :4.488     Mean   :3.054     
    ##  3rd Qu.:12.915   3rd Qu.:0.9523         3rd Qu.:4.945     3rd Qu.:4.036     
    ##  Max.   :19.030   Max.   :1.0459         Max.   :6.365     Max.   :5.051     
    ##  NA's   :1        NA's   :1              NA's   :1         NA's   :1         
    ##      health          day_out         night_out      alcohol_or_narcotics
    ##  Min.   : 1.921   Min.   :0.0000   Min.   :0.0000   Min.   :0.00        
    ##  1st Qu.:13.332   1st Qu.:0.0000   1st Qu.:0.0000   1st Qu.:0.00        
    ##  Median :23.959   Median :0.8992   Median :0.0000   Median :0.00        
    ##  Mean   :26.177   Mean   :0.7100   Mean   :0.2212   Mean   :0.35        
    ##  3rd Qu.:38.512   3rd Qu.:0.8992   3rd Qu.:0.4757   3rd Qu.:1.00        
    ##  Max.   :38.512   Max.   :2.3812   Max.   :0.6879   Max.   :3.00        
    ##  NA's   :1        NA's   :1        NA's   :1        NA's   :1           
    ##      mentor     mentor_meetings  A - 1. I am enjoying the subject
    ##  Min.   :0.00   Min.   :0.0000   Min.   :3.00                    
    ##  1st Qu.:0.00   1st Qu.:0.0000   1st Qu.:4.00                    
    ##  Median :0.00   Median :0.0000   Median :5.00                    
    ##  Mean   :0.41   Mean   :0.2705   Mean   :4.49                    
    ##  3rd Qu.:1.00   3rd Qu.:0.5045   3rd Qu.:5.00                    
    ##  Max.   :1.00   Max.   :0.7618   Max.   :5.00                    
    ##  NA's   :1      NA's   :1        NA's   :1                       
    ##  A - 2. Classes start and end on time
    ##  Min.   :3.00                        
    ##  1st Qu.:4.00                        
    ##  Median :5.00                        
    ##  Mean   :4.68                        
    ##  3rd Qu.:5.00                        
    ##  Max.   :5.00                        
    ##  NA's   :1                           
    ##  A - 3. The learning environment is participative, involves learning by doing and is group-based
    ##  Min.   :3.00                                                                                   
    ##  1st Qu.:4.00                                                                                   
    ##  Median :4.00                                                                                   
    ##  Mean   :4.35                                                                                   
    ##  3rd Qu.:5.00                                                                                   
    ##  Max.   :5.00                                                                                   
    ##  NA's   :1                                                                                      
    ##  A - 4. The subject content is delivered according to the course outline and meets my expectations
    ##  Min.   :3.00                                                                                     
    ##  1st Qu.:4.75                                                                                     
    ##  Median :5.00                                                                                     
    ##  Mean   :4.74                                                                                     
    ##  3rd Qu.:5.00                                                                                     
    ##  Max.   :5.00                                                                                     
    ##  NA's   :1                                                                                        
    ##  A - 5. The topics are clear and logically developed
    ##  Min.   :2.00                                       
    ##  1st Qu.:4.00                                       
    ##  Median :5.00                                       
    ##  Mean   :4.65                                       
    ##  3rd Qu.:5.00                                       
    ##  Max.   :5.00                                       
    ##  NA's   :1                                          
    ##  A - 6. I am developing my oral and writing skills
    ##  Min.   : 2.30                                    
    ##  1st Qu.:39.67                                    
    ##  Median :39.67                                    
    ##  Mean   :45.72                                    
    ##  3rd Qu.:68.40                                    
    ##  Max.   :68.40                                    
    ##  NA's   :1                                        
    ##  A - 7. I am developing my reflective and critical reasoning skills
    ##  Min.   :2.00                                                      
    ##  1st Qu.:4.00                                                      
    ##  Median :4.00                                                      
    ##  Mean   :4.38                                                      
    ##  3rd Qu.:5.00                                                      
    ##  Max.   :5.00                                                      
    ##  NA's   :1                                                         
    ##  A - 8. The assessment methods are assisting me to learn
    ##  Min.   :1.00                                           
    ##  1st Qu.:4.00                                           
    ##  Median :5.00                                           
    ##  Mean   :4.61                                           
    ##  3rd Qu.:5.00                                           
    ##  Max.   :5.00                                           
    ##  NA's   :1                                              
    ##  A - 9. I receive relevant feedback
    ##  Min.   :3.00                      
    ##  1st Qu.:4.00                      
    ##  Median :5.00                      
    ##  Mean   :4.58                      
    ##  3rd Qu.:5.00                      
    ##  Max.   :5.00                      
    ##  NA's   :1                         
    ##  A - 10. I read the recommended readings and notes
    ##  Min.   :3.00                                     
    ##  1st Qu.:4.00                                     
    ##  Median :5.00                                     
    ##  Mean   :4.55                                     
    ##  3rd Qu.:5.00                                     
    ##  Max.   :5.00                                     
    ##  NA's   :1                                        
    ##  A - 11. I use the eLearning material posted
    ##  Min.   :3.0                                
    ##  1st Qu.:4.0                                
    ##  Median :5.0                                
    ##  Mean   :4.7                                
    ##  3rd Qu.:5.0                                
    ##  Max.   :5.0                                
    ##  NA's   :1                                  
    ##  B - 1. Concept 1 of 6: Principles of Business Intelligence and the DataOps Philosophy
    ##  Min.   :1.00                                                                         
    ##  1st Qu.:4.00                                                                         
    ##  Median :4.00                                                                         
    ##  Mean   :4.25                                                                         
    ##  3rd Qu.:5.00                                                                         
    ##  Max.   :5.00                                                                         
    ##  NA's   :1                                                                            
    ##  B - 2. Concept 3 of 6: Linear Algorithms for Predictive Analytics
    ##  Min.   : 3.476                                                   
    ##  1st Qu.: 6.222                                                   
    ##  Median : 9.588                                                   
    ##  Mean   : 9.588                                                   
    ##  3rd Qu.:13.545                                                   
    ##  Max.   :13.545                                                   
    ##  NA's   :1                                                        
    ##  C - 2. Quizzes at the end of each concept
    ##  Min.   :2.00                             
    ##  1st Qu.:4.00                             
    ##  Median :5.00                             
    ##  Mean   :4.59                             
    ##  3rd Qu.:5.00                             
    ##  Max.   :5.00                             
    ##  NA's   :1                                
    ##  C - 3. Lab manuals that outline the steps to follow during the labs
    ##  Min.   :3.00                                                       
    ##  1st Qu.:4.00                                                       
    ##  Median :5.00                                                       
    ##  Mean   :4.61                                                       
    ##  3rd Qu.:5.00                                                       
    ##  Max.   :5.00                                                       
    ##  NA's   :1                                                          
    ##  C - 4. Required lab work submissions at the end of each lab manual that outline the activity to be done on your own
    ##  Min.   :3.00                                                                                                       
    ##  1st Qu.:4.00                                                                                                       
    ##  Median :5.00                                                                                                       
    ##  Mean   :4.55                                                                                                       
    ##  3rd Qu.:5.00                                                                                                       
    ##  Max.   :5.00                                                                                                       
    ##  NA's   :1                                                                                                          
    ##  C - 5. Supplementary videos to watch
    ##  Min.   :1.00                        
    ##  1st Qu.:4.00                        
    ##  Median :4.00                        
    ##  Mean   :4.19                        
    ##  3rd Qu.:5.00                        
    ##  Max.   :5.00                        
    ##  NA's   :1                           
    ##  C - 6. Supplementary podcasts to listen to
    ##  Min.   : 2.241                            
    ##  1st Qu.:36.899                            
    ##  Median :36.899                            
    ##  Mean   :42.486                            
    ##  3rd Qu.:62.983                            
    ##  Max.   :62.983                            
    ##  NA's   :1                                 
    ##  C - 7. Supplementary content to read C - 8. Lectures slides
    ##  Min.   :1.00                         Min.   :2.0           
    ##  1st Qu.:4.00                         1st Qu.:4.0           
    ##  Median :4.00                         Median :5.0           
    ##  Mean   :4.17                         Mean   :4.6           
    ##  3rd Qu.:5.00                         3rd Qu.:5.0           
    ##  Max.   :5.00                         Max.   :5.0           
    ##  NA's   :1                            NA's   :1             
    ##  C - 9. Lecture notes on some of the lecture slides
    ##  Min.   :2.0                                       
    ##  1st Qu.:4.0                                       
    ##  Median :5.0                                       
    ##  Mean   :4.6                                       
    ##  3rd Qu.:5.0                                       
    ##  Max.   :5.0                                       
    ##  NA's   :1                                         
    ##  C - 10. The quality of the lectures given (quality measured by the breadth (the full span of knowledge of a subject) and depth (the extent to which specific topics are focused upon, amplified, and explored) of learning - NOT quality measured by how fun/comical/lively the lectures are)
    ##  Min.   :2.00                                                                                                                                                                                                                                                                                 
    ##  1st Qu.:4.00                                                                                                                                                                                                                                                                                 
    ##  Median :5.00                                                                                                                                                                                                                                                                                 
    ##  Mean   :4.54                                                                                                                                                                                                                                                                                 
    ##  3rd Qu.:5.00                                                                                                                                                                                                                                                                                 
    ##  Max.   :5.00                                                                                                                                                                                                                                                                                 
    ##  NA's   :1                                                                                                                                                                                                                                                                                    
    ##  C - 11. The division of theory and practice such that most of the theory is done during the recorded online classes and most of the practice is done during the physical classes
    ##  Min.   :2.00                                                                                                                                                                    
    ##  1st Qu.:4.00                                                                                                                                                                    
    ##  Median :5.00                                                                                                                                                                    
    ##  Mean   :4.49                                                                                                                                                                    
    ##  3rd Qu.:5.00                                                                                                                                                                    
    ##  Max.   :5.00                                                                                                                                                                    
    ##  NA's   :1                                                                                                                                                                       
    ##  C - 12. The recordings of online classes
    ##  Min.   :2.00                            
    ##  1st Qu.:4.00                            
    ##  Median :5.00                            
    ##  Mean   :4.33                            
    ##  3rd Qu.:5.00                            
    ##  Max.   :5.00                            
    ##  NA's   :1                               
    ##  D - 1. Write two things you like about the teaching and learning in this unit so far.
    ##  Length:101                                                                           
    ##  Class :character                                                                     
    ##  Mode  :character                                                                     
    ##                                                                                       
    ##                                                                                       
    ##                                                                                       
    ##                                                                                       
    ##  D - 2. Write at least one recommendation to improve the teaching and learning in this unit (for the remaining weeks in the semester)
    ##  Length:101                                                                                                                          
    ##  Class :character                                                                                                                    
    ##  Mode  :character                                                                                                                    
    ##                                                                                                                                      
    ##                                                                                                                                      
    ##                                                                                                                                      
    ##                                                                                                                                      
    ##  Average Course Evaluation Rating Average Level of Learning Attained Rating
    ##  Min.   :2.909                    Min.   : 4.545                           
    ##  1st Qu.:4.273                    1st Qu.:11.616                           
    ##  Median :4.545                    Median :14.722                           
    ##  Mean   :4.531                    Mean   :15.736                           
    ##  3rd Qu.:4.909                    3rd Qu.:18.214                           
    ##  Max.   :5.000                    Max.   :22.098                           
    ##  NA's   :1                        NA's   :1                                
    ##  Average Pedagogical Strategy Effectiveness Rating
    ##  Min.   :3.182                                    
    ##  1st Qu.:4.068                                    
    ##  Median :4.545                                    
    ##  Mean   :4.432                                    
    ##  3rd Qu.:4.909                                    
    ##  Max.   :5.000                                    
    ##  NA's   :1                                        
    ##  Project: Section 1-4: (20%) x/10 Project: Section 5-11: (50%) x/10
    ##  Min.   :  0.0                    Min.   : 0.00                    
    ##  1st Qu.:169.8                    1st Qu.:20.43                    
    ##  Median :243.2                    Median :31.77                    
    ##  Mean   :234.3                    Mean   :26.66                    
    ##  3rd Qu.:282.5                    3rd Qu.:35.33                    
    ##  Max.   :373.1                    Max.   :48.73                    
    ##                                                                    
    ##  Project: Section 12: (30%) x/5 Project: (10%): x/30 x 100 TOTAL
    ##  Min.   :0.0000                 Min.   :  0.0                   
    ##  1st Qu.:0.0000                 1st Qu.:269.9                   
    ##  Median :0.0000                 Median :346.2                   
    ##  Mean   :0.1288                 Mean   :329.0                   
    ##  3rd Qu.:0.3894                 3rd Qu.:386.6                   
    ##  Max.   :0.4806                 Max.   :631.1                   
    ##  NA's   :1                                                      
    ##  Quiz 1 on Concept 1 (Introduction) x/32 Quiz 3 on Concept 3 (Linear) x/15
    ##  Min.   :1.972                           Min.   :2.349                    
    ##  1st Qu.:3.010                           1st Qu.:4.721                    
    ##  Median :3.389                           Median :5.766                    
    ##  Mean   :3.391                           Mean   :5.963                    
    ##  3rd Qu.:3.735                           3rd Qu.:7.224                    
    ##  Max.   :4.426                           Max.   :8.585                    
    ##                                          NA's   :2                        
    ##  Quiz 4 on Concept 4 (Non-Linear) x/22 Quiz 5 on Concept 5 (Dashboarding) x/10
    ##  Min.   : 3.018                        Min.   : 0.000                         
    ##  1st Qu.:11.045                        1st Qu.: 5.672                         
    ##  Median :13.677                        Median : 7.306                         
    ##  Mean   :14.126                        Mean   : 7.395                         
    ##  3rd Qu.:17.755                        3rd Qu.: 9.403                         
    ##  Max.   :22.351                        Max.   :15.477                         
    ##  NA's   :6                             NA's   :12                             
    ##  Quizzes and  Bonus Marks (7%): x/79 x 100 TOTAL
    ##  Min.   : 5.998                                 
    ##  1st Qu.: 7.611                                 
    ##  Median : 8.444                                 
    ##  Mean   : 8.399                                 
    ##  3rd Qu.: 9.072                                 
    ##  Max.   :10.669                                 
    ##                                                 
    ##  Lab 1 - 2.c. - (Simple Linear Regression) x/5
    ##  Min.   :3.000                                
    ##  1st Qu.:5.000                                
    ##  Median :5.000                                
    ##  Mean   :4.898                                
    ##  3rd Qu.:5.000                                
    ##  Max.   :5.000                                
    ##  NA's   :3                                    
    ##  Lab 2 - 2.e. -  (Linear Regression using Gradient Descent) x/5
    ##  Min.   :2.150                                                 
    ##  1st Qu.:3.150                                                 
    ##  Median :4.850                                                 
    ##  Mean   :4.166                                                 
    ##  3rd Qu.:5.000                                                 
    ##  Max.   :5.000                                                 
    ##  NA's   :6                                                     
    ##  Lab 3 - 2.g. - (Logistic Regression using Gradient Descent) x/5
    ##  Min.   :2.85                                                   
    ##  1st Qu.:4.85                                                   
    ##  Median :4.85                                                   
    ##  Mean   :4.63                                                   
    ##  3rd Qu.:4.85                                                   
    ##  Max.   :5.00                                                   
    ##  NA's   :9                                                      
    ##  Lab 4 - 2.h. - (Linear Discriminant Analysis) x/5
    ##  Min.   :1.850                                    
    ##  1st Qu.:4.100                                    
    ##  Median :4.850                                    
    ##  Mean   :4.425                                    
    ##  3rd Qu.:5.000                                    
    ##  Max.   :5.000                                    
    ##  NA's   :18                                       
    ##  Lab 5 - Chart JS Dashboard Setup x/5 Lab Work (7%) x/25 x 100
    ##  Min.   :0.000                        Min.   :  487.6         
    ##  1st Qu.:0.000                        1st Qu.:12326.1         
    ##  Median :7.400                        Median :16481.8         
    ##  Mean   :5.035                        Mean   :17845.7         
    ##  3rd Qu.:7.400                        3rd Qu.:26213.8         
    ##  Max.   :7.400                        Max.   :28051.3         
    ##                                                               
    ##  CAT 1 (8%): x/38 x 100 CAT 2 (8%): x/100 x 100
    ##  Min.   : 89.36         Min.   :  0.00         
    ##  1st Qu.:196.81         1st Qu.: 77.21         
    ##  Median :245.41         Median : 98.84         
    ##  Mean   :246.66         Mean   : 97.83         
    ##  3rd Qu.:310.02         3rd Qu.:131.42         
    ##  Max.   :385.48         Max.   :165.00         
    ##  NA's   :4              NA's   :31             
    ##  Attendance Waiver Granted: 1 = Yes, 0 = No Absenteeism Percentage
    ##  Min.   :0.00000                            Min.   : 0.000        
    ##  1st Qu.:0.00000                            1st Qu.: 4.668        
    ##  Median :0.00000                            Median : 7.867        
    ##  Mean   :0.04951                            Mean   : 7.726        
    ##  3rd Qu.:0.00000                            3rd Qu.:10.580        
    ##  Max.   :1.00000                            Max.   :19.312        
    ##                                                                   
    ##  Coursework TOTAL: x/40 (40%) EXAM: x/60 (60%)
    ##  Min.   : 17.21               Min.   : 5.473  
    ##  1st Qu.: 75.11               1st Qu.:31.465  
    ##  Median : 99.06               Median :41.922  
    ##  Mean   :101.33               Mean   :42.037  
    ##  3rd Qu.:129.18               3rd Qu.:52.569  
    ##  Max.   :169.62               Max.   :71.564  
    ##                               NA's   :4       
    ##  TOTAL = Coursework TOTAL + EXAM (100%)    GRADE          
    ##  Min.   : 14.21                         Length:101        
    ##  1st Qu.:170.57                         Class :character  
    ##  Median :243.94                         Mode  :character  
    ##  Mean   :240.33                                           
    ##  3rd Qu.:305.62                                           
    ##  Max.   :430.99                                           
    ## 

``` r
# Calculate the skewness before the Yeo-Johnson transform
sapply(student_performance_yeo_johnson_transform[,7:13],  skewness, type = 2)
```

    ##        read_content_before_lecture          anticipate_test_questions 
    ##                        -0.02202912                        -0.08806466 
    ##        answer_rhetorical_questions           find_terms_I_do_not_know 
    ##                        -0.07841231                        -0.14603821 
    ## copy_new_terms_in_reading_notebook       take_quizzes_and_use_results 
    ##                        -0.17895513                        -0.26899345 
    ##          reorganise_course_outline 
    ##                        -0.13223830

``` r
sapply(student_performance_yeo_johnson_transform[,7:13], sd)
```

    ##        read_content_before_lecture          anticipate_test_questions 
    ##                          0.8662634                          3.9741298 
    ##        answer_rhetorical_questions           find_terms_I_do_not_know 
    ##                          1.9144278                          5.3019548 
    ## copy_new_terms_in_reading_notebook       take_quizzes_and_use_results 
    ##                          4.4288683                         10.3154487 
    ##          reorganise_course_outline 
    ##                          2.0796060

``` r
model_of_the_transform <- preProcess(student_performance_yeo_johnson_transform,
                                     method = c("YeoJohnson"))
print(model_of_the_transform)
```

    ## Created from 51 samples and 57 variables
    ## 
    ## Pre-processing:
    ##   - ignored (4)
    ##   - Yeo-Johnson transformation (53)
    ## 
    ## Lambda estimates for Yeo-Johnson transformation:
    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ## -1.6603  0.9926  1.0025  0.7521  1.0102  1.1188

``` r
student_performance_yeo_johnson_transform <- predict(model_of_the_transform, # nolint
                                                     student_performance_yeo_johnson_transform)

# AFTER
summary(student_performance_yeo_johnson_transform)
```

    ##  class_group            gender            YOB       regret_choosing_bi
    ##  Length:101         Min.   :0.0000   Min.   :1998   Min.   :0.0000    
    ##  Class :character   1st Qu.:0.0000   1st Qu.:2000   1st Qu.:0.0000    
    ##  Mode  :character   Median :1.0000   Median :2001   Median :0.0000    
    ##                     Mean   :0.5743   Mean   :2001   Mean   :0.0198    
    ##                     3rd Qu.:1.0000   3rd Qu.:2002   3rd Qu.:0.0000    
    ##                     Max.   :1.0000   Max.   :2003   Max.   :1.0000    
    ##                                                                       
    ##   drop_bi_now       motivator      read_content_before_lecture
    ##  Min.   :0.0000   Min.   :0.0000   Min.   :0.9683             
    ##  1st Qu.:0.0000   1st Qu.:1.0000   1st Qu.:1.8949             
    ##  Median :0.0000   Median :1.0000   Median :2.7955             
    ##  Mean   :0.0198   Mean   :0.7525   Mean   :2.5650             
    ##  3rd Qu.:0.0000   3rd Qu.:1.0000   3rd Qu.:2.7955             
    ##  Max.   :1.0000   Max.   :1.0000   Max.   :4.5442             
    ##                                                               
    ##  anticipate_test_questions answer_rhetorical_questions find_terms_I_do_not_know
    ##  Min.   : 1.477            Min.   :1.201               Min.   : 1.570          
    ##  1st Qu.: 7.255            1st Qu.:4.512               1st Qu.: 8.354          
    ##  Median :11.537            Median :6.519               Median :13.674          
    ##  Mean   :10.095            Mean   :5.445               Mean   :12.903          
    ##  3rd Qu.:11.537            3rd Qu.:6.519               3rd Qu.:20.329          
    ##  Max.   :16.739            Max.   :8.722               Max.   :20.329          
    ##                                                                                
    ##  copy_new_terms_in_reading_notebook take_quizzes_and_use_results
    ##  Min.   : 1.476                     Min.   : 1.871              
    ##  1st Qu.: 7.253                     1st Qu.:12.606              
    ##  Median :11.538                     Median :22.440              
    ##  Mean   :10.554                     Mean   :23.689              
    ##  3rd Qu.:11.538                     3rd Qu.:35.796              
    ##  Max.   :16.746                     Max.   :35.796              
    ##                                                                 
    ##  reorganise_course_outline write_down_important_points space_out_revision
    ##  Min.   :1.184             Min.   : 1.724              Min.   :1.085     
    ##  1st Qu.:4.371             1st Qu.:10.401              1st Qu.:3.596     
    ##  Median :4.371             Median :17.805              Median :3.596     
    ##  Mean   :5.193             Mean   :17.668              Mean   :3.946     
    ##  3rd Qu.:6.276             3rd Qu.:27.486              3rd Qu.:4.966     
    ##  Max.   :8.353             Max.   :27.486              Max.   :6.396     
    ##                                                                          
    ##  studying_in_study_group schedule_appointments goal_oriented  
    ##  Min.   :0.5946          Min.   :0.3491        Min.   :0.000  
    ##  1st Qu.:0.5946          1st Qu.:0.3491        1st Qu.:0.000  
    ##  Median :0.8786          Median :0.4240        Median :0.000  
    ##  Mean   :0.9077          Mean   :0.4026        Mean   :0.198  
    ##  3rd Qu.:1.0606          3rd Qu.:0.4240        3rd Qu.:0.000  
    ##  Max.   :1.2951          Max.   :0.4877        Max.   :1.000  
    ##                                                               
    ##  spaced_repetition testing_and_active_recall  interleaving     categorizing  
    ##  Min.   :1.168     Min.   :1.357             Min.   :0.8988   Min.   :1.277  
    ##  1st Qu.:2.601     1st Qu.:5.963             1st Qu.:1.6746   1st Qu.:3.029  
    ##  Median :4.240     Median :5.963             Median :1.6746   Median :5.186  
    ##  Mean   :3.551     Mean   :6.276             Mean   :1.8445   Mean   :4.630  
    ##  3rd Qu.:4.240     3rd Qu.:9.111             3rd Qu.:2.3799   3rd Qu.:5.186  
    ##  Max.   :6.050     Max.   :9.111             Max.   :3.0371   Max.   :7.704  
    ##                                                                              
    ##  retrospective_timetable cornell_notes        sq3r           commute     
    ##  Min.   :0.9586          Min.   :1.033   Min.   :0.9949   Min.   :1.157  
    ##  1st Qu.:1.8634          1st Qu.:2.112   1st Qu.:1.9828   1st Qu.:2.560  
    ##  Median :1.8634          Median :3.223   Median :2.9663   Median :4.152  
    ##  Mean   :2.2093          Mean   :2.727   Mean   :2.5849   Mean   :3.797  
    ##  3rd Qu.:2.7351          3rd Qu.:3.223   3rd Qu.:2.9663   3rd Qu.:5.902  
    ##  Max.   :3.5829          Max.   :4.357   Max.   :3.9465   Max.   :5.902  
    ##                                                           NA's   :1      
    ##    study_time     repeats_since_Y1  paid_tuition   free_tuition 
    ##  Min.   :0.3020   Min.   :0.0000   Min.   :0.00   Min.   :0.00  
    ##  1st Qu.:0.3020   1st Qu.:0.0000   1st Qu.:0.00   1st Qu.:0.00  
    ##  Median :0.3541   Median :0.9256   Median :0.00   Median :0.00  
    ##  Mean   :0.3345   Mean   :0.7118   Mean   :0.11   Mean   :0.27  
    ##  3rd Qu.:0.3541   3rd Qu.:1.1293   3rd Qu.:0.00   3rd Qu.:1.00  
    ##  Max.   :0.3867   Max.   :1.7687   Max.   :1.00   Max.   :1.00  
    ##  NA's   :1        NA's   :1        NA's   :1      NA's   :1     
    ##  extra_curricular sports_extra_curricular exercise_per_week    meditate     
    ##  Min.   :0.00     Min.   :0.00            Min.   :0.0000    Min.   :0.0000  
    ##  1st Qu.:0.00     1st Qu.:0.00            1st Qu.:0.8037    1st Qu.:0.0000  
    ##  Median :1.00     Median :0.00            Median :0.8037    Median :0.3827  
    ##  Mean   :0.53     Mean   :0.36            Mean   :0.8089    Mean   :0.2143  
    ##  3rd Qu.:1.00     3rd Qu.:1.00            3rd Qu.:1.3956    3rd Qu.:0.3827  
    ##  Max.   :1.00     Max.   :1.00            Max.   :1.8828    Max.   :0.5215  
    ##  NA's   :1        NA's   :1               NA's   :1         NA's   :1       
    ##       pray          internet        laptop  family_relationships
    ##  Min.   :0.000   Min.   :0.00   Min.   :1   Min.   : 7.149      
    ##  1st Qu.:1.408   1st Qu.:1.00   1st Qu.:1   1st Qu.:30.457      
    ##  Median :3.605   Median :1.00   Median :1   Median :30.457      
    ##  Mean   :4.241   Mean   :0.87   Mean   :1   Mean   :35.720      
    ##  3rd Qu.:6.567   3rd Qu.:1.00   3rd Qu.:1   3rd Qu.:50.660      
    ##  Max.   :6.567   Max.   :1.00   Max.   :1   Max.   :50.660      
    ##  NA's   :1       NA's   :1      NA's   :1   NA's   :1           
    ##   friendships     romantic_relationships spiritual_wellnes financial_wellness
    ##  Min.   : 4.199   Min.   :0.0000         Min.   :1.085     Min.   :1.004     
    ##  1st Qu.:12.976   1st Qu.:0.0000         1st Qu.:3.592     1st Qu.:2.012     
    ##  Median :12.976   Median :0.0000         Median :4.959     Median :3.023     
    ##  Mean   :13.346   Mean   :0.2075         Mean   :4.501     Mean   :3.055     
    ##  3rd Qu.:12.976   3rd Qu.:0.4711         3rd Qu.:4.959     3rd Qu.:4.037     
    ##  Max.   :19.137   Max.   :0.4927         Max.   :6.386     Max.   :5.053     
    ##  NA's   :1        NA's   :1              NA's   :1         NA's   :1         
    ##      health          day_out         night_out      alcohol_or_narcotics
    ##  Min.   : 1.936   Min.   :0.0000   Min.   :0.0000   Min.   :0.00        
    ##  1st Qu.:13.637   1st Qu.:0.0000   1st Qu.:0.0000   1st Qu.:0.00        
    ##  Median :24.652   Median :0.8941   Median :0.0000   Median :0.00        
    ##  Mean   :26.990   Mean   :0.7056   Mean   :0.1311   Mean   :0.35        
    ##  3rd Qu.:39.829   3rd Qu.:0.8941   3rd Qu.:0.2866   3rd Qu.:1.00        
    ##  Max.   :39.829   Max.   :2.3539   Max.   :0.3497   Max.   :3.00        
    ##  NA's   :1        NA's   :1        NA's   :1        NA's   :1           
    ##      mentor     mentor_meetings  A - 1. I am enjoying the subject
    ##  Min.   :0.00   Min.   :0.0000   Min.   :3.00                    
    ##  1st Qu.:0.00   1st Qu.:0.0000   1st Qu.:4.00                    
    ##  Median :0.00   Median :0.0000   Median :5.00                    
    ##  Mean   :0.41   Mean   :0.1648   Mean   :4.49                    
    ##  3rd Qu.:1.00   3rd Qu.:0.3249   3rd Qu.:5.00                    
    ##  Max.   :1.00   Max.   :0.4144   Max.   :5.00                    
    ##  NA's   :1      NA's   :1        NA's   :1                       
    ##  A - 2. Classes start and end on time
    ##  Min.   :3.00                        
    ##  1st Qu.:4.00                        
    ##  Median :5.00                        
    ##  Mean   :4.68                        
    ##  3rd Qu.:5.00                        
    ##  Max.   :5.00                        
    ##  NA's   :1                           
    ##  A - 3. The learning environment is participative, involves learning by doing and is group-based
    ##  Min.   :3.00                                                                                   
    ##  1st Qu.:4.00                                                                                   
    ##  Median :4.00                                                                                   
    ##  Mean   :4.35                                                                                   
    ##  3rd Qu.:5.00                                                                                   
    ##  Max.   :5.00                                                                                   
    ##  NA's   :1                                                                                      
    ##  A - 4. The subject content is delivered according to the course outline and meets my expectations
    ##  Min.   :3.00                                                                                     
    ##  1st Qu.:4.75                                                                                     
    ##  Median :5.00                                                                                     
    ##  Mean   :4.74                                                                                     
    ##  3rd Qu.:5.00                                                                                     
    ##  Max.   :5.00                                                                                     
    ##  NA's   :1                                                                                        
    ##  A - 5. The topics are clear and logically developed
    ##  Min.   :2.00                                       
    ##  1st Qu.:4.00                                       
    ##  Median :5.00                                       
    ##  Mean   :4.65                                       
    ##  3rd Qu.:5.00                                       
    ##  Max.   :5.00                                       
    ##  NA's   :1                                          
    ##  A - 6. I am developing my oral and writing skills
    ##  Min.   : 2.313                                   
    ##  1st Qu.:40.614                                   
    ##  Median :40.614                                   
    ##  Mean   :46.890                                   
    ##  3rd Qu.:70.318                                   
    ##  Max.   :70.318                                   
    ##  NA's   :1                                        
    ##  A - 7. I am developing my reflective and critical reasoning skills
    ##  Min.   :2.00                                                      
    ##  1st Qu.:4.00                                                      
    ##  Median :4.00                                                      
    ##  Mean   :4.38                                                      
    ##  3rd Qu.:5.00                                                      
    ##  Max.   :5.00                                                      
    ##  NA's   :1                                                         
    ##  A - 8. The assessment methods are assisting me to learn
    ##  Min.   :1.00                                           
    ##  1st Qu.:4.00                                           
    ##  Median :5.00                                           
    ##  Mean   :4.61                                           
    ##  3rd Qu.:5.00                                           
    ##  Max.   :5.00                                           
    ##  NA's   :1                                              
    ##  A - 9. I receive relevant feedback
    ##  Min.   :3.00                      
    ##  1st Qu.:4.00                      
    ##  Median :5.00                      
    ##  Mean   :4.58                      
    ##  3rd Qu.:5.00                      
    ##  Max.   :5.00                      
    ##  NA's   :1                         
    ##  A - 10. I read the recommended readings and notes
    ##  Min.   :3.00                                     
    ##  1st Qu.:4.00                                     
    ##  Median :5.00                                     
    ##  Mean   :4.55                                     
    ##  3rd Qu.:5.00                                     
    ##  Max.   :5.00                                     
    ##  NA's   :1                                        
    ##  A - 11. I use the eLearning material posted
    ##  Min.   :3.0                                
    ##  1st Qu.:4.0                                
    ##  Median :5.0                                
    ##  Mean   :4.7                                
    ##  3rd Qu.:5.0                                
    ##  Max.   :5.0                                
    ##  NA's   :1                                  
    ##  B - 1. Concept 1 of 6: Principles of Business Intelligence and the DataOps Philosophy
    ##  Min.   :1.00                                                                         
    ##  1st Qu.:4.00                                                                         
    ##  Median :4.00                                                                         
    ##  Mean   :4.25                                                                         
    ##  3rd Qu.:5.00                                                                         
    ##  Max.   :5.00                                                                         
    ##  NA's   :1                                                                            
    ##  B - 2. Concept 3 of 6: Linear Algorithms for Predictive Analytics
    ##  Min.   : 3.505                                                   
    ##  1st Qu.: 6.295                                                   
    ##  Median : 9.727                                                   
    ##  Mean   : 9.732                                                   
    ##  3rd Qu.:13.775                                                   
    ##  Max.   :13.775                                                   
    ##  NA's   :1                                                        
    ##  C - 2. Quizzes at the end of each concept
    ##  Min.   :2.00                             
    ##  1st Qu.:4.00                             
    ##  Median :5.00                             
    ##  Mean   :4.59                             
    ##  3rd Qu.:5.00                             
    ##  Max.   :5.00                             
    ##  NA's   :1                                
    ##  C - 3. Lab manuals that outline the steps to follow during the labs
    ##  Min.   :3.00                                                       
    ##  1st Qu.:4.00                                                       
    ##  Median :5.00                                                       
    ##  Mean   :4.61                                                       
    ##  3rd Qu.:5.00                                                       
    ##  Max.   :5.00                                                       
    ##  NA's   :1                                                          
    ##  C - 4. Required lab work submissions at the end of each lab manual that outline the activity to be done on your own
    ##  Min.   :3.00                                                                                                       
    ##  1st Qu.:4.00                                                                                                       
    ##  Median :5.00                                                                                                       
    ##  Mean   :4.55                                                                                                       
    ##  3rd Qu.:5.00                                                                                                       
    ##  Max.   :5.00                                                                                                       
    ##  NA's   :1                                                                                                          
    ##  C - 5. Supplementary videos to watch
    ##  Min.   :1.00                        
    ##  1st Qu.:4.00                        
    ##  Median :4.00                        
    ##  Mean   :4.19                        
    ##  3rd Qu.:5.00                        
    ##  Max.   :5.00                        
    ##  NA's   :1                           
    ##  C - 6. Supplementary podcasts to listen to
    ##  Min.   : 2.263                            
    ##  1st Qu.:38.335                            
    ##  Median :38.335                            
    ##  Mean   :44.290                            
    ##  3rd Qu.:65.886                            
    ##  Max.   :65.886                            
    ##  NA's   :1                                 
    ##  C - 7. Supplementary content to read C - 8. Lectures slides
    ##  Min.   :1.00                         Min.   :2.0           
    ##  1st Qu.:4.00                         1st Qu.:4.0           
    ##  Median :4.00                         Median :5.0           
    ##  Mean   :4.17                         Mean   :4.6           
    ##  3rd Qu.:5.00                         3rd Qu.:5.0           
    ##  Max.   :5.00                         Max.   :5.0           
    ##  NA's   :1                            NA's   :1             
    ##  C - 9. Lecture notes on some of the lecture slides
    ##  Min.   :2.0                                       
    ##  1st Qu.:4.0                                       
    ##  Median :5.0                                       
    ##  Mean   :4.6                                       
    ##  3rd Qu.:5.0                                       
    ##  Max.   :5.0                                       
    ##  NA's   :1                                         
    ##  C - 10. The quality of the lectures given (quality measured by the breadth (the full span of knowledge of a subject) and depth (the extent to which specific topics are focused upon, amplified, and explored) of learning - NOT quality measured by how fun/comical/lively the lectures are)
    ##  Min.   :2.00                                                                                                                                                                                                                                                                                 
    ##  1st Qu.:4.00                                                                                                                                                                                                                                                                                 
    ##  Median :5.00                                                                                                                                                                                                                                                                                 
    ##  Mean   :4.54                                                                                                                                                                                                                                                                                 
    ##  3rd Qu.:5.00                                                                                                                                                                                                                                                                                 
    ##  Max.   :5.00                                                                                                                                                                                                                                                                                 
    ##  NA's   :1                                                                                                                                                                                                                                                                                    
    ##  C - 11. The division of theory and practice such that most of the theory is done during the recorded online classes and most of the practice is done during the physical classes
    ##  Min.   :2.00                                                                                                                                                                    
    ##  1st Qu.:4.00                                                                                                                                                                    
    ##  Median :5.00                                                                                                                                                                    
    ##  Mean   :4.49                                                                                                                                                                    
    ##  3rd Qu.:5.00                                                                                                                                                                    
    ##  Max.   :5.00                                                                                                                                                                    
    ##  NA's   :1                                                                                                                                                                       
    ##  C - 12. The recordings of online classes
    ##  Min.   :2.00                            
    ##  1st Qu.:4.00                            
    ##  Median :5.00                            
    ##  Mean   :4.33                            
    ##  3rd Qu.:5.00                            
    ##  Max.   :5.00                            
    ##  NA's   :1                               
    ##  D - 1. Write two things you like about the teaching and learning in this unit so far.
    ##  Length:101                                                                           
    ##  Class :character                                                                     
    ##  Mode  :character                                                                     
    ##                                                                                       
    ##                                                                                       
    ##                                                                                       
    ##                                                                                       
    ##  D - 2. Write at least one recommendation to improve the teaching and learning in this unit (for the remaining weeks in the semester)
    ##  Length:101                                                                                                                          
    ##  Class :character                                                                                                                    
    ##  Mode  :character                                                                                                                    
    ##                                                                                                                                      
    ##                                                                                                                                      
    ##                                                                                                                                      
    ##                                                                                                                                      
    ##  Average Course Evaluation Rating Average Level of Learning Attained Rating
    ##  Min.   :2.909                    Min.   : 4.57                            
    ##  1st Qu.:4.273                    1st Qu.:11.72                            
    ##  Median :4.545                    Median :14.87                            
    ##  Mean   :4.531                    Mean   :15.90                            
    ##  3rd Qu.:4.909                    3rd Qu.:18.41                            
    ##  Max.   :5.000                    Max.   :22.35                            
    ##  NA's   :1                        NA's   :1                                
    ##  Average Pedagogical Strategy Effectiveness Rating
    ##  Min.   :3.182                                    
    ##  1st Qu.:4.068                                    
    ##  Median :4.545                                    
    ##  Mean   :4.432                                    
    ##  3rd Qu.:4.909                                    
    ##  Max.   :5.000                                    
    ##  NA's   :1                                        
    ##  Project: Section 1-4: (20%) x/10 Project: Section 5-11: (50%) x/10
    ##  Min.   :  0.0                    Min.   : 0.00                    
    ##  1st Qu.:218.4                    1st Qu.:23.97                    
    ##  Median :319.5                    Median :38.34                    
    ##  Mean   :309.1                    Mean   :32.21                    
    ##  3rd Qu.:374.5                    3rd Qu.:42.93                    
    ##  Max.   :502.8                    Max.   :60.47                    
    ##                                                                    
    ##  Project: Section 12: (30%) x/5 Project: (10%): x/30 x 100 TOTAL
    ##  Min.   :0.0000                 Min.   :  0.0                   
    ##  1st Qu.:0.0000                 1st Qu.:295.7                   
    ##  Median :0.0000                 Median :381.1                   
    ##  Mean   :0.1288                 Mean   :362.6                   
    ##  3rd Qu.:0.3894                 3rd Qu.:426.5                   
    ##  Max.   :0.4806                 Max.   :703.0                   
    ##  NA's   :1                                                      
    ##  Quiz 1 on Concept 1 (Introduction) x/32 Quiz 3 on Concept 3 (Linear) x/15
    ##  Min.   :1.939                           Min.   :2.337                    
    ##  1st Qu.:2.944                           1st Qu.:4.683                    
    ##  Median :3.308                           Median :5.714                    
    ##  Mean   :3.309                           Mean   :5.907                    
    ##  3rd Qu.:3.640                           3rd Qu.:7.151                    
    ##  Max.   :4.303                           Max.   :8.490                    
    ##                                          NA's   :2                        
    ##  Quiz 4 on Concept 4 (Non-Linear) x/22 Quiz 5 on Concept 5 (Dashboarding) x/10
    ##  Min.   : 3.018                        Min.   : 0.000                         
    ##  1st Qu.:11.046                        1st Qu.: 5.676                         
    ##  Median :13.678                        Median : 7.311                         
    ##  Mean   :14.127                        Mean   : 7.400                         
    ##  3rd Qu.:17.757                        3rd Qu.: 9.411                         
    ##  Max.   :22.354                        Max.   :15.492                         
    ##  NA's   :6                             NA's   :12                             
    ##  Quizzes and  Bonus Marks (7%): x/79 x 100 TOTAL
    ##  Min.   : 5.871                                 
    ##  1st Qu.: 7.429                                 
    ##  Median : 8.232                                 
    ##  Mean   : 8.187                                 
    ##  3rd Qu.: 8.837                                 
    ##  Max.   :10.370                                 
    ##                                                 
    ##  Lab 1 - 2.c. - (Simple Linear Regression) x/5
    ##  Min.   :3.000                                
    ##  1st Qu.:5.000                                
    ##  Median :5.000                                
    ##  Mean   :4.898                                
    ##  3rd Qu.:5.000                                
    ##  Max.   :5.000                                
    ##  NA's   :3                                    
    ##  Lab 2 - 2.e. -  (Linear Regression using Gradient Descent) x/5
    ##  Min.   :2.150                                                 
    ##  1st Qu.:3.150                                                 
    ##  Median :4.850                                                 
    ##  Mean   :4.166                                                 
    ##  3rd Qu.:5.000                                                 
    ##  Max.   :5.000                                                 
    ##  NA's   :6                                                     
    ##  Lab 3 - 2.g. - (Logistic Regression using Gradient Descent) x/5
    ##  Min.   :2.85                                                   
    ##  1st Qu.:4.85                                                   
    ##  Median :4.85                                                   
    ##  Mean   :4.63                                                   
    ##  3rd Qu.:4.85                                                   
    ##  Max.   :5.00                                                   
    ##  NA's   :9                                                      
    ##  Lab 4 - 2.h. - (Linear Discriminant Analysis) x/5
    ##  Min.   :1.850                                    
    ##  1st Qu.:4.100                                    
    ##  Median :4.850                                    
    ##  Mean   :4.425                                    
    ##  3rd Qu.:5.000                                    
    ##  Max.   :5.000                                    
    ##  NA's   :18                                       
    ##  Lab 5 - Chart JS Dashboard Setup x/5 Lab Work (7%) x/25 x 100
    ##  Min.   :0.000                        Min.   :  487.8         
    ##  1st Qu.:0.000                        1st Qu.:12331.9         
    ##  Median :8.775                        Median :16489.9         
    ##  Mean   :5.969                        Mean   :17854.6         
    ##  3rd Qu.:8.775                        3rd Qu.:26227.2         
    ##  Max.   :8.775                        Max.   :28065.8         
    ##                                                               
    ##  CAT 1 (8%): x/38 x 100 CAT 2 (8%): x/100 x 100
    ##  Min.   : 89.42         Min.   :  0.00         
    ##  1st Qu.:196.97         1st Qu.: 79.35         
    ##  Median :245.62         Median :101.77         
    ##  Mean   :246.88         Mean   :100.82         
    ##  3rd Qu.:310.31         3rd Qu.:135.62         
    ##  Max.   :385.84         Max.   :170.58         
    ##  NA's   :4              NA's   :31             
    ##  Attendance Waiver Granted: 1 = Yes, 0 = No Absenteeism Percentage
    ##  Min.   :0.00000                            Min.   : 0.000        
    ##  1st Qu.:0.00000                            1st Qu.: 4.584        
    ##  Median :0.00000                            Median : 7.682        
    ##  Mean   :0.04951                            Mean   : 7.532        
    ##  3rd Qu.:0.00000                            3rd Qu.:10.294        
    ##  Max.   :1.00000                            Max.   :18.642        
    ##                                                                   
    ##  Coursework TOTAL: x/40 (40%) EXAM: x/60 (60%)
    ##  Min.   : 17.24               Min.   : 5.475  
    ##  1st Qu.: 75.29               1st Qu.:31.489  
    ##  Median : 99.32               Median :41.957  
    ##  Mean   :101.60               Mean   :42.073  
    ##  3rd Qu.:129.55               3rd Qu.:52.616  
    ##  Max.   :170.13               Max.   :71.633  
    ##                               NA's   :4       
    ##  TOTAL = Coursework TOTAL + EXAM (100%)    GRADE          
    ##  Min.   : 14.22                         Length:101        
    ##  1st Qu.:170.83                         Class :character  
    ##  Median :244.36                         Mode  :character  
    ##  Mean   :240.74                                           
    ##  3rd Qu.:306.16                                           
    ##  Max.   :431.81                                           
    ## 

``` r
# Calculate the skewness after the Yeo-Johnson transform
sapply(student_performance_yeo_johnson_transform[7:13],  skewness, type = 2)
```

    ##        read_content_before_lecture          anticipate_test_questions 
    ##                        -0.02310650                        -0.07868266 
    ##        answer_rhetorical_questions           find_terms_I_do_not_know 
    ##                        -0.07338346                        -0.13412193 
    ## copy_new_terms_in_reading_notebook       take_quizzes_and_use_results 
    ##                        -0.16660932                        -0.25677395 
    ##          reorganise_course_outline 
    ##                        -0.12429464

``` r
sapply(student_performance_yeo_johnson_transform[7:13], sd)
```

    ##        read_content_before_lecture          anticipate_test_questions 
    ##                           0.864615                           4.058663 
    ##        answer_rhetorical_questions           find_terms_I_do_not_know 
    ##                           1.939664                           5.471590 
    ## copy_new_terms_in_reading_notebook       take_quizzes_and_use_results 
    ##                           4.594626                          10.866952 
    ##          reorganise_course_outline 
    ##                           2.124359
