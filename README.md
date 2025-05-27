# showbf

Show backfill scheduling windows on a [slurm](https://slurm.schedmd.com/) cluster.
Requires [pyslurm](https://pyslurm.github.io).

cores, memory, gpus, reservations, and local disk (tmp) are tracked.

## showbf [-h] [-f|-v|-vv]
Show which resources are available and for how long. Users can use this to tweak their job requests and have the best chance of their job running "now". This is an instantaneous guestimate and doesn't include many factors (eg. numa, software licenses), but it's most of what slurm allows us to see.

eg.
```
% showbf
milan
   2 slots for 48-core jobs free (96 cores total) 
   1 slot  for 39-core jobs free (39 cores total) for 35:41:32             
   1 slot  for 37-core jobs free (37 cores total) 
   1 slot  for 36-core jobs free (36 cores total) (low memory jobs only)
   1 slot  for 34-core jobs free (34 cores total) 
   2 slots for 31-core jobs free (62 cores total) for 41:30:28 to 133:56:12 
                     ...
   5 slots for 2-core jobs free (10 cores total) for 42:00:12 to     Inf 
   4 slots for 1-core jobs free (4 cores total) for 17:23:45 to 117:56:28 
trevor
  18 nodes (12 core) free (216 cores total) for 15:23:45             
   1 slot  for 11-core jobs free (11 cores total) for 15:23:45             
```
The full list of backfill windows is available with -f.
There is much more detailed information available via the -v and -vv options.


## qinfo [-h] [-s|-v]
If invoked as `qinfo`, this codebase also provides information about available queues and resources.
eg.
```
% qinfo -v
QUEUE/                NODES                        CORES                      GPUS
PARTITION       A   I   O   B   T         A     I     O     B     T      A  I  O  B  T
--------------------------------------------------------------------------------------
milan         174   1   6   0 180     10050   807   304     7 10864         -
milan-gpu      11  10   1   0  22        68    83    16     0  1008     47 14  3  2 63
trevor          1  18   1   0  20         1   227    12     0   228         -

  A/I/O/B/T = Allocated/Idle/Offline/Blocked/Total
     Blocked resources are those that are idle but unavailable
     due to resource requests from other jobs.
```

A third mode is available if the code is invoked as `spart`. It's kinda a combination of both of the above. I like it, but it's pretty ugly and perhaps more useful to admins than users.

## Installation
Edit the section at the top of the code to fill in your cluster details and limits you'd like to flag etc.

(c) 2019 Robin Humble. insert this github username @ gmail.com
