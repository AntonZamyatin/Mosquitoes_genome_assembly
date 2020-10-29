###run Juicer
```

module load bwa 
module load jdk

./scripts/juicer.sh -S "early" -g arabiensis -s Arima \
-z arabiensis.fasta -y arabiensis_Arima.txt -p assembly \
-q defq -l defq -D [juicer directory] 
```
### run 3d-DNA
```
module load python3/3.7.2 
module load jdk
module load parallel

./run-asm-pipeline.sh arabiensis.fasta merged_nodups.txt 
```