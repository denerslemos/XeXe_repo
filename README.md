# XeXe analysis at 5.44 TeV

This repository was created to contain relevant information about the data processing (foresting) of XeXe at 5.44 TeV dataset collected by CMS in the special Run containing around 18.5 million events.

## Code structure and steps:

HiForest production -> Make the skims -> produce histograms -> run macros for plots

> HiForest
> > Setup for official HiForest setup. Intructions to add event plane informations are also included

> List_of_files
> > To make it easy and fast the skim production I already include the list of forest files for data and MC in this folder 

> Skim
> > Produce the skims using HiForest as input. We can use CRAB3 or HTCondor to production and is useful to reduce the size of files.

> Histo
> > C++ code using ROOT framework to produce the histograms for analysis: Jets, 2PC, HBT, ... . Mixing is done at this step.

> Macros
> > Codes using ROOT to produce the result plots, fits and so on for our analysis 

## Status:

1. HiForest production: Ongoing -> stored at T2_BR_SPRACE
   - Data
     - [ ] MB
       - [ ] XXXX

   - MC simulations: Ongoing -> stored at T2_BR_SPRACE
     - [ ] EPOS MB
         
     - [ ] HIJING MB
         - p-going: 
         - Pb-going:
         
     - [ ] AMPT MB
         - p-going: 
         - Pb-going:
         
     - [x] Pythia8 - Dijet - unembedded - EP information not included
       - [x] pthat > 15 GeV 
         - p-going:  /store/user/ddesouza/Dijet_pThat-15_pPb-Bst_8p16_Pythia8/New_HiForest_pPb_PYTHIA8_pthat15_p-going_out/220105_185751/0000
         - Pb-going: /store/user/ddesouza/Dijet_pThat-15_PbP-Bst_8p16_Pythia8/New_HiForest_pPb_PYTHIA8_pthat15_Pb-going_out/220105_190525/0000
   
     - [x] Pythia8  - Dijet - embedded (using EPOS) - EP information not included
       - [x] pthat > 15 GeV
         - p-going:  /store/user/ddesouza/Dijet_pThat-15_pPb-EmbEPOS_8p16_Pythia8/New_HiForest_pPb_PYTHIA8_EPOS_emb_pthat15_p-going_out/220106_053602/0000  

2. Skim production (it depends what you need. The example code are for jets and/or tracks)
   - [ ] MB data
   - [ ] EPOS MC
   - [ ] EPOS MC
   - [ ] EPOS MC

3. Histograms for observables (example code for jet studies)
   - [ ]

## Some advice for CMS users: 
### Add the following lines in your ~/.bashrc

Crab setup
```
source /cvmfs/cms.cern.ch/crab3/crab.sh
```

Useful for HTcondor jobs:
```
alias bigbird08='export _condor_SCHEDD_HOST="bigbird08.cern.ch" export _condor_CREDD_HOST="bigbird08.cern.ch"'
alias bigbird09='export _condor_SCHEDD_HOST="bigbird09.cern.ch" export _condor_CREDD_HOST="bigbird09.cern.ch"'
alias bigbird10='export _condor_SCHEDD_HOST="bigbird10.cern.ch" export _condor_CREDD_HOST="bigbird10.cern.ch"'
alias bigbird11='export _condor_SCHEDD_HOST="bigbird11.cern.ch" export _condor_CREDD_HOST="bigbird11.cern.ch"'
alias bigbird12='export _condor_SCHEDD_HOST="bigbird12.cern.ch" export _condor_CREDD_HOST="bigbird12.cern.ch"'
alias bigbird13='export _condor_SCHEDD_HOST="bigbird13.cern.ch" export _condor_CREDD_HOST="bigbird13.cern.ch"'
alias bigbird14='export _condor_SCHEDD_HOST="bigbird14.cern.ch" export _condor_CREDD_HOST="bigbird14.cern.ch"'
alias bigbird15='export _condor_SCHEDD_HOST="bigbird15.cern.ch" export _condor_CREDD_HOST="bigbird15.cern.ch"'
alias bigbird16='export _condor_SCHEDD_HOST="bigbird16.cern.ch" export _condor_CREDD_HOST="bigbird16.cern.ch"'
alias bigbird17='export _condor_SCHEDD_HOST="bigbird17.cern.ch" export _condor_CREDD_HOST="bigbird17.cern.ch"'
alias bigbird18='export _condor_SCHEDD_HOST="bigbird18.cern.ch" export _condor_CREDD_HOST="bigbird18.cern.ch"'
alias bigbird19='export _condor_SCHEDD_HOST="bigbird19.cern.ch" export _condor_CREDD_HOST="bigbird19.cern.ch"'

alias condstat='condor_status -schedd' 
```
### Useful CRAB3 commands
First import your voms using
```
voms-proxy-init -rfc -voms cms
```
In the crab configuration files included, the jobs are submitted using a python command (do not forget voms command)
```
python crabfile.py
```
To check status of your jobs, you can just use ```crab status -d workArea/requestName/```, where workArea and requestName are folders generated automatically based on the name included in your crab configuration file. Example: for (must be finalized today)
```
crab status -d workArea/requestName/
```

### Useful xrootd commands

To copy files for your local machine use xrdcp, example
```
xrdcp -d 1 -f root://cmsxrootd.fnal.gov//store/user/ddesouza/PAEGJet1/HiForest_pPb_8TeV_p-going_JetSamples_out/211211_161432/0000/HiForestAOD_1.root . &> out.txt &
```

To access files and create a list of files you can use xrdfs, example:
```
xrdfs root://cmsxrootd.fnal.gov ls /store/user/ddesouza/PAEGJet1/HiForest_pPb_8TeV_p-going_JetSamples_out/211211_161432/0000/ &> listofforestfiles.txt &
```
