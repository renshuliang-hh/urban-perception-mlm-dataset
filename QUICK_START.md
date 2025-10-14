# Quick Start Guide

## 🚀 数据集上传指南

### 1. 创建GitHub仓库

1. 访问 https://github.com/new
2. 仓库名: `urban-perception-mlm-dataset`
3. 描述: `Urban Perception Assessment with Multimodal Large Language Models and Street-View Imagery Dataset`
4. 设为公开仓库
5. 不要初始化README（我们已有完整文档）

### 2. 上传数据文件

#### 方法A: 通过GitHub网页界面（最简单）
1. 进入你创建的GitHub仓库
2. 点击 "uploading an existing file"
3. 拖拽以下文件和文件夹：
   - `README.md`
   - `LICENSE`
   - `data/` (整个文件夹)
   - `docs/` (整个文件夹)
   - `metadata/` (整个文件夹)

#### 方法B: 使用Git命令
```bash
git clone https://github.com/YOUR_USERNAME/urban-perception-mlm-dataset.git
cd urban-perception-mlm-dataset

# 复制准备好的文件
cp -r /tmp/github_upload/urban-perception-mlm-dataset/* .

git add .
git commit -m "Initial commit: Urban Perception Dataset"
git push origin main
```

### 3. 处理图片文件（选择一种方法）

#### 方法A: GitHub Releases（推荐）
```bash
# 在原始数据目录创建压缩包
cd /home/rsl/data/green_llm/benchmark_emotion

# 为每种情绪创建压缩包
for emotion in more_boring more_depressing livelier more_beautiful safer wealthier; do
    tar -czf "${emotion}_images.tar.gz" "$emotion"/train_image "$emotion"/test_image
done

# SFT数据集
cd /home/rsl/data/green_llm/SFT_boring_dataset
tar -czf "boring_images.tar.gz" boring_data/

# 然后在GitHub仓库页面：
# 1. 点击 "Releases"
# 2. 点击 "Create a new release"
# 3. Tag: v1.0.0-images
# 4. 上传所有 .tar.gz 文件
```

#### 方法B: Git LFS
```bash
git lfs install
git lfs track "*.jpg"
git lfs track "*.jpeg"

# 复制图片文件
rsync -av /home/rsl/data/green_llm/benchmark_emotion/*/train_image/ data/benchmark_emotion/
rsync -av /home/rsl/data/green_llm/benchmark_emotion/*/test_image/ data/benchmark_emotion/
rsync -av /home/rsl/data/green_llm/SFT_boring_dataset/boring_data/ data/sft_boring_dataset/boring_data/

git add .
git commit -m "Add images with Git LFS"
git push origin main
```

## 📊 最终数据集结构

```
urban-perception-mlm-dataset/
├── README.md                    # ✅ 项目主文档
├── LICENSE                      # ✅ MIT许可证
├── data/
│   ├── benchmark_emotion/       # ✅ 6种情绪数据
│   │   ├── beijing_data_case.csv
│   │   ├── more_boring/         # 更无聊评估
│   │   ├── more_depressing/     # 更抑郁评估
│   │   ├── livelier/           # 更有活力评估
│   │   ├── more_beautiful/     # 更美丽评估
│   │   ├── safer/              # 更安全评估
│   │   └── wealthier/          # 更富裕评估
│   └── sft_boring_dataset/     # ✅ SFT实验数据
├── docs/                       # ✅ 详细文档
│   ├── dataset_description.md   # 数据集说明
│   └── methodology.md          # 数据收集方法
└── metadata/                   # ✅ 数据统计信息
    └── data_statistics.json    # 完整统计
```

## 📋 数据内容概览

- **30,342个图像对** (6种情绪维度)
- **36,764张街景图像**
- **北京案例研究** (6条带反馈的样本)
- **SFT实验结果** (JSON格式)
- **完整文档** (方法论和描述)

## ⚠️ 重要提醒

1. **纯数据仓库**: 只包含数据和文档，无代码
2. **文件大小**: 图片文件约10GB，需要用GitHub Releases或Git LFS
3. **数据格式**: CSV (标注), JPG (图像), JSON (实验结果)
4. **使用许可**: MIT License，可自由使用

## 🔗 有用链接

- **数据集说明**: [docs/dataset_description.md](docs/dataset_description.md)
- **方法论**: [docs/methodology.md](docs/methodology.md)
- **数据统计**: [metadata/data_statistics.json](metadata/data_statistics.json)
- **GitHub大文件限制**: [GitHub documentation](https://docs.github.com/en/repositories/working-with-files/managing-large-files)

---

*数据集上传完成！这是一个纯数据仓库，为研究社区提供城市感知评估的宝贵资源。*