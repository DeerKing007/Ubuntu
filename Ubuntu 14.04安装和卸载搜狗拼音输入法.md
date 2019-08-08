# Ubuntu 14.04安装和卸载搜狗拼音输入法

## 安装

### 添加fcitx的PPA

```python
sudo add-apt-repository ppa:fcitx-team/nightly
sudo apt-get update
sudo apt-get install im-config
sudo apt-get -f install
```

### 官网下载 
[sogou pinyin](http://pinyin.sogou.com/linux/?r=pinyin)

### 安装sogoupinyin*.deb

```python
# 注意可能会安装失败 再执行一次 sudo apt-get -f install即可
sudo dpkg -i sogoupinyin_2.0.0.0068_amd64.deb

sudo im-config -s fcitx -z default

sudo reboot
```





## 卸载

### 查看

```python
sudo dpkg -l so*
```

### 卸载sogou pinyin

```python
sudo apt-get purge sogoupinyin
```

### 卸载fcitx

```
sudo apt-get purge fcitx
sudo apt-get autoremove
sudo reboot
```

重启命令可用注销代替 
无法注销时可执行下面命令

```python
sudo pkill Xorg
```