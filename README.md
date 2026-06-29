# ViMovieABSA: A Vietnamese Aspect-Based Sentiment Dataset for Movie Reviews with Reliability-Decomposed Annotation

[![Dataset Size](https://img.shields.io/badge/Dataset--Size-10%2C797--comments-blue)](https://github.com/AlyThien/ViMovieABSA-A-Vietnamese-Aspect-Based-Sentiment-Dataset-for-Movie-Reviews-with-Reliability-Decompos)
[![Domain](https://img.shields.io/badge/Domain-Movie--Reviews-orange)](https://github.com/AlyThien/ViMovieABSA-A-Vietnamese-Aspect-Based-Sentiment-Dataset-for-Movie-Reviews-with-Reliability-Decompos)
[![Language](https://img.shields.io/badge/Language-Vietnamese-red)](https://github.com/AlyThien/ViMovieABSA-A-Vietnamese-Aspect-Based-Sentiment-Dataset-for-Movie-Reviews-with-Reliability-Decompos)
[![License](https://img.shields.io/badge/License-CC--BY--4.0-green)](https://creativecommons.org/licenses/by/4.0/)

Official repository for the paper **"ViMovieABSA: A Vietnamese Aspect-Based Sentiment Dataset for Movie Reviews with Reliability-Decomposed Annotation"**. 

This repository contains the dataset and benchmarking code for the first Vietnamese Aspect-Category Sentiment Classification (ACSC) dataset in the movie domain.

---

## 📌 Dataset Overview

**ViMovieABSA** consists of **10,797 Vietnamese social media comments** collected from four platforms: **YouTube**, **Facebook**, **VnExpress**, and **TikTok**. Each comment is annotated across **six aspect categories** with four possible sentiment polarities: `{Positive, Negative, Neutral, none}` (where `none` indicates the aspect is not mentioned).

### Aspect Schema & Definitions

| Aspect | Definition | Key Triggers / Keywords |
| :--- | :--- | :--- |
| **Overall** | General opinion about the film. | phim, bộ phim, tác phẩm, coi, xem... |
| **Plot** | Story, script, narrative structure, ending. | cốt truyện, kịch bản, tình tiết, cái kết, nội dung... |
| **Acting** | Performance quality of the cast. | diễn viên, diễn xuất, nam chính, nữ phụ, vai diễn... |
| **Director** | Directing style, cinematography decisions, editing. | đạo diễn, chỉ đạo, quay phim, dựng phim... |
| **Music** | Soundtrack, sound effects, theme song (OST). | nhạc nền, âm thanh, bài hát, OST, nhạc phim... |
| **Visual** | Cinematography, visual effects, CGI, set design. | hình ảnh, kỹ xảo, bối cảnh, CGI, góc quay... |

### Dataset Statistics (Train/Test Split)

| Aspect | Train (Pos / Neg / Neu / None) | Test (Pos / Neg / Neu / None) |
| :--- | :--- | :--- |
| **Overall** | 3,346 / 2,629 / 373 / 2,289 | 837 / 657 / 94 / 572 |
| **Plot** | 1,260 / 1,784 / 637 / 4,956 | 321 / 433 / 152 / 1,254 |
| **Acting** | 667 / 579 / 125 / 7,266 | 184 / 144 / 36 / 1,796 |
| **Director** | 344 / 380 / 66 / 7,847 | 98 / 110 / 11 / 1,941 |
| **Music** | 369 / 149 / 39 / 8,080 | 89 / 32 / 9 / 2,030 |
| **Visual** | 601 / 379 / 114 / 7,543 | 168 / 86 / 23 / 1,883 |
| **Total** | **8,637 comments** | **2,160 comments** |

---

## 🛠️ Annotation Pipeline & Reliability

Our annotation pipeline uses a semi-automatic approach:
1. **Stage 1 (LLM Labeling):** A tuned few-shot prompt with `gemma-4-31b` generates first-pass labels. High-confidence labels ($\ge 0.75$) are retained.
2. **Stage 2 (Human Verification):** 913 comments are annotated/verified by five trained native Vietnamese speakers.

### Inter-Annotator Agreement (Krippendorff's $\alpha$)
We report agreement by **decomposing** the annotation task into two sub-tasks on a 97-comment gold standard subset:

*   **Aspect Detection (binary):** $\alpha = 0.657$ (Substantial Agreement)
*   **Sentiment Polarity (3-class):** $\alpha = 0.724$ (Substantial Agreement)
*   **Overall Agreement (4-class):** $\alpha = 0.669$

---

## 🚀 Baseline Results

We benchmarked four models using Macro-F1 scores over the three expressed sentiment classes `(Pos, Neg, Neu)` with class-imbalance controls:

| Aspect | Logistic Regression | BiLSTM | SVM + TF-IDF | PhoBERT (Multi-Task) |
| :--- | :---: | :---: | :---: | :---: |
| **Overall** | 0.632 | 0.554 | 0.652 | **0.734** |
| **Plot** | 0.606 | 0.581 | 0.609 | **0.711** |
| **Acting** | 0.547 | 0.523 | 0.506 | **0.657** |
| **Director** | 0.557 | 0.529 | 0.493 | **0.544** |
| **Music** | 0.497 | 0.506 | 0.465 | **0.564** |
| **Visual** | 0.460 | 0.441 | 0.466 | **0.601** |
| **Average** | 0.550 | 0.522 | 0.532 | **0.635** |

*Note: Multi-task `PhoBERT-large` fine-tuning sets the state-of-the-art baseline on this dataset with **0.635** average Macro-F1.*

---

## 📁 Repository Structure

```text
└── README.md                            # Repository documentation (this file)
```

---

## 📝 Citation

If you use this dataset or code in your research, please cite our paper:

```bibtex
@inproceedings{thien2026vimovieabsa,
  title={ViMovieABSA: A Vietnamese Aspect-Based Sentiment Dataset for Movie Reviews with Reliability-Decomposed Annotation},
  author={Le Tran Duc Thien and Le Hoang Thai and Nguyen Hien Tran and Phan Nam Thanh and Dao Minh Thien and Huynh Van Tin},
  booktitle={Proceedings of the Conference},
  year={2026}
}
```

---

## 📄 License

The dataset is licensed under a [Creative Commons Attribution 4.0 International License (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).
The code is licensed under the [MIT License](LICENSE).
