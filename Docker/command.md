# Image

## 下載 image

```shell
// 從官方 repository 下載
> docker pull ubuntu:latest

// 從其他 repository 下載
> docker pull dockerpool.com:5000/ubuntu:latest
```

## 列出本機 image

```shell
> docker images
```

## 建立 image

### 修改現有的 image

```shell
// 新建並啟動 container
> docker run -t -i ubuntu:latest /bin/bash

// 修改 container 內容
root@fdf163bad713:/# apt install php php-cli

// 離開 container
root@fdf163bad713:/# exit

// 建立 image
> docker commit -m "Added php" -a "Greasy Owl" fdf163bad713 ubuntu:php
-m: commit的訊息
-a: commit的使用者
```

### 使用 Dockerfile

```shell
// Dockerfile 建立完成後，建立 image
> docker build -t="ubuntu:php" .
* . 代表 Dockerfile 所在的路徑
```

## 移除 image

```shell
> docker rmi ubuntu:php
* 在移除 image 之前，要先移除依賴於這個 image 的所有 container
```
