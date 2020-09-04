# Oonagh - LAMBS lab documentation 

## How to set up a repository on your own computer

Easiest way to contribute to the website is to set up a local project copy (repository) of this content on your own computer. That way, you can make change to your *local* copy and upload it to the main GitHub repository once you are ready. But don't forget to do this often so that others can also contribute to the most up-to-date version of the file.

### Using RStudio

You need to make sure

  1. Git is installed on your computer, and
  2. RStudio can find Git on your computer
  
  *Note*: [this](https://cfss.uchicago.edu/setup/git-with-rstudio/) can help.


### Using GitHub Desktop

### Using the Command Line

## How to Add Content to the Website



1. Create content in markdown (.md) or Rmarkdown (.Rmd) format. You can do so by
 
   a) click on the **docs/** folder, then at the top click "Add File" and create a new .md file:
   <img src="/docs/new_file.png" width="700">
   <img src="/docs/new_file2.png" width="700">

   b) OR upload an existing file to the docs folder by clicking on the **docs/** folder, then at the top click "Add File" and click "Upload Files" instead,
   
   c) OR upload an existing file from your local repository using the command line
   ```
   git add .
   git -m commit "commit new file"
   git push
   ```

