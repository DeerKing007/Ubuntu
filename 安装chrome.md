# 安装chrome

### 以Ubuntu14.04 64位系统为例：

```markdown
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb

sudo dpkg -i google-chrome-stable_current_amd64.deb

sudo apt-get -f install
```

这三步走完chrome就已经安装到系统上了，但是就我现在的时间点（2017.11）来说，软件是装上了，点了图标之后根本打不开浏览器。

但是可以通过终端命令来打开软件：

```
google-chrome
```

问题所在：

```
chrome版本来说，这个NSS版本低了。 
```

### 升级NSS

```python
sudo apt-get install libnss3
```

