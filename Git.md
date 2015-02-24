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
3.2.1 Various ways to check your working tree
git diff            //changes in the working tree not yet staged for the next commit
git diff --cached   //Changes between the index and your last commit; 
                    //what you would be committing if you run "git commit" without "-a" option.
git diff HEAD       //Changes in the working tree since your last commit; 
                    //what you would be committing if you run "git commit -a"
git diff --stated  //show the change you just staged;
```
```
3.2.2 Comparing branches
git diff topic master    //Changes between the tips of the topic and the master branches.
git diff topic..master   //Same as above.
git diff topic...master  //Changes that occurred on the master branch since when the topic branch was started off it.
```
#####3.3 git add
```
 git add <file.name>  //start tracking file.name
 git add -A  //stages All (modified, deleted, untracted, and new files);
 git add -u  //stages modified and deleted, without new;
 git add . //stages new and modified, without deleted;
```

#####3.4 git reset
```
git reset HEAD [file.name] //unstage a single file
git reset --hard HEAD //undo commits permanently, reset your local branch to the HEAD commit 
git reset --soft //undo a commit, does not touch the index file or the working tree at all, \
                 //but resets the head to <commit>
```

#####3.5 git rm
```
git rm --cached //remove file from the index but not working dir
git rm $(git ls-files --deleted) // With red color(--deleted files), "git add -A". 
                                 //Deleted files become green color. Then "git commit -m 'delete files'"
```  

####4. Branching and Merging
#####4.1 git branch
```
git branch // list local branches
git branch [branch_name] //create a new branch
git branch -d [branch_name] //delete a branch (locally !!!)
                            //The branch must be fully merged in its upstream branch, or in HEAD if no upstream was set with                             //-track or --set-upstream.
git branch -D [branch_name] // delete a branch irrespective of ites merged status.                            
git branch -r //view available local remote branches
git branch -vv //view the tracking branch
git branch -a //List both remote-tracking branches and local branches
git branch -u //setup upstream
git branch --contains [<commit>] //Only list branches which contain the specified commit (HEAD if not specified). 
                                 //Implies --list.
git branch --merged [<commit>] //Only list branches whose tips are reachable from the specified commit 
                               //(HEAD if not specified). Implies --list.
git branch --no-merged [<commit>] //Only list branches whose tips are not reachable from the specified commit 
                                  //(HEAD if not specified). Implies --list.
```
#####4.2 git checkout
```
git checkout [file_name] // Discard changes in working directory
git checkout [branch_name] // switch to a new branch
git checkout master  // switch to master branch
git checkout -b [branch_name]// Create a new branch named [new_branch] and start it at [start_point]
git checkout -B [branch_name]// Creates the branch <new_branch> and start it at <start_point>; 
                //if it already exists, then reset it to <start_point>.
git checkout -b [branch_name] master // create a new branch and start it at master                
git checkout --track origin/serverfix // change the tracking branch                

```

#####4.3 git merge
```
git merge [branch_name]  // merge [branch_name] into master
git merge [branch_name] --commit // Perform the merge and commit the result.
git merge [branch-name] --no-commit // perform the merge but pretend the merge failed and do not autocommit, to give the user                                     // a chance to inspect and further tweak the merge result before committing.
git merge --abort // only works when there are conflicts for git merge

```
```
3.4 

git push origin --delete <branchName>  -- delete a remote branch
or git push origin :<branchName>
git push  -- commit master
```
  
```
```
3.6 git clean -f -X -d -- remove all unstaged files (great for cleaning up after a build)
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
