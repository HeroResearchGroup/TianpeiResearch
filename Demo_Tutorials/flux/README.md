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