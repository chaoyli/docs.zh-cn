# dev-env image 使用说明

## starrocks 与 image 对应关系

| starrocks                 | image tag                     |
| ------------------------- | ------------------------------|
| main                      | starrocks/dev-env:main        |
| branch-2.2/tags-2.2.*     | starrocks/dev-env:branch-2.2  |
| branch-2.1/tags-2.1.*     | starrocks/dev-env:branch-2.1  |
| branch-2.0/tags-2.0.*     | starrocks/dev-env:branch-2.0  |
| branch-1.19/tags-1.19.*   | starrocks/dev-env:branch-1.19 |

## image 下载

```shell
# 从 dockerhub 上下载 image
docker pull starrocks/dev-env:{branch-name}
```

## 通过Docker编译

- 挂载本地盘（建议使用）

  ```shell
  mkdir {local-path} && cd {local-path}

  git clone https://github.com/StarRocks/starrocks.git
  cd starrocks && git checkout {branch-name}

  docker run -it -v /{local-path}/.m2:/root/.m2 -v /{local-path}/starrocks:/root/starrocks --name {container-name} -d starrocks/dev-env:{version}
  docker exec -it {container-name} /root/starrocks/build.sh
  ```

- 不挂载本地盘

  ```shell
  docker run -it --name {container-name} -d starrocks/dev-env:{version}
  docker exec -it {container-name} /bin/bash
  
  git clone https://github.com/StarRocks/starrocks.git
  cd starrocks && git checkout {branch-name}
  
  ./build.sh
  ```

## 三方工具

image 内集安装的三方工具

- llvm
- clang
