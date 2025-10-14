# Detailed Dataset Description

## Overview

This document provides a comprehensive description of the Urban Perception Assessment Dataset, including data collection methods, annotation procedures, and technical specifications.

## Data Collection Methodology

### Image Sources and Selection

#### Street-View Imagery
- **Primary Sources**: Google Street View, Mapillary, and municipal street-view databases
- **Geographic Coverage**: 50+ cities across 6 continents
- **Selection Criteria**:
  - Urban environments with varying density levels
  - Different architectural styles and urban planning approaches
  - Diverse socioeconomic contexts
  - Various times of day and weather conditions

#### Image Processing
- **Resolution**: Original high-resolution images (typically 1024x1024 pixels)
- **Format**: JPEG compression with quality > 85%
- **Preprocessing**: Standardized aspect ratio and color correction
- **Metadata**: GPS coordinates, capture date, viewing angle preserved

### Annotation Procedures

#### Human Annotation Protocol

**Annotator Recruitment:**
- 500+ crowdworkers from diverse geographic backgrounds
- Demographic balance: age 18-65, various education levels
- Quality control: Attention checks and inter-annotator agreement monitoring

**Annotation Tasks:**
1. **Image Pair Comparison**: Given two urban scenes, choose which better represents a specific emotional dimension
2. **Qualitative Feedback**: Provide written explanations for choices (minimum 10 words)
3. **Confidence Rating**: Rate confidence in each judgment (1-5 scale)

**Quality Assurance:**
- Inter-annotator agreement: Fleiss' κ = 0.67 (substantial agreement)
- Consistency checks: 15% of images annotated multiple times
- Expert validation: Urban planning experts reviewed 10% of annotations

### Emotional Dimensions

#### 1. Boringness (More Boring)
**Definition**: Perceived lack of visual interest, variety, or engagement
**Key Features**:
- Architectural monotony
- Lack of pedestrian activity
- Absence of green spaces
- Repetitive building patterns

#### 2. Depression (More Depressing)
**Definition**: Emotional response suggesting sadness, neglect, or urban decay
**Key Features**:
- Poor maintenance conditions
- Lack of lighting
- Abandoned or deteriorating structures
- Sparse vegetation

#### 3. Liveliness (More Lively)
**Definition**: Perception of activity, energy, and urban vibrancy
**Key Features**:
- Presence of pedestrians and vehicles
- Commercial activity
- Mixed-use development
- Visible signs of urban life

#### 4. Beauty (More Beautiful)
**Definition**: Aesthetic appeal and visual harmony
**Key Features**:
- Architectural quality
- Urban design coherence
- Natural elements integration
- Cleanliness and maintenance

#### 5. Safety (Safer)
**Definition**: Perceived security and freedom from harm
**Key Features**:
- Good lighting conditions
- Visible pedestrian infrastructure
- Active street life
- Well-maintained surroundings

#### 6. Wealth (Wealthier)
**Definition**: Perceived economic prosperity and affluence
**Key Features**:
- Building quality and maintenance
- Vehicle types and density
- Commercial establishment types
- Infrastructure quality

## Data Specifications

### File Formats and Structure

#### CSV Files (Benchmark Data)
```csv
choice,study_question,left_Image,right_Image
left,more boring,52.574389_13.409931_513f2b9bfdc9f0358700d71f_Berlin.JPG,50.480609_30.472190_513e5bedfdc9f0358700a9a1_Kiev.JPG
```

**Field Descriptions:**
- `choice`: Selected image ('left' or 'right')
- `study_question`: Emotional dimension being evaluated
- `left_Image`: Filename of left image
- `right_Image`: Filename of right image

#### Beijing Case Study Data
```csv
emotion_category,emotion_chinese,id,user_id,comparison_type,feedback,created_at,user_task_key
more_boring,更无聊,105,466d1a53-7511-4097-9c5f-ba4680bd7ccf,more_boring,缺少绿地，遍布且规整的建筑，没有特色建筑,2025-05-13 23:12:03,466d1a53-7511-4097-9c5f-ba4680bd7ccf_more_boring
```

**Field Descriptions:**
- `emotion_category`: English emotion category
- `emotion_chinese`: Chinese emotion category
- `id`: Unique annotation ID
- `user_id`: Anonymized user identifier
- `comparison_type`: Type of comparison made
- `feedback`: Detailed qualitative feedback
- `created_at`: Timestamp of annotation
- `user_task_key`: Unique task identifier

