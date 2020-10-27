We used fastQC for Illumina data quality control and multiQC for reports summarizing. These operations were done for both genomic short reads and Hi-C data.

```
READSDIR=[path]
OUTDIR=[path]
CPUs=[#cpu]

READS=find $READSDIR -name *.fastq
fastqc $READS --outdir $OUTDIR -t $CPUs

multiqc $OUTDIR
```