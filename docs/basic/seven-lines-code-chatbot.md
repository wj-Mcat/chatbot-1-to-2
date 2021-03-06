---
slug: /seven-lines-code-chatbot/
title: 七行代码机器人
sidebar_label: 七行代码机器人
---

:::tip 本章知识点

* 初步认识 Wechaty
* Wechaty 如何监听事件

:::

## 世界上最简短的机器人

相信大家已经很迫不及待想要看看七行代码机器人长什么样子，Talk is Cheep, show you the code.

```typescript
const { Wechaty } = require('wechaty') // import { Wechaty } from 'wechaty'

Wechaty.instance() // Global Instance
.on('scan', (qrcode, status) => console.log(`Scan QR Code to login: ${status}\nhttps://wechaty.js.org/qrcode/${encodeURIComponent(qrcode)}`))
.on('login',            user => console.log(`User ${user} logged in`))
.on('message',       message => console.log(`Message: ${message}`))
.start()
```

以上代码即可运行一个具备监控扫码、登录以及消息事件的聊天机器人，是不是很简单。

使用Wechaty开发聊天机器人的两个核心步骤：
* 指定对接的IM平台协议
* 监听对应的事件

前者是需要根据对应IM平台协议添加不同的参数配置，比如飞书平台上是需要指定`App ID`，`App Secret`， `Verification Token`，而这些参数是可以通过环境变量参数传递到底层Puppet中。使用其他平台的Puppet原理也是如此，只需要简单的几行配置即可完成对不同平台的对接。

可在任何简单的事情背后，Wechaty做了大量的工作，才放开发者只需要简单的七行代码便能够开发出一个聊天机器人。

## 事件监听

在与IM平台中的对接中，所有的消息接受都是以事件监听的形式来完成，比如扫码登录消息，登录消息，聊天消息等。此处总共由如下消息内容。

目前系统中存在的事件如下：

| 事件类型 | 关键字      | 备注                              |
| -------- | ----------- | --------------------------------- |
| 基础事件 | scan        | 当出现二维码扫描登录时触发的事件  |
| 基础事件 | login       | 当用户登录完成之后时触发的事件    |
| 基础事件 | logout      | 当用户注销完成之后时触发的事件    |
| 基础事件 | message     | 当用户收到消息之后时触发的事件    |
| 基础事件 | friendship  | 当用户接收到好友申请时触发的事件  |
| 群聊事件 | room-topic  | 当群名变动时触发的事件            |
| 群聊事件 | room-invite | 当邀请群成员入群时触发的事件      |
| 群聊事件 | room-join   | 当有成员加入到某群时触发的事件    |
| 群聊事件 | room-leave  | 当有群成员退出群聊时触发的事件    |
| 系统事件 | ready       | 当Wechaty数据加载完毕时触发的事件 |
| 系统事件 | heartbeat   | 当接收到系统心跳包时触发的事件    |
| 系统事件 | error       | 当接受系统错误时触发的事件        |

而所有事件的注册只需要使用`on`函数即可完成。

:::warning

不过需要注意的是，不同事件的对应的参数是不一样的，这也是很多开发者会遇到的问题，具体的参数列表可查看官网文档：https://wechaty.js.org/docs/recipes/event#login-event-bot-contact

:::

## 总结

七行代码机器人让大家对Wechaty开发聊天机器人有了一个初步的认识，只是实现了飞鼠平台的Puppet使用以及事件的监听。然而在实际的机器人对接过程中，是需要有更多更复杂的场景机器人的，比如最基础的消息回复机器人，那么接下来我将给大家介绍最简单的叮咚机器人的开发。