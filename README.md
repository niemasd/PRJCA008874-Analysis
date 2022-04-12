This repository contains a (re-)analysis of SARS-CoV-2 FASTQs from [PRJCA008874](https://ngdc.cncb.ac.cn/bioproject/browse/PRJCA008874) using the [SARS-CoV-2 analysis pipeline developed for UC San Diego's Return to Learn program](https://github.com/ucsd-ccbb/C-VIEW).

# 0: Input Data
The FASTQ files from [PRJCA008874](https://ngdc.cncb.ac.cn/bioproject/browse/PRJCA008874) can be found here:
* **HTTP:** [https://download.cncb.ac.cn/gsa/CRA006587](https://download.cncb.ac.cn/gsa/CRA006587)
* **FTP:** [ftp://download.big.ac.cn/gsa/CRA006587](ftp://download.big.ac.cn/gsa/CRA006587)
* **Metadata:** [`CRA006587.xlsx`](data/metadata/CRA006587.xlsx) ([Markdown](data/metadata/CRA006587.md))

# 1: Mapping Reads + Sorting BAM
I'm using [Minimap2 v2.24](https://github.com/lh3/minimap2/releases/tag/v2.24) to map reads against the [NC_045512.2](data/ref/NC_045512.2.fas) reference genome, piped to [samtools v1.14](https://github.com/samtools/samtools/releases/tag/1.14) to sort and output as BAM.

## 1.1: Index Reference Genome
```bash
minimap2 -t 2 -d NC_045512.2.fas.mmi NC_045512.2.fas > NC_045512.2.fas.mmi.log 2>&1
```
* **Input:** [`NC_045512.2.fas`](data/ref/NC_045512.2.fas)
* **Output:** [`NC_045512.2.fas.mmi`](data/ref/NC_045512.2.fas.mmi)
* **Log:** [`NC_045512.2.fas.mmi.log`](data/ref/NC_045512.2.fas.mmi.log)

## 1.2: Map Reads
Some of the files are quite huge, so rather than downloading them locally, I will map reads on-the-fly *while* downloading. For convenience, I have created a CSV file containing the FASTQ FTP paths ([`fastq_list.csv`](data/fastq/fastq_list.csv)). The individual Minimap2 command is as follows:

```bash
minimap2 -t THREADS -a -x sr REF.MMI READ1.FASTQ.GZ READ2.FASTQ.GZ | samtools sort --threads THREADS -o SORTED.BAM
```

However, I'll use named pipes for the FASTQ files to download + map on-the-fly, and I'll throw out unmapped reads (via Minimap2's `--sam-hit-only` flag):

```bash
minimap2 --sam-hit-only -t THREADS -a -x sr REF.MMI <(wget -qO- READ1.FASTQ.GZ.URL) <(wget -qO- READ2.FASTQ.GZ.URL) | samtools sort --threads THREADS -o SORTED.BAM
```

Putting everything together, here's the looped command for doing everything:

```bash
for f in $(cat fastq/fastq_list.csv) ; do crr=$(echo $f | cut -d'/' -f6) && url1=$(echo $f | cut -d',' -f1) && url2=$(echo $f | cut -d',' -f2) && minimap2 --sam-hit-only -t 1 -a -x sr ref/NC_045512.2.fas.mmi <(wget -qO- "$url1") <(wget -qO- "$url2") 2> "bam/$crr.01.sorted.untrimmed.bam.log" | samtools sort --threads 1 -o "bam/$crr.01.sorted.untrimmed.bam" ; done
```
