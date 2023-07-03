# Learned-1-D-advection-with-GEOS-FP-wind
This codebase demonstrates the machine-learned 1-D advection with GEOS-FP wind field. (Under construction now)

## Introduction
This repository has the code to train and implement CNN-based 1-D horizontal advection emulating L94 type advection solver. The spatial domain is the North American grid of GEOS-FP (refer to https://wiki.seas.harvard.edu/geos-chem/index.php/GEOS-Chem_horizontal_grids#GMAO_0.25_x_0.3125_grid). This work also includes a trial in 2-D horizontal advection with the nondirectional splitting mechanism in LR96 paper. Basically, this repository contains Julia codes in Jupyter Notebook to emulate the L94 advection scheme in 1-D and 2-D.

This project is an extension of our previous repository (https://github.com/manozzing/Learned-1-D-advection-solver-with-grid-spacing-physics). We found out a mistake in latitude/longitude confusion and corrected it here. We also extend our scope into 2-D applications.

The aims of this project include:

* Develop a surrogate scheme of 1-D horizontal passive scalar advection with spatial and temporal coarse-graining
* Evaluate the performance of surrogate schemes in accuracy and computational speed
* Test the generalization ability of the learned scheme in the regime out of the training dataset
* Implement 2-D horizontal advection using the learned solver trained here.

## Main Directory (here)

1. 8x16t_** - Those figures are the visualization of an example demonstration in 8-time spatial coarsening and 16-time temporal coarsening.

2. Velocity_Sampling_using_Julia.ipynb - This notebook has Julia codes to collect the velocity components (u and v at the ground level) from the GEOS-FP meteorological data.

## Velocity_corrected Directory

This directory has the velocity datasets used in this study. We specified the name of the csv files as "velocity component (u or v)"_"month"_"a location the 1-D line passes"_"time span of the data (optional, whether 10 or 30)."

## advect_NN Directory

1. Van_Leer_Type_Scheme_(L94).ipynb - This notebook has functions to integrate the passive scalar advection with a given initial condition and wind velocity field. This notebook is used to generate training/testing dataset. For the testing dataset, we made separate notebooks to demark notebooks for the generalization dataset, further extending to the advection in the longitudinal direction, and longer time span.

2. 1d_adv_Conv1D_spacing_phys_normalized.ipynb - This notebook has codes to build (or load) CNN model and train the model. 1d_adv_Conv1D_spacing_phys_normalized-gpu.ipynb is a trial to use GPU and is not yet completed.

3. 1d_conv_wo_phys_stats_zero_grad.ipynb - This notebook has codes to bring in the model output and calculate statistical indices including MAE, RMSE, r<sup>2</sup>.

4. 1d_gen_test_**.ipynb - This notebook has codes to test the generalization ability of learned models in several different conditions, including the changes in the timespan, initial conditions, spatial domain (longitudes and latitudes), and seasons.

5. 2D Velocity_Sampling.ipynb - This notebook is the 2-D version of velocity sampling. The sampled velocity fields were used in 2-D implementation.

6. 2D Velocity downsampling.ipynb - This notebook is used to downsample the 2-D velocity.

7. 2d_advection.ipynb - This notebook has codes to implement 2-D horizontal advection using LR96 mechanism both in the traditional approach (with L94 1-D advection) and the data-driven approach (the learned 1-D advection solver developed here).

8. Map_Visualization.ipynb - This code is used to create a figure displaying the spatial domain we studied.

9. Max_CFL_Calculation.ipynb - The code in this notebook can be used to calculate the maximum CFL number in a velocity dataset.

10. Testing speed.ipynb - This notebook has codes to benchmark the computational time spent to implement advection.

## Data
1. models_and_outputs - The model parameters and outputs will be uploaded in a separate Zenodo space due to the large volume.

## Acknowledgment
This work is financially supported by the Early Career Faculty grant of National Aeronautics and Space Administration (grant no. 80NSSC21K1813). MP is supported by the Carver Fellowship and Illinois Distinguished Fellowship.
