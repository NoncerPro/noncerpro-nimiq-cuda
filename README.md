# Nimiq GPU miner for Nvidia graphic cards.

This is the first Nimiq GPU miner that utilizes the standard Nano mining protocol and is compatible with all of the available nimiq pools.

### Download 

releases: https://github.com/NoncerPro/noncerpro-nimiq-cuda/releases

Donation addresses
-------------------

Please consider supporting this project by donating to these addresses (EhssanD):

	  BTC  : 15h2QmsRwwwEdNNC6HbYHJU9mpbLrjUdDK

      NIM  : NQ52 7TL5 RA6B SSAS FULC P3SR D88B X2CK 0VTX


Options
------------------------------------------
```
  -a, --address    Nimiq wallet address                      [string] [required]
  -s, --server     Pool server address
                   Default: us.nimpool.io                               [string]
  -p, --port       Pool server port
                   Default: 8444                                        [number]
  -d, --devices    Active GPUs
                   Example: -d=0 1 3
                   Default: All available GPUs                           [array]
  -t, --threads    Number of threads per GPU
                   Example: -t=2 or -t=2 2 4
                   Default: 1                                            [array]
  -b, --batchsize  batchsize per thread.
                   Example: -b=100 or -b=100 120 200
                   Default: auto based on available device memory        [array]
  -h, --help       Show help                                           [boolean]
  -v, --version    Show version number                                 [boolean]
```

Config file
------------------------------------------
In addition to the above command line options, there is a miner.conf file which has the exact same options. If you uncomment any config option, it will be used as the default value for that option in the next run. Config options can still be overridden by command line options.


Requirements
------------------------------------------
Binary packages have been built with **CUDA 10.0**. You need to update your driver to the latest version in order to use them.

The minimum supported Compute Capability is SM3.5. You can check your cards' SM support in the following link:
https://developer.nvidia.com/cuda-gpus

If you are using Windows, the minimum virtual memory must be set to the total amount of allocated gpu memory. So if you have 6 x 1080 tis and want to use 8GB on each card, you will need 48 GB of virtual memory. This only applies to Windows.

If you are running the noncerpro.exe file directly, make sure you have set UV_THREADPOOL_SIZE to atleast 32;

Usage
------------------------------------------
Download the binary packge for Windows/Linux, edit mine.bat/mine.sh file and insert your own wallet address and run it.

You can control the amount of memory allocation per thread by using --batchsize option. Here is how it works:

    Allocated memory per thread = batchsize * 100 * 512 KB. For example batchsize 200 will try to allocate about 10 GB of memory.

Notice that this allocation is per thread, so if you have more than one thread you must adjust the batchsize accordingly.
    
    
Best settings
------------------------------------------
The default values are pretty good but for the best performance try different values for --threads and --batchsize options. Here are my best parameters for 1080 ti on Linux and Windows:
    
    Linux: --threads=4 --batchsize=50
    Windows: --threads=2 --batchsize=92

Overclocking
------------------------------------------
Argon2d is highly dependent on memory bandwidth and memory clock. Try settings the memory clock as high as possible, usually around +1000. Other parameters must be adjusted based on the specific card and OS.

Happy mining!
