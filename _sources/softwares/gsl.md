# GSL

```{admonition} Versions Installed
:class: note

`Kay: gcc/2.5`

`LXP: `
```

## Description

GSL (the GNU Scientific Library) is a numerical library for C and C++ programmers. The library provides a wide range of mathematical routines such as random number generators, special functions and least-squares fitting. There are over 1000 functions in total with an extensive test
suite.

## License

GSL is available under the [GNU General Public License](http://www.gnu.org/copyleft/gpl.html "GPL homepage").

## Benchmarks

N/A

## Additional Notes

GSL is developed and maintained for the GCC compiler. As such it can be awkward to compile successfully with third party compilers. Consequently we are not able to provide a version built with Intel compilers on Kay.

To use the GSL on Kay load the relevant environment module:

```bash
module load gsl/gcc/2.5
```

