# MicroRNA profiling of severe uncontrolled allergic asthmatic patients
Repository containing all code used for the development of this work. 

AÑADIR ABSTRACT DEFINITIVO

The tow main codes, `miRNAs_normalization.R` and `miRNAs_diff_exp.R`, have been mainly developed taking into account the characteristics of this project:

- Serum miRNA profiling by RT-qPCR using 7900HT Fast Real-Time PCR System with 384-Well Block Module (Thermo-Fisher) and miRCURY LNA miARN miRNome PCR Panels( Human panel I +II). 
- Used plates must have 3 UniSP3 IPC detectors, used for normalization. 
- Three groups of subjects have been considered. 

You need to take into account the neccessary changes in paths, file names and variables for the script to properly work. If you needed, you can contact me: andrea.escolar99@gmail.com

## _miRNAs_normalization.R_

### Data preparation and code execution

1. After performing RT-qPCR and once the data is ready, export the amplification data in txt foramt with RQ-Manager. The first lines of the file look like this:

~~~
RQ Manager 1.2 RQ Study Results
StudyName	Analisis_201130_P1.sdm
Operator	

Well	PlateID	Sample	Detector	Task	Ct	delta Rn	delta Ct	Ct Avg	Ct SD	Avg Delta Ct	delta Ct SD	Endo Ct Avg	Endo Ct SD	delta delta Ct	RQ	RQ Min	RQ Max	Baseline Type	Baseline Start	Baseline Stop	Threshold Type	Threshold	Instrument	Well Status	Rejected	
1		C21	hsa-miR-7-5p	Target	35.899082	2.1804953		35.899082		-4.100918		40.0						Automatic			Manual	0.2440619	279003019			
2		C21	hsa-miR-217	Target	Undetermined	-0.0019455318		40.0				40.0						Automatic			Automatic	0.04405315	279003019			
3		C21	hsa-miR-337-5p	Target	Undetermined	-0.0034669808		40.0				40.0						Automatic			Manual	0.2304093	279003019			
4		C21	hsa-miR-328-3p	Target	Undetermined	0.0077628708		40.0				40.0						Automatic			Automatic	0.30034572	279003019			
5		C21	hsa-miR-374b-3p	Target	Undetermined	0.009943667		40.0				40.0						Automatic			Manual	0.14125375	279003019			
~~~

2. In this file there are Summary lines that are necesary to delete before starting the analysis. 
3. Change blank spaces in detector names by "_". 
4. In the first script to be used, `miRNAs_normalization.R`, change lines 54-65 to define specify your 3 groups. In this case, samples starting with G1 belong to ICS group; samples starting with G5 to C (control) group; the rest, to Uc group. 
5. Before starting the analysis, you must have the folders to analyze and the scripts in one folder. Each folder to analyze must contain the amplification data (step one) in one or more txt files. Each folder is for one one panel (one folder to panel I and other folder for panel II).
6. To execute the script, you only need to execute the functions in the given code and, after that, execute this line:

~~~
main("your_folder", "1", "GME")
~~~

The fisrt argument is the folder you want to analyze, the second argument is the number of the panel of the data (remember that used panels are Human I or II) and the third is the normalization method to use. Currently, there is only one method available (GME). 


### Results

The executed script will generate a new folder called as the name of the used method (GME). Inside, there are folders (belonging to each used panel) with process control files (1-6). There is also a common to all panels control files (7) and the results file (8). This results file look like this: 

~~~
Plate_ID	miRNA	2^-AACt	ARn	Group
G1-1	hsa-miR-7-5p	1.52175143038046	2.620233	ICS
G1-1	hsa-miR-337-5p	2.78929668054527	2.2103508	ICS
G1-1	hsa-miR-328-3p	0.454750477475097	2.1269748	ICS
G1-1	hsa-miR-143-3p	1.84732555889577	2.583681	ICS
G1-1	hsa-miR-136-5p	0.0761552103131045	1.8813963	ICS
~~~

The columns represent the ID of the panel (the sample name), the name of the miRNA, the normalized expression value, ΔRn value and the group of the sample. 


### How it works?

This script is used to perform RT-qPCR expression values normalization and developes the next functions:
- data_collection: gets the data from all the input files and turn some of its columns into manageable lists.
- undetermined_IPC_delete: Function that deletes the data of those plates that have 2 or 3 of its IPCs as undetermined.
- cts_transformation_40_NA: Function that transforms some Ct values following criteria in image below.

![image](https://user-images.githubusercontent.com/67425702/206719120-02a46280-d95b-46b2-9951-87467cc38e1a.png)

- blank_NA_delete: Function that deletes those miRNAs whose cts are NA or whose miRNA names are Blank.
- interplate_normalization: Function that do interplate normalization on the data.
- GME: Function that applies GME normalization method.

![image](https://user-images.githubusercontent.com/67425702/207880665-9d023688-42c8-42ee-b2dc-510371bf14a5.png)

- ΔΔCt: Function that does ΔΔCt normalization.

![image](https://user-images.githubusercontent.com/67425702/207880923-f0ac69ae-df6d-4597-a6c0-4ddf3dc545df.png)


- DOS_ΔΔct: Function that calculates 2^-ΔΔCt.
- main: Function that executes the main code. 


## _miRNAs_diff_exp.R_

This script is used to perform differential expression analysis between groups of subjects (control, mild and severe uncontrolled):
- data_collection: gets the data from all the input files and turn some of its columns into manageable lists.
- statistical_tests_pvalues: Function that does different statistical tests. 
- main: Function that executes the main code. It also calculates the Fold Changes of each miRNA in each subjects' comparative. 


~~~
You have to take into account the neccessary changes in paths, file names and variables for the script to properly work
~~~
