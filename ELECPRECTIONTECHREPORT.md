

---

# Technical Report: Predictive Modeling of Global Electrification Trends using Generative AI and Deep Learning

**Prepared by:** [SAMWEL ODIEK]

**Date:** FEBRUARY 2026

**Subject:** Capstone Project - Energy Data Science

---

## 1. Abstract

This report details the development of a predictive framework to forecast household electrification rates across 124 non-OECD countries. By integrating historical data (1960–present) with modern AI techniques, the project addresses the challenge of data sparsity through **Generative Adversarial Networks (GANs)** and achieves high-accuracy time-series forecasting via **Long Short-Term Memory (LSTM)** networks. The final output is a deployed web-based dashboard that identifies nations at risk of missing the 2030 Sustainable Development Goal 7 (SDG 7).

## 2. Introduction and Problem Statement

Access to electricity is a fundamental driver of economic development, healthcare, and education. Despite global efforts, many non-OECD nations suffer from inconsistent reporting and slow infrastructure growth. The objective of this project is to:

1. Analyze historical trends in total, rural, and urban electrification.
2. Augment sparse datasets using Generative AI.
3. Predict electrification requirements through 2030.
4. Provide a scalable, cloud-deployed tool for policymakers.

The primary dataset utilized is the **Electrification Database (Aklin et al.)**, which provides a comprehensive panel of 124 countries.

---

## 3. Data Ingestion and Preprocessing

The raw data, provided in `.dta` (Stata) format, required significant cleaning to be suitable for Deep Learning.

### 3.1 Handling Missing Values (Interpolation)

Real-world energy data often contains gaps. For instance, a country might report data for 2005 and 2010 but miss the intervening years. We implemented **linear interpolation** grouped by country. This ensures that the time-series remains continuous without introducing global biases between different nations.

### 3.2 Feature Scaling

Neural networks are sensitive to the magnitude of input values. We applied **Min-Max Scaling** to transform electrification rates (0–100%) into a range of (0–1).



This step is critical for preventing gradient explosion and ensuring faster convergence during the training of the LSTM and GAN models.

---

## 4. Phase 1: Generative AI for Data Augmentation (GANs)

One of the core innovations of this project is using Generative AI to enhance the dataset.

### 4.1 The GAN Architecture

We designed a **Generative Adversarial Network (GAN)** specifically for tabular data.

* **The Generator:** Takes a random noise vector (latent space) as input and attempts to generate synthetic rows of electrification data (Total, Rural, and Urban rates) that mimic the statistical properties of the real data.
* **The Discriminator:** A binary classifier that attempts to distinguish between "Real" historical data and "Fake" data produced by the Generator.

### 4.2 Purpose of Augmentation

In developing nations, historical records are often sparse. By training the GAN, we can generate "plausible future scenarios" or "synthetic neighbor countries." This augmentation allows our predictive model to generalize better, making it more robust against outliers and noise in the real dataset.

---

## 5. Phase 2: Time-Series Forecasting with Deep Learning (LSTM)

Standard regression models fail to capture the "memory" of infrastructure projects. Electrification is a cumulative process—what happened five years ago directly influences next year's progress.

### 5.1 Why LSTM?

We utilized **Long Short-Term Memory (LSTM)** networks, a specialized type of Recurrent Neural Network (RNN). LSTMs solve the "vanishing gradient" problem by using a **Forget Gate**, an **Input Gate**, and an **Output Gate**. This allows the model to remember long-term trends (like a decade-long national grid project) while ignoring short-term fluctuations.

### 5.2 Windowing and Sequence Generation

To train the model, we transformed the data into **sliding windows**. We used a 5-year look-back period () to predict the electrification rate at year . This structure teaches the model the *momentum* of electrification.

---

## 3. Implementation and Deployment Strategy

A capstone project is only as good as its accessibility. We moved the model from a local notebook to a **Full-Stack AI Architecture**.

### 6.1 Backend: FastAPI and Render

The trained LSTM model is hosted on a **FastAPI** server on **Render.com**. This provides a REST endpoint where a country name can be sent, and the model returns a 2030 forecast in JSON format.

### 6.2 Middleware: Supabase Edge Functions

To ensure security and scalability, we utilized **Supabase Edge Functions**. These functions act as a "Serverless" bridge, handling CORS preflight requests and securely invoking the Python backend without exposing sensitive logic to the client-side.

### 6.3 Frontend: Lovable (React) Dashboard

The user interface, built using **Lovable**, provides an interactive experience. Users can select any of the 124 countries and instantly view:

* **Historical Trends:** Plotted from the original database.
* **AI Forecast:** A visual projection to 2030.
* **Risk Indicators:** Automated alerts if a country is projected to stay below 50% electrification.

---

## 7. Results and Discussion

Our model identifies a significant divide in electrification progress.

### 7.1 Identification of "At-Risk" Nations

By running the LSTM forecast globally, we identified a cluster of countries (predominantly in Sub-Saharan Africa and parts of Southeast Asia) that are "At-Risk." These nations show a "stagnation curve" where grid expansion has slowed relative to population growth.

### 7.2 Policy Recommendations

1. **Decentralized Solutions:** For nations projected to remain below 50% by 2030, the model suggests that traditional grid expansion is too slow. Investment should shift toward solar microgrids.
2. **Urban-Rural Focus:** In many cases, urban electrification is near 90%, but rural rates pull the average down. Policies must target rural-specific infrastructure to bridge the gap.

## 8. Conclusion

This project demonstrates that Deep Learning and Generative AI are not just for images or text—they are powerful tools for global development. By combining the historical depth of the Aklin et al. dataset with the predictive power of LSTMs and the creative potential of GANs, we have created a proactive tool for planning the world's energy future.

---

