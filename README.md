# 跨境电商 Ontology PoC Playbook（Palantir Foundry）

> 仓库目标：用**最小可行本体（MVO）**在跨境电商场景中快速验证：
> 1) 业务语义建模速度；2) 数据到本体映射效率；3) AI 可直接调用本体对象/动作的可行性。

## 1. 为什么是 Ontology（不是传统“慢建模”）
传统数据中台通常先做“全量对象+全量逻辑”设计，周期长、跨团队协调重。Ontology 的核心价值是：
- 以业务对象为中心组织数据（Object / Property / Link）
- 以可执行语义承载流程（Action / Function）
- 让 AI 在“有权限、可追踪”的业务语义层中工作

你本次 PoC 的判定标准不是“模型是否完美”，而是：
- 是否能在 2~4 周内跑通一个端到端业务闭环
- 是否能让业务角色通过对象关系定位问题并触发动作
- 是否能让 AI 在该语义层稳定执行

## 2. 学习地图（你学到什么、位于体系哪一层）

| 学习知识点              | 在 Ontology 体系的位置 | 你要达到的能力                             |
| ----------------------- | ---------------------- | ------------------------------------------ |
| Object Type（对象类型） | 核心建模层             | 把“货号主档/库存/销售”等定义为统一业务对象 |
| Property（属性）        | Schema 层              | 区分主键、业务字段、状态字段、时间字段     |
| Link（关系）            | 对象关系层             | 设计货号→平台映射→库存/销售/内容的业务链路 |
| Action（动作）          | 执行层                 | 定义“建任务卡/发审批/更新状态”等可执行操作 |
| Function（函数）        | 计算层                 | 计算断货风险、低转化预警、内容缺失评分     |
| Workflow / App          | 应用层                 | 让运营、商品、投放按对象和动作协作         |
| Governance（权限治理）  | 安全层                 | 控制谁能看成本价、谁能触发审批             |
| AI + Ontology           | AI 执行层              | 让 AI 基于对象、关系、动作做检索与操作建议 |

## 3. 第一批核心对象（MVO）
你给出的对象非常适合作为第一批核心对象，建议保留：

1. 货号主档（ProductMaster）
2. 平台映射（PlatformListingMap）
3. 库存记录（InventoryRecord）
4. 销售记录（SalesRecord）
5. 内容资产（ContentAsset）
6. 流量转化（TrafficConversion）
7. 任务卡（TaskCard）
8. 审批记录（ApprovalRecord）
9. 复盘记录（PostmortemRecord）

> 最小实现建议：首周先启用前 6 个对象；第 2 周加 TaskCard + ApprovalRecord；第 3 周再加 PostmortemRecord。

## 4. 建议关系图（Link）
- ProductMaster 1:N PlatformListingMap
- ProductMaster 1:N InventoryRecord
- ProductMaster 1:N SalesRecord
- ProductMaster 1:N ContentAsset
- ProductMaster 1:N TrafficConversion
- ProductMaster 1:N TaskCard（可选）
- TaskCard 1:N ApprovalRecord
- TaskCard 1:N PostmortemRecord

## 5. 第一批动作（Actions）
建议只做 4 个动作，避免复杂化：
1. CreateTaskFromAlert：从异常指标生成任务卡
2. SubmitApproval：提交审批（价格/活动/库存）
3. ApproveOrReject：审批通过/驳回
4. CloseTaskWithPostmortem：任务关闭并写复盘

## 6. 第一批函数（Functions）
1. calc_stockout_risk(sku, market)：断货风险评分
2. calc_low_conversion_score(sku, platform, shop)：低转化评分
3. detect_content_gap(sku, platform)：内容缺失检测
4. summarize_action_effect(task_id)：动作前后效果摘要

## 7. 21 天 PoC 计划
### Week 1（建模与接数）
- 明确对象边界与主键
- 接入最小数据源（商品、库存、销售、流量）
- 跑通对象与关系

### Week 2（执行闭环）
- 上线 TaskCard + ApprovalRecord
- 配置 2 个预警函数（断货、低转化）
- 跑通“预警 -> 任务 -> 审批���

### Week 3（AI 与评估）
- 接入 AI 检索+动作触发
- 补 PostmortemRecord
- 评估建模效率、业务采纳率、执行成功率

## 8. 成功验收指标（建议）
- 建模效率：核心对象首版完成时间 <= 10 个工作日
- 问题定位时间：从发现异常到定位责任对象 <= 30 分钟
- 执行效率：任务闭环周期降低 >= 20%
- AI 可用性：AI 建议可执行率 >= 70%，越权率 = 0