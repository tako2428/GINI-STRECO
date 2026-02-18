
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

> On first run, models may take many minutes depending on machine speed.

### 1) Install Git LFS (Large File Storage)

Download git LFS from https://git-lfs.com/
Unzip the file
Then in Terminal:
cd ~/Downloads/git-lfs-3.7.1.  [or fill in the file path to your downloaded the program file]
ls  [you should see install.sh]
chmod +x install.sh   [make sure it’s executable]
./install.sh
git lfs install
git lfs version
If a version number is returned, git LFS is installed


### 2) Clone the repository and ensure Git LFS works within it

Still in Terminal:
git clone https://github.com/sgortman/GINI-STRECO.git
cd ~/Documents/Projects/GINI-STRECO
git lfs install
git lfs pull



### 3) Open the R project

Open GINI-STRECO.Rproj in RStudio

### 4) Restore the package environment

In the R console:
install.packages("renv")   # if not already installed
renv::restore()

### 5) Stan backend: cmdstanr / CmdStan (required for brms models)
This project uses cmdstanr as the brms backend (more reliable than rstan on many systems).
If CmdStan is not already installed, in R console:
install.packages("cmdstanr",
  repos = c("https://stan-dev.r-universe.dev", getOption("repos"))
)

cmdstanr::install_cmdstan()
cmdstanr::cmdstan_version()
If cmdstanr::cmdstan_version() returns a version number (e.g., "2.38.0"), CmdStan is installed and ready.

### 6) Run the full analysis

source("analysis.R")
Figures from the publication and some model outputs are written to the output/ directory.
Some intermedate figures that you may wish to inspect are written to the R Plots pane


Notes
The large Excel file in data/ is tracked using Git LFS.
If it appears as a small pointer file or has size 0, run:

git lfs pull

To regenerate outputs from scratch:

rm -r output/
Then rerun:
source("analysis.R")

Developed and tested with R 4.5.2. on a Mac chip Apple M4 Pro under Tahoe 26.2. 