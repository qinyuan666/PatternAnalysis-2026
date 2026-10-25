# COMP3710 项目启动清单

选题已确定：HipMRI 2D 分割，标准 2D U-Net 基线，2D Improved U-Net 主模型（Normal），账号 s4906920。数据准备、两模型真实单轮 pilot、各 20 epoch 正式训练及按 Case 验证已完成，权重重载和预测输出已检查。固定测试 Dice/IoU 已完成；整病例测速已在用户关闭游戏后复测，保留首次受干扰记录。边界与失败分析及最终交付尚未完成。

## 现在从这里开始

1. 查看 [数据获取与本地位置](recognition/hipmri_unet_qinyuan666/DATA_ACCESS.md)：课程数据位于项目内的 `private_data/keras_slices_data/`，25,320 个文件和 12,660 对图像/标注均通过本地完整性检查。
2. [正式基线报告](recognition/hipmri_unet_qinyuan666/FORMAL_UNET.md) 与 [Improved U-Net 验证比较](recognition/hipmri_unet_qinyuan666/FORMAL_IMPROVED_UNET.md) 记录训练和验证。[最终测试结果](recognition/hipmri_unet_qinyuan666/TEST_RESULTS.md)：两模型前列腺像素汇总 Dice 为 0.8460 / 0.8495，病例平均为 0.8416 / 0.8406，均达到 0.75；尚不能宣称改进模型全面更好。
3. 中期材料保留在 [一页评估 PDF](recognition/hipmri_unet_qinyuan666/feasibility_review.pdf) 和 [中文讨论笔记](recognition/hipmri_unet_qinyuan666/MIDPOINT_NOTES_ZH.md)，描述当时的合成验证阶段。
4. 完整运行方法、实验记录和 AI 披露见 [项目 README](recognition/hipmri_unet_qinyuan666/README.md)。

当前 Improved U-Net 后台训练及验证均已完成，状态为 `completed`；
[查看日志与状态](recognition/hipmri_unet_qinyuan666/TRAINING_PLAN.md#当前后台任务)。
无需重新训练。固定测试评分及 [关闭游戏后的整病例复测](recognition/hipmri_unet_qinyuan666/CASE_BENCHMARK.md) 已完成，下一步是边界与失败案例分析。

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

最新课程说明、中期检查安排和最终提交日期以 Blackboard/course profile 为准。

- [x] 确定一个选题、主模型、基线模型和目标难度。
- [x] 本机运行环境和 GPU 已验证，已测量显存和耗时。
- [x] 已获取官方 HipMRI 原始数据包和标签说明，完成大小、ZIP CRC、配对清单和三个体积样本的基本检查。
- [x] 已收到 Rangpur 终端截图，确认六个相关目录、五组训练文件名的对应线索和可见数据使用条款；已补充来源致谢与引用。
- [x] 已下载并检查一对课程 2D 样本：图像/标注形状及 affine 一致、数值有限、标签为整数，现有读取函数通过。
- [x] 完整课程目录已下载，本地 gzip/NIfTI、配对、形状、affine 和有限整数标签检查通过；文件名中的病例编号跨 train/validate/test 无重叠，六项检查工具测试通过。
- [x] 采用官方标签字典并核对三个包含全部六类的训练病例；保留课程病例分组，生成哈希固定的私有 CSV，全部源文件哈希已复核。
- [x] 实现按比例缩放与补边，真实数据在 256 输入设置下保留全部标注像素；训练/预测模式一致，旧 checkpoint 行为保留。
- [x] 数据检查和模型流程已通过人工 NIfTI 测试、合成训练及真实数据单轮训练。
- [x] 准备一页可行性评估、PDF 和讨论笔记。
- [x] 完成真实 U-Net 基线试跑，测量六类别配置的损失、验证指标与 GPU 开销，检查权重重载和预测输出。
- [x] 完成按 Case 汇总的验证指标，固定两模型各 20 epoch 的正式训练预算。
- [x] 完成正式基线 20 epoch 训练、最佳权重重载、全部验证切片的 Case 评估及阳性切片示例检查。
- [x] 完成 Improved U-Net 真实六类单轮试跑、资源测量、权重重载与病例评估。
- [x] 完成 Improved U-Net 20 epoch 正式训练、验证指标核验、同切片预测展示与基线验证比较。
- [x] 完成固定测试集 Dice/IoU 及病例比较，两种聚合方式下前列腺 Dice 均达到 0.75。
- [x] 整病例测速已在用户关闭游戏后复测，原始受干扰记录保留，预测哈希与权重一致。
- [ ] 完成边界及失败案例分析。
- [ ] 本人在 practical 与 tutor 讨论，并确认 check-off 已登记。

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
- README 包含 `Artificial Intelligence Usage Disclosure`。本次 Codex 已辅助规划、代码、测试、合成实验和报告；学生仍需亲自理解代码并验证真实数据与结论。
- 截止前提交包含可运行版本的 GitHub PR，并将最终项目 README 导出为 PDF 交 Turnitin。
- 教师发布代码评审后，在课程指定窗口内回复并完成修改；窗口日期以课程通知为准。
