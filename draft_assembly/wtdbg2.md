```
READS="fastq file"
PREFIX="Species_name"
GENOMESIZE=[estimated genome size (270m)]
CPUs=[# cpu]

# assemble long reads
wtdbg2 -x ont -g $GENOMESIZE -t $CPUs -i $READS -fo ${PREFIX}

# derive consensus
wtpoa-cns -t $CPUs -i ${PREFIX}.ctg.lay.gz -fo ${PREFIX}.wtdbg2_ctg.fasta
```