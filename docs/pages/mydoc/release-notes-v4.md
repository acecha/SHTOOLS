---
title: "SHTOOLS release notes: Version 4"
keywords: spherical harmonics software package, spherical harmonic transform, legendre functions, multitaper spectral analysis, fortran, Python, gravity, magnetic field
sidebar: mydoc_sidebar
permalink: release-notes-v4.html
summary:
toc: true
---

## Version 4.4

**New Slepian expansion routines**

* Added the new Fortran 95 functions `SHRotateTapers` for rotating spherical cap Slepian functions, `SlepianCoeffs` for expanding a function in a Slepian basis, and `SlepianCoeffsToSH` to convert the Slepian coefficients into spherical harmonic coefficients.
* Added two python classes `Slepian` and `SlepianCoeffs` for managing Slepian basis functions and the Slepian expansion coefficients of a function.

**Legendre and spherical harmonic convenience functions**

* Added 4 python convenience functions for computing Legendre and spherical harmonic functions: `legendre()` to compute all the legendre functions, `legendre_lm()` to compute the legendre function for a specified degree and order, `spharm()` to compute all the spherical harmonic functions, and `spharm_lm()` to compute the spherical harmonic functions for a specific degree and order.

**Other improvements**

* Added the option to perform a weighted least squares inversion in the fortran routine `SHExpandLSQ`, and added a python wrapped function `SHExpandWLSQ()`.
* Added `min()` and `max()` methods to the `SHGrid` class, to return the minimum and maximum value of the gridded data.
* Added the property `mass` to the `SHGravCoeffs` class, which is computed by the input GM and the codata value for `G`.
* Add the optional parameter `omega` to `SHGravCoeffs.geoid()` to override the value provided in the class instance.
* Fixed some minor typos and usability issues, and cleaned up the python wrapper and signature files.

