---
layout: post
title: "Could not allocate metaspace using qualimap"
subtitle: "JAVA allocate metaspace"
author: "Jinfeng"
header-mask: 0.4
tags:
  - Linux
  - JAVA
  - qualimap
---

Running into problem when using qualimap to summary bam files. 

```

qualimap bamqc -bam test.bam --java-mem-size=2G -nt 1 -outformat PDF

JVM will be started with AWT in headless mode Creating JVM object Error occurred during initialization of VM Could not allocate metaspace: 1073741824 bytes

```

The error can be fixed by turning mem required from SGS, SLURM, PBS

```
echo "For SGE, use more mem than require by qualimap will fix the problem" 

#$ -l h_vmem=6g

```
