# Ubuntu14.04 安装 gitlab

### 安装vim

```python
# Install vim and set as default editor
# 新系统先更新
sudo apt-get update
sudo apt-get install -y vim
sudo update-alternatives --set editor /usr/bin/vim.basic
```

### 安装git(源码编译)

```python
# Install dependencies
sudo apt-get install -y libcurl4-openssl-dev libexpat1-dev gettext libz-dev libssl-dev build-essential

# Download and compile pcre2 from source
curl --silent --show-error --location https://ftp.pcre.org/pub/pcre/pcre2-10.33.tar.gz --output pcre2.tar.gz
tar -xzf pcre2.tar.gz
cd pcre2-10.33
chmod +x configure
./configure --prefix=/usr --enable-jit
make
sudo make install

# Download and compile from source
cd /tmp
curl --remote-name --location --progress https://www.kernel.org/pub/software/scm/git/git-2.21.0.tar.gz
echo '85eca51c7404da75e353eba587f87fea9481ba41e162206a6f70ad8118147bee  git-2.21.0.tar.gz' | shasum -a256 -c - && tar -xzf git-2.21.0.tar.gz
cd git-2.21.0/
./configure --with-libpcre
make prefix=/usr/local all

# Install into /usr/local/bin
sudo make prefix=/usr/local install

# When editing config/gitlab.yml (Step 5), change the git -> bin_path to /usr/local/bin/git
```

### 安装邮件服务器

```python
# 安装(安装Postfix期间选择 'Internet Site' )
sudo apt-get install curl openssh-server ca-certificates postfix
   
### 邮箱设置
   
# 卸载
apt-get purge postfix
```
![youxiang](https://github.com/DeerKing007/Ubuntu/blob/master/pic/youxiang.png)

### 添加并安装GitLab包

```python
>>>curl -sS http://packages.gitlab.cc/install/gitlab-ce/script.deb.sh | sudo bash
>>>sudo apt-get install gitlab-ce
>>>下载的版本安装命令如下：sudo dpkg –i gitlab-ce.deb
出现如下图表示安装成功

```
![gitlab](https://github.com/DeerKing007/Ubuntu/blob/master/pic/gitlab.png)


### **修改gitlab配置**

```python
>>>sudo vim /etc/ gitlab/gitlab.rb
```
![gitlab](https://github.com/DeerKing007/Ubuntu/blob/master/pic/seting01.png)
![gitlab](https://github.com/DeerKing007/Ubuntu/blob/master/pic/seting02.png)
![gitlab](https://github.com/DeerKing007/Ubuntu/blob/master/pic/seting03.png)
![gitlab](https://github.com/DeerKing007/Ubuntu/blob/master/pic/seting04.png)

```python
>>>sudo gitlab-ctl reconfigure   #重新启动

```
![gitlab](https://github.com/DeerKing007/Ubuntu/blob/master/pic/seting05.png)



### 在浏览器访问GitLab主机名

```python
# 如果安装gitlab的linux主机IP是192.168.0.10或者ubuntu(ubuntu为gitlab服务器的名字)，就在浏览器中输入192.168.0.10或者http://ubuntu，刷新一次，会让输入新的root密码。登录成功。
```
![gitlab](https://github.com/DeerKing007/Ubuntu/blob/master/pic/gitlabok.png)

** FQA **

```python
# 502 Whoops, GitLab is taking too much time to respond
修改/etc/gitlab/gitlab.rc里面  unicorn['port'] = 11011。
端口被占用可以命令强制杀死 sudo fuser -k -n tcp 11011。
高版本此项不需要配置


# 忘记管理员账户密码

```python
# 进入控制台，因为默认登陆邮箱是无用的
sudo gitlab-rails console production

# 进入控制台后查询用户1的信息
user = User.where(id: 1).first

# 修改密码。
u.password=12345678
u.password_confirmation=12345678

# 保存信息。
user.save!

```

```

