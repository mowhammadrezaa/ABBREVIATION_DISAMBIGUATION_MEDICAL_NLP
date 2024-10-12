# Abbreviation Disambiguation Using Negative Sampling

## Project Overview
This project focuses on **Abbreviation Disambiguation (AD)** in the medical field, employing state-of-the-art **NLP techniques**. The goal is to associate abbreviations in sentences with their corresponding full forms from a set of potential expansions. We fine-tuned three pre-trained models—**TinyBERT**, **BioBERT**, and **SciBERT**—to build an AD system, using a **negative sampling** approach to improve model performance.

The experiments showed that SciBERT outperformed the others with an **F1-score of 0.81**, demonstrating its superior capacity to handle the complexities of medical abbreviation disambiguation.

## Key Features
- **Models**: TinyBERT, BioBERT, SciBERT
- **Dataset**: [MeDAL Dataset](https://www.aclweb.org/anthology/2020.clinicalnlp-1.15/) (Medical Dataset for Abbreviation Disambiguation)
- **Approach**: Negative Sampling with a prompt-based model inspired by Wu et al. (2022)
- **Best Performance**: SciBERT with an F1-score of 0.81

## System Architecture
The system leverages **BERT-based architectures** with an additional linear layer to handle classification. The model encodes input sequences (context + candidate expansion) and outputs logits, which are then processed to predict the correct expansion.

### Input
- Contextual text where the abbreviation appears.
- List of possible expansions for the abbreviation.

### Model Process
1. Tokenize context and expansions.
2. Encode using pre-trained BERT models.
3. Apply negative sampling to handle incorrect expansions.
4. Use a linear layer to generate logits and apply loss functions to refine predictions.

Here’s the updated section of the `README.md` including the loss formula:

---

### Loss Function
The model uses a specialized loss function that combines **Cross Entropy (CE) Loss** and **Hinge Loss** to improve the classification of abbreviation expansions. The goal is to prioritize the correct expansion while ensuring that original negative expansions (hard negatives) are separated from additional negative expansions (easy negatives).

#### Cross Entropy Loss:
The **Cross Entropy (CE) Loss** is used to ensure that the model assigns the highest score to the correct expansion, which is the ground truth.

#### Hinge Loss:
The **Hinge Loss** is designed to maintain a margin between the scores of the original negative expansions and additional negative expansions. The formula is as follows:

```markdown
Loss_hinge = max(gap - min(S_ori) + max(S_add), 0)
```

Where:
- `S_ori` is the set of scores for the original expansions.
- `S_add` is the set of scores for the additional negative expansions.
- `gap` is a hyperparameter controlling the margin between the original and additional expansions.

#### Total Loss:
The overall loss combines **Cross Entropy** and **Hinge Loss** as follows:

```markdown
Loss = Loss_CE + mu * Loss_hinge
```

Where:
- `mu` is a hyperparameter that controls the weighting of the hinge loss component.

This combined loss function encourages the model to correctly identify the true expansion while maintaining a clear separation between hard and easy negative expansions.

## Preprocessing
Preprocessing is a critical step to ensure the data is clean, consistent, and ready for model training. For this project, we implemented several preprocessing techniques to optimize the data:

1. **Stopword Removal**:
    - Removed irrelevant stopwords from labels to avoid distracting the model during training. Stopwords don't contribute meaningfully to the abbreviation and can hinder the model's accuracy.
  
2. **Label Correction**:
    - Ensured that the expanded labels are consistent with their corresponding abbreviations. For instance, we aligned the words in the label with the letters in the abbreviation. If there was a mismatch, the labels were corrected automatically based on matching patterns.
  
3. **Handling Odd Labels**:
    - Some labels contained more words than their corresponding abbreviations. We identified and corrected these cases by aligning the label words with the abbreviation letters, often reviewing the one word before and after the expected match.

4. **Numerical Label Handling**:
    - Special attention was given to labels where the abbreviation contained numbers (e.g., "4" being represented as "fourth"). These labels were excluded from correction processes to avoid conflicts.

5. **Stopword Mapping**:
    - After preprocessing, we created a mapping dictionary to track changes made to the labels. This allowed for verification of whether corrections were necessary.

6. **Manual Corrections**:
    - For particularly challenging cases (e.g., "AD" misclassified as "DAT"), manual corrections were made. This involved human verification for complex abbreviations.

7. **Post-Processing Step**:
    - After model predictions, we applied a post-processing mapping (`bad_label2good_label`) to further correct any errors where the model struggled with confusing abbreviations.

These preprocessing steps helped improve model performance by ensuring that the input data was structured and representative of the desired task.

## Dataset
The **MeDAL** dataset was used, consisting of 5 million sampled data points from the original 14 million entries. Each entry includes:
- A unique ID.
- Textual content.
- Abbreviation positions within the text.
- Ground truth labels (full forms of abbreviations).

The dataset contains over 5700 distinct abbreviations, with expansions ranging from 1 to 65 options per abbreviation.

## Results
| Model   | Train F1 | Validation F1 | Test F1 |
|---------|----------|---------------|---------|
| Baseline| 0.34     | 0.32          | 0.34    |
| TinyBERT| 0.31     | 0.28          | 0.30    |
| BioBERT | 0.74     | 0.62          | 0.64    |
| SciBERT | 0.88     | 0.79          | 0.81    |

## Error Analysis
- **Common Misclassifications**: Errors typically occurred with abbreviations that have conceptually similar expansions, such as abbreviations with multiple variations of the same term.
- **Post-Processing**: A mapping step was introduced to handle cases where expansions had incorrect labels due to dataset inconsistencies.

## Future Work
- **Expand dataset** to include more abbreviations and candidate expansions.
- **Leverage larger models** like BIOGPT for improved accuracy and context understanding.
- **Improve preprocessing** to handle nuanced errors in data more effectively.

## Authors
- Mohammadreza Hosseini       | mohammadrez.hossein2@studio.unibo.it
- Parvaneh Soleimanybaraijany | p.soleimanybaraijany@studio.unibo.it

## License
This project is licensed under the MIT License.



