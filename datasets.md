---
layout: bootstrap
---

## Data Sets
Several sets of data were collected with OpenAg devices and published on GitHub.

### Basil Flavor Data
The Basil Flavor data contained in [flavor-data](https://github.com/OpenAgricultureFoundation/flavor-data) was collected
for the [Flavor-cyber-agriculture: Optimization of plant metabolites in an open-source control environment through surrogate modeling](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0213918)
paper. The goal of the paper was to show that applying machine learning to controlled environment growing could increase 
production of compounds in a plant. In this case optimizing the environment to produce more flavor compounds in basil.

The repository contains the measurements of volatile molecules as collected, measured, and identified by 
[headspace-solid phase microextraction-gas chromatography-mass spectrometry (HS-SPME-GC-MS, or GC-MS for short)](http://www.chromatographyonline.com/headspace-solid-phase-microextraction-coupled-gas-chromatography-mass-spectrometry-characterization).

### Cooper-Hewitt Data
From May 2019 through January 2020, 3 different PFC machines were set up in the [Cooper-Hewitt Museum](https://www.cooperhewitt.org/).
While network connectivity was an issue for two of the machines (due to conditions at the museum), at least one of the PFC-EDU
machines reported back data for nearly the entire time in the museum. The [Cooper_Hewitt_PFC_Data](https://github.com/OpenAgricultureFoundation/Cooper_Hewitt_PFC_Data)
repository contains all the data collected with some visualizations of the data from that one machine. While in the museum, 
the PFC was growing basil, while running a single light recipe. At times the plants were replaced as they grew to large/old, and the machine was 
cleaned a few times. (You can see the timing of the cleanings in PH and EC measurements)

### Tomato Experiment
While developing software for the PFC-EDUs one team member decided to grow [Tiny Tim dwarf tomato plants](https://www.seedsnow.com/products/tomato-tiny-tim) 
in three PFC-EDU machines, with different conditions (A control, one with basil in the same machine, and one that had no photo-rest period, but
used blue (no-ir) light for the night phase. All the data was recorded for the 3 or so months, along with harvest data. 
You can find this data in the [Tomato_Experiment](https://github.com/OpenAgricultureFoundation/Tomato_Experiment) repository.
