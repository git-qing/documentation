
# FAQ
### 1. Can I use git-qing on a Windows machine?
git-qing cannot be directly used under a Windows system. However, it can be used in Cygwin or a Linux virtual enviroment on a Windows machine.

### 2. Can I use git-qing in my Macbook?   
If your Macbook default shell is zsh, git-qing cannot be directly used. You have a few options to choose:

(1) install GNU-compatible coreutils, findutils, and grep (recommended)      
`brew install coreutils findutils grep `        

(2) install a Linux container 

(3) install a Linux virtual machine     

### 3. How to update a binary file?

#### 3.1 git rm; copy files and then deposit
```
git rm path_to_files
copy updated files
git qing deposit
git add 
git status
git commit
```  
#### 3.2 withdraw, update and then deposit
```
git qing withdraw
update files
git qing deposit
git add
git status
git commit
```  
The second method will take longer time, especially when data size is large

### 4. what the difference between "install" Git-Qing and "git qing install"?

The Git-Qing software must be installed in a computer system first so that it can be used for different repositories on that computer system. This only needs to be done once per computer platform.

`git qing install` is to install the git-qing filter, and, if .gitattributes does not exist, create a default git-qing setting for a repository. Each fresh clone of a repository will need to run "git qing install" once. 

The git-qing setting is configured per commit. Each commit (branch, tag) can have their own git-qing settings.

### 5. How do I track a binary file in the regular GIT space instead of the QING space?
Add the follwoing line into the .gitattributes file:   
`file_name qing.largefiles=none`

### 6. How do I force a small file to be tracked in the QING space? 
Add the follwoing line into the .gitattributes file:   
`file_name qing.largefiles=force` 

### 7. I got unexpected changes when I checkout an old commit.    

If you run `git qing install` for a recent commit and want to checkout an old commit which contains large binary files, git-qing will take effect and filter large binary files. This may introduce unexpected changes. You can discard those changes. Or you may temporarily run `git qing unstall` to disable the git-qing filter. After completion, run `git qing install` again. 

### 8. I got weird behaviors and I cannot figure out the reason.    

You repository may have installed other git hooks which conflicts with the git-qing interface.

### 9. The `git status` says there are changes but `git diff` show no changes at all. 

This is due to the different "newline" character representation in different computer systems. You may safely ignore this.

### 10. It looks like the binary files are not tracked in my first commit ?  
Don't commit large files at the first commit, otherwise it is not tracked in qing history. 





