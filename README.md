# Probabilistic Generative Models: City at Night & Starry Night Sky

An interactive exploration of probabilistic programming and generative art, translating statistical distributions into visual stories. Built as two distinct generative models from Stanford's **Probability for Artificial Intelligence (PAI)** course—**City at Night** and **Starry Night Sky**—each canvas renders a brand-new scene on every sample by drawing from parameterized probability distributions[cite: 7, 15, 18].

---

## 1. City at Night

A generative streetscape of 24 buildings where architectural purpose drives nighttime lighting patterns[cite: 2, 3]. Rather than treating every window independently, the model uses a hierarchical structure[cite: 1, 2, 3]:

* **Building Height (`NumFloors`):** Each building independently samples a discrete uniform height between 7 and 16 floors[cite: 2, 3].
* **Building Type (`Bernoulli`):** Each building flips a weighted coin controlled by parameter $\theta_3$ (*"Chance a building is an office"*)[cite: 5, 7]. 
  * **Office Towers:** Low probability of lit windows, creating dark silhouettes[cite: 2, 7].
  * **Residential Apartments:** High probability of lit windows, producing bright, lived-in towers[cite: 2, 7].
* **Window Lighting:** Conditioned on building type, each floor flips its own coin to determine illumination[cite: 2, 3].

### Visuals & Model Parameters
<p float="left">
  <img src="art model-1/1.png" width="48%" alt="City at Night Canvas Comparison" />
  <img src="art model-2/2.png" width="48%" alt="City Model Parameters" />
</p>

<p float="left">
  <img src="art model-3/3.png" width="48%" alt="Window Distribution Histogram" />
  <img src="art model-4/4.png" width="48%" alt="Custom Color Palettes" />
</p>

---

## 2. Starry Night Sky

A generative cosmos on a $360 \times 360$ canvas that pairs spatial uniformity with a heavy-tailed size distribution and size-conditioned color mapping[cite: 10, 12, 16]:

* **Spatial Coordinates (`X`, `Y`):** For a set number of stars (`NumStars`, default 200), each star independently samples continuous uniform coordinates across the sky[cite: 10, 11].
* **Heavy-Tailed Star Sizing (`USize` $\rightarrow$ `Radius`):** Each star draws a uniform helper variable and transforms it via an inverse power-law rule controlled by two parameters[cite: 11, 12, 15]:
  * $\theta_2$ (*Smallest star size*): Sets the baseline minimum radius[cite: 15].
  * $\theta_3$ (*How rare big stars are*): Controls tail decay so most stars remain tiny points while a rare few expand into dominant celestial giants[cite: 13, 14, 15].
* **Size-Conditioned Color Mapping:** Each star's palette index is linked to its generated radius[cite: 16], mapping smaller dust particles to lower indices and massive focal stars toward cooler periwinkle/blue tones[cite: 16, 18].

### Starry Canvas & Parameter Configuration
<p float="left">
  <img src="art model-2/1.png" width="48%" alt="Starry Night Sky Canvas" />
  <img src="art model-2/2.png" width="48%" alt="Starry Model Parameters" />
</p>

### Generated Multi-Sample Variations
<p float="left">
  <img src="art model-2/3.jpg" width="48%" alt="Starry Samples Part 1" />
  <img src="art model-2/4.jpg" width="48%" alt="Starry Samples Part 2" />
</p>

---

## Key Concepts Demonstrated

| Concept | Implementation in Models |
| :--- | :--- |
| **Parameters ($\theta$)** | User-adjustable dials set before sampling begins (e.g., office probability, minimum star radius, tail rarity)[cite: 7, 15]. |
| **Hierarchical Conditioning** | Building type is sampled once per building and governs the lighting distribution of all windows within it[cite: 2, 3]. |
| **Heavy-Tailed Distributions** | Transforming uniform draws (`USize`) to produce many small observations and rare extreme outliers (`Radius`)[cite: 12, 13, 15]. |
| **Feature Coupling** | Mapping continuous size (`Radius`) to discrete palette indices so visual color reinforces spatial hierarchy[cite: 16]. |

---

## License

This project is open-source and available under the [MIT License](LICENSE).
