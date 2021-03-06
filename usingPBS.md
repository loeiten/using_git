# Portable Batch System (PBS)

Used to run jobs on clusters.

## TORQUE

TOURQUE is a fork of openPBS. Get the version on a cluster with
```
qstat --version
```

http://en.wikipedia.org/wiki/Portable_Batch_System

http://www.adaptivecomputing.com/products/open-source/torque/

Documentation:

http://docs.adaptivecomputing.com/ -> Archived Documentation

## Commonly used commands

 Command                                       | Result
-----------------------------------------------|--------------------------------------------------------|
`qsub myPBSScript`                             | Submits a job to the cluster
`qsub -W depend=afterok:pid myOtherPBSScript`  | Submits a job to the cluster after `pid` is done
`qstat`                                        | Prints jobs currently running on the cluster
`qstat -u username`                            | Prints the jobs submitted by `username`
`qstat -f pid`                                 | Displays full info of job with process id `pid`
`qstat -f pid | grep -i Job_name`              | Displays full job name for `pid` using `grep`
`qhold pid`                                    | Prevent job `pid` to run until released
`qrls pid`                                     | Releases job `pid` from a hold
`qdel pid`                                     | Delete the job with process id `pid`
``qdel `seq -f "%.0f" 512173 512175` ``        | Delete the jobs `512173`, `512174` and `512175`
`qdel all`                                     | Delete all jobs (your jobs if you are not admin)
`qstat -q`                                     | Shows available queues and their walltime-limit
`showq`                                        | Show the queue (works at least with `Maui` scheduler)

## Example script

```sh
#!/bin/sh 
### Three #'s denotes a comment, one # denotes a PBS command
### ====================================================================
### Job name 
#PBS -N name
### ====================================================================
### ====================================================================
### Number of nodes and processors per node
### For optimal run, should run so that whole machines are
### occupied
#PBS -l nodes=2:ppn=12
### ====================================================================
### ====================================================================
### Maximum wallclock time, format HOURS:MINUTES:SECONDS
#PBS -l walltime=50:00:00
### ====================================================================
### ====================================================================
### Queue name (depends on cluster)
# PBS -q workq
### ====================================================================
### ====================================================================
### Output
### PBS -o is the terminal output
### PBS -e is the error produced by the code
#PBS -o nameOfLogfile.log
#PBS -e nameOfErrorfile.err 
### ====================================================================
### ====================================================================
### Mail notification when job is done
#PBS -m e
### ====================================================================
### ====================================================================
### $PBS_O_WORKDIR enables writing in the folder you do qsub from
cd $PBS_O_WORKDIR
### Command you want to run on the cluster, for example
mpirun -np 16 myCommand
exit
### ====================================================================
```

## Maui cluster scheduler

http://en.wikipedia.org/wiki/Maui_Cluster_Scheduler

Documentation:

http://docs.adaptivecomputing.com/maui/pdf/mauiadmin.pdf

## Links

https://www.osc.edu/supercomputing/batch-processing-at-osc/monitoring-and-managing-your-job
