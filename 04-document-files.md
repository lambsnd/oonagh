
# Introduction

This documents the file structure of folder Data & Documentation, which contains two main folders: Assessments Info and Assessments Data. It also describes the AP-CAT project regarding assignments, system usernames, teachers and classes system IDs.


# Assessments Info/


## Assessments Info R Script


### Inputs

It uses the file  [all\_assignments\_[DATE].csv](#org20d2048) to obtain information about which assessments were given each year by the AP-CAT project and which were given by the teachers participating in the study (as practice assignments). This script will need to be re-run by the end of the data collection in May/2020.

This script sorts assignments by `pilot year` (1 to 5), `creator_role` (*`staff`*, *`teacher`*, *`test`*), [`assessment_type`](#org3bfa743) (*`apcat`*, *`practice`*, *`system-test`*), and provides information on the due date of each AP-CAT assessment, [`assessment_id`](#org23a51e3) associated with each teacher (`creator_id`) and class (`assessment_group_id`) in the study, whether the test was adaptive, whether it was published at the time the data was retrieved from the system. Please use `documentation.pdf` to match teacher and class IDs with their actual names.


### Outputs

-   [assessment-names.csv](#orge469f66)
    
    **WARNING**: this file contains identifiable information.

-   [assessments-info-[DATE].csv](#orgab20b5d)
    
    **WARNING**: this file contains identifiable information.


## -info .csv file


### Description:

This file contains info on assessments administered in the AP-CAT project from 2015-16 (first pilot) to 2018-19 (fourth pilot). It includes information on assignment names, school year it was administered, class and teacher information, and its original due date. This data file may be used to learn which assignments were administered each year, chronological order of the assessments within a year, which assessment IDs belong to a specific assessment, etc. Use of the `tidyverse` R package is recommended. File was created with the script in [Assessments Info/assessments-info.R](#org0908d6a) and using [Assessments Data/Raw/IRT\\<sub>calibration.csv</sub>](#org4c058f1).


### Data columns:

-   <a id="org23a51e3"></a> `assessment_id`: unique number identifying each assessment created in the AP-CAT system, usually corresponding to one assessment created for each class.
-   `assessment_name`: name given to the assessment at the time of administration.
-   `pilot_year`: values 1 through 5, where
    -   1 = 2015-16
    -   2 = 2016-17
    -   3 = 2017-18
    -   4 = 2018-19
    -   5 = 2019-20
-   <a id="org3bfa743"></a> `assessment_type`: 
    -   *`apcat`* if assessment was planned by the AP-CAT staff (assessment may have been created for a staff class and should not be included in the analysis)
    -   *`practice`* if assessment was created by one of the teachers (you may or may not want to include these responses in your analysis)
    -   *`system-test`* if assessment was create by staff with the purpose of testing the system (responses are also test responses and should be excluded from analysis).
-   `creator_id`: ID number of the creator account who added the assessment into the system; assessments are added to a teacher&rsquo;s class by a staff member of the AP-CAT project or by the teacher responsible for that class (in the case of practice assigments).
-   `creator_role`: 
    -   *`teacher`* if creator one of the teachers participating in the study
    -   *`staff`* if creator is involved in the project management
-   `assessment_group_id`: unique number identifying class to which the assessment was administered.
-   `is_published`: status of the assessment at the time the data was retrieved.
    -   If *`True`*, the assessment was published, and therefore it administered to students at least once.
    -   If *`False`*, assessment was not published at the data was retrieved, that is, at that time, the assignment was not visible to any students.
    -   If *`NA`*, the assessment was not published, and it was not administered to any students. This happens, for example, when an assignment is created on a staff&rsquo;s account before being copied into an account of a teacher participating in the study.
-   `due_date`: date (and time) the assessment was due (set by the teacher responsible for the class).


## Assessments Names .csv File

This file is created by the script in [Assessments Info/assessments-info.R](#org0908d6a) and it contains a single column with the names of all the assessments that were planned and administered by the AP-CAT staff, that is, it *does not* include practice assignments created by teachers or system-test type of assessments.

To learn which assignments were administered each year, the chronological order of the assessments within a year, assessment IDs, etc. refer to [Assessments Info/assessments-info.csv](#orgab20b5d).


## Assessments QIDs .csv File


# Assessments Data/


## Raw/


### all\_assignments.csv

This raw file is named all\_assignments\_[DATE].csv. File is generated by the AP-CAT system. It is NOT comma separated. In R, you will need to speficy separator is &ldquo;\t&rdquo;. File contains the following columns:

1.  `assessment_group_id`: unique number identifying class to which the assessment was administered.
2.  `assessment_group_name`: name of the class taking the assessment, either chosen by the teacher or the AP-CAT team. **May not be unique**, that is, for different pilot years of the study, there may exist classes that were given the same name. For example, &ldquo;Period 1&rdquo;.
3.  `creator_id`: ID number of the creator account who added the assessment into the system; assessments are added to a teacher&rsquo;s class by a staff member of the AP-CAT project or by the teacher responsible for that class (in the case of practice assigments).
4.  `due_date`: date (and time) the assessment was due (set by the teacher responsible for the class).
5.  `is_adaptive`: whether the assessment was adaptive. If *`True`*, after the first 3 items, the next item was chosen based on the test-taker&rsquo;s performance up until this point.
6.  `is_published`: status of the assessment at the time the data was retrieved.
    -   If *`True`*, the assessment was published, and therefore it administered to students at least once.
    -   If *`False`*, assessment was not published at the data was retrieved, that is, at that time, the assignment was not visible to any students.
    -   If *`NA`*, the assessment was not published, and it was not administered to any students. This happens, for example, when an assignment is created on a staff&rsquo;s account before being copied into an account of a teacher participating in the study.
7.  `name`: name given to the assessment at the time of administration.


### IRT\_calibration.csv

1.  Description:

    *The name of this file is very misleading. It does NOT contain any type of item parameter calibration (that is, estimates of item difficulty). Instead, it contains the information you would use to obtain item parameters, i.e., the item responses.*
    
    This is a long-format data file of item responses, blank-field answers, answer choices, and item-level response times. This data set contains one observation per row; each row corresponds to an answer given by a student to a question while taking a specific assignment. The same student might have answered the same question more than once (on assignments given at different times).

2.  Data columns:

    1.  `user_id`: number that identifies each student account in the AP-CAT system. Student accounts might belong to high school students participating in the study, or they might belong to teachers or staff members that have created student &ldquo;test accounts&rdquo;.
    2.  `Qid`: unique identifier for each question in the AP-CAT system. Renamed `qid` in other files.
    3.  `assignment_name`: name given to the assessment in the AP-CAT system at the time of administration (see details in `documentation.pdf`)
    4.  `assessment_group_name`: name of the class taking the assessment, either chosen by the teacher or the AP-CAT team. **May not be unique**, that is, for different pilot years of the study, there may exist classes that were given the same name. For example, &ldquo;Period 1&rdquo;.
    5.  `teacher_id`: ID number of the teacher (creator) account who added the assessment into the system. Assessments may be added to a teacher&rsquo;s class by a staff member of the AP-CAT project or by the teacher responsible for that class (in the case of practice assigments).
    6.  `is_correct`: logical type of data indicating whether the item was answered correctly (&ldquo;TRUE&rdquo;) or incorrectly (&ldquo;FALSE&rdquo;), or `NA` if not shown to the student (if the question was given to student, but they *skipped* it, the question is automatically scored as incorrect).
    7.  `is_skipped`: logical type of data indicating whether the student skipped the question.
    8.  `response_time`: amount of time (in seconds) spent by the student on that item. If student moved on but then returned to question during the assessment, *previous and current time are summed up*.
    9.  `choice_id`: unique number identifying which answer choice was selected by the student on that item. In order to make sense of these numbers, we need another file to match them to the answer choices shown for each question.
    10. `blankfield_ans`: numerical variable containing the observed answer for a blankfield item. If *`NA`*, item type is multiple-choice and not blankfield.


## Clean/


### Item Response & Time R script

Script to create master file named [`item-resp-time-data.csv`](#orgea66162) containing item and time response data.

1.  Inputs

2.  Outputs


### Item Response & Time master file

1.  Description:

    This file is named item-resp-time-data.csv and it contains both item responses and response times at the item level for each student, each item and each assessment administered by the AP-CAT projecs. This file was created with the script in [resp-time-data.R](#org7f0504e) and using the raw data file [all\_assignments\_[DATE].csv](#org20d2048).
    
    **Note**: data generated by `practice` or `test` assessments have been removed (see [`assessment_type`](#org3bfa743) variable description).

2.  Data columns:

    -   `user_id`: unique number that identifies each student account in the AP-CAT system.
    -   `qid`: unique identifier for each question in the AP-CAT system.
    -   `item_type`: CREATE THIS VARIABLE. Item type is *`blankfield`* or *`multchoice`*.
    -   `multchoice_ans`: CREATE THIS VARIABLE. answer choice was A, B, C or D, etc.
    -   `response_time`: amount of time (in seconds) spent by the student on that item. If student moved on but then returned to question during the assessment, *previous and current time are summed up*.
    -   `is_correct`: item response data indicating whether the item was answered correctly (1) or incorrectly (0), or `NA` if not shown to the student (if the question was given to student, but they skipped it, the question is automatically scored as incorrect).
    -   `is_skipped`: indicates if student skipped (1) or not (0) a question that was given, or `NA` is question was not given to student in that assignment.
    -   `assessment_name`: name given to the assessment in the AP-CAT system at the time of administration (see details in `documentation.pdf`)
    -   `assessment_group_name`: name of the class taking the assessment, either chosen by the teacher or the AP-CAT team. **May not be unique**, that is, for different pilot years of the study, there may exist classes that were given the same name. For example, &ldquo;Period 1&rdquo;.
    -   `teacher_id`: teacher ID responsible for the class taking the assessment
    -   `creator_role`: actually don&rsquo;t need this column but it is left over from the original dataset.

