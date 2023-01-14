### Nov 29th, 2022
By: `Keren`

From the previous week, `SRR10600885` file is too larger to assemble and I do not have enough disk space on my virtual machine. Thus, I picked another library with potential novel virus, that is smaller in size. 

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

...

===== Assembling finished. Used k-mer sizes: 33, 49 

 * Assembled transcripts are in /home/kk/SPAdes-3.15.5-Linux/bin/run1/transcripts.fasta
 * Paths in the assembly graph corresponding to the transcripts are in /home/kk/SPAdes-3.15.5-Linux/bin/run1/transcripts.paths
 * Hard filtered transcripts are in /home/kk/SPAdes-3.15.5-Linux/bin/run1/hard_filtered_transcripts.fasta
 * Soft filtered transcripts are in /home/kk/SPAdes-3.15.5-Linux/bin/run1/soft_filtered_transcripts.fasta
 * Assembly graph is in /home/kk/SPAdes-3.15.5-Linux/bin/run1/assembly_graph.fastg
 * Assembly graph in GFA format is in /home/kk/SPAdes-3.15.5-Linux/bin/run1/assembly_graph_with_scaffolds.gfa

======= SPAdes pipeline finished.

SPAdes log can be found here: /home/kk/SPAdes-3.15.5-Linux/bin/run1/spades.log

