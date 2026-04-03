# figma-skills-router

这是一个面向 Figma 工作流的 Skill 路由仓库。

它的目标不是重写 Figma 官方 skills，而是在保留官方内容的前提下，对外只暴露一个统一入口 skill：`figma-skills-router`。调用方只需要先加载这一个 router，再由它按任务目标分发到对应的参考 guide。

同时，这个仓库也收录了一个通用方法论 skill：`skill-router-creator`，用于沉淀“如何把多个 skills 聚合成一个单入口 router skill”的实践方式。

## 项目结构

```text
figma-skills-router/
├── figma-skills/                  # Figma 官方上游仓库，使用 submodule 引入
└── skills/
    ├── figma-skills-router/
    │   ├── SKILLS.md              # 面向 Figma 工作流的 router skill
    │   └── references/            # 官方 skills 的镜像参考资料
    └── skill-router-creator/
        └── SKILLS.md              # 通用的 skill router 设计方法论
```

### 目录说明

- `figma-skills/`
  - 上游 Figma 官方 skills 来源目录。
  - 保持只读，尽量不要在这个目录里做定制修改。

- `skills/figma-skills-router/SKILLS.md`
  - 本仓库真正对外提供的 skill。
  - 负责根据用户最终想要的产出物进行分流。

- `skills/figma-skills-router/references/`
  - 从上游镜像过来的参考资料目录。
  - 每个参考目录对应一个官方 Figma skill。
  - 这些参考资料保留了原始正文、参考文档和脚本，供 router 按需加载。

## 当前支持的路由目标

`figma-skills-router` 目前会将请求分发到以下 guide：

- `figma-implement-design`
  - 将 Figma 设计实现为仓库中的代码。
- `figma-use`
  - 直接在 Figma 中创建、编辑、删除或检查节点。
- `figma-generate-design`
  - 从代码或描述在 Figma 中生成整页或整屏设计。
- `figma-generate-library`
  - 在 Figma 中搭建设计系统、变量、组件库和 foundations。
- `figma-code-connect`
  - 处理 Code Connect 模板和映射。
- `figma-create-design-system-rules`
  - 生成项目级的 Figma 实现规范或规则文档。
- `figma-create-new-file`
  - 创建新的 Figma 或 FigJam 空白文件。

## 当前收录的 Skills

- `figma-skills-router`
  - 面向 Figma 工作流的单入口 router skill。
- `skill-router-creator`
  - 通用的 router skill 设计方法论，用于聚合多个已有 skills。

## 设计原则

- 只对外暴露一个 router skill，减少调用方选择成本。
- 官方 skills 作为参考资料保留，避免在上游正文上做大量二次改写。
- 按“最终交付物”分流，而不是按工具名分流。
- 对需要 `figma-use` 的复杂工作流，在 router 中明确组合依赖。

## References 的整理规则

`references/` 中的内容来自上游 `figma-skills/skills/`，同步时遵循以下规则：

- 官方 skill 主文档复制到本地后改名为 `GUIDE.md`
- `references/`、`scripts/`、`.d.ts` 等其余文件尽量原样保留
- 只做最小限度的机械化修正
  - 例如入口文件名替换
  - 例如文档内部相对链接修正
  - 例如修复已知错链

## 如何使用

如果你是这个仓库的使用方，直接从下面这个文件开始：

- [skills/figma-skills-router/SKILLS.md](./skills/figma-skills-router/SKILLS.md)

它会根据任务类型，把请求路由到最合适的参考 guide。

## 如何同步上游

当 Figma 官方 skills 更新后，推荐按下面的顺序同步：

1. 更新 `figma-skills` submodule
2. 将上游 `figma-skills/skills/` 下的 skill 目录重新镜像到 `skills/figma-skills-router/references/`
3. 将每个 skill 的入口文件统一整理为 `GUIDE.md`
4. 修正文档内部的相对链接
5. 检查是否存在新增、删除或改名的 skill

## 仓库定位

这个仓库本质上是一个“Figma skill 分发层”。

它更关注：

- 如何对外提供一个稳定、统一的 skill 入口
- 如何把官方 skills 整理成适合路由加载的参考结构
- 如何在保留上游可同步性的同时，降低调用侧的复杂度

而不是：

- 重写官方 Figma skills
- 改造官方脚本逻辑
- 在本仓库中实现新的 Figma MCP 能力
