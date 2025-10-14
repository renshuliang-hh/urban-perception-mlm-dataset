# Data Collection and Annotation Methodology

## Research Design

### Study Objectives

This dataset was created to address several key research questions in urban perception and multimodal AI:

1. **How well can multimodal large language models understand human perception of urban environments?**
2. **What visual features contribute to different emotional responses to urban scenes?**
3. **How consistent are urban perception judgments across different cultural contexts?**
4. **Can we systematically evaluate and improve model performance on urban understanding tasks?**

### Theoretical Framework

The study is grounded in:
- **Environmental Psychology**: Relationships between physical environments and emotional responses
- **Urban Planning Theory**: Principles of urban design and their psychological impacts
- **Multimodal Learning**: Integration of visual and textual information in AI systems
- **Cross-Cultural Studies**: Universal vs. culture-specific perception patterns

## Data Collection Protocol

### Image Acquisition

#### Source Platforms
1. **Google Street View API**
   - Coverage: 100+ countries
   - Resolution: 1024x1024 pixels
   - Metadata: GPS coordinates, timestamp, heading

2. **Mapillary**
   - Community-contributed imagery
   - Multiple temporal snapshots
   - Various weather conditions

3. **Municipal Databases**
   - Official city imaging projects
   - High-quality professional photography
   - Regular update schedules

#### Sampling Strategy

**Geographic Stratification:**
- **Continents**: 6 continents represented
- **City Types**: Mega-cities (>5M), large cities (1-5M), medium cities (100K-1M)
- **Urban Forms**: Downtown, residential, commercial, industrial, mixed-use

**Temporal Stratification:**
- **Seasons**: Spring, Summer, Fall, Winter (where applicable)
- **Time of Day**: Morning, Afternoon, Evening, Night
- **Weather**: Clear, Cloudy, Rainy, Snow conditions

**Socioeconomic Stratification:**
- **Income Levels**: High, middle, low-income neighborhoods
- **Development Status**: Developed, developing countries
- **Urban Quality**: Well-maintained vs. deteriorating areas

### Quality Control Pipeline

#### Automated Filtering
```python
def image_quality_filter(image_path):
    img = Image.open(image_path)

    # Resolution check
    if min(img.size) < 512:
        return False

    # Blur detection
    blur_score = calculate_blur_score(img)
    if blur_score < threshold:
        return False

    # Brightness check
    brightness = calculate_brightness(img)
    if not (min_brightness < brightness < max_brightness):
        return False

    # Privacy detection
    if detect_faces_license_plates(img):
        return False

    return True
```

#### Human Review Process
1. **Initial Screening**: Trained reviewers assess image quality
2. **Urban Content Validation**: Ensure clear urban features
3. **Privacy Check**: Manual verification of automated privacy filtering
4. **Metadata Verification**: Confirm location and temporal accuracy

## Annotation Design

### Task Specification

#### Primary Task: Image Pair Comparison
**Instructions to Annotators:**
```
You will be shown two images of urban scenes. For each pair, determine which image
better represents the given emotional dimension. Consider all visual aspects of the
scenes including architecture, street activity, green spaces, lighting, and overall
atmosphere. After making your selection, please provide a brief explanation for your choice.
```

#### Secondary Task: Qualitative Feedback
**Requirements:**
- Minimum 10 words explanation
- Specific visual evidence from images
- Personal interpretation and reasoning
- Confidence rating (1-5 scale)

### Annotator Recruitment and Training

#### Recruitment Criteria
- **Age**: 18-65 years
- **Geographic Diversity**: At least 3 different countries of residence
- **Urban Experience**: Current or former residence in urban areas
- **Language Proficiency**: English or Chinese fluency
- **Technical Requirements**: Reliable internet, modern browser

#### Training Protocol

**Phase 1: Introduction (15 minutes)**
- Study overview and objectives
- Task instructions and examples
- Interface navigation tutorial

