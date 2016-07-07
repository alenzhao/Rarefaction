# Rarefaction tool kit - rtk
A rarefaction software written in C++11 to rarefy large high count datasets quickly and return diversity measures.

# Installation
To use rtk you can download the binary files under https://github.com/hildebra/Rarefaction/releases or compile from source.

## Compile from source
To build this software you will need to have a compiler for C++11 on your system. On a GNU/Linux system you usuallu have to install developer tools to do that. For Ubuntu this is explained here: https://help.ubuntu.com/community/InstallingCompilers


rtk was tested to compile successfully on windows (version? with compiler XY), GNU/Linux (g++ v. 4.8.5 and v. 6.1.1) and on Mac OS 10.11.2 (Apple LLVM version 7.0.0 (clang-700.0.72)).


**Compile in UNIX**
```bash
git clone https://github.com/hildebra/Rarefaction
cd Rarefaction/Rare
make
```

# Usage
Two modes for rarefaction of a count table are available

```bash
./rtk rare_inmat input.csv output.file depth.int repeats NoOfMatrices threads

./rtk rare_lowMem input.csv output.file depth.int repeats NoOfMatrices threads
```

### Options:
- **input.csv** (required)
- **output.file**: In mode `rare_inmat` the output file will be placed here. In mode `rare_lowMem` temporary files may also be stored at this location. See XYZ for details about temporary files.
- **depth.int**: Depth to rarefy to. If set to 0 a rarefaction depth of 0.95 times the smallest column sum will be used.
- **repeats**: Number of times diversity measures for all samples should be computed.
- **NoOfMatrices**: Number of rarefied matrices should be written to disk. Can be 0 or any `integer <= repeats`
- **threads**: If possible the software can use multiple threads (`default 1`).

### Ouput files:

**median_alpha_diversity.tsv**

This file contains the median diversity measures for all Samples in a tab separated format.

**[samplename]_alpha_div.tsv**

For each sample the diversity measures of all rarefaction attemts are written to an individual file. These contain for each diversity measurements multiple values. The median of which can be found in the previously mentioned file.

**rarefied_to_X_n_Y.tsv**

If `NoOfMatrices > 0` each raefied matrix will be saved in the output directory under this file. The structure of all files is the same and similar to the input file.

**sums.txt**

This file contains the column sums of all samples. It can be used to estimate well suited rarefaction depth

### Temporary files
Only in mode `rare_lowMem` temporay files will be produced to reduce RAM usage. Thus the input matrix will be first split into its columns and each column will be written into a single file.

If ...




## Input data format
Input data for rtk should be a count table in a .tsv or .csv format.
Row and column names must be provided and be unique.

**Example file:**
|       | Sample a | Sample b | Sample c | Sample d |
|-------|----------|----------|----------|----------|
| OTU 1 | 0        | 12       | 4        | 80       |
| OTU 2 | 5        | 30       | 0        | 10       |
| OTU 3 | 110       | 0        | 1       | 0        |
| OTU 4 | 43       | 253        | 15       | 30        |
| OTU 5 | 0       | 0        | 15       | 0        |
| OTU ... | ...       | ...        | ...       | ...        |
| OTU ... | ...       | ...        | ...       | ...        |
| OTU n | 25       | 12        | 3       | 0        |

Rarefaction is always performed on the columns of the dataset. If you want to rarefy on the rows please consider transposing your input data ahead of rarefaction.

### Transposing input data
On a UNIX system use AWK to transpose a `.csv` table:
http://stackoverflow.com/questions/1729824/transpose-a-file-in-bash





# Example


# Copyright
rtk is licensed unde rthe GPLv2. See notice and license file for more information.

Copyright (c) 2016 by Falk Hildebrand and Paul Saary
