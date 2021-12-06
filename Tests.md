# Test 1
## CMD
Writing 150m of sequential data: `fio --name=seq_write --ioengine=posixaio --rw=write --bs=1m --size=150m --numjobs=1 --iodepth=1 --runtime=60 --output=/home/seq_write.json --output-format=json --time_based --end_fsync=1`
## Output
```
fio --name=write --ioengine=posixaio --rw=write --bs=1m --size=150m --numjobs=1 --iodepth=1 --runtime=30 --time_based --end_fsync=1
write: (g=0): rw=write, bs=(R) 1024KiB-1024KiB, (W) 1024KiB-1024KiB, (T) 1024KiB-1024KiB, ioengine=posixaio, iodepth=1
fio-3.28
Starting 1 process
write: Laying out IO file (1 file / 150MiB)
Jobs: 1 (f=1): [F(1)][100.0%][eta 00m:00s]                       
write: (groupid=0, jobs=1): err= 0: pid=39: Sun Dec  5 00:54:06 2021
  write: IOPS=7, BW=8058KiB/s (8251kB/s)(321MiB/40792msec); 0 zone resets
    slat (usec): min=33, max=30402, avg=167.51, stdev=1694.50
    clat (usec): min=202, max=9122.6k, avg=95395.12, stdev=755934.90
     lat (usec): min=246, max=9122.7k, avg=95562.63, stdev=755945.49
    clat percentiles (usec):
     |  1.00th=[    221],  5.00th=[    235], 10.00th=[    245],
     | 20.00th=[    260], 30.00th=[    273], 40.00th=[    306],
     | 50.00th=[    343], 60.00th=[    383], 70.00th=[    408],
     | 80.00th=[    437], 90.00th=[    474], 95.00th=[    570],
     | 99.00th=[4395631], 99.50th=[6677332], 99.90th=[9059697],
     | 99.95th=[9059697], 99.99th=[9059697]
   bw (  KiB/s): min= 8192, max=307200, per=100.00%, avg=81920.00, stdev=105750.71, samples=8
   iops        : min=    8, max=  300, avg=80.00, stdev=103.27, samples=8
  lat (usec)   : 250=14.95%, 500=79.44%, 750=0.62%
  lat (msec)   : 10=0.93%, 20=1.25%, 250=0.62%, 1000=0.62%, >=2000=1.56%
  cpu          : usr=0.01%, sys=0.15%, ctx=626, majf=0, minf=343
  IO depths    : 1=100.3%, 2=0.0%, 4=0.0%, 8=0.0%, 16=0.0%, 32=0.0%, >=64=0.0%
     submit    : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     complete  : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     issued rwts: total=0,321,0,0 short=0,0,0,0 dropped=0,0,0,0
     latency   : target=0, window=0, percentile=100.00%, depth=1

Run status group 0 (all jobs):
  WRITE: bw=8058KiB/s (8251kB/s), 8058KiB/s-8058KiB/s (8251kB/s-8251kB/s), io=321MiB (337MB), run=40792-40792msec
```

