# Probabilistic Generative Paintings: City at Night & Starry Night Sky

An interactive exploration of probabilistic programming and generative art, translating statistical distributions into visual stories. Built as two distinct generative models—**City at Night** and **Starry Night Sky**—each canvas renders a brand-new scene on every sample by drawing from parameterized probability distributions[cite: 7, 15, 18].

---

## 1. City at Night

A generative streetscape of 24 buildings where architectural purpose drives nighttime lighting patterns[cite: 2, 3]. Rather than treating every window independently with a single global probability, the model uses a hierarchical structure[cite: 1, 2, 3]:

* **Building Height (`NumFloors`):** Each of the 24 buildings independently samples a discrete uniform integer height between 7 and 16 floors[cite: 2, 3].
* **Building Type (`Bernoulli`):** Each building flips a weighted coin controlled by parameter $\theta_3$ (*"Chance a building is an office"*)[cite: 5, 7]. 
  * **Office Towers:** Low probability of lit windows, creating dark silhouettes late at night[cite: 2, 7].
  * **Residential Apartments:** High probability of lit windows, producing bright, lived-in towers[cite: 2, 7].
* **Window Lighting:** Conditioned on the building's type, each floor/window flips its own coin to determine whether it is illuminated[cite: 2, 3].

This two-stage hierarchy reproduces the bimodal distribution seen in real cityscapes—where most buildings are either nearly dark or brightly lit, rather than every building hovering around the same average brightness[cite: 1, 3, 5].

---

## 2. Starry Night Sky

A generative cosmos on a $360 \times 360$ canvas that pairs spatial uniformity with a heavy-tailed size distribution and size-conditioned color mapping[cite: 10, 12, 16]:

* **Spatial Coordinates (`X`, `Y`):** For a set number of stars (`NumStars`, default 200), each star independently samples continuous uniform coordinates across the $360 \times 360$ sky[cite: 10, 11].
* **Heavy-Tailed Star Sizing (`USize` $\rightarrow$ `Radius`):** Each star draws a uniform helper variable $U \in [0, 1]$ and transforms it via an inverse power-law rule controlled by two parameters[cite: 11, 12, 15]:
  * $\theta_2$ (*Smallest star size*): Sets the baseline minimum radius (e.g., `1.5`)[cite: 15].
  * $\theta_3$ (*How rare big stars are*): Controls the tail decay so that the vast majority of stars form a fine mist of tiny points while a rare few expand into dominant celestial giants[cite: 13, 14, 15].
* **Size-Conditioned Color Mapping:** Rather than assigning colors purely at random, each star's palette index is linked to its generated radius[cite: 16]. Using a 5-swatch palette (such as the **Gold** theme featuring warm cream/pink accents alongside cool periwinkle-blue giants), smaller dust particles cluster in the lower indices while massive stars shift toward the upper-index focal tones[cite: 16, 18].

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
