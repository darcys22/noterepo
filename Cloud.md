```
sudo apt update && sudo apt upgrade
sudo apt dist-upgrade && sudo apt autoremove
sudo apt-get install curl git vim wget tmux

ssh-keygen -t ed25519 -C “darcys22@gmail.com”
eval `ssh-agent -s`
ssh-add ~/.ssh/id_ed25519
cat ~/.ssh/id_ed25519.pub

// git clone git@github.com:darcys22/dev.git
git clone https://github.com/darcys22/dev.git

ln -s ~/dev/dotfiles/vimrc .vimrc
ln -s ~/dev/dotfiles/tmux.config .tmux.conf
ln -s ~/dev/vim/ .vim

mkdir ./.config/nvim
ln -s ~/dev/nvim/init.vim ~/.config/nvim/init.vim

sudo apt-get install build-essential openssl curl git-core zlib1g zlib1g-dev libssl-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt-dev autoconf libc6-dev ncurses-dev automake libtool bison subversion pkg-config cmake libsodium-dev libgmp-dev libcurl4-openssl-dev

```
