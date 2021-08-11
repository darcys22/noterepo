## Neovim
https://launchpad.net/~neovim-ppa/+archive/ubuntu/unstable

```
sudo add-apt-repository ppa:neovim-ppa/unstable
sudo apt-get update
sudo apt install neovim

sudo update-alternatives --install $(which vim) vim $(which nvim) 10
sudo update-alternatives --config vim


sh -c 'curl -fLo "${XDG_DATA_HOME:-$HOME/.local/share}"/nvim/site/autoload/plug.vim --create-dirs \
       https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim'
```
