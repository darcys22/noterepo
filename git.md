## Git

Initial Cloning
https://stackoverflow.com/questions/67699/how-to-clone-all-remote-branches-in-git

### Clone Repo
```
git clone https://github.com/darcys22/loki-core.git loki_source
```

list all remote branches
```
git branch -a
```

checkout dev
```
git checkout origin/dev
```

create new branch for dev after checking out remote branch
```
git checkout dev
```
### Add upstream sources
View current sources
```
git remote -v
```

Add new source:
```
$ git remote add upstream https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git
git remote add upstream https://github.com/loki-project/loki-core.git
```
### New Branch

create the new branch whilst on dev
```
git checkout -b pull-request-name
```

### Delete after pull request merged
```
git push -d <remote_name> <branch_name>
git branch -d <branch_name>
```

### Pull upstream changes
```
git checkout dev

$ git pull https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git BRANCH_NAME
git pull upstream/dev dev

git pull upstream dev

```

### Pull upstream branch changes
From within the branch you are working on 
```
git checkout pull-request-name
git pull origin dev
```

### Compare two files not in a repo
```
git diff --no-index --word-diff old_file.txt new_file.txt
```

### Compare branch to original branch that would show in github pull request
Use triple dot syntax between branches
```
git diff dev...hotfix-branch
```

### Clean up commit series 
When I’m happy with the functionality in my local branch. When the bug seems to be fixed or the feature seems to be doing what it’s supposed to do and the test suite runs fine locally.

I then clean up the commit series with `git rebase -i` (or if it is a single commit I can instead use just `git commit --amend`).

### List all commits on branch
```
git cherry -v dev hotfix-branch
```

### Checkout Pull Requests from Github
Fetch the reference to the pull request based on its ID number, creating a new branch in the process. Branchname can be be anything you want (Not dependant on PR details)
```
$ git fetch origin pull/ID/head:BRANCHNAME
```
Switch to the new branch that's based on this pull request:
```
[main] $ git checkout BRANCHNAME
> Switched to a new branch 'BRANCHNAME'
```

### View Coworkers gits
```
git remote add coworker git://coworkersUsername/repo.git
git fetch coworker 
git branch --all # choose a branch
git checkout --track -b aBranch coworker/aBranch
```

### Rebase and Squash 

- Make sure your branch is up to date with the master branch.
```
git fetch upstream
git rebase dev
```
- Run git rebase `-i master`.
- You should see a list of commits, each commit starting with the word "pick".
- Make sure the first commit says "pick" and change the rest from "pick" to "squash". -- This will squash each commit into the previous commit, which will continue until every commit is squashed into the first commit.
- Save and close the editor.
- It will give you the opportunity to change the commit message.
- Save and close the editor again.
- Then you have to force push the final, squashed commit: `git push --force-with-lease origin`.
