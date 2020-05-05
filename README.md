# parallel-remote-rsync
Script to handle parallel data transfer from a remote server to a local host.

I have created this sript to easely download the results of my simulations from a remote cluster to my local machine.
Here, I use GNU Parallel (http://dx.doi.org/10.5281/zenodo.16303) to transfer data using multiple threads and rsync (http://rsync.samba.org/) to find files that need to be transferred, that is, files that have changed in size or in last-modified time.

Here I decided to go for a ssh to list the files to be downloaded, but it is also possible to run rsync using the --dry-run flag to see what files will be affected.

-----------------------

Supposing that the remote directory has the tree structure depicted below. The script will download the files creating automatically the same structure in your local machine. 
```
remote_dir
│    source_code01.f90
│    source_code02.f90
│         ...
│
└────folder1
│    │    result01.out
│    │    result02.out
│    │        ...
│    │    rstfile.001
│    │    rstfile.002
│    │        ...
│    |
│    └────subfolder1
│         │    data01.dat
│         │    data02.dat
│         │       ...
│   
└────folder2
     │    file021.txt
     │    file022.txt
```
Moreover, in my case, I used to have some files (named rstfile.\*) of which only the last N of them needed to be downloaded, where N is a user-defined parameter. This feature is also included in the script.
