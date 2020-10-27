```
TARGET=[genome assembly .fasta file]
NAME=[string with run name]
OUTDIR=[path]
BUSCODIR=[path to default output]
CPUS=[# cpu]

db="diptera_odb9/"
run_BUSCO.py -i ${TARGET} -o ${NAME} -l ${db} -m genome -c $CPUS -f

mv ${BUSCODIR}/run_${NAME} ${OUTDIR}

NAME="arab7_chromosomes_mz"
db="metazoa_odb9/"

run_BUSCO.py -i ${TARGET} -o ${NAME} -l ${db} -m genome -c $CPUS

mv ${BUSCODIR}/run_${name} ${OUTDIR}
```