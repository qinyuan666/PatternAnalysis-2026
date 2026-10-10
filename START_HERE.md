# COMP3710 项目启动清单

当前目标是准备中期可行性检查材料。选题已确定：HipMRI 2D 分割，标准 2D U-Net 基线，2D Improved U-Net 主模型（Normal）。学生信息和检查日期待确认；真实数据尚未提供。

## 仓库

- 工作仓库 / 课程 Fork（`origin`）：https://github.com/qinyuan666/PatternAnalysis-2026.git
- 课程仓库（`upstream`）：https://github.com/shakes76/PatternAnalysis-2026.git
- 保留的原仓库（`original`）：https://github.com/qinyuan666/comp3710-Final.git
- 本地开发分支：`topic-recognition`
- 分支跟踪：`origin/topic-recognition`；默认推送远端：`origin`。
- 开发起点：课程 `topic-recognition` 分支的提交 `552b9029a3fbee3e12d0b4e95f38e73d8d1d51a5`。

已在 GitHub 创建并通过 API 验证真实 Fork：`qinyuan666/PatternAnalysis-2026` 的 `fork` 为 `true`，`parent.full_name` 为 `shakes76/PatternAnalysis-2026`，且存在 `topic-recognition` 分支。本地已关联该分支。

原 `comp3710-Final` 是独立空仓库，保留不变；后续课程开发使用真正的 Fork。开发记录以 `git log` 为准。

最终 PR 的目标仓库和分支为 `shakes76/PatternAnalysis-2026:topic-recognition`，来源为 `qinyuan666/PatternAnalysis-2026:topic-recognition`。只有完成可运行版本和报告后，才创建课程提交 PR。

## 首次开发前

- [ ] 在 Blackboard/course profile 确认最终任务说明、中期检查日期和最终截止日期。当前参考 PDF 仍标为 DRAFT，未列具体日期。
- [x] 确定一个选题、主模型、基线模型和目标难度。
- [ ] 确认数据访问权限、运行环境和 GPU/显存预算。
- [ ] 明确数据划分方法和验收指标；医疗图像须按患者划分，避免同一患者跨集合。
- [ ] 建立数据检查及可视化，跑通少量样本的训练、保存、加载和预测流程。
- [ ] 准备一页可行性评估，并在规定时间内完成 tutor check-off。

已确认路线：HipMRI 标准 2D U-Net 基线，2D Improved U-Net（Normal）主模型，并在相同患者划分上比较。项目位置：`recognition/hipmri_unet_qinyuan666/`。

## 确认选题后的代码结构

在 `recognition/<有意义的项目名>/` 中实现：

| 文件 | 职责 |
| --- | --- |
| `modules.py` | PyTorch 或 TensorFlow 模型组件 |
| `dataset.py` | 数据加载、预处理、无泄漏划分和增强 |
| `train.py` | 训练、验证、测试、保存模型及训练曲线 |
| `predict.py` | 加载已训练权重，预测并展示结果 |
| `README.md` | 最终技术报告、可行性评估及复现说明 |

实现真实功能后再添加相应文件。依赖版本、随机种子、实验配置和数据划分应记录并可复现。模型权重保存在本地或课程允许的存储位置，报告说明如何获得或重新训练。

## 开发记录和最终交付

- 每完成真实的小里程碑，提交对应代码和清晰的 commit message；不在最后一次性提交全部工作。
- 数据集和模型文件不得提交；报告用图可放在项目内的 `figures/` 目录。提交前检查 `git status` 和暂存内容。
- 主模型与已实现基线使用相同评估划分；记录任务指标、参数量、峰值显存和推理时间。
- 分析 3–5 个真实失败案例，并给出有证据支持的工程建议。
- 最终 README 包含可行性评估、运行步骤、精确依赖版本、实验和引用。
- 最终 README 必须包含 `Artificial Intelligence Usage Disclosure`，如实说明工具、用途及验证方式。本次已使用 Codex 辅助阅读任务说明和准备仓库；尚未生成或验证模型代码。
- 截止前提交包含可运行版本的 GitHub PR，并将最终项目 README 导出为 PDF 交 Turnitin。
- 教师发布代码评审后，在课程指定窗口内回复并完成修改；窗口日期以课程通知为准。
