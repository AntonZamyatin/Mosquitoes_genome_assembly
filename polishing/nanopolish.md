```
DRAFT=[path to draft assembly .fasta]
READS=[reads .fastq]
NAME=[prefix name]
CPUS=[# cpu]
OUTFOLDER=[path]
FAST5_FOLDER=[path to ONT raw signal]
SUMMARY=[ONT sequencing summary file]

#data preprocessing
nanopolish index -d ${FAST5_FOLDER} \
                ${READS} -s ${SUMMARY} --verbose

minimap2 -ax map-ont ${DRAFT} ${READS} -t $
{CPUS} | samtools sort \
           -o ${OUTFOLDER}${NAME}.sorted.bam -T ${OUTFOLDER}${NAME}.tmp
	   samtools index ${OUTFOLDER}${NAME}.sorted.bam

export HDF5_USE_FILE_LOCKING='FALSE'

python nanopolish_makerange.py ${DRAFT} | \
    parallel --results ${OUTFOLDER}nanopolish.results -P 40 \
    /groups/cbi/Users/azamyatin/nanopolish/nanopolish variants \
    --consensus -o ${OUTFOLDER}polished.{1}.vcf \
    -w {1} -r ${READS} \
    -b ${OUTFOLDER}${NAME}.sorted.bam -g ${DRAFT} \
    -t 1

nanopolish vcf2fasta -g ${DRAFT} ${OUTFOLDER}polished.*.vcf > ${OUTFOLDER}${NAME}_np.fa
```