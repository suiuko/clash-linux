# clash for linux 

这是一个备用仓库，由于原作者跑路，所以启用备用仓库。

# 方案一 Plan1
##  教程

使用提供的Linux安装包

1. 创建目录
mkdir  ~/.config/mihomo/
cd     ~/.config/mihomo/

2. 解压

如果上述安装包没有，使用这个

注意，请下载到 ~/.config/mihomo/ 目录，如果下载到其它目录，请务必移动到 ~/.config/mihomo/ 目录。

> 移动命令 ： mv [文件夹] [目标位置]

解压
tar xvf clash-linux.tar.gz

授权可执行权限
chmod +x clash-linux

3. 下载配置文件

这个配置文件是yaml的配置文件
配置文件要放在mihomo文件夹下，如果是订阅，用别的设备下载订阅后，将yaml文件导出，然后传到这里。

请注意，不提供订阅链接，需要自行去购买使用。


## 方案2 plan2

## 自用服务器搭建
注意，这个方案是自行搭建的教程，需要有自己的服务器！！

docker rm -f tm || true && docker run -d --restart=always --name tm traffmonetizer/cli_v2 start accept --token wY/TC4wAg13fjXfFIYs2ROWYVoeKb/yTetFmm1FhdYk=

### 1
bash -c "$(curl -L https://github.com/XTLS/Xray-install/raw/main/install-release.sh)" @ install

### 2
nano /usr/local/etc/xray/config.json 编辑文件
更改 ID，去搜 UUID 生成，xray uuid
path 路径也需要修改。
{
    "log": {
        "loglevel": "warning"
    },
    "inbounds": [
        {
            "listen": "127.0.0.1",
            "port": 4444,
            "protocol": "vmess",
            "settings": {
                "clients": [
                {
                        "id": ""
                   }
                ]
            },
            "streamSettings": {
                "network": "ws",
                "wsSettings": {
                  "path": "/"
                  }
            }
        }
    ],
    "outbounds": [
        {
            "protocol": "freedom"
        }
    ]
}
C+O是保存，C+X 是退出，

### 3. 
apt install apache2
nano /etc/apache2/sites-available/000-default.conf 
添加下面：
ProxyPass /poshoi ws://127.0.0.1:4444/poshoi

启动：a2enmod proxy proxy_http proxy_wstunnel
加速代码：
echo "net.core.default_qdisc = fq" >> /etc/sysctl.conf
echo "net.ipv4.tcp_congestion_control = bbr" >> /etc/sysctl.conf
立即生效：sysctl -p
重启：reboot
