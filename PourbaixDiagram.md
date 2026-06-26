# Building a Pourbaix Diagram using modified TidyPHREEQC

>The original Pourbaix diagram code published by TidyPHREEQC uses pe and pH as the primary units. Here, I altered the code to plot the Pourbaix diagram in Eh and pH space.

# Choose your aqueous species and mineral of interest

As discussed in the "README.md" document, thermodynamic calculations should be used as a guide rather than as definitive evidence of the processes occurring in an experimental solution or natural environment. At the same time, thermodynamics predicts the equilibrium state of a system. For example, the dominant aqueous species or the most stable mineral phase, it does not account for reaction kinetics. Consequently, metastable minerals often precipitate before the thermodynamically most stable phase because they have lower kinetic barriers to formation. For this reason, thermodynamic predictions should always be interpreted alongside experimental/environmental observations.

# Code for building a Pourbaix diagram

> The following code allows you to calculate the Pourbaix diagram in Eh and pH space. 

```
library(tidyverse)
library(tidyphreeqc)

library(conflicted)
conflict_prefer("select", "dplyr")
conflict_prefer("mutate", "dplyr")
conflict_prefer("filter", "dplyr")

phr_use_db_minteq.v4()
theme_set(theme_bw())

# =========================================================
# PARAMETERS
# =========================================================

pH_seq <- seq(0, 13, 0.1)
pe_seq <- seq(-25, 50, 0.1)

aqueous_species <- c(
  "Co+2", "Co+3", "CoHPO4", "Co(OH)2", "CoOH+", "CoNO2+", "CoNO3+","Co(NO3)2, CoSO4,Co(NH3)+2"
)

solid_phases <- c(
  "Co(OH)2", "Co3(PO4)2", "CoHPO4", "Co3O4"
)

solid_labels <- solid_phases

plot_title <- "Co Eh-pH Diagram at 25°C"
plot_subtitle <- "PHREEQC (minteq database)"

# =========================================================
# 1. PHREEQC RUN
# =========================================================

result <- phr_run(
  phr_solution_list(
    pH = pH_seq,
    pe = pe_seq,
    Co = 0.00168,
    P = 35.86,
    temp = 25
  ),
  phr_selected_output(
    activities = aqueous_species,
    saturation_indices = solid_phases,
    totals = "Co",
    temp = TRUE
  )
)

# =========================================================
# 2. DATA PROCESSING
# =========================================================

result_df <- result %>%
  as_tibble() %>%
  mutate(Eh = 0.05916 * pe) %>%
  dplyr::select(
    pH, Eh,
    starts_with("si_"),
    starts_with("la_")
  )

# =========================================================
# 3. SOLID PHASES
# =========================================================

phase_map <- result_df %>%
  dplyr::select(pH, Eh, starts_with("si_")) %>%
  pivot_longer(
    cols = starts_with("si_"),
    names_to = "phase",
    values_to = "SI"
  ) %>%
  mutate(phase = str_remove(phase, "^si_")) %>%
  group_by(pH, Eh) %>%
  slice_max(SI, n = 1, with_ties = FALSE) %>%
  ungroup() %>%
  mutate(phase = factor(phase, levels = solid_phases))

# =========================================================
# 4. AQUEOUS SPECIES
# =========================================================

result_activity <- result_df %>%
  dplyr::select(pH, Eh, starts_with("la_")) %>%
  pivot_longer(
    cols = starts_with("la_"),
    names_to = "species",
    values_to = "log_activity"
  ) %>%
  mutate(species = str_remove(species, "^la_")) %>%
  group_by(pH, Eh) %>%
  summarise(
    species = species[which.max(log_activity)],
    .groups = "drop"
  )

result_labels <- result_activity %>%
  group_by(species) %>%
  summarise(
    pH = mean(pH),
    Eh = mean(Eh),
    .groups = "drop"
  )

# =========================================================
# 5. PLOT (SI COLORED ONLY)
# =========================================================

p <- ggplot() +
  
  # SI PHASES (COLORED BACKGROUND)
  geom_raster(
    data = phase_map,
    aes(x = pH, y = Eh, fill = phase),
    interpolate = TRUE
  ) +
  
  # BOUNDARIES
  geom_contour(
    data = result_activity %>%
      mutate(id = as.numeric(factor(species))),
    aes(x = pH, y = Eh, z = id),
    color = "black",
    linewidth = 0.4
  ) +
  
  # AQUEOUS LABELS (CLEAN)
  geom_text(
    data = result_labels,
    aes(x = pH, y = Eh, label = species),
    size = 2.5,
    check_overlap = TRUE,
    color = "black"
  ) +
  
  # COLOR ONLY FOR SOLIDS
  scale_fill_brewer(
    palette = "Set2",
    breaks = solid_phases,
    labels = solid_labels
  ) +
  
  labs(
    title = plot_title,
    subtitle = plot_subtitle,
    fill = "Solid phase",
    x = "pH",
    y = "Eh (V)"
  ) +
  
  scale_x_continuous(
    breaks = seq(0, 13, 1),
    expand = c(0, 0)
  ) +
  
  scale_y_continuous(
    breaks = seq(-1, 1, by = 0.2),
    expand = c(0, 0)
  ) +
  
  geom_hline(
    yintercept = 0,
    linetype = "dashed",
    linewidth = 0.4
  ) +
  
  coord_cartesian(expand = FALSE) +
  
  theme(
    panel.grid = element_blank()
  )

# =========================================================
# 6. SAVE
# =========================================================

ggsave(
  filename = "Co_Eh_pH_diagram.pdf",
  plot = p,
  width = 8,
  height = 6,
  units = "in"
)
```

> The results from this run look something like this:

<img width="958" height="722" alt="Co_Eh_pH" src="https://github.com/user-attachments/assets/63700138-8cb2-4698-b2f6-bb1f4baadef8" />




