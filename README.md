# Near-unity absorption in J-aggregate gratings

Code for the paper

> M. V. Rodrigues, M. S. Barreiro, M. I. Vasilevskiy, N. M. R. Peres and G. A. Farias,
> *Tunable Near-Unity Light Absorption via Surface Exciton-Polaritons in Periodic Gratings of
> Anisotropic Polarizable Materials*, J. Phys.: Condens. Matter (submitted).

## Model

A TM-polarized plane wave hits a one-dimensional grating of ribbons made of a nearly two-dimensional
polarizable material (a J-aggregate film in all examples). The ribbons lie at the interface between two
dielectrics; the lower one is a spacer of thickness *d* on top of a Drude metal. The ribbons are treated as a
polarization sheet with in-plane and out-of-plane susceptibilities (Felderhof–Marowsky boundary conditions).
The fields are expanded in Bloch orders −N…N, and the boundary conditions give a linear system for the
reflected and transmitted amplitudes (Eq. (21) of the paper). From its solution the notebook computes the
reflectance *R*, the power *A*<sub>m</sub> that enters the metal and the absorptance of the layer,
*A*<sub>J</sub> = 1 − *R* − *A*<sub>m</sub>.

## Files

| | |
|---|---|
| `J_aggregate_gratings.ipynb` | the model and all figures |
| `figures/` | the figures produced by the notebook (PDF) |
| `requirements.txt` | Python packages |

## Running

```
pip install -r requirements.txt
jupyter notebook J_aggregate_gratings.ipynb
```

Run the cells in order. A full run takes about 7 minutes on a laptop, most of it in Fig. 8; with
`FAST = True` (first code cell) the maps of Fig. 8 use a coarser grid. Tested with Python 3.13, NumPy 2.5,
SciPy 1.18 and Matplotlib 3.11.

## Figures

| paper | file in `figures/` |
|---|---|
| Fig. 2 | `band_structure.pdf` |
| Fig. 3 | `Absorbance_for_different_R.pdf`, `Absorbance_for_different_R_zoom.pdf` |
| Fig. 4 | `Absorbance_for_different_angles.pdf`, `Absorbance_for_different_angles_psi_30.pdf` |
| Fig. 5 | `Absorbance_for_different_filling_factors.pdf` |
| Fig. 6 | `Absorbance_with_and_without_metal.pdf` |
| Fig. 7 | `Absorbance_for_different_values_of_d.pdf`, `Absorbance_for_different_d.pdf` |
| Fig. 8 | `Absorptance_limit_lossy_metal.pdf` |
| Fig. R1 of the reply to the referees | `Absorbance_for_different_angles_psi_50.pdf` |

Fig. 1 (sketches of the system) is not generated here. The last section of the notebook also prints the
numbers quoted in the reply to the referees: air superstrate, closed form for a homogeneous sheet, and the
absorption in a silver mirror.

## Notes

- SI units, time dependence e<sup>−iωt</sup>, frequencies given as ω/ω<sub>0</sub> with ħω<sub>0</sub> = 2.1 eV.
  Default parameters: ε<sub>1</sub> = ε<sub>2</sub> = 2.3, ε<sub>b</sub> = 1, *f*<sub>0</sub> = 10 nm,
  ħγ<sub>0</sub> = 0.01 eV, Ψ = 15°, *R* = 70 nm, *F* = 0.75, *d* = 60 nm, ħω<sub>p</sub> = 9 eV, *N* = 50.
- The geometry is kept in module-level variables set by `configure()`. Calling it without arguments restores
  the values of the paper. Temporary changes (lossy or no metal, other superstrate, other oscillator
  strength) are context managers, so they are undone at the end of the `with` block.
- The ribbon edges are smoothed by a Gaussian of width σ, chosen for each filling factor, so that the Fourier
  series of the susceptibility converges.
- `power_balance` evaluates the flux into region III at the metal surface, *z* = −*d*. This only matters for a
  lossy metal; for a transparent region III it is the transmittance, and for the lossless metal it vanishes.
- The Fourier matrices are kept in single precision, as in the calculations of the paper. The source term of
  the linear system is now computed in double precision; the spectra change by less than 10<sup>−7</sup>.

## Citation

If you use this code, please cite the paper above and the archived version of the code:
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.23669740.svg)](https://doi.org/10.5281/zenodo.23669740)
