# frpc-in-docker是什么
利用Docker快速部署Frpc

> 更新时间 2022-10-29

# 使用说明

# 安装Docker
```bash
#国外机
wget -qO- https://get.docker.com/ | sh 

#国内机
curl -sSL https://get.daocloud.io/docker | sh 
```


# 抽取镜像
```bash
docker pull ruiny/frpc
```

frps的0.17.0和0.24.1两个版本和下个版本不兼容，如果需要可以pull这两个镜像，一般情况用上面这个命令就行
```bash
docker pull ruiny/frpc:0.24.1
docker pull ruiny/frpc:0.17.0
```

## 添加frps.ini配置文件
```bash
rm -rf /var/frp && \
mkdir /var/frp && \
mkdir /var/frp/conf && \
cd /var/frp/conf && \
wget https://raw.githubusercontent.com/ruinny/frpc-in-docker/master/frpc.ini && \
chmod +x frpc.ini
```

#### 根据需要修改配置文件
`nano /var/frp/conf/frpc.ini` 


## 启动镜像（docker run方式）
```bash
docker run --name frpc --restart=always -d --network host \
-v /var/frp/conf/frpc.ini:/var/frp/conf/frpc.ini \
ruiny/frpc
```

> 说明
 - 配置文件存放在/var/frp/conf
 - 只适用于x64，不适用于arm

