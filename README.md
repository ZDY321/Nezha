> 哪吒面板V0 & 魔改主题的备份

### 后台安装
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
2. 运行安装脚本
~~~bash
curl -L https://raw.githubusercontent.com/naiba/nezha/master/script/install.sh  -o nezha.sh && chmod +x nezha.sh && sudo ./nezha.sh
~~~
> V0版本先选择n，之后在选择1

### 安装魔改主题
~~~yaml
使用上面的docker-compose方法安装时：

1.template里面的文件放到服务端/opt/nezha/dashboard/resource/template/theme-custom目录里面

2.static里面的文件放到服务端/opt/nezha/dashboard/resource/static/custom目录里面

2.重启哪吒面板服务

3.在哪吒面板后台主题选择Custom(local)

4.将 自定义代码.txt 里面的内容复制到哪吒面板后台的“自定义代码”文本框里

~~~
