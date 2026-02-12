# Learning Probability Density Functions using Data Only

## Objective
The objective of this project is to learn the probability distribution of a transformed variable `z` **without assuming any analytical form**.  
A Generative Adversarial Network (GAN) is trained to generate samples that follow the same distribution as the observed data.

---

## Dataset
**Feature used:** NO₂ concentration (`x`)  
**Source:** Kaggle – India Air Quality Data.

---

## Methodology

### Step 1 – Data Transformation
Each value of `x` is converted into `z` using:

z = x + a_r * sin(b_r * x)

where:

- `a_r = 0.5 * (r mod 7)`
- `b_r = 0.3 * ((r mod 5) + 1)`
- `r` = university roll number

This produces the training samples for the model.

---

### Step 2 – GAN Based Distribution Learning
The probability density is assumed **unknown**.

A GAN is trained using only samples of `z`.

#### Generator
- Input → random noise sampled from N(0,1)  
- Output → synthetic sample `z_f`

#### Discriminator
- Input → either real `z` or generated `z_f`  
- Output → probability of being real

Both networks compete, and over time the generator learns to produce realistic samples.

---

### Step 3 – PDF Estimation
After training:

1. A large number of samples are generated from the generator.
2. Histogram or Kernel Density Estimation (KDE) is applied.
3. The resulting curve approximates the learned probability density.

---

## Results
The estimated density shows:

- a dominant central region where most values lie  
- lower probability for extreme values  
- a smooth distribution learned purely from samples  

This indicates that the generator has successfully captured the structure of the data.

---

## Observations

### Mode Coverage
The generator reproduces the main high-density region visible in the real data.

### Training Stability
Loss values stabilize after sufficient epochs, and generated samples become consistent.

### Quality of Generated Distribution
The produced samples follow realistic ranges and do not show random noise or collapse.

---

## Technologies Used
- Python  
- Pandas  
- NumPy  
- PyTorch  
- Matplotlib  
- Scikit-learn (KDE)

---

## Conclusion
The project demonstrates that GANs can model complex data distributions **without requiring an explicit mathematical formula**.  
The learned generator can produce new samples that closely resemble the transformed dataset.
