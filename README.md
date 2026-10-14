# Modelling the thermodynamic structure of the solar photosphere with machine-learning methods

Master's thesis, University of Belgrade, Faculty of Mathematics, 2026.

**Author:** David Živković
**Supervisor:** Dr. Ivan Milić, Assistant Professor, Faculty of Mathematics, University of Belgrade

**Thesis (PDF):** [`Zivkovic_MSc_thesis_2026.pdf`](Zivkovic_MSc_thesis_2026.pdf)
The thesis is written in Serbian (Cyrillic). The abstract below is an English translation, and the
code that implements it is documented in English.

**Code:** [pinn-solar-photosphere](https://github.com/davidzivkovic/pinn-solar-photosphere)

---

## Abstract (English translation)

Observations of the solar atmosphere do not provide its full three-dimensional structure. The
measured intensity is the solution of the radiative transfer equation along the line of sight, so
the contributions of different layers are entangled and the information about a large part of the
domain remains inaccessible. The aim of this thesis is to examine to what extent physics-informed
neural networks can reconstruct the full set of physical parameters of the solar photosphere from an
incomplete dataset.

A MURaM simulation of the solar photosphere with dimensions 300 × 300 × 48 points was used as the
test problem, in which the temperature, pressure, velocity field and magnetic field are known at
every point of the domain. The network is set up as a continuous representation of the domain, a
mapping from spatial coordinates to eight physical quantities, where the input coordinates pass
through a Fourier-feature encoder. The reconstruction was tested by deliberately removing layers of
constant height from the training set and reconstructing the missing part of the domain with the
help of additional terms in the loss function derived from the magnetohydrodynamic equations.

It is shown that introducing the condition ∇·**B** = 0 reduces the reconstruction error in layers
without data by 11% on average, with the largest gain for the components of the magnetic field, up
to 35% for B<sub>z</sub>. The stationary continuity equation brings an average improvement of 5%
and benefits the velocity field the most, up to 11% for v<sub>z</sub>. In both cases the improvement
in layers without data is accompanied by some deterioration in layers with data, which corresponds
to the expected compromise between agreement with the measurements and with the physical model.
Each equation helps most precisely the quantities it explicitly couples. The results show that
physical constraints can partially compensate for missing data, which is a step towards
reconstructing layers of the solar atmosphere that are inaccessible to direct observation.

**Keywords:** Sun, photosphere, magnetohydrodynamics, machine learning

*Original title:* Моделирање термодинамичке структуре фотосфере Сунца методама машинског учења

---

## Main results

Mean reduction of the reconstruction error (NRMSE<sub>σ</sub>) in height layers withheld from
training, relative to a reference network trained on the same layers without physics terms
(thesis Tables 4.1–4.3; 10 of 48 layers supervised):

| Constraint added to the loss | Mean improvement, layers without data | Largest single-field gain | Mean error change, layers with data |
|---|---|---|---|
| ∇·**B** = 0 | +11.25% | B<sub>z</sub> +34.62% | 9.71% → 11.24% |
| ∇·(ρ**v**) = 0 | +4.65% | v<sub>z</sub> +10.85% | 9.71% → 10.94% |
| Both | +12.96% | B<sub>z</sub> +33.85% | 9.71% → 12.34% |

The stationary momentum equation was also tested. Its residual in the simulation data is large, and
imposing it increased the error, so it is kept as a control experiment rather than as a constraint.

The three points the thesis draws from these runs:

1. Physical constraints can partially compensate for missing data.
2. Each equation most improves the quantities it explicitly couples (∇·**B** the magnetic field,
   ∇·(ρ**v**) the velocities), which indicates that the network uses the structure of the imposed
   constraint and not only the effect of additional regularization.
3. The improvement in layers without data is accompanied by some deterioration in layers with
   data, the expected compromise between agreement with the data and with the physical model.

## Scope and limitations

This is a proof of concept on simulated data and not a method ready for application to
observations. Layers were removed at constant geometric height, while spectropolarimetric
inversions return quantities on surfaces of constant optical depth. Only equations without time
derivatives could be used, since the work uses a single snapshot. The directions for further work
are listed in Chapter 5 of the thesis.

## Contents of the thesis

1. Introduction: the Sun, the solar atmosphere, simulations of the solar atmosphere
2. Machine learning: supervised learning, neural networks, Fourier-feature encoding, physics-informed neural networks
3. Data and the reconstruction method: MURaM data, network architecture, choice of parameters, choice of equations
4. Results: training on complete data, removal of layers, addition of physical equations, comparison of synthetic spectra
5. Conclusion and further work

## Citation

See [`CITATION.cff`](CITATION.cff).
