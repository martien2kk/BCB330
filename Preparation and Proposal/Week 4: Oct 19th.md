### Oct 19th, 2022  
{Keren}  
Created and Submitted proposl  
   
#### Introduction  
Since its legalization in Canada and other countries around the world, the marijuana industry
has been blossoming and becoming an important part of the economy. As we all know, marijuana
refers to the dried leaves, flowers, stems, and seeds from the hemp plant, Cannabis sativa
(Chiginsky et al., 2021) —it has been a popular news topic recently. Instead of being secretly
traded in the underground market, now marijuana could be legally grown in industrial agriculture
facilities. However, not a lot of research regarding the professional growing of medical or
recreational marijuana has been observed in published journals. Specifically, there is a lack of
detailed information regarding the viruses that could possibly infect Cannabis sativa. Thus, this
project seeks to computationally sequence and analyze some viruses or viroids that could cause
plant disease and even plant death in Cannabis sativa. The research question to be answered is:
What are the viruses infecting Cannabis sativa? This could be helpful for the Marijuana industry
in terms of preventing the spread of Cannabis viruses, minimizing plant loss, and maximizing the
profit for the Cannabis sativa grown.  
   
#### Goals of Project
The primary goal of this research project is to identify novel RNA virus infecting Cannabis
by retrieving raw sequence data from the National Center for Biotechnology Information (NCBI)
Sequence Read Archive (SRA) or similar database, and to search for virus-like sequences using
bioinformatic tools such as Serratus.io. Also, existing sequences of known viruses that infect
Cannabis could be utilized as a query to search for novel viruses based on percentage identity.
The purpose of these goals is to expand the knowledge on known marijuana viruses to help hemp
growers prevent production loss, and to expand the related database to serve as a foundation for
future attempts at Cannabis virus prevention and surveillance.  
   
#### Background
Cannabis sativa, also known as marijuana, is a herbaceous plant with an Eastern Asian
origin. It has been a crucial component to traditional medicine, food, oil and industrial fiber for
quite a long time (Andre et al., 2016). However, recent interest in the plant is more revolved
around its recreational use as both a stimulant and a depressant. After its legalization in Canada
in 2018, the Cannabis industry quickly flourished and became a major contributor to the
agri-food sector. In fact, according to the Government of Canada, merely one year after the
decriminalization of marijuana, a significant $1.7 billion was added to licensed Cannabis
producer receipts (2020). Similarly, a report by Deloitte Canada comments that since 2018, the
Canadian National GDP has increased by a total of $43.5 Billion due to the marijuana market
(Malkani, 2022). More than 16 million packaged Cannabis units were sold across Canada, where
the total comprised 58% dried Cannabis, 24% edible Cannabis and 17% Cannabis extracts
(Health Canada, 2022). This is paralleled by the expansion of agricultural land that is dedicated
for Cannabis farming. Particularly, a 2021 report by Health Canada mentions that indoor and
outdoor Cannabis farming area is about 1,756,642m2 and 7,130,900m2
respectively (2022).  
   
From the statistics mentioned above, it is evident that Cannabis sativa is truly an imperative
crop in the Canadian market. Thus, efficient disease identification and management in the hemp
plant would really help to increase crop yield and reduce profit loss. According to the
government of British Columbia, the top three pathogens that affect the marijuana crop are
bacteria, fungi and viruses (2021), the last of which will be the focus of this study. Plant viruses
are an emerging agricultural risk around the world; it is estimated that global crop yield losses
due to viruses sum up to a total of $30 billion in 2022 (Hilaire et al., 2022). Although specific
data for Cannabis itself is currently unavailable due to the lack of research, it is not hard to
imagine that this herbaceous plant is also significantly impacted by viral pathogens.
Consequently, this study will attempt to contribute to the understudied topic of Cannabis virus,
help with the establishment of disease regulation in hemp, and aid the development of prevention
strategies.  
   
