sudo apt-get update
sudo apt-get install curl git vim

ssh-keygen -t rsa -C “darcys22@gmail.com”
ssh-add id_rsa
cat ~/.ssh/id_rsa.pub

git clone git@github.com:darcys22/dev.git

ln -s ~/dev/dotfiles/vimrc .vimrc
ln -s ~/dev/dotfiles/tmux.config .tmux.conf
ln -s ~/dev/vim/ .vim

sudo apt-get install build-essential openssl curl git-core zlib1g zlib1g-dev libssl-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt-dev autoconf libc6-dev ncurses-dev automake libtool bison subversion pkg-config
