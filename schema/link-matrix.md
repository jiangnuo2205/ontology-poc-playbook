# 关系矩阵（Link Matrix）

| From          | To                 | Cardinality | 关系说明                            |
| ------------- | ------------------ | ----------- | ----------------------------------- |
| ProductMaster | PlatformListingMap | 1:N         | 一个货号可映射多个平台/店铺 Listing |
| ProductMaster | InventoryRecord    | 1:N         | 一个货号在多个市场/仓库有库存记录   |
| ProductMaster | SalesRecord        | 1:N         | 一个货号有多天多店销售记录          |
| ProductMaster | ContentAsset       | 1:N         | 一个货号可有多种内容资产            |
| ProductMaster | TrafficConversion  | 1:N         | 一个货号有多平台流量转化记录        |
| TaskCard      | ApprovalRecord     | 1:N         | 一个任务可触发多次审批流程          |
| TaskCard      | PostmortemRecord   | 1:N         | 一个任务可多次复盘                  |