# Random Write
## CMD
Writing 150m of random: `fio --name=randwrite --ioengine=posixaio --rw=randwrite --bs=1m --size=150m --numjobs=1 --iodepth=1 --runtime=60 --output=/home/rand_write.json --output-format=json --time_based --end_fsync=1`
## Output
```
fio --name=randwrite --ioengine=posixaio --rw=randwrite --bs=1m --size=150m --numjobs=1 --iodepth=1 --runtime=30 --time_based --end
_fsync=1
randwrite: (g=0): rw=randwrite, bs=(R) 1024KiB-1024KiB, (W) 1024KiB-1024KiB, (T) 1024KiB-1024KiB, ioengine=posixaio, iodepth=1
fio-3.28
Starting 1 process
randwrite: Laying out IO file (1 file / 150MiB)
Jobs: 1 (f=1): [F(1)][100.0%][w=1025KiB/s][w=1 IOPS][eta 00m:00s]
randwrite: (groupid=0, jobs=1): err= 0: pid=92729: Sun Dec  5 00:57:40 2021
  write: IOPS=4, BW=4560KiB/s (4669kB/s)(157MiB/35258msec); 0 zone resets
    slat (usec): min=34, max=1048, avg=66.23, stdev=80.21
    clat (usec): min=234, max=27048k, avg=216163.46, stdev=2222607.31
     lat (usec): min=296, max=27048k, avg=216229.69, stdev=2222615.88
    clat percentiles (usec):
     |  1.00th=[     255],  5.00th=[     318], 10.00th=[     334],
     | 20.00th=[     347], 30.00th=[     359], 40.00th=[     383],
     | 50.00th=[     408], 60.00th=[     424], 70.00th=[     445],
     | 80.00th=[     469], 90.00th=[     494], 95.00th=[     545],
     | 99.00th=[ 6811550], 99.50th=[17112761], 99.90th=[17112761],
     | 99.95th=[17112761], 99.99th=[17112761]
   bw (  KiB/s): min=12288, max=307200, per=100.00%, avg=159744.00, stdev=208534.28, samples=2
   iops        : min=   12, max=  300, avg=156.00, stdev=203.65, samples=2
  lat (usec)   : 250=0.64%, 500=90.45%, 750=6.37%
  lat (msec)   : 10=0.64%, 20=0.64%, >=2000=1.27%
  cpu          : usr=0.02%, sys=0.08%, ctx=300, majf=0, minf=175
  IO depths    : 1=100.6%, 2=0.0%, 4=0.0%, 8=0.0%, 16=0.0%, 32=0.0%, >=64=0.0%
     submit    : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     complete  : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     issued rwts: total=0,157,0,0 short=0,0,0,0 dropped=0,0,0,0
     latency   : target=0, window=0, percentile=100.00%, depth=1

Run status group 0 (all jobs):
  WRITE: bw=4560KiB/s (4669kB/s), 4560KiB/s-4560KiB/s (4669kB/s-4669kB/s), io=157MiB (165MB), run=35258-35258msec
```
 

# Sequential Read
## CMD
Reading 150m of sequential data: `fio --name=read --ioengine=posixaio --rw=read --bs=1m --size=150m --numjobs=1 --iodepth=1 --runtime=60 --output-format=json --output=/home/seq_read.json --time_based --end_fsync=1`
## Output
```
fio --name=read --ioengine=posixaio --rw=read --bs=1m --size=150m --numjobs=1 --iodepth=1 --runtime=30 --time_based --end_fsync=1
read: (g=0): rw=read, bs=(R) 1024KiB-1024KiB, (W) 1024KiB-1024KiB, (T) 1024KiB-1024KiB, ioengine=posixaio, iodepth=1
fio-3.28
Starting 1 process
read: Laying out IO file (1 file / 150MiB)
Jobs: 1 (f=1): [R(1)][100.0%][r=1648MiB/s][r=1647 IOPS][eta 00m:00s]
read: (groupid=0, jobs=1): err= 0: pid=46585: Sun Dec  5 00:55:51 2021
  read: IOPS=1537, BW=1538MiB/s (1612MB/s)(45.0GiB/30002msec)
    slat (usec): min=10, max=37517, avg=61.60, stdev=593.67
    clat (nsec): min=720, max=380324k, avg=513579.55, stdev=3773191.61
     lat (usec): min=71, max=380359, avg=575.17, stdev=3820.10
    clat percentiles (usec):
     |  1.00th=[    88],  5.00th=[   106], 10.00th=[   116], 20.00th=[   128],
     | 30.00th=[   139], 40.00th=[   149], 50.00th=[   161], 60.00th=[   174],
     | 70.00th=[   188], 80.00th=[   210], 90.00th=[   269], 95.00th=[  3326],
     | 99.00th=[  5604], 99.50th=[  6063], 99.90th=[  7177], 99.95th=[  8225],
     | 99.99th=[212861]
   bw (  MiB/s): min=   32, max= 1840, per=99.98%, avg=1537.15, stdev=509.31, samples=59
   iops        : min=   32, max= 1840, avg=1537.15, stdev=509.31, samples=59
  lat (nsec)   : 750=0.01%, 1000=0.01%
  lat (usec)   : 2=0.02%, 4=0.01%, 20=0.01%, 50=0.01%, 100=2.98%
  lat (usec)   : 250=85.43%, 500=3.43%, 750=0.05%, 1000=0.11%
  lat (msec)   : 2=1.11%, 4=2.86%, 10=3.94%, 20=0.01%, 50=0.01%
  lat (msec)   : 100=0.01%, 250=0.02%, 500=0.01%
  cpu          : usr=1.33%, sys=16.34%, ctx=77097, majf=0, minf=46148
  IO depths    : 1=100.0%, 2=0.0%, 4=0.0%, 8=0.0%, 16=0.0%, 32=0.0%, >=64=0.0%
     submit    : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     complete  : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     issued rwts: total=46129,0,0,0 short=0,0,0,0 dropped=0,0,0,0
     latency   : target=0, window=0, percentile=100.00%, depth=1

Run status group 0 (all jobs):
   READ: bw=1538MiB/s (1612MB/s), 1538MiB/s-1538MiB/s (1612MB/s-1612MB/s), io=45.0GiB (48.4GB), run=30002-30002msec
``` 

