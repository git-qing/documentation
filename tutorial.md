## A Quick Git-Qing Tutorial

### 1. Clone and install the Git-Qing software in your computer system:
```
git clone https://github.com/git-qing/git-qing
cd git-qing
./install
```
This will install the git-qing software under the `$HOME/local/git-qing` directory.
Be sure to add `$HOME/local/git-qing` to your `PATH` enviromental variable in your .bashrc or .cshrc file.

### 2. git qing commands
run `git qing help` to show avaible git qing commands:
```
  qit qing [help]
  git qing hello
  git qing install
  git qing deposit/withdraw <dir|file>
  git qing upload/download
  git qing gethash file
  git qing compareDirs src dest
  git qing verify <dir>
  git qing repair <dir>
  git qing allHandsCheck
  git qing uninstall
```

### 3. Clone a demostration Git-Qing repository
```
cd A_PATH (enter the directory where you want to clone the demo repository)
git clone https://github.com/git-qing/demo
cd demo
```

### 4. Generate a few files (including text files and large binary files)
make sure you are under the `demo/` directory
```
./genFiles.sh  
ls -l
```
NOTE:   
a. Comment out the "10G" line first if you want to test a file of 10G in size  
b. This step may take a few minutes. 


### 5. install the git-qing filter for this repository/branch
`git qing install`

### 6. Deposit large binary files into the QING space
`git qing deposit .`
 
You may notice that large files (such as 3G.img) will take longer time to process.  

Run `ls -l` again, you will see that large or binary files were deposited into the QING space and links were created at their original location.

### 7. Commit changes
```
   git status
   git add .
   git commit -m "Add large/binary files"
```

### 8. Push changes to servers; upload local large/binary files to a local and/or remote MIRRORs
### 8.1 Push changes to a Github repository

Following normal procedures to push local changes to a Github repository. For example, your Github repo URL is: https://github.com/myaccount/demo.
```
git remote add myaccount https://github.com/myaccount/demo
git push myaccount main
```
You may notice that only the light-weighted GIT space was pushed to the Github repository. The large/binary files still stay at the local QING space. We will upload those large/binary file in the next step

### 8.2 upload large/binary files to a local and/or remote MIRRORs
```
git qing upload
```
The output will say: `.plugins-qing/upload not found`

This is correct, as we don't provide download/upload plugins yet.   
Let's create them based on example plugins:  
```
cd demo
mkdir -p .plugins-qing   ## be sure to have a leading dot
cd .plugins-qing
cp $HOME/local/git-qing/plugins/cp_mv.plugins-qing/* .
```     
If you want to save a copy to HPSS, you can use the HPSS plugins
`cp $HOME/local/git-qing/plugins/hpss.plugins-qing/* .`

For simplicity and demonstration purpose, let's remove the whole `if` block in mirror.sh and add one line as follows:     
```
MIRROR="/Path/to/demo_mirror" 
#Recommend to use an absolute path
```  

Now run `git qing upload` again.
It shows what files will be uploaded to MIRROR and which command to run to complete this process:
```
run the following command to upload to MIRROR-/tmp/gge/demo_mirror
   /tmp/gge/demo/.git/tmp_copy_qing_files

after that, run 'git qing upload' again to make sure no more qing files need to be uploaded
```

Run the given command. In the example here, it is `/tmp/gge/demo/.git/tmp_copy_qing_files`.

Now all files are succesfully uploaded into the MIRROR `/Path/to/demo_mirror`.       

If you use the HPSS version plugins, a copy is also uploaded to HPSS.





