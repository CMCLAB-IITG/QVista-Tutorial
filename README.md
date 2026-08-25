# QVista Tutorial — moved

**This tutorial now lives inside the QVista repository, at
[`docs/tutorial/`](https://github.com/CMCLAB-IITG/QVista/tree/main/docs/tutorial).**

Read it there. This repository is archived: it is kept read-only so that
existing links do not break, and it is no longer updated.

## Why it moved

Documentation that sits in a repository of its own cannot see the program
it documents, and it drifts. This tutorial did. Its installation steps were
still describing `requirements.txt` and `python -m qvista` after QVista had
moved to `pip install -e .` and a `qvista` command on PATH — nobody's
mistake, just what two repositories do to one set of instructions.

Living beside the code, the pages link to QVista's own README for
installation instead of restating it, and the screenshot tools in
`docs/tutorial/tools/` run from the repository root against the demo
structure that ships there.

## Where each page went

Every page kept its filename. `08-bonding.md` here is
[`docs/tutorial/08-bonding.md`](https://github.com/CMCLAB-IITG/QVista/blob/main/docs/tutorial/08-bonding.md)
there, and so on for all fifteen.

The pages below are the frozen copies. Each carries a link to its current
version at the top.

| | | |
|---|---|---|
| **1** | [Opening a structure](01-opening-structures.md) | load a crystal, look at it properly |
| **2** | [POTCAR](02-potcar.md) | pseudopotentials, and why the order matters |
| **3** | [INCAR](03-incar.md) | one page per job type: optimisation, DOS, band, phonon, AIMD |
| **4** | [KPOINTS](04-kpoints.md) | k-spacing and custom meshes |
| **5** | [Optimisation with CHGNet](05-optimization.md) | relax without a cluster |
| **6** | [Symmetry and k-paths](06-symmetry.md) | space group, Wyckoff sites, Brillouin-zone paths |
| **7** | [Electronic structure](07-electronic-structure.md) | bands, DOS, band centre, orbitals |
| **8** | [Bonding and charge](08-bonding.md) | Bader, DDEC6, COHP, electronegativity |
| **9** | [Phonons](09-phonons.md) | dispersion, stability, thermal properties |
| **10** | [NEB](10-neb.md) | migration barriers |
| **11** | [Molecular dynamics](11-molecular-dynamics.md) | AIMD, MSD, RDF, Van Hove, diffusion |
| **12** | [Mechanical properties](12-mechanical.md) | elastic constants and moduli |
| **13** | [Ionic conductivity](13-conductivity.md) | Nernst–Einstein, and the correlation caveat |
| **14** | [Plots and export](14-plots-and-export.md) | figures fit to publish |
| **15** | [Editing structures](15-editing-structures.md) | vacancies, slabs, format conversion |

QVista itself is at
[github.com/CMCLAB-IITG/QVista](https://github.com/CMCLAB-IITG/QVista).
