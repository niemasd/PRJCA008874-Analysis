This repository contains a (re-)analysis of SARS-CoV-2 FASTQs from [PRJCA008874](https://ngdc.cncb.ac.cn/bioproject/browse/PRJCA008874) using the [SARS-CoV-2 analysis pipeline developed for UC San Diego's Return to Learn program](https://github.com/ucsd-ccbb/C-VIEW).

# 0: Input Data
The FASTQ files from [PRJCA008874](https://ngdc.cncb.ac.cn/bioproject/browse/PRJCA008874) can be found here:
* **HTTP:** [https://download.cncb.ac.cn/gsa/CRA006587](https://download.cncb.ac.cn/gsa/CRA006587)
* **FTP:** [ftp://download.big.ac.cn/gsa/CRA006587](ftp://download.big.ac.cn/gsa/CRA006587)
* **Metadata:** [`CRA006587.xlsx`](data/metadata/CRA006587.xlsx) ([Markdown](data/metadata/CRA006587.md))

# 1: Mapping Reads
I'm using [Minimap2 v2.24](https://github.com/lh3/minimap2/releases/tag/v2.24) to map reads against the [NC_045512.2](data/ref/NC_045512.2.fas) reference genome.

## 1.1: Index Reference Genome
```bash
minimap2 -t 2 -d NC_045512.2.fas.mmi NC_045512.2.fas > NC_045512.2.fas.mmi.log 2>&1
```
* **Input:** [`NC_045512.2.fas`](data/ref/NC_045512.2.fas)
* **Output:** [`NC_045512.2.fas.mmi`](data/ref/NC_045512.2.fas.mmi)
* **Log:** [`NC_045512.2.fas.mmi.log`](data/ref/NC_045512.2.fas.mmi.log)
