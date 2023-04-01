# Welcome to Git-Qing!

`Git-Qing` is a **Q**uick **I**nterface for **N**esting **G**igantic-data within git repositories.    
It is designed to help scientists, engineers, and others seamlessly integrate invaluable volumes of data with their Git workflow.

# 1. Why Git-Qing?

In today's big data landscape, we encounter enormous amounts of data on a daily basis. In many cases, we want to implement version control for large data volumes in addition to our source code. For instance, when conducting scientific/engineering simulations or working with machine learning models, we may want to version control the simulation results, prerequisite or training datasets, which can consist of massive amounts of data such as high-resolution images or videos. The size of these datasets can easily exceed 100 GB (some may even reach a few terabytes). 

Let's consider a scenario where two teams, each consisting of 25 members, share a repository that contains 100 GB of binary data but work from different locations. In practice, only one copy of the 100 GB data is needed at each site, and every team member should be able to access it transparently and effortlessly. It is unreasonable for each member to clone an individual copy of the data as it would put an enormous burden on network bandwidth as well as disk space, and significantly increase the clone time, leading to a poor user experience.  Unfortunately, the current GIT utilities available in the market, such as [git-lfs](https://git-lfs.com/), cannot meet the above version control requirements.

Upon closer examination,  we can see that most heavy-lift aspects of version controlling gigantic data is the transfer and archiving of these data. Tracking the change history is a light task in comparison. We only need to record when and why a file is changed and do not necessarily need to perform a git diff on two large binary files. This has inspired me to design this **Q**uick **I**nterface for **N**esting **G**igantic data within git repositories, which allows users to leverage existing data transfer and archiving services, such as local disks, [NAS](https://www.seagate.com/blog/what-is-nas-master-ti/), [HPSS](https://computing.llnl.gov/projects/hpss), FTP, Amazon Web Services, etc.
# 2. How does Git-Qing work?

Git-Qing splits a repository into two spaces: the `GIT` space and the `QING` space. 

The `QING` space is where all the large volume of data actually reside, under the ".qing/" directory of a repository. 

The `GIT` space is the space we are familiar with. All files outside the QING space are in the GIT space.

A `QING` file is a file that has been deposited in the `QING` space and is referenced through a link in the `GIT` space. A `QING` file is named using the SHA512 hash of its content. This provides full assurance of data integrity, as it is impossible for anyone to accidentally corrupt a file without being aware of it.

Users can choose how to transfer, archive, or back up a QING space by providing their own "download" and "upload" plugin scripts in a repository's ".plugins-qing/" directory. Git-Qing provides some example plugins.

The following figure illustrates the difference between a regular `Git` repository and a `Git-Qing` repository.

![photo](figs/git-qing01.jpg)

`Git-Qing` introduces a local mirror so that multiple users in the same computer platform can share one single copy of gigantic data. 

![photo](figs/git-qing02.jpg)

# 3. System requirements

 - Linux systems or other Unix systems with GNU-compatible coreutils, findutils, and grep installed.
 - Git 2.15+
 - 64-bit computer systems are preferred

# 4. A quick tutorial
### 4.1. Clone and install the Git-Qing software in your computer system:
```
git clone https://github.com/git-qing/git-qing
cd git-qing
./install
```
This will install the git-qing software under the `$HOME/local/git-qing` directory.
Be sure to add `$HOME/local/git-qing` to your `PATH` enviromental variable in your .bashrc or .cshrc file.

### 4.2 git qing commands
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

### 4.3. Click the following link for more
[Git-Qing quick tutorial](tutorial.md)

# 5. Best practice to use Git-Qing
To nest a large volume of data into a Git repository, it's best to use the `git qing deposit` command before `git add`. This will deposit large volume of data into the qing space first and then create links at the original file location. 

Using `git add` directly without first using `git qing deposit` can result in repeated computation of SHA512 hash during the "`git add`", "`git status`", and "`git commit`" steps. This can significantly increase the time required to process large amounts of data. By using `git qing deposit` before `git add`, the hash computation is only performed once during the deposit process, resulting in a more streamlined and efficient workflow.

# 6. Potential problems
-   Git-Qing has not been tested for files with empty spaces in their names.
-   It is recommended to avoid using Git-Lfs and Git-Qing simultaneously for a Git repository.
-   It is advised not to use the ".qing" string to name any Git-Qing MIRRORs.
-   Manually creating links inside a Git-Qing MIRROR is not recommended.
-   Git-Qing has not been fully tested for repositories with a pre-commit hook and/or a clean filter, which may cause conflicts.
-   (Note: this applies only to those who use git worktrees) Limited testing has been done for git worktrees, so it is suggested to perform Git-Qing operations under the main worktree instead of linked worktrees.
 
# 7. [FAQ](FAQ.md)
Click this [link](FAQ.md) to visit FAQ

Click this [link](https://github.com/git-qing/git-qing/discussions) to ask questions or join discussions.
