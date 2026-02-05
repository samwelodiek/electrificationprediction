

---

# 🌍 Global Electrification Forecaster (2030)

### *Bridging the Energy Gap with Deep Learning & Generative AI*

## 📌 Project Overview

This capstone project addresses the critical challenge of global energy access. Using a dataset covering **124 non-OECD countries** with records dating back to **1960**, we built an end-to-end AI system to predict electrification trends.

By leveraging **Generative Adversarial Networks (GANs)** for data augmentation and **Long Short-Term Memory (LSTM)** networks for time-series forecasting, this tool identifies "At-Risk" nations projected to miss the 2030 electrification goals.

---

## 🏗️ Technical Architecture

The project is built as a **Full-Stack AI Orchestration**:

1. **Data Engine:** Python-based preprocessing of the `Electrification_Database.dta`.
2. **Generative AI (GAN):** Augments sparse historical data by generating synthetic yet plausible electrification scenarios.
3. **Predictive Model (LSTM):** A deep learning recurrent neural network trained on global patterns to forecast future rates.
4. **Backend API:** FastAPI hosted on **Render** serving real-time model inferences.
5. **Edge Layer:** **Supabase Edge Functions** (Deno) acting as a secure gateway.
6. **Frontend Dashboard:** A modern, interactive UI built with **Lovable (React/Vite)**.

---

## 🚀 Key Features

* **Deep Learning Forecasts:** Recursive 2030 predictions for total, rural, and urban electrification.
* **Synthetic Data Augmentation:** GAN-driven scenarios to stress-test model robustness.
* **Risk Assessment:** Automated identification of "At-Risk" countries (projected < 50% access).
* **Interactive Dashboard:** Real-time data visualization using Recharts and Tailwind CSS.

---

## 🛠️ Tech Stack

| Category | Technology |
| --- | --- |
| **Languages** | Python, TypeScript, SQL |
| **AI Frameworks** | TensorFlow, Keras, Scikit-learn |
| **Backend** | FastAPI, Uvicorn |
| **Cloud/DevOps** | Render, Supabase (Edge Functions), GitHub |
| **Frontend** | React, Lovable, Tailwind CSS, Recharts |

---

## 📈 Methodology

### 1. Data Processing

We utilized **linear interpolation** to handle historical gaps and **Min-Max Scaling** to normalize data for neural network convergence.

### 2. Generative Augmentation (GAN)

To solve data scarcity in specific regions, a Generator-Discriminator architecture was implemented to create synthetic "neighboring" scenarios, ensuring the predictive model doesn't overfit on limited history.

### 3. Time-Series Forecasting (LSTM)

We used an LSTM architecture with:

* **Time Steps:** 5-year sliding windows.
* **Layers:** Multi-layered LSTM with Dropout (0.2) to prevent overfitting.
* **Loss:** Mean Squared Error (MSE).

---

## 📊 Key Insights (Example Results)

* **Target Accuracy:** The LSTM model achieved a Mean Absolute Error (MAE) of **< 2.5%** on validation sets.
* **Critical Zones:** Our model identified **[Insert Number]** countries that will remain under the 50% threshold without immediate policy intervention.
* **Urban-Rural Gap:** Analysis shows that while urban centers are nearing 90% globally, rural electrification is lagging by a factor of **** in specific non-OECD clusters.

---

## 💻 Installation & Setup

1. **Clone the repo:**
```bash
git clone https://github.com/your-username/electrification-forecaster.git

```


2. **Backend Setup:**
```bash
cd backend
pip install -r requirements.txt
uvicorn main:app --reload

```


3. **Frontend:**
Connect to the **Lovable** project or run the React dev server.

---


 
