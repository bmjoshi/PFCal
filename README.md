# PFCal: standalone simulation studies

[Twiki with the Instructions](https://twiki.cern.ch/twiki/bin/view/CMS/HGCALSimulationAndPerformance)
[HGCAL Documentation](https://hgcaldocs.web.cern.ch/)

# Instructions for generating samples

```
cmsrel CMSSW_12_4_9
cd CMSSW_12_4_9/src
git clone git@github.com:bmjoshi/PFCal.git
cd PFCal/PFCalEE
```
**Do Not** run `cmsenv` command. Instead, build the code using the following command:
```
source g4env.sh
mkdir -p userlib/{lib,obj,bin} && cd userlib && make dictionary && make -j 5 && cd - && ./makeG4
```
The to generate the jobs and submit production use the `submitProd.py` script.
```
usage: submitProd.py [-h] [-t GITTAG] [--nRuns NRUNS] [-v VERSION] [-m MODEL]
                     [-a ETAS [ETAS ...]] [-p PHI] [--shape SHAPE] [-b BFIELD]
                     [-d DATATYPE] [-f DATAFILE] [-F DATAFILEEOS] [-n NEVTS]
                     [-o OUT] [-e EOS] [-g] [--enList ENLIST [ENLIST ...]]
                     [-S]

optional arguments:
  -h, --help            show this help message and exit
  -t GITTAG, --git-tag GITTAG
                        git tag version (default: )
  --nRuns NRUNS         number of run, 0-indexed (default: -1)
  -v VERSION, --version VERSION
                        detector version (default: 3)
  -m MODEL, --model MODEL
                        detector model (default: 3)
  -a ETAS [ETAS ...], --etas ETAS [ETAS ...]
                        incidence eta (default: None)
  -p PHI, --phi PHI     incidence phi angle in pi unit (default: 0.5)
  --shape SHAPE         shape (default: 1)
  -b BFIELD, --Bfield BFIELD
                        B field value in Tesla (default: 0)
  -d DATATYPE, --datatype DATATYPE
                        data type or particle to shoot (default: e-)
  -f DATAFILE, --datafile DATAFILE
                        full path to HepMC input file (default: )
  -F DATAFILEEOS, --datafileeos DATAFILEEOS
                        EOS path to HepMC input file (default: )
  -n NEVTS, --nevts NEVTS
                        number of events to generate (default: 1000)
  -o OUT, --out OUT     output directory (default: $PWD)
  -e EOS, --eosOut EOS  eos path to save root file to EOS (default: )
  -g, --gun             use particle gun. (default: False)
  --enList ENLIST [ENLIST ...]
                        E_T list to use with gun (default: [5, 10, 20, 30, 40,
                        60, 80, 100, 150, 200])
  -S, --no-submit       Do not submit batch job. (default: False)
```

Use `piProd.sh` script for submit multiple production job submission.
