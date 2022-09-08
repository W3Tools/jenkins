# W3Tools jenkins

## 1. 构建镜像
```
docker-compose build
```

## 2. 启动镜像
```
docker-compose up -d 
```

## 3. 查看jenkins初始密码(过滤出来的日志, 密码在匹配行的上两行)
```
docker-compose logs -f | grep -3a "initialAdminPassword"
```

## 4. 开始使用页面....

## 5. 手动构建pipeline使用的镜像(可选)
```
docker-compose exec jenkins bash # 进入jenkins容器
cd dockerfile # 切换到容器里存放dockerfile的目录
docker build . -f w3tools-awscli -t w3tools-awscli:latest  # 在容器里构建awscli镜像
docker build . -f w3tools-node -t w3tools-node:latest  # 在容器里构建node环境镜像
```
#### 构建完成后, 在pipeline文件里面可以修改成手动构建的两个镜像. 也可以使用public镜像w3tools/w3tools-node18:latest和w3tools/w3tools-awscli:latest