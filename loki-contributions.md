## Download Sources 

**1) Fork the loki-core to your personal github repository**

**2) Click green clone/download button on your personal github to copy the repo to your clipboard**

**3) Git clone to your personal computer**
```
git clone https://github.com/darcys22/loki-core.git
```

**4) Install Dependencies**
```
git submodule update --init --recursive
```

**5) Change to dev branch**
Currently your local copy only has the master branch. View all the remote branches with `git branch -a`

View the remote dev branch
```
git checkout origin/dev
```

Now you can copy the remote dev branch to make edits
```
git checkout dev
```

**6) Compile the sources**
from the root directory call:
```
make
```

## Create a new branch to work on

**1) While on the dev branch create a new branch**
I am using pull-request-name as the name of the branch, this should be changed to reflect the actual changes being made
```
git checkout -b pull-request-name
```

**2) Make edits to source**

**3) Commit changes and push to origin (your github)**
```
git push origin pull-request-name
```

**4) Make pull request!**
There will be a green pull request button on the repo page of your personal github

**5) Make updates as necessary**
continue pushing with `git push origin pull-request-name` as you make changes and it will automatically be applied to the pull request

**6) When authors merge your request you will be able to delete the branch from your github and your local copy**
```
git push -d origin pull-request-name
git branch -d pull-request-name
```