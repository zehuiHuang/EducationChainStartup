# Certification链启动脚本

## 搭建步骤

### 安装Parity
* 可以去官网下载发布版安装包 https://www.parity.io/
* Parity github源码中也有多种安装方式 https://github.com/paritytech/parity

安装完以后使用version查看是否安装成功
```
$ parity --version

Parity
  version Parity/v1.10.1-beta-45c29a2a5-20180413/x86_64-linux-gnu/rustc1.25.0
Copyright 2015, 2016, 2017, 2018 Parity Technologies (UK) Ltd
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

By Wood/Paronyan/Kotewicz/Drwięga/Volf
   Habermeier/Czaban/Greeff/Gotchac/Redmann

```

### 启动普通节点
打开 `shell.toml` 文件，该文件为节点的配置文件，注释掉mining中的以下这行
```
engine_signer = "0x035a274de01f0bd4a3e3c30a9d7c13a7911389df"
```
然后运行start即可
```
./start
```

### 启动Authority节点
接着上一步，主链在初始化的时候就预先生成了很多地址和私钥，并且写在了shell.json中，shell.json是区块链初始文件，一旦正式部署，则不可改变。
* 先在parity的ui中导入一个Authority节点的私钥
* 关闭parity节点
* 在`shell.toml`中取消engine_signer的注释，并把地址改为刚才导入的地址
* 在`password`文件中填入刚才导入钱包时输入的密码
* 重启钱包
然后节点久升级为Authority节点，并且会自动生成块.
** 注意 ** ：info.md中记录了相关钱包的私钥，千万不能外泄


## 其他功能

### 获取本节点的enode信息
```
./getennode
```
注意把节点末尾的ip改为服务器的外网ip后，其他在其他节点上才能生效。如果搭建了新的节点，可以在shell.toml的bootnodes中统一添加

### 重新获取ui的token
```
./getuitoken
```
