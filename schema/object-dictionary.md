# 对象字典（Object Dictionary）

> 版本：v0.1（PoC）
> 目标：先保证能跑通，再逐步扩展字段与校验规则。

## 1) ProductMaster（货号主档）
| 字段        | 类型          | 必填 | 说明                    |
| ----------- | ------------- | ---- | ----------------------- |
| sku_code    | string        | Y    | 货号主键                |
| category    | string        | Y    | 品类                    |
| season      | string        | N    | 季节                    |
| color       | string        | N    | 颜色                    |
| size        | string        | N    | 尺码                    |
| cost        | decimal(18,2) | N    | 成本                    |
| supplier_id | string        | N    | 供应商ID                |
| image_path  | string        | N    | 主图路径                |
| status      | string        | Y    | 状态（active/inactive） |
| updated_at  | timestamp     | Y    | 更新时间                |