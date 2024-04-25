---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
kernelspec:
  display_name: Python 3
  language: python
  name: python3
mystnb:
  render_markdown_format: myst
---

# Software Support

ICHEC provides access and support to a large range of compilers, libraries and high-performance computing packages on it's supercomputer systems (Kay). If you are interested in using software which is not on the list, it is best to email us at support@ichec.ie or log a query using the Helpdesk Portal. ICHEC can also assist you with installing packages for your own use.

We do our best to offer latest versions of all required software. If you require a newer version please ask us for it.

On the interim service system, [Meluxina](https://docs.lxp.lu/) we are also making sure all the softwares of user's interest are installed.

## Software support from ICHEC

The following list is not exhaustive and does not include many packages one might take for granted, e.g. perl. Certain packages are installed on a request basis and so may not yet have been requested on a given system. Some are general purpose compilers or libraries, other are softwares specific to a domain, such as material science, physics, chemistry, computational biology, statistics etc. For more details about the software, please click on the link therein.

We provide support for all of these softwares. We will keep adding further documentations, illustrations and examples on these, and other softwares that ICHEC users intend to use.


| Package Name: Description                                                      | Version(s) | Domain |
|--------------------------------------------------------------------------------|------------|--------|
| [Abaqus](./softwares/abaqus.md): Finite Element Analysis                       |            | Engineering |
| [Abinit](./softwares/abinit.md): DFT based simulation                          |            | Physics     |
| [Amber](./softwares/amber.md)                                                  |            |        |
| [ANSYS](./softwares/ansys.md)                                                  |            |        |
| [Cmake3](./softwares/cmake3.md)        |            |        |
| [Cp2k-0](./softwares/cp2k-0.md)                                                |            |        |
| [Cuda-Toolkit](./softwares/cuda-toolkit.md)                                    |            |        |
| [Dlpoly](./softwares/dlpoly.md)                                                |            |        |
| [Gamess-Us](./softwares/gamess-us.md)                                          |            |        |
| [Gaussian](./softwares/gaussian.md)                                            |            |        |
| [Gcc](./softwares/gcc.md)                                                      |            |        |
| [GNU Parallel](./softwares/parallel.md)                                        |            |        |
| [Gromacs](./softwares/gromacs.md)                                              |            |        |
| [Gsl](./softwares/gsl.md)                                                      |            |        |
| [Intel-Compiler](./softwares/intel-compiler.md)                                |            |        |
| [JupyterLab](./softwares/jupyter-lab.md)                                |            |        |
| [Namd](./softwares/namd.md)                                                    |            |        |
| [Openfoam](./softwares/openfoam.md)                                            |            |        |
| [Orca](./softwares/orca.md)                                                    |            |        |
| [Paraview](./softwares/paraview.md)                                            |            |        |
| [Python/Conda](./softwares/python-conda.md)                                    |            |        |
| [Quantum-Espresso](./softwares/quantum-espresso.md)                            |            |        |
| [R](./softwares/r.md)                                                          |            |        |
| [Siesta](./softwares/siesta.md)                                                |            |        |
| [Singularity](./softwares/singularity.md)                                      |            |        |
| [Vasp](./softwares/vasp.md)                                                    |            |        |
| [Voro++: A three dimensional Voronoi cell library in C++](./softwares/voro.md) |            |        |

```{code-cell} python3
:tags: ['remove-input', 'remove-output']
import json
from IPython.display import display, Markdown
with open("./list_packages.json") as f:
    ll = json.load(f)
keys = list(ll[0].keys())
keys.remove("path")
ss = ''
ss += "|" +  "|".join([_.upper() for _ in keys]) + "|\n"
ss += "|" + "|".join(['---' for _ in keys]) + "|\n"
for item in ll:
    item["name"] = f"[{item['name']}]({item['path']})"
    ss += "|" + "|".join([item[k] for k in keys]) + "|\n"
display(Markdown(ss))
#
```


## Software Catalogue on Meluxina

Following is a snapshot of the `module avail` command on Meluxina. It showcases the list of softwares readily available on the compute nodes.

- Note the software under the heading `/project/home/p200272/modules`. This is the list of softwares maintained by ICHEC staff, so the issues related to these can be directly handled by ICHEC. For the rest, we need to coordinate with Meluxina support staff.

- The next heading `/apps/USE/system/modules` contains a list of high level modules which themselves contain several modules, that one can load.

- The third heading `/apps/USE/easybuild/release/2023.1/modules/all` shows the list of modules available through the high level module `env/release/2023.1`

```{margin}
:class: tip
On Meluxina, the list of software packages are grouped into releases, as seen the the second heading. Different releases have more or less the same set of softwares, however their version progressively change release to release.

So if you can see the software you want in the list below, or by running `module avail` on the compute node, you can change the release by `module purge && module load env/release/xxxx.x` and see which release seems to have the version you want.
```

```bash
mel0134 02:42:18 0 ~  module avail

------------------------------------------------------------------------------- /project/home/p200272/modules -------------------------------------------------------------------------------
   ORCA/4.2.1    RASPA/2.0.41-foss-2023a    amber/22-foss-2023a-CUDA-12.2    ccp4/7.0          micromamba/1.5.7    vasp5/5.4.4                                    vasp6/6.4.2 (D)
   ORCA/5.0.2    abaqus/2023                ansys/2023R2                     gaussian/16c02    taskfarm/3.0        vasp6/6.4.2_nvhpc_23.7_cuda_12.2_ompi_4.1.5

--------------------------------------------------------------------------------- /apps/USE/system/modules ----------------------------------------------------------------------------------
   deploy/EasyBuild/4.7.0           deploy/deploy-apps-2023.1    env/release/2021.3        env/release/2023.1 (S,L,D)    env/staging/2023.1      (D)
   deploy/EasyBuild/4.8.0    (D)    deploy/deploy-apps           env/release/2021.5        env/staging/2021.5            lxp-tools/myquota/0.3.1 (S)
   deploy/deploy-apps-2022.1        deploy/deploy-user           env/release/2022.1 (S)    env/staging/2022.1            lxp-tools/myquota/0.3.2 (S,L,D)

---------------------------------------------------------------------- /apps/USE/easybuild/release/2023.1/modules/all -----------------------------------------------------------------------
   520nmx/20.4                                              OpenFOAM/v2312-foss-2023a                                      gocryptfs/2.4.0-GCCcore-12.3.0
   ACTC/1.1-GCCcore-12.3.0                                  OpenFOAM/10-foss-2023a                                  (D)    gompi/2023a
   AMD-uProf/4.1.424                                        OpenJPEG/2.5.0-GCCcore-12.3.0                                  googletest/1.13.0-GCCcore-12.3.0
   AOCC/4.0.0-GCCcore-12.3.0                                OpenMPI/4.1.5-GCC-12.3.0                                       gperf/3.1-GCCcore-12.3.0
   ATK/2.38.0-GCCcore-12.3.0                                OpenMPI/4.1.5-NVHPC-23.7-CUDA-12.2.0                    (D)    gperftools/2.12-GCCcore-12.3.0
   Abseil/20230125.3-GCCcore-12.3.0                         OpenPGM/5.2.122-GCCcore-12.3.0                                 graphite2/1.3.14-GCCcore-12.3.0
   Advisor/2023.2.0                                         OpenSSL/1.1                                                    graphviz-python/0.20.1-GCCcore-12.3.0
   Apptainer/1.2.4-GCCcore-12.3.0                           PAPI/7.0.1-GCCcore-12.3.0                                      groff/1.22.4-GCCcore-12.3.0
   Armadillo/12.6.2-foss-2023a                              PCRE/8.45-GCCcore-12.3.0                                       gzip/1.12-GCCcore-12.3.0
   Arrow/14.0.1-gfbf-2023a                                  PCRE2/10.42-GCCcore-12.3.0                                     h5py/3.2.1-foss-2023a
   Autoconf/2.71-GCCcore-12.3.0                             PDT/3.25.1-GCCcore-12.3.0                                      h5py/3.9.0-foss-2023a                                 (D)
   Autoconf/2.71                                    (D)     PETSc/3.19.4-foss-2023a                                        hatchling/1.18.0-GCCcore-12.3.0-python-3.10.8
   Automake/1.16.5-GCCcore-12.3.0                           PETSc/3.20.3-foss-2023a                                 (D)    hatchling/1.18.0-GCCcore-12.3.0                       (D)
   Automake/1.16.5                                  (D)     PLUMED/2.9.0-foss-2023a                                        help2man/1.47.16-GCCcore-10.2.0
   Autotools/20220317-GCCcore-12.3.0                        PMIx/4.2.6-GCCcore-12.3.0                                      help2man/1.49.3-GCCcore-12.3.0                        (D)
   Autotools/20220317                               (D)     POV-Ray/3.7.0.10-GCC-12.3.0                                    hwloc/2.9.1-GCCcore-12.3.0
   BLIS/0.9.0-GCC-12.3.0                                    PROJ/9.2.0-GCCcore-12.3.0                                      hypothesis/6.82.0-GCCcore-12.3.0-python-3.10.8
   Bazel/6.3.1-GCCcore-12.3.0                               Pango/1.50.14-GCCcore-12.3.0                                   hypothesis/6.82.0-GCCcore-12.3.0                      (D)
   BeautifulSoup/4.12.2-GCCcore-12.3.0                      ParMETIS/4.0.3-gompi-2023a                                     ifpgasdk/20.4
   Bison/3.7.1-GCCcore-10.2.0                               ParaView/5.11.2-foss-2023a                                     iimpi/2023a
   Bison/3.8.2-GCCcore-12.3.0                               Paraver/4.11.1-foss-2023a                                      imageio/2.33.1-gfbf-2023a
   Bison/3.8.2                                      (D)     Perl-bundle-CPAN/5.36.1-GCCcore-12.3.0                         imkl-FFTW/2023.1.0-iimpi-2023a
   Blender/4.0.2-linux-x86_64-CUDA-12.2.0                   Perl/5.36.1-GCCcore-12.3.0                                     imkl/2023.1.0
   Boost/1.82.0-GCC-12.3.0                                  Pillow-SIMD/9.5.0-GCCcore-12.3.0                               impi/2021.9.0-intel-compilers-2023.1.0
   Brotli/1.0.9-GCCcore-12.3.0                              Pillow/10.0.0-GCCcore-12.3.0-python-3.10.8                     intel-compilers/2023.1.0
   Brunsli/0.1-GCCcore-12.3.0                               Pillow/10.0.0-GCCcore-12.3.0                            (D)    intel/2023a
   CFITSIO/4.3.0-GCCcore-12.3.0                             PyCairo/1.25.0-GCCcore-12.3.0                                  intltool/0.51.0-GCCcore-12.3.0
   CGAL/5.6-GCCcore-12.3.0                                  PyGObject/3.46.0-GCCcore-12.3.0                                itac/2021.10.0
   CMake/3.18.4-GCCcore-10.2.0                              PyYAML/6.0-GCCcore-12.3.0                                      jbigkit/2.1-GCCcore-12.3.0
   CMake/3.26.3-GCCcore-12.3.0                      (D)     PyZMQ/25.1.1-GCCcore-12.3.0                                    jemalloc/5.3.0-GCCcore-12.3.0
   CP2K/2023.1-foss-2023a-CUDA-12.2.0                       PycURL/7.45.2-GCCcore-12.3.0                                   json-c/0.16-GCCcore-12.3.0
   CP2K/2023.1-foss-2023a                           (D)     Python-bundle-PyPI/2023.06-GCCcore-12.3.0-python-3.10.8        jupyter-server/2.7.2-GCCcore-12.3.0
   CUDA/12.1.1                                              Python-bundle-PyPI/2023.06-GCCcore-12.3.0               (D)    kim-api/2.3.0-GCC-12.3.0
   CUDA/12.2.0                                      (D)     Python/3.10.8-GCCcore-12.3.0                                   libGLU/9.0.3-GCCcore-12.3.0
   Catch2/2.13.9                                            Python/3.11.3-GCCcore-12.3.0                            (D)    libarchive/3.4.3-GCCcore-10.2.0
   Check/0.15.2-GCCcore-12.3.0                              Qhull/2020.2-GCCcore-12.3.0                                    libarchive/3.6.2-GCCcore-12.3.0                       (D)
   Clang/16.0.6-GCCcore-12.3.0-CUDA-12.2.0                  Qiskit/0.45.1-foss-2023a                                       libcap/1.2.53-GCCcore-12.3.0
   Clang/16.0.6-GCCcore-12.3.0                      (D)     Qt5/5.15.10-GCCcore-12.3.0                                     libcerf/2.3-GCCcore-12.3.0
   CppUnit/1.15.1-GCCcore-12.3.0                            QuantumESPRESSO/7.2-foss-2023a                                 libcircle/0.3-gompi-2023a
   CubeGUI/4.8.2-GCCcore-12.3.0                             R/4.3.2-foss-2023a-bare                                        libdeflate/1.18-GCCcore-12.3.0
   CubeLib/4.8.1-GCCcore-12.3.0                             R/4.3.2-gfbf-2023a                                      (D)    libdrm/2.4.115-GCCcore-12.3.0
   CubeWriter/4.8.1-GCCcore-12.3.0                          RE2/2023-08-01-GCCcore-12.3.0                                  libepoxy/1.5.10-GCCcore-12.3.0
   DBus/1.15.4-GCCcore-12.3.0                               RapidJSON/1.1.0-20230928-GCCcore-12.3.0                        libevent/2.1.12-GCCcore-12.3.0
   Doxygen/1.9.7-GCCcore-12.3.0                             ReFrame/4.4.0                                                  libfabric/1.18.0-GCCcore-12.3.0
   ELPA/2023.05.001-foss-2023a                              Rust/1.70.0-GCCcore-12.3.0                                     libffi/3.4.4-GCCcore-12.3.0
   ELPA/2023.05.001-intel-2023a                     (D)     Rust/1.75.0-GCCcore-12.3.0                              (D)    libgd/2.3.3-GCCcore-12.3.0
   Eigen/3.4.0-GCCcore-12.3.0                               SCOTCH/7.0.3-gompi-2023a                                       libgeotiff/1.7.1-GCCcore-12.3.0
   Extrae/4.0.6-gompi-2023a                                 SDL2/2.28.2-GCCcore-12.3.0                                     libgit2/1.7.1-GCCcore-12.3.0
   FFTW.MPI/3.3.10-gompi-2023a                              SIONlib/1.7.7-GCCcore-12.3.0-tools                             libglvnd/1.6.0-GCCcore-12.3.0
   FFTW/3.3.10-GCC-12.3.0                                   SQLite/3.42.0-GCCcore-12.3.0                                   libiconv/1.17-GCCcore-12.3.0
   FFmpeg/6.0-GCCcore-12.3.0                                SWIG/4.1.1-GCCcore-12.3.0                                      libjpeg-turbo/2.1.5.1-GCCcore-12.3.0
   FLAC/1.4.2-GCCcore-12.3.0                                ScaFaCoS/1.0.4-foss-2023a                                      libogg/1.3.5-GCCcore-12.3.0
   FLINT/3.0.1-gfbf-2023a                                   ScaLAPACK/2.2.0-gompi-2023a-fb                                 libopus/1.4-GCCcore-12.3.0
   FLTK/1.3.8-GCCcore-12.3.0                                Scalasca/2.6.1-gompi-2023a-CUDA-12.2.0                         libpciaccess/0.17-GCCcore-12.3.0
   FUSE/2.9.7-GCCcore-12.3.0                                Scalasca/2.6.1-gompi-2023a                              (D)    libpng/1.6.39-GCCcore-12.3.0
   FUSE/3.16.2-GCCcore-12.3.0                       (D)     SciPy-bundle/2023.07-gfbf-2023a-python-3.10.8                  libreadline/8.2-GCCcore-12.3.0
   FlexiBLAS/3.3.1-GCC-12.3.0                               SciPy-bundle/2023.07-gfbf-2023a                         (D)    libsndfile/1.2.2-GCCcore-12.3.0
   FriBidi/1.0.12-GCCcore-12.3.0                            Score-P/8.1-gompi-2023a-CUDA-12.2.0                            libsodium/1.0.18-GCCcore-12.3.0
   GCC/12.3.0                                               Score-P/8.1-gompi-2023a                                 (D)    libtirpc/1.3.3-GCCcore-12.3.0
   GCCcore/10.2.0                                           Shapely/2.0.1-gfbf-2023a-python-3.10.8                         libtool/2.4.7-GCCcore-12.3.0
   GCCcore/12.3.0                                   (D)     Spark/3.5.0-foss-2023a                                         libtool/2.4.7                                         (D)
   GDAL/3.7.1-foss-2023a                                    SuiteSparse/5.13.0-foss-2023a-METIS-5.1.0                      libunwind/1.6.2-GCCcore-12.3.0
   GDB/13.2-GCCcore-12.3.0                                  SuiteSparse/7.1.0-foss-2023a                            (D)    libvorbis/1.3.7-GCCcore-12.3.0
   GDRCopy/2.3.1-GCCcore-12.3.0                             SuperLU_DIST/8.1.2-foss-2023a                                  libvori/220621-GCCcore-12.3.0
   GEOS/3.12.0-GCC-12.3.0                                   SymEngine-python/0.11.0-GCC-12.3.0                             libwebp/1.3.1-GCCcore-12.3.0
   GLPK/5.0-GCCcore-12.3.0                                  SymEngine/0.11.2-GCC-12.3.0                                    libxc/6.2.2-GCC-12.3.0
   GLib/2.77.1-GCCcore-12.3.0                               Szip/2.1.1-GCCcore-12.3.0                                      libxml2/2.11.4-GCCcore-12.3.0
   GMP/6.2.1-GCCcore-12.3.0                                 Tcl/8.6.13-GCCcore-12.3.0                                      libxslt/1.1.38-GCCcore-12.3.0
   GObject-Introspection/1.76.1-GCCcore-12.3.0              TensorFlow/2.13.0-foss-2023a                                   libxsmm/1.17-GCC-12.3.0
   GROMACS/2023.3-foss-2023a-CUDA-12.2.0                    Tk/8.6.13-GCCcore-12.3.0                                       libyaml/0.2.5-GCCcore-12.3.0
   GROMACS/2023.3-foss-2023a                        (D)     Tkinter/3.11.3-GCCcore-12.3.0                                  lwgrp/1.0.5-gompi-2023a
   GSL/2.7-GCC-12.3.0                                       UCC-CUDA/1.2.0-GCCcore-12.3.0-CUDA-12.2.0                      lxml/4.9.2-GCCcore-12.3.0
   GST-plugins-bad/1.22.5-GCC-12.3.0                        UCC/1.2.0-GCCcore-12.3.0                                       lz4/1.9.4-GCCcore-12.3.0
   GST-plugins-base/1.22.5-GCC-12.3.0                       UCX-CUDA/1.14.1-GCCcore-12.3.0-CUDA-12.1.1                     magma/2.7.2-foss-2023a-CUDA-12.1.1
   GStreamer/1.22.5-GCC-12.3.0                              UCX-CUDA/1.14.1-GCCcore-12.3.0-CUDA-12.2.0              (D)    make/4.4.1-GCCcore-12.3.0
   GTK2/2.24.33-GCCcore-12.3.0                              UCX/1.14.1-GCCcore-12.3.0                                      makeinfo/7.0.3-GCCcore-12.3.0
   GTK3/3.24.37-GCCcore-12.3.0                              UDUNITS/2.2.28-GCCcore-12.3.0                                  matplotlib/3.7.2-gfbf-2023a
   GTK4/4.13.1-GCC-12.3.0                                   UnZip/6.0-GCCcore-12.3.0                                       maturin/1.1.0-GCCcore-12.3.0
   GTS/0.7.6-GCCcore-12.3.0                                 VMD/1.9.4a57-foss-2023a-CUDA-12.2.0                            maturin/1.4.0-GCCcore-12.3.0-Rust-1.75.0              (D)
   Gdk-Pixbuf/2.42.10-GCCcore-12.3.0                        VMD/1.9.4a57-foss-2023a                                 (D)    meson-python/0.13.2-GCCcore-12.3.0-python-3.10.8
   Ghostscript/10.01.2-GCCcore-12.3.0                       VTK/9.3.0-foss-2023a                                           meson-python/0.13.2-GCCcore-12.3.0                    (D)
   GlobalArrays/5.8.2-intel-2023a                           VTune/2023.2.0                                                 mpi4py/3.1.4-gompi-2023a
   Go/1.20.4                                                Valgrind/3.21.0-gompi-2023a                                    mpifileutils/0.11.1-foss-2023a
   Go/1.21.2                                        (D)     Voro++/0.4.6-GCCcore-12.3.0                                    muparserx/4.0.12-GCCcore-12.3.0
   Graphene/1.10.8-GCCcore-12.3.0                           WRF/4.5.1-foss-2023a-dmpar                                     ncurses/5.9
   Graphviz/8.1.0-GCCcore-12.3.0                            Wayland/1.22.0-GCCcore-12.3.0                                  ncurses/6.2-GCCcore-10.2.0
   HDF/4.2.16-2-GCCcore-12.3.0                              X11/20230603-GCCcore-12.3.0                                    ncurses/6.2
   HDF5/1.10.7-gompi-2023a                                  XZ/5.2.5-GCCcore-10.2.0                                        ncurses/6.3
   HDF5/1.14.0-gompi-2023a                                  XZ/5.4.2-GCCcore-12.3.0                                 (D)    ncurses/6.4-GCCcore-12.3.0                            (D)
   HDF5/1.14.0-iimpi-2023a                          (D)     Xerces-C++/3.2.4-GCCcore-12.3.0                                netCDF-C++4/4.3.1-gompi-2023a
   HH-suite/3.3.0-gompi-2023a                               Xvfb/21.1.8-GCCcore-12.3.0                                     netCDF-Fortran/4.6.1-gompi-2023a
   HPCX/2.16-GCCcore-12.3.0                                 Yasm/1.3.0-GCCcore-12.3.0                                      netCDF-Fortran/4.6.1-iimpi-2023a                      (D)
   HarfBuzz/5.3.1-GCCcore-12.3.0                            Z3/4.12.2-GCCcore-12.3.0-Python-3.11.3                         netCDF/4.9.2-gompi-2023a
   Highway/1.0.4-GCCcore-12.3.0                             Z3/4.12.2-GCCcore-12.3.0                                (D)    netCDF/4.9.2-iimpi-2023a                              (D)
   Hypre/2.28.0-foss-2023a                                  ZeroMQ/4.3.4-GCCcore-12.3.0                                    nettle/3.9.1-GCCcore-12.3.0
   Hypre/2.29.0-foss-2023a                          (D)     Zip/3.0-GCCcore-12.3.0                                         networkx/3.1-gfbf-2023a
   ICU/73.2-GCCcore-12.3.0                                  ant/1.10.14-Java-11                                            nlohmann_json/3.11.2-GCCcore-12.3.0
   IOR/3.3.0-gompi-2023a                                    archspec/0.2.1-GCCcore-12.3.0                                  nodejs/18.17.1-GCCcore-12.3.0
   IPython/8.14.0-GCCcore-12.3.0                            aria2/1.36.0-GCCcore-12.3.0                                    nsync/1.26.0-GCCcore-12.3.0
   ISL/0.26-GCCcore-12.3.0                                  arpack-ng/3.9.0-foss-2023a                                     numactl/2.0.16-GCCcore-12.3.0
   ImageMagick/7.1.1-15-GCCcore-12.3.0                      at-spi2-atk/2.38.0-GCCcore-12.3.0                              numba/0.57.1-foss-2023a-CUDA-12.2.0-python-3.10.8
   Imath/3.1.7-GCCcore-12.3.0                               at-spi2-core/2.49.91-GCCcore-12.3.0                            numba/0.58.1-foss-2023a                               (D)
   Inspector/2023.2.0                                       attr/2.5.1-GCCcore-12.3.0                                      nvompic/2023a
   JasPer/4.0.0-GCCcore-12.3.0                              aws-cli/2.7.1                                                  patchelf/0.18.0-GCCcore-12.3.0
   Java/11.0.18                                     (11)    binutils/2.35-GCCcore-10.2.0                                   pixman/0.42.2-GCCcore-12.3.0
   Java/17.0.6                                      (D)     binutils/2.35                                                  pkgconf/1.8.0
   JsonCpp/1.9.5-GCCcore-12.3.0                             binutils/2.40-GCCcore-12.3.0                                   pkgconf/1.9.5-GCCcore-12.3.0                          (D)
   Julia/1.9.3-linux-x86_64                                 binutils/2.40                                           (D)    pkgconfig/1.5.5-GCCcore-12.3.0-python
   JupyterHub/4.0.2-GCCcore-12.3.0                          bokeh/3.2.2-foss-2023a                                         poetry/1.5.1-GCCcore-12.3.0-python-3.10.8
   JupyterLab/4.0.5-GCCcore-12.3.0                          bzip2/1.0.8-GCCcore-10.2.0                                     poetry/1.5.1-GCCcore-12.3.0                           (D)
   KaHIP/3.14-gompi-2023a                                   bzip2/1.0.8-GCCcore-12.3.0                              (D)    popt/1.19
   KaHIP/3.16-gompi-2023a                           (D)     c-ares/1.19.1-GCCcore-12.3.0                                   protobuf-python/4.24.0-GCCcore-12.3.0
   Kokkos/4.1.0-GCC-12.3.0                                  cURL/7.72.0-GCCcore-10.2.0                                     protobuf/24.0-GCCcore-12.3.0
   LAME/3.100-GCCcore-12.3.0                                cURL/8.0.1-GCCcore-12.3.0                               (D)    pscom/5.7.0-1-GCCcore-12.3.0-CUDA-12.2.0
   LAMMPS/2Aug2023_update2-foss-2023a-kokkos                cairo/1.17.8-GCCcore-12.3.0                                    pscom/5.7.0-1-GCCcore-12.3.0                          (D)
   LERC/4.0.0-GCCcore-12.3.0                                cffi/1.15.1-GCCcore-12.3.0-python-3.10.8                       psmpi/5.9.2-1-GCC-12.3.0-CUDA-12.2.0
   LLVM/16.0.6-GCCcore-12.3.0-python-3.10.8                 cffi/1.15.1-GCCcore-12.3.0                              (D)    psmpi/5.9.2-1-GCC-12.3.0                              (D)
   LLVM/16.0.6-GCCcore-12.3.0                       (D)     cirq-core/1.2.0-foss-2023a                                     pybind11/2.11.1-GCCcore-12.3.0-python-3.10.8
   LibTIFF/4.5.0-GCCcore-12.3.0                             configurable-http-proxy/4.5.6-GCCcore-12.3.0                   pybind11/2.11.1-GCCcore-12.3.0                        (D)
   Libint/2.7.2-GCC-12.3.0-lmax-6-cp2k                      cppy/1.2.1-GCCcore-12.3.0                                      pytest-flakefinder/1.1.0-GCCcore-12.3.0
   Linaro-Forge/23.0.3-GCC-12.3.0                           cryptography/41.0.1-GCCcore-12.3.0-python-3.10.8               pytest-rerunfailures/12.0-GCCcore-12.3.0
   LittleCMS/2.15-GCCcore-12.3.0                            cryptography/41.0.1-GCCcore-12.3.0                      (D)    pytest-shard/0.1.2-GCCcore-12.3.0
   Lua/5.4.6-GCCcore-12.3.0                                 cuDF/23.10.0-foss-2023a-CUDA-12.2.0-python-3.10.8              qsimcirq/0.17.0-foss-2023a
   M4/1.4.18-GCCcore-10.2.0                                 cuDNN/8.9.2.26-CUDA-12.1.1                                     rapidsai/23.10.0-foss-2023a-CUDA-12.2.0-python-3.10.8
   M4/1.4.18                                                cuDNN/8.9.2.26-CUDA-12.2.0                              (D)    re2c/3.1-GCCcore-12.3.0
   M4/1.4.19-GCCcore-12.3.0                                 cuGraph/23.10.0-foss-2023a-CUDA-12.2.0-python-3.10.8           retworkx/0.13.2-foss-2023a
   M4/1.4.19                                        (D)     cuML/23.10.0-foss-2023a-CUDA-12.2.0-python-3.10.8              rustworkx/0.13.2-foss-2023a
   MCR/R2023a                                               cuQuantum-Python/23.10.0-foss-2023a-CUDA-12.2.0                s3cmd/2.2.0
   MDI/1.4.26-gompi-2023a                                   cuQuantum/23.10.0-CUDA-12.2.0                                  scikit-build/0.17.6-GCCcore-12.3.0-python-3.10.8
   METIS/5.1.0-GCCcore-12.3.0                               cuSpatial/23.10.0-foss-2023a-CUDA-12.2.0-python-3.10.8         scikit-build/0.17.6-GCCcore-12.3.0                    (D)
   MPC/1.3.1-GCCcore-12.3.0                                 cuTENSOR/1.7.0.1-CUDA-12.2.0                                   scikit-image/0.22.0-foss-2023a
   MPFR/4.2.0-GCCcore-12.3.0                                dask-cuDF/23.10.0-foss-2023a-CUDA-12.2.0-python-3.10.8         scikit-learn/1.3.1-gfbf-2023a
   MUMPS/5.5.1-foss-2023a-metis                             dask/2023.9.2-foss-2023a                                       setuptools-rust/1.6.0-GCCcore-12.3.0-python-3.10.8
   MUMPS/5.6.1-foss-2023a-metis                     (D)     dill/0.3.7-GCCcore-12.3.0                                      setuptools-rust/1.6.0-GCCcore-12.3.0                  (D)
   Mako/1.2.4-GCCcore-12.3.0                                dotNET-Core-Runtime/7.0.11-GCCcore-12.3.0                      setuptools/69.0.0-GCCcore-12.3.0
   Mesa/23.1.4-GCCcore-12.3.0                               dotNET-SDK/7.0.401-linux-x64                                   snappy/1.1.10-GCCcore-12.3.0
   Meson/1.1.1-GCCcore-12.3.0-python-3.10.8                 double-conversion/3.3.0-GCCcore-12.3.0                         spdlog/1.11.0-GCCcore-12.3.0
   Meson/1.1.1-GCCcore-12.3.0                       (D)     dtcmp/1.1.4-gompi-2023a                                        squashfuse/0.2.0-GCCcore-12.3.0
   NAMD/3.0b5-multicore-AVX512-bin                          elfutils/0.189-GCCcore-12.3.0                                  sympy/1.12-gfbf-2023a
   NAMD/3.0b5-multicore-bin                                 expat/2.5.0-GCCcore-12.3.0                                     tbb/2021.10.0-GCCcore-12.3.0
   NAMD/3.0b5-multicore-CUDA-bin                    (D)     expecttest/0.1.5-GCCcore-12.3.0                                tbb/2021.11.0-GCCcore-12.3.0                          (D)
   NASM/2.16.01-GCCcore-12.3.0                              ffnvcodec/12.0.16.0                                            tcsh/6.24.10-GCCcore-12.3.0
   NCCL/2.18.3-GCCcore-12.3.0-CUDA-12.1.1                   flatbuffers-python/23.5.26-GCCcore-12.3.0                      time/1.9-GCCcore-12.3.0
   NCCL/2.18.3-GCCcore-12.3.0-CUDA-12.2.0           (D)     flatbuffers/23.5.26-GCCcore-12.3.0                             tornado/6.3.2-GCCcore-12.3.0
   NLopt/2.7.1-GCCcore-12.3.0                               flex/2.6.4-GCCcore-10.2.0                                      tqdm/4.66.1-GCCcore-12.3.0
   NSPR/4.35-GCCcore-12.3.0                                 flex/2.6.4-GCCcore-12.3.0                                      typing-extensions/4.8.0-GCCcore-12.3.0
   NSS/3.89.1-GCCcore-12.3.0                                flex/2.6.4                                              (D)    utf8proc/2.8.0-GCCcore-12.3.0
   NTL/11.5.1-GCC-12.3.0                                    flit/3.9.0-GCCcore-12.3.0-python-3.10.8                        util-linux/2.39-GCCcore-12.3.0
   NVHPC/23.7-CUDA-12.2.0                                   flit/3.9.0-GCCcore-12.3.0                               (D)    virtualenv/20.23.1-GCCcore-12.3.0-python-3.10.8
   NVHPC/23.7                                       (D)     fontconfig/2.14.2-GCCcore-12.3.0                               virtualenv/20.23.1-GCCcore-12.3.0                     (D)
   NVSHMEM/2.9.0-gompi-2023a-CUDA-12.2.0                    foss/2023a                                                     wxWidgets/3.2.2.1-GCC-12.3.0
   NWChem/7.2.2-intel-2023a                                 fpga-samples/1.0.0                                             x264/20230226-GCCcore-12.3.0
   Ninja/1.11.1-GCCcore-12.3.0-python-3.10.8                freetype/2.13.0-GCCcore-12.3.0                                 x265/3.5-GCCcore-12.3.0
   Ninja/1.11.1-GCCcore-12.3.0                      (D)     gettext/0.21                                                   xorg-macros/1.20.0-GCCcore-12.3.0
   OPARI2/2.0.7-GCCcore-12.3.0                              gettext/0.21.1-GCCcore-12.3.0                                  xprop/1.2.6-GCCcore-12.3.0
   ORCA/5.0.4-gompi-2023a                           (D)     gettext/0.21.1                                          (D)    xxd/9.0.2116-GCCcore-12.3.0
   OSU-Micro-Benchmarks/7.2-gompi-2023a-CUDA-12.2.0         gfbf/2023a                                                     zlib/1.2.11-GCCcore-10.2.0
   OSU-Micro-Benchmarks/7.2-gompi-2023a             (D)     giflib/5.2.1-GCCcore-12.3.0                                    zlib/1.2.11
   OTF2/3.0.3-GCCcore-12.3.0                                git-lfs/3.4.0                                                  zlib/1.2.13-GCCcore-12.3.0
   OpenBLAS/0.3.23-GCC-12.3.0                               git/2.41.0-GCCcore-12.3.0-nodocs                               zlib/1.2.13                                           (D)
   OpenEXR/3.1.7-GCCcore-12.3.0                             gmpy2/2.1.5-GCC-12.3.0                                         zstd/1.5.5-GCCcore-12.3.0
   OpenFOAM/v2306-foss-2023a                                gnuplot/5.4.8-GCCcore-12.3.0

  Where:
   S:        Module is Sticky, requires --force to unload or purge
   L:        Module is loaded
   Aliases:  Aliases exist: foo/1.2.3 (1.2) means that "module load foo/1.2" will load foo/1.2.3
   D:        Default Module

If the avail list is too long consider trying:

"module --default avail" or "ml -d av" to just list the default modules.
"module overview" or "ml ov" to display the number of modules for each name.

Use "module spider" to find all possible modules and extensions.
Use "module keyword key1 key2 ..." to search for all possible modules matching any of the "keys".


mel0134 02:43:03 0 ~ 
```

## Using the module system

