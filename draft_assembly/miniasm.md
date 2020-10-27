Miniasm assembler script

```
READS=[fastq file]
CPUs = [#cpu]

minimap2  -x ava-ont -t $CPUs $READS $READS > reads.paf.gz 
miniasm -f $READS reads.paf.gz > assembly.gfa

awk ’/^S/{print “>”$2”\n”$3}’ assembly.gfa > miniasm_assembly.fasta
```