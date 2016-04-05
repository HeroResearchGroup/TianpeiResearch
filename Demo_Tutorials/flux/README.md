# Flux and HPC resources at U of M

## Overview
__Flux__ is a shared computing cluster used by students and research at U of M. Flux is managed by Advanced Research Computing - Technology Services (ARC-TS). For more information about Flux, refer to the [ARC-TS website](http://arc-ts.umich.edu/resources/compute-resources/).

## Logging In

In order to access Flux, you must first do the following:

1. Create a flux account [here](https://arc-ts.umich.edu/fluxform/)
and obtain an MToken
2. Require flux allocation. 

Once you've done both of these things, open a terminal window and
enter the following (replacing `uniqname` with your uniqname):

```
$ ssh uniqname@flux-login.arc-ts.umich.edu
```

If you use a Windows machine, you can use
[putty](http://www.putty.org/) to SSH into flux.

You'll be prompted for both an MToken code and a password when you log
in.

## FLUX Configuration
Before ordering for a flux allocation, see [Flux configuration](http://arc-ts.umich.edu/flux/flux-configuration/)

| Resources                     |  Configuration   |  Price  |
| ----------------------------- |:-------------:| -----:|
| Standard Memory Flux core     |  one compute core with 4GB RAM | $6.60 per core/month |
| Large Memory Flux      | about 25GB per core,  or 1TB in a 40-core node     |  $13.30 per core/month |
| Flux GPUs | FLUX has 40 NVIDIA K20x GPUs available      |    $60 per month |

## Submit a job via qsub
You can follow the [FLUX IN 10 EASY STEPS](http://arc-ts.umich.edu/flux/using-flux/flux-in-10-easy-steps/)

### PBS Jobs

In order to access the your flux account, you must first
request compute time by submitting a PBS script. We've included a PBS
template in the `pbs` directory that you can use to get started. Let's
take a look at a few important parts:

Here, you can replace `job_name` with whatever you want, like
`hero_groups`. Pick something descriptive!

```
#PBS -N job_name
```

Here, make sure to replace `uniqname` with your actual uniqname:

```
#PBS -M uniqname@umich.edu
```

This line specifies how much computing power you want. Make sure to
request a little more than you think you need (but not too much!). As
is, we are requesting 1 processor on 1 node (each node has 16
processors) and 2000 mb of RAM, for 1 hour. If your job ends before
time is up, nothing bad will happen. However, if time is up before
your job ends, you might lose the results of your computation. It's
therefore good practice to save intermediate snapshots of your results
when running long jobs.

```
#PBS -l nodes=1:ppn=1,mem=2000mb,walltime=01:00:00
```

At the end of the script, you can load the modules you need and run
whatever commands you want.

```
#  Load the modules you need
module load epd

#  Put your job commands here:
echo "Hello, world"
```

A note on modules: most of the Python libraries you need will be
loaded when you load the `epd` module. Other modules you might want
include `matlab`, `torch`, `caffe`. **If you can't find something you
need on flux, email hpc-support@umich.edu for help before trying to
install it yourself!** Most things you need are already installed, and
if not, ARC-TS might be able to install it for you.

Trying modifying `pbs_template.pbs` to make it load and run a python
script of your choosing, and save it as `myfirstpbs.pbs`. You can
submit the job to flux by entering the following:

```
$ qsub pbs/myfirstpbs.pbs
```

You'll receive an email when the job starts running, and an additional
email when it either aborts or completes.

### Interactive Jobs

Often, you'll want to test things out interactively before submitting
big jobs. You can spawn an interactive session on Flux by including
the `#PBS -I` flag in your PBS scripts. For convenience, we've
included a script that will launch an interactive session. To launch,
simply run the script (no need to qsub, the script will qsub itself):

```
$ ./interactive_flux.sh
```

Make sure to edit the file to include your own uniqname first.

**Do not do any big computations on the flux-login node!** You can use
  the login node to download files and edit source code. Use
  interactive sessions when you need to debug or play around with
  data. If you use too much computation time on the login nodes Flux
  will kick you off.


## Get files
In terminal (Linux or Mac), you can use `scp` method to get file. Note that the transfer node is different from the log-in node. 

```
% scp localfile uniqname@flux-xfer.arc-ts.umich.edu:remotefile (copy a file)
```
or
```
% scp -r localdir  uniqname@flux-xfer.arc-ts.umich.edu:remotedir    (copy an entire directory)
```

## Check your available module
Use `module` command to load software. 
```
module avail
module list
module load modulename    (eg module load R)
module unload modulename    (eg module unload R)
```
## Submit, Delete and Check jobs
Submitting your Job:
```
qsub filename.pbs    (eg qsub sample.pbs … outputs jobid on successful submission)
```

Checking the status of your Job:
```
For a single job: qstat jobid     OR  
checkjob  jobid   (just the numeric portion)
```

To see all of your jobs: `qstat -u uniqname`  OR `showq -w user=uniqname`

Deleting your job:
```
qdel  jobid
```

If a job doesn’t start in within 30 minutes, send an email with a copy of your PBS script and the job number to `flux-support@umich.edu`.  Do not delete the job.


## Get output
When your job is completed, you will receive an email from flux. Check if the job is done successfully. 