####1. Configuration
####2. Remote Repo Commands

####1. Configuration
```
1.1 git config --global user.name "[name]"
1.2 git config --global user.email "[email address]"
```
```
1.3 git config --global http.proxy http://proxyuser:proxypwd@proxy.server.com:8080 
    //set http proxy in git config
```
```
1.4 git config -l //view git configs
```

####2.Remote Repo Commands
```
2.1 git init //initialize a git repo in the current directory
```
```
2.2 git clone https://github.com/user/repo.git -o notorigin 
    //sets the remote to "notorigin"
```
```
2.3 git remote add origin https://github.com/user/repo.git 
    //set a new remote
```
```
2.4 git remote set-url origin https://github.com/user/repo2.git 
    //change the remote URL for origin
```
```
2.5 git remote update //update the local repo with remote tracking branches. Use this if you don't see you branch using git branch -r
```
```
2.6 git remote -v //verify new remote
```

####3. Make Changes
#####3.1 git status
```
git status // lists all new or modified unstaged files
git status -b // show the branch and tracking info
```
#####3.2 git diff
```
git diff            //changes in the working tree not yet staged for the next commit
git diff --cached   
git diff HEAD       (3)
```
#####3.1 git add
```
 git add <file.name>  //start tracking file.name
 git add -A  //stages All (modified, deleted, untracted, and new files);
 git add -u  //stages modified and deleted, without new;
 git add . //stages new and modified, without deleted;
```

#####3.2 git branch
```
git branch // 
git branch -r -- view available local remote branches
git branch -vv -- view the tracking branch
git branch <branch_name> -- create a new branch
git checkout <branch_name> -- switch to a new branch
git checkout master  -- switch to master branch
git merge <branch_name>  -- merge <branch_name> into master
git branch -d <branch_name> -- delete a branch (locally !!!)
git push origin --delete <branchName>  -- delete a remote branch
or git push origin :<branchName>
git push  -- commit master
```

```
3.2 git status -- show current state of project
```
```
3.3 git checkout --track origin/serverfix -- change the tracking branch
```
```
3.4 git diff --cached -- shows changes in index
    git diff HEAD -- show the diff of the most recent commit;
    git diff --stated  --show the change you just staged;
```
```
3.5 git rm --cached -- remove file from the index but not working dir
    git rm $(git ls-files --deleted)
    
    With red color(--deleted files), "git add -A". Deleted files become green color. Then "git commit -m 'delete files'"
```
```
3.6 git clean -f -X -d -- remove all unstaged files (great for cleaning up after a build)
```

```
3.7 git reset --hard HEAD -- reset your local branch to the HEAD commit
    git reset <file.name> -- unstage the file
```
```
3.8 git checkout HEAD -- folder1/pom.xml -- reset a single file to the HEAD commit
```
```
3.9 git show-ref -- shows the refs for the repo (still figuring this out)
```

```
3.10 git filter-branch --prune-empty --subdirectory-filter lib master -- split out a sub dir into a repository
```

```
3.11 
```

```
3.12 git commit -m 'add a message' -- files are listed in stating area.
```

```
3.13 git log -- show all changes we have committed so far.
```

####4. Git Workflow
```
4.1 git checkout -b john-dev-2 origin/release-1.0.0 -- check out from a remote branch
```

```
4.2 git push -u origin john-dev-2 -- push feature branch to remote repo
```

```
4.3 git pull origin john-dev-2 -- pull feature branch
```

```
4.4 git push origin :john-dev-2 -- delete the remote feature branch (see the git-scm page)
```

###5. Git Misc Commands
```
5.1 git diff-tree -r --root 40a450274b128348ec30d69abc51981ea7be20df -- see a full diff-tree
```

####6. Git Alias
```
Edit your ~/.gitconfig to add useful git aliases. see (Effective pull requests and other good practices for teams using github)
[alias]
    hist = log --color --pretty=format:\"%C(yellow)%h%C(reset) %s%C(bold red)%d%C(reset) 
    %C(green)%ad%C(reset) %C(blue)[%an]%C(reset)\" --relative-date --decorate
```

####7. Git troubleshooting
```
to debug problems with an HTTP proxy set the environmental variable GIT_CURL_VERBOSE=1
The ours merge technique to replace master
git checkout seotweaks
        git merge -s ours master  
        git checkout master  
        git merge seotweaks
```

####8. Git empty repository

You have an empty repository
To get started you will need to run these commands in your terminal.

Configure Git for the first time
```
git config --global user.name "John Doe"
git config --global user.email "johndoe@yahoo.com"
```
Working with your repository
I just want to clone this repository
If you want to simply clone this empty repository then run this command in your terminal.
```
git clone http:github.bryanshubo.git
```
My code is ready to be pushed
If you already have code ready to be pushed to this repository then run this in your terminal.
```
cd existing-project
git init
git add --all
git commit -m "Initial Commit"
git remote add origin http:github.bryanshubo.git
git push origin master
```

My code is already tracked by Git
If your code is already tracked by Git then set this repository as your "origin" to push to.
```
cd existing-project
git remote set-url origin http:github.bryanshubo.git
git push origin master
```
git diff --name-only --diff-filter=U
