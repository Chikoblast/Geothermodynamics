# Standardized element and speciation names in TidyPHREEQC (and in PHREEQC)

> The Minteq.v4 database provides standardized naming conventions for each element, sometimes including oxidation states, and specifies the associated aqueous species used to represent chemical speciation in thermodynamic calculations. Example of Minteq.v4 database standardized naming is shown below:

> If you are using a different database, carefully check how each element and its speciation are defined in each thermodynamic database (go to folder 'ThermodynamicDatabase.'

**Table 1.** Standardized element (sometimes with oxidation state) and aqueous speciation names in Minteq.v4. 
| Element name        | PHREEQC Minteq.v4 element | PHREEQC Minteq.v4 speciation |
|---------------------|--------------------------|------------------------------|
| Silver              | Ag                       | Ag+                          |
| Aluminum            | Al                       | Al+3                         |
| Arsenic             | As                       | H3AsO4                       |
|                     | As(3)                    | H3AsO3                       |
|                     | As(5)                    | H3AsO4                       |
| Boron               | B                        | H3BO3                        |
| Barium              | Ba                       | Ba+2                         |
|                     | Be                       | Be+2                         |
| Bromine             | Br                       | Br-                          |
| Carbon              | C                        | CO3-2                        |
|                     | C(4)                     | CO3-2                        |
| Cyanide             | Cyanide                 | Cyanide-                     |
| DOM                 | Dom_a                    | Dom_a                        |
|                     | Dom_b                    | Dom_b                        |
|                     | Dom_c                    | Dom_c                        |
| Calcium             | Ca                       | Ca+2                         |
| Cadmium             | Cd                       | Cd+2                         |
| Chloride            | Cl                       | Cl-                          |
| Cobalt              | Co                       | Co+3                         |
|                     | Co(2)                    | Co+2                         |
|                     | Co(3)                    | Co+3                         |
| Chromium            | Cr                       | CrO4-2                       |
|                     | Cr(2)                    | Cr+2                         |
|                     | Cr(3)                    | Cr(OH)2+                     |
|                     | Cr(6)                    | CrO4-2                       |
| Copper              | Cu                       | Cu+2                         |
|                     | Cu(1)                    | Cu+                          |
|                     | Cu(2)                    | Cu+2                         |
| Fluorine            | F                        | F-                           |
| Iron                | Fe                       | Fe+3                         |
|                     | Fe(2)                    | Fe+2                         |
|                     | Fe(3)                    | Fe+3                         |
| Hydrogen            | H                        | H+                           |
|                     | H(0)                     | H2                           |
|                     | H(1)                     | H+                           |
| Mercury             | Hg                       | Hg(OH)2                      |
|                     | Hg(0)                    | Hg                           |
|                     | Hg(1)                    | Hg2+2                        |
|                     | Hg(2)                    | Hg(OH)2                      |
| Iodine              | I                        | I-                           |
| Potassium           | K                        | K+                           |
| Lithium             | Li                       | Li+                          |
| Magnesium           | Mg                       | Mg+2                         |
| Manganese           | Mn                       | Mn+3                         |
|                     | Mn(2)                    | Mn+2                         |
|                     | Mn(3)                    | Mn+3                         |
|                     | Mn(6)                    | MnO4-2                       |
|                     | Mn(7)                    | MnO4-                         |
| Molybdenum          | Mo                       | MoO4-2                       |
| Nitrogen            | N                        | NO3-                         |
|                     | N(-3)                    | NH4+                         |
|                     | N(3)                     | NO2-                         |
|                     | N(5)                     | NO3-                         |
| Sodium              | Na                       | Na+                          |
| Nickel              | Ni                       | Ni+2                         |
| Phosphorus          | P                        | PO4-3                        |
| Lead                | Pb                       | Pb+2                         |
| Sulfur              | S                        | SO4-2                        |
|                     | S(-2)                    | HS-                          |
|                     | S(0)                     | S                            |
|                     | S(6)                     | SO4-2                        |
| Antimony            | Sb                       | Sb(OH)6-                     |
|                     | Sb(3)                    | Sb(OH)3                      |
|                     | Sb(5)                    | Sb(OH)6-                     |
| Selenium            | Se                       | SeO4-2                       |
|                     | Se(-2)                   | HSe-                         |
|                     | Se(4)                    | HSeO3-                       |
|                     | Se(6)                    | SeO4-2                       |
| Silicon             | Si                       | H4SiO4                       |
| Tin                 | Sn                       | Sn(OH)6-2                    |
|                     | Sn(2)                    | Sn(OH)2                      |
|                     | Sn(4)                    | Sn(OH)6-2                    |
| Strontium           | Sr                       | Sr+2                         |
| Thallium            | Tl                       | Tl(OH)3                      |
|                     | Tl(1)                    | Tl+                          |
|                     | Tl(3)                    | Tl(OH)3                      |
| Uranium             | U                        | UO2+2                        |
|                     | U(3)                     | U+3                          |
|                     | U(4)                     | U+4                          |
|                     | U(5)                     | UO2+                         |
|                     | U(6)                     | UO2+2                        |
| Vanadium            | V                        | VO2+                         |
|                     | V(2)                     | V+2                          |
|                     | V(3)                     | V+3                          |
|                     | V(4)                     | VO+2                         |
|                     | V(5)                     | VO2+                         |
| Zinc                | Zn                       | Zn+2                         |
| Benzoate            | Benzoate                | -                            |
| Phenylacetate       | Phenylacetate           | -                            |
| Isophthalate        | Isophthalate            | -                            |
| Diethylamine        | Diethylamine            | -                            |
| Butylamine          | Butylamine              | -                            |
| Methylamine         | Methylamine             | -                            |
| Dimethylamine       | Dimethylamine           | -                            |
| Hexylamine          | Hexylamine              | -                            |
| Ethylenediamine     | Ethylenediamine         | -                            |
| Propylamine         | Propylamine             | -                            |
| Isopropylamine      | Isopropylamine          | -                            |
| Trimethylamine      | Trimethylamine          | -                            |
| Citrate             | Citrate                 | -                            |
| NTA                 | Nta                     | -                            |
| EDTA                | Edta                    | -                            |
| Propionate          | Propionate              | -                            |
| Butyrate            | Butyrate                | -                            |
| Isobutyrate         | Isobutyrate             | -                            |
| 2-Picoline          | Two_picoline            | -                            |
| 3-Picoline          | Three_picoline          | -                            |
| 4-Picoline          | Four_picoline           | -                            |
| Formate             | Formate                 | -                            |
| Isovalerate         | Isovalerate             | -                            |
| Valerate            | Valerate                | -                            |
| Acetate             | Acetate                 | -                            |
| Tartarate           | Tartarate               | -                            |
| Glycine             | Glycine                 | -                            |
| Salicylate          | Salicylate              | -                            |
| Glutamate           | Glutamate               | -                            |
| Phthalate           | Phthalate               | -                            |
