```
READS=[ONT reads fastq file]
DB=[database name]
OUTFILE=[path for Kraken2 out]
CPUs=[# cpu]

export KRAKEN2_NUM_THREADS=$CPUs

kraken2 --db $DB ${READS} --output ${OUTFILE}
```
