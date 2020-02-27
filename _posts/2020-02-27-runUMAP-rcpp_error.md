---
layout: post
title: "Fix runUMAP 'memory not mapped' errors"
subtitle: "r-rcppparallel bug for umap"
author: "Jinfeng"
header-mask: 0.4
tags:
  - Linux
  - Seurat
  - scRNA
  - umap
---

Seurat or SingleR reports a bug when using runUMAP: address 0xfffffffffffffff7, cause 'memory not mapped'
The way to fix this is to reinstall "r-rcppparallel" package in conda

```
# In your R env, remove "RcppParallel" first 
/PATH/envs/scRNA/bin/R
remove.packages('RcppParallel')

# Then, install "r-rcppparallel" with conda
conda install -n scRNA -c conda-forge r-rcppparallel
```
