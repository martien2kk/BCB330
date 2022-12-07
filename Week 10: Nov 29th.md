### Nov 29th, 2022
By: `Keren`

Novel Virus Library: `SRR7630408` ; score: `96`; percentage identity: `76`

In Oracle VM:

1. Open SRA Toolkit in terminal
```
kk@kk-VirtualBox:~$ cd /home/kk/sratoolkit.3.0.1-ubuntu64/bin/ 

kk@kk-VirtualBox:~/sratoolkit.3.0.1-ubuntu64/bin$
```

2. prefetch SRA for `SRR7630408`
```
kk@kk-VirtualBox:~/sratoolkit.3.0.1-ubuntu64/bin$ prefetch SRR7630408 

2022-12-07T10:59:24 prefetch.2.11.3: Current preference is set to retrieve SRA Normalized Format files with full base quality scores.
2022-12-07T10:59:25 prefetch.2.11.3: 1) Downloading 'SRR7630408'...
2022-12-07T10:59:25 prefetch.2.11.3: SRA Normalized Format file is being retrieved, if this is different from your preference, it may be due to current file availability.
2022-12-07T10:59:25 prefetch.2.11.3:  Downloading via HTTPS...
2022-12-07T11:02:48 prefetch.2.11.3:  HTTPS download succeed
2022-12-07T11:02:53 prefetch.2.11.3:  'SRR7630408' is valid
2022-12-07T11:02:53 prefetch.2.11.3: 1) 'SRR7630408' was downloaded successfully
2022-12-07T11:02:53 prefetch.2.11.3: 'SRR7630408' has 0 unresolved dependencies
```

3. download fastq file for `SRR7630408`
```
kk@kk-VirtualBox:~/sratoolkit.3.0.1-ubuntu64/bin$ fasterq-dump SRR7630408

spots read      : 17,124,977
reads read      : 34,249,954
reads written   : 34,249,954
```

4. Use Adapter Remover to remove adapters
```
kk@kk-VirtualBox:~$ cd /home/kk/adapterremoval-2.3.1/

kk@kk-VirtualBox:~/adapterremoval-2.3.1$ AdapterRemoval --file1 /home/kk/sratoolkit.3.0.1-ubuntu64/bin/SRR7630408_1.fastq --file2 /home/kk/sratoolkit.3.0.1-ubuntu64/bin/SRR7630408_2.fastq

Trimming paired end reads ...
Opening FASTQ file '/home/kk/sratoolkit.3.0.1-ubuntu64/bin/SRR7630408_1.fastq', line numbers start at 1
Opening FASTQ file '/home/kk/sratoolkit.3.0.1-ubuntu64/bin/SRR7630408_2.fastq', line numbers start at 1
Processed a total of 34,249,954 reads in 2:56.1s; 194,000 reads per second on average ...
```

5. Use Spades to assembe genome
```
k@kk-VirtualBox:~/SPAdes-3.15.5-Linux/bin$ spades.py -1 SRR7630408_1.fastq -2 SRR7630408_2.fastq --rna -o run1
```


