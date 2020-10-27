We used fastP for Illumina data filtration

```
fastp -i SRR606146_1.fastq -I SRR606146_2.fastq -o SRR606146_1_filtered.fastq -O SRR606146_2_filtered.fastq -A -5 -3 -M 28 -w 36
```