# 參考連結
- http://vinn.logdown.com/posts/2014/06/14/ubuntu-server-nginx-passenger-deploy
- Passenger documantation https://www.phusionpassenger.com/documentation_and_support

# 前置作業

## Add new user xxx
```
useradd -m username
passwd username
sudo adduser username sudo
```

## Basic tools
```
sudo apt-get update
sudo apt-get upgrade
```

### 一行裝全部
`sudo apt-get install build-essential zlib1g-dev libssl-dev libreadline-dev git zsh curl nodejs libv8-dev libsqlite3-dev ruby-dev`

### 或分開裝
```
sudo apt-get install build-essential zlib1g-dev libssl-dev
sudo apt-get install libreadline-dev
sudo apt-get install libreadline5-dev
sudo apt-get install git zsh curl
sudo apt-get install nodejs  (for JavaScript runtime)
sudo apt-get install libv8-dev
sudo apt-get install sqlite3 libsqlite3-dev
sudo apt-get install libreadline-dev
sudo apt-get install ruby-dev
sudo curl -L http://install.ohmyz.sh | sh
chsh -s /bin/zsh
git clone https://github.com/icarus4/icarus4.tools.git
```

## Install rbenv (github)
```
git clone https://github.com/sstephenson/rbenv.git ~/.rbenv
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.common_shell_rc
echo 'eval "$(rbenv init -)"' >> ~/.common_shell_rc
git clone https://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build
sudo apt-get install libbuilder-ruby
```

## Install Ruby
```
rbenv install 2.0.0-p481
rbenv global 2.0.0-p481
rbenv rehash
```

## Install RubyGem
```
git clone https://github.com/rubygems/rubygems.git
cd rubygems; sudo ruby setup.rb
sudo gem1.8 install rubygems-update
echo "install:  --no-rdoc --no-ri" >> ~/.gemrc
echo "update:  --no-rdoc --no-ri" >> ~/.gemrc
```

## Install Rails
```
gem install bundler
sudo gem install rails --version 4.0.5
rbenv rehash
```

## Install Nginx with Passenger support （by passenger-install-nginx-module）
### 安裝 Nginx
```
gem install passenger
sudo passenger-install-nginx-module
```

## 安裝執行script
```
cd /etc/init.d
sudo wget https://raw.github.com/chloerei/nginx-init-ubuntu-passenger/master/nginx
sudo update-rc.d nginx defaults
sudo chmod +x nginx
```

# 此區方法容易失敗，請參考 passenger-install-nginx-module 的安裝方式）Install Nginx with Passenger support ([reference](https://www.phusionpassenger.com/documentation/Users%20guide%20Nginx.html#install_on_debian_ubuntu))
## Adding Passenger APT repository
`sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 561F9B9CAC40B2F7`

## Add HTTPS support for APT.
`sudo apt-get install apt-transport-https ca-certificates`

## 新增檔案
`sudo touch /etc/apt/sources.list.d/passenger.list`

## 根據 Linux 版本不同，選擇其中一行加入/etc/apt/sources.list.d/passenger.list
```
##### !!!! Only add ONE of these lines, not all of them !!!! #####
# Ubuntu 14.04
deb https://oss-binaries.phusionpassenger.com/apt/passenger trusty main
# Ubuntu 12.04
deb https://oss-binaries.phusionpassenger.com/apt/passenger precise main
# Ubuntu 10.04
deb https://oss-binaries.phusionpassenger.com/apt/passenger lucid main
# Debian 7
deb https://oss-binaries.phusionpassenger.com/apt/passenger wheezy main
# Debian 6
deb https://oss-binaries.phusionpassenger.com/apt/passenger squeeze main
```

## Secure passenger.list and update your APT cache:
```
sudo chown root: /etc/apt/sources.list.d/passenger.list
sudo chmod 600 /etc/apt/sources.list.d/passenger.list
sudo apt-get update
```

## 安裝 Nginx with passenger-module
`sudo apt-get install nginx-extras passenger`

## 修改 /etc/nginx/nginx.conf
### 第一行加上：
`env PATH;`

### 拿掉 passenger_root 和 passenger_ruby 的註解
### 將 passenger_root 那行改成執行 `/usr/bin/passenger-config --root` 的結果（`/usr/bin` 是必要的）
ex:
`passenger_root /usr/lib/ruby/vendor_ruby/phusion_passenger/locations.ini;`

### 並將 passenger_ruby 那行改成 `rbenv which ruby` 的結果
ex:
```
passenger_ruby /home/xxxx/.rbenv/shims/ruby;
passenger_ruby /home/icarus4/.rbenv/versions/2.0.0-p481/bin/ruby;
```

## 為ruby添加passenger支援
`gem install passenger`

## Restart Nginx
`sudo service nginx restart`


# 修改 Nginx 設定檔

## 編輯 /opt/nginx/conf/nginx.conf，寫入以下內容：

### 第一行加上：
`env PATH;`

### server 設定：
```
server {
    listen 80 default;
    server_name example.com; # 這裡填寫你真實域名
    root /var/www/example.com/current/public;
    passenger_enabled on;
    rails_env development;
}
```

### 重啟 nginx：
`$ sudo service nginx restart`


# PostgreSQL
## Install PostgreSQL
```
sudo apt-get install libpq-dev
sudo apt-get install postgresql postgresql-contrib
```

## Setup PostgreSQL
- change password of postgres (default database user)
```
sudo -u postgres psql postgres
\password postgres
```

- create db
`sudo -u postgres createdb mydb`

- or create a superuser first then create db by the superuser
```
sudo -u postgres createuser --superuser username
createdb [db name] -O [username] -E UTF8 -e
```

# SSH 設定
- 細節參考 http://stackoverflow.com/questions/2643502/git-permission-denied-publickey
- 主要步驟如下
    - cd ~/.ssh && ssh-keygen
    - 到github 的 SSH 設定頁，貼上 id_rsa.pub 此檔案之值



# 自動化佈署: Mina
- 安裝 mina
`gem install mina`

- 在 project 根目錄底下輸入
`mina init`

- 修改設定檔 config/deploy.rb
```
set :deploy_to, '/var/www/project-name'
.
.
```
- 在 server 先 create 好要上傳的資料夾根目錄（deploy.rb 的 :deploy_to）
（資料夾權限可能也需要一併設定）

- 利用 mina 建立資料夾結構
`mina setup`

- 若此步驟卡在輸入密碼，則在deploy.rb加入這行
`set :term_mode, nil`

- 佈署
`mina deploy`

- 若佈署時出現以下錯誤，解決辦法是用 rbenv 安裝 1.9.3 版的 ruby
```
Your Ruby version is 1.9.3, but your Gemfile specified 2.0.0-p481
! ERROR: Deploy failed.
-----> Cleaning up build
$ rm -rf "$build_path"
Unlinking current
$ rm -f "deploy.lock"
```

- 並且在 deploy.rb 取消註解以下這行
`invoke :'rbenv:load'`

