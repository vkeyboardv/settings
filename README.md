# Settings
Personal settings

## fish (git status)
```bash
sudo apt install fish
chsh -s /usr/bin/fish # set as a default

~/.config/fish/config.fish:
# fish git prompt
set __fish_git_prompt_showdirtystate 'yes'
set __fish_git_prompt_showstashstate 'yes'
set __fish_git_prompt_showupstream 'yes'
set __fish_git_prompt_color_branch yellow

# Status Chars
set __fish_git_prompt_char_dirtystate '⚡'
set __fish_git_prompt_char_stagedstate '→'
set __fish_git_prompt_char_stashstate '↩'
set __fish_git_prompt_char_upstream_ahead '↑'
set __fish_git_prompt_char_upstream_behind '↓'
 
function fish_prompt
        set last_status $status
        set_color $fish_color_cwd
        printf '%s' (prompt_pwd)
        set_color normal
        printf '%s ' (__fish_git_prompt)
       set_color normal
end
```

## AWS CodeCommit SSH
```bash
ssh-keygen

# .ssh/config:
Host git-codecommit.*.amazonaws.com
  User APKAEIBAERJR2EXAMPLE
  IdentityFile ~/.ssh/codecommit_rsa

chmod 600 config
```

## NPM
```bash
sudo apt install npm
sudo npm install -g npm # npm@latest
```

## Node
```bash
sudo npm cache clean -f
sudo npm install -g n
sudo n stable # n latest or n #.#.# to get a specific version
```

## Git Credentials
```bash
git config user.name --global "Name"
git config user.email --global "email@email.com"
```

## Error: ENOSPC: System limit for number of file watchers reached
```bash
echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p
```

## Pretty log terminal
```bash
sudo apt-install pino-pretty
# *command* + | pino-pretty -t
```

## Redis Docker
```bash
docker run --name redis -p 6379:6379 -d redis
```

## Stop Node servers
```bash
killall node
```
or 

```bash
netstat -nlp | grep :8080 # kill *number* (-9 flag for force kill)
```

## ANDROID SDK for fish
```bash
# First :
 $ touch ~/.config/fish/config.fish; nano ~/.config/fish/config.fish

# Copy this in the file :

set --export ANDROID $HOME/Library/Android;
set --export ANDROID_HOME $ANDROID/sdk;
set -gx PATH $ANDROID_HOME/tools $PATH;
set -gx PATH $ANDROID_HOME/tools/bin $PATH;
set -gx PATH $ANDROID_HOME/platform-tools $PATH;

set --export JAVA_HOME /Applications/Android\ Studio.app/Contents/jre/jdk/Contents/Home;
set -gx PATH $JAVA_HOME/bin $PATH;
```

## Watchman for Ubuntu
```bash
git clone https://github.com/facebook/watchman.git
cd watchman
git checkout v4.9.0  # the latest stable release
sudo apt-get install libtool
sudo apt-get install pkg-config
./autogen.sh
./configure --without-python  --without-pcre --enable-lenient
make
sudo make install
```

## Deleting Old Local Branches
```bash
git remote prune origin 
git branch -vv | grep 'origin/.*: gone]' | awk '{print $1}' | xargs git branch -d
```

## Text Interface for Git
```bash
sudo apt install tig # then use <command> | tig
```

## Docker commands without sudo
```bash
cat /etc/group | grep docker # to check users in docker group
sudo gpasswd -a $USER docker
sudo usermod -a -G docker $USER # https://techoverflow.net/2017/03/01/solving-docker-permission-denied-while-trying-to-connect-to-the-docker-daemon-socket/
sudo service docker restart
```
