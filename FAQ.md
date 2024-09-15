
# FAQ
### 1. Can I use git-mega on a Windows machine?
git-mega cannot be directly used under a Windows system. However, it can be used in Cygwin or a Linux virtual enviroment on a Windows machine.

### 2. Can I use git-mega in my Macbook?   
If your Macbook default shell is zsh, git-mega cannot be directly used. You have a few options to choose:

(1) install GNU-compatible coreutils, findutils, and grep (recommended)      
`brew install coreutils findutils grep `        

(2) install a Linux container 

(3) install a Linux virtual machine     

### 3. How to update a binary file?

Two options:  
#### 3.1 git rm; copy files and then deposit
```
git rm path_to_files
copy updated files
git mega deposit
git add 
git status
git commit
```  
#### 3.2 withdraw, update and then deposit
```
git mega withdraw
update files
git mega deposit
git add
git status
git commit
```  
The second method will take longer time, especially when data size is large

### 4. what the difference between "install" Git-Mega and "git mega install"?

The Git-Mega software must be installed in a computer system first so that it can be used for different repositories on that computer system. This only needs to be done once per computer platform.

`git mega install` is to install the git-mega filter, and, if .gitattributes does not exist, create a default git-mega setting for a repository. Each fresh clone of a repository will need to run "git mega install" once. 

The git-mega setting is configured per commit. Each commit (branch, tag) can have their own git-mega settings.

### 5. How do I track a binary file in the regular GIT space instead of the MEGA space?
Add the follwoing line into the .gitattributes file:   
`file_name mega.largefiles=none`  
It is highly recommended NOT to track a binary file in the regular GIT space.

### 6. How do I force a small file to be tracked in the MEGA space? 
Add the follwoing line into the .gitattributes file:   
`file_name mega.largefiles=force` 

### 7. I got unexpected changes when I checkout an old commit.    

If you run `git mega install` for a recent commit and want to checkout an old commit which contains large binary files not tracked by git-mega, git-mega will filter large binary files in that old commit. This may introduce unexpected changes relating to unconsistent new line characters. You can discard those changes. Or you may temporarily run `git mega unstall` to disable the git-mega filter and then work on old commits. After completion, you can run `git mega install` again for target commits.

### 8. I got weird behaviors and I cannot figure out the reason.    

You repository may have installed other git hooks which conflicts with the git-mega interface.

### 9. The `git status` says there are changes but `git diff` show no changes at all. 

This is due to the different "newline" character representation in different computer systems. You may safely ignore this.

### 10. It looks like the binary files are not tracked in my first commit ?  
Don't commit large files at the first commit, otherwise it is not tracked in mega history (a known bug to be fixed). 