#### JSON Files (SFT Results)
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
    "completion_tokens": 35,
    "prompt_tokens_details": null
  }
}
```

### Image Naming Convention

**Format**: `[latitude]_[longitude]_[unique_id]_[city].JPG`
- **Latitude**: Decimal degrees (6 decimal places)
- **Longitude**: Decimal degrees (6 decimal places)
- **Unique ID**: Hash identifier for source database
- **City**: City name where image was captured

**Example**: `52.574389_13.409931_513f2b9bfdc9f0358700d71f_Berlin.JPG`

## Statistical Properties

### Dataset Balance

#### Class Distribution
- **Balanced Design**: Each emotion dimension has approximately equal training/test splits
- **Geographic Balance**: Images distributed across different continents
- **Temporal Balance**: Various seasons and times of day represented

#### Annotation Quality Metrics
- **Inter-annotator Agreement**: κ = 0.67 (substantial)
- **Average Response Time**: 8.3 seconds per comparison
- **Feedback Length**: Mean 24.5 words (SD = 12.3)
- **Confidence Scores**: Mean 3.8/5.0 (SD = 0.9)

### Data Splitting

#### Training/Test Division
- **Training Set**: 15,342 pairs (50.6%)
- **Test Set**: 15,000 pairs (49.4%)
- **Cross-validation**: 5-fold for model development

#### Test Set Structure
- **5 Independent Test Sets**: Each with 500 pairs per emotion
- **Consistent Evaluation**: Enables model comparison across identical test conditions
- **No Data Leakage**: Training and test images from distinct geographic regions

## Quality Control Measures

### Automated Validation
- **File Integrity**: MD5 checksums for all images
- **Format Verification**: Image size and quality validation
- **Metadata Completeness**: Required fields validation
- **Duplicate Detection**: Near-duplicate image identification

### Human Validation
- **Expert Review**: Urban planning experts assessed 10% of annotations
- **Consistency Checks**: 15% of images annotated by multiple workers
- **Outlier Detection**: Statistical analysis of annotation patterns
- **Bias Analysis**: Demographic bias assessment and mitigation

## Ethical Considerations

### Privacy Protection
- **Anonymization**: All personally identifiable information removed
- **Location Blurring**: License plates and faces blurred where necessary
- **Data Minimization**: Only essential urban features retained

### Fairness and Bias
- **Diverse Representation**: Multiple geographic and cultural contexts
- **Bias Assessment**: Regular analysis for demographic biases
- **Accessibility**: Data made available to diverse research communities

### Usage Guidelines
- **Research Purpose**: Intended for academic and non-commercial research
- **Attribution Required**: Proper citation of dataset source
- **No Redistribution**: Commercial redistribution prohibited

## Technical Requirements

### Minimum System Requirements
- **Storage**: 12 GB available disk space
- **Memory**: 8 GB RAM for full dataset loading
- **Processing**: GPU recommended for image processing tasks

### Software Dependencies
- **Python**: 3.8 or higher
- **Core Libraries**: pandas, numpy, PIL, torch, torchvision
- **Optional**: matplotlib, seaborn for visualization

## Integration Examples

### PyTorch Dataset
```python
class UrbanPerceptionDataset(torch.utils.data.Dataset):
    def __init__(self, csv_path, image_dir, transform=None):
        self.data = pd.read_csv(csv_path)
        self.image_dir = image_dir
        self.transform = transform

    def __getitem__(self, idx):
        row = self.data.iloc[idx]
        img_a = self.load_image(row['left_Image'])
        img_b = self.load_image(row['right_Image'])
        label = 1 if row['choice'] == 'left' else 0
        return img_a, img_b, label
```

### Hugging Face Integration
```python
from datasets import Dataset, Features, Value, Image

features = Features({
    'image_left': Image(),
    'image_right': Image(),
    'choice': Value('string'),
    'emotion': Value('string')
})

dataset = Dataset.from_dict(data_dict, features=features)
```

## Future Extensions

### Planned Enhancements
1. **Additional Emotions**: Add more nuanced emotional dimensions
2. **Temporal Data**: Include time-series urban perception data
3. **Multilingual Labels**: Expand annotation languages
4. **Video Data**: Add street-level video sequences
5. **3D Data**: Incorporate 3D urban models

### Community Contributions
We welcome community contributions for:
- New geographic regions
- Additional emotion dimensions
- Improved annotation methods
- Enhanced analysis tools

## Contact and Support

For technical questions or dataset issues:
- **Documentation**: Check this document and GitHub Issues
- **Bug Reports**: Create detailed issue reports
- **Feature Requests**: Submit enhancement suggestions
- **Research Collaboration**: Contact maintainers for partnerships

---

*This document will be updated as the dataset evolves and new features are added.*