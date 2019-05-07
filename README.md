
# FIREVAT

<!--[![Build Status](https://travis-ci.org/klugjo/hexo-autolinker.svg?branch=master)](https://travis-ci.org/klugjo/hexo-autolinker)-->
[![](https://www.r-pkg.org/badges/version/badger?color=green)](https://cran.r-project.org/package=FIREVAT)
[![](http://cranlogs.r-pkg.org/badges/grand-total/badger?color=green)](https://cran.r-project.org/package=FIREVAT)
[![GPLv2 license](https://img.shields.io/badge/License-GPLv2-blue.svg)](http://perso.crans.org/besson/LICENSE.html)

```FIREVAT``` (**FI**nding **RE**liable **V**ariants without **A**r**T**ifacts) is an R package that performs variant refinement on cancer sequencing data. ```FIREVAT``` uses mutational signatures to identify sequencing artifacts and low-quality variants.

<p float="left">
  <img src="FIREVAT_Workflow_Figure.png" width="100%"/>
</p>

## Getting started

### Installation

You can install the released version of ```FIREVAT``` from CRAN:

```r
install.packages("FIREVAT")
```

You can also install the developmental version of ```FIREVAT``` from github:

```r
install.packages("devtools")
library(devtools)
install_github("cgab-ncc/FIREVAT")
```

### Usage

```FIREVAT``` accepts a Variant Call Format (VCF) file as the primary input. It also requires a configuration file that corresponds to the attributes found in the VCF file. The variant refinement is then performed by running the following code example:

```r
library(FIREVAT)

# Output directory
output.dir <- "" # assign this path

# VCF file
sample.vcf.file <- system.file("extdata", "DCC_PCAWG_Cell_Lines_HCC1954.vcf", package = "FIREVAT")

# Configuration file
config.file <- system.file("config", "PCAWG_DKFZ_Cell_Line_Filtering_Params.json", package = "FIREVAT")

# Run FIREVAT
results <- RunFIREVAT(vcf.file = sample.vcf.file,
                      vcf.file.genome = 'hg19',
                      config.file = config.file,
                      df.ref.mut.sigs = GetPCAWGMutSigs(),
                      target.mut.sigs = GetPCAWGMutSigsNames(),
                      sequencing.artifact.mut.sigs = PCAWG.All.Sequencing.Artifact.Signatures,
                      output.dir = output.dir,
                      objective.fn = Default.Obj.Fn,
                      num.cores = 2,
                      ga.pop.size = 100,
                      ga.max.iter = 5,
                      ga.run = 5,
                      perform.strand.bias.analysis = TRUE,
                      ref.forward.strand.var = "TumorDPRefForward",
                      ref.reverse.strand.var = "TumorDPRefReverse",
                      alt.forward.strand.var = "TumorDPAltForward",
                      alt.reverse.strand.var = "TumorDPAltReverse",
                      annotate = FALSE)
```

Running the code above will generate FIREVAT outputs, including ```HTML``` report, ```refined.vcf```, and ```artifact.vcf``` files:


For your convenience, we have prepared configuration files for popularly used variant callers:
```r
# MuTect2
mutect2.config.file <- system.file("config", "MuTect2_Filtering_Params.json", package = "FIREVAT")

# Muse
muse.config.file <- system.file("config", "Muse_Filtering_Params.json", package = "FIREVAT")

# SomaticSniper
somaticsniper.config.file <- system.file("config", "SomaticSniper_Filtering_Params.json", package = "FIREVAT")

# Varscan2
varscan2.config.file <- system.file("config", "Varscan2_Filtering_Params.json", package = "FIREVAT")
```

In [**Introduction to FIREVAT**](https://github.com/cgab-ncc/FIREVAT/tree/master/vignettes/firevat.html), you can find advanced examples and detailed tutorials on how to use ```FIREVAT```.

## Suggested workflow

Based on our validation studies, We suggest using ```FIREVAT``` in the following workflow:

<p float="left">
  <img src="FIREVAT_Suggested_Workflow.png" width="100%"/>
</p>

## Paper

[]()

## Authors
* Andy Jinseok Lee, Bioinformatics Analysis Team, National Cancer Center Korea.
* Hyunbin Kim, Bioinformatics Analysis Team, National Cancer Center Korea.

## Attributions

FIREVAT is developed and maintained by Andy Jinseok Lee (jinseok.lee@ncc.re.kr) and Hyunbin Kim (khb7840@ncc.re.kr).

## License
[GPL-2](https://github.com/cgab-ncc/FIREVAT/blob/master/LICENSE)

[mutalisk]: http://mutalisk.org/
[paper]: https://academic.oup.com/nar/article/46/W1/W102/5001159
