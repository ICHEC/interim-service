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

The following list is not exhaustive and does not include many packages one might take for granted, e.g. perl. Certain packages are installed on a request basis and so may not yet have been requested on a given system. Some are general purpose compilers or libraries, other are softwares specific to a domain, such as material science, physics, chemistry, computational biology, statistics etc. For more details about the software, please click on the link therein.


| Package Name: Description                                                      | Version(s) | Domain |
|--------------------------------------------------------------------------------|------------|--------|
| [Abaqus](./softwares/abaqus.md): Finite Element Analysis                       |            | Engineering |
| [Abinit](./softwares/abinit.md): DFT based simulation                          |            | Physics     |
| [Amber](./softwares/amber.md)                                                  |            |        |
| [ANSYS](./softwares/ansys.md)                                                  |            |        |
| [Cmake3-Cross-Platform-Make](./softwares/cmake3-cross-platform-make.md)        |            |        |
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