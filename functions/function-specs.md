# 函数规格（Function Specs）

## F1. calc_stockout_risk(sku_code, market)
- 依赖对象：InventoryRecord, SalesRecord
- 输出：risk_score, risk_level

## F2. calc_low_conversion_score(sku_code, platform, shop_id)
- 依赖对象：TrafficConversion, SalesRecord
- 输出：low_conversion_score, diagnosis_tag

## F3. detect_content_gap(sku_code, platform)
- 依赖对象：ContentAsset, PlatformListingMap
- 输出：gap_count, gap_list

## F4. summarize_action_effect(task_id)
- 依赖对象：TaskCard, ApprovalRecord, PostmortemRecord
- 输出：before_after_delta, result_status, recommended_next_action
