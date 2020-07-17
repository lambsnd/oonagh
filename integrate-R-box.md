
## How to read files from Box directly into R

### 1. Create a Box developer app

Follow the instructions in https://r-box.github.io/boxr/articles/boxr-app-interactive.html

### 2. Install `boxr` package

After you have created a Box app, install the package `boxr` in R and load using `library(boxr)`.

### 3. Authenticate Box aacount

Now use function `box_auth()` and the app's `client_id` and `client_secret` to authenticate your Box account. Follow the instructions here: https://r-box.github.io/boxr/articles/boxr.html#authentication 

You are now ready to load files directly from Box using the `boxr` package in R.

### 4. Use `boxr` functions to load a Box file

#### a) Search for a file

In this example, we are searching for an anonimized version of the survey data from Pilot 5. We recall the file has the tag "anon" in it, but we do not remember the exact name. When searching for a file, use the most unique part of a file name. For example, if you include the word "data" in your search, you will receive a long list of results. If your search returns more than 10 objects, the `box_search()` function outputs only the first 10 objects.
```R
bs <- box_search("merged")
bs
```

You will see the following output (owner's email account was omitted):

    box.com remote object list (26 objects)

      Summary of first 10:

                                         name type           id   size           owner
    1                  pilot5_merged_anon.csv file ********9808   5 MB --------@nd.edu
    2                       pilot5_merged.rds file ********9752 580 kB --------@nd.edu
    3                  pilot5_merged_anon.csv file ********7291   4 MB --------@nd.edu
    4                  pilot5_merged_anon.rds file ********7845 580 kB --------@nd.edu
    5                         merged_data.csv file ********4632 360 kB --------@nd.edu
    6                         merged_data.csv file ********9954 300 kB --------@nd.edu
    7                       pilot5_merged.csv file ********4394   4 MB --------@nd.edu
    8  pilot4_merged_APmock_data_20200305.csv file ********6741 970 kB --------@nd.edu
    9  pilot4_merged_APmock_data_20200305.rds file ********8022 230 kB --------@nd.edu
    10  pilot4_merged_data_updated_20200305.R file ********7744  61 kB --------@nd.edu
  
    Use as.data.frame() to extract full results.

#### b) Load file from Box into R

We would like to load the first file, `pilot5_merged_anon.csv`, onto R. This is the clean, anonimized survey dataset we were looking for. Now we use the output from `box_search()` directly into `box_read()`:

```R
bs <- box_search("pilot5_merged_anon.csv")
all_survey <- box_read(bs) # reads first file on the list
```

Done! You can now use the object `all_survey` in your environment in R.

#### Other ways to search for a file

Suppose you do not remember the file name, but you remember the folder name. For example, we may recall this data file is somewhere in the "AP-CAT Fifth Pilot" folder in Box. You can first find the folder ID (`box_search()`), change the directory to that folder (`box_setwd()`), and list all the files on that folder (`box_ls`) or narrow your search within that file:

```R
fs <- box_search("Fifth Pilot",
                 type = "folder")
fs
```

      Summary of first 1:

                    name   type          id   size           owner
    1 AP-CAT Fifth Pilot folder *******1415 420 MB --------@nd.edu

Change the directory to "AP-CAT Fifth Pilot":
```R
fs %>%
  as.data.frame() %>%
  filter(name == "AP-CAT Fifth Pilot") %>%
  select(id) %>% unlist() -> wd_id
box_setwd(wd_id) # changes directory to 
```

    box.com working directory changed to 'AP-CAT Fifth Pilot'

          id: *******1415
        tree: All Files/NSF AP_CAT/AP-CAT Fifth Pilot
       owner: --------@nd.edu
    contents: 3 files, 8 folders

And list all objects in the folder:
```
box_ls()
```

    box.com remote object list (11 objects)

      Summary of first 10:

                                                name   type           id   size
    1                      2019-20 class information folder  *******0003 330 MB
    2                         2019-2020 Assignment 1 folder  *******3656 3.6 MB
    3                         2019-2020 Assignment 2 folder  *******4475 1.1 MB
    4                         2019-2020 Assignment 3 folder  *******1296 810 kB
    5              2019-2020 Assignment 4 (adaptive) folder  *******7035  63 kB
    6                           Administrative forms folder  *******1727 1.2 MB
    7                          AP-CAT raffle winners folder  *******0214 5.8 kB
    8                                           Data folder  *******6259  85 MB
    9                                  all_users.csv   file  *******9066 100 kB
    10 pilot5_student_roster_2020_03_06_updated.xlsx   file  *******7581  45 kB

Alternatively, we can search directly for the file:

```R
bs <- box_search("merged")
bs
```

And the output will be:

      Summary of first 10:

                                         name type           id   size
    1                  pilot5_merged_anon.csv file 692412069808   5 MB
    2                       pilot5_merged.rds file 631004009752 580 kB
    3                  pilot5_merged_anon.csv file 678762427291   4 MB
    4                  pilot5_merged_anon.rds file 678762767845 580 kB
    5                         merged_data.csv file 448094904632 360 kB
    6                         merged_data.csv file 408895539954 300 kB
    7                       pilot5_merged.csv file 631016974394   4 MB
    8  pilot4_merged_APmock_data_20200305.rds file 661155798022 230 kB
    9  pilot4_merged_APmock_data_20200305.csv file 628364146741 970 kB
    10  pilot4_merged_data_updated_20200305.R file 628360947744  61 kB

Finally, read file and create data object:
```R
all_survey <- box_read(bs) # reads first file on the list
```


### Extras

#### How to upload file into Box

You can also save a new file or update an existing file directly into box. The important detail to pay attention to is to make sure you are working with the intended folder. First search folder:

```R
ws <- box_search("Combined",
                 type = "folder")
ws
```

      Summary of first 2:

                     name   type           id   size           owner
    1       Combined Data folder  *******4491  34 MB --------@nd.edu
    2 Combined Clean Data folder  *******2557 6.2 MB --------@nd.edu

Then, using piping commands from the package `dplyr`, obtain the `id` for the "Combined Data" folder, and use this `id` as the `dir_id` when writing a file into box using the `box_write()` function:

```R
## using piping commands from 'dplyr'  
ws %>%
  as.data.frame() %>%
  filter(name == "Combined Data") %>%
  select(id) %>% unlist() %>%
  box_write(dir_id = .,
            x = all_survey,
            file_name = "pilot5_merged.rds")
```

If file with that name already exists, `boxr` will attempt to upload a new version of the file.

    |======================================================================| 100%
    File 'pilot5_merged.rds' aleady exists. Attempting to upload new version (V9).
    |======================================================================| 100%

    box.com remote file reference

     name        : pilot5_merged.rds 
     file id     : *******9752 
     version     : V9 
     size        : 600 kB 
     modified at : 2020-07-17 12:24:44 
     created at  : 2020-07-17 12:24:44 
     uploaded by : --------@nd.edu 
     owned by    : --------@nd.edu 
     shared link : None 

     parent folder name :  Combined Data 
     parent folder id   :  *******4491 
