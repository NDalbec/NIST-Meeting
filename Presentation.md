---
marp: true
theme: default
title : Accurate Unsupervised Photon Counting from Transition Edge Sensor Signals
author : Nicolas Dalbec-Constant
paginate: true
math : True
---

<style>
img[alt~="center"] {
  display: block;
  margin: 0 auto;
}
section {
 font-family: 'Times', sans-serif;
}
</style>

## Code Availability

<center>

Presentation                                          | <center> Full Research   
:----------------------------------------------------:|:-----------------------
![width:300px center](assets/github_presentation.png) |![width:300px center](assets/github_poly.png)
NIST-Meeting                                           | Photon-Number-Classification

</center>

---

## Accurate Unsupervised Photon Counting from Transition Edge Sensor Signals

Nicolas Dalbec-Constant


---

## Some Features

#### Recovery time  : $\sim 10 \mu s$ 
> L. A. Morais et al. (2024), doi: 10.22331/q-2024-05-23-1355.

#### Efficiency : $\sim 98\%$ 
> D. Fukuda et al. (2011), doi: 10.1364/OE.19.000870.

#### Working temperature : $\sim 50-100 mK$ 
> L. A. Morais et al. (2024), doi: 10.22331/q-2024-05-23-1355.

#### Photon number range : $\text{0 to 33 photons}$
> M. Eaton et al. (2023), doi: 10.1038/s41566-022-01105-9.

---

<!-- ## Working Principle

![width:700px center](assets/TransitionEdge.png)
<p style="text-align:center;">Fig. 1 : Sketch of a TES's resistance variation with temperature.</p>

--- -->

## Signals

![width:700px center](assets/TracesUniform.png)
<p style="text-align:center;">Fig. 2 : 3 000 TES signals.</p>

---

## Problem Formulation

```python
def function(Signals : np.array):
  '''
  Function to transform TES signals into photon numbers.

  Parameters
  ----------
  Signals : np.array
    TES signal matrix of shape 
    (number of signals, number of time steps in each signal)

  Returns
  -------
  Photon_Numbers : np.array
    Array that contains the photon number associated with each 
    signal in `Signals`.

  '''
  return Photon_Numbers
```

---

<!-- 
footer: L. A. Morais et al., “Precisely determining photon-number in real time,” Quantum 1355, May 2024.
-->

## Historical Methods

 1. Operation                               |  2. Latent Space                | 3. Distribution
:------------------------------------------:|:-------------------------------:|:-------------------------:
![fit](assets/Trace_MAX.svg)  |![fit](assets/Maximum-Value.svg) |![fit](assets/Distribution_MAX.svg)
![fit](assets/Trace_AREA.svg)          |![fit](assets/Area.svg)          |![fit](assets/Distribution_AREA.svg)

---

<!-- 
footer: P. C. Humphreys et al., “Tomography of photon-number resolving continuous-output detectors,” New J. Phys., vol. 17, no. 10, p. 103044, Oct. 2015.
-->

## Principal Component Analysis (PCA)

1. Signals                     |  2. Latent Space             | 3. Distribution
:-----------------------------:|:-----------------------:|:-------------------------:
![fit](assets/Trace_PCA.svg)   |![fit](assets/PCA.svg)   |![fit](assets/Distribution_PCA.svg)

---

<!-- footer: "" -->

![bg right width:500px](assets/PCA.svg)

## Dimensionality Reduction

<small>
  Transforming high-dimensional data into a lower-dimensional representation that retains a maximum of information.
</small>

## Clustering

<small>
  Identifying groups of similar samples inside a latent space based on some criteria.
</small>

## Unsupervised Classification

<small>
  Each signal can be associated with a class and the true label of each sample is unknown.
</small>

---

<!-- 
footer: T. Gerrits et al., “Extending single-photon optimized superconducting transition edge sensors beyond the single-photon counting regime,” Opt. Express, Oct. 2012
-->

## Dataset (NIST)


 Signals                                 |  <center> Expected Distribution           
:---------------------------------------:|:---------------------------------------------
![width:500px](assets/TracesUniform.png) |![width:500px](assets/Distribution_Uniform.svg)



---

<!-- 
footer: ''
-->

## Exploration of Dimensionality Reduction Techniques