# Random Read
## CMD
Reading 150m of random data: `fio --name=randread --ioengine=posixaio --rw=randread --bs=1m --size=150m --numjobs=1 --iodepth=1 --runtime=60 --output-format=json --output=/home/rand_read.json --time_based --end_fsync=1`
## Output
```
fio --name=randwrite --ioengine=posixaio --rw=randread --bs=1m --size=150m --numjobs=1 --iodepth=1 --runtime=30 --time_based --end_
fsync=1
randwrite: (g=0): rw=randread, bs=(R) 1024KiB-1024KiB, (W) 1024KiB-1024KiB, (T) 1024KiB-1024KiB, ioengine=posixaio, iodepth=1
fio-3.28
Starting 1 process
Jobs: 1 (f=1): [r(1)][100.0%][r=780MiB/s][r=780 IOPS][eta 00m:00s]
randwrite: (groupid=0, jobs=1): err= 0: pid=379: Sun Dec  5 01:00:52 2021
  read: IOPS=598, BW=599MiB/s (628MB/s)(17.5GiB/30002msec)
    slat (usec): min=18, max=42400, avg=80.27, stdev=922.00
    clat (usec): min=2, max=51603, avg=1511.58, stdev=4081.63
     lat (usec): min=649, max=71195, avg=1591.85, stdev=4216.44
    clat percentiles (usec):
     |  1.00th=[  816],  5.00th=[  914], 10.00th=[  955], 20.00th=[ 1012],
     | 30.00th=[ 1057], 40.00th=[ 1090], 50.00th=[ 1123], 60.00th=[ 1156],
     | 70.00th=[ 1205], 80.00th=[ 1254], 90.00th=[ 1352], 95.00th=[ 1418],
     | 99.00th=[ 1958], 99.50th=[45351], 99.90th=[46400], 99.95th=[47449],
     | 99.99th=[51643]
   bw (  KiB/s): min=20480, max=851968, per=99.38%, avg=609332.07, stdev=330273.51, samples=59
   iops        : min=   20, max=  832, avg=595.05, stdev=322.53, samples=59
  lat (usec)   : 4=0.01%, 500=0.01%, 750=0.19%, 1000=17.94%
  lat (msec)   : 2=80.86%, 4=0.13%, 10=0.03%, 50=0.80%, 100=0.03%
  cpu          : usr=0.77%, sys=6.64%, ctx=30772, majf=0, minf=17982
  IO depths    : 1=100.0%, 2=0.0%, 4=0.0%, 8=0.0%, 16=0.0%, 32=0.0%, >=64=0.0%
     submit    : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     complete  : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     issued rwts: total=17964,0,0,0 short=0,0,0,0 dropped=0,0,0,0
     latency   : target=0, window=0, percentile=100.00%, depth=1

Run status group 0 (all jobs):
   READ: bw=599MiB/s (628MB/s), 599MiB/s-599MiB/s (628MB/s-628MB/s), io=17.5GiB (18.8GB), run=30002-30002msec
```

