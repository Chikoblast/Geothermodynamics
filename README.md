# Geothermodynamics tutorial by Chikoblast
Using TidyPHREEQC to calculate 1) aqueous speciation, 2) saturation indicies of minerals, and 3) make Pourbaix diagram.

# Important links

Original code of TidyPHREEQC: https://github.com/paleolimbot/tidyphreeqc

Blog on TidyPHREEQC: https://dewey.dunnington.ca/post/2018/pourbaix-ish-diagrams-using-phreeqc-and-r/

PHREEQC by USGS: https://www.usgs.gov/software/phreeqc-version-3

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
