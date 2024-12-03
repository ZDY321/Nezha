### 公开备注个性化

> [improve: status-server主题agent账单信息展示 by nap0o · Pull Request #425 · nezhahq/nezha](https://github.com/nezhahq/nezha/pull/425)

#### 账单和剩余时间
支持价格和期限单独设置
账单信息附加到group分组控制
一些其他优化
演示地址： https://dev.nezha.pp.ua/


**【20241104更新】支持vps账单，vps套餐展示的PublicNote字段配置**

配置位置：后台-> 服务器 -> 编辑服务器 -> 公开备注
![image](https://eimg.utools.top/i/2024/12/03/12mz24f.png)

完整配置，包含过期时间、价格展示、套餐展示

~~~yaml
{
   "billingDataMod": {
       "startDate": "2024-10-01T00:00:00+08:00",
       "endDate": "2024-11-01T00:00:00+08:00",
       "autoRenewal": "1",
       "cycle": "月",
       "amount": "$3.99"
   },
   "planDataMod": {
       "bandwidth": "30Mbps",
       "trafficVol": "1TB/月",
       "trafficType": "1",
       "IPv4": "1",
       "IPv6": "1",
       "networkRoute": "CN2,GIA",
       "extra": "传家宝,AS9929"
   }
}
~~~


可以单独配置过期时间
~~~yaml
{
   "billingDataMod": {
       "startDate": "2024-10-01T00:00:00+08:00",
       "endDate": "2024-11-01T00:00:00+08:00",
       "autoRenewal": "1",
       "cycle": "月"
   }
}
~~~

可以单独配置价格展示
~~~yaml
{
   "billingDataMod": {
       "cycle": "月",
       "amount": "$3.99"
   }
}
~~~

可以单独配置套餐信息
~~~yaml
{
   "planDataMod": {
       "bandwidth": "30Mbps",
       "trafficVol": "1TB/月",
       "trafficType": "1",
       "IPv4": "1",
       "IPv6": "1",
       "networkRoute": "CN2,GIA",
       "extra": "传家宝,9929"
   }
}
~~~

#### billingDataMod 配置详细说明：

startDate 账单开始时间
~~~yaml
格式如 2022-04-01T23:59:59+08:00
~~~

endDate 账单到期时间
~~~yaml
格式如 2022-05-01T23:59:59+08:00
当以0000-00-00开头时，表示账单无期限，适用于永久免费的vps，如0000-00-00T23:59:59+08:00
~~~

Date格式说明

~~~yaml
分3部分：
1. 日期：2022-04-01
2. 时间：T23:59:59
3. 时区：+08:00
例如：
2024-10-01T23:59:59+05:00
2024-09-21T12:00:00-05:00
2024-03-15T23:59:59+00:00
~~~
autoRenewal 自动续期

~~~yaml
支持值
1：自动续期
0：不自动续期
当设置 "autoRenewal": 1 时，程序会根据当前时间自动判断，vps账单到期后无需手动更改startDate和endDate
~~~

amount 价格

~~~yaml
格式如 $9.99 、€19.92 、¥199、19.99HKD、9.99USD、49.99CNY
如果vps是免费的，请设置为"0" , 如 "amount": "0", 前台展示为 FREE
如果vps是按量收费，请设置为"-1" , 如 "amount": "-1", 前台展示为PAYG
~~~

cycle 付费周期

~~~yaml
支持格式（英文大小写字母都支持，大小写字母混用也支持）
1. 月、month、monthly、m、mo
2. 季、quarterly、q
3. 半年、半、half、semi-annually、h
4. 年、year、annually、y、yr
~~~

#### planDataMod 配置详细说明：

特别提醒
以下字段都不是必填项！！！ 各位老板请根据自己需要自由填写！！！
以下字段都不是必填项！！！ 各位老板请根据自己需要自由填写！！！
以下字段都不是必填项！！！ 各位老板请根据自己需要自由填写！！！

bandwidth 带宽

~~~yaml
格式如 "30Mbps", "1Gbps", "Unlimited"
~~~

trafficVol 流量

~~~yaml
格式如 "1TB/月", "500GB/月", "Unlimited"
~~~

trafficType 流量计费类型

~~~yaml
支持值
1:只单向上行流量计费 
2:双向上下行流量同时计费
3:取入栈和出栈最大的计费 [ Max(In, Out) ]
~~~

IPv4 是否拥有IPv4地址

~~~yaml
支持值
1:有 
0:无
~~~

IPv6 是否拥有IPv6地址

~~~yaml
支持值
1:有 
0:无
~~~

networkRoute 网络路由

~~~yaml
多个用英文逗号','分割, 格式如 "联通4837,移动CMI,电信163"
~~~

extra 其他信息

~~~yaml
多个用英文逗号','分割, 格式如"传家宝,搬瓦工"
~~~

效果图

![image](https://eimg.utools.top/i/2024/12/03/12ujpdc.png)

分组展示不同需求的agent

~~~yaml
使用场景：把需要展示相同账单信息的vps分到一组，使得表头保持一致
~~~

### [【技术】哪吒监控面板SeverStatus美化及手机端自定义部分显示功能](https://www.nodeseek.com/post-151790-1)
~~~yaml
<style>
/* 手机端（屏幕宽度小于 1080px）样式 */
@media (max-width: 1080px) {
    .load {
        display: none; /* 隐藏负载列 */
    }
 .os {
        display: none; /* 隐藏负载列 */
    }
 .traffic {
        display: block; /* 隐藏负载列 */
    }
.name {
    width: 10px;           /* 将宽度固定为 30px */
    overflow: hidden;      /* 隐藏超出部分 */
    white-space: nowrap;   /* 禁止换行 */
    text-overflow: ellipsis; /* 如果内容超过宽度，显示省略号 */
}
}
body[theme]::before {
    background-image: url(https://yourimage.jpg); /* 替换为自己的背景图片链接 */
}

/* 字体设置 */
body[theme] {
    font-family: "Consolas", Arial, Helvetica, sans-serif; /* 修改默认字体 */
}
</style>
<!-- 网站统计 -->
<script async src="https://www.googletagmanager.com"></script> /* 替换为自己的统计代码 */
<!-- 默认半透明模式 -->
<script>
// server-status 默认开启分组
    localStorage.setItem("showGroup", true)
// server-status 主题默认半透明模式
    localStorage.setItem('semiTransparent', true); 
</script>

<!-- Logo设置 -->
<script>
    document.addEventListener('DOMContentLoaded', function() {
        var logo = document.querySelector('.navbar-brand img');
        if (logo) {
            logo.src = 'https://yourlogo.png'; /* 替换为自己的 Logo 图片链接 */
        }
    });
</script>

<!-- Favicon设置 -->
<script>
    var faviconurl = "https://yourlogo.png"; /* 替换为自己的 Logo 图片链接 */
    var link = document.querySelector("link[rel*='icon']") || document.createElement('link');
    link.type = 'image/png';
    link.rel = 'shortcut icon';
    link.href = faviconurl;
    document.getElementsByTagName('head')[0].appendChild(link);
</script>
/* 服务中不显示文字 */
<style>
.service-status .delay-today-text{display: none;visibility: hidden;}
</style>
~~~
**剩余时间**
增加剩余时间列，并添加倒计时进度条动画，在原帖基础上增加了不同进度条颜色改变，已经当开始时间和结束时间都设置为'9999-01-01T00:00:00+08:00'时将显示为999天（适用永久免费的服务器）
[原贴参考链接](https://www.nodeseek.com/post-132638-1)
代码：
~~~yaml
<script>
document.addEventListener('DOMContentLoaded', function() {
    // 在表头添加“剩余时间”列
    var downtimeCells = document.querySelectorAll('th.node-cell.os.center');
    downtimeCells.forEach(function(cell) {
        var newTh = document.createElement('th');
        newTh.className = 'node-cell downtime center';
        newTh.textContent = '剩余时间';
        cell.parentNode.insertBefore(newTh, cell.nextSibling);
    });
    // 定义节点信息
    const affLinks = {
        1: { 
            startDate: new Date('2024-08-12T00:00:00+08:00'),
            expirationDate: new Date('2025-02-01T00:00:00+08:00'),
            content: {
                type: 'text',
                value: ''
            }
        },/* 正常节点 */
        2: { 
            startDate: new Date('2024-08-12T00:00:00+08:00'),
            expirationDate: new Date('2024-08-20T00:00:00+08:00'),
            content: {
                type: 'text',
                value: ''
            }
        },/* 过期节点 */
        3: { 
            startDate: new Date('9999-01-01T00:00:00+08:00'),
            expirationDate: new Date('9999-01-01T00:00:00+08:00'),
            content: {
                type: 'text',
                value: ''
            }
        }/* 永久节点 */
  };

   const createLink = (linkConfig) => {
       const $link = document.createElement('a');
       $link.href = linkConfig.value;
       $link.textContent = linkConfig.label || linkConfig.value;

       if (linkConfig.icon) {
           const $icon = document.createElement('img');
           $icon.src = linkConfig.icon;
           $icon.alt = linkConfig.iconAlt || '';
           $link.appendChild($icon);
       }

       if (linkConfig.text) {
           const $text = document.createElement('span');
           $text.textContent = linkConfig.text;
           $link.appendChild(document.createTextNode(' '));
           $link.appendChild($text);
       }

       return $link;
   };

   const createIcon = (iconConfig) => {
       const $icon = document.createElement('img');
       $icon.src = iconConfig.value;
       $icon.alt = iconConfig.label || 'Icon';

       if (iconConfig.text) {
           const $text = document.createElement('span');
           $text.textContent = iconConfig.text;
           $icon.appendChild(document.createTextNode(' '));
           $icon.appendChild($text);
       }

       return $icon;
   };

   const createSmokeAnimation = () => {
       const $smokeContainer = document.createElement('div');
       $smokeContainer.className = 'smoke-container';

       for (let i = 0; i < 5; i++) {
           const $particle = document.createElement('div');
           $particle.className = 'smoke-particle';
           $smokeContainer.appendChild($particle);
       }

       return $smokeContainer;
   };

   const createCountdown = (startDate, expirationDate) => {
       const total = expirationDate.getTime() - startDate.getTime();

       const $countdownContainer = document.createElement('div');
       $countdownContainer.style.position = 'relative';
       $countdownContainer.style.width = '100%';
       $countdownContainer.style.backgroundColor = '#333';
       $countdownContainer.style.borderRadius = '5px';
       $countdownContainer.style.overflow = 'hidden';
       $countdownContainer.style.boxShadow = 'inset 0 1px 3px rgba(0,0,0,0.2), 0 1px 2px rgba(0,0,0,0.3)'; // 背景3D效果
       $countdownContainer.style.background = 'linear-gradient(to bottom, #444, #222)'; // 背景渐变效果

       const $progressBar = document.createElement('div');
       $progressBar.style.position = 'absolute';
       $progressBar.style.top = '0';
       $progressBar.style.left = '0';
       $progressBar.style.height = '100%';
       $progressBar.style.backgroundColor = '#388e3c'; // 调暗后的绿色进度条
       $progressBar.style.width = '0%';
       $progressBar.style.boxShadow = 'inset 0 1px 3px rgba(0,0,0,0.2), 0 1px 2px rgba(0,0,0,0.3)'; // 进度条3D效果

       const $countdownTime = document.createElement('span');
       $countdownTime.style.position = 'relative';
       $countdownTime.style.zIndex = '1';
       $countdownTime.style.color = '#fff'; // 恢复为白色字体
       $countdownTime.style.padding = '5px';
       $countdownTime.style.fontSize = '12px'; // 调小字体
       $countdownTime.textContent = ' ';

       const $smoke = createSmokeAnimation();

      const updateCountdown = () => {
        const now = new Date();
        const diff = now.getTime() - startDate.getTime();

    // 判断是否为特殊日期
    if (startDate.getTime() === new Date('9999-01-01T00:00:00+08:00').getTime() &&
        expirationDate.getTime() === new Date('9999-01-01T00:00:00+08:00').getTime()) {
        $progressBar.style.width = '100%';
        $progressBar.style.backgroundColor = '#2e7d32'; // 特殊情况的颜色（绿色）
        $countdownTime.textContent = '999天';
        return;
    }

    if (diff >= total) {
        clearInterval(countdownInterval);
        $countdownTime.textContent = '已过期';
        $progressBar.style.backgroundColor = '#c62828'; // 到期后的深红色
        $progressBar.style.width = '100%';
        return;
    }

    const remainingDays = Math.ceil((total - diff) / (1000 * 60 * 60 * 24));
    $countdownTime.textContent = `${remainingDays}天`;
    const progress = 100 - (diff / total) * 100;
    $progressBar.style.width = `${progress}%`;

    // 根据剩余进度设置进度条颜色
    if (progress <= 25) {
        $progressBar.style.backgroundColor = '#c05000'; // 橙色
    } else if (progress <= 50) {
        $progressBar.style.backgroundColor = '#f9a825'; // 黄色
    } else {
        $progressBar.style.backgroundColor = '#388e3c'; // 绿色
    }

    // 更新烟雾动画的位置
    $smoke.style.left = `${progress}%`;
};


       const countdownInterval = setInterval(updateCountdown, 1000);
       updateCountdown();

       $countdownContainer.appendChild($progressBar);
       $progressBar.appendChild($smoke);
       $countdownContainer.appendChild($countdownTime);

       return $countdownContainer;
   };

   const rows = document.querySelectorAll('tr');
   rows.forEach((row) => {
       let osCell = row.querySelector('td.node-cell.os.center');
       let downtimeCell = document.createElement('td');
       downtimeCell.classList.add('node-cell', 'downtime', 'center');
       let nodeId = row.id.substring(1); 
       let affLink = affLinks[nodeId];
       if (!affLink) {
           affLink = {
               content: {
                   type: 'text',
                   value: '  '
               }
           };
       }
       if (osCell && affLink && affLink.content) {
           switch (affLink.content.type) {
               case 'link':
                   let link = createLink(affLink.content);
                   downtimeCell.appendChild(link);
                   break;
               case 'icon':
                   let icon = createIcon(affLink.content);
                   downtimeCell.appendChild(icon);
                   break;
               default:
                   let text = document.createTextNode(affLink.content.value);
                   downtimeCell.appendChild(text);
                   break;
           }

           if (affLink.startDate && affLink.expirationDate) {
               let countdown = createCountdown(affLink.startDate, affLink.expirationDate);
               downtimeCell.appendChild(countdown);
           }

           osCell.parentNode.insertBefore(downtimeCell, osCell.nextSibling);
       }
   });
});
</script>

<style>
@keyframes smoke {
   0% {
       transform: translateY(0) scale(1);
       opacity: 1;
   }
   100% {
       transform: translateY(-20px) scale(0.5);
       opacity: 0;
   }
}
.smoke-container {
   position: absolute;
   top: 0;
   right: 0;
   width: 10px;
   height: 100%;
   overflow: visible;
}
.smoke-particle {
   position: absolute;
   bottom: 0;
   width: 4px;
   height: 4px;
   background: rgba(144, 238, 144, 0.7); /* 淡绿色 */
   border-radius: 50%;
   animation: smoke 1s infinite;
}
.smoke-particle:nth-child(1) {
   left: 0;
   animation-delay: 0s;
}
.smoke-particle:nth-child(2) {
   left: 2px;
   animation-delay: 0.2s;
}
.smoke-particle:nth-child(3) {
   left: 4px;
   animation-delay: 0.4s;
}
.smoke-particle:nth-child(4) {
   left: 6px;
   animation-delay: 0.6s;
}
.smoke-particle:nth-child(5) {
   left: 8px;
   animation-delay: 0.8s;
}
</style>
~~~
**页面特效**
~~~yaml
<script src="https://cdn.jsdelivr.net/gh/mocchen/cssmeihua/js/aixin.js"></script>/* 点击爱心特效 */
<script src="https://cdn.jsdelivr.net/gh/mocchen/cssmeihua/js/yinghua.js"></script>/* 页面樱花特效 */
~~~
**手机端自定义功能**
配合主题颜色，手机端状态栏始终显示为白色。增加手机端启动动画（配合安卓apk打包或ios免签封装为webapp使用效果更佳）。自定义更改手机端背景图片。
~~~yaml
<head>
    <meta http-equiv="Content-Type" content="text/html;">
    <meta http-equiv="x-ua-compatible" content="">
    <meta name="theme-color" content="#FFFFFF">/* 白色 */
    <style>
        /* 适用于iPhone 15 Pro的样式其他机型可自行更改最大及最小宽度 */
        @media only screen and (min-device-width: 375px) and (max-device-width: 1179px) {
            /* 启动动画的样式 */
            #loading-animation {
                position: fixed;
                top: 0;
                left: 0;
                width: 100%;
                height: 100%;
                background-color: #fff; /* 背景颜色 */
                z-index: 9999;
                display: flex;
                align-items: center;
                justify-content: center;
                overflow: hidden; /* 防止图片超出视口 */
            }

            #loading-animation img {
                width: 100vw; /* 图片宽度占满视口宽度 */
                height: 100vh; /* 图片高度占满视口高度 */
                object-fit: cover; /* 图片按比例填充并覆盖整个视口 */
                animation: fadeInOut 3s ease-in-out infinite; /* 动画效果 */
            }

            /* 图片渐变的动画效果 */
            @keyframes fadeInOut {
                0%, 100% {
                    opacity: 1;
                }
                50% {
                    opacity: 0.5;
                }
            }
        }

        /* 其他样式 */
        body[theme]::before {
            background-image: url(https://yourimage.jpg); /* 替换为自己的背景图片链接 */
        }

        /* 字体设置 */
        body[theme] {
            font-family: "Consolas", Arial, Helvetica, sans-serif; /* 修改默认字体 */
        }
    </style>
</head>

<body>
    <!-- 启动动画HTML -->
    <div id="loading-animation" style="display: none;">
        <img src="https://yourimage.gif" alt="Loading..."> <!-- 替换为自己的动画图片链接 -->
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function () {
            var loadingAnimation = document.getElementById('loading-animation');
            // 检查是否为主页面
            if (window.location.pathname === '/' || window.location.pathname === '/index.html') {
                // 如果是主页面，显示加载动画
                loadingAnimation.style.display = 'flex';

                // 设置5秒后隐藏加载动画
                setTimeout(function() {
                    loadingAnimation.style.display = 'none';
                }, 5000); // 5秒（5000毫秒）
            }
        });
    </script>
</body>
~~~


### 官方自定义
> [🎉 通过自定义代码实现server-status主题深色模式半透明样式的前置准备 by nap0o · Pull Request #395 · nezhahq/nezha](https://github.com/nezhahq/nezha/pull/395)
实现server-status主题深色模式半透明样式的自定义代码如下：
~~~yaml
<style>
body[theme="dark"]::before {
    content: "";
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    /** bing每日壁纸 **/
    background: url(https://imgapi.cn/bing.php) no-repeat 50% 50%;
    background-size: cover;
    z-index: -1;
}

body[theme="dark"] {
    font-family: "Helvetica Neue",Helvetica,Arial,sans-serif;
    background: rgba(0, 0, 0, 0.8);
    color: #f1f1f1;
}

body[theme="dark"]::after {
    content: "";
    position: fixed;
}

body[theme="dark"] .navbar {
    /** 顶部导航条 背景 **/
    background-color: rgba(0, 0, 0, 0.8);
    box-shadow: none;
    border: none;
}

body[theme="dark"] .navbar .navbar-brand {
    color: #ffffff;
}

body[theme="dark"] .navbar .dropdown-menu {
    /** 二级导航下拉 背景 **/
    background-color: rgba(0, 0, 0, 0.85);
    border-top: none;
    border-color: #31363b;
    box-shadow: rgba(0, 0, 0, 0.18) 0px 6px 12px;
}

body[theme="dark"] .navbar .dropdown-menu > li > a {
    color: #c8c3bc;
}

body[theme="dark"] .navbar .dropdown-menu > li > a:focus,
body[theme="dark"] .navbar .dropdown-menu > li > a:hover {
    /** 二级导航鼠标悬停选中背景 **/
    background-color: rgba(0, 0, 0, 0.95);
    background-image: linear-gradient(#1c1d26 0, #1c1d26 100%);
}

body[theme="dark"] .navbar .navbar-nav .open .dropdown-menu > li > a {
    color: #f1f1f1;
}

body[theme="dark"] .table,
body[theme="dark"] .table-condensed > tbody > tr,
body[theme="dark"] .table-hover > tbody > tr,
body[theme="dark"] .table-hover > tbody > tr:hover,
body[theme="dark"] .table-striped tbody > tr.even,
body[theme="dark"] .table-striped tbody > tr.odd,
body[theme="dark"] .table-striped tbody > tr.even > td,
body[theme="dark"] .table-striped tbody > tr.even > th,
body[theme="dark"] .table-striped tbody > tr.odd > td,
body[theme="dark"] .table-striped tbody > tr.odd > th,
body[theme="dark"] .table-striped tbody > tr.even > td:hover,
body[theme="dark"] .table-striped tbody > tr.even > th:hover,
body[theme="dark"] .table-striped tbody > tr.odd > td:hover,
body[theme="dark"] .table-striped tbody > tr.odd > th:hover,
body[theme="dark"] .table-striped tbody > tr.expandRow:hover {
    background-color: transparent !important;
}

body[theme="dark"] .content {
    /** 主box 背景 **/
    background-color: rgba(28, 29, 38, 0.8); 
    border: none;
    box-shadow: rgba(0, 0, 0, 0.5) 0 0.625em 2em;
    -webkit-box-shadow: rgba(0, 0, 0, 0.5) 0 0.625em 2em;
    box-shadow: rgba(0, 0, 0, 0.5) 0 0.625em 2em;
}

body[theme="dark"] .table > thead > tr.node-group-tag > th,
body[theme="dark"] .table > thead > tr.node-group-tag > th:before {
    background: unset;
}

body[theme="dark"] .table > tbody > tr > td:before,
body[theme="dark"] .table > tfoot > tr > td:before,
body[theme="dark"] .table > thead > tr > td:before,
body[theme="dark"] .table > thead > tr.node-group-cell > th:before{
     /** border-bottom 颜色 **/
    background-color: rgba(155, 155, 155, 0.1); 
}

body[theme="dark"] .table-hover > tbody > tr:not(.expandRow):hover > td {
    background-color: unset;
}

/* expandRow展开部分样式 */
body[theme="dark"] .table > tbody > tr.expandRow.odd > td:before{
    background-color: unset;
}

body[theme="dark"] .table > tbody > tr.expandRow.even > td:before{
    background-color: unset;
}
/* expandRow展开部分样式结束 */

body[theme="dark"] .progress {
    background-image: none;
    background-color: rgba(255, 255, 255, 0.075); 
}
</style>
~~~
