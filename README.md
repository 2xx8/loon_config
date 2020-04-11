# IOS国际版抖音(Tik Tok)通过代理工具突破限制

## 2020/4/11测试可正常使用
- 理论上支持rewrite功能的代理软件都可行
- 本教程建议APP版本较低，无需通过rewrite修改版本号，与国区APP不冲突
### 使用环境
- IOS系统版本：13.3.1
- 代理工具：Loon 2.1.0(132)
- 旧版Tik Tok
- 无需代理节点，可直连

### 以下版本可突破限制使用
港区和美区的区别如下（**版本ID**抓包时会用到）
商店地区|港区|美区
:--:|:--:|:--:
版本号|8.2.0|13.2.2
**版本ID**|**832883719**|**832984563**
登录|√|√
切换地区|√|×
发布视频|√|×
点赞评论|√|√
看直播|×|√
话题标签|√|×
App共存|√|√

### 需要用到的工具
- 旧版iTunes
- 外区AppleID
- 抓包工具
- 可能会用到iTools、爱思助手之类工具（用于安装旧版APP）
- [App版本ID在线查询工具](https://tools.lancely.tech/apple/app-search)
- [iTunes历史版本下载](https://www.theiphonewiki.com/wiki/ITunes)

## 操作流程

### 准备工作
- 安装好旧版iTunes，有应用商店界面的，可使用12.3.2.35
- 安装好抓包工具，以下教程以Fiddler为例
- 申请好外区AppleID（申请时需挂代理，**支付方式**选“无”，**账单地址**根据所选地区在谷歌地图随意选）

### 抓包安装旧版Tik Tok
- 网上很多演示教程
- [Fiddler抓包旧版APP参考教程](https://olook.me/posts/a4b9cc89.html)
```
    抓包断点
    bpu MZBuy.woa
```

### Loon配置文件修改
- 添加Rewrite规则
```
    # 解锁 TikTok
    # 更换 TikTok 区域请修改下方国家代码，韩国KR 日本JP 台湾TW
    (?<=(carrier|account|sys|sim)_region=)CN KR 307
    # 去水印
    (.*video_id=\w{32})(.*watermark=)(.*) $1 302
```
- 添加hostname
```
    ,api*.tiktokv.com,api*.musical.ly,api*.amemv.com,aweme*.snssdk.com
```
