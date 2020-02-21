---
layout: post
title: "HPC SGE command"
subtitle: "Use SEG cluster
author: "Jinfeng"
header-mask: 0.4
tags:
  - Linux
  - HPC
---

## A example shell script to run speedseq with SGE

```
#!/bin/sh
#$ -pe smp 8
#$ -l h_vmem=10G
#$ -l h_rt=80:00:00
#$ -e run_speedseq_SGE.sh.$JOB_ID_$TASK_ID.error.txt
#$ -o run_speedseq_SGE.sh.$JOB_ID_$TASK_ID.output.txt
#$ -cwd

start=`date +%s`

CPU=$NSLOTS
if [ ! $CPU ]; then
   CPU=2
fi

N=$SGE_TASK_ID
if [ ! $N ]; then
    N=$1
fi

echo "$CPU"
echo "$N"

export PATH=$PATH:~/Software/Speedseq/speedseq/bin
export PYTHONPATH=~/Software/conda/miniconda3/envs/Speedseq/lib/python2.7/site-packages:
export PERL5LIB=~/Software/conda/miniconda3/envs/Speedseq/lib/site_perl/5.26.2

FILE=`ls *_1.fq.gz | grep _1\.fq\.gz | head -n $N | tail -n 1`
R1=$FILE
R2=`echo $R1 | perl -p -e 's/_1\.fq/_2.fq/'`
SAMPLE=${FILE%_1.fq.gz}
#R1=Clean_100B_1.test.fq
#R2=Clean_100B_2.test.fq
echo "File: $FILE"
echo "Read: $R1 and $R2"
echo "Sample: $SAMPLE"
speedseq=~/Software/Speedseq/speedseq/bin/speedseq
genome=genome.fasta
if [ ! -e $SAMPLE\.bam ] && true ; then
echo "mapping $SAMPLE ..."
$speedseq align \
     -t $CPU \
     -o $SAMPLE \
     -R "@RG\tID:id$SAMPLE\tSM:$SAMPLE\tLB:lib$SAMPLE" \
     -M 20 \
     -v \
     $genome \
     $R1 \
     $R2
fi

end=`date +%s`
runtime=$((end-start))

echo "Start: $start"
echo "End: $end"
echo "Run time: $runtime"


```
## Some command to monitor or control resource and SGE job

```
qhost -F will show the resources available for each node

```
