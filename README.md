# user spec

给长期项目的记忆。你和 agent 聊设计时，它边聊边把你的想法、需求、设计记进项目里的文档，按主题整理好。存和读都是自动的；compact 之后、换个会话、换个 harness，agent 读一遍就能接着干。

最关键的一点：**你的想法、需求、设计和 agent 的想法分开放。** CLAUDE.md、Claude Code 的 auto memory、Spec Kit / Kiro 也会把东西写进文档，但写进去以后，分不清哪句是你要的、哪句是 agent 自己推断的。user spec 里，spec 只放你说过或认可的；agent 选的做法记成决策，写明理由和放弃了的方案；它额外的想法标上「agent 注」。

## 它带来什么

- **随聊随记。** 和 agent 谈话过程中几乎所有的设计想法都会沉淀下来，compact 之后也记得住。agent 知道以前的设计原因和思路，能做出更好的设计。随口说的「以后要做」会挂进待办，还没想好的记成「未定」，为干活查过的资料也会留下来。记下的是你的想法，不是 agent 的猜测，以后的 agent 读到的就是你真正要的。

- **方便你回顾。** 翻一翻 user spec 就能回顾当前的设计。比起让 agent 讲一大串、每次说法还不一样，读同一份文档更熟悉；你给项目里的东西起的名字也记在一处，用词前后一致。里面都是你说过的话，所以你认得出自己。

- **agent 敢动旧代码。** agent 平时爱留旧接口、加兜底、让新旧两套并存，因为它不知道旧代码是不是你有意留的。在 user spec 里，spec 写着你真正要的，决策写着每个做法为什么在这、是不是随时可以重新考虑。知道哪些不能动，别的就敢删敢换，项目不会越堆越像屎山。

## 适合谁

维护长期项目、并且会和 agent 讨论设计的人。只下指令、不聊设计，就沉淀不出什么；做完就扔的小项目也用不上。

## 怎么用

### 安装

把这句话发给你的 agent：

> 把 https://github.com/realskc/user-spec 用 git clone 装成你的全局 skill，目录名叫 user-spec。

装完要是找不到这个 skill，重启一下工具。

也可以手动装：

```sh
git clone https://github.com/realskc/user-spec ~/.agents/skills/user-spec

# Claude Code 再加一个链接
mkdir -p ~/.claude/skills
ln -s ~/.agents/skills/user-spec ~/.claude/skills/user-spec
```

### 调用

在项目里调用一次：Codex 里输入 `$user-spec`，Claude Code 里输入 `/user-spec`，其他工具直接说「调用 user-spec」。新项目、已有项目都可以。

### 之后

什么都不用管，正常和 agent 聊天、干活就行。规则已经写进项目自己的 `AGENTS.md`（Claude Code 通过 `CLAUDE.md` 读到它），换一个没装这个 skill 的 agent 也照样生效。

### 已有项目

- 不动代码，只动文档。
- 已有的文档会被整理，可能换位置：技术文档放进 `docs/`，讨论稿放进 `user-spec/discussions/`，外部资料放进 `references/`。你亲手写的稿子、笔记、数据原地不动。改完会提交，不满意可以用 git 回退。
- 过去的理由找不回来。文档和这次对话里没提到的，决策里就写「当时的理由不清楚」。记忆从调用那一刻开始积累，用得越久越有用。
- 需要你花点时间：看起来像你的想法、但拿不准的，agent 会先问你；整理完还会请你通读一遍它整理出来的「你的想法」，拿不准的放在最前面。

## 会往项目里放什么

```
AGENTS.md          给 agent 的规则，也是你对工作方式的要求
CLAUDE.md          一行 @AGENTS.md，让 Claude Code 读到规则
TODO.md            待办：以后要做的事，每条指向详情
user-spec/         你的想法、需求、设计
  vision.md        离实现还远的想法
  concepts/        项目的词典：你给东西起的名字
  decisions/       决策：每个做法为什么这么选
  discussions/     讨论稿：讨论复杂时写给你反复看的讲解
references/        外部资料：查过的产品、论文、数据，带出处
docs/              技术文档：怎么实现的
```

刚调用完，这些文件几乎是空的。

## 特点

- **容量和你的想法成正比。** 你没说的，user spec 里就没有。agent 不会为了填满它去问你问题，也不会替你编需求。
- **内容是你的，整理是 agent 的。** 忠实于你的意思，由 agent 组织成连贯、脱离原会话也读得懂的文档；不替你补想法，不替你取舍。
- **记忆跟着项目走。** 都在仓库里，换会话、换 harness 都能用。规则也在项目里，不依赖这个 skill。

## 许可证

MIT
