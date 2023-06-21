# Kgen <img src="https://github.com/PalaeoCarb/Kgen/blob/docs/assets/images/logo.png" align="right" alt="" width="120" />
Coefficients for consistently calculating and pressure correcting Ks for carbon calculation. 

### [Find out about Kgen](https://palaeocarb.github.io/Kgen/).

This fork of Kgen provides equilibrium constants in the correct format required for [PyCO2SYS](https://PyCO2SYS.readthedocs.io/) via the function `Kgen.calc_Ks_PyCO2SYS`:

```python
from kgen import calk_Ks_PyCO2SYS
import PyCO2SYS as pyco2

# First, use Kgen to calculate equilibrium constants etc.
kgen_constants = calc_Ks_PyCO2SYS(TempC=20, Salinity=35, Pressure=0, Mg=0.3, Ca=None)

# Then, put these into PyCO2SYS, along with whatever else you need, e.g.:
results = pyco2.sys(par1=2300, par2=2100, par1_type=1, par2_type=2, **kgen_constants)
# See the PyCO2SYS docs for an explanation of par1, par2 etc.
```

The arguments to `calc_Ks_PyCO2SYS` are identical to those for `calc_Ks` described above.

In the above code, PyCO2SYS will use the equilibrium constants and total salt concentrations calculated by Kgen for all its calculations, instead of evaluating them internally.

Note that `kgen_constants` includes the values provided to `calc_Ks_PyCO2SYS` (or the Kgen defaults if none provided) for temperature, salinity, pressure, pH scale, and total sulfate, fluoride and calcium, so these cannot be provided separately to `pyco2.sys()`.

## Test Status

Language-specific packages:

[![Check K values - Matlab](https://github.com/PalaeoCarb/Kgen/workflows/Check%20K%20values%20-%20Matlab/badge.svg)](https://github.com/PalaeoCarb/Kgen/actions/workflows/matlab-tests.yml)
[![Check K values - Python](https://github.com/PalaeoCarb/Kgen/workflows/Check%20K%20values%20-%20Python/badge.svg)](https://github.com/PalaeoCarb/Kgen/actions/workflows/python-tests.yml)
[![Check K values - R](https://github.com/PalaeoCarb/Kgen/workflows/Check%20K%20values%20-%20R/badge.svg)](https://github.com/PalaeoCarb/Kgen/actions/workflows/r-tests.yml)

Language inter-comparison:

[![Crosscheck Methods](https://github.com/PalaeoCarb/Kgen/workflows/Crosscheck%20Methods/badge.svg)](https://github.com/PalaeoCarb/Kgen/actions/workflows/crosscheck.yml)

## Development Stuff

### What KGen Does

Kgen will provide K's in a consistent, stable output format from specifically defined inputs that have been checked against external reference values and across platforms. We guarantee to keep the input and output format of Kgen stable within major version number (i.e. within the 'X' of version X.y.z), so that updates will not break [your favourite carbon calculator].

### What Kgen Does Not Do

<s>Kgen is *not* intended to provide Ks in the correct format for [your favourite carbon calculator]. We recommend adding Kgen as an [optional] dependency, and implementing any required input/output parsing within [your favourite carbon calculator].</s>

This fork of Kgen *does* provide Ks in the correct format for [PyCO2SYS](https://PyCO2SYS.readthedocs.io/) via the function `Kgen.calc_Ks_PyCO2SYS`.

### Talk to Us!

If you have any ideas for improving Kgen, please [Open a New Issue](https://github.com/PalaeoCarb/Kgen/issues/new/choose) on GitHub to discuss how it might best be implemented.
