# Oonagh - LAMBS lab documentation 

## How to set up a repository on your own computer

Easiest way to contribute to the website is to set up a local project copy (repository) of this content on your own computer. That way, you can make change to your *local* copy and upload it to the main GitHub repository once you are ready. But don't forget to do this often so that others can also contribute to the most up-to-date version of the file.

### Using RStudio

You need to make sure

  1. Git is installed on your computer, and
  2. RStudio can find Git on your computer
  
  *Note*: [this](https://cfss.uchicago.edu/setup/git-with-rstudio/) can help.

If you have installed Git and RStudio knows how to find it, you can now set up a repository on your computer by copying the files to your computer.

#### Copy repository into your computer

This is called "cloning" the repository.
  1. Go to the `oonagh` repository and click the green button "Code" on the upper hand corner. To clone with SSH, copy the address. You might need to authenticate first.
  2. *File > New Project* > *Version Control* > *Git*. Under _Repository URL_, paste the address from step 1.
  3. Change the _Project directory name_, or keep it as is.
  4. Click on _Browse..._ to choose the folder in which you will create a copy of the repository in your computer. This will create a folder in the directory you choose.
  5. Click _Create repository_.
  
#### Upload changes to GitHub




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

