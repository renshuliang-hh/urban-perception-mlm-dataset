# Urban Perception Assessment with Multimodal Large Language Models and Street-View Imagery Dataset

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Dataset Size](https://img.shields.io/badge/Size-10%2B%20GB-blue.svg)](https://github.com/yourusername/urban-perception-mlm-dataset)
[![Python](https://img.shields.io/badge/Python-3.8%2B-green.svg)](https://www.python.org/)

## 📖 Overview

This comprehensive dataset is designed for research in **urban perception assessment** using **multimodal large language models (MLLMs)** and **street-view imagery**. It provides a systematic evaluation framework for understanding how AI models perceive and interpret various emotional and aesthetic aspects of urban environments.

The dataset supports research on:
- **Urban perception analysis** across multiple emotional dimensions
- **Multimodal learning** with street-view images and textual descriptions
- **Model evaluation** and enhancement strategies
- **Cross-cultural urban perception** studies
- **Fine-tuning datasets** for vision-language models

## 🗂️ Dataset Structure

```
urban-perception-mlm-dataset/
├── README.md                           # This file
├── LICENSE                             # MIT License
├── data/
│   ├── benchmark_emotion/              # 6-dimensional emotion perception data
│   │   ├── beijing_data_case.csv       # Beijing case study data
│   │   ├── more_boring/                # Boringness assessment
│   │   │   ├── more_boring_train.csv
│   │   │   ├── more_boring_test1.csv through test5.csv
│   │   │   ├── train_image/            # Training images
│   │   │   └── test_image/             # Test images
│   │   ├── more_depressing/            # Depression assessment
│   │   ├── livelier/                   # Liveliness assessment
│   │   ├── more_beautiful/             # Beauty assessment
│   │   ├── safer/                      # Safety assessment
│   │   └── wealthier/                  # Wealth assessment
│   └── sft_boring_dataset/             # SFT training data
│       ├── boring_data/                # Street-view images for SFT
│       └── experiment_results/         # Model evaluation results
├── docs/
│   ├── dataset_description.md          # Detailed dataset documentation
│   └── methodology.md                  # Data collection methodology
└── metadata/
    └── data_statistics.json            # Dataset statistics
```

## 📊 Dataset Components

### 1. Beijing Case Study Data (`beijing_data_case.csv`)
- **6 annotated cases** with detailed human feedback
- **Multiple emotion categories**: boringness, depression, liveliness, beauty, safety, wealth
- **Chinese and English labels** for cross-cultural studies
- **Rich textual feedback** explaining perception judgments

### 2. Multi-Dimensional Emotion Perception Data

#### 6 Emotional Dimensions:
1. **Boringness** (`more_boring/`)
   - Train: 1,348 pairs
   - Test: 5 × 500 pairs (test1-test5)
   - Images: 1,636 (train) + 2,660 (test)

2. **Depression** (`more_depressing/`)
   - Train: 1,821 pairs
   - Test: 5 × 500 pairs (test1-test5)
   - Images: 2,212 (train) + 3,440 (test)

3. **Liveliness** (`livelier/`)
   - Train: 3,389 pairs
   - Test: 5 × 500 pairs (test1-test5)
   - Images: 4,116 (train) + 3,040 (test)

4. **Beauty** (`more_beautiful/`)
   - Train: 3,101 pairs
   - Test: 5 × 500 pairs (test1-test5)
   - Images: 3,768 (train) + 3,200 (test)

5. **Safety** (`safer/`)
   - Train: 3,340 pairs
   - Test: 5 × 500 pairs (test1-test5)
   - Images: 4,064 (train) + 3,200 (test)

6. **Wealth** (`wealthier/`)
   - Train: 2,343 pairs
   - Test: 5 × 500 pairs (test1-test5)
   - Images: 2,848 (train) + 2,880 (test)

### 3. SFT Training Dataset (`sft_boring_dataset/`)
- **3,425 street-view images** from global cities
- **Model comparison results** with detailed reasoning
- **Multiple evaluation metrics** and token usage statistics
- **Benchmark results** for various MLLM architectures

## 🎯 Research Applications

### Primary Use Cases:
1. **Multimodal Model Training**: Fine-tune vision-language models for urban perception
2. **Benchmarking**: Evaluate model performance on urban understanding tasks
3. **Cross-Cultural Studies**: Compare perception patterns across different regions
4. **Feature Analysis**: Study which visual features influence perception judgments
5. **Model Enhancement**: Develop and test improvement strategies

### Supported Tasks:
- **Image Pair Comparison**: Choose which scene better represents a given emotion
- **Perception Scoring**: Rate urban scenes on emotional dimensions
- **Textual Explanation**: Generate reasoning for perception judgments
- **Zero-shot Evaluation**: Test model generalization to new urban environments

## 📁 Data Format

### CSV Files (Emotion Data)
```csv
choice,study_question,left_Image,right_Image
left,more boring,scene_A.jpg,scene_B.jpg
right,more beautiful,scene_C.jpg,scene_D.jpg
```

### Beijing Case Study
```csv
emotion_category,emotion_chinese,id,user_id,comparison_type,feedback,created_at,user_task_key
more_boring,更无聊,105,user123,more_boring,缺少绿地，遍布且规整的建筑，没有特色建筑,2025-05-13 23:12:03,task_key
```

### JSON Files (SFT Results)
```json
{
  "pair_id": "10",
  "scene_a": "case10_sceneA_TelAviv.JPG",
  "scene_b": "case10_sceneB_Toronto.JPG",
  "comparison_result": "Scene A is more boring because...",
  "model": "Qwen2.5-vl-7b-1",
  "usage": {
    "prompt_tokens": 385,
    "total_tokens": 420,
    "completion_tokens": 35
  }
}
```

## 🚀 Quick Start

### Download Dataset
```bash
git clone https://github.com/yourusername/urban-perception-mlm-dataset.git
cd urban-perception-mlm-dataset
```

### Data Access
This is a **data-only repository** containing:

1. **CSV files** with annotation data
2. **Image files** in JPG format
3. **JSON files** with experimental results
4. **Documentation** describing dataset structure and methodology

### Data Format Examples

**Emotion Comparison Data (CSV):**
```csv
choice,study_question,left_Image,right_Image
left,more boring,scene_A.jpg,scene_B.jpg
right,more beautiful,scene_C.jpg,scene_D.jpg
```

**Beijing Case Study (CSV):**
```csv
emotion_category,emotion_chinese,feedback
more_boring,更无聊,缺少绿地，遍布且规整的建筑，没有特色建筑
```

**SFT Results (JSON):**
```json
{
  "pair_id": "10",
  "scene_a": "case10_sceneA_TelAviv.JPG",
  "scene_b": "case10_sceneB_Toronto.JPG",
  "comparison_result": "Scene A is more boring because...",
  "model": "Qwen2.5-vl-7b-1"
}
```

## 📈 Dataset Statistics

| Dimension | Total Pairs | Training Pairs | Test Pairs | Total Images |
|-----------|-------------|---------------|-----------|--------------|
| Boringness | 3,848 | 1,348 | 2,500 | 4,296 |
| Depression | 4,321 | 1,821 | 2,500 | 5,652 |
| Liveliness | 5,889 | 3,389 | 2,500 | 7,156 |
| Beauty | 5,601 | 3,101 | 2,500 | 6,968 |
| Safety | 5,840 | 3,340 | 2,500 | 7,264 |
| Wealth | 4,843 | 2,343 | 2,500 | 5,728 |
| **Total** | **30,342** | **15,342** | **15,000** | **36,764** |

## 🏙️ Coverage

### Geographic Diversity:
- **Global Coverage**: Images from 50+ cities worldwide
- **Urban Types**: Downtown, residential, commercial, industrial areas
- **Cultural Context**: Both Western and Eastern urban environments

### Visual Features:
- **Architecture**: Building styles, density, height variation
- **Infrastructure**: Roads, public transport, utilities
- **Green Spaces**: Parks, trees, vegetation coverage
- **Human Activity**: Pedestrians, vehicles, commercial activity

## 📚 Related Research

This dataset supports research in:
- **Urban Computing**: Understanding cities through computational methods
- **Multimodal Learning**: Integrating visual and textual information
- **Environmental Psychology**: Human perception of built environments
- **AI Ethics**: Bias and fairness in urban perception models

## 📋 Data Usage Guidelines

### File Locations
- **Emotion data**: `data/benchmark_emotion/[emotion]/`
- **Beijing case study**: `data/benchmark_emotion/beijing_data_case.csv`
- **SFT results**: `data/sft_boring_dataset/`
- **Images**: Located in respective `train_image/` and `test_image/` folders

### Recommended Usage
1. **Load CSV files** using pandas, Excel, or your preferred data analysis tool
2. **Access images** using the provided file paths
3. **Reference documentation** in the `docs/` folder for detailed methodology
4. **Check metadata** for dataset statistics and information

### Data Citation
When using this dataset, please cite:
- The dataset itself (see citation below)
- The original research paper: *"Urban Perception Assessment with Multimodal Large Language Models and Street-View Imagery: A Systematic Evaluation of Accuracy and Enhancement Strategies"*

## 📄 Citation

If you use this dataset in your research, please cite:

```bibtex
@dataset{urban_perception_mlm_2024,
  title={Urban Perception Assessment with Multimodal Large Language Models and Street-View Imagery Dataset},
  author={shuliang ren},
  year={2024},
  publisher={GitHub},
  journal={GitHub repository},
  howpublished={\url{https://github.com/yourusername/urban-perception-mlm-dataset}}
}
```

## 📄 License

This dataset is released under the **MIT License**. See the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Original image sources from various street-view imagery providers
- Human annotators who provided detailed perception judgments
- Research community for feedback and validation

## 📞 Contact

For questions, suggestions, or collaboration opportunities:
- **Email**: renhusliang@stu.pku.edu.cn


---

**Note**: This dataset is provided for research purposes only. Users should comply with the terms of service of original image providers and respect privacy considerations.
