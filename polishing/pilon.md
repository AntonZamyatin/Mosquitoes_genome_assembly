```
TARGET=[draft assembly .fasta file]
READS1=[forward Illumina reads .fastq file]
READS2=[reverse Illumina reads .fastq file]
OUTFOLDER=[path]
ILL_FOLDER=[Illumina data dir]
CPUS=[# cpu]

bwa index ${TARGET}

for SRR in SRR314645 SRR314650 SRR314652 SRR529989 SRR529992 SRR529994 SRR529995 
do
	bwa mem -t $CPUS ${TARGET}  ${ILL_FOLDER}/${SRR}_1_filtered.fastq ${ILL_FOLDER}/${SRR}_2_filtered.fastq  |  \
	samtools view - -Sb | \
	samtools sort - -@$CPUS -o ${OUTFOLDER}${SRR}_ill_aln.bam
done

# or

bwa mem ${TARGET} ${READS1} ${READS2} -t $CPUS | \
samtools view -bS > ${OUTFOLDER}aln.bam

cd ${OUTFOLDER}
samtools merge  -@ $CPUS Merged.bam SRR314645_ill_aln.bam \
	SRR314650_ill_aln.bam SRR314652_ill_aln.bam SRR529989_ill_aln.bam \
	SRR529992_ill_aln.bam SRR529994_ill_aln.bam SRR529995_ill_aln.bam 

samtools sort Merged.bam -o Merged_sorted.bam
samtools index Merged_sorted.bam

pilon -Xmx160048m --genome ${TARGET} --frags Merged_sorted.bam --outdir ${OUTFOLDER} \
	--diploid --threads $CPUS
```