**Phase 2: Practice Session (20 minutes)**
- 10 practice pairs with feedback
- Quality criteria demonstration
- Common pitfalls explanation

**Phase 3: Certification (10 minutes)**
- 5 certification pairs
- Minimum 80% accuracy required
- Performance feedback and clarification

### Quality Assurance Measures

#### Inter-annotator Agreement Monitoring
```python
def calculate_fleiss_kappa(annotations):
    """
    Calculate Fleiss' kappa for multiple annotators
    on the same set of image pairs
    """
    n_raters = len(annotations[0])
    n_items = len(annotations)

    # Calculate agreement statistics
    p_j = np.zeros(n_categories)
    for j in range(n_categories):
        p_j[j] = sum([row.count(j) for row in annotations]) / (n_items * n_raters)

    p_e = np.sum(p_j ** 2)

    p_a = 0
    for i in range(n_items):
        n_ij = np.bincount(annotations[i], minlength=n_categories)
        p_a += (np.sum(n_ij ** 2) - n_raters) / (n_raters * (n_raters - 1))
    p_a /= n_items

    kappa = (p_a - p_e) / (1 - p_e)
    return kappa
```

#### Attention Checks
- **Known Pairs**: 5% of pairs with predetermined "correct" answers
- **Time Checks**: Minimum 3 seconds per pair to prevent random clicking
- **Consistency Checks**: Repeated pairs to test consistency

#### Performance Monitoring
- **Real-time Feedback**: Immediate notification of failed attention checks
- **Progress Tracking**: Completion rate and accuracy monitoring
- **Adaptive Difficulty**: Adjust pair difficulty based on performance

## Emotional Dimension Development

### Literature Review and Expert Consultation

**Academic Sources:**
1. Environmental psychology literature on urban perception
2. Urban planning studies on neighborhood quality
3. Cross-cultural research on environmental preferences
4. AI research on multimodal understanding

**Expert Panel:**
- **Urban Planners**: 5 professionals with 10+ years experience
- **Environmental Psychologists**: 3 academic researchers
- **Architects**: 4 practitioners specializing in urban design
- **Data Scientists**: 3 experts in multimodal AI

### Dimension Definition Process

#### Iterative Refinement
1. **Initial Draft**: Based on literature review
2. **Expert Review**: Panel feedback and suggestions
3. **Pilot Testing**: 100 annotators, 1000 pairs
4. **Statistical Analysis**: Factor analysis and reliability testing
5. **Final Refinement**: Based on quantitative and qualitative feedback

#### Operational Definitions

Each emotion dimension was defined with:
- **Conceptual Definition**: Theoretical grounding
- **Operational Criteria**: Specific visual features to consider
- **Example Scenarios**: Concrete illustrations
- **Common Misconceptions**: What to avoid in judgments

### Validation Studies

#### Reliability Testing
- **Test-Retest Reliability**: Same annotators, different sessions
- **Internal Consistency**: Cronbach's alpha for items within dimensions
- **Inter-rater Reliability**: Fleiss' kappa across multiple raters

#### Construct Validity
- **Convergent Validity**: Correlation with established urban quality measures
- **Discriminant Validity**: Low correlation between different dimensions
- **Known-Groups Validity**: Differences across known urban quality variations

## Technical Infrastructure

### Annotation Platform

#### Frontend Development
```javascript
// Annotation interface component
const AnnotationInterface = {
  components: {
    ImageViewer: {
      sideBySideDisplay: true,
      zoomControls: true,
      fullscreenOption: true
    },
    ResponseCollector: {
      choiceButtons: ['left', 'right'],
      textInput: {
        minLength: 10,
        placeholder: 'Please explain your choice...'
      },
      confidenceSlider: {
        min: 1,
        max: 5,
        step: 1
      }
    },
    ProgressIndicator: {
      currentPair: number,
      totalPairs: number,
      estimatedTime: string
    }
  }
}
```

