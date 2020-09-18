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