M. A. Wieczorek, M. Meschede, E. Sales de Andrade, I. Oshchepkov, B. Xu, and A. Walker (2018). SHTOOLS: Version 4.4, Zenodo, doi:[10.5281/zenodo.592762](https://doi.org/10.5281/zenodo.592762)

## Version 4.3

**New Gravity and Magnetic field classes**

* Added gravity classes `SHGravCoeffs`, `SHGravGrid`, `SHGravTensor` and `SHGeoid`.
* Added magnetic field classes `SHMagCoeffs`, `SHMagGrid`, and `SHMagTensor`.
* Added new fortran subroutine `MakeMagGradGridDH`, which is analogous to `MakeGravGradGridDH`.
* Reorded the arguments of `CilmPlusRhoHDH` to be consistent with `CilmPlusDH`.
* The python routine `MakeMagGridDH` now also outputs the magnetic potential as a grid.

**Better figures**

* Addition of the function `pyshtools.utils.figstyle()`, that sets several matplotlib parameters for better figures. This function takes as optional parmeters the maximum useable width of a journal page, the relative width of the figure with respect to this value, and the screen resolution in dpi.
* Most plotting routines have optional parameters to set minor tick intervals, grids, label font size, and tick font size.
* Degree symbols are plotted on tick labels for maps.
* `examples/python/Common/FigStyle.py` was removed from the examples.
* Added the options `vmin` and `vmax` to the plotting methods `SHCoeffs.plot_spectrum2d()` in order to specify the limits of the color scale.
* Added the option to plot colorbars on `SHGrid` plots, along with the option to specify their orientation and a text label.
* All notebooks have been updated.

**New constant subpackage**

* The `constant` subpackage has been completely rewritten and now makes use of the [astropy](http://docs.astropy.org/en/latest/constants/index.html) `Constant` class. This class has attributes `name`, `value`, `uncertainty`, `unit`, and `reference`. The naming of the constants has changed in some cases for consistency. A few constants that are not necessary were removed. Many of the constants were updated with more recent values. `Constants` can be used in arithmetic operations with either other `Constants` or with objects of the astropy class `Quantity`.
* Constants are organized into modules for each of the planets (`Mercury`, `Venus`, `Earth`, `Moon`, and `Mars`), and for convenience, these are all added to the main namespace. The fundamental constants `G` and `mu0` from the astropy constants package were added (as taken from CODATA 2014).

**Other changes**

* Fixed a bug in how the random coeffcients were determined for unnormalized coeffcients in SHCoeffs.
* Optional parameter `seed` added to `SHCoeffs.from_random()` to allow for reproducibility.
* One can now specify colat instead of lat for the method SHCoeffs.expand().
* Added `__repr__` methods to all pyshtools classes.
* Changed the mathematical operators of `SHCoeffs` such that addition and subtraction of a constant only affects the degree 0 term.
* Added the optional parameter `lmax` to `SHCoeffs.plot_spectrum()` and `SHCoeffs.plot_spectrum2d()`.
* Fixed a bug in `SHCoeffs.pad()` where the attribute `mask` was not similarly padded.
* For mathematical operations with `SHCoeffs` grids, it is now required that the
two class instances have the same `lmax`.
* Clarified the documentation of `SHRotateCoef` to point out that this is only valid for intrinsically real functions that are expressed in complex harmonics.
* Added the method `volume()` to the class SHCoeffs, that calculates the volume of the object.
* Added the attributes `area` and `shannon` to `SHWindow`, which provides the area of the concentration domain and the shannon number.
* Removed python installation support from Makefile: use pip instead.

**Citation:**

M. A. Wieczorek, M. Meschede, E. Sales de Andrade, I. Oshchepkov, B. Xu, and A. Walker (2018). SHTOOLS: Version 4.3, Zenodo, doi:[10.5281/zenodo.1346663](https://doi.org/10.5281/zenodo.1346663)


## Version 4.2

**Change log:**

* Full support added for the use of unnormalized harmonics in the classes `SHCoeffs` and `SHGrid`. To make use of this normalization, just specify `normalization='unnorm'`.
* Added a new python native routine `mag_spectrum()` in the subpackage `gravmag` that replaces the original fortran wrapped routines. The old python wrapped functions have been removed from pyshtools. This new routine is nearly the same as `spectrum()`, and further allows one to compute the spectrum of the potential or magnetic intensity.
* The old fortran based `SHRead` function has been replaced with a python native version `shread()`. The functionality is nearly identical as before, and combines the previous routines `SHRead`, `SHReadError`, `SHReadErrorH` and `SHReadH` into one. Differences include: (1) It is no longer necessary to specify the lmax of the file: This is determined automatically by reading the file from the end, (2) both real and complex coefficients are supported, (3) a header line can be output, but it is a simple list of type str that will need to be converted to the correct format by the user, and (4) "comment" lines are read and ignored: A valid line is one where there are 4 or more words, and where the first two words are integers.
* A new python native function `convert()` was added in the subpackage `shio` that converts between arrays of spherical harmonic coefficients with different normalizations. The class `SHCoeffs` was then simplified by using this external function for all conversions involving `SHCoeffs` class instances.
* The optional parameter lmax was added to `SHCoeffs.spectrum()`.
* When plotting grid from the class `SHGrid`, one can now specify the label to use for the x and y axes with `xlabel` and `ylabel`, as well as the interval to use when plotting ticks on both axes using `tick_interval`.
* The pyshtools rotation routines now allow you to specify the optional parameter `convention` to treat Euler angles in either the `x` or `y` conventions (i.e., which axes to use for the second rotation). Furthermore, the optional argument `body` allows you to specify if you want to rotate the body (True), or coordinate system (False, default). The tutorial number 3 was updated to clear up some inconsistencies in how the angles were defined.
* New optional parameters added to `SHWindow.plot_windows()` and `SHWindow.plot_spectra()` that include `xlim` and `ylim` for the limits when plotting spectra, `maxcolumns` for the number of columns to use when plotting several windows, and `lmax` which controls the grid spacing when plotting the windows.
* Added the optional argument `lmax` to `SHCoeffs.from_random()` that allows you to create coefficients with maximum bandwidths that are either greater or less than the bandwidth of the input power spectrum.
* Added a warning message when using `SHCoeffs.rotate()` with degrees greater than 1200, as the routine is not accurate beyond this value.
* Added an optional argument `legend` to `SHWindow.plot_windows()` to control whether the legend is plotted or not.
* Fixed a minor bug in ClassExample.py file concerning the use of `SHCoeffs.rotate()`.
* Added support for plotting to an already existing figure by allowing the user to specify an existing matplotlib axes.
* Removed some non-standard ascii dashes in the documentation files, and forced all doc files to be opened as `utf-8`.
* HTML documentation was completely redone using Jekyll. The markdown source files are now located in `pages/mydoc`. A static html web site is built using `jekyll`, whose files are located in `doc`. Github will automatically create the static pages and serve them on [shtools.github.io/SHTOOLS](https://shtools.github.io/SHTOOLS/). To build the static pages yourself, it is only necessary to execute `bundle exec jekyll build` in the directory `doc`, which will build the site into `_site` in the same directory. Alternatively, `make www` in the main directory will create a static site in the top-level directory `www` that could be used to deploy on a different web server. The site is based on the template [Jekyll documentation theme](https://github.com/tomjoht/documentation-theme-jekyll) by @tomjoht.

**Citation:**

M. A. Wieczorek, M. Meschede, E. Sales de Andrade, I. Oshchepkov, B. Xu, and A. Walker (2018). SHTOOLS: Version 4.2, Zenodo, doi:[10.5281/zenodo.1250054](https://doi.org/10.5281/zenodo.1250054)


## Version 4.1

This version adds improved functionality to SHTOOLS and fixes a couple of minor bugs. In addition, this release will be the first where pre-built wheels for unix/macOS/windows will be distributed via PYPI.

**Change log:**

* Added an optional argument `lmax` to `SHCoeffs.from_array()`.
* Coefficients are zero-padded when `lmax` is greater than the maximum degree in `SHCoeffs.to_array()`.
* The method `pad()` was added to the `SHCoeffs` class that zero pads or truncates the coefficients to a different `lmax`.
* Fixed the method `SHCoeffs.from_file()` such that the maximum spherical harmonic degree of the class is the maximum spherical harmonic degree of the coeffs (and not `lmaxin` as before).
* Fixed formatting issues with error messages in `SHCoeffs`.
* Removed print statements from the fortran code in `BAtoHilm` and `BAtoHilmRohH` that served no purpose.
* Fixed a bug in the argument order of the python wrappers of `CilmPlusRhoDH` and `BAtoHilmRhoDH`.
* Fixed the makefile to remove the `dist` directory during clean.
* Fixed a bug in the python routine `cross_spectrum()`, where the numpy arange function was incorrectly called.
* Fixed the`SHWindow` plotting methods to work when the number of rows is equal to 1.
* Conditional tests in the routine `Wigner3j` were reordered to avoid a division by zero.
* Numpy's auto-configuration is now used to detect the LAPACK libraries.
* Many minor updates to the python documentation and unix man pages.

**Citation:**

M. A. Wieczorek, M. Meschede, E. Sales de Andrade, I. Oshchepkov, B. Xu, and A. Walker (2017). SHTOOLS: Version 4.1, Zenodo, doi:[10.5281/zenodo.1067108](https://doi.org/10.5281/zenodo.1067108)


## Version 4.0
This is a major update that fixes bugs, adds new functionality, and improves Python error handing. All users are requested to upgrade to 4.0.

**Change log:**

* Instead of executing a Fortran STOP, which kills the Python kernel, the Fortran subroutines now return an `exitstatus` that allows Python to raise an exception. This technique does not work with the few Fortran functions that pyshtools calls, but these functions are relatively benign, and will soon be phased out for Python native functions.
* The Fortran `powerspectrum` routines have been removed from pyshtools, and have been replaced with Python native routines `spectrum` and `cross_spectrum`. The Python routines allow to specify the normalization, whether the output should be power, energy or l2norm, and whether the spectrum is per degree, per coefficient, or per log bandwidth.
* The method `plot_spectrum2d()` was added to the class `SHCoeffs` to plot the power as a function of degree and order.
* All pyshtools modules have been converted into proper Python subpackages. The subpackage `localizedpsectralanalysis` has been merged into `spectralanalysis`, and the subpackage `other` has been renamed `utils`.
* The Python class method `SHCoeffs.expand()` now can evaluate the function either on an SHGrid or for a list of latitude and longitude points. As part of this change, a new fortran function `MakeGridPointC` was created for complex coefficients.
* The majority of the methods for the classes `SHCoeffs`, `SHGrid` and `SHWindow` have been rename for consistency (see documentation!). Also, the classes now give the option of reading or saving to files as numpy arrays.
* Added new Python function `read_icgen_gfc` for reading ICGEM-format gravity coefficient files.
* The operator `pow` was added to the class `SHCoeffs`.
* All methods in the pyshtools classes now return copies by default, which can be modified by the optional argument `copy`.
* Added `pot` as a mandatory return argument for the Python routine `MakeGravGridDH`.
* Several minor modifications and bug fixes were made to the makefiles to improve compatibility and to allow the use of `make -j`.
* The routines `other.EigValSym`, `other.EigValVecSym`, `other.EigValVecSymTri`, `other.RandomGaussian`, `other.RandomN` and `other.PreGLQ` were removed from pyshtools, as these can be found in other scipy packages.
* The SHTOOLS routine `DHaj` was added to the pyshtools subpackage `utils`.
* Python docstrings have been streamlined and standardized.
* ...plus, many minor changes and optimizations...

**Citation:**

M. A. Wieczorek, M. Meschede, I. Oshchepkov, E. Sales de Andrade, and heroxbd  (2016). SHTOOLS: Version 4.0. Zenodo. doi:[10.5281/zenodo.206114](https://doi.org/10.5281/zenodo.206114)
