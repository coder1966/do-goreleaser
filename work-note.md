# GoReleaser 使用

##  GoReleaser 介绍
   goreleaser 是一个方便的 go 二进制包分发工具。可以帮助我们进行go 二进制包的快速，简单分发。
   
   我们可以用来创建一个项目，打包成不同格式，一键发布到 github、gitlib、gitea 。

   我们可以把项目一键打包等 docker镜像，发布到 docker.io、gcr.io 。

## 安装 
   go install github.com/goreleaser/goreleaser@latest

   或

   sudo snap install --classic goreleaser

## 创建 go 项目
   略

## 项目发布
### 添加goreleaser 支持 创建 .goreleaser.yaml
   goreleaser init

### 检测 .goreleaser.yaml
   goreleaser check

### 本地测试构建
   goreleaser --snapshot --skip-publish --rm-dist

### 准备发布，设置 ENV github token 
   export GITHUB_TOKEN="YOUR_GITHUB_TOKEN"
### 创建 tag
   git tag -a v0.1.0 -m "First release"

### Docker 相关
####  创建 Makefile
   ```
      FROM scratch
      COPY YOUR_BINARY_NAME /app
      ENTRYPOINT ["/app"]  
   ```
#### 文件 .goreleaser.yaml 加上
   ```
   dockers:
     - image_templates:
       - "docker.io/YOUR_DOCKER_IO_NAME/YOUR_IMG_NAME:{{ .Version }}-amd64"
       # - "docker.io/YOUR_DOCKER_IO_NAME/YOUR_IMG_NAME:{{ .Version }}-arm64v8" 
   ```
#### 可能用到的 DOCKER 指令
   ```
   显示: docker images
   清空: docker system prune -a
   执行: docker run YOUR_IMG_NAME:VERSION
   推送：docker push YOUR_IMG_NAME:VERSION
   登录：docker login --username=YOUR_NAME
   ```  
## 发布到 github && docker.io
   goreleaser release --rm-dist

## 软件构建
### 多平台的二进制 + tar 包
### 多平台的 Docker 镜像
### 多操作系统的 FPM 包
https://goreleaser.com/customization/nfpm/
### 可选）Homebrew 的安装包

1.   ## 发布到 https://hub.docker.com/
https://goreleaser.com/customization/docker/
http://www.idmiss.com/701   (不含docker)

#### 构建以下图像并将其发布到docker.io和gcr.io：
https://goreleaser.com/customization/docker/?h=docker



docker tag coder1966/test01/goreleaser coder1966/test01:77

```
docker tag tomcat poloyy/tomcat:77
给需要上传的镜像重新打一个 tag，来说下重点
可套用的公式其实是： docker tag 需要上传的镜像[:TAG] [docker hub自己注册的账号名]/镜像名[:TAG]
 tomcat ：待上传的镜像名，可以指定 TAG
 poloyy ：就是我 Docker hub 的账号，这里换成自己的账号即可
 poloyy/tomcat:77 ：意味生成在 poloyy 账号下的 tomcat 仓库，并且打了个 77 标签

```

## 推送 yaml wget 等仓库

## GoReleaser 可以创建macOS 通用二进制文件- 也称为胖二进制文件
https://goreleaser.com/customization/universalbinaries/
## ubuntu20.04配置docker代理
https://www.jianshu.com/p/82f6cf124805

###  镜像 命名
https://hub.docker.com/_/golang/tags
##  github actions
https://goreleaser.com/ci/actions/

##  通过 Github Actions 部署 Mkdocs 文档

https://cloud.tencent.com/developer/article/1935771

### 本地文档书写、调试
#### 安装 Mkdocs 以及 Mkdocs 主题
pip install --user mkdocs mkdocs-material
#### 创建并测试站点
通过 mkdocs new <目录> 就可以快速创建文档站点。目录里会生成 mkdocs.yml 文件和docs目录，目录内有默认的index.md文件，你可以修改和增加文件。
#### 发行
<目录> 里 mkdocs serve

## 国际化网站，多语言下拉选择

例如： https://github.com/aws/copilot-cli/tree/mainline/site/content/docs

效果： https://aws.github.io/copilot-cli/ja/

参考案例： https://gitlab.com/mkdocs-i18n/mkdocs-i18n/-/blob/main/mkdocs.yml

### 多语言实施

本地安装 pip3 install mkdocs-i18n，否则 mkdocs serve 受影响。

.github/workflows/rmkdocs_actions.yml 文件加上引用 mkdocs-i18n

      `- run: pip install mkdocs-material mkdocs-awesome-pages-plugin mkdocs-section-index mkdocs-i18n`

mkdocs.yml 文件，参考 demo 写。每个语言一个文件，XXX.zh.md XXX.md XXX.jp.md 就可以。i18n 可以选择正确的显示出来。

## action 发版

【项目】--》【Settings】==》【Secrets】==》【action】==》【New repository secret】==》【Name=BOT_GITHUB_TOKEN】【Secret=我账户下生成的】
### 打tig

【主要页面】==》【Releases】==》【Draft a new Releases】==>选 旧tag==》v1.1.1【title = V1.1.1 (2022-11-04)】==>发布


## GITHUB FLOW

https://github.com/selfteaching/the-craft-of-selfteaching/issues/67    