# Sequential Read & Write
## CMD
Read and write 150m of data: `fio --name=readwrite --ioengine=posixaio --rw=readwrite --bs=1m --size=150m --numjobs=1 --iodepth=1 --runtime=60 --output-format=json --output=/home/seq_rw.json --time_based --end_fsync=1`
## Output
```
fio --name=randwrite --ioengine=posixaio --rw=readwrite --bs=1m --size=150m --numjobs=1 --iodepth=1 --runtime=30 --time_based --end
_fsync=1
randwrite: (g=0): rw=rw, bs=(R) 1024KiB-1024KiB, (W) 1024KiB-1024KiB, (T) 1024KiB-1024KiB, ioengine=posixaio, iodepth=1
fio-3.28
Starting 1 process
Jobs: 1 (f=1): [F(1)][100.0%][eta 00m:00s]                                        
randwrite: (groupid=0, jobs=1): err= 0: pid=92904: Sun Dec  5 01:08:06 2021
  read: IOPS=6, BW=6947KiB/s (7113kB/s)(285MiB/42011msec)
    slat (usec): min=16, max=251, avg=39.30, stdev=21.51
    clat (usec): min=70, max=12876, avg=301.07, stdev=889.03
     lat (usec): min=95, max=12967, avg=340.37, stdev=892.73
    clat percentiles (usec):
     |  1.00th=[   74],  5.00th=[   98], 10.00th=[  117], 20.00th=[  135],
     | 30.00th=[  151], 40.00th=[  163], 50.00th=[  174], 60.00th=[  182],
     | 70.00th=[  192], 80.00th=[  212], 90.00th=[  239], 95.00th=[  306],
     | 99.00th=[ 4228], 99.50th=[ 4490], 99.90th=[12911], 99.95th=[12911],
     | 99.99th=[12911]
   bw (  KiB/s): min= 2048, max=315392, per=100.00%, avg=72960.00, stdev=107748.59, samples=8
   iops        : min=    2, max=  308, avg=71.25, stdev=105.22, samples=8
  write: IOPS=7, BW=7532KiB/s (7713kB/s)(309MiB/42011msec); 0 zone resets
    slat (usec): min=21, max=19576, avg=122.64, stdev=1112.16
    clat (nsec): min=1130, max=17495M, avg=107387080.17, stdev=1062673074.17
     lat (usec): min=180, max=17495k, avg=107509.72, stdev=1062670.38
    clat percentiles (usec):
     |  1.00th=[     167],  5.00th=[     194], 10.00th=[     204],
     | 20.00th=[     217], 30.00th=[     235], 40.00th=[     249],
     | 50.00th=[     269], 60.00th=[     289], 70.00th=[     310],
     | 80.00th=[     351], 90.00th=[     429], 95.00th=[     482],
     | 99.00th=[ 3472884], 99.50th=[ 3774874], 99.90th=[17112761],
     | 99.95th=[17112761], 99.99th=[17112761]
   bw (  KiB/s): min= 8192, max=307200, per=100.00%, avg=70087.11, stdev=104732.61, samples=9
   iops        : min=    8, max=  300, avg=68.44, stdev=102.28, samples=9
  lat (usec)   : 2=0.17%, 100=2.53%, 250=62.79%, 500=29.97%, 750=0.51%
  lat (usec)   : 1000=0.17%
  lat (msec)   : 2=0.67%, 4=1.01%, 10=0.34%, 20=0.17%, 100=0.17%
  lat (msec)   : 250=0.17%, 750=0.17%, 1000=0.17%, 2000=0.17%, >=2000=0.84%
  cpu          : usr=0.04%, sys=0.14%, ctx=1081, majf=0, minf=619
  IO depths    : 1=100.2%, 2=0.0%, 4=0.0%, 8=0.0%, 16=0.0%, 32=0.0%, >=64=0.0%
     submit    : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     complete  : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     issued rwts: total=285,309,0,0 short=0,0,0,0 dropped=0,0,0,0
     latency   : target=0, window=0, percentile=100.00%, depth=1

Run status group 0 (all jobs):
   READ: bw=6947KiB/s (7113kB/s), 6947KiB/s-6947KiB/s (7113kB/s-7113kB/s), io=285MiB (299MB), run=42011-42011msec
  WRITE: bw=7532KiB/s (7713kB/s), 7532KiB/s-7532KiB/s (7713kB/s-7713kB/s), io=309MiB (324MB), run=42011-42011msec
```

