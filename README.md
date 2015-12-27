# PANGEA.HIV.sim
HIV Phylogenetic Simulation Model for the PANGEA-HIV methods comparison exercise.

### Overview
The Phylogenetics And Networks for Generalised HIV Epidemics in Africa (PANGEA-HIV) consortium 
aims to provide viral sequence data from across sub-Saharan Africa, and to evaluate their viral 
phylogenetic relationship as a marker of recent HIV transmission events [9]. 

Research groups were invited to participate in a blinded methods comparison exercise on simulated 
HIV sequence data sets to test the performance of current phylogenetic methods before their application 
on real data. The methods comparison exercise was announced in October 2014, and closed in August 2015. 
Research groups were asked to estimate 
* reductions in HIV incidence during a typical community-based intervention in sub-Saharan Africa,
* the proportion of HIV transmissions arising from individuals during their first three months of infection (early transmission) at the start of the intervention from sequence data.

Secondary objective were to evaluate the merits of full genome sequence data, the 
impact of various aspects of sequence sampling, and the impact of the proportion of transmissions 
originating from outside the study area.

Generalised HIV-1 epidemics were simulated for a relatively small village population of ~8,000 
individuals and a larger regional population of ~80,000 individuals from two structurally different, agent-based 
epidemiological models. The regional simulation captures individual-level HIV transmission dynamics in a larger 
regional population that is broadly similar to a site (cluster) of the HPTN071/PopART HIV prevention trial in South 
Africa [Hayes]. 

This code repository contains the simulation code to generate sequence data and phylogenetic trees 
that correspond to epidemic scenarios under the regional model. 

### Authors of PANGEA.HIV.sim

* Oliver Ratmann <oliver.ratmann@imperial.ac.uk>
* Mike Pickles <m.pickles@imperial.ac.uk>
* Anne Cori <a.cori@imperial.ac.uk>
* Christophe Fraser <c.fraser@imperial.ac.uk>

# Installation

The simulation code ships as an `R` package and requires third party code before installation:

* GNU Scientific Library http://www.gnu.org/software/gsl/

After these dependencies are installed, type in `R`:

```r
library(devtools)
install_github("olli0601/PANGEA.HIV.sim")
```

# Using the package

`PANGEA.HIV.sim` contains just two functions, `sim.regional.args` and `sim.regional`. We now describe these briefly, and the various options in more detail below.
* `sim.regional.args`: Set all input arguments to the simulation. Returns a `data.table` with columns `stat` (name of input argument) and `v` (value of input argument).
* `sim.regional`: Create a UNIX shell script that can be called to generate a single simulation. Takes as input a directory name in which the simulations are to be created, and a `data.table` with all input arguments. Returns the file name to the shell script.

Fire up `R`, and type 

```r
library(PANGEA.HIV.sim)
?sim.regional
```

This will show a first example on how to use the simulation code, followed by code to simulate the PANGEA-HIV 
sequences data sets to address the primary objectives of the methods comparison exercise, and code to simulate 
the PANGEA-HIV tree data sets to address the secondary objectives of the methods comparison exercise.


# Output of the simulation

`PANGEA.HIV.sim` produces the following files:

*File name*         | *Description*
--------------------|--------------------
.fa                 | Fasta file of aligned, simulated sequences. One for each gene.
_metadata.csv       | Information on sampled individuals.
_SURVEY.csv         | Cross-sectional surveys conducted on a random subset of the simulated population.
_DATEDTREE.newick   | Trees in newick format. Each tree corresponds to the simulated viral phylogeny among sampled individuals of one simulated transmission chain. One tree per line.

Variables in the simulated cross-sectional surveys in file `_SURVEY.csv` are:

*Group variable*    | *Description*
--------------------|--------------------
YR                  | Time at which the survey was taken 
Gender              | Gender
AGE                 | Age

*Count by group*    | *Description*
--------------------|--------------------
ALIVE_N             | Number of sexually active individuals
ALIVE_AND_DIAG_N    | Number of diagnosed individuals
ALIVE_AND_ART_N     | Number of individuals that started ART 
ALIVE_AND_SEQ_N     | Number of individuals with a sequence

Variables of simulated individuals in file `_metadata.csv` are:
￼
*Variable*          | *Description*
--------------------|--------------------------------------------------------------------------------
IDPOP               | Identifier of individual that can be linked to sequences or tips in the viral phylogeny
GENDER              | Gender, NA if archival sequence
DOB                 | Date of birth, NA if archival sequence
DOD                 | Date of death, NA if alive at end of simulation
DIAG_T              | Time of diagnosis, NA if archival sequence
DIAG_CD4            | CD4 count at diagnosis, NA if archival sequence
￼￼ART1_T              | ART start date, NA if ART not started
ART1_CD4            | CD4 count at ART start, NA if ART not started
TIME_SEQ            | Date sequence taken
RECENT_TR           | Y if transmission occurred at most 6 months after diagnosis, N otherwise


x



