# XZT-XFS_TMT_VIV_model
A MATLAB implementation of a 2-DOF mixed Timoshenko beam–wake oscillator solver for vortex-induced vibration analysis, including dynamic axial-tension feedback, semi-rigid boundary conditions, RK4/Newmark-β time integration, modal verification, and direct recovery of bending moment, shear force, and stress indicators.
# IMU-TJU TMT-VIV Model

A two-degree-of-freedom mixed Timoshenko beam–wake oscillator solver for vortex-induced vibration analysis of flexible cylindrical structures.

> **Code release status**  
> This repository is currently prepared as a pre-release project page.  
> The full simulation code, examples, and documentation will be formally open-sourced after the associated research paper is accepted or published.

---

## Overview

This project provides a MATLAB-based reduced-order solver for the two-degree-of-freedom vortex-induced vibration (VIV) response of long flexible circular cylinders. The model combines a mixed Timoshenko beam formulation with acceleration-coupled wake oscillators, enabling simultaneous prediction of displacement response, dynamic axial-tension feedback, internal-force distribution, and boundary-sensitive hotspot behaviour.

Unlike displacement-only beam formulations, the present model retains both transverse displacements and sectional rotations as independent unknowns. This allows bending moment, shear force, bending stress, and shear-stress indicators to be recovered directly from the solved structural fields rather than reconstructed only from displacement derivatives.

The solver is designed for research on flexible risers, marine cables, slender cylindrical structures, and wake–structure interaction problems where displacement amplitude alone is insufficient and mechanically interpretable internal-force information is required.

---

## Main Features

- Two-degree-of-freedom in-line and cross-flow VIV simulation
- Mixed Timoshenko beam formulation with independent displacement and rotation variables
- Acceleration-coupled Van der Pol wake oscillators
- Staggered RK4/Newmark-β time-integration framework
- Dynamic axial-tension feedback based on geometric stretching
- Direct recovery of bending moment, shear force, bending stress, and shear-stress indicators
- Unified boundary treatment for pinned, clamped, free, guided, semi-rigid, and elastic supports
- Ghost-point central-difference implementation for endpoint boundary conditions
- Modal-analysis branch for dry or still-water natural-frequency verification
- Time-domain response statistics, RMS envelopes, internal-force hotspots, and post-processing exports
- Support for ultra-slender configurations and non-uniform incoming-flow profiles

---

## Physical and Numerical Model

The structural subsystem is based on a mixed Timoshenko beam model. For each transverse direction, the structural equations are expressed in terms of displacement and sectional rotation. The internal force quantities are recovered as

- bending moment from the sectional rotation gradient,
- shear force from the Timoshenko shear deformation,
- resultant bending moment and resultant shear force from the in-line and cross-flow components.

The wake subsystem is represented by modified Van der Pol-type wake oscillators. The in-line wake variable describes the fluctuating drag component, while the cross-flow wake variable describes the fluctuating lift component. The wake equations are coupled to the structural acceleration.

The full time-domain solver uses a staggered explicit–implicit strategy:

- the wake oscillators are advanced explicitly by the fourth-order Runge–Kutta method;
- the structural subsystem is advanced implicitly by the average-acceleration Newmark-β method;
- dynamic axial tension is updated within the time-marching process when axial-tension feedback is activated.

When the hydrodynamic excitation is switched off, the wake subsystem is bypassed and the solver reduces to a structural modal-analysis or free-vibration verification framework.

---

## Boundary Conditions

The code supports a unified endpoint-boundary framework. The following support types are included:

- `pinned_pinned`
- `clamped_clamped`
- `free_free`
- `guided_guided`
- `semi_rigid_both`
- `elastic_both`
- mixed boundary cases, such as clamped–free or clamped–pinned
- manual boundary specification

Semi-rigid and elastic supports are represented through translational and rotational stiffness/damping parameters. This allows continuous transition between idealised pinned and clamped conditions and enables the effect of support stiffness on end-region bending and shear hotspots to be evaluated.

---

## Repository Status

This repository is currently under preparation.

The full source code will be released after publication of the associated manuscript. The public release is expected to include:

- MATLAB source code
- example input files
- benchmark case settings
- plotting and post-processing scripts
- documentation for key parameters
- instructions for reproducing the main figures
- license information

Until the formal release, this repository may contain only the README, release notes, and partial documentation.

---

## Planned Code Structure

The final open-source version is expected to follow a structure similar to:

```text
IMU-TJU_TMT_VIV_model/
│
├── README.md
├── LICENSE
├── main/
│   └── main_Timo2DOF_VIV.m
│
├── src/
│   ├── assembly/
│   ├── boundary/
│   ├── wake/
│   ├── time_integration/
│   ├── postprocessing/
│   └── utilities/
│
├── examples/
│   ├── modal_verification/
│   ├── viv_uniform_flow/
│   ├── viv_sheared_flow/
│   └── semi_rigid_boundary/
│
├── data/
│   └── reference_data/
│
└── docs/
    └── parameter_description.md
