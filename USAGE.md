# Comedy Shortform Skill Pack 使用说明

这套 Skill 用于把喜剧短视频创意发展成可拍的短剧本，或诊断已有剧本。主要入口是 [`comedy-shortform-writer`](.agents/skills/comedy-shortform-writer/SKILL.md)。如果只想解决其中一个问题，可以单独使用喜剧机制、Sketch 结构、双主角结构或剧本诊断 Skill。

本文面向在 Codex 中使用本仓库 `.agents/skills/` 的创作者。安装步骤见 [README](README.md#安装)。当前发布包是 Markdown 指令与参考资料，不需要另行启动服务或运行脚本。

## 1. 三十秒上手

安装后开启一个新的 Codex 对话，在消息中明确点名 Skill。Codex 支持用 `$` 前缀显式调用；也可以直接说“请使用 comedy-shortform-writer Skill”。

```text
$comedy-shortform-writer
请写一个约 60 秒的双人喜剧短剧初稿。
前提：健身房教练把会员的每个请假理由都当成新的训练项目。
限制：两名演员、一个室内场景、只有计时器和毛巾两件道具。
请给出连续时间码、可拍动作、对白和估算时长。
```

如果只想诊断已有稿件，把入口改成 `$script-diagnosis`，并贴上原稿。若希望结果保存为文件，另写明项目根目录和具体文件名，例如“请把最终稿保存到 `<项目根目录>/02_Script/短剧本.md`”。Skill 本身规定创作流程和输出，不会替你指定项目文件路径。

## 2. 先选对入口

| 你现在要做什么 | 使用 Skill | 会得到什么 |
| --- | --- | --- |
| 从一句创意写完整短剧，或对已有稿件做完整改稿 | [`comedy-shortform-writer`](.agents/skills/comedy-shortform-writer/SKILL.md) | 前提与假设、形式与人物、连续时间码 Beat Sheet、动作对白剧本、诊断与修订点。 |
| 只有一个模糊笑点，想找到能反复产生变化的规则 | [`comedy-engine`](.agents/skills/comedy-engine/SKILL.md) | 一句话喜剧规则、角色动机、至少两次不同变化和可能的兑现。 |
| 规则已确定，只想排 Sketch 节拍 | [`structure-sketch`](.agents/skills/structure-sketch/SKILL.md) | 规则建立、变化、payoff、估算时间码和拍摄限制；不是完整剧本。 |
| 重点在两个人如何互相改变局面 | [`structure-duo`](.agents/skills/structure-duo/SKILL.md) | 双方目标、信息差、攻防节拍、权力变化和结尾兑现；不是完整剧本。 |
| 已有剧本，先找问题或做一次明确授权的定向改写 | [`script-diagnosis`](.agents/skills/script-diagnosis/SKILL.md) | 有文本证据的问题清单、优先级和修订方案；只有明确要求改稿时才附改稿。 |

Sketch 与双主角可以同时成立。例如，两人争夺同一台“每按一次按钮就改变身份”的机器，既有可重复规则，也有双方攻防。需要完整成稿时，直接使用主入口，并告诉它两种结构都要保留。

## 3. 提供哪些信息

信息越具体，越容易得到符合拍摄条件的稿件。可以只给一句创意；如果核心行动、人物目标或必须保留的内容不明确，Skill 会先问决定性问题。

| 信息 | 推荐写法 | 为什么需要 |
| --- | --- | --- |
| 创意或原稿 | 一句话前提，或粘贴／指向现有剧本。 | 决定改写对象和核心笑点。 |
| 人物 | 人数、关系、眼前目标、各自不肯让步的事。 | 决定冲突和人物选择。 |
| 时长 | “以 60 秒为目标”或“成片不得超过 60 秒”。 | 前者是规划目标，后者是明确硬上限。 |
| 拍摄条件 | 演员、场景、道具、可否配音、能否出现第三人。 | 避免写出无法拍摄的动作。 |
| 基调与观众 | 例如冷幽默、荒诞、职场、亲子。 | 帮助选择动作和对白的强度。 |
| 保留项 | “保留人物关系、第二个笑点和结尾的反转”。 | 防止改稿时换掉你真正想保留的内容。 |
| 本轮任务 | “先发散”“只诊断”“写初稿”“压成成片版”。 | 决定交付深度，以及是否授权改写。 |

### 从零创作模板

```text
$comedy-shortform-writer
本轮任务：写完整初稿。
一句话前提：[谁在什么场合，用什么错误方法达成什么目标]
人物与关系：[人数、彼此关系、各自的眼前目标]
喜剧基调：[例如荒诞但表演克制]
目标时长：[例如以 60 秒为规划目标]
拍摄限制：[演员、场景、道具、特效、配音等]
必须出现：[你最想保留的动作、笑点或结尾]
不要出现：[明确禁用的人物、设定或表现]
输出：连续时间码 Beat Sheet、可拍动作与对白、估算总时长；若偏离目标，指出具体可删或可补的段落。
```

### 用已有剧本改稿模板

```text
$comedy-shortform-writer
本轮任务：在原稿基础上改稿，并说明改了什么。
原稿：[粘贴全文，或给出 Codex 可读取的文件路径]
必须保留：[人物关系、核心笑点、重要情节节点]
希望解决的问题：[例如前 15 秒建立太慢、结尾缺少兑现]
时长要求：[目标时长，或明确的成片硬上限]
拍摄限制：[演员、场景、道具]
如有修改会触及必须保留项，请先说明冲突并询问我。
```

如果只是想知道原稿哪里有问题，使用 `$script-diagnosis`，并写“只诊断，不改写”。这样可以先确认问题，再决定是否授权改稿。

## 4. 推荐工作流

### 路线 A：一句创意到完整初稿

1. 用 `$comedy-shortform-writer` 提供前提、人物、时长目标和拍摄限制。
2. 检查它复述的明确要求与必要假设是否正确。关键事实冲突时先回答澄清问题。
3. 阅读 Beat Sheet，确认 setup、变化和 payoff 是同一条因果链。
4. 阅读剧本中的动作和对白，标出你想保留或替换的部分。
5. 根据估算时长和具体剪辑点，决定是否继续压缩或补充。

初稿以 60 秒为目标，并不等于每次都必须恰好写成 60 秒。如果估算是 68 秒，Skill 应指出可省时间的具体段落；真正要交付不超过 60 秒的版本，再明确提出硬上限。

```text
请沿用上一版人物、核心规则和结尾兑现，把它改成成片候选稿，估算总时长不得超过 60 秒。
实际删改重复节拍和冗长对白，重新排连续时间码；列出删改取舍，不要只把原时间码改小。
```

### 路线 B：先验证机制，再写剧本

适合“有趣，但还不知道能不能撑满一条短视频”的创意。

```text
$comedy-engine
前提：公司里每个人道歉都必须办理责任交接。
请提炼一句可观察的喜剧规则，给出两次不同后果和一次结尾兑现。
先不要写完整剧本。
```

机制成立后，可用 `$structure-sketch` 排建立、变化和兑现；若两人的攻防是重点，再用 `$structure-duo` 检查双方是否都推动局面。最后把选定规则和节拍交给 `$comedy-shortform-writer` 写完整稿。你也可以跳过中间步骤，直接用主入口完成全流程。

### 路线 C：先诊断，再定向改稿

```text
$script-diagnosis
下面是现有剧本：[粘贴原稿]
请只诊断结构、笑点兑现、节奏与可拍性。引用具体动作或台词作为证据，按影响排序。
保留人物关系和最后一个反转。暂时不要改写。
```

看完诊断后，再选择一个明确方向：

```text
请按诊断中的前两项问题做一次定向改稿。保留原稿人物关系与最后一个反转；改后说明每处修改解决了什么问题，并重新估算时长。
```

诊断 Skill 不会仅凭“我觉得不好笑”判定问题；它应指出问题所在的文本位置、影响和修改理由。若修订必须触及你指定的保留项，它会先询问取舍。

### 路线 D：只解决局部结构

不需要完整稿时，可以把问题限定在单个入口：

```text
$structure-sketch
规则：每盖一次章，顾客就被分配一个新身份。两名演员、一个柜台、45 秒目标。
只排建立、两次不同变化和结尾兑现，给连续时间码，不写完整对白。
```

```text
$structure-duo
两人都想关闭同一台会自动续费的机器。请分别写清双方目标、信息差、第一次权力落点和三轮攻防。
如果删掉任一人后故事仍然成立，请指出原因并调整结构。先不要写完整剧本。
```

## 5. 怎样理解输出

主入口的完整输出通常分为五部分：

1. **创意或原稿摘要与保留项／假设**：核对它有没有误解你给的事实，尤其是原稿中必须保留的人物关系、核心笑点和节点。
2. **喜剧形式与人物配置**：看它如何判断 Sketch 规则、双主角关系，或两者兼有。
3. **时间码 Beat Sheet**：从 0 秒连续到剧本结尾，标出建立、变化和兑现。目标时长与估算总时长应分开写。
4. **短剧本**：动作、反应、停顿和对白都要能被演员及镜头具体执行。
5. **诊断和本轮修订点**：区分“初稿”“成片候选稿”和仍有明确要求未满足的“待修改稿”；未实际改写时，应给具体可剪／可补位置。

时间码是写作估算，不是经过试读的成片计时。并行动作和对白只算一次实际经过时间；静默、反应与停顿也占时间。准备拍摄前，应至少朗读、走位和计时一次，再据此调整。

## 6. 进阶：九个书籍路由

一般创作直接使用五个常用入口即可。若你想单独研究某种方法，可调用下列路由 Skill；它们会按自身路由表选参考能力卡或细分 Skill。

| 路由 Skill | 适合单独处理的问题 | 细分 Skill 示例 |
| --- | --- | --- |
| [`comic-toolbox`](.agents/skills/comic-toolbox/SKILL.md) | 喜剧前提、人物视角、危险性、Sketch 或情节贯穿。 | [`comic-premise`](.agents/skills/comic-premise/SKILL.md)、[`comic-jeopardy`](.agents/skills/comic-jeopardy/SKILL.md) |
| [`art-of-character`](.agents/skills/art-of-character/SKILL.md) | 人物欲望、矛盾、过去经历与变化。 | [`character-desire`](.agents/skills/character-desire/SKILL.md)、[`character-contradiction`](.agents/skills/character-contradiction/SKILL.md) |
| [`hidden-tools-comedy`](.agents/skills/hidden-tools-comedy/SKILL.md) | 喜剧主人公的行动力、喜剧力量与直／弯角色分工。 | [`comic-hero`](.agents/skills/comic-hero/SKILL.md)、[`straight-wavy-line`](.agents/skills/straight-wavy-line/SKILL.md) |
| [`comedy-writers-companion`](.agents/skills/comedy-writers-companion/SKILL.md) | 笑点骨架、升级、双人或多人配置。 | [`comic-skeleton`](.agents/skills/comic-skeleton/SKILL.md)、[`comic-duo`](.agents/skills/comic-duo/SKILL.md) |
| [`comedy-bible`](.agents/skills/comedy-bible/SKILL.md) | 单个笑话、铺垫与包袱、三次法、回调。 | [`setup-punchline`](.agents/skills/setup-punchline/SKILL.md)、[`callback`](.agents/skills/callback/SKILL.md) |
| [`writing-dialogue`](.agents/skills/writing-dialogue/SKILL.md) | 对白误导、压缩、张力与沉默。 | [`dialogue-misdirection`](.agents/skills/dialogue-misdirection/SKILL.md)、[`dialogue-compression`](.agents/skills/dialogue-compression/SKILL.md) |
| [`screenplay`](.agents/skills/screenplay/SKILL.md) | 场景设计、冲突串联、人物与情节的关系。 | [`scene-design`](.agents/skills/scene-design/SKILL.md)、[`conflict-chain`](.agents/skills/conflict-chain/SKILL.md) |
| [`comedy-movie`](.agents/skills/comedy-movie/SKILL.md) | 更长篇幅的喜剧骨架、类型公式和升级。 | [`genre-formulas`](.agents/skills/genre-formulas/SKILL.md)、[`comic-engine-blake`](.agents/skills/comic-engine-blake/SKILL.md) |
| [`sitcom`](.agents/skills/sitcom/SKILL.md) | 情景喜剧引擎、角色群像、单集和弧线。 | [`sitcom-engine`](.agents/skills/sitcom-engine/SKILL.md)、[`sitcom-arc`](.agents/skills/sitcom-arc/SKILL.md) |

路由 Skill 并非九个必须依次执行的步骤。明确只要某个细分方法时，可以直接点名相应的细分 Skill；需要完整 60 秒短剧时，仍以 `comedy-shortform-writer` 为主入口。

## 7. 常见问题

### Skill 没有出现

先确认目标目录下确实有 `SKILL.md`：例如 Windows 用户安装后的主入口位于 `$HOME/.agents/skills/comedy-shortform-writer/SKILL.md`。安装后新开一个 Codex 对话再试；还可在请求中直接写“请使用 comedy-shortform-writer Skill”。若只复制了仓库根目录下的 `skills/SKILL.md`，请按 README 安装完整的 `.agents/skills/` 目录。

### 只给出了大纲，没有剧本

检查是否调用了 `structure-sketch` 或 `structure-duo`。这两个入口只负责局部结构；要动作、对白和完整时间码，请改用 `comedy-shortform-writer`，并明确说“写完整短剧本”。

### 指定 60 秒，却得到 68 秒初稿

“以 60 秒为目标”允许初稿如实标注偏差并给剪辑建议。若必须不超 60 秒，写“成片候选稿，估算总时长不得超过 60 秒”，并要求实际删改、重排时间码。最终时长仍应以试读和拍摄计时确认。

### Skill 先提问，没有继续写

通常是核心创意、关键事实、制作限制或保留项互相冲突。回答决定性问题，或明确允许它采用哪种假设；不要让它暗自改掉原稿核心笑点。

### 想直接生成 AI 视频提示词

这套 Skill 交付的是剧本、结构和诊断，短剧本并不等于某个视频模型可直接执行的提示词。完成剧本后，再按目标模型的规格单独做分镜和提示词转换，并用实际模型结果验证。

## 8. 交稿前的人工检查

- 喜剧规则能否用一句“每当 X，角色就错误地做 Y”说清楚，且至少产生两种不同后果？
- 每次变化是否增加了新的代价、对象、信息或权力变化，而不是重复同一个包袱？
- 结尾是否兑现前面建立的规则或双人关系？
- 每个动作、道具、演员和场景是否符合拍摄条件？
- 时间码是否从 0 秒连续覆盖全稿，动作、对白和停顿的估算是否合理？
- 必须保留的原稿内容是否仍在？改稿说明是否如实描述了实际删改？
- 朗读和试拍后的计时、表演效果与目标观众反馈，是否支持继续制作？

## 参考

- [仓库 README 与安装说明](README.md)
- [主入口 Skill 原文](.agents/skills/comedy-shortform-writer/SKILL.md)
- [OpenAI：在 Codex 中用 `$` 显式调用 Skill](https://developers.openai.com/blog/eval-skills)
