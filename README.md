Data files
----------

This repository "contains" 
- `inputs/` directory with sample data to be used in the gears tests
- `gears/**/tests/TESTNAME/` directories with target data files

Those data files are not committed directly to git but managed by
[git-annex](http://git-annex.branchable.com/), while actual files reside in one
of the clones of this repository on one of my (@yarikoptic) http servers.  To
get access to those files, you would need to either

- run `git annex enableremote washoe-http` in your local clone
- run `git annex get .` to get all data files or just `git annex get inputs`
  if you are interested only in the input files

or

- use [datalad](http://datalad.org) would enable that remote automagically
  upon installation of this repository/dataset.  So the command

       datalad install -g https://github.com/yarikoptic/gearificated-nipype

  would not only clone this repository but also download all current versions of
  the input/output data files.
