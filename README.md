<p align="center"><img width="100" src="http://xkctk.jtys.tj.gov.cn/templates/XKCTK/images/top1_tjjt.png" alt="tjjt logo"></p>

<p align="center">
  <img src="https://img.shields.io/badge/build-passing-green" alt="Version">
  <img src="https://img.shields.io/badge/license-MIT-blue" alt="License">
</p>

<h2 align="center">Indicator</h2>

Indicator是一个由go编写，可以定时推送中签结果到微信的服务。

## 效果

![O4lN3ijeJyUF1hH](https://i.loli.net/2021/03/09/O4lN3ijeJyUF1hH.png)

## 功能
- 支持直接推送中签结果到微信
- 支持设置多个申请人信息
- 支持自定义推送时间

## 使用
1、登录天津市小客车调控管理信息系统：http://xkctk.jtys.tj.gov.cn， 登录成功之后可以看到如下信息，复制图中蓝色框的申请编码以备后用。

![QTVUpdFo8rqWMin](https://i.loli.net/2021/03/08/QTVUpdFo8rqWMin.png)

2、到[Server酱](https://sct.ftqq.com/) 申请SendKey

![eHE8zZylTUIaqwP](https://i.loli.net/2021/03/08/eHE8zZylTUIaqwP.png)

3、绑定消息通道（消息通道建议绑定企业微信，当然也可以选择其他的）

![EmiuYAeXROj7cDJ](https://i.loli.net/2021/03/08/EmiuYAeXROj7cDJ.png)

4、从[release版本](https://github.com/liuqitoday/indicator/releases) 中选择最新的下载

5、修改配置文件[app.yaml](https://github.com/liuqitoday/indicator/blob/master/app.yaml)

```
# server酱：https://sct.ftqq.com/
serverChan:
  secret: TTTTTTTCT1566KbEBnK00lM4cMpEdZ   # 密钥

# 指标申请人，可以填写多个
applicant:
  - name: 张三                                 # 申请人真实姓名
    nickname: zhangsan                        # 申请人昵称，推送到微信时会显示改昵称
    code: 1234102865678                       # 申请人申请编码
    applyDate: 2022年02月09日                  # 申请日期
  - name: 王五
    nickname: wangwu
    code: 3256102247899
    applyDate: 2022年02月09日

cron: '0 0 8 27,28,29 * *'                    # cron表达式，可以自定义时间
```
cron表达式可以设置一个最近的未来时间，用作调试，举个栗子：

> '0 24 18 * * *' # 每天的18:24执行

6、上传indicator、app.yaml到服务器

![GBZKUNdzxiQ2Vsn](https://i.loli.net/2021/03/08/GBZKUNdzxiQ2Vsn.gif)

```
chmod 773 indicator

nohup ./indicator &  

tail -f nohup.out
```

## Docker 方式使用
1、 宿主机中创建配置文件 app.yaml ，填写如下内容，并按照实际情况进行修改
```
# server酱：https://sct.ftqq.com/
serverChan:
  secret: SCT15665TJKOcMpEdZ   # 密钥

# 指标申请人，可以填写多个
applicant:
  - name: 张三                                 # 申请人真实姓名
    nickname: zhangsan                        # 申请人昵称，推送到微信时会显示改昵称
    code: 1234102865678                       # 申请人申请编码
    applyDate: 2022年02月09日                  # 申请日期，可填写任意值，仅用于提醒自己记得去手动续期
  - name: 王五
    nickname: wangwu
    code: 1234567897899
    applyDate: 2022年02月10日

cron: '0 0 8 27,28,29 * *'                    # cron表达式，可以自定义时间
```
2、在 app.yaml 目录下使用以下命令运行，可根据需求修改
```
docker run -d \
  -v $PWD/app.yaml:/app.yaml \
  --name indicator \
  --restart unless-stopped \
  liuqitoday/indicator:latest
```

## 后记（telami）
兄弟们，我改成竞拍了，现在牌子已经上完了

![gKmADx](http://cdn.telami.cn/uPic/gKmADx.png)

## 鸣谢
[Go](https://github.com/golang/go)

[GoLand](https://www.jetbrains.com/go/)
