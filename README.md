# XeXe analyses at 5.44 TeV

# HiForest Setup

For  at 8.16 TeV the CMSSW version 9_4_1 must be used (based on https://twiki.cern.ch/twiki/bin/viewauth/CMS/HiForestSetup):
```
#VOMS
voms-proxy-init -rfc -voms cms
# Setup CMSSW version
export SCRAM_ARCH=slc7_amd64_gcc630
cmsrel CMSSW_9_4_1
cd CMSSW_9_4_1/src
cmsenv
git cms-merge-topic -u CmsHI:forest_CMSSW_9_4_1
git remote add cmshi git@github.com:CmsHI/cmssw.git
cd HeavyIonsAnalysis/JetAnalysis/python/jets
./makeJetSequences.sh
cd ../../../..
# Dener's changes
cp /afs/cern.ch/work/d/ddesouza/public/ForForest/TrackAnalyzer.cc $CMSSW_BASE/src/HeavyIonsAnalysis/TrackAnalysis/src/
# Now compile and test
scram build -j10
# Once tests are done, go to:
cd $CMSSW_BASE/src/HeavyIonsAnalysis/JetAnalysis/test/workstation
#for quick test go to quickcheck folder and run 
cd quickcheck
cmsRun runForestAOD_pPb_DATA_80X.py &> out.txt &
```
Each folder inside of ```workstation``` contain the crab configuration files to submit for different datasets. You do not need to change anything. Do not run for MC yet (will be updated soon).
To submit crab jobs you just need to use the following command (after the VOMS command):
```
python crab_file.py
```
The Forest root output files will be stored at SPRACE/Brazil.
