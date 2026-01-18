# NLP-framework

## RE-Flow: Transformer-Based Pipeline for Requirements Classification and Agile User Story Generation

This repository contains the implementation, datasets, and trained models for our paper:

**RE-Flow: A Transformer-Based Pipeline for Automating Requirement Classification and Agile User Story Generation**

Agile software development depends on accurate, consistent requirements. Manual classification of requirements and their reformulation as user stories is time-consuming and error-prone.  
RE-Flow addresses this challenge by providing an **end-to-end NLP pipeline** that:

1. **Phase 1 – Requirement Classification:**  
   Classifies requirements into functional and non-functional categories.

2. **Phase 2 – User Story Generation:**  
   Automatically transforms functional requirements into structured, agile-ready user stories.

> ⚠️ **Important:** The pipeline folder and scripts have been modified to enforce this two-phase execution order:  
> 👉 **You must run Phase 1 first, then Phase 2.**

---

## 📂 Repository Structure

```

├── models/
│   ├── PURE_REQ/      # Phase 1: Classification    models trained on PURE_REQ
│   ├── PROMISE/       # Phase 1: Classification models trained on PROMISE
│   └── Phase2/        # Phase 2: User story generation models
│
├── data/
│   ├── PURE_REQ/      # Benchmark dataset for requirement classification
│   ├── PROMISE/       # Benchmark dataset for requirement classification
│   └── userstory/     # Dataset for requirement → user story generation
│
├── pipeline/           # Two Phase pipeline
└── README.md          # Project documentation

```

---

## ⚙️ Setup & Running Instructions

### ✅ **Recommended Environment**

For best performance and reproducibility, we recommend running this project on:

- **Kaggle Notebook**
- **Accelerator: 2 × T4 GPUs**
- CUDA-enabled environment

This setup is required for large models (T5-Large, LLaMA-2, Mistral-7B with LoRA).

---

## 🚀 Running the Pipeline (MANDATORY ORDER)

### **Step 1 — Phase 1: Requirement Classification (RUN FIRST)**

Make sure your dataset is placed **inside the `data/` folder** before running.

Run:

```bash
python scripts/train_classification.py \
  --dataset data/PURE_REQ \
  --output models/PURE_REQ
```

⚠️ **Before running:**

- Verify the dataset path exists:
  `data/PURE_REQ/`
- Ensure correct file names inside the folder.

You may also train on PROMISE:

```bash
python scripts/train_classification.py \
  --dataset data/PROMISE \
  --output models/PROMISE
```

---

### **Step 2 — Phase 2: User Story Generation (RUN AFTER PHASE 1)**

⚠️ **Important:**
You must complete Phase 1 first, as Phase 2 depends on classified functional requirements.

Place your user-story dataset in:

```
data/userstory/
```

Then run:

```bash
python scripts/train_generation.py \
  --dataset data/userstory \
  --output models/Phase2
```

Supported models in Phase 2:

- T5-Large
- LLaMA-2 (with LoRA)
- Mistral-7B (with LoRA)

---

## 📊 Benchmark Results

| Task                     | Dataset   | Best Model                         | Metric        |
| ------------------------ | --------- | ---------------------------------- | ------------- |
| Classification (Phase 1) | PROMISE   | RoBERTa + BiLSTM + Attention       | F1 = 0.97     |
| Classification (Phase 1) | PURE_REQ  | RoBERTa + BiLSTM + Attention       | F1 = XX       |
| Generation (Phase 2)     | Userstory | T5-Large (semantic fidelity)       | F1 = 0.95     |
| Generation (Phase 2)     | Userstory | Mistral-7B (LoRA, fluency-focused) | METEOR = 0.73 |

_(Update PURE_REQ F1 when finalized.)_

---

## 📌 Notes on Datasets

- All datasets **must be placed inside the `data/` folder** before running.
- Do not change folder names unless you also update script paths.
- The pipeline expects:

```
data/
 ├── PURE_REQ/
 ├── PROMISE/
 └── userstory/
```

---

## 🙌 Acknowledgments

- The PURE_REQ and PROMISE datasets were sourced from prior work in requirements engineering.
- LLaMA-2, Mistral-7B, and T5 are used under their respective licenses.
- We thank the open-source NLP community for libraries such as Hugging Face Transformers, PyTorch, and PEFT.
