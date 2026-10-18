# English Vocabulary Video Prompts

A reusable Codex skill for English vocabulary teaching video prompts, designed around **“This is the …”** and **two seconds per vocabulary item**. Intended for Google Flow by default; you can name another video tool.

可复用的 Codex Skill，用于编写英语词汇教学视频提示词。默认面向 **Google Flow**，采用 **“This is the …”** 句式，**每个词条严格 2 秒**。也可以指定其他视频工具。

## English

### What it does

- Writes complete English prompts, ready to paste into a video tool; it does not generate videos automatically.
- Uses the person in your uploaded reference image. Without an image or another explicit character choice, it uses **Milo**, an adult male English teacher.
- Preserves the vocabulary order. Multiword phrases count as one item.
- Groups up to five items per video: each full group is 10 seconds; any remaining items form a separate video at two seconds per item.
- Uses a silent 0.5-second quiz followed by a 1.5-second answer window. The presenter reads the answer sentence exactly once.
- Includes English-only subtitles, yellow answer highlighting, static shots, and hard cuts.
- Asks before changing the requested duration. Explicit grouping requests take precedence.

### Install

Copy this repository's `english-vocab-video-prompts` folder into your Codex skills directory (`$CODEX_HOME/skills`, or `~/.codex/skills` by default). `SKILL.md` must be directly inside that folder. Reload your skill list or start a new session if necessary.

Alternatively, clone the repository directly into the default skill directory:

```bash
git clone https://github.com/leehongkuan/english-vocab-video-prompts.git ~/.codex/skills/english-vocab-video-prompts
```

### Use

Invoke the skill and provide your words. Attach a character image if you want a custom presenter.

```text
Use $english-vocab-video-prompts to write Google Flow prompts for:
Truck, Bulldozer, Excavator, Concrete Mixer, Crane, Forklift, Loader, Road Roller.
```

Result: two independently usable English prompts — **10 seconds for the first five items, then 6 seconds for the remaining three**. Without an image, both use Milo.

```text
Use $english-vocab-video-prompts with the person in my uploaded image as Lumi.
Vocabulary: Windshield, Hood, Trunk.
```

Result: one **6-second** prompt with the reference-image presenter.

You can explicitly override grouping, for example: “Make the eight items into two 8-second clips.” No image is needed for the default Milo presenter.

### Timing examples

| Items | Clip durations |
|---:|---|
| 1 | 2 seconds |
| 3 | 6 seconds |
| 5 | 10 seconds |
| 6 | 10 + 2 seconds |
| 8 | 10 + 6 seconds |
| 10 | 10 + 10 seconds |
| 13 | 10 + 10 + 6 seconds |

These are requested prompt timings, not a guarantee of model output or platform-supported export lengths. If a generation tool rejects a duration, choose a workaround before changing timing. The skill does not automatically pad or repeat words. Concrete singular nouns and noun phrases work best with the requested sentence frame.

## 中文

### 功能

- 输出可直接复制的完整英文提示词，不自动调用视频生成或产生生成费用。
- 上传人物参考图时，以图片中的人物为主角；没有图片且未另行指定人物时，默认使用成年男英语老师 **Milo**。
- 保持单词原始顺序；`Concrete Mixer` 等词组按一个词条计算。
- 每 5 个词条组成一个 10 秒视频；剩余词条单独成段，时长为“剩余词条数 × 2 秒”。不足 5 个同样按词条数 × 2 秒计算。
- 每个词条先静默出题 0.5 秒，再用 1.5 秒揭晓并完整读一句，只读一次。
- 英文字幕、黄色答案高亮、固定镜头、硬切转场。
- 改动时长前先询问用户；用户明确指定的分段方式优先。

### 安装

将仓库文件夹 `english-vocab-video-prompts` 放入 Codex 的 skills 目录：默认是 `~/.codex/skills`，如已设置 `CODEX_HOME` 则使用其下的 `skills` 目录。确保 `SKILL.md` 直接位于该文件夹内。必要时刷新技能列表或开启新会话。

也可以直接使用上方的 `git clone` 命令安装。

### 使用示例

```text
使用 $english-vocab-video-prompts，为下面的单词生成 Google Flow 英文提示词：
Truck、Bulldozer、Excavator、Concrete Mixer、Crane、Forklift、Loader、Road Roller。
```

输出：前 5 个词为 **10 秒**，后 3 个词为 **6 秒**，共两段完整英文提示词。无参考图时使用 Milo。

```text
使用 $english-vocab-video-prompts，以上传图片中的人物为 Lumi。
单词：Windshield、Hood、Trunk。
```

输出：一段 **6 秒**的完整英文提示词，使用图片中的人物。

如需自定义分组，可明确写：“这 8 个词做成两个 8 秒视频。”默认规则不会擅自覆盖你的明确要求。

提示词中的时长是生成目标，不代表平台一定支持该导出长度，也不保证生成模型完全遵守。遇到平台时长限制时，先商量处理方式，不自动延长或重复。该句式最适合具体的单数名词和名词词组。

## Files / 文件

- `SKILL.md`: skill instructions / 技能指令。
- `agents/openai.yaml`: Codex display metadata / Codex 展示信息。
- `README.md`: English and Chinese usage / 中英双语使用说明。