# Random Read & Write
## CMD
Read and write 150m of random data: `fio --name=randrw --ioengine=posixaio --rw=randrw --bs=1m --size=150m --numjobs=1 --iodepth=1 --runtime=60 --output-format=json --output=/home/rand_rw.json --time_based --end_fsync=1`
## Output
```
fio --name=randrw --ioengine=posixaio --rw=randrw --bs=1m --size=150m --numjobs=1 --iodepth=1 --runtime=30 --time_based --end_fsync=
1
randrw: (g=0): rw=randrw, bs=(R) 1024KiB-1024KiB, (W) 1024KiB-1024KiB, (T) 1024KiB-1024KiB, ioengine=posixaio, iodepth=1
fio-3.28
Starting 1 process
randrw: Laying out IO file (1 file / 150MiB)
Jobs: 1 (f=1): [F(1)][100.0%][eta 00m:00s]                                        
randrw: (groupid=0, jobs=1): err= 0: pid=93514: Sun Dec  5 01:11:23 2021
  read: IOPS=3, BW=3559KiB/s (3645kB/s)(152MiB/43728msec)
    slat (usec): min=21, max=179, avg=49.33, stdev=17.97
    clat (usec): min=122, max=11654k, avg=104343.77, stdev=944175.53
     lat (usec): min=158, max=11654k, avg=104393.10, stdev=944176.25
    clat percentiles (usec):
     |  1.00th=[     128],  5.00th=[     147], 10.00th=[     153],
     | 20.00th=[     192], 30.00th=[    1156], 40.00th=[    1254],
     | 50.00th=[   44303], 60.00th=[   45351], 70.00th=[   45876],
     | 80.00th=[   46400], 90.00th=[   46400], 95.00th=[   50594],
     | 99.00th=[  513803], 99.50th=[11609834], 99.90th=[11609834],
     | 99.95th=[11609834], 99.99th=[11609834]
   bw (  KiB/s): min= 2048, max=131072, per=100.00%, avg=23945.85, stdev=33269.60, samples=13
   iops        : min=    2, max=  128, avg=23.38, stdev=32.49, samples=13
  write: IOPS=3, BW=3513KiB/s (3597kB/s)(150MiB/43728msec); 0 zone resets
    slat (usec): min=28, max=115, avg=64.50, stdev=15.97
    clat (usec): min=175, max=15173k, avg=155788.97, stdev=1341618.17
     lat (usec): min=203, max=15173k, avg=155853.47, stdev=1341616.80
    clat percentiles (usec):
     |  1.00th=[     202],  5.00th=[     223], 10.00th=[     241],
     | 20.00th=[     269], 30.00th=[     359], 40.00th=[     383],
     | 50.00th=[     404], 60.00th=[     416], 70.00th=[     433],
     | 80.00th=[     449], 90.00th=[     478], 95.00th=[     510],
     | 99.00th=[ 6140462], 99.50th=[15233713], 99.90th=[15233713],
     | 99.95th=[15233713], 99.99th=[15233713]
   bw (  KiB/s): min= 2048, max=114688, per=100.00%, avg=25429.33, stdev=29568.39, samples=12
   iops        : min=    2, max=  112, avg=24.83, stdev=28.88, samples=12
  lat (usec)   : 250=17.22%, 500=41.06%, 750=1.32%, 1000=0.66%
  lat (msec)   : 2=12.25%, 50=22.85%, 100=2.65%, 250=0.33%, 750=0.33%
  lat (msec)   : 2000=0.33%, >=2000=0.99%
  cpu          : usr=0.01%, sys=0.09%, ctx=620, majf=0, minf=328
  IO depths    : 1=100.3%, 2=0.0%, 4=0.0%, 8=0.0%, 16=0.0%, 32=0.0%, >=64=0.0%
     submit    : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     complete  : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     issued rwts: total=152,150,0,0 short=0,0,0,0 dropped=0,0,0,0
     latency   : target=0, window=0, percentile=100.00%, depth=1

Run status group 0 (all jobs):
   READ: bw=3559KiB/s (3645kB/s), 3559KiB/s-3559KiB/s (3645kB/s-3645kB/s), io=152MiB (159MB), run=43728-43728msec
  WRITE: bw=3513KiB/s (3597kB/s), 3513KiB/s-3513KiB/s (3597kB/s-3597kB/s), io=150MiB (157MB), run=43728-43728msec
```

