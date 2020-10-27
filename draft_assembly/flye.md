```
READS=[fastq file]
GENOMESIZE=[estimated genome size (270m)]
OUTDIR=[path]
CPUs = [#cpu]

flye --nano-raw $READS --genome-size $GENOMESIZE \
     --threads $CPUs --out-dir $OUTDIR
```