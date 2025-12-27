# Geophysical Investigation of Subsurface Structure (Yellowstone · Biscuit Basin)

A compact geophysical data analysis project that integrates **seismic (refraction + reflection)**, **gravity**, and **magnetic** observations to infer subsurface structure beneath **Biscuit Basin, Yellowstone National Park**, motivated by the **2024 hydrothermal explosion** near the site.

This repo focuses on an end-to-end workflow:
**data loading → modeling/estimation → forward simulation → misfit evaluation → integrated cross-section visualization**.

---

## Project Context
Hydrothermal explosions can be driven by fluid/gas/heat accumulation in shallow crust. To better constrain subsurface conditions beneath Biscuit Basin, a multi-method geophysical profile was analyzed along a **50 km survey line** with **1 km station spacing** (seismic receivers + gravity + magnetics collected along the same transect).

---

## What This Project Does
- **Seismic Refraction**: fits the travel-time curve using **multi-segment linear regression** to estimate apparent P-wave velocities for multiple refracted phases.
- **Seismic Reflection**: applies **hyperbolic moveout** via linear regression of \(t^2\) vs \(x^2\) to estimate **reflection velocity** and **reflector depth**.
- **Gravity Forward Modeling**: uses prism/block-based models to simulate gravity anomalies and compares against observations using RMS misfit.
- **Magnetic Forward Modeling**: builds a multi-block magnetization model to reproduce observed magnetic anomalies and evaluates RMS misfit.
- **Integrated Interpretation**: combines seismic layering with gravity/magnetic anomaly blocks into a **complete cross-section**.

---

## Key Results (Highlights)

### Seismic Refraction (3 segments)
Estimated apparent velocities:
- Layer 1: **~4453 m/s** (0–16.7 km)
- Layer 2: **~5949 m/s** (16.7–33.3 km)
- Layer 3: **~6250 m/s** (33.3–50 km)

### Seismic Reflection (4 reflectors)
Estimated reflector velocity and depth:
- Reflector 1: **v ~ 2700 m/s**, **depth ~ 385 m**
- Reflector 2: **v ~ 3780 m/s**, **depth ~ 2119 m**
- Reflector 3: **v ~ 4712 m/s**, **depth ~ 4911 m**
- Reflector 4: **v ~ 5387 m/s**, **depth ~ 7984 m**

### Combined Seismic Velocity Model
A conceptual **five-layer** model with interfaces at approximately:
**385 m, 2110 m, 4910 m, 7984 m**, plus a bottom boundary near **~9 km**.

### Gravity Modeling
Forward models suggest **two low-density zones** (block-based):
- ~14–18 km along profile, depth ~1.5–4.0 km
- ~30–48 km along profile, depth ~2.5–9.5 km

### Magnetic Modeling
A three-block forward model reproduces the main magnetic anomaly shape with:
- RMS misfit **~3.035 nT**

### Integrated Interpretation (One-line summary)
Overlapping gravity + magnetic lows beneath/near the explosion site support a **thermally active system**: a **shallow hydrothermal zone** underlain by **deeper magmatic influence**.

---

## Repository Structure
- `Yellowstone_Subsurface_Analysis_RickDai.ipynb`  
  Seismic refraction + reflection estimation, gravity & magnetic forward modeling, and figure export.
- `SeismicCrossSection_RickDai.ipynb`  
  Builds the seismic velocity-layer cross section visualization.
- `CompleteCrossSection_RickDai.ipynb`  
  Integrates seismic layers + gravity/magnetic blocks into a complete cross section figure.
- `Geophysical Investigation of Subsurface Structure_Yellowstone_YuyangDai.pdf`  
  Full report (methods, results, discussion, limitations).
- `CSV`  
  CSV inputs for refraction/reflection/gravity/magnetic profiles.

---

## How to Run

### 1) Create & activate a virtual environment (optional but recommended)
```bash
python -m venv venv
````

Activate it:

* macOS / Linux

  ```bash
  source venv/bin/activate
  ```
* Windows

  ```bash
  venv\Scripts\activate
  ```

### 2) Install dependencies (based on imports in notebooks)

This repo does **not** include `requirements.txt`.
Install packages based on the `import ...` statements in the notebooks.

Typical packages:

```bash
pip install numpy pandas matplotlib scikit-learn jupyter
pip install harmonica verde pyrocko
```

If you see `ModuleNotFoundError`, install the missing package:

```bash
pip install <missing-package-name>
```

### 3) Run notebooks

```bash
jupyter notebook
```

Open and run:

* `Yellowstone_Subsurface_Analysis_RickDai.ipynb`
* `SeismicCrossSection_RickDai.ipynb`
* `CompleteCrossSection_RickDai.ipynb`

---

## Outputs

Typical generated outputs include:

* Gravity observed vs modeled comparison plot
* Magnetic observed vs modeled anomaly plot
* Seismic velocity-layer cross section
* Integrated complete cross section (seismic + gravity/magnetic features)

---

## Notes & Limitations

* Seismic layers are modeled as **flat interfaces with constant velocities** (conceptual simplification).
* Gravity/magnetic models use **block/prism geometry**; multiple subsurface configurations can fit similar anomalies (non-uniqueness).
* 2D profile + sparse spacing limits resolution; denser arrays and 3D inversion/modeling would improve interpretability.

---

## References

* Morgan, Shanks, & Pierce (2009). Hydrothermal processes above the Yellowstone magma chamber.
* Fournier (1989). Geochemistry and dynamics of Yellowstone hydrothermal system.
* Muñoz-Saez et al. (2016). Physical/hydraulic properties of sinter deposits.
* Brown et al. (2009). Lab measurements of crust–mantle boundary analog velocities.

```
