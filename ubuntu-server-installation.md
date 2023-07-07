## 在Ubuntu服务器上安装MatterMost服务器的过程记录

安装环境Ubuntu 22.04
1、操作系统升级
```
  sudo apt update
  sudo apt upgrade
```
2、安装postgresql
```
  sudo apt install postgresql
```
  创建数据库：
  ```
    sudo -u postgres psql
    postgres=# CREATE DATABASE mattermost;
    postgres=# CREATE USER mmuser WITH PASSWORD 'mmuserpassword';
    postgres=# GRANT ALL PRIVILEGES ON DATABASE mattermost to mmuser;
               GRANT USAGE, CREATE ON SCHEMA PUBLIC TO mmuser;
    postgres=# \q
  sudo systemctl restart postgresql
  sudo vi /etc/postgresql/{version}/main/pg_hba.conf
```
  修改：
  ```
    local   all             all                                     peer
    host    all             all             127.0.0.1/32            scram-sha-256
    host    all             all             ::1/128                 scram-sha-256
```
  为：
  ```
    local   all             all                                     trust
    host    all             all             127.0.0.1/32            trust
    host    all             all             ::1/128                 trust
```
  sudo systemctl reload postgresql

3、下载mattermost，并解压
```
  wget https://releases.mattermost.com/7.10.3/mattermost-7.10.3-linux-amd64.tar.gz
  tar -xvzf mattermost*.gz
  sudo mv mattermost /opt
  sudo mkdir /opt/mattermost/data（目录下存放聊天数据）
  sudo useradd --system --user-group mattermost
  sudo chown -R mattermost:mattermost /opt/mattermost
  sudo chmod -R g+w /opt/mattermost
  sudo touch /lib/systemd/system/mattermost.service
  sudo vi /lib/systemd/system/mattermost.service，以下是文件内容，输入后保存文件

  [Unit]
  Description=Mattermost
  After=network.target
  After=postgresql.service
  BindsTo=postgresql.service

  [Service]
  Type=notify
  ExecStart=/opt/mattermost/bin/mattermost
  TimeoutStartSec=3600
  KillMode=mixed
  Restart=always
  RestartSec=10
  WorkingDirectory=/opt/mattermost
  User=mattermost
  Group=mattermost
  LimitNOFILE=49152

  [Install]
  WantedBy=multi-user.target

  sudo systemctl daemon-reload
  sudo cp /opt/mattermost/config/config.json /opt/mattermost/config/config.defaults.json
  sudo vi /opt/mattermost/config/config.json, 编辑config.json文件：
    "SiteURL": "https://www.wochat.org",
    "DriverName": "postgres",
    "DataSource": "postgres://mmuser:mmuserpassword@localhost/mattermost?sslmode=disable\u0026connect_timeout=10\u0026binary_parameters=yes",
```
  sudo systemctl start mattermost，启动mattermost
  
  在/opt/mattermost/logs/mattermost.log中，如果有:"Server is listening on [::]:8065","caller":"app/server.go:971","address":"[::]:8065"}，则说明安装成功，如果没有请排查错误。
  
  systemctl enable mattermost.service，开机自启动。

4、mattermost初步安装完成，通过http://www.wochat.org:8065可以初步访问mattermost

5、允许用户注册
  System Control->AUTHENTICATION->Signup->Enable Open Server->true
  
## https配置，包含音频通话的配置

编辑/opt/mattermost/config/config.json，保存修改
```
  "SiteURL": "https://www.wochat.org",
  "ListenAddress": ":443",
  "ConnectionSecurity": "TLS",
  "UseLetsEncrypt": true,
  "Forward80To443": true,
```
允许mattermost绑定1024以下端口，否则报没有权限绑定443端口
```
  sudo setcap cap_net_bind_service=+ep /opt/mattermost/bin/mattermost
```
重新启动服务
```
  sudo systemctrl restart mattermost.service
```
音频通话，需要打开如下端口
- 入站：tcp 80 443 8045，udp 8443
- 出站：udp 3478

