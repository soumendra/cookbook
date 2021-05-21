## Setting up python in a remote server

```python
sudo apt -y update
sudo apt -y upgrade
sudo apt -y install build-essential libsqlite3-dev sqlite3 bzip2 libbz2-dev zlib1g-dev libssl-dev openssl libgdbm-dev libgdbm-compat-dev liblzma-dev libreadline-dev libncursesw5-dev libffi-dev uuid-dev curl git

git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.8.1
echo -e ". $HOME/.asdf/asdf.sh" >> ~/.bashrc 
echo -e ". $HOME/.asdf/completions/asdf.bash" >> ~/.bashrc
source ~/.bashrc

asdf plugin add python
asdf install python 3.8.6
asdf global python 3.8.6
asdf reshim
```
