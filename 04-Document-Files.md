
# Table of Contents

1.  [Introduction](#org24ec74f)
2.  [Assessments Info/](#org2bcece7)
    1.  [assessments-info.R](#orgd3aeff7)
        1.  [Inputs](#org00a4528)
        2.  [Outputs:](#org0a6b194)
    2.  [assessments-info-[DATE].csv](#org04c6078)
        1.  [Description:](#orgb191e11)
        2.  [Data columns:](#org564d087)
    3.  [assessment<sub>names.csv</sub>:](#org4667a34)
    4.  [assessments-qids.csv](#orgaec6ef7)
3.  [Assessments Data/](#orgb3f51fa)
    1.  [Raw/](#org0573aa8)
        1.  [all<sub>assignments</sub>\_[DATE].csv:](#org2207ee8)
        2.  [IRT<sub>calibration.csv</sub>:](#org45c5380)
    2.  [Clean/](#orgd0893a7)
        1.  [resp-time-data.R](#org09ff2d4)
        2.  [item-resp-time-data.csv](#org6e4edbf)



<a id="org24ec74f"></a>

# Introduction

This documents the file structure of folder Data & Documentation, which contains two main folders: Assessments Info and Assessments Data. It also describes the AP-CAT project regarding assignments, system usernames, teachers and classes system IDs.


<a id="org2bcece7"></a>

# Assessments Info/


<a id="orgd3aeff7"></a>

## <a id="orga24e39f"></a> assessments-info.R


<a id="org00a4528"></a>

### Inputs

It uses the file  [Assessments Data/Raw/all\\<sub>assignments</sub>\\\_[DATE].csv](#orgcc78e69) to obtain information about which assessments were given each year by the AP-CAT project and which were given by the teachers participating in the study (as practice assignments). This script will need to be re-run by the end of the data collection in May/2020.

This script sorts assignments by `pilot year` (1 to 5), `creator_role` (*`staff`*, *`teacher`*, *`test`*), [`assessment_type`](#org543b534) (*`apcat`*, *`practice`*, *`system-test`*), and provides information on the due date of each AP-CAT assessment, [`assessment_id`](#orgc5dbfb3) associated with each teacher (`creator_id`) and class (`assessment_group_id`) in the study, whether the test was adaptive, whether it was published at the time the data was retrieved from the system. Please use `documentation.pdf` to match teacher and class IDs with their actual names.


<a id="org0a6b194"></a>

### Outputs:

-   [assessment-names.csv](#org8df3cc4)
    
    **WARNING**: this file contains identifiable information.

-   [assessments-info-[DATE].csv](#org79d9bc7)
    
    **WARNING**: this file contains identifiable information.


<a id="org04c6078"></a>

## <a id="org79d9bc7"></a> assessments-info-[DATE].csv


<a id="orgb191e11"></a>

### Description:

This file contains info on assessments administered in the AP-CAT project from 2015-16 (first pilot) to 2018-19 (fourth pilot). It includes information on assignment names, school year it was administered, class and teacher information, and its original due date. This data file may be used to learn which assignments were administered each year, chronological order of the assessments within a year, which assessment IDs belong to a specific assessment, etc. Use of the `tidyverse` R package is recommended. File was created with the script in [Assessments Info/assessments-info.R](#orga24e39f) and using [Assessments Data/Raw/IRT\\<sub>calibration.csv</sub>](#orgdb4ecc2).


<a id="org564d087"></a>

### Data columns:

-   <a id="orgc5dbfb3"></a> `assessment_id`: unique number identifying each assessment created in the AP-CAT system, usually corresponding to one assessment created for each class.
-   `assessment_name`: name given to the assessment at the time of administration.
-   `pilot_year`: values 1 through 5, where
    -   1 = 2015-16
    -   2 = 2016-17
    -   3 = 2017-18
    -   4 = 2018-19
    -   5 = 2019-20
-   <a id="org543b534"></a> `assessment_type`: 
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


<a id="org4667a34"></a>

## <a id="org8df3cc4"></a> assessment<sub>names.csv</sub>:

This file is created by the script in [Assessments Info/assessments-info.R](#orga24e39f) and it contains a single column with the names of all the assessments that were planned and administered by the AP-CAT staff, that is, it *does not* include practice assignments created by teachers or system-test type of assessments.

To learn which assignments were administered each year, the chronological order of the assessments within a year, assessment IDs, etc. refer to [Assessments Info/assessments-info.csv](#org79d9bc7).


<a id="orgaec6ef7"></a>

## assessments-qids.csv


<a id="orgb3f51fa"></a>

# Assessments Data/


<a id="org0573aa8"></a>

## Raw/


<a id="org2207ee8"></a>

### <a id="orgcc78e69"></a> all<sub>assignments</sub>\_[DATE].csv:

Raw file generated by the AP-CAT system. It is NOT comma separated; in R, you need to speficy separator is &ldquo;\\\t&rdquo;. File contains the following columns:

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


<a id="org45c5380"></a>

### <a id="orgdb4ecc2"></a> IRT<sub>calibration.csv</sub>:

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


<a id="orgd0893a7"></a>

## Clean/


<a id="org09ff2d4"></a>

### resp-time-data.R

Script to create master file named [`item-resp-time-data.csv`](#orgeaf7785) containing item and time response data.

1.  Inputs:

2.  Outputs


<a id="org6e4edbf"></a>

### <a id="orgeaf7785"></a> item-resp-time-data.csv

1.  Description:

    This file contains response times at the item level for each student, each item and each assessment administered by the AP-CAT project (see details in `documentation.pdf`). This file was created with the script in `resp-time-data.R` and using the raw data file `Assessments Data/Raw/all_assignments_[DATE].csv`.
    
    **Note**: data generated by practice or test assessments have been removed.

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

