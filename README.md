# Grain Hill Model


## About

This repository contains source code for the Grain Hill cellular automaton model.
 Grain Hill simulates the morphology and evolution of a hypothetical hillslope cross-sectional profile. The model builds on [CellLab-CTS](https://github.com/landlab/landlab/wiki/CellLab-CTS-2015-Users-Manual) framework, which is an element of the [Landlab Toolkit](http://landlab.github.io).  The package includes the Grain Facet model, which is a variant of Grain Hill that models the cross-sectional profile evolution of a normal-fault facet, with slip on a 60-degree dipping normal fault. The Grain Hill and Grain Facet models, their underlying continuous-time stochastic algorithms, and the Landlab framework on which they are built, are described in several journal articles. Tucker et al. (2016) present the general CellLab-CTS framework and its algorithms. Tucker et al. (2018) describe the Grain Hill model, and use the model to analyze a range of different types of hillslope landform. Tucker et al. (in review) present the Grain Facet model and use it to analyze the necessary and sufficient conditions to account for observed facet landforms and their variations. The Landlab Toolkit itself is described by Hobley et al. (2017) and Barnhart et al. (in review).


## Dependencies

Grain Hill requires [Landlab](https://landlab.github.io) version 2.0.0beta or higher, and [bmipy](https://github.com/csdms/bmi-python).


## Installation

Clone or fork this repository. To install, navigate to the `grain_hills` folder and run `python setup.py`.


## How to Run

The simplest usage is to navigate to the `grain_hills` folder in a terminal window, and run:

`python run_grain_hill.py <input file>`

A good starting example, available in the `examples` folder, is:

`python run_grain_hill.py examples/small_regolith_hill.txt`

GrainHill can also be run using [Basic Model Interface (BMI)](https://bmi.readthedocs.org) functions executed in a Python script, shell, or notebook. Because the GrainHill (and BlockHill and GrainFacetSimulator) models are implemented as classes, they can be directly instantiated and initialized in a Python script, with parameters passed as individual arguments to the `__init__` method, or in a dictionary (passed using `**` preceding the name of the dictionary).


## Input and Output Files

The `run_grain_hill.py` script reads parameters from a text file in `yaml` format. An example is:

    # GrainHill input file:
    #
    # small_regolith_hill: runs a simulation with steady uplift and
    # all regolith material (no rock)
    #
    number_of_node_rows: 40
    number_of_node_columns: 92
    cell_size: 0.1
    grav_accel: 9.8
    friction_coef: 1.0
    run_duration: 3000.0
    uplift_interval: 100.0
    disturbance_rate: 0.01
    weathering_rate: 0.001
    rock_state_for_uplift: 7
    opt_rock_collapse: 0
    opt_track_grains: False
    save_plots: True
    plot_filename: 'small_hill'
    plot_filetype: '.png'
    plot_interval: 500.0
    output_interval: 1.0e20
    report_interval: 5.0

GrainHill output is saved in Landlab native format, and can be opened and read using the Landlab `load_grid` function (`from landlab.io.native_landlab import load_grid`). This saves the Landlab grid object along with all of its fields, including the `node_state` field that encodes the current state code for each node in the grid. For information on the native Landlab format, see the documentation for the [`save_grid`](https://landlab.readthedocs.io/en/master/reference/io/native_landlab.html#landlab.io.native_landlab.save_grid) and [`load_grid`](https://landlab.readthedocs.io/en/master/reference/io/native_landlab.html#landlab.io.native_landlab.load_grid) functions.

In addition, if `save_plots` is `True` and the `plot_interval` is less than the `run_duration`, plots will be saved to files in addition to being displayed on screen (the default format is .png; this can be changed using the `plot_filetype` parameter).


## Examples

Several example input files can be found in the `examples` folder.


## Running tests

If you have `pytest` installed, you can run the built-in tests by navigating to the `grainhill` folder and running:

`pytest --doctest-modules`

The result should say something like: `22 passed` (plus some number of warnings, which you can usually safely ignore).


## How to Cite

Recommended citations:

- GrainHill package: Tucker et al. (2018)
- GrainFacet package: Tucker et al. (in review)
- CellLab-CTS : Tucker et al. (2016)
- Landlab Toolkit: Hobley et al. (2017), Barnhart et al. (in review)


## References:

Barnhart, K. R., et al. (in review) Landlab v2.0: A software package
for Earth surface dynamics.

Tucker, G. E., Hobley, D. E. J., McCoy, S. W., & Struble, W. T. (in review). Modeling the Shape and Evolution of Normal-Fault Facets.

Tucker, G. E., McCoy, S. W., & Hobley, D. E. (2018). [A lattice grain model of hillslope evolution.](https://doi.org/10.5194/esurf-6-563-2018) Earth Surface Dynamics, 6(3), 563-582, doi:10.5194/esurf-6-563-2018.

Hobley, D. E., Adams, J. M., Nudurupati, S. S., Hutton, E. W., Gasparini, N. M., Istanbulluoglu, E., & Tucker, G. E. (2017) [Creative computing with Landlab: an open-source toolkit for building, coupling, and exploring two-dimensional numerical models of Earth-surface dynamics.](https://www.earth-surf-dynam.net/5/21/2017/) Earth Surface Dynamics. doi:10.5194/esurf-5-21-2017.

Tucker, G.E., Hobley, D.E.J., Hutton, E., Gasparini, N.M., Istanbulluoglu, E., Adams, J.M., and Nudurupati, S.S. (2016) CellLab-CTS 2015: [Continuous-time stochastic cellular automaton modeling using Landlab.](https://www.geosci-model-dev.net/9/823/2016/) Geoscientific Model Development., v. 9, p. 823-839, doi:10.5194/gmd-9-823-2016.
