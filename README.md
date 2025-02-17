![](https://raw.githubusercontent.com/idootop/mi-gpt/main/assets/demo.png)

# MiGPT：智能家居，从未如此贴心 ❤️

[![npm version](https://badge.fury.io/js/mi-gpt.svg)](https://www.npmjs.com/package/mi-gpt) [![Docker Image Version](https://img.shields.io/docker/v/idootop/mi-gpt?color=%23086DCD&label=docker%20image)](https://hub.docker.com/r/idootop/mi-gpt)

在这个数字化的世界里，家已不仅仅是一个居住的地方，而是我们数字生活的延伸。

`MiGPT` 通过将小爱音箱、米家智能设备，与 ChatGPT 的理解能力完美融合，让你的智能家居更懂你。

`MiGPT` 不仅仅是关于设备自动化，而是关于：**打造一个懂你、有温度、与你共同进化的家**。

未来，你的每个智能家居设备，从灯泡、插座，到扫地机器人、电视等，

都可以作为一个个独立的智能体 (Agent)，更智能、更贴心的响应你的指令。

这些独立的智能体，也可以彼此感知，彼此配合，构成一个更强大的协作网络。

而小爱音箱就像是，你的智能家居专属管家，全心全意为你服务，释放智能家居真正的潜力。

## ✨ 项目亮点

- **🎓 LLM 回答**。想象一下，你的小爱音箱变身聊天高手，可以使用 [ChatGPT](https://chat.openai.com) 等大模型来回答你，比你懂更多。
- **🎭 角色扮演**。一秒调教小爱，无论是成为你的完美伴侣，还是那个能听你倾诉心事的贴心闺蜜，都不在话下。
- **💬 流式响应**。爱情来得太快就像龙卷风，而你的小爱音箱也是，对你的爱意秒回，爱你不会让你等太久。
- **🧠 长短期记忆**。小爱音箱现在能记住你们之间的每一次对话，越聊越默契，就像是你身边的老朋友。
- **🔊 自定义 TTS**。厌倦了小爱同学的语音？帮你解锁[「豆包」](https://doubao.com)同款音色，就像真人在回你的消息。
- **🤖️ 智能家居 Agent**。心情不好？小爱立刻懂你，自动帮你播放喜欢的音乐，调节灯光，逗你开心。_TODO_

## 🚀 启动项目

`MiGPT` 有两种启动方式: [Docker](#docker) 和 [Node.js](#nodejs)。

### Docker

[![Docker Image Version](https://img.shields.io/docker/v/idootop/mi-gpt?color=%23086DCD&label=docker%20image)](https://hub.docker.com/r/idootop/mi-gpt)

对于电脑小白或者不想自己配置代码运行环境（Node）的同学，可以使用 Docker 启动方式。

请先按照[「配置参数」](#%EF%B8%8F-配置参数)章节，配置好你的 `.env` 和 `.migpt.js` 文件。然后使用以下命令启动 docker：

```shell
docker run -d  --env-file $(pwd)/.env \
    -v $(pwd)/.migpt.js:/app/.migpt.js \
    idootop/mi-gpt:latest
```

### Node.js

[![npm version](https://badge.fury.io/js/mi-gpt.svg)](https://www.npmjs.com/package/mi-gpt)

如果你是一名前端 (Node) 开发者，也可以通过 NPM 安装 `mi-gpt` 启动 `MiGPT`。

```shell
npm install mi-gpt # 安装依赖
```

然后，创建并启动 `MiGPT` 实例。初始化参数请看下面的[「配置参数」](#%EF%B8%8F-配置参数)章节。

```typescript
import { MiGPT } from "mi-gpt";

async function main() {
  const client = MiGPT.create({
    speaker: {
      userId: process.env.MI_USER,
      password: process.env.MI_PASS,
      did: process.env.MI_DID,
    },
  });
  await client.start();
}

main();
```

## ⚙️ 配置参数

### 环境变量

重命名本项目根目录下的 `.env.example` 文件为 `.env`。

然后，将里面的环境变量修改成你自己的，参数含义如下：

| 环境变量名称           | 描述                                                                                        | 示例                                 |
| ---------------------- | ------------------------------------------------------------------------------------------- | ------------------------------------ |
| **小米服务**           |                                                                                             |                                      |
| `MI_USER`              | 小米账户                                                                                    | `"12345678901"`                      |
| `MI_PASS`              | 账户密码                                                                                    | `"123456"`                           |
| `MI_DID`               | 小爱音箱 ID 或名称                                                                          | `"小爱音箱 Pro"`                     |
| **OpenAI**             |                                                                                             |                                      |
| `OPENAI_API_KEY`       | OpenAI API 密钥                                                                             | `abc123`                             |
| `OPENAI_MODEL`         | 使用的 OpenAI 模型                                                                          | `gpt-4o`                             |
| `AZURE_OPENAI_API_KEY` | 可选，[Microsoft Azure OpenAI](https://www.npmjs.com/package/openai#microsoft-azure-openai) | `abc123`                             |
| `OPENAI_BASE_URL`      | 可选，OpenAI API BaseURL                                                                    | `https://api.openai.com/v1`          |
| **提示音效（可选）**   |                                                                                             |                                      |
| `AUDIO_SILENT`         | 静音音频链接                                                                                | `"https://example.com/slient.wav"`   |
| `AUDIO_BEEP`           | 默认提示音链接                                                                              | `"https://example.com/beep.wav"`     |
| `AUDIO_ACTIVE`         | 唤醒提示音链接                                                                              | `"https://example.com/active.wav"`   |
| `AUDIO_ERROR`          | 出错提示音链接                                                                              | `"https://example.com/error.wav"`    |
| **豆包 TTS（可选）**   |                                                                                             |                                      |
| `TTS_DOUBAO`           | 豆包 TTS 接口                                                                               | `"https://example.com/tts.wav"`      |
| `SPEAKERS_DOUBAO`      | 豆包 TTS 音色列表接口                                                                       | `"https://example.com/tts-speakers"` |

### .migpt.js

重命名本项目根目录下的 `.migpt.example.js` 文件为 `.migpt.js`。

然后，将里面的配置参数修改成你自己的，参数含义如下：

| 参数名称                     | 描述                                                          | 示例                                               |
| ---------------------------- | ------------------------------------------------------------- | -------------------------------------------------- |
| **bot**                      |                                                               |                                                    |
| `name`                       | 对方名称（小爱音箱）                                          | `"傻妞"`                                           |
| `profile`                    | 对方的个人简介/人设                                           | `"性别女，性格乖巧可爱，喜欢搞怪，爱吃醋。"`       |
| **master**                   |                                                               |                                                    |
| `name`                       | 主人名称（我自己）                                            | `"陆小千"`                                         |
| `profile`                    | 主人的个人简介/人设                                           | `"性别男，善良正直，总是舍己为人，是傻妞的主人。"` |
| **room**                     |                                                               |                                                    |
| `name`                       | 会话群名称                                                    | `"魔幻手机"`                                       |
| `description`                | 会话群简介                                                    | `"傻妞和陆小千的私聊"`                             |
| **speaker**                  |                                                               |                                                    |
| `userId`                     | 小米账户                                                      | `"12345678901"`                                    |
| `password`                   | 账户密码                                                      | `"123456"`                                         |
| `did`                        | 小爱音箱 ID 或名称                                            | `"小爱音箱 Pro"`                                   |
| `ttsCommand`                 | 小米音箱 TTS 指令（[可在此查询](https://home.miot-spec.com)） | `[5, 1]`                                           |
| `wakeUpCommand`              | 小米音箱唤醒指令（[可在此查询](https://home.miot-spec.com)）  | `[5, 3]`                                           |
| **speaker 其他参数（可选）** |                                                               |                                                    |
| `callAIKeywords`             | 当消息以关键词开头时，会调用 AI 来响应用户消息                | `["请", "傻妞"]`                                   |
| `wakeUpKeywords`             | 当消息以关键词开头时，会进入 AI 唤醒状态                      | `["召唤傻妞", "打开傻妞"]`                         |
| `exitKeywords`               | 当消息以关键词开头时，会退出 AI 唤醒状态                      | `["退出傻妞", "关闭傻妞"]`                         |
| `onEnterAI`                  | 进入 AI 模式的欢迎语                                          | `["你好，我是傻妞，很高兴认识你"]`                 |
| `onExitAI`                   | 退出 AI 模式的提示语                                          | `["傻妞已退出"]`                                   |
| `onAIAsking`                 | AI 开始回答时的提示语                                         | `["让我先想想", "请稍等"]`                         |
| `onAIReplied`                | AI 结束回答时的提示语                                         | `["我说完了", "还有其他问题吗"]`                   |
| `onAIError`                  | AI 回答异常时的提示语                                         | `["出错了，请稍后再试吧！"]`                       |
| `exitKeepAliveAfter`         | 无响应一段时间后，多久自动退出唤醒模式（单位秒，默认 30 秒）  | `30`                                               |

## 💬 常见问题

**Q：启动项目后控制台有打印新消息，但是没有 AI 回复**

消息默认不会调用 AI 进行回复，请检查消息是否以召唤关键词开头，或包含唤醒词。

**Q：控制台有打印 AI 回复，但是设备没有播放**

不同型号的小爱音箱 TTS 指令不同: [https://github.com/idootop/mi-gpt/issues/5](https://github.com/idootop/mi-gpt/issues/5#issuecomment-2122881495)

可以到 https://home.miot-spec.com 查询具体的 TTS 指令，然后修改配置文件中的指令参数。

<details>
<summary>👉 查看教程</summary>

![](https://raw.githubusercontent.com/idootop/mi-gpt/main/assets/search.jpg)
![](https://raw.githubusercontent.com/idootop/mi-gpt/main/assets/command.jpg)

</details>

**Q：怎样使用豆包的音色**

很遗憾，豆包上的音色需要豆包 TTS 接口支持，本项目暂不对外提供此服务。

**Q：我还有其他问题**

请在此处提交 [issue](https://github.com/idootop/mi-gpt/issues)，有时间我会查看并解答。

## 🚨 免责声明

本项目旨在分享学习大型语言模型（LLM）智能对话及智能家居自动化相关知识，严禁用于任何商业目的或违反所在地区的法律法规。使用者须知悉，本项目代码可能存在未知的缺陷或风险，因使用本项目引起的任何形式的损失或损害（包括但不限于设备故障、账户封禁等），使用者需自行承担全部责任。

## ❤️ 鸣谢

- https://github.com/yihong0618/xiaogpt
- https://github.com/inu1255/mi-service
- https://github.com/Yonsm/MiService