Thank you for using SPAdes!
```

Using assembled transcpit, inputted in to ORF Finder
Contig:`NODE_1`, Length: `7297`
```
>NODE_1_length_7297_cov_16729.226821_g0_i0
TAAGGCCACGTGACTGGAGTTCAGACGTGTGCTCTTCCGATCTCGTGAACATAACACAAAGAAAGCAAAATGTCTTTCGCTTATCGTTCACCACAAGAGATTTTTCTACAAACAATACCTCAAACTTATGCTGAACCACTATATAAAAAAACATCAGAATCAATCTCAAAAATCATCGACGATTCAGATTTTTTTAAATATAGCTGTTCATCAGAAGTTAAAGAACGTCTTGTAAAGGCAGGGTTACCAATATCTCCATTTCTATATTTAATACACTCTCATCCAGCATGCAAAATGTTAGAAAATTACATGTTATTTGTTTGCGCAAAAGATTACATATTTAAGAATAAGTCAGTTTTAATATCTATGAAGGAATGCAAAATAAACATCCTGTGTAGGAGAAATGATGTTAACATCCCTTTCCTTAATAGATTGGTTGTGGCCAAAGATTCCTTCAGATATGACGAGCCAAGTGTATGTGCAATAAATGAGCTAGCAGTTAAGGTTAGGGACTCAGGGAGAAAGTCTGTGTTTATACACGATGAGGTGCATTACTGGAGCATGGAAGATTTGAACAGCTTCATATCAATTTCAGAGGTTGATAACATTTTGTGTACCGTCGTGTTCCCACCTGAAATCCTTAATGGGTCAAAAAGTTCATTGAATCCTGAGTTGTATAGTTTCAAGATTGTTGGTGACAGAGTTGTTTTTGCCCCGGATGGAAATTATTCAGAATCTTACACCCAACCGAAGCGGTGTGACATATTGAGATTGAGAGGGTTAAATGTGGGGAACAAAAAGTATGCAGTAACTATGCTCAAAAGTGTGGGTGCTCATCACTTGGTGTTTATTAAAAGGATGAGCTATTTGAACGAACCTGAGGTTAGATTTTTCGACACTCCATCTGCCGTCGATTTTAATTTATTGCTACCTGGAAGGTTGAAGGGGTCATGTAAAATAAGGTTAGAAATTCTGAAGAAAATGATTGCTTACTTGTTGGCTCTTAAAAAATCAGATGCAAATTCAGCTGTTGCCAAATTGAGGTCATTGTCAGTAAGTGAAATTTACCTTGATGAAATAACTCTAGCAATGCATCTGGGTAAGGTGTTTGAAAATCTCAAGCTTCAGGAGGCTGTTGGAATTGTTGGAATATTTGATCGTCTTTTGCTCTTTATGAAGGATGTTTTCCTTATGGATGGTTTGATTGAGTGGTCAGATAGAAGGAAAGAGGAAAGTGCATTAAGGTTCATATCAAATTTGGATTCTTATTCTCTATCAATTGAAACTTTTGTGGCCAAGGATCGCCTGATGCGGTCTACGCAGGCTTGTGAATCCGACTCTGAGGGTGAGTCTGATGGGGCATTAGAGAATGAAATAAATGACAGACTCCCAGACCCATATTTTATAATCAATGGCTCAGATGTTGAGGGTGATTATGATGACCTTACAGACTGTGTTTATTTGGAGTCTGGATTGAAGCTACTCCCTGTTTGGCCCGATGAGATTGAGAGGAACGTTAGGGAAATCAGGGAGAGGAATAGAAGGAGAGAAAGTTTTTACAAACCTGGAGATTTCATAAGCTTTGAAGAGCTGCATTACCTCATAAATTCTAAGGAGTTGAATGTTGGAAATGTAATTTATAGAAGAAATTCCATGATTTTTCAGGTCAGACCATTATTGATAGAGGGTTGCCCCAAGCCACAAGAGATGGAGGTTCAACTTCCAGTTGAAATGGATTTTGAGTTTGATAACCAAAATGATAAAGGGAGGGATGTGACTGATATTGAAGATGTTCAGACCGAGGACCCTCTCATTAAAGCATCTAGCTCAAGAGTCAGTTTGAACTGTGGATGTGGCATGTCAATACCAATCGAGGAGGTTGATGGTGAGCTGGATTTGGATTTTATCAACTTTAAGGATGATCTTAAAAATAGGGTAGCCACATTTTTCTCAAGGAATGGTGAGGGTTACAGTTATAATGGTGGTAGCCATAAATCTGATGGATGGCCGGAAGAGCTGGATAAAATTCTTAGGGCGTTAAATGTTGATGTGAATGATTATAACCACTGTCTGGTGCAAAAGTATAGGAAAGGGGGAAAGATAGGTTTTCATTCAGATAATGAAAATTGTTACCCAAAAGGAAATGAGATTTTAACAGTTTCAATTGGTGAAGGTATCTTTTCAATTAAATGTGAGAGAGGTTCAGGGATGACAAATCTGAATGGAAGGATACACTTCAAAATGCCTAAAGGGTTTCAAGAAACACATAAACATTCAGTGATCTGCACTGAAGGCAGGATATCAATGACATTCAGAAGCACAGGTAAGCAGGCTGAGAGAGCCTACGTTGATGATGCAGAAGTTAGTGATGATTACAACGATGAAGAAGGGTGTATTAGTGACGATGATGAGCAGGTTTCAAGCTCTTTTCAAATCAATTTCGATCAAGTTAGCAAAATGATAAAGAGTGGAGGTTCAAGAAATGCATGTTTATTAGTTGCATTGGCAGATTTGATGAATAGTGACAAATATTTGGTCTTGAGCTTATTAGTTGGTGCTGATTCAAGCTGGATTGACTGGTTCATCAAAGATGACGGTGCCGGATTTGACGATGTTGTGAAAGCTGTGACAGAACTGAACATGCGTGTAAACTTATATGAGAAAGAAAAAGTCACTTTGATAAACCCTGATTCAAGTTACAACACTGGAGATCTGTATCTGAGTGACGGGCACATTAGTTCTCAAAAGCCATCTAACTTTGAAGGTATCAAGACCTTTGGTAGTACAAGTTTCTTTTCAGATTTCTTGACCCAGTTTGAGAGATTGGCTGGGGCAGGTAGAGTGAAATACGATGCGAGGTCTGAAAGGGCTAACGCACTGATAGAGAGCTTTCAGGATAACTTTACTGGTGTGTTTGCAAATAAGTTCAAACTGCAGTTAGAGAGGGTCATTGAGGACAAGTCATTTGAGATAGTGAGCATCACGGGATTCGCAGGTTCAGGAAAAAGTAGAGGGGTTCAAGCTTTGATGAGGGGTATGTTTAACAAAAAGAGCTCACTAGTGATTAGTCCAAGAAAGGCATTGCTTGAAGATTGGAGAGTAAAACTAAAAGAAGGTTTTAAAGGGAGGTTGAAGACCTTTGAGGTTGCATTGAAAGAGATTAGATGTGCTGAACTTATAATTGTGGATGAATTAACACTGTTTCCAAATGGATATTTGGACTTGTTGCTGTTGAGTTCGAAAGCACAGATAGTAGTTTTATATGATCCAATGCAGGCAAGGTACTTTCCAAGGAACGACTCGTTCAAATTGAGTAGTGTGCATGATGTTGATAGAATAGAGGTTAAAGAATATTTGATGTACTCTCACAGGATGTCGAAAAGCATGGATATGTTTGATGTGAACTGTCTAGGATCTGGAGAATTGTGGGAGTTTCACAACAGGAGGTTTAATGAGGCTGCTGCTATGTACAAAGCTCTTAAGGACTATGATTGCTTAATTCTTGCACCATCAGAGTCAAAAAAAATCGAGATGGAGAAGTTTGGTAGATCAAGCACATTTGGGTCAGCACAGGGGCTTTCAAGTGACTATGTTGTGATAGTCGTTGATCAAGATGCATTCATAACCTCTCAAGATCATTGGATAGTCGCATTAACAAGAGCGAGGAAAGGTATAGCATTTCTTTATCAAGGTTTTAGGGATGTGAACGTATTTGCTGAATCACATCGTGGGACTTTGATTGGGAAGGTGTTGCTTGGCAAAAAGGTTTCGGAGGACCATCTGATATTTGGGGCAGGGACTGTTTTAAAGAAGGCAAGGATAATAAGGGAACCTGAAAGCATGAAGGATGAGGCTATGGAGATCAAACTGTCTGGTGATCCATGGCTTAAAGGGCAGTTGAATTTGCTCGAGAATGTTGAGTTGGATGATGTGGAACCAAGGGAAGTTGATAGGAATGACTCGCCACCGAGAACACATCTGAACATATGTACAGAGGACGCTTTCTGTGAACTTTCTGAAATCAAAGCCAGGGAATATAGGGAGTTCTTAAGCCCAAATGATATGTCAAATCAATTCAACGACATGAAGACATTGAGAGAAAAAAATTGGAATAATTATGTATATGTTTTTGAGACAATATACCCGAGGCACCAGAGCTCGGATGACCTGACTTTTTTTGCAGCGATACAAAAGAGGTTGCTGAGGTCCAATCCTGAAAAGGAAGCAAGAAAATTGGAAAAAAGTTGGGGAATAGGCTCAATAATGTTTCACGAGTTGAAAAGGACGTTGGGATTGAATCCGAATGTCTACATTGATGAAGAGGTGGTTAATAGGGAGTTTGTGCAAAAAAGGTTGAACAAATCAGCAAAATTGATAGAGAACCACTCAGGAAGATCAGACCCAGATTGGAGATTGGATCATTTCTTCCTGTTTATGAAATCACAACTCTGCACTAAGTTTGAAAAAAGGTTCGTAGATGCAAAGGCTGGTCAGACTCTTGCATGTTTCTCTCATCAGATACTGACAAGATTTGGTGTTGCATTCAGAACATTTGAAAAAAAATTTTCAGCTAACCTGCCAAAAACATGGTACGTTCATACGATGAAAAACTTTGATCAGCTGAACTTGTGGGCTTGTGAAAATGTGAAGGAAAGGGAGGGTACTGAATCTGATTATGAAGCTTTCGACAGATCCCAAGATGCTCCAATTCTGGCATTTGAGATATTAATGCTGAGATTCTTCAACTGGCCAGAGGATTTGATTCAAGATTACAAAATGATTAAGCTTTGGATGGGATGCAGGTTAGGAGCTGTAGCCATAATGCGATTTACAGGTGAATTTGGGACATTCTTTTTTAACACACTAGTGAACATGGCCTTCACAGTCATGCGTTACCATGTGAATAAGGAAAGTGTAATAGCTTTTGCTGGTGATGATATGTATGCTGCTGGTTTTCTGAAGAGGAGAGTTGATCTCGAGTTTGCCTTGGACCAGCTAACTTTAAAGGCGAAAGTTCAATTCACAAGAAGACCAATGTTTTGCGGATGGTATATGACTCCAATGGGGATAGTTAAGGAACCAAGATTGGTGCTTGAAAGATGGAAAATAGCTGAACAAAAAGGGAACCTGAGGGATGTGATAATAAACTATGCTCTGGAGGTATCGTATGGGTACAGATTAGGTGAGTACCTCTGGGAGGTTCTTGATAATTTAGAGAGTCAACAAGAGATTGTGAGAAATATTGTGAAAAGCAAGCATCTATTGCCATTGAAGGTTAGACATTTCTTTTCAGCTGTTGACAATGAAACGCTCAGTACAGAGTTTTCAGAGTACATGGGACAACACCCAAAGTTTACTGAAAGCTGTGGACTCGAGTGTAGTCTATTCAAACGAGCTTAACCCATTCTCCAGAGCCAGTATCAAGAAGACGGAGTATAGTATCAAAGTTGAGAGTGATACTGGAATTCTGACCACTGCTGGGGTACCTATATTTGACAGTGATGAAATTAAGAGTATAATGGATTCGAAATACAATTTTGTTCATCTGGGTGCATTCATTTTTGGACTGCAAGCTCACTTCCCTGATGCTGATGATGTGACCGGCAAACTCTTTGTTATAGACCACAGGAGATCAGACCCAACAAAAGCTGTGATCGCGAAAAGGGCAATAAGATTCGTAAATGGAAAATCTGCGGTTATGATAAAACCAAACTTTTCAATAAGGAAGTCGGACCTTGAACAGGCAAACTGTTTCTCGGCTTACTTTGTTATGGAGGGTGTAGATTTTAAGGCCAGCTTTTCACCATTTTCAGTTGTGGGGGGTTCAATATATAGGTTGACCTATGGTCTATCTGGCAAATCTAATAACCTGGCTTTCGGATCATGCTCTCCGGTGGATTTGGGAGGAACATCTGATTTAACAAAGGGAAGTTTGAGTGGTGATGAAATTGAAATGATAGAGGGTCTGGGCAAGAAACCTGAGCTTGTAAGTACAAGGTATGTAGGGAGGGGTTCAAGATTTGCAGAACCGATAAAGCTGAGGGAGTATGGAAGCAGGAGAAAAAGGTCGCAAGTTATGTGTAGCGCGTCGGAACGATTTGGAAATGGCGACAGACTTTTCGAAGATAGTGAGGCAAAGAGTAAAGAACCTGCTAGAGCTAGCTTTTCAGGCACAAGTGAATCGAGCTTCGGAACCGGTAAGAAGGGATTCAAGGAGAGCTTTACTGAGATTCATATTCGGAAGATTCGCAGTGATGGGGACCAGTCCGAAGACGAAATATCCGGATGAGAATGTGAACTCGGAAGAGTTTCATTTAATAAACCCTAATAATGATGTGGAGAGAGTGAGTTTCACAGTTAATTTCTTTAGCGTTAAGAACATGATATGTACCTCTTTAATGACTGGGGATTCCAACTATGTGAGAAGCATGACTTTCAGAGCCGCTTGTAGACCTTTTGCAAGGTATGCGTTTAGGTATTTGGAGCAGTTTGACGTGGTGACATGTTTAATGCAAAAATTACCTGCCACCTGTGCGAATGGGCCTCATGTAGCTTTTGATTTTGCTGATGGTTTAGTAGCTGATAGACTTGGAAGAGTCTTGTCACTGGAGGAAAAACGAGTCATACAGAGGTTACATAGAAGAGTTTTTGCAACTGCTAATAGGTTATCTGTGATAAGCGCTCAATCCGAAATGAATGATGATGAGATATAAGTAGTGATGGTCAGGCCAACACATGACCTTAAACCTGATTTGTTGGTTAATGTAGTATGTTAAGTTAGTTAACCTAGTTTAATGGATATGTTAGTAAGCTTGTTGTCGGTCAAGGAATGCATAGATAAGATAAAGGTTCCTGATGCATCTGAAACACCAAGATCACACAATGAGTTGCCCTCAGAAATCAAAAGCATTATCTTTAAAATGTTCAAAGAGAGACATCTACATGAACATTATGGGAATGTACGCAGTAAGCAACCGGGACTGAGCCCGTATGCAAAAAGAAGAAGAGCTAAAATGCTAGGGGTTTGTCATAAATGTGGAAGAACGAACTGTGATGGTGTTTTTAGACAGTTGCAAGGTTCCACTAGGCCTTGTGATGGTGGTTTTGGGATAATGAGTTCCAAAAGAGCTGCAAAACTAGAGGAGATAAGGTATGGCAGAGTAACTTCGTGAGACGCATACTTTATCTTTAAAATAGTCTCATATTAGTTGGAACTTAATCCCACTAATCGCAAGGTTTTATTAAGCATCTTTTCCAGATCGGAAGAGCGTCGTGTAGGGAAAGAGTGTAGATCTCG
```

ORFs found: `148` Genetic code: `1` Start codon: `stop-to-stop`
```
>lcl|ORF1
MKESKMSFAYRSPQEIFLQTIPQTYAEPLYKKTSESISKIIDDSDFFKYS
CSSEVKERLVKAGLPISPFLYLIHSHPACKMLENYMLFVCAKDYIFKNKS
VLISMKECKINILCRRNDVNIPFLNRLVVAKDSFRYDEPSVCAINELAVK
VRDSGRKSVFIHDEVHYWSMEDLNSFISISEVDNILCTVVFPPEILNGSK
SSLNPELYSFKIVGDRVVFAPDGNYSESYTQPKRCDILRLRGLNVGNKKY
AVTMLKSVGAHHLVFIKRMSYLNEPEVRFFDTPSAVDFNLLLPGRLKGSC
KIRLEILKKMIAYLLALKKSDANSAVAKLRSLSVSEIYLDEITLAMHLGK
VFENLKLQEAVGIVGIFDRLLLFMKDVFLMDGLIEWSDRRKEESALRFIS
NLDSYSLSIETFVAKDRLMRSTQACESDSEGESDGALENEINDRLPDPYF
IINGSDVEGDYDDLTDCVYLESGLKLLPVWPDEIERNVREIRERNRRRES
FYKPGDFISFEELHYLINSKELNVGNVIYRRNSMIFQVRPLLIEGCPKPQ
EMEVQLPVEMDFEFDNQNDKGRDVTDIEDVQTEDPLIKASSSRVSLNCGC
GMSIPIEEVDGELDLDFINFKDDLKNRVATFFSRNGEGYSYNGGSHKSDG
WPEELDKILRALNVDVNDYNHCLVQKYRKGGKIGFHSDNENCYPKGNEIL
TVSIGEGIFSIKCERGSGMTNLNGRIHFKMPKGFQETHKHSVICTEGRIS
MTFRSTGKQAERAYVDDAEVSDDYNDEEGCISDDDEQVSSSFQINFDQVS
KMIKSGGSRNACLLVALADLMNSDKYLVLSLLVGADSSWIDWFIKDDGAG
FDDVVKAVTELNMRVNLYEKEKVTLINPDSSYNTGDLYLSDGHISSQKPS
NFEGIKTFGSTSFFSDFLTQFERLAGAGRVKYDARSERANALIESFQDNF
TGVFANKFKLQLERVIEDKSFEIVSITGFAGSGKSRGVQALMRGMFNKKS
SLVISPRKALLEDWRVKLKEGFKGRLKTFEVALKEIRCAELIIVDELTLF
PNGYLDLLLLSSKAQIVVLYDPMQARYFPRNDSFKLSSVHDVDRIEVKEY
LMYSHRMSKSMDMFDVNCLGSGELWEFHNRRFNEAAAMYKALKDYDCLIL
APSESKKIEMEKFGRSSTFGSAQGLSSDYVVIVVDQDAFITSQDHWIVAL
TRARKGIAFLYQGFRDVNVFAESHRGTLIGKVLLGKKVSEDHLIFGAGTV
LKKARIIREPESMKDEAMEIKLSGDPWLKGQLNLLENVELDDVEPREVDR
NDSPPRTHLNICTEDAFCELSEIKAREYREFLSPNDMSNQFNDMKTLREK
NWNNYVYVFETIYPRHQSSDDLTFFAAIQKRLLRSNPEKEARKLEKSWGI
GSIMFHELKRTLGLNPNVYIDEEVVNREFVQKRLNKSAKLIENHSGRSDP
DWRLDHFFLFMKSQLCTKFEKRFVDAKAGQTLACFSHQILTRFGVAFRTF
EKKFSANLPKTWYVHTMKNFDQLNLWACENVKEREGTESDYEAFDRSQDA
PILAFEILMLRFFNWPEDLIQDYKMIKLWMGCRLGAVAIMRFTGEFGTFF
FNTLVNMAFTVMRYHVNKESVIAFAGDDMYAAGFLKRRVDLEFALDQLTL
KAKVQFTRRPMFCGWYMTPMGIVKEPRLVLERWKIAEQKGNLRDVIINYA
LEVSYGYRLGEYLWEVLDNLESQQEIVRNIVKSKHLLPLKVRHFFSAVDN
ETLSTEFSEYMGQHPKFTESCGLECSLFKRA
```

Top Hit: Select seq gb|`AZM68728.1`|; `RNA-dependent RNA polymerase [Potato virus T]` ;	`Potato virus T` 
Percentage Identity: `50.24% `
Query Cover: `81%`
E-value: `0.0`
Country: `Bolivia`

Screen Shot: `https://files.slack.com/files-pri/TV2KYQBQA-F04E4QBCGTV/image.png`
```
RNA-dependent RNA polymerase [Potato virus T]
Sequence ID: AZM68728.1 Length: 1607 Number of Matches: 2
Range 1: 581 to 1606GenPeptGraphicsNext MatchPrevious Match
Alignment statistics for match #1
Score	Expect	Method	Identities	Positives	Gaps
978 bits(2527)	0.0	Compositional matrix adjust.	519/1033(50%)	691/1033(66%)	38/1033(3%)
Query  776   DEEGCISDDDEQVSS---------------SFQINFDQVSKMIKSGGSRNACLLVALADL  820
             DE G  S++ EQ+ S               S++I+F+ +   + SGG R  CLL ALA +
Sbjct  581   DENGANSEECEQLDSEDDVGSFEYEETKADSYEIDFEAILNRVNSGGLRGVCLLDALAKI  640

Query  821   MNSDKYLVLSLLVGADSSWIDWFIKDDGAGFDDVVKAVTELNMRVNLYEKEKVTLINPDS  880
               + + + LS+L+G D +W DWF+KD GA FDDV KAV++L++   +  KE     + + 
Sbjct  641   TGTKREITLSILLGRDGTWADWFLKDKGATFDDVFKAVSDLDLNCTICTKEGSFNAHVNR  700

Query  881   SYNTGDLYLSDGHISSQKPSN--FEGIKTFGSTSFFSDFLTQFERLAGAGRVKYDARSER  938
             +Y    LYL D H+S ++P    FE ++         DFL  FE+  GAG+ +Y+A +ER
Sbjct  701   NYKHNFLYLFDEHVSLERPKVMLFEQVRHQKI-----DFLGAFEKCPGAGKFRYEALAER  755

Query  939   ANALIESFQDNFTGVFANKFKLQLERVIEDKSFEIVSITGFAGSGKSRGVQALMRGMFNK  998
              + L  + +DN TGV ++KF    +    D   EI+ + GFAGSGK+RG+  +++ MFN 
Sbjct  756   GSLLASALKDNLTGVISSKFNWDPKCEFVDIEKEILVVAGFAGSGKTRGICQIVKSMFNN  815

Query  999   KSSLVISPRKALLEDWRVKLKEGFKG---RLKTFEVALKEIRCAELIIVDELTLFPNGYL  1055
             K +LV+SPRK L +DW   L    +    ++ TFE  L+ ++ + LI++DEL+L PNGYL
Sbjct  816   KKTLVLSPRKNLADDWVKNLANLHRPSHVKVMTFEAGLRRVQKSSLIVIDELSLMPNGYL  875

Query  1056  DLLL-LSSKAQIVVLYDPMQARYFPRNDSFKLSSVHDVDRIEVKEYLMYSHRMSKSMDMF  1114
             D+L+ ++ +A  + L+DP+QARY  ++D  ++S  +DVDRI+V +YL +S RMS  +D F
Sbjct  876   DMLINMNEEATFITLFDPLQARYHAKSDVLRVSPENDVDRIKVPKYLFFSKRMSSELDFF  935

Query  1115  DVNCLGSGELWEFHNRRFNEAAAMYKALKDYDCLILAPSESKKIEMEKFG------RSST  1168
             DV C    + WE H +++ E AA+++ +K  +  IL+PS     EM K+       +S T
Sbjct  936   DVRCSSDQKKWELHGKQYREPAALFRDIKGQEFTILSPSFETAREMSKYADIKDGCKSMT  995

Query  1169  FGSAQGLSSDYVVIVVDQDAFITSQDHWIVALTRARKGIAFLYQGFRDVNVFAESHRGTL  1228
             FG +QGL+ +  VIVVDQD   TS  HWIVALTR+R+G   L     D+    +  + ++
Sbjct  996   FGESQGLTVNKAVIVVDQDLVATSVLHWIVALTRSRQGFVILVHKVFDMKTLIQPVQNSI  1055

Query  1229  IGKVLLGKKVSEDHLIFGAGTVLKKARIIREPESMK-DEAMEIKLSGDPWLKGQLNLLEN  1287
             IG VL G KVS +HLI  AG  L +A I+ E E+ K  E  E  L GDPWLKGQL L ++
Sbjct  1056  IGLVLRGVKVSREHLINTAGKCLSEAEIVEELETFKRTEEDEDLLEGDPWLKGQLFLCQS  1115

Query  1288  VELDDVEPREVDRNDSPPRTHLNICTEDAFCEL-SEIKAREYREFLSPNDMSNQFNDMKT  1346
             VELD+V P E  R++SPPRTHL +  E     L S +KARE REF++P+  S QF D K 
Sbjct  1116  VELDEVTPEEPLRHESPPRTHLPLPVEGLTPLLMSNVKAREDREFITPSGWSKQFRDDK-  1174

Query  1347  LREKNWNNYVYV--FETIYPRHQSSDDLTFFAAIQKRLLRSNPEKEARKLEKSWGIGSIM  1404
                 +W N  Y   FETIYP+H++SDD+T +AAIQKR++ ++P + A KL+K   I + +
Sbjct  1175  -ENVDWRNVSYADAFETIYPKHEASDDITLWAAIQKRIVMADPFRNAMKLQKVEPISAEI  1233

Query  1405  FHELKRTLGLNPNVYIDEEVVNREFVQKRLNKSAKLIENHSGRSDPDWRLDHFFLFMKSQ  1464
             F+E+ + L LNP+V +D + V +EF++KRLNKS KLIE+HS RS  DW +DHFFLFMKSQ
Sbjct  1234  FNEMNKILLLNPHVSVDRDQVYKEFLRKRLNKSKKLIESHSERSSDDWPIDHFFLFMKSQ  1293

Query  1465  LCTKFEKRFVDAKAGQTLACFSHQILTRFGVAFRTFEKKFSANLPKTWYVHTMKNFDQLN  1524
             LCTKFEKRFVDAKAGQTLACFSH++LTRFG AFR FEKKF+ANLP +WY+HTMKNFDQLN
Sbjct  1294  LCTKFEKRFVDAKAGQTLACFSHKLLTRFGPAFREFEKKFTANLPPSWYIHTMKNFDQLN  1353

Query  1525  LWACENVKEREGTESDYEAFDRSQDAPILAFEILMLRFFNWPEDLIQDYKMIKLWMGCRL  1584
              W    V + EGTESDYEAFDRSQDA IL  EI  L+ F W +DLI DY+ +KLWMGCRL
Sbjct  1354  NWVINYVDQEEGTESDYEAFDRSQDAIILGLEIECLKLFGWDQDLIDDYRKLKLWMGCRL  1413

Query  1585  GAVAIMRFTGEFGTFFFNTLVNMAFTVMRYHVNKESVIAFAGDDMYAAGFLKRRVDLEFA  1644
             GA+AIMRFTGEFGTFFFNT+ N+AFT +RY++ +++VIAFAGDDMYA+G L+ R D E  
Sbjct  1414  GAIAIMRFTGEFGTFFFNTIANIAFTCLRYNITRDTVIAFAGDDMYASGKLEIRKDREDL  1473

Query  1645  LDQLTLKAKVQFTRRPMFCGWYMTPMGIVKEPRLVLERWKIAEQKGNLRDVIINYALEVS  1704
             L  LTLKAKVQFT +PMFCGWY+  MGIVKEPRLVLERW IAE+K  +    INY++EVS
Sbjct  1474  LAHLTLKAKVQFTEKPMFCGWYIKKMGIVKEPRLVLERWLIAERKKVIDQCFINYSIEVS  1533

Query  1705  YGYRLGEYLWEVLDNLESQQEIVRNIVKSKHLLPLKVRHFFSAVDNETLSTEFSEYMGQH  1764
             YGYRLGEYLWE  DNLE  Q IVR ++K K  LP  +R  F   +    S E  E MG  
Sbjct  1534  YGYRLGEYLWEYFDNLEDFQAIVRLVIKKKKQLPPAIRRIFETSNGVDFSGEVQETMGGE  1593

Query  1765  PKFTESCGLECSL  1777
              +   SCGL C+L
Sbjct  1594  GEHHGSCGLWCNL  1606


Range 2: 1 to 467GenPeptGraphicsNext MatchPrevious MatchFirst Match
Alignment statistics for match #2
Score	Expect	Method	Identities	Positives	Gaps
340 bits(873)	8e-91	Compositional matrix adjust.	193/471(41%)	276/471(58%)	31/471(6%)
Query  6    MSFAYRSPQEIFLQTIPQTYAEPLYKKTSESISKIIDDS-DFFKYSCSSEVKERLVKAGL  64
            MSF++R+P E+F+Q++P+ YAE  +K  + +     D     F ++CSS VKERL KAG+
Sbjct  1    MSFSFRTPAELFVQSLPKEYAEACFKSHAANFQIRSDKGIGLFDFACSSVVKERLTKAGI  60

Query  65   PISPFLYLIHSHPACKMLENYMLFVCAKDYIFKNKSVLISMKECKINILCRRNDVNIPFL  124
            P+S F    HSHPA KM+EN++L+    +Y+       IS+K+ K+  L +    ++   
Sbjct  61   PVSAFCNQEHSHPASKMIENHLLYNILPNYLNLKNYTAISIKDSKVRKLLKNGVDSLETF  120

Query  125  NRLVVAKDSFRYDEPSVCAINELAVKVRDSGRKSVFIHDEVHYWSMEDLNSFISISEVDN  184
            NRL   KD+ RY +P  C +++   +V  S R  +F+ DE+HYWSM  L+ F+  S V  
Sbjct  121  NRLFSCKDALRYVDPETCDMDKFIARVHHSTR--IFLFDELHYWSMNSLSDFLDRSNVKE  178

Query  185  ILCTVVFPPEILNGSKSSLNPELYSFKIVGDRVVFAPDGNYSESYTQPKRCDILRL-RGL  243
            +L T+VFP EIL GSK SLNPELY F+I   ++ F PDG  SESY+QPK CDIL++ R +
Sbjct  179  LLATIVFPIEILLGSKRSLNPELYEFEISRGKLHFFPDGCTSESYSQPKDCDILKVNRIV  238

Query  244  NVGNKKYAVTMLKSVGAHHLVFIKRMSYLNEPEVRFFDTPSAVDFNLLLPGRLKGSCKIR  303
                K ++V ++ ++GA+H+V IK  S+  + E RFFD  SA+  +LL+P R   + +IR
Sbjct  239  TKTGKIFSVELIHTIGANHMVMIKEGSFDVDSE-RFFDRSSALTTSLLMPTRAGKALRIR  297

Query  304  LEILKKMIAYLLALKKSDANSAVAKLRSLSVSEIYLDEITLAMHLGKVFENLKLQEAVGI  363
             + L ++I YL +LKK D +SA+AK+R  S   I+ DEI LA H+GK+FE L      G+
Sbjct  298  RKFLLRLIIYLFSLKKPDHHSAIAKIRQSSDDSIFCDEIMLADHVGKIFEKLDPASPFGV  357

Query  364  VGIFDRLLLFMKDVFLMDGLIEWSDRRKEESALRFISNLDSYSLSIETFVAKDRLMRS--  421
             G+FD L    KD+FL+DGL  WSDRRK E  + F+  LD  +  + T      +MRS  
Sbjct  358  KGVFDLLTSIFKDIFLLDGLFNWSDRRKSEKFVEFMRALDYQTNKVVTCTFSGGVMRSGF  417

Query  422  ------TQACESDSEG-----------------ESDGALENEINDRLPDPY  449
                     CE+ SEG                  S  AL   I DR P+PY
Sbjct  418  LAEFFLDNDCEA-SEGLDEVISRFDTFFDPKKEYSAHALRVNIKDRTPNPY  467
```

Node 1 PalmID analysis:
```
palmprint:

>NODE_1_length_7297_cov_16729.226821_g0_i0
TESDYEAFDRSQDAPILAFEILMLRFFNWPEDLIQDYKMIKLWMGCRLGAVAIMRFTGEFGTFFFNTLVNMAFTVMRYHV
NKESVIAFAGDDMYA

 catalytic motifs:

>NODE_1_length_7297_cov_16729.226821_g0_i0
   A:262-273(18.8)      B:318-331(21.4)      C:349-356(12.0)
   TESDYEAFDRSQ    <44> TGEFGTFFFNTLVN  <17> FAGDDMYA  [95]
   +|+||.+|| ||         |||..||++|||+|       |+|||| .
   lenDyskFDksq         SGdanTslGNTltn       vsGDDsvv
Score 62.1, high-confidence-RdRP: high-PSSM-score.reward-DDGGDD.good-segment-length.
```