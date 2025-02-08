# Mfsign
mfuns自动签到

# 如何使用

### 1. 首先fork本仓库
`fork`在右上角`star`的旁边

### 2.设置用户名和密码

打开`Setting`→`Secrets and variables`(选择`Action`)

添加`Repository secrets`
![Repository secrets](https://pic-oss.mouup.top/pic/2025/02/b1e33fa04c7b057d043cb055bf12b6e8.png)

依此添加以下`secret`

| name        | secret             |
|-------------|--------------------|
| `ACCOUNT`   | 你的mfuns账号(手机号/用户名) |
| `PASSWORD`  | 你的密码               |


### 3.设置签到时间
回到[Code](../../code)页面，编辑`github/workflows`下的`auto_sign.yml`文件

```
name: Mfuns_auto_sign
on:
  workflow_dispatch:
  schedule:
    # IMPORTANT: Set cron job in UTC timezone
    - cron:  '0 0 * * *'
......
```
修改`cron`参数

* 从左往右第一位表示`一小时中的某分钟`
* 第二位表示`一天中的某个小时`
* 第三位表示`一个月中的某一天`
* 第四位表示`月份`
* 第五位表示`一周中的某一天`
* 星号表示任意

比如这里的`0 0 * * *`表示每天UTC时间0:00(北京时间早上8:00)

你可以设置自己想要的签到时间

改完后点右上角的`Commit changes`，然后在弹出的框中再点`Commit changes`保存更改

### 4.测试运行
前往[Actions](../../actions)页面

按照以下步骤测试运行



## 添加飞书通知

![Feishunotice](https://pic-oss.mouup.top/pic/2025/02/dc839114f1c0ee4f7c5be014cebbb807.png)

### 1.
首先参考[官方文档](https://open.feishu.cn/document/client-docs/bot-v3/add-custom-bot?lang=zh-CN#399d949c)
创建机器人

记得在`安全设置`中勾选`签名校验`

至此，我们得到了`webhook地址`和`签名校验用的密钥`

### 2.
再次打开`Setting`→`Secrets and variables`(选择`Action`)

添加`Repository secrets`

依此添加以下`secret`

| name        | secret         |
|-------------|----------------|
| `FEISHU_WEBHOOK`   | 刚刚拿到的webhook地址 |
| `FEISHU_BOT_SECRET`  | 签名校验用的密钥           |

然后以后每次签到成功就会收到飞书的通知了