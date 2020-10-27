CANU was run in grid mode using SLURM system on GWU colonialone computational cluster.

```
READS=[fastq file]
PREFIX="Species_name"
GENOMESIZE=[estimated genome size (270m)]
OUTDIR=[path]

canu -p $PREFIX \
     -d $OUTDIR \
     genomeSize=$GENOMESIZE \
     useGrid=true \
     gridOptions="--partition=defq,tiny,short -t 08:00:00" \
     gridOptionsoea="--partition=defq -t 3-00:00:00" \
     gridOptionsovl="--partition=defq -t 3-00:00:00" \
     gridOptionsmhap="--partition=defq -t 3-00:00:00" \
     gridOptionsmmap="--partition=defq -t 3-00:00:00" \
     -nanopore-raw $READS > $OUTDIR/canu_out
```