## Sequential Read from Two Nodes
## CMD
Execute on two nodes: 
`fio --name=read-n1 --ioengine=posixaio --rw=read --bs=1m --size=150m --numjobs=1 --iodepth=1 --runtime=60 --output-format=json --output=/home/seq_read_n1.json --time_based --end_fsync=1`
`fio --name=read-n2 --ioengine=posixaio --rw=read --bs=1m --size=150m --numjobs=1 --iodepth=1 --runtime=60 --output-format=json --output=/home/seq_read_n2.json --time_based --end_fsync=1`
## Output
### Node 1
```
fio --name=read --ioengine=posixaio --rw=read --bs=1m --size=150m --numjobs=1 --iodepth=1 --runtime=30 --time_based --end_fsync=1
read: (g=0): rw=read, bs=(R) 1024KiB-1024KiB, (W) 1024KiB-1024KiB, (T) 1024KiB-1024KiB, ioengine=posixaio, iodepth=1
fio-3.28
Starting 1 process
Jobs: 1 (f=1): [R(1)][100.0%][r=258MiB/s][r=258 IOPS][eta 00m:00s]
read: (groupid=0, jobs=1): err= 0: pid=93834: Sun Dec  5 01:14:38 2021
  read: IOPS=114, BW=115MiB/s (120MB/s)(3445MiB/30039msec)
    slat (usec): min=13, max=25995, avg=79.10, stdev=578.51
    clat (nsec): min=730, max=9707.2M, avg=8562518.24, stdev=183369251.61
     lat (usec): min=74, max=9707.3k, avg=8641.61, stdev=183369.17
    clat percentiles (usec):
     |  1.00th=[     87],  5.00th=[    106], 10.00th=[    117],
     | 20.00th=[    131], 30.00th=[    143], 40.00th=[    153],
     | 50.00th=[    165], 60.00th=[    178], 70.00th=[    198],
     | 80.00th=[    231], 90.00th=[    400], 95.00th=[   4359],
     | 99.00th=[ 158335], 99.50th=[ 258999], 99.90th=[1920992],
     | 99.95th=[2734687], 99.99th=[9730786]
   bw (  KiB/s): min=16384, max=1388544, per=100.00%, avg=251904.00, stdev=281753.66, samples=28
   iops        : min=   16, max= 1356, avg=246.00, stdev=275.15, samples=28
  lat (nsec)   : 750=0.03%, 1000=0.03%
  lat (usec)   : 2=0.03%, 4=0.03%, 50=0.03%, 100=2.61%, 250=80.49%
  lat (usec)   : 500=6.94%, 750=0.32%, 1000=0.20%
  lat (msec)   : 2=0.99%, 4=2.82%, 10=4.03%, 20=0.06%, 50=0.09%
  lat (msec)   : 100=0.20%, 250=0.49%, 500=0.41%, 750=0.03%, 2000=0.09%
  lat (msec)   : >=2000=0.09%
  cpu          : usr=0.16%, sys=1.22%, ctx=6012, majf=0, minf=3465
  IO depths    : 1=100.0%, 2=0.0%, 4=0.0%, 8=0.0%, 16=0.0%, 32=0.0%, >=64=0.0%
     submit    : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     complete  : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     issued rwts: total=3445,0,0,0 short=0,0,0,0 dropped=0,0,0,0
     latency   : target=0, window=0, percentile=100.00%, depth=1

Run status group 0 (all jobs):
   READ: bw=115MiB/s (120MB/s), 115MiB/s-115MiB/s (120MB/s-120MB/s), io=3445MiB (3612MB), run=30039-30039msec
```
### Node 2
```
fio --name=read2 --ioengine=posixaio --rw=read --bs=1m --size=150m --numjobs=1 --iodepth=1 --runtime=30 --time_based --end_fsync=1
read2: (g=0): rw=read, bs=(R) 1024KiB-1024KiB, (W) 1024KiB-1024KiB, (T) 1024KiB-1024KiB, ioengine=posixaio, iodepth=1
fio-3.28
Starting 1 process
read2: Laying out IO file (1 file / 150MiB)
Jobs: 1 (f=1): [R(1)][100.0%][r=1747MiB/s][r=1747 IOPS][eta 00m:00s]
read2: (groupid=0, jobs=1): err= 0: pid=94780: Sun Dec  5 01:14:56 2021
  read: IOPS=1120, BW=1120MiB/s (1175MB/s)(32.8GiB/30001msec)
    slat (usec): min=11, max=42791, avg=61.71, stdev=623.21
    clat (nsec): min=520, max=465833k, avg=755121.46, stdev=8051456.96
     lat (usec): min=72, max=465856, avg=816.83, stdev=8075.49
    clat percentiles (usec):
     |  1.00th=[    89],  5.00th=[   108], 10.00th=[   117], 20.00th=[   129],
     | 30.00th=[   139], 40.00th=[   149], 50.00th=[   159], 60.00th=[   172],
     | 70.00th=[   186], 80.00th=[   208], 90.00th=[   277], 95.00th=[  3523],
     | 99.00th=[  5800], 99.50th=[  6390], 99.90th=[ 98042], 99.95th=[175113],
     | 99.99th=[434111]
   bw (  MiB/s): min=    4, max= 1800, per=99.10%, avg=1110.03, stdev=713.86, samples=59
   iops        : min=    4, max= 1800, avg=1110.03, stdev=713.86, samples=59
  lat (nsec)   : 750=0.01%, 1000=0.01%
  lat (usec)   : 2=0.01%, 4=0.01%, 20=0.01%, 50=0.01%, 100=2.79%
  lat (usec)   : 250=85.29%, 500=3.56%, 750=0.07%, 1000=0.10%
  lat (msec)   : 2=1.08%, 4=2.90%, 10=3.95%, 20=0.01%, 50=0.01%
  lat (msec)   : 100=0.10%, 250=0.07%, 500=0.03%
  cpu          : usr=1.01%, sys=11.98%, ctx=56950, majf=0, minf=33626
  IO depths    : 1=100.0%, 2=0.0%, 4=0.0%, 8=0.0%, 16=0.0%, 32=0.0%, >=64=0.0%
     submit    : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     complete  : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     issued rwts: total=33606,0,0,0 short=0,0,0,0 dropped=0,0,0,0
     latency   : target=0, window=0, percentile=100.00%, depth=1

Run status group 0 (all jobs):
   READ: bw=1120MiB/s (1175MB/s), 1120MiB/s-1120MiB/s (1175MB/s-1175MB/s), io=32.8GiB (35.2GB), run=30001-30001msec
```


# Delete Test
## CMD
Delete file from previous test `time rm -rf random-write.0.0`
## Output
time rm -rf random-write.0.0 
real	0m 0.00s
user	0m 0.00s
sys	0m 0.00s


# Plots 
`fio-plot -n 1 -i ./ --source "Saurabh Joshi"  -T "Comparing IOPs performance over time" -g -t iops -r read --xlabel-parent 0`