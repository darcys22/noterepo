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
```
