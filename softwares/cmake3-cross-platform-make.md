# CMAKE3: Cross-platform make


```{admonition} Versions Installed

`Kay: 3.12.3, 3.15.1, 3.15.4, 3.20.1`

`LXP: `

```

## Description

CMake is a family of tools designed to build, test and package
software. CMake is used to control the software compilation process
using simple platform and compiler independent configuration
files. CMake generates native makefiles and workspaces that can be
used in the compiler environment of your choice.

## License

CMake is freely available under the [CMAKE (BSD) License](http://www.cmake.org/cmake/project/license.html "CMAKE (BSD) License").

## Benchmarks

N/A.

## Additional Notes

To use CMake 3.12.3 load the relevant environment module:

```bash
module load cmake/3.12.3
```

By default CMake will use the GNU compiler suite. If you want to use
the Intel compilers, and this is recommended for best performance,
they can by set by issuing the following commands:

```bash
export CC=icc export CXX=icpc export FC=ifort
```

Further information can be found [here](http://www.cmake.org).

