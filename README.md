I am honored that DARTNODE is offering a free server to sponsor my project.DARTNODE's official website:https://dartnode.com

![image](297966509-bda45b56-490a-4964-a782-6e0e70783d36.png)

ubuntu-18.04不能像ubuntu14一样通过编辑rc.local来设置开机启动脚本，通过下列简单设置后，可以使rc.local重新发挥作用。

# 建立rc-local.service文件

```javascript
sudo vi /etc/systemd/system/rc-local.service
```

# 将下列内容复制进rc-local.service文件

```javascript
[Unit]
Description=/etc/rc.local Compatibility
ConditionPathExists=/etc/rc.local
 
[Service]
Type=forking
ExecStart=/etc/rc.local start
TimeoutSec=0
StandardOutput=tty
RemainAfterExit=yes
SysVStartPriority=99
 
[Install]
WantedBy=multi-user.target
```


# 创建文件rc.local　　
```javascript
sudo vi /etc/rc.local
```


# 将下列内容复制进rc.local文件

```javascript
#!/bin/sh -e
#
# rc.local
#
# This script is executed at the end of each multiuser runlevel.
# Make sure that the script will "exit 0" on success or any other
# value on error.
#
# In order to enable or disable this script just change the execution
# bits.
#
# By default this script does nothing.
echo "看到这行字，说明添加自启动脚本成功。" > /usr/local/test.log
exit 0
```


# 给rc.local加上权限

```javascript
sudo chmod +x /etc/rc.local
```


# 启用服务
```javascript
sudo systemctl enable rc-local
```

# 启动服务并检查状态
```javascript
sudo systemctl start rc-local.service
sudo systemctl status rc-local.service
```

# 重启并检查test.log文件
```javascript
cat /usr/local/test.log
```
