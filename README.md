# MicroRNA profiling of severe uncontrolled allergic asthmatic patients
Repository containing all code used for the development of this work

## _miRNAs_normalization.R_

This script is used to perform RT-qPCR expression values normalization and developes the next functions:
- data_collection: gets the data from all the input files and turn some of its columns into manageable lists.
- undetermined_IPC_delete: Function that deletes the data of those plates that have 2 or 3 of its IPCs as undetermined.
- cts_transformation_40_NA: Function that transforms some Ct values following criteria in image below.

![image](https://user-images.githubusercontent.com/67425702/206719120-02a46280-d95b-46b2-9951-87467cc38e1a.png)

- blank_NA_delete: Function that deletes those miRNAs whose cts are NA or whose miRNA names are Blank.
- interplate_normalization: Function that do interplate normalization on the data.
- GME: Function that applies GME normalization method.

![image](https://user-images.githubusercontent.com/67425702/206719972-6ff2d126-66bf-462b-afc9-a5065cca33df.png)

- ΔΔCt: Function that does ΔΔCt normalization.

![image](https://user-images.githubusercontent.com/67425702/206720501-ad3db4ab-830d-465e-9810-81d28cc9c039.png)

- DOS_ΔΔct: Function that calculates 2^-ΔΔCt.

** You have to take into account the neccessary changes in paths, file names and variables for the script to properly work
