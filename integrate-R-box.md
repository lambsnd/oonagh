
## How to read files from Box directly into R

### Step 1:

Create a Box developer app following the instructions in https://r-box.github.io/boxr/articles/boxr-app-interactive.html

### Step 2:

After you have created a Box app, install the package `boxr` in R and load using `library(boxr)`.

### Step 3:

Now use function `box_auth()` and the app's `client_id` and `client_secret` to authenticate your Box account. Follow the instructions here: https://r-box.github.io/boxr/articles/boxr.html#authentication 

You are now ready to load files directly from Box using the `boxr` package in R.

### Step 4:

Search for desired file:

```R
bs <- box_search("merged")
bs
```

You will see the following output (owner's email account was omitted):

    box.com remote object list (3 objects)

        Summary of first 3:
  
                        name type           id   size          owner
    1 pilot5_merged_anon.csv file 678762427291   4 MB -------@nd.edu
    2 pilot5_merged_anon.rds file 678762767845 580 kB -------@nd.edu
    3        READ ME.boxnote file 678762725496 1.7 kB -------@nd.edu

    Use as.data.frame() to extract full results.
    
Now load your data onto R:

