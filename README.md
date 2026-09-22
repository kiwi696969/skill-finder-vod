# Skill · 让 AI 帮你找到所需的华为云技能

ICT 大赛云赛道赛题 1.9：在 AI 开发者空间中使用 `huawei-cloud-find-skills` 按意图快速检索华为云技能，并使用 `huawei-cloud-vod-collector` 将体验问题与需求缺口沉淀为结构化问题单（VOD），最后把流程提炼为可复用的方法论。全程只读/本地操作，不创建云资源、不产生费用。

## 一、可复用方法论

**任意华为云服务场景：先找技能 → 没有/不满足就提问题单。**

```
用户意图
   │
   ▼
① 搜索：huawei-cloud-find-skills 按关键词/类目检索（名称+触发词+描述评分排序）
   │
   ▼
② 详情确认：查看 SKILL.md，确认功能是否匹配意图
   │
   ├── 匹配 → ③ 安装（npx skills add）→ 按需使用
   │
   └── 缺失/不满足 → ④ 反馈：huawei-cloud-vod-collector 沉淀为 VoD 问题单
                            → ⑤ 同步为 GitCode Issue，供产品团队跟踪
```

## 二、实操证据

### 第 1 步：按意图快速找技能

在 AI Shell 中表达需求："帮我找找华为云有没有管理 ECS 的技能？"

`huawei-cloud-find-skills` 实测输出（关键词 `管理 ECS` / `查询 ECS 计算资源`）：

- 命中 **25 个**相关技能，按评分排序
- **huawei-cloud-computing-query**（26 分）高居前列：覆盖 ECS/BMS/IMS/AS 实例、规格、密钥对、镜像、伸缩组等查询能力
- 其他候选：huawei-cloud-terraform-generator、huawei-cloud-ces-ecs-monitoring、huawei-cloud-ecs-dsh-deploy 等

### 第 2 步：安装技能

```bash
npx skills add https://gitcode.com/huaweicloud/huaweicloud-skills.git#master --skill huawei-cloud-computing-query -y
```

安装完成，技能可用于 ECS/BMS/IMS/AS 查询。

### 第 3 步：体验问题沉淀为 VoD 问题单

实测中发现缺口：`huawei-cloud-computing-query` 覆盖 ECS/BMS/IMS/AS，但**缺少 CCE 云容器引擎查询能力**。使用 `huawei-cloud-vod-collector` 一键沉淀为结构化问题单：

- 文件：`.vod/feedbacks/VOD-20260922-0001.md`（本仓库内）
- 结构：feedback_id / 类型 / 问题描述 / 复现场景 / 预期行为 / user_intent / agent_action / recurrence_count
- 已同步为 GitCode Issue：https://gitcode.com/developer-skill/vod-skill/issues/577

## 三、技能与工具

| 能力 | 技能/工具 | 作用 |
|------|----------|------|
| 搜索技能 | huawei-cloud-find-skills | 关键词/类目搜索 + 评分排序 + 一键安装 |
| 反馈收集 | huawei-cloud-vod-collector | 体验问题沉淀为结构化 VoD，同步 GitCode Issue |
| 两个技能均只读/本地 | — | 不创建云资源、不产生费用 |

## 四、核心收获

1. 技能库数百个技能，手动翻找效率低——让 AI 按意图检索 + 评分排序最省力；
2. 技能缺口不该被吞掉——VoD 把"不好用"变成产品团队可跟踪的高价值输入；
3. 完整闭环：**搜索命中 → 安装使用 → 发现缺口 → 提 VoD**，既是使用流程，也是反馈流程。