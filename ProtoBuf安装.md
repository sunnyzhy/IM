# 安装 protocol buffers（ProtoBuf）

## 下载地址

[protobuf 官网下载](https://github.com/protocolbuffers/protobuf/releases 'protobuf 官网下载')

## 安装

1. 下载并解压，假如下载到 ```/usr/local```
   ```bash
   # wget https://github.com/protocolbuffers/protobuf/releases/download/v26.1/protoc-26.1-linux-x86_64.zip -P /root

   # cd /usr/local
   
   # unzip protoc-26.1-linux-x86_64.zip -d protoc
   ```

2. 配置环境变量
   ```bash
   # vim /etc/profile
   export PROTOC_HOME=/usr/local/protoc
   export PATH=$PATH:$PROTOC_HOME/bin
   
   # source /etc/profile
   
   # protoc --version
   libprotoc 26.1
   ```
