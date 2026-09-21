# Fine-Tuning MatterSim-v1 on Hydrocarbon Energy Prediction

This repository contains the first-year undergraduate term project focused on fine-tuning the **MatterSim-v1** foundation model to predict the total internal energy of hydrocarbon systems. 

## Project Overview

The goal of this project is to adapt a state-of-the-art machine learning interatomic potential (**MatterSim-v1**) to accurately predict the internal energy (in eV) of various hydrocarbon configurations based on their atomic coordinates (XYZ structures).

### Key Results
* **Test Set Error:** Achieved a Mean Absolute Error (MAE) of **`0.000874 eV/atom`** on the independent test dataset.
* **Weighted Loss Function:** To mitigate spikes and stabilize predictions, a custom weighted Mean Squared Error (MSE) loss function was implemented, penalizing errors based on the molecular mass ($M_i$):

$$
\mathcal{L}_{\text{weighted}} = \frac{1}{N} \sum_{i=1}^{N} w(M_i) \cdot \left( y_i - \hat{y}_i \right)^2
$$

Where the weights $w(M_i)$ are defined as:

$$
w(M_i) = \begin{cases} 3.0, & \text{if } M_i < 50 \\\\ 1.0, & \text{if } 50 \le M_i < 100 \\\\ 1.5, & \text{if } 100 \le M_i \le 175 \\\\ 3.0, & \text{if } M_i > 175 \end{cases}
$$



---

## Repository Structure

* `train.xyz` — Training dataset containing atomic structures (XYZ coordinates) and their corresponding target internal energies (eV).
* `test.xyz` — Evaluation dataset used to benchmark final model performance.
* `training_mattersim.ipynb` — Jupyter Notebook detailing the data preprocessing, data loading pipelines, custom loss function implementation, and the fine-tuning training loop.
* `using_mattersim.ipynb` — Jupyter Notebook showing how to load the fine-tuned checkpoints, run inference on new structures, and evaluate test performance.
* `Trained_MS/` — Directory containing project outputs:
  * Model checkpoints and best-performing weight files.
  * Training history plots (loss curves and validation dynamics).

---

## Getting Started

### Prerequisites
Make sure you have `MatterSim` and its dependencies installed according to the official documentation.

### Running the Notebooks
1. **Training:** Open and run `training_mattersim.ipynb` to re-train the model or understand the fine-tuning process.
2. **Inference:** Open `using_mattersim.ipynb` to load the weights saved in `Trained_MS/` and evaluate predictions on `test.xyz` or your own structural data.
