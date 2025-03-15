# Pipeline for processing fluorescence data collected in ImageXpress® Micro XLS

SUMMARY

For analysis what we basically need is to be able to track which bead/phagosome (bead within phagosome) is flashing (or not) over time. The program needs to be able to track multiple beads over the length of the imaging period and be able to distinguish between the different beads i.e. bead 1 vs bead 2 vs bead 3 etc. We need a dataset that gives us fluorescence values for each timepoint per bead within the phagosome. These values need to correspond correctly to the same bead within the phagosome. Based on this, we will then see (and calculate) "eructophagy" events as well-separated elevations of "fluorescence intensity" in the Cy3 channel over time, with no elevations in the Cy5 channel.

<p align="center">
  <img src="Cy3_vs_Cy5_plots.png" alt="Illustration of Cy3/Cy5 signals">
</p>

Initially, a prototype was build in Google colab, and that can be found [here](identifyPeaks_ImageXpress.ipynb).

The above figures illustrate the concept of "fluorescent intensity": in the Cy3 resorufin channel will vary over time. This is our current method of quantifying eructophagy as “spikes” in fluorescence in the Cy3 channel. Y-axis is fluorescence intensity. X-axis is time. This one line represents one “track”/bead/phagosome. Eructophagy is a transient increase in fluorescent in response to a biochemical change in the phagosome of the cell. 

For both Cy3 and Cy5, we want the intensity of the bead inside the phagosome, NOT the intensity of the entire cell.

## DESCRIPTION OF DATA

- Data is provided in Excel files:

1. Column A contains the well of a 96-well plate that was analyzed (Well).

2. Each Sheet contain data from a site (field of view of the microscope), so each Excel workbook will contain as many sheets as sites were examined. This is registered in column B (Site).

3. Column C contains repeats for each measurement (beads). There are three repeats per bead. From the first two Cy5 records, only one is needed, the other one can be ignored. The first repeat will be used.

- Cy3 (Cyanine 3) is a fluorescent dye. It belongs to the cyanine dye family and is known for its bright orange-red fluorescence. In our case, the Cy3 channel was used to capture resorufin cellobioside flashes. Resorufin is a red fluorescent compound with Excitation ~570 nm and Emission ~585 nm.

What is the difference between Cy5 and Cy3?

Cy5 channel served as a negative control (bead-conjugated tracing fluor AF647SE) to ensure that any signal detected in the Cy3 channel was specific to resorufin fluorescence. Cy5 shouldn’t show any peaks because resorufin emits in the Cy3 range (~570 nm), not in the Cy5 range (~670 nm). If Cy5 does show a signal, it would indicate false positives, meaning there is bleed-through, autofluorescence, or non-specific fluorescence affecting the results. This comparison helps validate that the observed Cy3 signal is true resorufin fluorescence, not background noise or unintended fluorescence from other sources.

## RESULTS TO GENERATE

Generate an excel file from the one I gave you that gives me total number of peaks in cy3 channel (and no false positive in cy5) against each row, probably something in columns AT or AU for each bead.

