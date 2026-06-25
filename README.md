# Geothermodynamics tutorial by Chikoblast
Using TidyPHREEQC to calculate 1) aqueous speciation, 2) saturation indicies of minerals, and 3) make Pourbaix diagram.

# Important links

* Download R Studio: https://posit.co/products/open-source/rstudio

* Original code of TidyPHREEQC: https://github.com/paleolimbot/tidyphreeqc

* Blog on TidyPHREEQC: https://dewey.dunnington.ca/post/2018/pourbaix-ish-diagrams-using-phreeqc-and-r/

* PHREEQC by USGS: https://www.usgs.gov/software/phreeqc-version-3

# What is PHREEQC?
"PHREEQC (Version 3 available now) is a computer program written in the C++ programming language that is designed to perform a wide variety of aqueous geochemical calculations. PHREEQC implements several types of aqueous models, including two ion-association aqueous models." - by USGS

# What is TidyPHREEQC

TidyPHREEQC is an R-based package that uses thermodynamic data from various national laboratories and the PHREEQC program to calculate aqueous speciation, mineral saturation indices, and construct Pourbaix diagrams under specified solution compositions.

The thermodynamic databases that can be used are the following: https://rdrr.io/github/paleolimbot/tidyphreeqc/man/phr_use_db.html

```
phr_use_db(db_string, save = TRUE, name = NA)

phr_get_current_db()

phr_use_db_amm(save = TRUE)

phr_use_db_ex15(save = TRUE)

phr_use_db_iso(save = TRUE)

phr_use_db_llnl(save = TRUE)

phr_use_db_minteq(save = TRUE)

phr_use_db_minteq.v4(save = TRUE)

phr_use_db_pitzer(save = TRUE)

phr_use_db_sit(save = TRUE)

phr_use_db_wateq4f(save = TRUE)

phr_use_db_phreeqc(save = TRUE)
}
```
# TidyPHREEQC: Calculating Aqueous Speciation and Mineral Saturation Indices

## Step 1: Download R Studio (Link here: https://posit.co/products/open-source/rstudio).

> RStudio (now officially known as the Posit IDE) is a cross-platform integrated development environment (IDE). It natively runs on Windows, macOS, and Linux.

## Step 2: Define your solution chemistry

### For experimental solutions

> Carefully weigh all inorganic and organic salts added to your solution and calculate their final concentrations. Using these values, construct an aqueous composition table that lists the total concentrations of all major cations and anions present in the solution (e.g., Na⁺, K⁺, Ca²⁺, Cl⁻, NO₃⁻, HCO₃⁻) in units of mmol kg⁻¹ water. This table will serve as the input for TidyPHREEQC. Although TidyPHREEQC accepts concentrations in mmol kg⁻¹, the software reports concentrations internally and in its output as molarity (M). An example of an aqueous composition table is shown below.

### For field samples

> Conduct measurements of dissolved metals using inductively coupled plasma mass spectrometry (ICP-MS) and measure anion concentrations using ion chromatography (IC). Then make the aqueous composition table (see above). 

> One caveat of PHREEQC calculations is that the thermodynamic data (e.g., stability constants for organic ligands) are often either (1) poorly constrained or (2) not included in the database. If more up-to-date thermodynamic data for organic ligands are required, they can be added manually to the database file (which can be challenging in TidyPHREEQC), or alternative platforms can be used. One such platform is the Water–Organic–Rock–Microbe (WORM) Portal, which actively maintains and updates thermodynamic databases and also allows users to upload their own database files. The WORM Portal uses EQ3/6, a geochemical modeling package developed by the Lawrence Livermore National Laboratory. EQ3/6 consists of two linked programs: EQ3 – Performs aqueous speciation and solubility calculations, and EQ6 – Performs reaction-path modeling to simulate geochemical processes and system evolution.

```
```
