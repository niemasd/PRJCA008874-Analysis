This repository contains a (re-)analysis of SARS-CoV-2 FASTQs from [PRJCA008874](https://ngdc.cncb.ac.cn/bioproject/browse/PRJCA008874) ([Lu *et al*., The Lancet 2020](https://doi.org/10.1016/S0140-6736(20)30251-8)) using the SARS-CoV-2 analysis pipeline developed for UC San Diego's Return to Learn program ([C-VIEW](https://github.com/ucsd-ccbb/C-VIEW)).

# 0: Input Data
The FASTQ files from [PRJCA008874](https://ngdc.cncb.ac.cn/bioproject/browse/PRJCA008874) can be found here:
* **HTTP:** [https://download.cncb.ac.cn/gsa/CRA006587](https://download.cncb.ac.cn/gsa/CRA006587)
* **FTP:** [ftp://download.big.ac.cn/gsa/CRA006587](ftp://download.big.ac.cn/gsa/CRA006587)
* **Metadata:** [`CRA006587.xlsx`](data/metadata/CRA006587.xlsx) ([Markdown](data/metadata/CRA006587.md))

Here's a mapping of BioSample to various relevant IDs for convenience:

## Table: BioSamples

|BioSample                                                        |Description        |Experiment Accession                                               |Run Accession(s)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|-----------------------------------------------------------------|-------------------|-------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|[SAMC703641](https://ngdc.cncb.ac.cn/biosample/browse/SAMC703641)|WH19001 and WH19005|[CRX398523](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRX398523)|[CRR456568](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRR456568)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|[SAMC703642](https://ngdc.cncb.ac.cn/biosample/browse/SAMC703642)|WH19002            |[CRX398524](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRX398524)|[CRR456569](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRR456569)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|[SAMC703643](https://ngdc.cncb.ac.cn/biosample/browse/SAMC703643)|WH19004            |[CRX398525](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRX398525)|[CRR456570](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRR456570)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|[SAMC703644](https://ngdc.cncb.ac.cn/biosample/browse/SAMC703644)|WH19008            |[CRX398526](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRX398526)|[CRR456571](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRR456571)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|[SAMC703645](https://ngdc.cncb.ac.cn/biosample/browse/SAMC703645)|YS8011             |[CRX398527](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRX398527)|[CRR456572](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRR456572), [CRR456573](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRR456573)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|[SAMC703646](https://ngdc.cncb.ac.cn/biosample/browse/SAMC703646)|WH01               |[CRX398528](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRX398528)|[CRR456574](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRR456574), [CRR456575](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRR456575), [CRR456576](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRR456576), [CRR456577](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRR456577), [CRR456578](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRR456578), [CRR456579](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRR456579), [CRR456580](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRR456580), [CRR456581](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRR456581), [CRR456582](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRR456582), [CRR456583](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRR456583), [CRR456584](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRR456584), [CRR456585](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRR456585), [CRR456586](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRR456586), [CRR456587](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRR456587)|
|[SAMC703647](https://ngdc.cncb.ac.cn/biosample/browse/SAMC703647)|WH02               |[CRX398529](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRX398529)|[CRR456588](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRR456588), [CRR456589](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRR456589), [CRR456590](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRR456590), [CRR456591](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRR456591), [CRR456592](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRR456592), [CRR456593](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRR456593), [CRR456594](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRR456594), [CRR456595](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRR456595), [CRR456596](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRR456596), [CRR456597](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRR456597)                                                                                                                                                                                                                                                                                    |
|[SAMC703648](https://ngdc.cncb.ac.cn/biosample/browse/SAMC703648)|WH03               |[CRX398530](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRX398530)|[CRR456598](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRR456598), [CRR456599](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRR456599), [CRR456600](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRR456600), [CRR456601](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRR456601)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|[SAMC703649](https://ngdc.cncb.ac.cn/biosample/browse/SAMC703649)|WH04               |[CRX398531](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRX398531)|[CRR456602](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRR456602), [CRR456603](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRR456603), [CRR456604](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRR456604), [CRR456605](https://ngdc.cncb.ac.cn/gsa/browse/CRA006587/CRR456605)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |

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
Some of the FASTQ files are quite huge, so rather than downloading them locally, I will map reads on-the-fly *while* downloading. For convenience, I have created a CSV file containing the FASTQ FTP paths ([`fastq_list.csv`](data/fastq/fastq_list.csv)). The individual Minimap2 command is as follows:

```bash
minimap2 -t THREADS -a -x sr REF.MMI READ1.FASTQ.GZ READ2.FASTQ.GZ | samtools sort --threads THREADS -o SORTED.BAM
```
* `-a` means "output in the SAM format"
* `-x sr` means "use Minimap2's genomic short-read mapping preset"

However, I'll use named pipes for the FASTQ files to download + map on-the-fly, and I'll throw out unmapped reads (via Minimap2's `--sam-hit-only` flag):

```bash
minimap2 --sam-hit-only -t THREADS -a -x sr REF.MMI <(wget -qO- READ1.FASTQ.GZ.URL) <(wget -qO- READ2.FASTQ.GZ.URL) | samtools sort --threads THREADS -o SORTED.BAM
```

Putting everything together, here's the looped command for doing everything:

```bash
for f in $(cat fastq/fastq_list.csv) ; do crr=$(echo $f | cut -d'/' -f6) && url1=$(echo $f | cut -d',' -f1) && url2=$(echo $f | cut -d',' -f2) && minimap2 --sam-hit-only -t 1 -a -x sr ref/NC_045512.2.fas.mmi <(wget -qO- "$url1") <(wget -qO- "$url2") 2> "bam/$crr.01.sorted.untrimmed.bam.log" | samtools sort --threads 1 -o "bam/$crr.01.sorted.untrimmed.bam" ; done
```

The resulting BAM files can be found in the [`data/bam`](data/bam) folder.

## 1.3: Merging BAMs
As can be seen in [Table: BioSamples](#table-biosamples), some BioSamples have multiple FASTQ pairs (and thus BAMs). However, for any downstream analyses, I wanted to merge all of the BAMs corresponding to a single BioSample into a single BAM file. The [`samtools merge`](http://www.htslib.org/doc/samtools-merge.html) command merges multiple sorted BAMs into a single sorted output BAM.

```bash
samtools merge -o OUTPUT.BAM INPUT1.BAM INPUT2.BAM ...
```

The resulting merged BAM files can be found in the [`data/merged_bam`](data/merged_bam) folder.

**Note:** A [preprint](https://doi.org/10.5281/zenodo.6672912) was released in June 2022 in which the authors called consensus sequences (and performed downstream analyses on the consensus sequences, e.g. phylogenetic inference, tree dating) using the **untrimmed** BAMs from this repo. This is a technical Bioinformatics mistake: reads need to be **trimmed** in order to remove low-quality bases (which we will do in [Step 2](#2-trimming-bams--sorting-trimmed-bams)) ***prior*** to any downstream analyses. Trimming is an important Quality Control (QC) step in any sequence data analysis, something [I explained to the authors](https://github.com/niemasd/PRJCA008874-Analysis/issues/1#issuecomment-1152525690). If you want to learn more about read trimming and why QC is so important in sequence data analysis, [this Galaxy tutorial](https://training.galaxyproject.org/training-material/topics/sequence-analysis/tutorials/quality-control/tutorial.html) is an excellent resource. [This Data Carpentry tutorial about assessing read quality](https://datacarpentry.org/wrangling-genomics/02-quality-control/index.html) as well as [this subsequent tutorial about trimming and filtering](https://datacarpentry.org/wrangling-genomics/03-trimming/index.html) are also excellent resources.

# 2: Trimming BAMs + Sorting Trimmed BAMs
I'm using [iVar v1.3.1](https://github.com/andersen-lab/ivar/releases/tag/v1.3.1) to quality trim the mapped reads, and I'm using [samtools v1.14](https://github.com/samtools/samtools/releases/tag/1.14) to sort the trimmed BAMs.

```bash
ivar trim -e -i SORTED_UNTRIMMED.BAM -p UNSORTED_TRIMMED_PREFIX
samtools sort --threads 1 -o SORTED_TRIMMED.BAM UNSORTED_TRIMMED.BAM
```
* `-e` means "include reads without primers" (we're not trimming primers, as there were no primers to trim)

The resulting trimmed BAM files can be found in the [`data/trimmed_bam`](data/trimmed_bam) folder.

# 3: Calculating Coverage + Stats
I'm using [SamBamViz v0.0.4](https://github.com/niemasd/SamBamViz/releases/tag/0.0.4) to compute various statistics and produce various visualizations from the trimmed BAMs. I'm using a minimum base quality score of 20 (`-q 20`) to match standard consensus calling approaches such as iVar Consensus.

```bash
SamBamViz.py -i TRIMMED_SORTED.BAM -o OUT_DIR -q 20 --ylog
```

The resulting SamBamViz output files can be found in the [`data/sambamviz`](data/sambamviz) folder.

# 4: Creating Pile-Ups
I'm using [samtools v1.14](https://github.com/samtools/samtools/releases/tag/1.14) to create pile-up files from the trimmed BAMs. Because iVar Variants and Consensus read the pile-up from standard input anyways, I gzip the pile-up files to save space.

```bash
samtools mpileup -B -A -aa -d 0 -Q 0 --reference REF_GENOME.FASTA TRIMMED_SORTED.BAM | gzip -9 > PILEUP.TXT.GZ
```
* `-B` means "disable BAQ (per-base alignment quality)"
* `-A` means "count orphans (do not discount anomalous read pairs)"
* `-aa` means "output absolutely all positions, including unused reference sequences"
* `-d 0` means "don't cap the per-file depth"
* `-Q 0` means "skip bases with less than 0 base quality (i.e., don't skip any bases based on base quality)"

The resulting pile-up files can be found in the [`data/pileup`](data/pileup) folder.

# 5: Calling Variants
I'm using [iVar v1.3.1](https://github.com/andersen-lab/ivar/releases/tag/v1.3.1) to call variants.

```bash
zcat PILEUP.TXT.GZ | ivar variants -m 10 -r REF_GENOME.FASTA -g REF_GENOME.GFF -p VARIANTS.TSV
```
* `-m 10` means "minimum read depth to call a variant = 10 reads"

The resulting variant TSV files can be found in the [`data/variants`](data/variants) folder.

# 6: Calling Consensus Sequences
I'm using [iVar v1.3.1](https://github.com/andersen-lab/ivar/releases/tag/v1.3.1) to call consensus sequences.

```bash
zcat PILEUP.TXT.GZ | ivar consensus -m 10 -n N -t 0.5 -p OUT_PREFIX
```
* `-m 10` means "minimum read depth to call a base in the consensus sequence = 10 reads"
* `-t 0.5` means "a single base must show up in at least 50% of the reads covering a given position to show up in the consensus"
* `-n N` means "use the letter `N` to denote ambiguous positions (i.e., positions in which we were unable to call a base)"
  * To clarify, a position in the consensus sequence can be `N` if (1) it had a coverage of less than 10, or (2) it had a coverage of greater than 10 but none of the 4 possible bases had a frequency greater than or equal to 0.5

The resulting consensus sequences can be found in the [`data/consensus`](data/consensus) folder.

# Miscellaneous Comments
## Low Coverage After Trimming
As mentioned at the beginning of this document, this analysis was conducted using the [C-VIEW](https://github.com/ucsd-ccbb/C-VIEW) pipeline developed for UC San Diego's Return to Learn program, which uses [iVar Trim](https://andersen-lab.github.io/ivar/html/manualpage.html) to perform trimming. If you suspect that iVar Trim might be trimming the reads too aggressively, rather than skipping quality trimming entirely (which is objectively a bad idea), I would recommend trying a different read trimmer.

One popular option is [fastp](https://github.com/OpenGene/fastp). Note that fastp (and many other read trimmers) trim FASTQ files *before* read mapping (whereas iVar Trim trims BAM files *after* read mapping). As such, if you want to try out a read trimmer that trims FASTQ files (rather than BAM files), you will need to convert the [merged untrimmed BAM files](data/merged_bam) back into FASTQ files, e.g. using [`bamtofastq`](https://bedtools.readthedocs.io/en/latest/content/tools/bamtofastq.html). The FASTQ files you will get from using `bamtofastq` on the merged untrimmed BAM files will be much smaller than the [original FASTQ files](https://download.cncb.ac.cn/gsa/CRA006587) because the converted FASTQ files will only contain mapped reads (because the BAM files only contain mapped reads).

After you have converted the untrimmed BAM files into FASTQ files and then trimmed the FASTQ files using fastp (or whichever read trimmer you choose), you will need to remap the trimmed FASTQ files to the reference genome (as described in [Step 1](#1-mapping-reads--sorting-bam); this should be quite fast), which will result in trimmed BAM files. You will then be able to pick up the rest of the analysis starting at [Step 3](#3-calculating-coverage--stats).
