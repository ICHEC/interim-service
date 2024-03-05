# Voro++


```{admonition} Versions Installed
:class: note

`Kay: 0.4.6`

`LXP: `

```




## Description

Voro++ is a software library for carrying out three-dimensional computations of the Voronoi tessellation. A distinguishing feature of the Voro++ library is that it carries out cell-based calculations, computing the Voronoi cell for each particle individually. It is particularly well-suited for applications that rely on cell-based statistics, where features of Voronoi cells (*eg.* volume, centroid, number of faces) can be used to analyze a system of particles. Voro++
comprises of several C++ classes that can be built as a static library. A command-line utility is also provided that can use most features of the code. The direct cell-by-cell construction makes the library particularly well-suited to handling special boundary conditions and
walls. It employs algorithms that are tolerant for numerical precision errors, it exhibits high performance, and it has been successfully employed on very large particle systems.

## License

It is distributed under a modified BSD license, that makes it free for any purpose. 

## Benchmarks

N/A.

To load Voro++, use the following command in your SLURM script:

```bash
module load voro++/0.4.6
```

## Additional notes

Further information can be obtained [here](http://math.lbl.gov/voro++/doc/).
