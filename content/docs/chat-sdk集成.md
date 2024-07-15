+++
title = "chat-sdk集成"
weight = 6
+++

# chat-sdk 集成

`问答对话`页支持以下两种方式集成：

1. npm 组件包集成
2. iframe 嵌入

## npm 组件包集成

1. 进入到/webapp/packages/chat-sdk 目录，修改 package.json

```
{
  "name": "xxx-chat-sdk",
  "version": "x.x.x",
  ...
}
```

2. 执行`npm run build`
3. 执行`npm publish`，将组件发布到 npm 仓库
4. 在 react 前端项目执行`npm install xxx-chat-sdk`，安装 chat-sdk 组件包
5. 在 react 前端项目中引入 chat-sdk 包

```
import { Chat } from 'xxx-chat-sdk';

const ChatPage = () => {
  return (
    <Chat token="xxx" />
  );
};

export default ChatPage;
```

通过以上步骤便可以将`问答对话`页集成到业务系统中了

{{< hint info >}}
**提示**

1. npm 包名 name 和版本 version 需要自行根据项目业务需要进行设置
2. token 为 supersonic 用户登录认证 token
   {{< /hint >}}

## iframe 嵌入

将以下代码加入业务系统前端项目组件中

```
<iframe
  src="http://localhost:9080/chat/external"
  style={{ border: "none" }}
/>
```

通过以上步骤便可以将`问答对话`页嵌入到到业务系统中了

{{< hint info >}}
**提示**

1. 嵌入链接地址需要根据实际部署环境进行修改
2. 业务系统与 supersonic 登录认证已打通
   {{< /hint >}}
