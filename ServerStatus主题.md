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
