# Literature Review: Symmetry Discovery with Deep Learning

This repository contains an in-depth mathematical presentation reviewing the paper [“Symmetry discovery with deep learning” by Krish Desai, Benjamin Nachman, and Jesse Thaler](https://github.com/hep-lbdl/symmetrydiscovery). The presentation was created and delivered by Rajavivegan, IIT Madras as part of an academic research review at SENAI Lab, IIT Madras

## Contents

- `Symmetry_Discovery_Review.pdf`: The presentation slides (mathematical exposition, group theory, architecture, and experiments)
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






