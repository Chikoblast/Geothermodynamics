# Geothermodynamics tutorial
Using TidyPHREEQC (and the modified code), you can calculate (1) aqueous speciation, (2) mineral saturation indices, and (3) construct speciation and Pourbaix diagrams. Because the code runs within RStudio (now officially called the Posit IDE), it is fully compatible with Windows, macOS, and Linux, making thermodynamic calculations accessible to all users. In addition, since it is run on R, it is freely available and allows you to generate both speciation and Pourbaix diagrams for free.

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
# Before you get started

## Step 1: Download R Studio (Link here: https://posit.co/products/open-source/rstudio).

> RStudio (now officially known as the Posit IDE) is a cross-platform integrated development environment (IDE). It natively runs on Windows, macOS, and Linux.

## Step 2: Define your solution chemistry

### For experimental solutions

> Carefully weigh all inorganic and organic salts added to your solution and calculate their final concentrations. Using these values, construct an aqueous composition table that lists the total concentrations of all major cations and anions present in the solution (e.g., Na<sup>+</sup>, K<sup>+</sup>, Ca<sup>2+</sup>, Cl<sup>-</sup>, NO<sub>3</sub><sup>-</sup>, HCO<sub>3</sub><sup>-</sup>) in units of mM water. This table will serve as the input for TidyPHREEQC. Although TidyPHREEQC accepts concentrations in mM, the program reports concentrations internally and in its output as molarity (M). An example of an aqueous composition table is shown below.

**Table 1.** Example of the aqueous composition table. 
| Salt | EDTA | Cyanide (CN<sup>-</sup>) | K<sup>+</sup> | Na<sup>+</sup> | P | N (NH<sub>4</sub><sup>+</sup>) | N (NO<sub>3</sub><sup>−</sup>) | S (SO<sub>4</sub><sup>2−</sup>) | Mg<sup>2+</sup> | Cl<sup>−</sup> | Zn<sup>2+</sup> | Ca<sup>2+</sup> | Fe<sup>2+</sup> | Mo | Cu<sup>2+</sup> | Co<sup>2+</sup> | Mn<sup>2+</sup> |
|------|------|---------|--------------|--------------|--------------------------------|------------------------------|-------------------------------|-------------------------------|----------------|----------------|----------------|----------------|----------------|----------------|----------------|----------------|----------------|
| Units | mM | mM | mM | mM | mM | mM | mM | mM | mM | mM | mM | mM | mM | mM | mM | mM | mM |
| K<sub>2</sub>HPO<sub>4</sub> | 0 | 0 | 44.54 | 0 | 22.27 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| NaH<sub>2</sub>PO<sub>4</sub> | 0 | 0 | 0 | 13.59 | 13.59 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| (NH<sub>4</sub>)<sub>2</sub>SO<sub>4</sub> | 0 | 0 | 0 | 0 | 0 | 30.28 | 0 | 15.14 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| MgCl<sub>2</sub> | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0.49188 | 0.98376 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| EDTA | 0.03422 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| Cyanide | 0 | 0.0097 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| ZnSO<sub>4</sub> | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0.00696 | 0 | 0 | 0.00696 | 0 | 0 | 0 | 0 | 0 | 0 |
| CaCl<sub>2</sub> | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0.0136 | 0 | 0.0068 | 0 | 0 | 0 | 0 | 0 |
| FeSO<sub>4</sub> | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0.01798 | 0 | 0 | 0 | 0 | 0.01798 | 0 | 0 | 0 | 0 |
| Na<sub>2</sub>MoO<sub>4</sub> | 0 | 0 | 0 | 0.00166 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0.00083 | 0 | 0 | 0 |
| CuSO<sub>4</sub> | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0.0008 | 0 | 0 | 0 | 0 | 0 | 0 | 0.0008 | 0 | 0 |
| CoCl<sub>2</sub> | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0.00168 | 0 |
| MnCl<sub>2</sub> | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0.00616 |
| NaNO<sub>3</sub> | 0 | 0 | 0 | 20 | 0 | 0 | 20 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| **Sum** | 0.03422 | 0.0097 | 44.54 | 33.59166 | 35.86 | 30.28 | 20 | 15.16574 | 0.49188 | 1.01304 | 0.00696 | 0.0068 | 0.01798 | 0.00083 | 0.0008 | 0.00168 | 0.00616 |

### For field samples

> Conduct measurements of dissolved metals using inductively coupled plasma mass spectrometry (ICP-MS) and measure anion concentrations using ion chromatography (IC). Then make the aqueous composition table (see above). 

### Caution
> One caveat of PHREEQC calculations is that the thermodynamic data (e.g., stability constants for organic ligands) are often either (1) poorly constrained or (2) not included in the database. If more up-to-date thermodynamic data for organic ligands are required, they can be added manually to the database file (which can be challenging in TidyPHREEQC), or alternative platforms can be used. One such platform is the Water–Organic–Rock–Microbe (WORM) Portal (runs on Jupiter Notebook; Link here: https://worm-portal.asu.edu/), which actively maintains and updates thermodynamic databases and also allows users to upload their own database files. The WORM Portal uses EQ3/6, a geochemical modeling package developed by the Lawrence Livermore National Laboratory. EQ3/6 consists of two linked programs: EQ3 – Performs aqueous speciation and solubility calculations, and EQ6 – Performs reaction-path modeling to simulate geochemical processes and system evolution.

# To construct a speciation and Pourbaix diagram

>Please read the 'AqueousSpeciation.md' and 'Pourbaix.md' for more information.

# Standardized element and speciation names

>To see how elements (including oxidation states) and their speciation are named across databases, start with StandardizedNames.md, then check the ThermodynamicData folder for further information.










