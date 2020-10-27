```
TARGET=[assembly .fasta]
OUTDIR=[path]
REFERENCE=[reference genome (Agamb PEST) .fasta file]
LABELS=[genome prefix labels]
CPUS=[# cpu]

quast.py -o ${OUTDIR} -r ${REFERENCE} --threads $CPUS \
         --labels ${LABELS} \
         --large -k -s\
         --eukaryote --fragmented ${TARGET}
```