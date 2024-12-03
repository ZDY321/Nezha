> 哪吒面板V0 & 魔改主题的备份

### 后台面板安装
1. `docker-compose.yml`:
~~~yaml
# 魔改版
services:
  dashboard:
    image: ghcr.io/naiba/nezha-dashboard:v0.20.13
    container_name: nezha
    restart: always
    volumes:
      - ./data:/dashboard/data
      - ./theme-custom/static:/dashboard/resource/static/theme-custom:ro
      - ./dashboard-custom/static:/dashboard/resource/static/dashboard-custom:ro
      - ./theme-custom/template:/dashboard/resource/template/theme-custom:ro
      - ./dashboard-custom/template:/dashboard/resource/template/dashboard-custom:ro
    ports:
      - 8008:80
      - 5555:5555
~~~

`docker-compose up -d `

2. 运行面板安装脚本
~~~bash
curl -L https://raw.githubusercontent.com/naiba/nezha/master/script/install.sh  -o nezha.sh && chmod +x nezha.sh && sudo ./nezha.sh
~~~

当在线脚本失效时，使用`nezha0+1_install.sh`文件；将下载的文件放在`/root`,改名为`nezha.sh`之后运行`chmod +x nezha.sh && sudo ./nezha.sh`

> V0版本先选择n，之后在选择1

### 安装魔改主题

使用上面的docker-compose方法安装时：

1. template里面的文件放到服务端`/opt/nezha/dashboard/theme-custom/template`目录里面。
~~~plaintext
目录结构：
template/
│
├── header.html      # 网站头部组件
├── footer.html      # 网站底部组件
├── menu.html        # 导航菜单组件
├── home.html        # 首页模板
├── network.html     # 网络相关页面模板
├── service.html     # 服务页面模板
└── viewpassword.html # 查看密码页面模板
~~~

2. static里面的文件放到服务端`/opt/nezha/dashboard/static-custom/static`目录里面。
~~~plaintext
目录结构：
static/
└── head.png     # 头像图片
~~~

3. 运行`/root/data/docker_data/nezha/`下的`./nezha_v0.sh`
2.重启哪吒面板服务，docker版本用 `docker restart pid` ，独立安装用 `systemctl restart nezha-dashboard`

3.重启进入后台，在哪吒面板后台主题选择Custom(local)

4.将 自定义代码.txt 里面的内容复制到哪吒面板后台的“自定义代码”文本框里

~~~
