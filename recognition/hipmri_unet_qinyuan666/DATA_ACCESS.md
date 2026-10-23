# 第 1 步：获取 HipMRI 原始数据与说明

本次范围是取得真实数据、记录来源和原始标签说明，并检查下载完整性。
患者划分、2D 切片处理、训练和模型比较属于后续步骤。

## 官方来源与课程数据的关系

原任务文件 `COMP3710_Report_2026_draft_v2.2.pdf` 第 17 页给出的
HipMRI 链接是 [DOI 10.25919/45t8-p065](https://doi.org/10.25919/45t8-p065)。
它对应 CSIRO 的 [Labelled weekly MR images of the male pelvis](https://data.csiro.au/collection/csiro:51392)。
已通过官方接口核对 Version 2：

- [集合元数据](https://data.csiro.au/dap/ws/v2/collections/52549)。
- [文件清单](https://data.csiro.au/dap/ws/v2/collections/52549/data)。
- [原始 ZIP 下载](https://data.csiro.au/dap/ws/v2/collections/52549/data/58895460)。
- [BriefDataDescription.txt](https://data.csiro.au/dap/ws/v2/collections/52549/support/5034)。

集合的元数据版本是 2，但其数据文件名仍是
`HipMRI_study_complete_release_v1.zip`；文件名本身不能用来判断集合版本。
官方页面标明文件公开，许可为 CC BY-NC-ND 4.0。保留原始文件、许可和来源引用，
数据及标注不上传项目 GitHub 仓库。

**官方原始包包含 3D 体积，并不包含课程的 `keras_slices_data` 目录。**
当前模型仍然是 2D；得到这个原始包不等于已经得到课程预处理的 2D 切片，
也不代表现在可以直接把 3D 文件交给现有 2D 数据加载器。

## 本地文件与获取状态

以下路径均相对于本项目目录，位于 Git 忽略的 `private_data/` 中：

```text
private_data/
  downloads/HipMRI_study_complete_release_v1.zip
  hipmri_csiro_v2/
    semantic_MRs_anon/
    semantic_labels_anon/
  source_metadata/
    BriefDataDescription_v2.txt
    download_receipt.json
```

目录索引已核对：211 个 MRI 体积、211 个对应标注，按文件名中的 Case/Week
键可以配成 211 对，包含 38 个 Case 编号组和 Week0–Week7。
这些是原始 3D 体积的数量，不能当作 2D 切片数量。

下载和解压已完成：压缩包为 1,373,932,069 字节，与官方清单一致；ZIP CRC
校验通过，解压得到 422 个 NIfTI 文件。保存的 SHA-256 是本地计算的记录，
没有声称与官方公布的独立哈希比对。

另外按文件名排序选取首、中、末三对体积作获取后的基本检查：三对均为
`256×256×128`，图像与 mask 的形状和 affine 一致，图像及 mask 均为有限值，
mask 原始值均为整数 `0–5`。这不是所有体积的完整审计，也没有计算模型准确率。

完整汇总见 [results/data_source.json](results/data_source.json)。
本地原始报告保留在 `private_data/source_metadata/`。

## 原始数据的标签字典

以下映射直接来自上述 CSIRO `BriefDataDescription.txt`：

| 原始值 | 官方名称 | 含义 |
|---|---|---|
| 0 | Background | 背景 |
| 1 | Body | 身体 |
| 2 | Bones | 骨骼 |
| 3 | Bladder | 膀胱 |
| 4 | Rectum | 直肠 |
| 5 | Prostate | 前列腺 |

这是官方原始数据的定义。课程 2D 预处理是否保留这套编号，仍要与实际文件及
课程说明核对。不能直接使用论文列举类别时的顺序编号来替代 NIfTI 原始值。

官方说明指出，Week0 在治疗前采集，Week1–Week7 是治疗期间的每周扫描。
原始文件采用下面的配对形式：

```text
semantic_MRs_anon/Case_<编号>_Week<周数>_LFOV.nii.gz
semantic_labels_anon/Case_<编号>_Week<周数>_SEMANTIC_LFOV.nii.gz
```

这些模式来自实际压缩包目录。病例编号与患者身份的映射依据应在正式划分前记录清楚；
同一病例的不同 Week 及其切片不能分到不同数据集。当前没有生成训练/验证/测试划分。

## 已登录 Rangpur 后的最小核对

用户已确认可从自己的终端登录 Rangpur；助手环境的一次非交互连接在 22 端口超时。
当前尚未取得课程数据目录的实际输出，因此不能把登录成功视为已核对数据目录。

在已经登录的远程终端中，逐条执行：

```bash
hostname
python3 --version
ls -ld /home/groups/comp3710/HipMRI_Study_open/keras_slices_data
ls -1 /home/groups/comp3710/HipMRI_Study_open | head -20
ls -1 /home/groups/comp3710/HipMRI_Study_open/keras_slices_data | head -20
```

这些命令只打印版本、目录属性和前 20 个名称，不修改源数据，不启动训练。
如需更严格限制目录遍历，可使用已有的 [只读预检脚本](inspect_rangpur.py)，
操作见 [RANGPUR.md](RANGPUR.md)。实际目录输出和患者文件名保持私有。

还需确认：课程 2D 图像与 mask 如何配对、切片如何关联患者及周次、是否做过
标签重编码，以及课程预处理采用了什么方向和尺寸。
之后再选择取得课程切片，或从官方体积进行明确记录的 2D 预处理；本次不提前执行。

## 以往实验文件的用途

提供的 `COMP3710_Lab_2_2026_v2.01.pdf` 包含 Fourier/PCA/CNN、CIFAR10
及 OASIS 脑图像任务；`COMP3710_Lab_1.3.py` 是 Gaussian、sine 和 Gabor
示例。它们可参考课程概念和 GPU 使用方式，但没有提供 HipMRI 标签或患者映射。
Lab 2 的 OASIS 下载地址及现场演示要求不替代本项目任务文件中的 HipMRI 要求。

## 后续步骤的边界

本次仅完成数据获取与说明核对。尚未完成课程 2D 数据等价性确认、患者划分、
全数据空间/标签审计、真实 MRI 训练、测试集评估或失败案例分析。
现有高 Dice 图仍然来自合成数据。
