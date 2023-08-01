# xeno_rasa
Recommended:  [![Linzepore's Blog](https://img.shields.io/badge/xeno--rasa-v0.2.4-ffb02e.svg)](https://hub.docker.com/r/zepore/xeno_rasa)   

xeno nlu module developed by Xeno-onloaded Team.

## 配置Docker加速

编辑窗口内的JSON串，追加填写下方加速器地址：

```json
,
  "registry-mirrors": [
        "https://docker.mirrors.ustc.edu.cn"
    ]
```



## 通过 Docker Hub 拉取镜像

### 1.将模型放置在当前宿主机的挂载目录中

宿主机目录：`A:/Data_Docker/rasa_demo/xeno_data`

### 2.Windows拉取镜像

**xeno_rasa>=`v0.2.3`提供模型启动脚本**

```shell
#拉取镜像
docker pull zepore/xeno_rasa:[版本号]
# 创建容器
docker run -p 35005:5005 -u root --name=xeno_nlu -v [宿主机目录]:/[容器目录] -itd --privileged=true zepore/xeno_rasa:v0.2.4

### 例子
docker pull zepore/xeno_rasa:v0.2.4
docker run -p 35005:5005 -u root --name="xeno_nlu" -v A:/Data_Docker/rasa_demo/xeno_data:/xeno_data -itd --privileged=true zepore/xeno_rasa:v0.2.4
```

### 3.启动并容器，启动模型

```shell
# 检查启动情况
docker ps -a
# 启动
docker start xeno_nlu
# 进入容器同时启动模型
docker exec -it xeno_nlu bash [容器中模型路径]

### 例子
docker start xeno_nlu
docker exec -it xeno_nlu bash ./model_start.sh /xeno_data/nlu-xxxxxx.tar.gz
```

### 4.后台模式运行

同时按住`CTRL` + `Q` + `P`

### 5.脚本测试

在程序执行的时候需要手动启动脚本，便于程序运行

```
# 在 XenoPyScript.py 所在目录下执行
python XenoPyScript.py 我今天有关于办公室的日程吗?

# 正常输出
{'orderType': 'ContentQueryPlan', 'planContent': '办公室', 'timeDetected': ['2023-07-09 00:00:00', '2023-07-09 23:59:59']}
```



## 卸载XenoNLU

卸载容器：`docker rm -f xeno_nlu`

卸载镜像：`docker rmi -f zepore/xeno_rasa:v0.2.3`



## 通过阿里云Docker镜像仓库

### 1. 登录阿里云Docker Registry

```
$ docker login --username=[username] registry.cn-shenzhen.aliyuncs.com
```

用于登录的用户名为阿里云账号全名，密码为开通服务时设置的密码。

### 2. 从Registry中拉取镜像

```
$ docker pull registry.cn-shenzhen.aliyuncs.com/xeno_onloaded/xeno:[镜像版本号]
```
