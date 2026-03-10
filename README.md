# Beyond Action Units: Towards Multi-cue Facial Emotion Analysis

> **Paper**: *Beyond Action Units: Towards Multi-cue Facial Emotion Analysis*
> **Journal**: Pattern Recognition
> **Authors**: Yucheng Shen, Jiulong Wu, Yikai Zhang, Lingyong Yan, Dawei Yin, Min Cao, Mang Ye

---

## Overview

Traditional Facial Emotion Analysis (FEA) relies solely on Action Units (AUs) to infer emotions, which is fragile when AUs are occluded, ambiguous, or externally caused. We propose **MFEA (Multi-cue Facial Emotion Analysis)**, a new paradigm that integrates three complementary facial cues — AUs, demographic attributes, and contextual factors — through a structured three-stage pipeline: **cue recognition → interpretable reasoning → emotion prediction**.

![Main Figure](asset/Main.png)

*Left: Conventional FEA relies solely on AUs, which can be misleading (e.g., externally forced smile). Right: MFEA integrates contextual and demographic cues to correctly infer emotion even when AUs are unreliable.*

## Key Contributions

- **MFEA Paradigm**: A systematic extension of FEA that shifts from single-cue to multi-cue analysis, enabling robust and interpretable emotion reasoning under real-world complexity.

- **MFEA-Bench**: A comprehensive benchmark comprising 5 evaluation subsets (25,770 samples total) with multi-layered annotations covering AUs, demographics, contextual factors, and emotions.

- **MFEA-CoT Score**: A novel evaluation metric that holistically measures cue recognition, reasoning quality, and emotion prediction accuracy in a unified chain-of-thought framework.

## Framework

![Framework](asset/case1.png)

*Left: The three-stage MFEA process on a facial image — (1) facial cue recognition, (2) interpretable reasoning, (3) emotion prediction. Right: The MFEA-CoT scoring pipeline combining traditional metrics with LLM-as-judge evaluation.*

## Benchmark: MFEA-Bench

![Data](asset/data.png)

MFEA-Bench is partitioned into five subsets:

| Subset | Samples | Evaluation Metric |
|---|---|---|
| MFEA-Main | 1,168 | Full MFEA-CoT Score |
| MFEA-Context | 503 | MFEA-CoT (context-dominant) |
| AU-only | 3,168 | AU Score |
| Emotion-only | 9,394 | Emotion Score |
| Demographic-only | 11,537 | Demographics Score |

## Key Findings

![Correlation](asset/cue%20vs%20emo.png)

*Strong positive correlation between cue recognition / reasoning quality and emotion recognition accuracy, suggesting that guiding models to recognize fine-grained facial cues directly improves downstream emotion prediction.*

- Closed-source models (Gemini-2.5-Pro, Grok-4) consistently outperform open-source models across all evaluation dimensions.
- Fine-tuning with only **700 curated samples** substantially closes the gap, with improvements generalizable across multiple base models (LLaVA-1.5-7B, Qwen2.5-VL-7B, Qwen3-VL-8B).
- MFEA preserves accuracy when AUs are reliable and significantly improves robustness when they are not.

## Data Release

### Annotations

All annotation files are provided in the `annotation/` directory in JSONL format:

| File | Samples | Description |
|---|---|---|
| `MFEA-Main.jsonl` | 1,168 | AUs + demographics + emotion labels |
| `MFEA-Context.jsonl` | 503 | Context + demographics + emotion labels |
| `AU-only.jsonl` | 3,168 | AU annotations |
| `Emotion-only.jsonl` | 9,394 | Emotion labels |
| `Demographic-only.jsonl` | 11,537 | Age, gender, race attributes |
| `Training-Set.jsonl` | 700 | Training samples with full annotations and CoT conversations |

### Images

Images can be downloaded via Baidu Netdisk:

[Baidu Netdisk (Password: ga27)](https://pan.baidu.com/s/1Avbx_6eCngpjquXvLgoVyA?pwd=ga27)

### Source Datasets

MFEA-Bench is built upon the following publicly available datasets. We sincerely thank the original authors for their contributions:

- **FER2013** — Goodfellow et al., *Challenges in Representation Learning: A Report on Three Machine Learning Contests*, 2013
- **AffectNet** — Mollahosseini et al., *AffectNet: A Database for Facial Expression, Valence, and Arousal Computing in the Wild*, 2017
- **ExpW** — Zhang et al., *From Facial Expression Recognition to Interpersonal Relation Prediction*, 2018
- **RAF-DB** — Li et al., *Reliable Crowdsourcing and Deep Locality-Preserving Learning for Expression Recognition in the Wild*, 2017
- **CK+** — Lucey et al., *The Extended Cohn-Kanade Dataset (CK+)*, 2010
- **KDEF** — Lundqvist et al., *The Karolinska Directed Emotional Faces*, 1998
- **NHFI** — Vaidya et al., *Natural Head and Face Images*, 2020
- **NIMH-ChEFS** — Egger et al., *NIMH Child Emotional Faces Picture Set*, 2011
- **WSEFEP** — Olszanowski et al., *Warsaw Set of Emotional Facial Expression Pictures*, 2015
- **HECO** — Yang et al., *Emotion Recognition in Context*, 2022
- **DISFA** — Mavadati et al., *DISFA: A Spontaneous Facial Action Intensity Database*, 2013
- **BP4D** — Zhang et al., *BP4D-Spontaneous: A High-Resolution Spontaneous 3D Dynamic Facial Expression Database*, 2014
- **RAF-AU** — Yan et al., *RAF-AU Dataset*, 2020
- **FABA** — Chaubey et al., *Face Action Beyond AUs*, 2025

> **Important**: All images are sourced from publicly available, IRB-approved datasets and are used strictly for research purposes. Please ensure you comply with the original license terms of each source dataset before use. Demographic annotations are employed solely for fairness and robustness analysis, not for profiling or surveillance.

## Citation

If you find this work useful, please consider citing:

```bibtex
@article{shen2025beyond,
  title={Beyond Action Units: Towards Multi-cue Facial Emotion Analysis},
  author={Shen, Yucheng and Wu, Jiulong and Zhang, Yikai and Yan, Lingyong and Yin, Dawei and Cao, Min and Ye, Mang},
  journal={Pattern Recognition},
  year={2025}
}
```

## License

This project is released under the [Apache 2.0 License](LICENSE).
