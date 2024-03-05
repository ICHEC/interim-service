# GNU Parallel 

```{admonition} Versions Installed
:class: note

`Kay: 20190722`

`LXP: `

```

## Description

GNU **parallel** is a shell tool for executing jobs in parallel using
one or more computers. A job can be a single command or a small script
that has to be run for each of the lines in the input. The typical input
is a list of files, a list of hosts, a list of users, a list of URLs, or
a list of tables. A job can also be a command that reads from a pipe.
GNU **parallel** can then split the input and pipe it into commands in
parallel.

## License

GNU **parallel** is free software; you can redistribute it and/or modify
it under the terms of the [GNU General Public License](http://www.gnu.org/licenses/gpl.html) as published by the Free Software Foundation; either version 3 of the License, or (at your option) any later version.

When using GNU **parallel** for a publication please cite:

*O. Tange (2018): GNU Parallel 2018, March 2018, https://doi.org/10.5281/zenodo.1146014.*

## Benchmarks

N/A.

### Additional Notes

To use GNU **parallel** load the relevant environment module:

```bash
module load parallel/20190722
```

Further information can be found [here](https://www.gnu.org/software/parallel/).  

