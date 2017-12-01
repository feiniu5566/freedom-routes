支持平台: Linux, Mac OS X, Windows, OpenWRT, DD-WRT, ASUSWRT

生成一个可以运行的脚本, 当VPN运行的时候, 自动添加国内的IP地址到系统`路由表`, 用`直接连接`方式访问国内的网站, 用`VPN`方式访问国外的网站, 从而提升网页浏览速度. (例如: 使用前ping baidu.com是300ms延迟, 使用后可以减少到30ms)

## 项目一览
命令行: [Go版本 - 本项目](https://github.com/SaberSalv/freedom-routes), [Python版本](https://github.com/fivesheep/chnroutes)

图形化应用程序: [Windows](https://github.com/cqjjjzr/freedom-routes#windows%E7%89%88%E5%9B%BE%E5%BD%A2%E5%8C%96%E5%BA%94%E7%94%A8%E7%A8%8B%E5%BA%8F)

## 对chnroutes的改进

1. Linux下导入路由的速度更快, 秒时间导入
2. 支持模板, 可以自定义脚本

# 网络版本

## 下载

每24小时更新一次.

- **Linux, OpenWRT, DD-WRT, ASUSWRT**: [routes-up.sh](http://dl.saber.li/freedom-routes/linux/routes-up.sh) [routes-down.sh](http://dl.saber.li/freedom-routes/linux/routes-down.sh)
- **Mac OS X**: [routes-up.sh](http://dl.saber.li/freedom-routes/mac/routes-up.sh) [routes-down.sh](http://dl.saber.li/freedom-routes/mac/routes-down.sh)
- **Windows**: [routes-up.bat](http://dl.saber.li/freedom-routes/windows/routes-up.bat) [routes-down.bat](http://dl.saber.li/freedom-routes/windows/routes-down.bat)
- **Android**: [routes-up.sh](http://dl.saber.li/freedom-routes/android/routes-up.sh) [routes-down.sh](http://dl.saber.li/freedom-routes/android/routes-down.sh)
- **RouterOS**: [freedomroutes.rsc](http://dl.saber.li/freedom-routes/routeros/freedomroutes.rsc)

## 使用方法

这些ip地址库并不是固定不变的, 尽管变化不大, 但还是建议每隔两三个月更新一次.

**手动运行**

```
启用
# ./routes-up.sh

停用
# ./routes-down.sh
```

Windows需要右键routes-up.bat -> 已管理员身份运行. 并且导入需要好几分钟, 请耐心等待, 有哪位大神知道有更好的方法的话, 求指教.
 
将 此routes-up.bat加入到windows定时计划中，每天中午12点开始执行，记的设置360不用拦截。

**OpenVPN**

```
# cp them to /etc/openvpn
# edit /etc/openvpn/hello.conf

  script-security 2
  up ./routes-up.sh
  down ./routes-down.sh
```

**PPTP**

```
cp routes-up.sh /etc/ppp/ip-pre-up
cp routes-down.sh /etc/ppp/ip-down.d/ip-down
```

# 本地版本

查看[本地版本使用说明](https://github.com/SaberSalv/freedom-routes/blob/master/docs/local.md)

# 开发

## 任何人都可以帮助这个项目

- 请保持低调, 不要推广本项目, 自己用的好就可以了, 不要点击右上角的star按钮
- 提交Bug/建议
- 帮助作者提高文档
- 欢迎其他开发者Fork和发送Pull-Request
- 欢迎其他开发者申请Collaborator权限

感谢所有[贡献者](https://github.com/SaberSalv/freedom-routes/contributors). </br>
感谢原来的[chnroutes](https://github.com/fivesheep/chnroutes)作者.

## 编译

```
$ mkdir output
$ sed -i '/const ASSETS_MODE/s/.*/const ASSETS_MODE = "runtime"/' routes/routes.go
$ go build -o output/freedom-routes
$ cp -r routes/templates output
```