Simple Feature                         |  Predictive                                | Non-Predictive
:-------------------------------------:|:------------------------------------------:|:-------------------------:
![fit](src/Results_Uniform/Density/MAX.svg)    | ![fit](<src/Results_Uniform//Density/PCA 1D.svg>)   | ![fit](<src/Results_Uniform//Density/tSNE 1D.svg>)
![fit](src/Results_Uniform//Density/AREA.svg)   | ![fit](<src/Results_Uniform//Density/PUMAP 1D.svg>) | ![fit](<src/Results_Uniform//Density/UMAP 1D.svg>)
.                                      | ![fit](<src/Results_Uniform//Density/PTSNE 1D.svg>) | ![fit](<src/Results_Uniform//Density/ISO 1D.svg>)
.                                      | .                                          | ![fit](<src/Results_Uniform//Density/NMF 1D.svg>)

---

## Exploration of Dimensionality Reduction Techniques

|  Predictive                                | Non-Predictive
|:------------------------------------------:|:-------------------------:
| ![fit](<src/Results_Uniform//Density/PCA 2D.svg>)   | ![fit](<src/Results_Uniform//Density/KPCA Cos.svg>)
| .                                          | ![fit](<src/Results_Uniform//Density/KPCA RBF.svg>)
| .                                          | ![fit](<src/Results_Uniform//Density/KPCA Sig.svg>)
| .                                          | ![fit](<src/Results_Uniform//Density/tSNE 2D.svg>)
| .                                          | ![fit](<src/Results_Uniform//Density/UMAP 2D.svg>)

---

<!-- 
footer: L. Van der Maaten and G. Hinton, “Visualizing data using t-SNE.,” Journal of machine learning research, vol. 9, no. 11, 2008
-->

## t-distributed stochastic neighbor embedding (t-SNE)

|  ![fit](<src/Results_Uniform/Density/tSNE 1D.svg>) | ![width:500px](<src/Results_Uniform//Density/tSNE 2D.svg>)
|:------------------------------------------:|:-------------------------:


---

<!-- 
footer: L. McInnes, J. Healy, N. Saul, and L. Großberger, “UMAP: Uniform Manifold Approximation and Projection,” Journal of Open Source Software, vol. 3, no. 29, p. 861, Sep. 2018.
-->

## Uniform Manifold Approximation and Projection (UMAP)

|  ![fit](<src/Results_Uniform//Density/UMAP 1D.svg>) | ![width:500px](<src/Results_Uniform//Density/UMAP 2D.svg>)
|:------------------------------------------:|:-------------------------:


---

<!-- 
footer: P. C. Humphreys et al., “Tomography of photon-number resolving continuous-output detectors,” New J. Phys., vol. 17, no. 10, p. 103044, Oct. 2015.
-->

## Confidence

$$
C_n = \int \frac{p(s|n)^2p(n)}{\sum_k p(s|k)p(k)} ds 
$$

<center> $p(s\|n)$ : Gaussians      | <center> $p(n)$ : Expected Distribution 
-----------------------------------:|:---------------------------------------
![fit](assets/PCA.svg)              | ![fit](assets/Distribution_Uniform.svg)


---

<!-- 
footer: ''
-->

## Benchmark

![width:800px center](src/Results_Uniform//Confidence.svg)

---

## Benchmark

![width:800px center](src/Results_Uniform//Confidence_Simple.svg)

---

## Outlier Detection (NRC)

![width:700px center](src/Results_Noise/Traces_Noise.png)

---

## Outlier Detection

![fit](<src/Results_Noise/PCA 1D.svg>)   | ![fit](<src/Results_Noise/PCA 2D.svg>)
--------------------------------:|:-------------------------------:

---

## Outlier Detection

![width:900px center](assets/noiseUMAP2D.png)


---

## Parametric Implementation of UMAP

![width:900px center](src/Results_Large/Confidence.svg)

---


## Summary

- Dimensionality reduction is useful to understand data.
- Nonlinear techniques can improve the photon number resolution of TESs.
- Neural networks provide a precise and efficient platform to achieve photon number prediction.

---

## Code Availability

<center>

Presentation                                          | <center> Full Research   
:----------------------------------------------------:|:-----------------------
![width:300px center](assets/github_presentation.png) |![width:300px center](assets/github_poly.png)
NIST-Meeting                                           | Photon-Number-Classification

</center>