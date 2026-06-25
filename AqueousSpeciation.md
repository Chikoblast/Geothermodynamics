# Obtaining Aqueous Speciation and Saturation Indices in Target Solutions

## Step 1: Calculate the aqueous composition table

Obtain information about the aqueous solution composition from your experimental or field solution and make a aqueous composition table (Table 1). 

**Table 1.** Example of aqueous composition table. 

| Salt | EDTA | Cyanide | K<sup>+</sup> | Na<sup>+</sup> | P (HPO<sub>4</sub><sup>2−</sup>) | N (NH<sub>4</sub><sup>+</sup>) | N (NO<sub>3</sub><sup>−</sup>) | S (SO<sub>4</sub><sup>2−</sup>) | Mg<sup>2+</sup> | Cl<sup>−</sup> | Zn<sup>2+</sup> | Ca<sup>2+</sup> | Fe<sup>2+</sup> | Mo<sup>4+</sup> | Cu<sup>2+</sup> | Co<sup>2+</sup> | Mn<sup>2+</sup> |
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


## Step 2: Run the TidyPHREEQC code for calculating aqueous speciation

> Take aqueous speciation table and place it in "phr_solution()" (see the code below). Be careful with the syntax or else the speciation will not be imported into the PHREEQC calculations. For the type of syntaxes available in each of your database. 

```
library(plyr)

#Tidyverse a R package for data science
library(tidyverse)

# devtools::install_github("paleolimbot/tidyphreeqc")
library(tidyphreeqc)

#Database you are using:
phr_use_db_minteq.v4()

#Solution - Initial condition
elm = "Co"

#pH - you can change the range of pH here
pHCode <- c(5,6,7,8,9,10)
pHLen =  1:length(pHCode)

#Phreeqc calculation input

  for (ipH in pHLen){
    #Change here ----->
    sink(sprintf("pH%s_%s_Scenario3.txt",pHCode[ipH],elm))
    phr_run(
      phr_solution(
        #Change here (units are in mM ----->
        "EDTA" = 0.03422,
        "K" = 44.54,
        "Na" = 33.59166, 
        "P" = 35.86,
        "N(3)" = "30.28 as NH4+",
        "N(5)" = "20 as NO3-",
        "S(6)" = "15.16574 as SO4-2", 
        "Mg" = 0.49188, 
        "Cl" = 1.01304,
        "Zn" = 0.00696,
        "Ca" = 0.0068,
        "Fe(2)" = 0.01798,
        "Mo" = 0.01798,
        "Cu(2)" = "0.0008 as Cu+2",
        "Co(2)" = "0.00168 as Co+2",
        "Mn(2)" = "0.00616 as Mn+2",
        "Cyanide" = 0.0097,
        "pH" = pHCode[ipH],
        "temp" = 25)
        ) %>%
        phr_print_output()
        sink()
        }
```
