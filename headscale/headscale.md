# headscale

# 1、headscale

## 1.1 安装

```
# 参考链接：https://mp.weixin.qq.com/s/1oYqQaMH0VquOcINpXBUyg
1、下载安装包 # 可以把版本更换为最新
wget https://github.com/juanfont/headscale/releases/download/v0.16.4/headscale_0.16.4_linux_amd64 -O /usr/local/bin/headscale
2、加执行权限
chmod +x /usr/local/bin/headscale
3、配置目录
mkdir -p /etc/headscale
4、创建用户
useradd \
 --create-home \
 --home-dir /var/lib/headscale/ \
 --system \
 --user-group \
 --shell /usr/sbin/nologin \
 headscale
5、创建unit文件
/etc/systemd/system/headscale.service
6、写配置文件
/etc/headscale/config.yaml
7、启动
systemctl enable headscale --now
```

# 2、derp

## 2.1 安装

```
1、安装命令
go install tailscale.com/cmd/derper@main
2、配置命令
mv ${GOPATH}/bin/derper /usr/local/bin
3、创建用户
useradd \
        --create-home \
        --home-dir /var/lib/derper/ \
        --system \
        --user-group \
        --shell /usr/sbin/nologin \
        derper
4、创建unit文件
/etc/systemd/system/derp.service
5、写配置文件
/etc/headscale/derper.yaml
6、启动
systemctl enable derper --now
```



```
# 注意生成的密钥名称要和配置指定的名称一致
openssl genrsa -out headscale.suanleme.cn.key 2048
openssl req -new -key headscale.suanleme.cn.key -out headscale.suanleme.cn.csr -config openssl.cnf
openssl x509 -req -days 365 -in headscale.suanleme.cn.csr -signkey headscale.suanleme.cn.key -out headscale.suanleme.cn.crt -extensions req_ext -extfile openssl.cnf
```