#### Backend Architecture
- **Database**: PostgreSQL for structured data
- **File Storage**: AWS S3 for image storage
- **API**: RESTful API for data exchange
- **Queue System**: Redis for task distribution

### Data Management

#### Version Control
- **Dataset Versioning**: Semantic versioning (v1.0.0, v1.1.0, etc.)
- **Change Tracking**: Detailed changelog for each version
- **Backward Compatibility**: Maintained for minor version updates

#### Backup and Recovery
- **Daily Backups**: Automated database backups
- **Geographic Redundancy**: Multiple storage locations
- **Recovery Testing**: Regular restore procedure testing

## Statistical Analysis Plan

### Power Analysis

**Sample Size Calculation:**
- **Effect Size**: Medium (Cohen's d = 0.5)
- **Power**: 0.80
- **Alpha**: 0.05
- **Required Sample**: 64 pairs per condition (actual: 500+ pairs)

### Analysis Methods

#### Descriptive Statistics
- **Distribution Analysis**: Histograms and Q-Q plots
- **Central Tendency**: Mean, median, mode calculations
- **Variability**: Standard deviation, interquartile range

#### Inferential Statistics
- **Chi-square Tests**: Categorical data analysis
- **T-tests**: Pairwise comparisons
- **ANOVA**: Multiple group comparisons
- **Correlation Analysis**: Relationship between variables

#### Multivariate Analysis
- **Factor Analysis**: Underlying dimension structure
- **Cluster Analysis**: Pattern recognition in perceptions
- **Regression Analysis**: Predictive modeling

## Ethical Considerations

### IRB Approval

**Study Classification:** Minimal Risk Research
**Approval Number:** [IRB-2024-XXXX]
**Review Process:** expedited review completed

### Informed Consent

**Participant Information:**
- Study purpose and procedures
- Time commitment and compensation
- Data privacy and confidentiality
- Right to withdraw without penalty

**Consent Process:**
- Electronic consent form
- Comprehension questions
- Explicit agreement required
- Copy of consent provided

### Privacy Protection

#### Data Anonymization
- **User IDs**: Random alphanumeric identifiers
- **IP Addresses**: Not recorded
- **Personal Information**: Not collected
- **Location Data**: Generalized to city level

#### Image Privacy
- **Face Detection**: Automatic blurring of faces
- **License Plates**: Blurring when present
- **Private Property**: Exclude images of private residences
- **Sensitive Locations**: Avoid schools, hospitals, religious institutions

## Limitations and Mitigation Strategies

### Known Limitations

1. **Geographic Bias**: Overrepresentation of certain regions
   - **Mitigation**: Targeted sampling from underrepresented areas

2. **Cultural Specificity**: Western-centric urban design concepts
   - **Mitigation**: Include diverse cultural perspectives in expert panel

3. **Temporal Snapshot**: Static images don't capture dynamics
   - **Mitigation**: Note as limitation, plan video data extension

4. **Language Barriers**: Limited to English and Chinese annotations
   - **Mitigation**: Plan multilingual expansion

### Quality Control Challenges

1. **Annotator Fatigue**: Long annotation sessions
   - **Mitigation**: Session length limits, regular breaks

2. **Subjectivity**: Individual differences in perception
   - **Mitigation**: Large sample size, statistical aggregation

3. **Technical Issues**: Platform reliability
   - **Mitigation**: Robust infrastructure, regular maintenance

## Future Improvements

### Data Collection Enhancements

1. **Longitudinal Data**: Track perception changes over time
2. **Video Sequences**: Add dynamic urban scenes
3. **3D Environments**: Incorporate spatial perception
4. **Multimodal Input**: Add audio, temperature, air quality data

### Methodology Improvements

1. **Adaptive Testing**: Dynamic difficulty adjustment
2. **Eye-tracking**: Visual attention analysis
3. **Physiological Measures**: Biometric response data
4. **Collaborative Annotation**: Group-based decision making

---

*This methodology document continues to evolve as we refine our data collection and annotation processes.*