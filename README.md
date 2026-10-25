# English-skill

专四英语口语思辨陪练的开源 Agent Skill。它把“开口练英语思辨”变成一个可循环的陪练闭环：AI 抛出英文话题并给出一正一反两句参考句型，你口头作答后，AI 做“转写 → 优化 → 点评”，重点纠正中式英语。

## 1. 项目解决什么问题

- 专四口语思辨题“没话说、不敢开口”：先给话题和正反参考句型，降低开口门槛。
- 中式英语无人纠：中文直译语序、中式搭配、逻辑断层、母语负迁移等问题，逐句指出并改成地道口语。
- 练一次就断：用【继续】/【重新回答】把一个话题练到透，而不是只给答案就结束。
- 纯文本即可使用：**无需联网、无需 PDF、无图形界面、无外部 API 依赖**。

## 2. 主要功能

- **话题输出**：每轮给出一个英文思辨 Topic，并附**两句纯英文参考句型**（一句肯定立场、一句否定立场）。
- **三项反馈**（作答后）：
  - ①【我的原句】：原样转写口述英文，保留原始表达；
  - ②【优化句】：只给 **1 版**适配专四口语的改写，优先修正中式英语，**改动核心内容加粗**，拒绝浅层同义词替换，不过度书面化；
  - ③【简短点评】：点明本次中式英语问题，并评价逻辑、句式、用词地道度。
- **循环训练**：
  - 【继续】——不换话题，AI 做深度追问（补论据、反方驳斥、举例等），开启新一轮作答；
  - 【重新回答】——不换话题，等你重新作答后再次反馈，可循环直到【继续】。
- **中文作答兼容**：可用中文作答，AI 会保留中文原句并给出对应英文表达与点评。

## 3. 安装方法

本 Skill 是一个纯文本文件夹，无需安装依赖、无需联网：

1. 把整个 `English-skill/` 文件夹复制到你的 Agent 技能目录，例如：

   ```
   workspace/.user_skills/English-skill/
   ```

   （或使用支持 Agent Skills 的客户端，直接“导入 / 添加技能”选择本文件夹。）

2. 确认目录结构如下：

   ```
   English-skill/
   ├── SKILL.md          # 元数据 + 陪练流程与输出规范（核心）
   └── agents/
       └── openai.yaml   # UI 展示元数据
   ```

3. 重启或刷新 Agent / 客户端，使技能被加载。

> 校验结构（可选）：`python <skill-creator>/scripts/quick_validate.py English-skill`，输出 `Skill is valid!` 即正常。

## 4. 使用方法

1. 加载技能后，向 AI 发起一句指令开始训练，例如：

   > 用 English-skill 开始一轮专四口语思辨训练。

2. AI 会输出英文话题 Topic 和正反两句参考句型，然后**等待你作答**。
3. 你用英文（或中文）口述你的观点。
4. AI 按【我的原句】→【优化句】→【简短点评】反馈，并给出【继续】/【重新回答】两个选项。
5. 选择下一步：
   - 输入 **【继续】**：在当前话题上被深度追问，继续作答；
   - 输入 **【重新回答】**：同一话题重新作答并再次反馈，直到输入【继续】。

## 5. 输入 / 输出示例

### 输入（AI 开局 + 用户作答）

```
Topic: Should college students take part-time jobs during the semester?

参考句型（正方）：I believe taking part-time jobs in college is worthwhile because it builds real-world skills early.
参考句型（反方）：While part-time jobs sound attractive, I'd rather focus on my studies because they matter more for the future.

> 用户作答：I think student should do part-time job, because it can improve my ability and also can earn some money.
```

### 输出（AI 三项反馈 + 选项）

```
①【我的原句】
I think student should do part-time job, because it can improve my ability and also can earn some money.

②【优化句】
I think students should **take part-time jobs**, because **they help us gain practical skills** and **let us earn some money at the same time**.

③【简短点评】
“student”缺复数、用词重复（can…can…）是典型中式英语；句式用“also”硬拼接导致逻辑松散。优化后补全主语复数、用“gain practical skills”替代中式“improve my ability”，逻辑更连贯、更口语。

【继续】
【重新回答】
```

### 分支示例：选择【继续】（同话题深度追问）

```
深挖一问：You chose part-time jobs — but what if working takes too much time and hurts your grades? How would you balance them?
```

## 边界说明

- 不支持网页抓取、读取 PDF、图形界面、外部 API。
- 不做语法讲解课，只做“作答 + 反馈”的陪练闭环。

## License

本项目采用 [MIT License](LICENSE)。本 Skill 为纯文本指令，无第三方代码或版权素材。
