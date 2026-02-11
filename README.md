
# GINI-STRECO

Code and data to reproduce figures and models for:

Kohler, Green and Ortman (2026).  
“Kuznets at -7000: Is there a really long-term relationship between growth and inequality?”  
*Structural Change and Economic Dynamics* 77 (2026): 207–217.

---

## Repository layout

- `analysis.R` — main script (data ingestion → figures → models)
- `data/` — input data files (includes one large Excel file tracked with Git LFS)
- `output/` — generated figures and model outputs (created at runtime; not versioned)
- `renv.lock` — reproducible R package environment

---

## Quick start

> On first run, models may take minutes to hours depending on machine speed.

### 1) Clone the repository (Git LFS required)

```bash
git lfs install
git clone https://github.com/sgortman/GINI-STRECO.git
cd GINI-STRECO
git lfs pull


### 2) Open the R project

Open GINI-STRECO.Rproj in RStudio.

### 3) Restore the package environment

In the R console:
install.packages("renv")   # if not already installed
renv::restore()

### 4) Run the full analysis

source("analysis.R")
Figures from the publication and some model outputs are written to the output/ directory.
Some intermedate figures that you may wish to inspect are written to the R Plots pane

Stan backend: cmdstanr / CmdStan (required for brms models)
This project uses cmdstanr as the brms backend (more reliable than rstan on many systems).
If CmdStan is not already installed:
install.packages("cmdstanr",
  repos = c("https://stan-dev.r-universe.dev", getOption("repos"))
)

cmdstanr::install_cmdstan()
cmdstanr::cmdstan_version()
If cmdstanr::cmdstan_version() returns a version number (e.g., "2.38.0"), CmdStan is installed and ready.

Notes
The large Excel file in data/ is tracked using Git LFS.
If it appears as a small pointer file or has size 0, run:

git lfs pull

To regenerate outputs from scratch:

rm -r output/
Then rerun:
source("analysis.R")

Developed and tested with R 4.5.2. on a Mac chip Apple M4 Pro under Tahoe 26.2. 