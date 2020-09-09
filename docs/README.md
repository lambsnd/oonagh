# Oonagh - LAMBS lab documentation 

## How to set up a repository on your own computer (using RStudio)

Easiest way to contribute to the website is to set up a local project copy (repository) of this content on your own computer. That way, you can make change to your *local* copy and upload it to the main GitHub repository once you are ready. But don't forget to do this often so that others can also contribute to the most up-to-date version of the file.

You need to make sure

  1. Git is installed on your computer, and
  2. RStudio can find Git on your computer
  
  *Note*: [this](https://cfss.uchicago.edu/setup/git-with-rstudio/) can help.

If you have installed Git and RStudio knows how to find it, you can now set up a repository on your computer by copying the files to your computer.

### Copy repository into your computer

This is called "cloning" the repository.
  1. Go to the `oonagh` repository and click the green button "Code" on the upper hand corner. To clone with SSH, copy the address. You might need to authenticate first.
  2. *File > New Project* > *Version Control* > *Git*. Under "Repository URL", paste the address from step 1.
  3. Change the "Project directory name", or keep it as is.
  4. Click on "Browse..." to choose the folder in which you will create a copy of the repository in your computer. This will create a folder in the directory you choose.
  5. Click "Create repository" to finish.
  
### Upload new file to GitHub

Suppose you have been working on a file you wish to share on GitHub. This example uses a markdown (.md) file, but you can follow the same steps for any file format.

1. If you have set up a local copy of the repository on GitHub, you can proceed to step 2. Otherwise, go to the [previous section](#copy-repository-into-your-computer).
2. Make sure the file is in the folder of the local copy of the repository. In RStudio, make sure you have opened the project of your local repository.
  
### Upload changes made to an existing file

Before starting to make any changes to an existing file, please **make sure the version on your computer is current** by downloading (pulling) the most up-to-date version from the GitHub repository: *Tools* > *Version Control* > *Pull Branches*.

1. After you have edited the file, save it and commit (save changes to your local git repository): *Tools* > *Version Control* > *Commit...*. 
2. On the commit window, check the box or boxes under the "Change" tab to stage your changes (signal to git that you want to commit the file).
3. Add a "Commit message" on the designated space in upper right corner. This message should be something descriptive, related to the changes you have made. 
4. Then click "Commit". You will now see the message "Your branch is ahead of 'origin/master' by 1 commit." on top of the commit window.
5. To upload updated files to GitHub, go to *Tools* > *Version Control* > *Push Branch*. You should now be able to see your updated file on the GitHub repository.

### Open existing repository into RStudio

### How to Add New Content to the Oonagh Website

1. Create content in markdown (.md) or Rmarkdown (.Rmd) format. You can do so by
 
   a) clicking on the **docs/** folder, then at the top click "Add File" and create a new .md file:
   <img src="/docs/new_file.png" width="700">
   <img src="/docs/new_file2.png" width="700">

   b) OR uploading an existing file to the docs folder by clicking on the **docs/** folder, then at the top click "Add File" and click "Upload Files" instead,
   
   c) OR uploading a file from your local repository using RStudio.

