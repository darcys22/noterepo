## Neovim
https://launchpad.net/~neovim-ppa/+archive/ubuntu/unstable

```
sudo add-apt-repository ppa:neovim-ppa/unstable
sudo apt-get update
sudo apt install neovim

sudo update-alternatives --install $(which vim) vim $(which nvim) 10
sudo update-alternatives --config vim
```
