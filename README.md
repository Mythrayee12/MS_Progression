# MS_Progression

A research project applying **semi-supervised representation learning** to disentangle inflammatory and neurodegenerative signals in Multiple Sclerosis (MS) disease progression using Variational Autoencoders (VAE) and synthetic patient data.

---

## 📌 Project Overview

Multiple Sclerosis progression is driven by two overlapping biological processes:
- **Inflammatory activity** — driven by relapse events
- **Neurodegeneration** — gradual, cumulative damage to the CNS

This project investigates whether semi-supervised autoencoders can learn to **disentangle these signals** from limited labeled clinical data, outperforming traditional supervised approaches when labels are scarce.

### Key Objectives

1. Generate biologically plausible synthetic MS patient data with ground-truth latent inflammatory (`z_inflam`) and neurodegenerative (`z_neurodeg`) factors
2. Train baseline supervised models (Logistic Regression, Random Forest)
3. Train an unsupervised autoencoder for representation learning
4. Train a semi-supervised autoencoder combining reconstruction + classification losses
5. Compare model performance and assess robustness under label sparsity (5%, 10%, 20%, 50%)
6. Validate biological plausibility via Pearson correlations with known latent factors

### Features Used

| Type     | Features |
|----------|----------|
| Clinical | EDSS baseline/slope, walking speed, dexterity score, cognitive score |
| MRI      | T2 lesion volume, new lesion count, brain volume |

---

## 🛠️ Installation & Setup

### Prerequisites

- Python 3.8+
- pip or conda

### Steps

1. **Clone the repository**
```bash
   git clone https://github.com/Mythrayee12/MS_Progression.git
   cd MS_Progression
```

2. **Create a virtual environment (recommended)**
```bash
   python -m venv venv
   source venv/bin/activate        # On Windows: venv\Scripts\activate
```

3. **Install dependencies**
```bash
   pip install -r requirements.txt
```

   Key libraries used:
   - `torch` — Autoencoder model training
   - `scikit-learn` — Baseline models, evaluation metrics
   - `numpy`, `pandas`, `scipy` — Data generation and analysis
   - `matplotlib`, `seaborn` — Visualization

---

## 🚀 Usage

Open and run the main notebook end-to-end:
```bash
jupyter notebook MS_Progression_VAE.ipynb
```

### Notebook Sections

| Section | Description |
|---------|-------------|
| **1. Data Generation** | Synthetic MS dataset with 2,000 patients; 20% labeled by default |
| **2. Baseline Models** | Logistic Regression and Random Forest trained on labeled data only |
| **3. Unsupervised AE** | Autoencoder trained with MSE reconstruction loss on all data |
| **4. Semi-Supervised AE** | Autoencoder with classification head; loss = reconstruction + λ × classification |
| **5. Model Comparison** | Accuracy, Precision, Recall, F1, ROC-AUC + paired t-tests |
| **6. Label Sparsity** | Performance vs. labeled fraction (5%–50%) |
| **7. Results Summary** | Biological plausibility checks, clinical distribution validation, conclusions |

### Semi-Supervised Loss Function

$$L_{total} = L_{recon}(X, \hat{X}) + \lambda \cdot L_{classif}(y, \hat{y})$$

- $L_{recon}$: MSE computed on **all** data
- $L_{classif}$: BCE computed only on **labeled** data
- $\lambda$: Balances reconstruction vs. classification objectives

---

## 📁 Project Structure
```
MS_Progression/
│
├── MS_Progression_VAE.ipynb     # Main research notebook
├── ms_synthetic_dataset.csv     # Generated synthetic dataset (auto-saved on run)
├── requirements.txt             # Python dependencies
└── README.md
```

---

## 📊 Results

The semi-supervised autoencoder demonstrates:
- Competitive ROC-AUC compared to fully supervised baselines
- Greater robustness to label scarcity vs. Logistic Regression
- Meaningful latent space structure correlated with true `z_inflam` and `z_neurodeg` factors

---

## 🤝 Contributing

Contributions are welcome! Please open an issue or submit a pull request.

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).

---

## 👩‍💻 Authors

- **Mythrayee12** — [GitHub Profile](https://github.com/Mythrayee12)
- **V-Preetha** — [GitHub Profile](https://github.com/V-Preetha)
