# Version Control using GitHub

## Summary (TL;DR)
  - *File > New Project* > *Version Control* > *Git*. 
    - [Set up a copy](#copy-github-repository-into-your-computer) of the GitHub repository (*local repository*) in your own computer.
  - *Tools* > *Version Control* > *Pull Branches*. 
    - Before you start to make any changes, make sure the file version in your computer is the most up-to-date. To do so, you will need to *pull* branches from the GitHub repository.
  - *Tools* > *Commit...*. 
    - Any time you make changes, you need to *commit* or [save changes](#upload-changes-made-to-an-existing-file) to your local repository. 
    - Add a descriptive *commit message* in case you ever need to go back to a certain version.
  - *Tools* > *Version Control* > *Push Branch*. 
    - After you commit, you will need to *push* the changes, or upload changes to GitHub.

## How to set up a repository on your own computer (using RStudio)

You need to make sure

  1. Git is installed on your computer, and
  2. RStudio can find Git on your computer
  
  *Note*: [this](https://cfss.uchicago.edu/setup/git-with-rstudio/) can help.

If you have installed Git and RStudio knows how to find it, you can now set up a repository on your computer by copying the files to your computer.

### Copy GitHub repository into your computer

This is called "cloning" the repository.
  1. Go to the `oonagh` repository on GitHub and click the green button "Code" on the upper hand corner. 
      - To clone with SSH or HTTPS, copy the address. 
      - You might need to authenticate into GitHub first.
  2. Go to *File > New Project* > *Version Control* > *Git*. 
      - Under "Repository URL", paste the address from step 1.
  3. Change the "Project directory name" (optional). Let's call it oonagh-local/.
  4. Click on "Browse..." and choose __the folder to house a copy of the repository__.
      - For example, if you choose ~/Documents/GitHub/, you can access a copy of the repository at ~/Documents/GitHub/oonagh-local/.
  5. Click "Create repository" to finish.
 
### Open existing local repository into RStudio

1. With RStudio open, go to *File* > *Open Project...*
2. Select the folder corresponding to your local repository, which in our example is oonagh-local/. You're done! 
 
## Using version control with RStudio

Before starting to make any changes to an existing file, please **make sure the version on your computer is current** by downloading (pulling) the most up-to-date version from the GitHub repository: *Tools* > *Version Control* > *Pull Branches*.

### Upload changes made to an existing file

1. After you have edited the file, save it and commit (save changes to your local git repository): *Tools* > *Version Control* > *Commit...*. 
2. On the Commit window, check the box or boxes under the "Change" tab to stage (signal to git that you want to commit the file) your changes.
3. Add a "Commit message" on the designated space in upper right corner. This message should be something descriptive, related to the changes you have made. 
4. Then click "Commit". You will now see the message "Your branch is ahead of 'origin/master' by 1 commit." on top of the commit window.
5. To upload updated files to GitHub, go to *Tools* > *Version Control* > *Push Branch*. You should now be able to see your updated file on the GitHub repository.

### Upload new file to GitHub

Suppose you have been working on a file you wish to share on GitHub. This example uses a markdown (.md) file, but you can follow the same steps for any file format.

1. If you have set up a local copy of the repository on GitHub, you can proceed to step 2. Otherwise, go to the [previous section](#copy-github-repository-into-your-computer).
2. Make sure the file is in the folder of the local copy of the repository, and that in RStudio you have opened the project of your local repository.
3. Click *Tools* > *Commit...* and check the to commit the new file under the "Change" tab.
4. Add a "Commit message" on the designated space in upper right corner. This message should be something descriptive, related to the changes you have made. 
4. Then click "Commit". You will now see the message "Your branch is ahead of 'origin/master' by 1 commit." on top of the commit window.
5. Go to *Tools* > *Version Control* > *Push Branch* to upload changes to GitHub. You should now be able to see your updated file on the GitHub repository.
  

<!-- ## How to add new content to the Oonagh website

<!-- Easiest way to contribute to the website is to [set up a local project copy](#copy-github-repository-into-your-computer) on your own computer. That way, you can make changes to your *local* copy of the files and upload them to the main GitHub repository once you are ready. But don't forget to do this often so that others can also contribute to the most up-to-date version of the files.


<!--1. Create content in markdown (.md) or Rmarkdown (.Rmd) format. You can do so by:

<!--   a) creating a file using RStudio by going to *File* > *New File* > *Markdown File* or *R Markdown...*,
 
<!--   b) OR clicking on the **docs/** folder, then at the top click "Add File" and create a new .md file:
   <img src="/docs/new_file.png" width="700">
   <img src="/docs/new_file2.png" width="700">

<!--   c) OR uploading an existing file to the docs folder by clicking on the **docs/** folder, then at the top click "Add File" and click "Upload Files" instead,
   
2. Edit and upload changes by:

    a) [using RStudio](#upload-new-file-to-github),
    
    b) OR editing the file directly on GitHub. Click on the file you want to edit, then on the file window, upper right corner, you will see a pencil :pencil2: icon to edit. GitHub provides a file preview for Markdown and RMarkdown files.
-->


## Git Vocabulary

- `clone`: when you _clone_ a repository, you effectively _download_ and _create a copy_ of the repository locally on your computer.
- `stage`: you need to _stage_ files to "warn" git that you intend to commit changes to a file.
- `commit`: when you _commit_ changes to your local repository, you are effectively "saving" the file and _creating a log_ of the changes when you add a _commit message_.
    - _commits_ create a picture of the file at a point in time; it does so by recording specifically which changes of made (as opposed to saving a full version of the file, like some software do).
    - 
- `push`: when you _push_ into a remote repository, it effectively _uploads_ or _updates_ files to the remote repository.
    - you can push into any repositories you own, but you might have to request special access to push into a shared repository.
- `pull`: when you _pull_ from a remote repository, you effectively _download_ files from the remote repository.
- `repository`: 
- `remote repository`:
- `local repository`:
- 

#### Tutorial by [Dani Rebouças](https://www.github.com/drebouca)
