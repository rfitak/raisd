
RAiSD: Software for selective sweep detection
===============================================

Authors: Nikolaos Alachiotis (n.alachiotis@gmail.com), Pavlos Pavlidis (ppavlidis@gmail.com)

Date: 9/6/2017

Version: 1.0

About
-----

RAiSD (Raised Accuracy in Sweep Detection) is a stand-alone software implementation of the μ statistic for selective sweep detection. Unlike existing implementations, including our previously released tools (SweeD and OmegaPlus), RAiSD scans whole-genome SNP data based on a composite evaluation scheme that captures multiple sweep signatures at once. 

Download and Compile
--------------------

The following commands can be used to download and compile the source code. 

    $ mkdir RAiSD
    $ cd RAiSD
    $ wget https://github.com/alachins/raisd/archive/master.zip
    $ unzip master.zip
    $ cd raisd-master
    $ make
    
The executable is placed in the path RAiSD/raisd-master/bin/release. A link to the executable is placed in the installation folder, i.e., raisd-master.

Test Run
--------

To verify that RAiSD is installed correctly, a test run can be done with the following commands. These commands are going to download a dataset (one of the many that we used for evaluation purposes) and execute RAiSD to process 1,000 simulated sets of SNPs (genomic region size = 100000 bp, weak bottleneck, selective sweep at the center of the region).
    
    $ wget 139.91.162.50/raisd_data/d1.tar.gz
    $ tar -xvzf d1.tar.gz
    $ ./RAiSD -n test_run -I d1/msselection1.out -L 100000
    
Upon completion, two output file are generated: RAiSD_Info.test_run and RAiSD_Report.test_run. 
    
In-tool Help
------------

RAiSD outputs a quick-reference help message that provides a short description for each of the supported command-line flags with the following command. 

    $ RAiSD -h
    
Input File Formats
----------------------

The current RAiSD release can process SNP data in Hudson's ms or VCF (Variant Call Format) file formats. The d1 test dataset, previously used for the test run, is in Hudson's ms format. For the VCF format, refer to the respective Wikipedia entry (https://en.wikipedia.org/wiki/Variant_Call_Format).

Output Files
------------

RAiSD generates two output files, the RAiSD_Info and the RAiSD_Report, with the run name (provided via "-n") as file extension. 

RAiSD_Info.test_run

The first 20 lines of the RAiSD_Info.test_run file are shown below.

    RAiSD, Raised Accuracy in Sweep Detection
    Copyright (C) 2017, and GNU GPL'd, by Nikolaos Alachiotis and Pavlos Pavlidis
    Contact n.alachiotis/pavlidisp at gmail.com

    Command: ./RAiSD -n test_run -I d1/msselection1.out -L 100000 -f 
    Samples: 20
    Region:  100000 bp
    Format:  ms

    A pattern structure of 65536 patterns (max. capacity) and approx. 1 MB memory footprint has been created.

    0: Set 0 | sites 6300 | snps 6300 | region 100000 - Var 53090 8.400e-04 | SFS 12005 1.000e+00 | LD 38385 1.333e+00 | MuStat 49905 3.908e-04
    1: Set 1 | sites 6296 | snps 6296 | region 100000 - Var 49665 1.970e-03 | SFS 3745 1.000e+00 | LD 46945 2.000e+00 | MuStat 49685 8.320e-04
    2: Set 2 | sites 6109 | snps 6109 | region 100000 - Var 50835 1.890e-03 | SFS 42100 1.000e+00 | LD 89390 1.500e+00 | MuStat 50770 6.825e-04
    3: Set 3 | sites 6052 | snps 6052 | region 100000 - Var 49590 1.880e-03 | SFS 5545 1.000e+00 | LD 22460 1.500e+00 | MuStat 50150 1.102e-03
    4: Set 4 | sites 6184 | snps 6184 | region 100000 - Var 51920 3.020e-03 | SFS 26445 1.000e+00 | LD 55080 1.333e+00 | MuStat 52400 1.180e-03
    5: Set 5 | sites 5519 | snps 5519 | region 100000 - Var 49310 1.660e-03 | SFS 5475 1.000e+00 | LD 42490 1.333e+00 | MuStat 47165 8.925e-04
    6: Set 6 | sites 6052 | snps 6052 | region 100000 - Var 49640 1.700e-03 | SFS 9090 1.000e+00 | LD 61435 1.250e+00 | MuStat 48080 6.200e-04
    7: Set 7 | sites 6274 | snps 6274 | region 100000 - Var 50480 2.100e-03 | SFS 18910 1.000e+00 | LD 36695 1.333e+00 | MuStat 50490 8.505e-04

The RAiSD_Info file provides execution- and dataset-related information (command line, number of samples, region size, dataset format), as well as a result line per SNP set in the input file. Each per-set result line provides the following information:
a) set index, b) number of sites, c) number of SNPs, d) region size, e) best-score location and the respective score for each of the factors that form the μ statistic, denoted as VAR, SFS, and LD, and f) best-score location and the respective score for the μ statistic (MuStat).

The RAiSD_Info file additionally reports total execution time, memory footprint, and statistics about the total number of SNP sets in the input file (total, processed, skipped), as shown in the last 6 lines of the file.

    Sets (total):     1000
    Sets (processed): 1000
    Sets (skipped):   0

    Total execution time 32.03070 seconds
    Total memory footprint 1109 kbytes
    
RAiSD_Report.test_run

The first 20 lines of the RAiSD_Report.test_run file are shown below.

    // 0
    65	9.000e-05	3.000e-01	4.000e-01	1.080e-05
    70	1.000e-04	2.000e-01	3.500e-01	7.000e-06
    85	1.300e-04	2.000e-01	3.200e-01	8.320e-06
    95	1.500e-04	2.000e-01	3.200e-01	9.600e-06
    95	1.500e-04	2.000e-01	3.200e-01	9.600e-06
    105	1.500e-04	1.000e-01	3.500e-01	5.250e-06
    110	1.600e-04	1.000e-07	3.500e-01	5.600e-12
    140	2.000e-04	1.000e-07	2.500e-01	5.000e-12
    155	2.100e-04	1.000e-01	2.400e-01	5.040e-06
    190	1.600e-04	2.000e-01	2.400e-01	7.680e-06
    225	2.100e-04	3.000e-01	5.000e-01	3.150e-05
    240	1.800e-04	3.000e-01	5.000e-01	2.700e-05
    255	1.700e-04	3.000e-01	5.833e-01	2.975e-05
    260	1.800e-04	3.000e-01	4.000e-01	2.160e-05
    265	1.700e-04	4.000e-01	5.000e-01	3.400e-05
    270	1.600e-04	4.000e-01	4.167e-01	2.667e-05
    305	1.300e-04	4.000e-01	2.500e-01	1.300e-05
    320	1.200e-04	4.000e-01	2.667e-01	1.280e-05
    330	1.200e-04	3.000e-01	4.000e-01	1.440e-05
    
For each set of SNPs (separated by a line that contains the separator symbol "//" followed by the set index), the RAiSD_Report file contains a set of result lines, one per evaluated genomic location, with each result line providing the genomic location followed by the calculated statistic values for the factors VAR, SFS, and LD, and finally the μ statistic. 
    
 

Command-line Input Arguments
------------------------
The basic execution mode DOES NOT require any FREE input parameters. 









