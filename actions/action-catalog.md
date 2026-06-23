# 动作目录（Action Catalog）

## A1. CreateTaskFromAlert
- 输入：task_type, target_object_type, target_object_id, evidence, due_at, assignee_role
- 输出：task_id

## A2. SubmitApproval
- 输入：task_id, requester, approver, trigger_reason
- 输出：approval_id

## A3. ApproveOrReject
- 输入：approval_id, decision, comment
- 输出：approval_status, execution_status

## A4. CloseTaskWithPostmortem
- 输入：task_id, before_metrics, after_metrics, result_status, lessons_tag
- 输出：postmortem_id
