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
create a build directory, call cmake and build

from the root directory call:
```
mkdir build
cd build
cmake ..
make -j16
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

## Version Bump
https://github.com/oxen-io/oxen-core/pull/1589/commits/ca5de63dbfbb09777d46e56d0bb98d2515ca30ec

## Linux Build

build:
```
cd loki-core
mkdir build
cd build
cmake -DCMAKE_BUILD_TYPE=Debug -DBUILD_TESTS=ON ..
make -j$(nproc)
```

## Windows cross compile build
If you want to do a windows build from your local linux box, install g++-mingw-w64-x86-64, and then build with
```
cmake -DCMAKE_TOOLCHAIN_FILE=../cmake/64-bit-toolchain.cmake -DBUILD_STATIC_DEPS=ON -DARCH=x86-64
```

## Set up service node
```
ExecStart=/home/snode/loki/lokid --non-interactive --service-node --service-node-public-ip SERVERIP --storage-server-port 23023
ExecStart=/home/snode/loki-storage 0.0.0.0 23023 --lokid-rpc-port 22023 --lokid-key  /home/snode/.loki/key
```

## Lokinet ping
```
/utils/lmq-rpc.py ipc://$HOME/.loki/testnet/lokid.sock 'admin.lokinet_ping' '{"version":[0,8,3]}'
```

## SS ping
```
/utils/lmq-rpc.py ipc://$HOME/.loki/testnet/lokid.sock 'admin.storage_server_ping' '{"version_major":2,"version_minor":1,"version_path":1}'
```

## Download Blockchain
use in tmux so it can download while you are not sshd in
```
sudo oxend-download-lmdb https://public.loki.foundation/loki/data.mdb
OR
sudo -u _loki curl https://public.loki.foundation/loki/data.mdb --output /var/lib/oxen/lmdb/data.mdb
```

## Compile Tests Faster
```
cmake .. -DBUILD_TESTS=ON -DCMAKE_BUILD_TYPE=Debug -DUSE_LTO=OFF
```
