# legendre_lm

Compute the associated Legendre function for a specific degree and order.

# Usage

`plm` = legendre_lm (`l`, `m`, `z`, [`normalization`, `csphase`, `cnorm`])

# Returns

`plm` : float
:   The associated Legendre functions for degree `l` and order `m`.

# Parameters

`l` : integer
:   The spherical harmonic degree.

`m` : integer
:   The spherical harmonic order.

`z` : float
:   The argument of the associated Legendre functions.

`normalization` : str, optional, default = '4pi'
:   '4pi', 'ortho', 'schmidt', or 'unnorm' for use with geodesy 4pi normalized, orthonormalized, Schmidt semi-normalized, or unnormalized spherical harmonic functions, respectively.

`csphase` : optional, integer, default = 1
:   If 1 (default), the Condon-Shortley phase will be excluded. If -1, the Condon-Shortley phase of (-1)^m will be appended to the associated Legendre functions.

`cnorm` : optional, integer, default = 0
:   If 1, the complex normalization of the associated Legendre functions will be used. The default is to use the real normalization.

# Description

`legendre_lm` will calculate the associated Legendre function for a specific degree `l` and order `m`. The Legendre functions are used typically as a part of the spherical harmonic functions, and three parameters determine how they are defined. `normalization` can be either '4pi' (default), 'ortho', 'schmidt', or 'unnorm' for use with 4pi normalized, orthonormalized, Schmidt semi-normalized, or unnormalized spherical harmonic functions, respectively. `csphase` determines whether to include or exclude (default) the Condon-Shortley phase factor. `cnorm` determines whether to normalize the Legendre functions for use with real (default) or complex spherical harmonic functions.

The Legendre functions are calculated using the standard three-term recursion formula, and in order to prevent overflows, the scaling approach of Holmes and Featherstone (2002) is utilized. The resulting functions are accurate to about degree 2800. See Wieczorek and Meschede (2018) for exact definitions on how the Legendre functions are defined.

# References

Holmes, S. A., and W. E. Featherstone, A unified approach to the Clenshaw summation and the recursive computation of very high degree and order normalised associated Legendre functions, J. Geodesy, 76, 279-299, doi:10.1007/s00190-002-0216-2, 2002.

Wieczorek, M. A., and M. Meschede. SHTools — Tools for working with spherical harmonics, Geochem., Geophys., Geosyst., 19, 2574-2592, doi:10.1029/2018GC007529, 2018.

# See also

[pylegendre](pylegendre.html), [pyplmbar](pyplmbar.html), [pyplmon](pyplmon.html), [pyplmschmidt](pyplmschmidt.html), [pyplegendrea](pyplegendrea.html), [pyplmindex](pyplmindex.html)
