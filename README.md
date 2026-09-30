# Cushion Impact & Damping Model

A browser-based calculator for packaging cushion design. It predicts peak deceleration (G), plots cushion curves, and derives an equivalent spring–dashpot model for packaging cushions, using published stress–energy constants. All units are metric.

**Live app:** https://YOUR-USERNAME.github.io/YOUR-REPO-NAME/

Core relations:

```
E  = σs · h / t          energy density, kJ/m³
Gm = σm(E) / σs          peak deceleration, multiples of g
```

where σs is static stress, h is drop height, t is cushion thickness, and σm is dynamic stress from the material's fitted curve.

---

## Features

### Cushion curves
- Peak G versus static stress for every selected material, at the current drop height and thickness
- Cushion coefficient (C = σm / E) versus dynamic stress; the minimum of each curve marks the material's most efficient working stress
- Operating point summary and a results table showing energy density, dynamic stress, G, strain band, best loading, bearing area needed for best loading, and pass/fail against the fragility limit
- Results export to CSV

### Damping
- Reduces the cushion to a single-degree-of-freedom spring and dashpot that reproduces the predicted peak G
- Reports natural frequency, stiffness, equivalent dynamic modulus and pulse duration
- With a measured rebound height: coefficient of restitution, damping ratio, damping coefficient, loss factor, Q, energy dissipated and velocity change
- Shock pulse plot (deceleration vs. time) and vibration transmissibility plot for resonance checks

### Fit your test data
- Paste your own drop test results and fit stress–energy constants (exponential and polynomial forms), with R² fit quality
- Add the fitted result as a custom material and compare it against the library

### Constants & sources
- Full material library with constants, fit form, R², supported range, and whether the data is measured or simulation-only
- Source references and a summary of the model's limits

---

## How to use

1. Open the live link in any modern browser (Chrome, Edge, Firefox, Safari). Nothing to install.
2. In the left panel, enter the **drop condition**: product mass (kg), drop height (mm), cushion thickness (mm), fragility limit (g), and bearing width × depth (mm). Bearing area is the total contact footprint of all pads on one face.
3. Tick the **materials** you want to compare.
4. Optionally enter a **measured rebound height** (mm) to enable the damping results.
5. Switch between the tabs to view curves, damping, fitting and sources. Hover over any chart for a crosshair readout.

### Input format for fitting

One drop per line, comma-separated:

```
drop height mm, thickness mm, static stress kPa, peak G
600, 50, 5.5, 41
450, 50, 5.5, 33
600, 25, 5.5, 88
```

Five columns are also accepted, with mass (kg) and bearing area (mm²) replacing static stress:

```
drop height mm, thickness mm, mass kg, area mm², peak G
```

---

## Material library

| Material | Basis | Source |
|---|---|---|
| EPE foam, 18 kg/m³ (exponential fit) | Measured | Xing, Sun & Chen 2023 |
| EPE foam, 18 kg/m³ (polynomial fit) | Measured | Xing, Sun & Chen 2023 |
| Ethafoam Select PE, 30 kg/m³ | Measured | Daum 2006 |
| Honeycomb paperboard, type A, 10 mm cell | Measured (drop-validated FE model) | Wu et al. 2026 |
| Rigid polyurethane foam | Simulation only | Wu et al. 2026 |
| Aluminium foam, 80.8% porosity | Simulation only | Wu et al. 2026 |

Every constant is transcribed from a published fit; nothing is interpolated between densities or carried over from similar grades. Results outside a material's supported range are flagged in the app.

---

## Model limits

- **Energy assumption.** E = σs·h/t assumes all drop energy goes into the cushion. Rebound returns some of it, so G is slightly conservative.
- **Strain is a band.** Reported as 1/C (constant-stress crushing) to 2/C (linear spring). Above roughly 70% strain the cushion densifies and the curve no longer holds.
- **Damping needs measured rebound.** It cannot be derived from a cushion curve alone.
- **Material type.** The stress–energy method was developed for closed-cell foams and corrugated structures. Open-cell polyurethane and similar materials can fit poorly.
- **First drop only.** Foams stiffen after the first impact; multi-drop sequences need second-to-fifth-drop constants.
- **One grade, one curve.** A different density, flute or supplier is a different material. Refit rather than scale.

This tool supports design estimates. It does not replace ASTM D1596 cushion testing or ISTA qualification testing.

---

## Notes

- Single self-contained HTML file, no external libraries or internet connection needed after loading.
- Custom materials added from the fitting tab are kept only for the current session and are cleared when the page is reloaded.
- Owner: Packaging Engineering.

## References

- Daum M. *A simplified process for determining cushion curves: the stress–energy method.* Proc. International Conference on Transport Packaging (Dimensions.06), San Antonio TX.
- Xing Y., Sun D. & Chen G. *Analysis of the dynamic cushioning property of expanded polyethylene based on the stress–energy method.* Polymers 2023, 15(17), 3603. doi:10.3390/polym15173603
- Wu Z., Xi Z., Li Y., Xiang X. & Li R. *Dynamic impact characteristics of airdrop cushioning materials and a C−σm curve-based cushioning pad design method.* Materials 2026, 19(12), 2526. doi:10.3390/ma19122526
- ASTM D1596, *Standard test method for dynamic shock cushioning characteristics of packaging material.*
