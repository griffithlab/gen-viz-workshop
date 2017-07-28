---
feature_text: |
  ## Genomic Visualization and Interpretations
title: Genome Browsing and Visualization - UCSC
categories:
    - Module 1
feature_image: "assets/genvis-dna-bg_optimized_v1a.png"
date: 0002-01-02
---

The [UCSC genome browser](https://genome.ucsc.edu/cgi-bin/hgGateway) is a powerful web application for exploring the genomes of a variety of organisms in the context of annotation tracks. Let's start by navigating to the UCSC genome browser homepage at [http://genome.ucsc.edu](http://genome.ucsc.edu) and clicking on Genome Browser. Over the course of this tutorial we will be highlighting features with a transparent textbox, please pay attention to these as they are relevant to the discussion.

{% include figure.html image="/assets/UCSC/ucscHomePage.png" width="750" %}

### Selecting an organism and assembly

This will take us to the browser gateway where we can select the organism we wish to view as well as the assembly for that organism. For this tutorial we will be using the Febuary 2009 assembly of the human genome (GRCh37/hg19), let's go ahead and select that from the Human Assembly dropdown menu and click on "GO".

{% include figure.html image="/assets/UCSC/selectAssembly.png" width="750" %}

### Navigating around the genome

We are now in the genome browser for our chosen reference assembly, there is alot of information here, but let's start with the basics, navigating around. We can jump to a position or genome by entering them in the highlighted text box below, let's jump to **PIK3CA** which has coordinates **chr3:178,866,311-178,952,497**. After jumping to PIK3CA we can see in the image below that PIK3CA is 86,187 base pairs long and resides on the q arm of chromosome 3 (green text boxes). We can shift our viewing window with the arrow keys on the top left and we can zoom in and out using the zoom buttions on the right (red text boxes). In addition clicking and dragging inside the coordinate track within the browser will zoom to the window highlighted by such an action. Performing this action within any of the other tracks will shift the viewing window left or right. These are analogous to using the buttons mentioned above but allow for more user control.

{% include figure.html image="/assets/UCSC/navigating.png" width="950" %}

### Genome browser tracks

One of the features that makes the genome browser so usefull are the tracks displayed in the context of the genome assembly. Users can add and remove tracks by using the buttons below the the genome browser, clicking on the name of a track will allow for more fine grain control of that track and give additional information regarding that track such as version numbers. A number of tracks are turned on by default, but let's go ahead and hide all tracks to get a better sense of what's going on, click on the "hide all" button below the genome browser.

{% include figure.html image="/assets/UCSC/hideAll.png" width="950" %}

The browser should now be empty of tracks, let's go ahead and add the ensembl gene track, find Ensembl Genes under "Genes and Gene Predictions" and click on the link. You should see a page similar to the one below. Go ahead and set the Display mode to "full" and turn "Color track by codons" on. This will turn on ensembl gene annotations using ensembl version 75.

{% include figure.html image="/assets/UCSC/ensemblTrack.png" width="750" %}

As is exhibited below we can now see the full list of ensembl transcipts of PIK3CA based on the ensembl version 75 annotations of which there are 5. You can add as many tracks onto the viewer as you want but note that the available tracks will differ between species and even between assemblies.

{% include figure.html image="/assets/UCSC/ensemblTranscripts.png" width="1150" %}

{% include question.html question="Turn on the GTEx track, which tissue has the highest expression of PIK3CA? hint: try clicking on the track in the genome browser once it's enabled" answer='Cells - EBV-transformed lymphocytes have the highest expression at 11.3 RPKM.'%}

### BLAST-like alignment tool

Our discussion of the genome browser would not be complete without mentioning the BLAST-like alignment tool commonly refered to as [BLAT](https://genome.ucsc.edu/cgi-bin/hgBlat?command=start). As the name would suggest [BLAT](https://genome.ucsc.edu/cgi-bin/hgBlat?command=start) works similar to [BLAST](https://blast.ncbi.nlm.nih.gov/Blast.cgi), however it works in conjunction with the [UCSC genome browser](https://genome.ucsc.edu/cgi-bin/hgGateway) and aligns only to the specified genome assembly. Let's use BLAT to look at which section of the hg19 genome assembly the first primer pair in Supplemental Table S2 is amplifying, from the paper: ["Non-exomic and synonymous variants in ABCA4 are an important cause of Stargardt disease."](https://www.ncbi.nlm.nih.gov/pubmed/23918662). The forward primer used in this experiment is **TTTCTGAAATTGGGATGCAG** and the reverse primer is **GTTTTCCCAGGCAGAACAGA**. Go ahead and input these primers into [BLAT](https://genome.ucsc.edu/cgi-bin/hgBlat?command=start) in fasta format. Make sure to select the human hg19 reference assembly, then go ahead and click on submit.

{% include figure.html image="/assets/UCSC/blatInput.png" width="750" %}

BLAT will search the genome and output a table of possible matches between the genome assembly and the primer sequences. Unsurprisingly there are only two entries, one for each primer and each with 100% identity. Go ahead and click on "browser" to view one of these on the [UCSC genome browser](https://genome.ucsc.edu/cgi-bin/hgGateway). The second primer should be close by, try and zoom out to find it.

{% include figure.html image="/assets/UCSC/blatResults.png" width="750" %}

{% include question.html question="Which gene do these primers attempt to amplify?" answer='ABCA4'%}

### UCSC Table Browser
[BLAT](https://genome.ucsc.edu/cgi-bin/hgBlat?command=start) allowed us to get a region based on a sequence, but what if we want to do the reverse of that, to get a sequence based on a region. Fortunately the [UCSC genome browser](https://genome.ucsc.edu/cgi-bin/hgGateway) has a tool for that as well called the [UCSC Table Browser](https://genome.ucsc.edu/cgi-bin/hgTables). Let's get the DNA sequence for the gene APC using this tool. First navigate to the [UCSC Table Browser](https://genome.ucsc.edu/cgi-bin/hgTables) and input the gene APC. There are alot of options here but we only need to concern ourselves with a few. First make sure that the proper assembly is specified, in our case this should be hg19 (red boxes). Next because we want to return the sequence of the APC gene "Genes and Gene Precitions" should be selected under group, and let's go ahead and look for this gene in the "UCSC Genes" track (green boxes). Further the table should be set to "knownGene" (blue box).

{% include figure.html image="/assets/UCSC/tableBrowserInput.png" width="750" %}

Next go ahead and click on "paste list" under "identifiers (names/accessions)" and specify that **APC** is the gene we want the sequence for.

{% include figure.html image="/assets/UCSC/specifyAPC.png" width="450" %}

From there change the "output format" to "sequence" and click on "get output". The table browser will ask what type of sequence we want for APC, let's go ahead and get the protein sequence.

{% include figure.html image="/assets/UCSC/specifyProteinSequence.png" width="450" %}

{% include question.html question="How many transcript are there for APC in the UCSC known genes track, use the results from the table browser?" answer='5'%}
{% include question.html question='Try using BLAT on the protein sequence for entry "uc010jbz.3", which ensembl transcript does this entry correspond to?' answer='note to authors, find a better example'%}