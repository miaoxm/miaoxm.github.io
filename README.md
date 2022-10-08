# Docsify
> docsify 可以快速生成文档网站
> 
> 只需要按照[**`快速开始`**](https://docsify.js.org/#/zh-cn/quickstart)生成文档网站需要的几个文件即可
> 
> 随后就可以开始编写文档并直接部署在[**`GitHub Pages`**](https://docsify.js.org/#/zh-cn/deploy)

# 快速开始
## 安装node环境
1. 下载安装包
```shell
https://nodejs.org/dist/v14.16.1/node-v14.16.1-linux-x64.tar.xz
```
2. 解压并放入指定的目录
```shell
xz -d node-v14.16.1-linux-x64.tar.xz
tar -xf node-v14.16.1-linux-x64.tar
mv node-v14.16.1-linux-x64 /usr/local/node
```
3. 建立软链接
```shell
ln -s /usr/local/node/bin/node /usr/local/bin
ln -s /usr/local/node/bin/npm /usr/local/bin
```
4. 配置淘宝镜像
```shell
npm config set registry https://registry.npm.taobao.org
```
5. 查看版本信息及镜像配置信息
```shell
npm -v
node -v
npm config get registry
```

## 快速开始
1. 全局安装
```shell
npm i docsify-cli -g
```
2. 初始化项目
```shell
docsify init ./docs
```
如果提示找不到 **`docsify`** 命令，在node的安装目录下 **`/usr/local/node/bin`** 目录下找到 **`docsify`**，将其变为全局命令，建立以下软链接 **`ln -s /usr/local/node/bin/docsify /usr/local/bin`**

3. 启动本地服务
```shell
docsify serve docs
```
