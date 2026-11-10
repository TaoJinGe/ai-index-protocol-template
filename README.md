# AI 编程文件系统索引协议 · 模板仓库

> 一套让 AI 先读规则、建索引、再精准改代码的协议。
> 本仓库是它的 **GitHub Template**：用它开一个新仓库，`docs/` 骨架和项目级 `AGENTS.md` 会一起就位。

**English**: A GitHub template for the AI-Coding / Vibe-Coding File System Index Protocol.
Create a new repository from it, and the `docs/` skeleton plus a project-level `AGENTS.md` come pre-wired.

---

## 快速开始（三步）

**1. 用模板建仓库**

在本仓库页面点 **Use this template → Create a new repository**，输入你自己的项目名。

这样得到的是一份**干净的新仓库**：没有本仓库的提交历史，`docs/` 骨架和四个索引目录都已就位。

**2. 克隆到本地**

```bash
git clone https://github.com/<你的账号>/<你的项目名>.git
cd <你的项目名>
```

**3. 第一次接入：让 AI 只建索引，别改代码**

在 DSH / Claude Code / Cursor 等支持 `AGENTS.md` 的 Agent 里，直接说：

```text
按 docs/AI_SYSTEM_RULES.md 接入本项目：先读 docs/AI_SYSTEM_RULES.md
和 docs/AI项目开发补充指南.md，然后基于当前真实文件系统生成
docs/root/、docs/tree/、docs/flow-root/、docs/flow-tree/ 四类索引。
本次只生成索引，不修改任何业务代码；无法确认的链路标记为「待确认」，不要编造。
```

> 这一步是**唯一需要手动点火的一次**。之后每次开发，Agent 都会先读索引再动手，
> 相关内容已写进本仓库根目录的 `AGENTS.md`，不会再出现「忘了先建地图就乱改代码」。

---

## 仓库结构

```text
.
├── AGENTS.md                       # 项目级触发器：强制读规则、缺索引先建、改完回写
├── README.md                       # 本文件
├── LICENSE
└── docs/
    ├── AI_SYSTEM_RULES.md          # 唯一规则文件（不可拆分）
    ├── AI项目开发补充指南.md         # 项目级补充（可裁剪，路径不可改）
    ├── root/.gitkeep               # 一级目录索引 ROOT_MAP_*.md 生成于此
    ├── tree/.gitkeep               # 二级文件索引 <path>.md 生成于此
    ├── flow-root/.gitkeep          # 功能域总览 FLOW_ROOT_MAP_*.md 生成于此
    └── flow-tree/.gitkeep          # 功能链路 FLOW_*.md 生成于此
```

### 四个目录为什么是空的

不是漏了，是**故意的**。`AI_SYSTEM_RULES.md` 第六章写死一条红线：

> 索引必须来源于真实文件系统，**不允许预设不存在结构**。

所以模板里只放 `.gitkeep` 占位，保证 `Use this template` 出来的新仓库能保留这四个目录，
但绝不预填任何示例索引——预填的假索引会被 AI 当成真实地图，比没有索引更危险。

判断规则很简单：**目录在、只有 `.gitkeep` ＝ 尚未接入，需要先跑第 3 步。**

---

## 这套协议在解决什么

AI 编程真正危险的地方通常不是「不会写代码」，而是：

- 不知道该改哪个文件 → 全项目扫描，烧掉上下文
- 不知道一个按钮背后牵着哪些接口和数据表
- 改动范围不可控，新功能覆盖旧功能
- 项目越改越乱，几个月后连作者自己都忘了链路

协议用两张地图解决：

| 地图 | 文件 | 回答什么问题 |
|---|---|---|
| 文件地图 | `docs/root/` + `docs/tree/` | **我该改哪个文件？** |
| 功能链路地图 | `docs/flow-root/` + `docs/flow-tree/` | **我改这里会影响谁？** |

配套的强制约束：单文件 ≤ 300 行、单文件单职责、`FLOW_ID` 唯一编号、修改前后必须同步索引。

完整规则见 [`docs/AI_SYSTEM_RULES.md`](docs/AI_SYSTEM_RULES.md)，
项目级补充见 [`docs/AI项目开发补充指南.md`](docs/AI项目开发补充指南.md)。

---

## 兼容性

- **GitHub**：本仓库已开启 Template 功能，可直接 Use this template
- **Agent**：依赖 `AGENTS.md` 约定；同时兼容 Claude Code 的 `CLAUDE.md`
  （`~/.dsh/AGENTS.md` 之类的用户全局规范会与项目级 `AGENTS.md` 同时生效，
  内容完全相同时会自动去重，不会重复占用上下文）
- **项目类型**：适合中大型站点、SaaS、管理后台、多页面工具站，以及需要长期维护的项目；
  一次性小 Demo、单页静态页用它属于杀鸡用牛刀

## License

[MIT](LICENSE)
