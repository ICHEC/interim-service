<a href="#main-content" class="visually-hidden focusable skip-link">Skip
to main content</a>

<a href="/" class="site-logo" rel="home" title="Home"><img
src="/themes/custom/weather/logo.svg" alt="Home" /></a>

<a href="#off-canvas" id="toggle-icon"
class="toggle responsive-menu-toggle-icon" title="Menu"><span
class="label">Menu</span><span class="icon"></span></a>

<a href="/" class="site-logo" rel="home"><img
src="/sites/default/files/ICHEC-Logo.png" alt="Home" /></a>

## Register

-   [User Registration & Project
    Applications](https://nationalservice.ichec.ie/)

Search

## Main navigation

-   <a href="/about" data-drupal-link-system-path="node/14">About</a>
-   <a href="/academic" data-drupal-link-system-path="node/424">Academic</a>
-   <a href="/partnerships"
    data-drupal-link-system-path="node/10">Partnerships</a>
-   <a href="/commercial" data-drupal-link-system-path="node/8"
    title="ICHEC Commercial Services">Commercial</a>
-   [EuroCC](https://www.eurocc-ireland.ie)
-   <a href="/articles" data-drupal-link-system-path="node/40"
    title="News, blogs and press releases">News</a>
-   [Careers](https://www.ichec.ie/careers "Welcome to our careers section")

## Academic

-   <a href="/academic/national-hpc"
    data-drupal-link-system-path="node/110">National HPC Service</a>
-   <a href="/academic/prace-access"
    data-drupal-link-system-path="node/175">PRACE Access</a>
-   <a href="/academic/training-education"
    data-drupal-link-system-path="node/56"
    title="Training and Education">Training and Education</a>

<span id="main-content" tabindex="-1"></span>

## National HPC

-   <a href="/academic/national-hpc/acceptable-usage-policy"
    data-drupal-link-system-path="node/442">Acceptable Usage</a>
-   <a href="/academic/national-hpc/documentation"
    data-drupal-link-system-path="node/592">Documentation - Start Here</a>
-   <a href="/academic/national-hpc/kay-statistics-and-usage"
    data-drupal-link-system-path="node/672">Kay Statistics and Usage</a>
-   <a href="/itsecurity" data-drupal-link-system-path="node/724">IT
    Security</a>
-   <a href="/academic/national-hpc/ns-activities"
    data-drupal-link-system-path="node/621">National Service Activities</a>
-   <a href="/academic/national-hpc/national-service-projects"
    data-drupal-link-system-path="node/171">National Service Projects</a>
-   <a href="/academic/national-hpc/publications"
    data-drupal-link-system-path="node/540">Publications</a>
-   <a href="/academic/national-hpc/user-support"
    data-drupal-link-system-path="node/172">User Support</a>
-   <a href="/academic/national-hpc-service/software"
    data-drupal-link-system-path="node/64">Software</a>

# <span class="field field--name-title field--type-string field--label-hidden">Gaussian</span>

## 

### Versions Installed

Kay: 09e01 / 16b01

### Description

Starting from the basic laws of quantum mechanics, Gaussian predicts the
energies, molecular structures, and vibrational frequencies of molecular
systems, along with numerous molecular properties derived from these
basic computation types.

### License

Gaussian is available for use. Please contact
the [Helpdesk](/academic/national-hpc/user-support "ICHEC Helpdesk") to
gain access.

### Benchmarks

N/A.

### Thin Component

Gaussian jobs on Kay are run via shared memory (**without Linda**) on
a **single** compute node. Users should specify 40 processes in their
Gaussian input file (.com or .gjf)

`%nproc=40`

or

<span style="background-color: rgb(17, 17, 17);">%cpu=0-39</span>

For good performance use the %mem directive. A good compromise would be
100GB. If needed at expense of I/O caches one can go as high as 150GB,
but expect a few percentages lost in performance compared with the 100GB
case. Of course you can fine tune these values.

`%mem=100000mb`

An example of submission slurm script:

    #!/bin/sh
    # All the information about queues can be obtained using 'sinfo'
    # PARTITION AVAIL  TIMELIMIT  
    # DevQ         up    1:00:00   
    # ProdQ*       up 3-00:00:00    
    # LongQ        up 6-00:00:00    
    # ShmemQ       up 3-00:00:00    
    # PhiQ         up 1-00:00:00   
    # GpuQ         up 2-00:00:00    

    # Slurm flags
    #SBATCH -p ProdQ
    #SBATCH -N 1
    #SBATCH -t 120:00:00
    #SBATCH --job-name=myjobname
       
    # Charge job to myproject 
    #SBATCH -A myproject

    # Write stdout+stderr to file
    #SBATCH -o output.txt

    # Mail me on job start & end
    #SBATCH --mail-user=myemailaddress@universityname.ie
    #SBATCH --mail-type=BEGIN,END

    cd $SLURM_SUBMIT_DIR



    echo $GAUSS_SCRDIR

    module load gaussian/16b01

    g16 < input.gjf > output.log   

### Additional notes

The Gaussian module sets the **GAUSS\_SCRDIR** to the correct location
for that node type. Jobs can use very large RWF files as the scratch
space is provided by a large high-performance shared volume including
the follow in your submission script:

    export GAUSS_SCRDIR=/scratch/local/

Further information can be obtained
at [www.gaussian.com](http://www.gaussian.com/ "Gaussian homepage").

## 

## Supported By

File Browser Reference

<img
src="/sites/default/files/styles/inline_image/public/Department%20of%20FHERIS%20Image_1.png?itok=U4c5dr-L"
class="image-style-inline-image" loading="lazy" width="300" height="79"
alt="Department FHERIS " />

<img
src="/sites/default/files/styles/inline_image/public/University_Of_Galway_Logo__Positive_Landscape.png?itok=Xjkb-i-L"
class="image-style-inline-image" loading="lazy" width="300" height="113"
alt="University of Galway" />

<img
src="/sites/default/files/styles/inline_image/public/HEA_Logo.png?itok=kg87NqJu"
class="image-style-inline-image" loading="lazy" width="300" height="73"
alt="HEA Logo" />

## Footer sub

-   <a href="/careers" data-drupal-link-system-path="node/39">Careers</a>
-   <a href="/sitemap" data-drupal-link-system-path="sitemap">Sitemap</a>
-   <a href="/articles/media-coverage"
    data-drupal-link-system-path="node/144">Media</a>
-   <a href="/about/contact-us" data-drupal-link-system-path="node/65"
    title="Contact Us">Contact</a>

## Footer Social Media Navigation

-   <a href="https://twitter.com/ichec?lang=en" class="social-link"
    target="_blank" rel="noopener"><img
    src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB3aWR0aD0iMjciIGhlaWdodD0iMjciIHZpZXdib3g9IjAgMCAyNyAyNyI+CiAgICAgICAgICAgICAgPGRlZnM+CiAgICAgICAgICAgICAgICA8Y2lyY2xlIGlkPSJ0d2l0dGVyLWYtYSIgY3g9IjEzLjUiIGN5PSIxMy41IiByPSIxMy41Ij48L2NpcmNsZT4KICAgICAgICAgICAgICAgIDxtYXNrIGlkPSJ0d2l0dGVyLWYtYiIgd2lkdGg9IjI3IiBoZWlnaHQ9IjI3IiB4PSIwIiB5PSIwIiBmaWxsPSIjZmZmIj4KICAgICAgICAgICAgICAgICAgPHVzZSB4bGluazpocmVmPSIjdHdpdHRlci1mLWEiIC8+CiAgICAgICAgICAgICAgICA8L21hc2s+CiAgICAgICAgICAgICAgPC9kZWZzPgogICAgICAgICAgICAgIDxnIGZpbGw9Im5vbmUiIGZpbGwtcnVsZT0iZXZlbm9kZCI+CiAgICAgICAgICAgICAgICA8cmVjdCB3aWR0aD0iMjciIGhlaWdodD0iMjciPjwvcmVjdD4KICAgICAgICAgICAgICAgIDx1c2Ugc3Ryb2tlPSIjRkZGIiBzdHJva2Utd2lkdGg9IjIiIG1hc2s9InVybCgjdHdpdHRlci1mLWIpIiB4bGluazpocmVmPSIjdHdpdHRlci1mLWEiIC8+CiAgICAgICAgICAgICAgICA8cGF0aCBmaWxsPSIjRkZGIiBkPSJNMTguNzMxOTU1LDEwLjMzNzE1MzUgQzE5LjI3ODA1NzksOS45OTI1MzE0OCAxOS42OTcwODk4LDkuNDQ2MDgyMjMgMTkuODkzNzQ3Myw4Ljc5NTEyOTU0IEMxOS4zODI0Mzc3LDkuMTE1MDIxNzMgMTguODE3NDI1NCw5LjM0NjM2NTIxIDE4LjIxNDU5NDQsOS40NzE2MDk3OSBDMTcuNzMzNTM5OCw4LjkyOTE0OTIxIDE3LjA0NTk5NDgsOC41OTA5MDkwOSAxNi4yODUwODE0LDguNTkwOTA5MDkgQzE0LjgyNTI3NzMsOC41OTA5MDkwOSAxMy42NDIzMDY2LDkuODM5MzY2MTQgMTMuNjQyMzA2NiwxMS4zNzg5OTY5IEMxMy42NDIzMDY2LDExLjU5NzU3NjYgMTMuNjY0MjQxNSwxMS44MTA1NzIxIDEzLjcwOTYyNCwxMi4wMTM5OTQ5IEMxMS41MTMxMTA1LDExLjg5NzUyNTQgOS41NjU0NDQ0NiwxMC43ODg2NzIxIDguMjYwNjk3MzEsOS4xMDA2NjI0OCBDOC4wMzMwMjgzOCw5LjUxMzg4OTggNy45MDI5MzE4NSw5Ljk5MjUzMTQ4IDcuOTAyOTMxODUsMTAuNTAzMDgyNiBDNy45MDI5MzE4NSwxMS40Njk5Mzg4IDguMzY5NjE1MzMsMTIuMzIzNTE2NSA5LjA3OTA5NTIzLDEyLjgyNDQ5NDggQzguNjQ1NjkyMjYsMTIuODEwMTM1NSA4LjIzODAwNjA1LDEyLjY4MzI5NTUgNy44ODA5OTY5NywxMi40NzU4ODQxIEw3Ljg4MDk5Njk3LDEyLjUxMDE4NjcgQzcuODgwOTk2OTcsMTMuODYxNTUxNyA4Ljc5MTY3MjY3LDE0Ljk4ODc1MjkgMTAuMDAyNjI5MywxNS4yNDQwMjg1IEM5Ljc4MDI1NTAxLDE1LjMwOTQ0MjggOS41NDcyOTE0NiwxNS4zNDIxNSA5LjMwNTI1MTQsMTUuMzQyMTUgQzkuMTM1MDY2OTksMTUuMzQyMTUgOC45Njg2NjQ0NiwxNS4zMjUzOTc2IDguODA4MzEyOTIsMTUuMjkyNjkwNCBDOS4xNDQxNDM1LDE2LjM5OTk0ODEgMTAuMTIwNjIzOCwxNy4yMDcyNTcxIDExLjI3Nzg3NzgsMTcuMjI4Nzk2IEMxMC4zNzI0OTY4LDE3Ljk3NzA3MjUgOS4yMzI2MzkzOSwxOC40MjIyMDkyIDcuOTk0NDUzMjUsMTguNDIyMjA5MiBDNy43ODExNTU0NSwxOC40MjIyMDkyIDcuNTcwMTI2NzgsMTguNDEwMjQzMiA3LjM2MzYzNjM2LDE4LjM4MzkxNzkgQzguNTMzNzQ4NzQsMTkuMTc0NDc0NCA5LjkyMzIwOTkxLDE5LjYzNjM2MzYgMTEuNDE2Mjk0NSwxOS42MzYzNjM2IEMxNi4yNzk3ODY4LDE5LjYzNjM2MzYgMTguOTM3Njg5MSwxNS4zODc2MjEgMTguOTM3Njg5MSwxMS43MDI4Nzc4IEMxOC45Mzc2ODkxLDExLjU4MTYyMTkgMTguOTM2MTc2MywxMS40NjExNjM3IDE4LjkzMDg4MTcsMTEuMzQyMzAxIEMxOS40NDc0ODYsMTAuOTQ5MDE3MSAxOS44OTY3NzI4LDEwLjQ1NzYxMTcgMjAuMjUsOS44OTgzOTg2MiBDMTkuNzc1NzUyOCwxMC4xMjAxNjkzIDE5LjI2NTk1NTksMTAuMjcwMTQzNyAxOC43MzE5NTUsMTAuMzM3MTUzNSBaIj48L3BhdGg+CiAgICAgICAgICAgICAgPC9nPgogICAgICAgICAgICA8L3N2Zz4=" />
    <span class="visually-hidden">Twitter</span></a>
-   <a href="mailto:info@ichec.ie" class="social-link" target="_blank"
    rel="noopener"><img
    src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB3aWR0aD0iMjciIGhlaWdodD0iMjciIHZpZXdib3g9IjAgMCAyNyAyNyI+CiAgICAgICAgICAgICAgPGRlZnM+CiAgICAgICAgICAgICAgICA8Y2lyY2xlIGlkPSJtYWlsLWYtYSIgY3g9IjEzLjUiIGN5PSIxMy41IiByPSIxMy41Ij48L2NpcmNsZT4KICAgICAgICAgICAgICAgIDxtYXNrIGlkPSJtYWlsLWYtYiIgd2lkdGg9IjI3IiBoZWlnaHQ9IjI3IiB4PSIwIiB5PSIwIiBmaWxsPSIjZmZmIj4KICAgICAgICAgICAgICAgICAgPHVzZSB4bGluazpocmVmPSIjbWFpbC1mLWEiIC8+CiAgICAgICAgICAgICAgICA8L21hc2s+CiAgICAgICAgICAgICAgPC9kZWZzPgogICAgICAgICAgICAgIDxnIGZpbGw9Im5vbmUiIGZpbGwtcnVsZT0iZXZlbm9kZCI+CiAgICAgICAgICAgICAgICA8dXNlIHN0cm9rZT0iI0ZGRiIgc3Ryb2tlLXdpZHRoPSIyIiBtYXNrPSJ1cmwoI21haWwtZi1iKSIgeGxpbms6aHJlZj0iI21haWwtZi1hIiAvPgogICAgICAgICAgICAgICAgPHBhdGggZmlsbD0iI0ZGRiIgZD0iTTguMDQ1NzIyNiwxMC42MTczMTMxIEM4LjIxNjUwNjg1LDEwLjcyODgzNDcgOC43MzEyNjM3LDExLjA2MDE0NzIgOS41OTAwODU2MiwxMS42MTA5OTM4IEMxMC40NDg5MDc1LDEyLjE2MTg0MDQgMTEuMTA2ODAxNCwxMi41ODYwMTYzIDExLjU2Mzg1OTYsMTIuODgzNDM1OCBDMTEuNjE0MDY4NSwxMi45MTYwNDUgMTEuNzIwNzc0LDEyLjk4NjkxMjEgMTEuODgzOTc2LDEzLjA5NjEyMjggQzEyLjA0NzE3ODEsMTMuMjA1NDE5MiAxMi4xODI4MjUzLDEzLjI5MzgzMTkgMTIuMjkwNzMyOSwxMy4zNjExOSBDMTIuMzk4NzMyOSwxMy40Mjg1NDggMTIuNTI5Mjk0NSwxMy41MDQxMjI1IDEyLjY4MjUxMDMsMTMuNTg3NzQyMyBDMTIuODM1NzI2LDEzLjY3MTM2MjEgMTIuOTgwMTU3NSwxMy43MzQxODQgMTMuMTE1NzEyMywxMy43NzU4NjU1IEMxMy4yNTEzNTk2LDEzLjgxNzgwMzggMTMuMzc2OTI4MSwxMy44Mzg2MDE4IDEzLjQ5MjQxNzgsMTMuODM4NjAxOCBMMTMuNSwxMy44Mzg2MDE4IEwxMy41MDc1ODIyLDEzLjgzODYwMTggQzEzLjYyMzA3MTksMTMuODM4NjAxOCAxMy43NDg2NDA0LDEzLjgxNzgwMzggMTMuODg0Mjg3NywxMy43NzU4NjU1IEMxNC4wMTk4NDI1LDEzLjczNDE4NCAxNC4xNjQzNjY0LDEzLjY3MTI3NjYgMTQuMzE3NDg5NywxMy41ODc3NDIzIEMxNC40NzA2MTMsMTMuNTA0MDM2OSAxNC42MDExNzQ3LDEzLjQyODU0OCAxNC43MDkxNzQ3LDEzLjM2MTE5IEMxNC44MTcxNzQ3LDEzLjI5MzgzMTkgMTQuOTUyNzI5NSwxMy4yMDU0MTkyIDE1LjExNTkzMTUsMTMuMDk2MTIyOCBDMTUuMjc5MTMzNiwxMi45ODY4MjY1IDE1LjM4NTkzMTUsMTIuOTE2MDQ1IDE1LjQzNjE0MDQsMTIuODgzNDM1OCBDMTUuODk4MDk5MywxMi41ODU5MzA3IDE3LjA3MzQzMTUsMTEuODMwNTI3OSAxOC45NjE3NjcxLDEwLjYxNzE0MTkgQzE5LjMyODM5MzgsMTAuMzgwMTQ3OCAxOS42MzQ2NDA0LDEwLjA5NDE5NzEgMTkuODgwNzg0Miw5Ljc1OTQ2MTA4IEMyMC4xMjcwMjA1LDkuNDI0ODk2MjIgMjAuMjUsOS4wNzM4OTg0MSAyMC4yNSw4LjcwNjYzODggQzIwLjI1LDguMzk5ODA0NTcgMjAuMTMwNjI2Nyw4LjEzNzEzMzkzIDE5Ljg5MjA2NTEsNy45MTg2MjY4OCBDMTkuNjUzNTAzNCw3LjcwMDExOTgyIDE5LjM3MDkyODEsNy41OTA5MDkwOSAxOS4wNDQ2MTY0LDcuNTkwOTA5MDkgTDcuOTU1MjkxMSw3LjU5MDkwOTA5IEM3LjU2ODU5OTMyLDcuNTkwOTA5MDkgNy4yNzEwNDQ1Miw3LjcxMTc1OTg0IDcuMDYyNjI2NzEsNy45NTM0NjEzNCBDNi44NTQyMDg5LDguMTk1MjQ4NDIgNi43NSw4LjQ5NzQ2MDg4IDYuNzUsOC44NjAwMTMxMiBDNi43NSw5LjE1Mjg5NjQ1IDYuODg4MTQzODQsOS40NzAyNTgwNSA3LjE2NDMzOTA0LDkuODExOTI2NzQgQzcuNDQwNTM0MjUsMTAuMTUzNTk1NCA3LjczNDM5MDQxLDEwLjQyMjA4NjEgOC4wNDU3MjI2LDEwLjYxNzMxMzEgWiBNMTkuNDk2NTg5LDExLjM2MzM4NjcgQzE3Ljg0OTQwNDEsMTIuMzk1MzI1NCAxNi41OTg3MTIzLDEzLjE5NzI4ODMgMTUuNzQ1MDY4NSwxMy43NjkxMDQgQzE1LjQ1ODc5NDUsMTMuOTY0MzMxMSAxNS4yMjY1MjA1LDE0LjExNjY3ODMgMTUuMDQ4MTU0MSwxNC4yMjU4MDM1IEMxNC44Njk4ODAxLDE0LjMzNTA5OTggMTQuNjMyNjEzLDE0LjQ0NjYyMTQgMTQuMzM2MjYwMywxNC41NjA1Mzk1IEMxNC4wNCwxNC42NzQ0NTc2IDEzLjc2MzgwNDgsMTQuNzMxMzczOCAxMy41MDc2NzQ3LDE0LjczMTM3MzggTDEzLjUsMTQuNzMxMzczOCBMMTMuNDkyNDE3OCwxNC43MzEzNzM4IEMxMy4yMzYyODc3LDE0LjczMTM3MzggMTIuOTYsMTQuNjc0NDU3NiAxMi42NjM3Mzk3LDE0LjU2MDUzOTUgQzEyLjM2NzQ3OTUsMTQuNDQ2NjIxNCAxMi4xMzAxMTk5LDE0LjMzNTA5OTggMTEuOTUxODQ1OSwxNC4yMjU4MDM1IEMxMS43NzM1NzE5LDE0LjExNjY3ODMgMTEuNTQxMjk3OSwxMy45NjQzMzExIDExLjI1NTAyNCwxMy43NjkxMDQgQzEwLjU3Njk3MjYsMTMuMzA4ODk1NSA5LjMyODk2MjMzLDEyLjUwNjkzMjcgNy41MTA5MDA2OCwxMS4zNjMzODY3IEM3LjIyNDYyNjcxLDExLjE4NjgxOCA2Ljk3MDk5MzE1LDEwLjk4NDQ4NzEgNi43NSwxMC43NTY3MzY1IEw2Ljc1LDE2LjI5MzI3NTYgQzYuNzUsMTYuNjAwMTk1NCA2Ljg2Nzk4NjMsMTYuODYyNzgwNSA3LjEwNDA1MTM3LDE3LjA4MTI4NzUgQzcuMzQwMTE2NDQsMTcuMjk5ODgwMiA3LjYyMzg5Mzg0LDE3LjQwOTA5MDkgNy45NTUzODM1NiwxNy40MDkwOTA5IEwxOS4wNDQ3MDg5LDE3LjQwOTA5MDkgQzE5LjM3NjEwNjIsMTcuNDA5MDkwOSAxOS42NTk4ODM2LDE3LjI5OTg4MDIgMTkuODk1OTQ4NiwxNy4wODEyODc1IEMyMC4xMzIxMDYyLDE2Ljg2MjY5NDkgMjAuMjUsMTYuNjAwMTk1NCAyMC4yNSwxNi4yOTMyNzU2IEwyMC4yNSwxMC43NTY3MzY1IEMyMC4wMzQsMTAuOTc5Nzc5OCAxOS43ODI5NTU1LDExLjE4MjExMDYgMTkuNDk2NTg5LDExLjM2MzM4NjcgWiI+PC9wYXRoPgogICAgICAgICAgICAgIDwvZz4KICAgICAgICAgICAgPC9zdmc+" />
    <span class="visually-hidden">Contact</span></a>
-   <a href="https://www.youtube.com/user/ichecireland" class="social-link"
    target="_blank" rel="noopener"><img
    src="data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjdweCIgaGVpZ2h0PSIyN3B4IiB2aWV3Ym94PSIwIDAgMjcgMjciIHZlcnNpb249IjEuMSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB4bWxuczp4bGluaz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94bGluayI+CiAgICAgICAgICAgICAgICA8ZGVmcz4KICAgICAgICAgICAgICAgICAgICA8Y2lyY2xlIGlkPSJwYXRoLTEiIGN4PSIxMy4yIiBjeT0iMTMuNTA1ODg3NSIgcj0iMTMuMiI+PC9jaXJjbGU+CiAgICAgICAgICAgICAgICAgICAgPG1hc2sgaWQ9Im1hc2stMiIgbWFza2NvbnRlbnR1bml0cz0idXNlclNwYWNlT25Vc2UiIG1hc2t1bml0cz0ib2JqZWN0Qm91bmRpbmdCb3giIHg9IjAiIHk9IjAiIHdpZHRoPSIyNi40IiBoZWlnaHQ9IjI2LjQiIGZpbGw9IndoaXRlIj4KICAgICAgICAgICAgICAgICAgICAgICAgPHVzZSB4bGluazpocmVmPSIjcGF0aC0xIiAvPgogICAgICAgICAgICAgICAgICAgIDwvbWFzaz4KICAgICAgICAgICAgICAgIDwvZGVmcz4KICAgICAgICAgICAgICAgIDxnIGlkPSItLS1GaW5hbC1Qcm9vZi1EZXNpZ25zLS0tIiBzdHJva2U9Im5vbmUiIHN0cm9rZS13aWR0aD0iMSIgZmlsbD0ibm9uZSIgZmlsbC1ydWxlPSJldmVub2RkIj4KICAgICAgICAgICAgICAgICAgICA8ZyBpZD0iRGVza3RvcC1ob21lLXBhZ2UiIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0xMTg3LjAwMDAwMCwgLTI0NDguMDAwMDAwKSI+CiAgICAgICAgICAgICAgICAgICAgICAgIDxnIGlkPSJib3R0b20tbmF2IiB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMTguMDAwMDAwLCAyNDAzLjAwMDAwMCkiPgogICAgICAgICAgICAgICAgICAgICAgICAgICAgPGcgaWQ9InNvY2lhbC1tZWRpYSIgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMTIwNS4wMDAwMDAsIDQ1LjAwMDAwMCkiPgogICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgIDxnIGlkPSJ5b3V0dWJlLXBsYXkiPgogICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICA8cmVjdCBpZD0iUmVjdGFuZ2xlIiB4PSIwIiB5PSIwIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48L3JlY3Q+CiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgIDx1c2UgaWQ9Ik92YWwiIHN0cm9rZT0iI0Y1RjVGNSIgbWFzaz0idXJsKCNtYXNrLTIpIiBzdHJva2Utd2lkdGg9IjIiIHhsaW5rOmhyZWY9IiNwYXRoLTEiIC8+CiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgIDxwYXRoIGQ9Ik0xOS4yLDE1LjMzODUwNzkgTDE5LjIsMTEuMDYxNDkyMSBDMTkuMiwxMS4wNjE0OTIxIDE5LjIsOSAxNy4xMzIwMzIsOSBMOS4yNjcyNjI0Niw5IEM5LjI2NzI2MjQ2LDkgNy4yLDkgNy4yLDExLjA2MTQ5MjEgTDcuMiwxNS4zMzg1MDc5IEM3LjIsMTUuMzM4NTA3OSA3LjIsMTcuNCA5LjI2NzI2MjQ2LDE3LjQgTDE3LjEzMjAzMiwxNy40IEMxNy4xMzIwMzIsMTcuNCAxOS4yLDE3LjQgMTkuMiwxNS4zMzg1MDc5IE0xNS41Mjk3MjcyLDEzLjIwNTk3ODQgTDExLjYwMTIyMywxNS41MDU5MDMgTDExLjYwMTIyMywxMC45MDUzNTA0IEwxNS41Mjk3MjcyLDEzLjIwNTk3ODQiIGlkPSJTaGFwZSIgZmlsbD0iI0YzRjNGMyI+PC9wYXRoPgogICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgIDwvZz4KICAgICAgICAgICAgICAgICAgICAgICAgICAgIDwvZz4KICAgICAgICAgICAgICAgICAgICAgICAgPC9nPgogICAgICAgICAgICAgICAgICAgIDwvZz4KICAgICAgICAgICAgICAgIDwvZz4KICAgICAgICAgICAgPC9zdmc+" />
    <span class="visually-hidden">YouTube</span></a>
-   <a href="tel:35315241608" class="social-link"><img
    src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB3aWR0aD0iMjciIGhlaWdodD0iMjciIHZpZXdib3g9IjAgMCAyNyAyNyI+CiAgICAgICAgICA8ZGVmcz4KICAgICAgICAgICAgPGNpcmNsZSBpZD0icGhvbmUtYSIgY3g9IjEzLjUiIGN5PSIxMy41IiByPSIxMy41Ij48L2NpcmNsZT4KICAgICAgICAgICAgPG1hc2sgaWQ9InBob25lLWIiIHdpZHRoPSIyNyIgaGVpZ2h0PSIyNyIgeD0iMCIgeT0iMCIgZmlsbD0iI2ZmZiI+CiAgICAgICAgICAgICAgPHVzZSB4bGluazpocmVmPSIjcGhvbmUtYSIgLz4KICAgICAgICAgICAgPC9tYXNrPgogICAgICAgICAgPC9kZWZzPgogICAgICAgICAgPGcgZmlsbD0ibm9uZSIgZmlsbC1ydWxlPSJldmVub2RkIj4KICAgICAgICAgICAgPHJlY3Qgd2lkdGg9IjI3IiBoZWlnaHQ9IjI3Ij48L3JlY3Q+CiAgICAgICAgICAgIDx1c2Ugc3Ryb2tlPSIjRkZGIiBzdHJva2Utd2lkdGg9IjIiIG1hc2s9InVybCgjcGhvbmUtYikiIHhsaW5rOmhyZWY9IiNwaG9uZS1hIiAvPgogICAgICAgICAgICA8cGF0aCBmaWxsPSIjRkZGIiBkPSJNMTQuODUsMTYuNjUgQzEzLjk1LDE2LjY1IDEzLjA1LDE1Ljc1IDEyLjE1LDE0Ljg1IEMxMS4yNSwxMy45NSAxMC4zNSwxMy4wNSAxMC4zNSwxMi4xNSBDMTAuMzUsMTEuMjUgMTEuMjUsMTEuMjUgMTIuMTUsMTAuMzUgQzEzLjA1LDkuNDUgMTAuMzUsNi43NSA5LjQ1LDYuNzUgQzguNTUsNi43NSA2Ljc1LDkuNDUgNi43NSw5LjQ1IEM2Ljc1LDExLjI1IDguNTk5NSwxNC44OTk1IDEwLjM1LDE2LjY1IEMxMi4wOTk2LDE4LjQwMDUgMTUuNzUsMjAuMjUgMTcuNTUsMjAuMjUgQzE3LjU1LDIwLjI1IDIwLjI1LDE4LjQ1IDIwLjI1LDE3LjU1IEMyMC4yNSwxNi42NSAxNy41NSwxMy45NSAxNi42NSwxNC44NSBDMTUuNzUsMTUuNzUgMTUuNzUsMTYuNjUgMTQuODUsMTYuNjUgWiI+PC9wYXRoPgogICAgICAgICAgPC9nPgogICAgICAgIDwvc3ZnPg==" /></a>

## Footer Last Navigation

-   <a href="/terms-and-conditions#cookies"
    data-drupal-link-system-path="node/440">Cookie Policy</a>
-   <a href="/foi" data-drupal-link-system-path="node/647">Freedom of
    Information</a>
-   <a href="/itsecurity" data-drupal-link-system-path="node/724">IT
    Security</a>
-   <a href="/terms-and-conditions#privacy"
    data-drupal-link-system-path="node/440">Privacy Policy</a>

-   <a href="/about" data-drupal-link-system-path="node/14">About</a>
    -   <a href="/about/key-milestones"
        data-drupal-link-system-path="node/429">Key Milestones</a>
    -   <a href="/about/activities" data-drupal-link-system-path="node/137"
        title="Introducing the concept of ICHEC Activities">Activities</a>
        -   <a href="/about/activities/novel-technologies"
            data-drupal-link-system-path="node/146"
            title="Overview of ICHEC&#39;s Novel Technologies Activity">Novel
            Technologies</a>
            -   <a
                href="/about/activities/novel-technologies/ichecs-quantum-programming-ireland-qpi-initiative"
                data-drupal-link-system-path="node/656">Quantum Programming
                Initiative</a>
            -   <a href="/academic/research/quantum-natural-language-processing-qnlp"
                data-drupal-link-system-path="node/657">Quantum Natural Language
                Processing (QNLP)</a>
            -   <a href="/qpfas" data-drupal-link-system-path="node/658">Quantum PFAS
                Chemicals Remediation (QPFAS)</a>
            -   <a
                href="/about/activities/novel-technologies/training-quantum-programming"
                data-drupal-link-system-path="node/659">Training in Quantum
                Programming</a>
            -   <a href="/about/activities/novel-technologies/artificial-intelligence"
                data-drupal-link-system-path="node/661">Artificial Intelligence</a>
                -   <a
                    href="/about/activities/novel-technologies/artificial-intelligence/training-deep-learning"
                    data-drupal-link-system-path="node/575">Training in Deep Learning</a>
            -   <a
                href="/academic/research/quantex-ichec-leading-international-quantum-circuit-simulation-project"
                data-drupal-link-system-path="node/665">Quantum Circuit Simulation</a>
            -   <a href="/about/activities/novel-technologies/many-core-rd"
                data-drupal-link-system-path="node/660">Many-core R&amp;D</a>
                -   <a
                    href="/about/activities/novel-technologies/many-core-rd/fpga-research-development"
                    data-drupal-link-system-path="node/422">FPGA Research &amp;
                    Development</a>
                -   <a
                    href="/about/activities/novel-technologies/many-core-rd/gpu-research-development"
                    data-drupal-link-system-path="node/420">GPU Research &amp;
                    Development</a>
        -   <a href="/about/activities/training-education-outreach"
            data-drupal-link-system-path="node/139"
            title="Overview of ICHEC&#39;s Training, Education &amp; Outreach Activity">Training,
            Education &amp; Outreach</a>
        -   <a href="/about/activities/environmental-sciences"
            data-drupal-link-system-path="node/135"
            title="Overview of ICHEC&#39;s Climate and Environmental Activity">Climate
            and Environmental Science</a>
        -   <a href="/about/activities/oil-gas"
            data-drupal-link-system-path="node/140"
            title="Overview of ICHEC&#39;s Oil &amp; Gas activity">Oil &amp; Gas</a>
        -   <a href="/about/activities/academic-user-support"
            data-drupal-link-system-path="node/141"
            title="Overview of ICHEC&#39;s (Academic) User Support activities">Academic
            User Support</a>
        -   <a href="/about/activities/public-sector-engagement"
            data-drupal-link-system-path="node/124"
            title="Overview of ICHEC&#39;s Public Sector Activity">Public Sector</a>
    -   <a href="/about/infrastructure" data-drupal-link-system-path="node/63"
        title="Our infrastructure">Infrastructure</a>
        -   <a href="/about/infrastructure/big-data-sandbox"
            data-drupal-link-system-path="node/290" title="UNECE Hadoop cluster">Big
            data Sandbox</a>
        -   <a href="/about/infrastructure/eduroam"
            data-drupal-link-system-path="node/602">eduroam</a>
        -   <a href="/about/infrastructure/hpc-museum"
            data-drupal-link-system-path="node/288"
            title="Decommissioned HPC machines">HPC Museum</a>
            -   <a href="/about/infrastructure/fionn"
                data-drupal-link-system-path="node/162">Fionn</a>
            -   <a href="/about/infrastructure/hpc-museum/hamilton"
                data-drupal-link-system-path="node/351">Hamilton</a>
            -   <a href="/about/infrastructure/hpc-museum/lanczos"
                data-drupal-link-system-path="node/363">Lanczos</a>
            -   <a href="/about/infrastructure/hpc-museum/schrodinger"
                data-drupal-link-system-path="node/364">Schrödinger</a>
            -   <a href="/about/infrastructure/hpc-museum/stokes"
                data-drupal-link-system-path="node/411">Stokes</a>
            -   <a href="/about/infrastructure/hpc-museum/stoney"
                data-drupal-link-system-path="node/451">Stoney</a>
            -   <a href="/about/infrastructure/hpc-museum/walton"
                data-drupal-link-system-path="node/331">Walton</a>
        -   <a href="/about/infrastructure/kay"
            data-drupal-link-system-path="node/623" title="Kay HPC System">Kay</a>
    -   <a href="/about/governance"
        data-drupal-link-system-path="node/89">Governance</a>
        -   <a href="/about/governance/governance-board"
            data-drupal-link-system-path="node/131">Governance Board</a>
        -   <a href="/about/governance/university-galway-ichec-management-committee"
            data-drupal-link-system-path="node/142">University of Galway-ICHEC
            Management Committee</a>
        -   <a href="/about/governance/executive-committee"
            data-drupal-link-system-path="node/145">Executive Committee</a>
        -   <a href="/about/governance/science-council"
            data-drupal-link-system-path="node/132">Science Council</a>
        -   <a href="/about/governance/users-council"
            data-drupal-link-system-path="node/133">Users Council</a>
        -   <a
            href="/about/governance/equality-diversity-and-inclusion-edi-committee"
            data-drupal-link-system-path="node/941" title="EDI Committee">Equality,
            Diversity and Inclusion (EDI) Committee</a>
    -   <a href="/careers" data-drupal-link-system-path="node/39"
        title="Opportunities to work with us">Careers</a>
        -   <a href="/careers" data-drupal-link-system-path="node/39">Current
            Vacancies</a>
        -   <a href="/careers/why-working-ichec-could-be-right-decision-you"
            data-drupal-link-system-path="node/136"
            title="Why working for ICHEC could be the right decision for you... A personal message by ICHEC Director, J.-C. Desplat">Why
            ICHEC?</a>
    -   <a href="/staff" data-drupal-link-system-path="node/41"
        title="Our staff">Staff</a>
    -   <a href="/about/contact-us"
        data-drupal-link-system-path="node/65">Contact Us</a>
-   <a href="/academic" data-drupal-link-system-path="node/424">Academic</a>
    -   <a href="/academic/national-hpc"
        data-drupal-link-system-path="node/110">National HPC Service</a>
        -   <a href="/academic/national-hpc/acceptable-usage-policy"
            data-drupal-link-system-path="node/442">Acceptable Usage</a>
        -   <a href="/academic/national-hpc/documentation"
            data-drupal-link-system-path="node/592">Documentation - Start Here</a>
        -   <a href="/academic/national-hpc/kay-statistics-and-usage"
            data-drupal-link-system-path="node/672">Kay Statistics and Usage</a>
        -   <a href="/itsecurity" data-drupal-link-system-path="node/724">IT
            Security</a>
        -   <a href="/academic/national-hpc/ns-activities"
            data-drupal-link-system-path="node/621">National Service Activities</a>
        -   <a href="/academic/national-hpc/national-service-projects"
            data-drupal-link-system-path="node/171">National Service Projects</a>
        -   <a href="/academic/national-hpc/publications"
            data-drupal-link-system-path="node/540">Publications</a>
        -   <a href="/academic/national-hpc/user-support"
            data-drupal-link-system-path="node/172">User Support</a>
        -   <a href="/academic/national-hpc-service/software"
            data-drupal-link-system-path="node/64">Software</a>
    -   <a href="/academic/prace-access"
        data-drupal-link-system-path="node/175">PRACE Access</a>
    -   <a href="/academic/training-education"
        data-drupal-link-system-path="node/56"
        title="Training and Education">Training and Education</a>
        -   <a href="/academic/training-education/upcoming-courses"
            data-drupal-link-system-path="node/812">Upcoming Courses</a>
        -   <a href="/academic/training-education/training-courses"
            data-drupal-link-system-path="node/436">Training Courses</a>
        -   <a href="/academic/training-education/graduate-modules"
            data-drupal-link-system-path="node/221">Graduate Modules</a>
-   <a href="/partnerships"
    data-drupal-link-system-path="node/10">Partnerships</a>
    -   <a href="/partnerships/h2020" data-drupal-link-system-path="node/103"
        title="Overview of ICHEC in H2020">Horizon 2020</a>
        -   <a href="/partnerships/h2020/e-cam"
            data-drupal-link-system-path="node/22">E-CAM</a>
        -   <a href="/partnerships/h2020/escape"
            data-drupal-link-system-path="node/224">ESCAPE</a>
        -   <a href="/partnerships/h2020/ESIWACE"
            data-drupal-link-system-path="node/122">ESiWACE</a>
        -   <a href="/partnerships/h2020/HPC-Europa-3"
            data-drupal-link-system-path="node/96">HPC Europa 3</a>
        -   <a href="/partnerships/h2020/prace"
            data-drupal-link-system-path="node/97">PRACE</a>
        -   <a href="/partnerships/h2020/READEX"
            data-drupal-link-system-path="node/113">READEX</a>
        -   <a href="/partnerships/h2020/sesame-net"
            data-drupal-link-system-path="node/123">SESAME Net</a>
    -   <a href="/partnerships/industry"
        data-drupal-link-system-path="node/105">Industry Partnerships</a>
        -   <a href="/partnerships/industry/intel"
            data-drupal-link-system-path="node/112">Intel</a>
        -   <a href="/partnerships/industry/ddn"
            data-drupal-link-system-path="node/332">DDN</a>
        -   <a href="/partnerships/industry/exseisdat"
            data-drupal-link-system-path="node/333">ExSeisDat</a>
        -   <a href="/partnerships/industry/skytek"
            data-drupal-link-system-path="node/558">Skytek</a>
        -   <a href="/partnerships/industry/tullow-oil-plc"
            data-drupal-link-system-path="node/336">Tullow Oil plc</a>
        -   <a href="/partnerships/industry/xilinx"
            data-drupal-link-system-path="node/335">Xilinx</a>
    -   <a href="/partnerships/public-sector"
        data-drupal-link-system-path="node/149">Public Sector</a>
        -   <a href="/partnerships/public-sector/cso"
            data-drupal-link-system-path="node/296">CSO</a>
        -   [Enterprise Ireland](/partnerships/state-supported#EI)
        -   [Environmental Protection
            Agency](/partnerships/state-supported#EPA)
        -   [European Space Agency](/partnerships/state-supported#ESA)
        -   <a href="/partnerships/public-sector/met-eireann"
            data-drupal-link-system-path="node/297">Met Éireann</a>
        -   [Science Foundation
            Ireland](/partnerships/state-supported#SFI)
        -   [Others](/partnerships/state-supported#Others)
    -   <a href="/partnerships/activities"
        data-drupal-link-system-path="node/264">All Partnerships</a>
-   <a href="/commercial" data-drupal-link-system-path="node/8"
    title="ICHEC Commercial Services">Commercial</a>
    -   <a href="/commercial" data-drupal-link-system-path="node/8"
        title="Overview of Commercial Services">Overview</a>
    -   <a href="/commercial/client-list"
        data-drupal-link-system-path="node/265"
        title="A list of our clients">Clients List</a>
    -   <a href="/commercial/case-studies"
        data-drupal-link-system-path="node/98">Case Studies</a>
-   [EuroCC](https://www.eurocc-ireland.ie)
    -   <a href="/eurocc/academic-flagship-programme"
        data-drupal-link-system-path="node/732">Academic Flagship Programme</a>
        -   <a
            href="/news/seven-irish-research-projects-benefit-euroccireland-academic-flagship-programme"
            data-drupal-link-system-path="node/763">Seven Irish Research Projects to
            benefit from EuroHPC Academic Flagship Programme</a>
-   <a href="/articles" data-drupal-link-system-path="node/40"
    title="News, blogs and press releases">News</a>
    -   <a href="/articles" data-drupal-link-system-path="node/40">Articles</a>
        -   <a
            href="/news/third-covid-research-project-approved-ichec-nuig-research-will-expedite-diagnosis-covid-19"
            data-drupal-link-system-path="node/782">Third COVID research project
            approved by ICHEC. NUIG research will expedite diagnosis of COVID-19
            disease from patient CT scans</a>
    -   <a href="/articles/outreach" data-drupal-link-system-path="node/134"
        title="Overview of ICHEC&#39;s outreach activities.">Outreach</a>
        -   <a href="/events/outreach/ichec-bt-young-scientist-exhibition"
            data-drupal-link-system-path="node/452" title="ICHEC @ BTYSTE">BT Young
            Scientist &amp; Technology Exhibition</a>
        -   <a href="/articles/outreach/isc-high-performance-conference"
            data-drupal-link-system-path="node/454" title="ICHEC @ ISC">ISC
            conference</a>
        -   <a href="/articles/outreach/sc-conference"
            data-drupal-link-system-path="node/453" title="ICHEC @ SC">SC
            Conference</a>
            -   <a
                href="/articles/outreach/sc-conference/supercomputing-conference-2017"
                data-drupal-link-system-path="node/571">Supercomputing Conference
                2017</a>
        -   <a href="/news/outreach/ichec-10th-anniversary"
            data-drupal-link-system-path="node/439"
            title="ICHEC&#39;s 10th Anniversary Celebrations">10th Anniversary</a>
    -   <a href="/news/events"
        data-drupal-link-system-path="node/471">Events</a>
        -   <a href="/news/events" data-drupal-link-system-path="node/471"
            title="Upcoming Events">Current Events</a>
        -   <a href="/news/events/archived" data-drupal-link-system-path="node/59"
            title="Past Events ">Archived events</a>
    -   <a href="/articles/media-coverage"
        data-drupal-link-system-path="node/144"
        title="Material for the media (high resolution logos and photos, corporate information, links to relevant info, etc.)">Media
        Coverage</a>
        -   <a href="/articles/media-coverage/archived-media-coverage"
            data-drupal-link-system-path="node/286"
            title="Older ICHEC related stories in the Media">Archived Media
            Coverage</a>
        -   <a href="/articles/media-coverage/media-coverage"
            data-drupal-link-system-path="node/274"
            title="Collection of ICHEC related stories in the media">Media
            Coverage</a>
-   [Careers](https://www.ichec.ie/careers "Welcome to our careers section")
