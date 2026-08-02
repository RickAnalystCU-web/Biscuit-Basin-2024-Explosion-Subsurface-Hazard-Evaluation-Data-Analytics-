# Biscuit Basin Subsurface Hazard Evaluation

Geophysical analysis of the subsurface structure beneath Biscuit Basin in Yellowstone National Park, motivated by the 2024 hydrothermal explosion near the site. The project combines seismic refraction, seismic reflection, gravity, and magnetic observations along a 50 km survey profile.

The complete methods, results, discussion, and limitations are documented in the [project report](Geophysical%20Investigation%20of%20Subsurface%20Structure_Yellowstone_YuyangDai.pdf).

## Analysis Workflow

1. Load the four profile datasets from the repository root.
2. Estimate apparent P-wave velocities from three linear refraction segments.
3. Estimate reflection velocities and reflector depths from linear fits of `t^2` against `x^2`.
4. Forward-model gravity anomalies with subsurface prisms and compare model RMS misfits.
5. Forward-model the magnetic anomaly with a three-block magnetization model.
6. Combine the seismic layers and gravity/magnetic bodies in an interpreted cross section.

## Repository Guide

| File | Purpose |
| --- | --- |
| [`Yellowstone_Subsurface_Analysis_RickDai.ipynb`](Yellowstone_Subsurface_Analysis_RickDai.ipynb) | Primary analysis: seismic estimation, gravity and magnetic forward models, RMS evaluation, and figure export. |
| [`SeismicCrossSection_RickDai.ipynb`](SeismicCrossSection_RickDai.ipynb) | Constructs the layered seismic velocity cross section. |
| [`CompleteCrossSection_RickDai.ipynb`](CompleteCrossSection_RickDai.ipynb) | Combines seismic layers with interpreted gravity and magnetic bodies. |
| [`yellowstone_refractions.csv`](yellowstone_refractions.csv) | Profile distance and P-wave refraction arrival times. |
| [`yellowstone_reflections.csv`](yellowstone_reflections.csv) | Profile distance and four P-wave reflection arrival series. |
| [`yellowstone_gravity.csv`](yellowstone_gravity.csv) | Profile distance and gravity anomaly observations. |
| [`yellowstone_magnetics.csv`](yellowstone_magnetics.csv) | Profile distance and magnetic anomaly observations. |
| [`Geophysical Investigation of Subsurface Structure_Yellowstone_YuyangDai.pdf`](Geophysical%20Investigation%20of%20Subsurface%20Structure_Yellowstone_YuyangDai.pdf) | Full project report. |

All notebook input paths are relative to the repository root. Run the notebooks from this directory so the CSV files resolve without path changes.

## Methods

- **Seismic refraction:** multi-segment linear regression of travel time against distance to estimate apparent P-wave velocities.
- **Seismic reflection:** hyperbolic moveout linearized as `t^2 = A + Bx^2` to estimate reflection velocity and depth.
- **Gravity modeling:** prism-based forward models evaluated against observations with RMS misfit.
- **Magnetic modeling:** a three-block magnetization model evaluated against observations with RMS misfit.
- **Integrated interpretation:** seismic layering and gravity/magnetic bodies assembled in a single conceptual cross section.

## Reported Results

The values below summarize the results already reported by the project; the notebooks and report provide the supporting calculations and interpretation.

### Seismic Refraction

| Segment | Profile interval | Apparent P-wave velocity |
| --- | ---: | ---: |
| 1 | 0-16.7 km | approximately 4,453 m/s |
| 2 | 16.7-33.3 km | approximately 5,949 m/s |
| 3 | 33.3-50 km | approximately 6,250 m/s |

### Seismic Reflection

| Reflector | Estimated velocity | Estimated depth |
| --- | ---: | ---: |
| 1 | approximately 2,700 m/s | approximately 385 m |
| 2 | approximately 3,780 m/s | approximately 2,119 m |
| 3 | approximately 4,712 m/s | approximately 4,911 m |
| 4 | approximately 5,387 m/s | approximately 7,984 m |

The combined interpretation is a conceptual five-layer velocity model with interfaces near 385 m, 2,110 m, 4,910 m, and 7,984 m, plus a lower boundary near 9 km.

### Gravity and Magnetics

The gravity forward models suggest two interpreted low-density zones:

- approximately 14-18 km along the profile and 1.5-4.0 km depth;
- approximately 30-48 km along the profile and 2.5-9.5 km depth.

The three-block magnetic forward model reports an RMS misfit of approximately 3.035 nT. In the project interpretation, overlapping gravity and magnetic lows beneath or near the explosion site are consistent with a shallow hydrothermal zone and deeper magmatic influence.

## Running the Notebooks

Python 3 and Jupyter are required. The repository does not include a pinned environment or `requirements.txt`; the package list below reflects the imports in the notebooks.

```bash
python -m venv .venv
```

Activate the environment:

```bash
# macOS or Linux
source .venv/bin/activate

# Windows PowerShell
.venv\Scripts\Activate.ps1
```

Install the imported packages:

```bash
python -m pip install jupyter numpy pandas matplotlib scikit-learn harmonica verde pyrocko
```

Start Jupyter from the repository root:

```bash
jupyter notebook
```

For the clearest progression, review or run the notebooks in this order:

1. `Yellowstone_Subsurface_Analysis_RickDai.ipynb`
2. `SeismicCrossSection_RickDai.ipynb`
3. `CompleteCrossSection_RickDai.ipynb`

Running the notebooks writes PNG figures to the repository root, including the refraction and reflection fits, gravity and magnetic model comparisons, and cross sections.

## Assumptions and Limitations

- Seismic layers are represented by flat interfaces with constant velocities.
- Gravity and magnetic models use block/prism geometries; multiple subsurface configurations can fit similar anomalies.
- The analysis is based on a two-dimensional profile with 1 km station spacing, which limits spatial resolution.
- Denser observations and three-dimensional modeling could improve subsurface resolution.

## References

- Morgan, Shanks, and Pierce (2009). Hydrothermal processes above the Yellowstone magma chamber.
- Fournier (1989). Geochemistry and dynamics of the Yellowstone hydrothermal system.
- Munoz-Saez et al. (2016). Physical and hydraulic properties of sinter deposits.
- Brown et al. (2009). Laboratory measurements of crust-mantle boundary analog velocities.
