# Literature Review: Symmetry Discovery with Deep Learning

This repository contains an in-depth mathematical presentation reviewing the paper [“Symmetry discovery with deep learning” by Krish Desai, Benjamin Nachman, and Jesse Thaler](https://github.com/hep-lbdl/symmetrydiscovery). The presentation was created and delivered by Rajavivegan, IIT Madras as part of an academic research review at SENAI Lab, IIT Madras

## Contents

- `Symmetry_Discovery_Review.pptx`: The presentation slides (mathematical exposition, group theory, architecture, and experiments)
- `README.md`: Project overview and summary

## About the Paper

The paper introduces **SymmetryGAN**, a novel generative adversarial network framework designed to discover continuous and discrete symmetries in datasets. By leveraging group theory and deep learning, the authors propose a method to identify transformations that leave the statistical properties of data unchanged, with applications in physics and data-driven science.

## What’s Inside the Presentation

- **Mathematical Foundations:**  
  - Definitions and examples of symmetry in datasets and individual data points  
  - Statistical and group-theoretic definitions of symmetry  
  - Overview of relevant groups (General Linear, Orthogonal, Special Orthogonal, Affine, Cyclic, Abelian)
  - Inertial distributions and equiareal maps

- **SymmetryGAN Architecture:**  
  - How the generator learns symmetry transformations  
  - The adversarial setup: generator applies candidate symmetry, discriminator distinguishes original vs. transformed data  
  - Implementation of inertial restrictions and loss functions (cross-entropy, cyclic symmetry regularization)
  - Strategies for symmetry enforcement (simultaneous discrimination, two-stage selection, upfront restriction)

- **Experiments & Results:**  
  - 1D Gaussian: Discovery of identity and reflection symmetries  
  - 2D Gaussian: Learning rotational and cyclic symmetries, SO(2) group  
  - High-dimensional (LHC Olympics dijet data): Discovery of rotational symmetries in SO(2) × SO(2) and SO(4)  
  - Symmetry verification via loss landscapes, KL divergence, and analytic checks  
  - Symmetry discovery maps and their topological implications

- **Applications:**  
  - Particle physics (Large Hadron Collider): Discovering symmetries in jet momentum distributions  
  - Broader impact on data augmentation and simulation

## References

- [Original Paper: Symmetry discovery with deep learning (arXiv)](https://arxiv.org/abs/2406.03619)
- [Official GitHub Repository](https://github.com/hep-lbdl/symmetrydiscovery)

---

**This presentation provides a comprehensive mathematical and experimental review of symmetry discovery in deep learning, making advanced group-theoretic concepts accessible and connecting them to practical neural network architectures.**






## Symmetry Discovery with Deep Learning: Mathematical Foundations, Architecture, and Experimental Results

The paper "Symmetry Discovery with Deep Learning" by Krish Desai et al. introduces a rigorous statistical framework for identifying symmetries in datasets and proposes a novel deep learning architecture, **SymmetryGAN**, to automatically discover such symmetries[2]. Below is a detailed summary of the mathematical definitions, the architecture, and key experimental results.

---

### Mathematical Formulation of Dataset Symmetry

Traditionally, the symmetry of a single data point \( x \) under a transformation \( g \) is defined as invariance:
\[
x \mapsto g \cdot x \quad \text{such that} \quad f(x) = f(g \cdot x)
\]
where \( f \) is some property or function of the data.

For a dataset described by a probability density \( p(x) \), a transformation \( g \) is a **symmetry** if it preserves the density up to a Jacobian factor:
\[
p(x) \, dx = p(g \cdot x) \, d(g \cdot x)
\]
However, when changing coordinates, the Jacobian determinant \( J_g(x) = \left| \frac{\partial (g \cdot x)}{\partial x} \right| \) must be considered. The statistical definition of symmetry thus becomes:
\[
p(x) = p(g \cdot x) \, J_g(x)
\]

To resolve ambiguities introduced by coordinate changes, the authors introduce the concept of an **inertial reference density** \( q(x) \), analogous to inertial frames in classical mechanics. The symmetry condition is then:
\[
\frac{p(x)}{q(x)} = \frac{p(g \cdot x)}{q(g \cdot x)}
\]
This definition ensures that symmetries are intrinsic to the data distribution, not artifacts of coordinate choices.

---

### SymmetryGAN Architecture

**SymmetryGAN** is a generative adversarial network (GAN) designed to learn symmetry transformations directly from data. Its key components are:

- **Generator (\( G_\theta \))**: Instead of generating new data, the generator applies a candidate symmetry transformation \( g_\theta \) (parameterized by neural network weights \( \theta \)) to real data samples \( x \):
  \[
  x' = g_\theta(x)
  \]

- **Discriminator (\( D_\phi \))**: The discriminator is trained to distinguish between original samples \( x \) and transformed samples \( x' \).

- **Adversarial Objective**: The generator seeks to find transformations \( g_\theta \) such that the discriminator cannot tell the difference between \( x \) and \( g_\theta(x) \). The adversarial loss is:
  \[
  \mathcal{L}_{\text{adv}} = \mathbb{E}_{x \sim p(x)} [\log D_\phi(x)] + \mathbb{E}_{x \sim p(x)} [\log(1 - D_\phi(g_\theta(x)))]
  \]

- **Inertial Regularization**: To ensure the learned symmetry is not just a permutation but preserves the inertial reference density, a regularization term is added:
  \[
  \mathcal{L}_{\text{inertial}} = \mathbb{E}_{x \sim p(x)} \left[ \left| \log \frac{q(x)}{q(g_\theta(x))} \right| \right]
  \]

- **Total Loss**: The generator minimizes a combination of adversarial and inertial losses.

- **Symmetry Group Discovery**: By parameterizing \( g_\theta \) to represent elements of various groups (e.g., SO(2), cyclic, affine), the architecture can discover both continuous and discrete symmetries.

---

### Experimental Results

#### **1D Gaussian Example**
- **Setup:** SymmetryGAN is trained on a 1D Gaussian distribution.
- **Discovery:** The model correctly identifies both the identity and reflection (\( x \mapsto -x \)) as symmetries.
- **Loss Landscape:** The analytic loss landscape matches the empirical results, confirming the method's validity.

#### **2D Gaussian Example**
- **Setup:** Training on a 2D Gaussian with known rotational symmetry.
- **Discovery:** The model uncovers the full SO(2) group of rotations as symmetries.
- **Cyclic Symmetry:** By constraining the transformation, the model can also discover discrete cyclic subgroups (e.g., \( C_4 \), the group of 90-degree rotations).
- **Quantitative Results:** The loss approaches zero as the learned transformation approaches the true symmetry, and the discovered group parameters match analytic expectations.

#### **High-Dimensional Physics Data (LHC Olympics Dijet Data)**
- **Setup:** Application to simulated Large Hadron Collider (LHC) data, where the true symmetry group is SO(2) × SO(2).
- **Discovery:** The model successfully learns the underlying rotational symmetries, as verified by:
  - **KL Divergence:** The KL divergence between the original and transformed data distributions is minimized.
  - **Loss Analysis:** The adversarial and inertial losses converge, indicating successful symmetry discovery.

#### **Symmetry Discovery Map**
- The paper introduces a "symmetry discovery map" that visualizes the relationship between initial and learned transformation parameters, revealing the topology of the symmetry group (e.g., showing the periodic structure of SO(2)).

---

### Key Takeaways

- **Mathematical Rigor:** The method provides a statistically and physically meaningful definition of dataset symmetries.
- **Flexible Architecture:** SymmetryGAN can discover both continuous and discrete symmetries, guided by group-theoretic parameterizations.
- **Empirical Validation:** The architecture is validated on toy (Gaussian) and real-world (LHC) datasets, with quantitative and visual evidence of successful symmetry discovery.

For further details, code, and experiments, see the [official GitHub repository](https://github.com/hep-lbdl/symmetrydiscovery).

---
