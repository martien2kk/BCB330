### Dec 21st, 2022
By: `Keren`

Previously, the main domains of the three ORFs of `SRR7630408` has been analyzed with InterPro. 
For better processing, these information with be turned in to GTF (Gene Transfer Format). 

According to `http://mblab.wustl.edu/GTF22.html`:
"GTF stands for Gene transfer format. It borrows from GFF, but has additional structure that warrants a separate definition and format name. "

Structure is as GFF, so the fields are:
`<seqname> <source> <feature> <start> <end> <score> <strand> <frame> [attributes] [comments]`

For `NODE_1` of `SRR7630408`:
```
Node_1 ORF_Finder Node_1                       0    7297 . + .; "Node_1"
Node_1 ORF_Finder 5UTR                         0    54   . + .; "5UTR"; 
ORF1   ORF_Finder CDS                          55   5400 . + 1; "ORF1";
ORF1   InterPro   Viral_methyltransferase      47   347  . + 1; "Viral_methyltransferase";
ORF1   InterPro   Oxoglu_Fe_dep_dioxygenase    668  757  . + 1; "Oxoglu_Fe_dep_dioxygenase";
ORF1   InterPro   Viral_RNA_helicase           976  1209 . + 1; "Viral_RNA_helicase";
ORF1   InterPro   RNA_dependent_RNA_polymerase 1340 1668 . + 1; "RNA_dependent_RNA_polymerase";
ORF24  ORF_Finder CDS                          5273	6289 . + 2; "ORF24";
ORF24  ORF_Finder Viral_movement_protein       5298	5463 . + 2; "Viral_movement_protein";
ORF39  ORF_Finder CDS                          6042	6713 . + 3; "ORF39";
ORF39  ORF_Finder Coat_protein                 6090	6263 . + 3; "Coat_protein";
Node_1 ORF_Finder 3UTR                         6714 7297 . + .; "3UTR";
```

However, after checking, the example on gggenes shows the following:
```
   molecule  gene  start    end  strand orientation
1   Genome5  genA 405113 407035 forward          -1
2   Genome5  genB 407035 407916 forward          -1
3   Genome5  genC 407927 408394 forward          -1
4   Genome5  genD 408387 408737 reverse          -1
5   Genome5  genE 408751 409830 forward           1
6   Genome5  genF 409836 410315 forward          -1
```

Reformatted info: 
```
```
