# NLP-framework

NLP-framework

# RE-Flow: Transformer-Based Pipeline for Requirements Classification and Agile User Story Generation

This repository contains the implementation, datasets, and trained models for our paper:

**RE-Flow: A Transformer-Based Pipeline for Automating Requirement Classification and Agile User Story Generation**

Agile software development depends on accurate, consistent requirements. Manual classification of requirements and their reformulation as user stories is time-consuming and error-prone.  
RE-Flow addresses this challenge by providing an **end-to-end NLP pipeline** that (i) classifies requirements into functional and non-functional categories, and (ii) automatically transforms functional requirements into structured, agile-ready user stories.

---

## 📂 Repository Structure

├── models/
│ ├── PURE_REQ/ # Phase 1: Classification models trained on the PURE_REQ dataset
│ ├── PROMISE/ # Phase 1: Classification models trained on the PROMISE dataset
│ └── Phase2/ # Phase 2: User story generation models (T5-Large, LLaMA-2, Mistral-7B + LoRA)
│
├── data/
│ ├── PURE_REQ/ # Benchmark dataset for requirement classification
│ ├── PROMISE/ # Benchmark dataset for requirement classification
│ └── userstory/ # Dataset for requirement → user story generation
│
└── README.md # Project documentation

---

## ⚙️ Setup Instructions

🚀 Running the Models
Phase 1: Requirement Classification

PURE_REQ Dataset
python scripts/train_classification.py --dataset data/PURE_REQ --output models/PURE_REQ

Phase 2: User Story Generation
T5-Large / LLaMA-2 / Mistral-7B (LoRA)
python scripts/train_generation.py --dataset data/userstory --output models/Phase2

| Task                     | Dataset   | Best Model                   | Metric (F1 / METEOR) |
| ------------------------ | --------- | ---------------------------- | -------------------- |
| Classification (Phase 1) | PROMISE   | RoBERTa + BiLSTM + Attention | F1 = 0.97            |
| Classification (Phase 1) | PURE_REQ  | RoBERTa + BiLSTM + Attention | F1 = XX (fill in)    |
| Generation (Phase 2)     | Userstory | T5-Large (semantic fidelity) | F1 = 0.95            |
| Generation (Phase 2)     | Userstory | Mistral-7B (LoRA, fluency)   | METEOR = 0.73        |

🙌 Acknowledgments

The PURE_REQ and PROMISE datasets were sourced from prior work in requirements engineering.

Large language models (LLaMA-2, Mistral-7B) and T5 are used under their respective licenses.

We thank the open-source NLP community for tools and libraries that made this research possible.