#### Preliminary Literature Review
There are limited reports or articles that present confirmed cases of marijuana viruses, but
in the literatures that do exist, the most frequently mentioned viruses include: the Beet Curly Top
Virus (BCTV), the Cannabis Cryptic Virus (CCV), the Tobacco Streak Virus (TSV), the Lettuce
Chlorosis Virus (LCV), and the Hop Latent Viroid (HLVd).
Firstly, according to an article published in Frontiers in Agronomy, one of the first viruses
reported in hemp is the BCTV, a member of the genus Curtovirus in the family Geminiviridae
(Chiginsky et al., 2021). This virus mostly infects sugar beets, but could also be found in other
species such as tomato, pepper, spinach, etc. It is a DNA virus that has a circulative propagative
way of transmission, that is, transmission by a vector species. Particularly, BCTV is only known
to be transmitted through the beet leafhopper insect. The leafhopper is not affected by the virus,
but becomes a carrier and transfers it to the plants they feed on through salivary glands. The
article identifies two major strains of BCTV, Worland (Wor) and Colorado (CO), which have
similar symptoms: up-curled and yellow hemp leaves and hindered photosynthesis abilities.
Another Cannabis virus discovered in this article is the TSV, a positive-strand RNA virus
in the family Bromoviridae, and genus Ilarvirus (Chiginsky et al., 2021). As the name suggests,
TSV is a virus that generally affects tobacco plants, but is also able to infect a wide range of
species such as peanuts, sunflower, soybean, cranberry, and of course, hemp. The authors
mention that the TSV they sequenced is quite variable compared to the sequences in the
GenBank database. Hence, a new genotype of the species might have been discovered. TSV
could be transmitted by seed and pollen to the next generation and usually has symptoms like
necrosis and chlorosis, meaning yellow due to lack of chlorophyll, in the leaves (Dijkstra, 1983).
One more early reported virus is the CCV, which is a double-stranded RNA virus and part
of the Partitiviridae family (Righetti et al., 2017). CCV is transmitted vertically, in other words, it
is passed through seeds to the next generation of plants. This virus is commonly detected with
the presence of another virus, namely the Hemp Streak Virus (HSV), but no symptom is able to
be identified with the presence of CCV alone. Researchers predicted that CCV could be able to
worsen or alter the viral symptoms of HSV in hemp plants. It might also be able to interact with
other types of pathogens like fungi to trigger disease symptoms.
    
Furthermore, the LCV is a positive-sense, single-stranded RNA virus and a member of
the Closteroviridae family (Hadad et al., 2019). The main characteristics of LCV infected plants
include nutrition deprivation, interveinal chlorosis, brittleness, and occasional necrosis. As
expected by its name, LCV primarily infects lettuce plants, but could also be recognized in other
species including beans, tomatoes and papayas. It could be transmitted from an infected
marijuana plant to a healthy marijuana plant via pests, especially the whitefly Bemisia tabaci.
Lastly, unlike the other ones mentioned, the HLVd is an RNA-based viroid as opposed to
a virus since it is missing a protein coat (Warren et al., 2019). This viroid is most frequently
observed in hop plants, and is often transmitted through agricultural tools and equipment such as
pruners. Symptoms of Cannabis plants infected with HLVd range from malformation or chlorosis
of leaves, to stunting and brittle stems.  
    
While knowledge of Cannabis virus that could be extracted from the current literature is
limited, the above information could be used to help with the understanding of the field. It
provides insight into the research to be done and serves as a basis for this investigation proposal.
By the end of this study, the hope is to expand the list of marijuana viruses identified and
enhance the related genomic database.  
    
#### Methodology
To begin with, the NCBI SRA (1) database will be used to identify runs associated with
Cannabis sativas. As of October 2022, there are a total of around 9000 results, but for the
purpose of this study, the RNA-seq subset of the SRA will be the main focus. Then, the
accession ID of the list of raw sequences will be downloaded in a text file. Each run will be
entered into the Explore RdRP Search tool (2) in Serratus.io (includes runs from 2013-2020), or
a similar bioinformatic tool for identifying RNA-based viruses. The best matches with alignment
identity greater than 70% and a bit lesser than 100% will be reviewed and their rdrp fasta files
will be downloaded. Next, contigs from these fasta files will be pasted into the NCBI Open
Reading Frame (ORF) Finder (3) with the start codon to use set to “Any Sense Codon”. The
ORFs will be used to BLAST (blastp) against the non-redundant protein (nr) database (4).
Following the blast, any outcome that has a percentage less than 70% could mean that a novel
virus has been identified. The Serratus PalmID tool (5) will also be used for further analysis. To
complete the steps mentioned above systematically, the Serratus SQL (6) server will be accessed
through pgadmin4 (7). Serratus will be queried via SQL (R-family) and data collected will be
stored in an Excel file. These methods are chosen as they are fast and clear ways of identifying
novel viruses and performing bioinformatic analysis, and efficiently help to achieve the goals of
this investigatio
