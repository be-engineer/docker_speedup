镜像加速器
国内从 Docker Hub 拉取镜像有时会遇到困难，此时可以配置镜像加速器。国内很多云服务商都提供了国内加速器服务，例如：

网易云加速器 https://hub-mirror.c.163.com
百度云加速器 https://mirror.baidubce.com
阿里云加速器(需登录账号获取)
由于镜像服务可能出现宕机，建议同时配置多个镜像。各个镜像站测试结果请到 docker-practice/docker-registry-cn-mirror-test 查看。

国内各大云服务商均提供了 Docker 镜像加速服务，建议根据运行 Docker 的云平台选择对应的镜像加速服务，具体请参考官方文档。

本节我们以 网易云 镜像服务 https://hub-mirror.c.163.com 为例进行介绍。

Ubuntu 16.04+、Debian 8+、CentOS 7
对于使用 systemd 的系统，请在 /etc/docker/daemon.json 中写入如下内容（如果文件不存在请新建该文件）

{
  "registry-mirrors": [
    "https://hub-mirror.c.163.com",
    "https://mirror.baidubce.com"
  ]
}
注意，一定要保证该文件符合 json 规范，否则 Docker 将不能启动。

之后重新启动服务。

$ sudo systemctl daemon-reload
$ sudo systemctl restart docker
注意：如果您之前查看旧教程，修改了 docker.service 文件内容，请去掉您添加的内容（--registry-mirror=https://hub-mirror.c.163.com）。

Windows 10
对于使用 Windows 10 的用户，在任务栏托盘 Docker 图标内右键菜单选择 Settings，打开配置窗口后在左侧导航菜单选择 Docker Engine，在右侧像下边一样编辑 json 文件，之后点击 Apply & Restart 保存后 Docker 就会重启并应用配置的镜像地址了。

{
  "registry-mirrors": [
    "https://hub-mirror.c.163.com",
    "https://mirror.baidubce.com"
  ]
}
macOS
对于使用 macOS 的用户，在任务栏点击 Docker Desktop 应用图标 -> Perferences，在左侧导航菜单选择 Docker Engine，在右侧像下边一样编辑 json 文件。修改完成之后，点击 Apply & Restart 按钮，Docker 就会重启并应用配置的镜像地址了。

{
  "registry-mirrors": [
    "https://hub-mirror.c.163.com",
    "https://mirror.baidubce.com"
  ]
}
检查加速器是否生效
执行 $ docker info，如果从结果中看到了如下内容，说明配置成功。

Registry Mirrors:
 https://hub-mirror.c.163.com/
k8s.gcr.io 镜像
可以登录 阿里云 容器镜像服务 镜像中心 -> 镜像搜索 查找。

例如 k8s.gcr.io/coredns:1.6.7 镜像可以用 registry.cn-hangzhou.aliyuncs.com/google_containers/coredns:1.6.7 代替。

一般情况下有如下对应关系：

# $ docker pull k8s.gcr.io/xxx

$ docker pull registry.cn-hangzhou.aliyuncs.com/google_containers/xxx
云服务商
某些云服务商提供了仅供内部访问的镜像服务，当您的 Docker 运行在云平台时可以选择它们。

Azure 中国镜像 https://dockerhub.azk8s.cn

腾讯云 https://mirror.ccs.tencentyun.com
