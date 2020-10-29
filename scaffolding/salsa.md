### Assebly scaffolding with SALSA2

```
ASSEMBLY=[polished assembly .fasta file]
ASSEMBLY_idx=[assebly index .fasta.fai file]
ALIGNMENT=[Hi-C reads to assembly BWA alignment.bed file]
RESTR_ENZIME='GATC,GANTC' # restriction sites
OUT_FOLDER='scaffolds'
ASSEMBLY_GRAPH=[canu assembly graph .gfa file]

# module load glibc/2.14

python SALSA/run_pipeline.py \
    -a ${ASSEMBLY} -l ${ASSEMBLY_idx} \
    -b ${ALIGNMENT} -e ${RESTR_ENZIME} \
    -o ${OUT_FOLDER} -m yes -g ${ASSEMBLY_GRAPH}
```

### .hic matrix creation

```
JUICER_JAR=[path to juicer_tools .jar file]
SALSA_OUT_DIR=[path]
SCRIPT_PATH=.

samtools faidx ${SALSA_OUT_DIR}/scaffolds_FINAL.fasta

cut -f 1,2 ${SALSA_OUT_DIR}/scaffolds_FINAL.fasta.fai > ${SALSA_OUT_DIR}/chromosome_sizes.tsv

python ${SCRIPT_PATH}/alignments2txt.py -b ${SALSA_OUT_DIR}/alignment_iteration_1.bed  -a ${SALSA_OUT_DIR}/scaffolds_FINAL.agp -l ${SALSA_OUT_DIR}/scaffold_length_iteration_1 > ${SALSA_OUT_DIR}/alignments.txt

awk '{if ($2 > $6) {print $1"\t"$6"\t"$7"\t"$8"\t"$5"\t"$2"\t"$3"\t"$4} else {print}}'  ${SALSA_OUT_DIR}/alignments.txt | sort -k2,2d -k6,6d -T $PWD --parallel=16 | awk 'NF'  > ${SALSA_OUT_DIR}/alignments_sorted.txt

java -jar ${JUICER_JAR} pre ${SALSA_OUT_DIR}/alignments_sorted.txt ${SALSA_OUT_DIR}/salsa_scaffolds.hic ${SALSA_OUT_DIR}/chromosome_sizes.tsv

```