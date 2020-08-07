# ubuntu18 部署flask

### 更新系统环境

```bash
sudo apt update
sudo apt install python3-pip python3-dev build-essential libssl-dev libffi-dev python3-setuptools
```

### 创建Python3虚拟环境

```bash
sudo apt install python3-venv
python3.6 -m venv testenv
source testenv/bin/activate
```

### 设置flask应用

```bash
pip install -r requirements.txt

# 设置uWSGI
pip install uwsgi flask
sudo ufw allow 5000 #启动防火墙，允许5000端口被访问
uwsgi --socket 0.0.0.0:5000 --protocol=http -w 模块名(减去.py扩展名):app #测试uWSGI是否可以正常运行

# 配置nginx代理
sudo apt-get install nginx
sudo rm /etc/nginx/sites-available/default
sudo vim /etc/nginx/sites-available/default 

server {
    listen 80;
    server_name xxx.xxx.xxx.xxx;    # 公网ip

    location /{
        proxy_pass http://127.0.0.1:5000; }
}
```

### 启动flask

```bash
gunicorn -w 3 -b 127.0.0.1:5000 main:app
或
python server.py
```

