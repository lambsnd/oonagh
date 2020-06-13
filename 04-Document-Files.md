
# Table of Contents

1.  [Introduction](#org158590f)
2.  [Assessments Info/](#org14cab80)
    1.  [-info R script](#org55c4ed7)
        1.  [Inputs](#org69d3329)
        2.  [Outputs](#orgfcc16ff)
    2.  [-info .csv file](#orgf87fb9a)
        1.  [Description:](#orgc413de7)
        2.  [Data columns:](#org417ed76)
    3.  [-names .csv file](#orgee4ee7e)
    4.  [-qids .csv file](#orgde0c34b)
3.  [Assessments Data/](#org2e211ef)
    1.  [Raw/](#org3c4c3e0)
        1.  [&ldquo;all assignments&rdquo;](#org6c9790d)
        2.  [&ldquo;IRT calibration&rdquo;](#org076ac0c)
    2.  [Clean/](#org02d25b9)
        1.  [Item Response & Time R script](#org4c5917b)
        2.  [Item Response & Time master file](#org9611305)



<a id="org158590f"></a>

# Introduction

This documents the file structure of folder Data & Documentation, which contains two main folders: Assessments Info and Assessments Data. It also describes the AP-CAT project regarding assignments, system usernames, teachers and classes system IDs.


<a id="org14cab80"></a>

# Assessments Info/


<a id="org55c4ed7"></a>

## <a id="org39d84ba"></a> -info R script


<a id="org69d3329"></a>

### Inputs

It uses the file  [all\\<sub>assignments</sub>\\\_[DATE].csv](#org92f87b4) to obtain information about which assessments were given each year by the AP-CAT project and which were given by the teachers participating in the study (as practice assignments). This script will need to be re-run by the end of the data collection in May/2020.

This script sorts assignments by `pilot year` (1 to 5), `creator_role` (*`staff`*, *`teacher`*, *`test`*), [`assessment_type`](#org73a4425) (*`apcat`*, *`practice`*, *`system-test`*), and provides information on the due date of each AP-CAT assessment, [`assessment_id`](#org1fa0073) associated with each teacher (`creator_id`) and class (`assessment_group_id`) in the study, whether the test was adaptive, whether it was published at the time the data was retrieved from the system. Please use `documentation.pdf` to match teacher and class IDs with their actual names.


<a id="orgfcc16ff"></a>

### Outputs

-   [assessment-names.csv](#org31f9cf6)
    
    **WARNING**: this file contains identifiable information.

-   [assessments-info-[DATE].csv](#org0419e7b)
    
    **WARNING**: this file contains identifiable information.


<a id="orgf87fb9a"></a>

## <a id="org0419e7b"></a> -info .csv file


<a id="orgc413de7"></a>

### Description:

This file contains info on assessments administered in the AP-CAT project from 2015-16 (first pilot) to 2018-19 (fourth pilot). It includes information on assignment names, school year it was administered, class and teacher information, and its original due date. This data file may be used to learn which assignments were administered each year, chronological order of the assessments within a year, which assessment IDs belong to a specific assessment, etc. Use of the `tidyverse` R package is recommended. File was created with the script in [Assessments Info/assessments-info.R](#org39d84ba) and using [Assessments Data/Raw/IRT\\<sub>calibration.csv</sub>](#org0c4fc78).


<a id="org417ed76"></a>

### Data columns:

-   <a id="org1fa0073"></a> `assessment_id`: unique number identifying each assessment created in the AP-CAT system, usually corresponding to one assessment created for each class.
-   `assessment_name`: name given to the assessment at the time of administration.
-   `pilot_year`: values 1 through 5, where
    -   1 = 2015-16
    -   2 = 2016-17
    -   3 = 2017-18
    -   4 = 2018-19
    -   5 = 2019-20
-   <a id="org73a4425"></a> `assessment_type`: 
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


<a id="orgee4ee7e"></a>

## <a id="org31f9cf6"></a> -names .csv file

This file is created by the script in [Assessments Info/assessments-info.R](#org39d84ba) and it contains a single column with the names of all the assessments that were planned and administered by the AP-CAT staff, that is, it *does not* include practice assignments created by teachers or system-test type of assessments.

To learn which assignments were administered each year, the chronological order of the assessments within a year, assessment IDs, etc. refer to [Assessments Info/assessments-info.csv](#org0419e7b).


<a id="orgde0c34b"></a>

## -qids .csv file


<a id="org2e211ef"></a>

# Assessments Data/


<a id="org3c4c3e0"></a>

## Raw/


<a id="org6c9790d"></a>

### <a id="org92f87b4"></a> &ldquo;all assignments&rdquo;

This raw file is named all\\<sub>assignments</sub>\\\_[DATE].csv. File is generated by the AP-CAT system. It is NOT comma separated. In R, you will need to speficy separator is &ldquo;\t&rdquo;. File contains the following columns:

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


<a id="org076ac0c"></a>

### <a id="org0c4fc78"></a> &ldquo;IRT calibration&rdquo;

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


<a id="org02d25b9"></a>

## Clean/


<a id="org4c5917b"></a>

### <a id="org3bc65b0"></a> Item Response & Time R script

Script to create master file named [`item-resp-time-data.csv`](#org2c53e7b) containing item and time response data.

1.  Inputs

2.  Outputs


<a id="org9611305"></a>

### <a id="org2c53e7b"></a> Item Response & Time master file

1.  Description:

    This file is named item-resp-time-data.csv and it contains both item responses and response times at the item level for each student, each item and each assessment administered by the AP-CAT projecs. This file was created with the script in [resp-time-data.R](#org3bc65b0) and using the raw data file [all\\<sub>assignments</sub>\\\_[DATE].csv](#org92f87b4).
    
    **Note**: data generated by `practice` or `test` assessments have been removed (see [`assessment_type`](#org73a4425) variable description).

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

