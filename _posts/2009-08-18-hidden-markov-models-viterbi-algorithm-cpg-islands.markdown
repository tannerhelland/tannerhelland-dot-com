---
author: tanner_h
date: 2009-08-18 02:08:09+00:00
excerpt: Today's project is something new to this site - bioinformatics code!  I feel
  a tad ridiculous that it's taken me so many years to post code related to my field,
  but hey - better late than never. Read on to discover the awesomeness of Hidden
  Markov models, the Viterbi algorithm (also known as Viterbi paths), CpG islands,
  and how these all work together to help scientists locate genes.
layout: post
slug: hidden-markov-models-viterbi-algorithm-cpg-islands
title: Hidden Markov Models, the Viterbi Algorithm, and CpG Islands
redirect_from:
  - /1187/hidden-markov-models-viterbi-algorithm-cpg-islands-in-vb6
  - /vb6/hidden-markov-models-viterbi-algorithm-cpg-islands-in-vb6
---

![images/3D-SIM-4_Anaphase_3_color.jpg](images/3D-SIM-4_Anaphase_3_color.jpg)

*Anaphase, c/o [Lothar Schermelleh](http://commons.wikimedia.org/wiki/File:3D-SIM-4_Anaphase_3_color.jpg)*

If you don't know what the title of this page references, here are some Wikipedia links to get you started:

* [Hidden Markov models (including examples in Python)](http://en.wikipedia.org/wiki/Hidden_Markov_model)
* [Viterbi algorithm / Viterbi paths (including more Python examples)](http://en.wikipedia.org/wiki/Viterbi_path)
* [CpG islands](http://en.wikipedia.org/wiki/CpG_islands)

As a bonus, I'm including sections from my original write-up on this program (it began as a university project) to help explain the purpose and design of the code.

The algorithm implementations are quite fast, and the visual feedback is a big improvement over traditional command-line tools. I've also included a FASTA file with data from chromosome #1 in the human genome (bases 6000-12000, I believe), which you can use to test the project.

_(FYI, my original lab assignment link is here: [http://dna.cs.byu.edu/bio465/Labs/hmm.shtml](http://dna.cs.byu.edu/bio465/Labs/hmm.shtml).  It contains additional resources if you're looking to write your own HMM implementation.)_

_(FYI #2, this project has been cited in the following paper: [Spontaneo L, Cercone N. Correlating CpG islands, motifs, and sequence variants in human chromosome 21. 2011. BMC Genomics 12(Suppl 2):S10](http://www.biomedcentral.com/1471-2164/12/S2/S10).  I recommend it to anyone seeking a more in-depth explanation of this approach.)_

**INTRODUCTION**

CpG islands are "regions of DNA characterized by a large number of cytosine and guanine nucleotides linked by phosphodiester bonds. Additionally, CpG islands appear in some 70% of promoters of human genes (40% of mammalian genes). Unlike CpG sites in the coding region of a gene, in most instances the CpG sites in CpG islands are unmethylated if genes are expressed. This observation led to the speculation that methylation of CpG sites in the promoter of a gene may inhibit the expression of a gene." *(Wikipedia, retrieved Feb 2007)*

This project uses a Hidden Markov model to define the relationship between normal states (B) and island states (I) within a region of the human chromosome. Such an implementation is useful for gene finding, as CpG islands tend to appear near the promoters of important mammalian genes. The automation of this process is critical because such islands are impossible to locate by simply looking at a strand of DNA; they may cover several hundred bases and their C/G content may be only slightly higher than expected values.

**PROCEDURE**

This project is coded in the Microsoft Visual Basic 6.0 programming language. VB6 provides a relevant blend of native-code processing speed (allowing fast implementation of the HMM and associated visualizations) and a simple, flexible GUI. Visual feedback is a key element of this process, as finding CpG islands using HMMs may require some some experimentation with input values to maximize efficiency and accuracy of the algorithm. To my knowledge, previous implementations of HMM-based CpG detection code have been command-line only, making this visual implementation first of its kind. _(Additional note: if you are a Linux user, please note that this project works flawlessly under Wine 1.1.27, and likely earlier versions as well.)_

I will refer to the following screenshot as I walk through my implementation of a HMM.

![HMM_screenshot](images/HMM_screenshot-600x401.png)

**Step 1: Loading a FASTA file**

This routine isn’t of much interest, except to mention a programming quirk particular to VB6. A, C, G, and T entries from the FASTA file are reassigned into a byte array as the numbers 0, 1, 2, and 3. In VB6, raw byte processing is generally faster than string comparison and processing, because VB6 string functions are built around 2-byte ["WCHARs"](https://msdn.microsoft.com/en-us/library/gg269344%28v=exchg.10%29.aspx?f=255&MSPPError=-2147217396).

**Step 2: HMM Parameters**

The GUI allows the user to change 14 HMM-related parameters. Additionally, I have added an option to let the program estimate the eight state probabilities. This is a trivial computation to perform, but it helps increase the accuracy of the algorithm. The estimation of A, C, G and T's being emitted in a B state is computed by the percentage of their respective occurrences in the original FASTA data. I predict that given the low percentage of I states in a length of DNA, this method of estimating emission probabilities is relatively accurate.

Once these probabilities have been estimated, the I state probabilities are estimated by doubling C and G probabilities and halving A and T probabilities.

**Step 3: The HMM and Viterbi algorithms**

This step begins by moving all HMM parameters into look-up tables. The logs of these values are pre-calculated, allowing us to add them (instead of multiplying) for fast HMM calculations.

Next, all HMM probabilities are calculated and stored.

This is followed by a second loop run backward through the data that calculates all data necessary for the Viterbi algorithm. _(Additional note: this is not necessarily the most efficient way to do this, but the speed difference is negligible for sequences less than 100,000 bases long.)_

After all Viterbi data has been pre-calculated, the traceback part of the Viterbi algorithm can be run very quickly. _(Additional note: execution speed of this chunk of code is slightly reduced because I translate the states into a string and display that string in the textbox in the upper-right of the program window. This is mainly for convenience and satisfying curiosity. If speed is your goal, it is trivial to disable this part of the code.)_

**Step 4: The Sliding Window**

This step is where visual feedback becomes an essential component. In this project, I have chosen to display two graphs built from the HMM data; the top graph displays raw counts of C and G occurrences as compared to the expected value (where 0.5 is used as the expected ratio). The bottom graph displays the ratio of I and B states, and this data is used to predict the location of any CpG islands.

A noteworthy shortcoming of this implementation is that it is designed to only find the _most_ probable CpG island (instead of multiple islands). In a more formal implementation, returning any/all potential CpG island locations would be more useful.

_(Additional note: this step is my favorite part of the program. I find it to be well-implemented and graphically pleasing relative to the average bioinformatics tool.)_

**RESULTS**

By my estimation, the program's most accurate CpG prediction for this FASTA file is bases 2018-2045 (which corresponds to bases 6018-6045 in the original data). Multiple runs with varying parameters generate similar estimates. Adjusting the sliding window size doesn't have a large effect on the estimates, although larger windows will (unsurprisingly) result in larger CpG island predictions. The percentage of I states varies dramatically; certain parameters result in levels as high as 30-40% while others are less than 5%. For my best estimate (above), the percentage of I states was 22%.

Finally, code execution is swift - typically a matter of seconds - and if the text display in the top-right is disabled, the program runs more-or-less instantaneously on current hardware.

**[Download the sample app and source code from GitHub](https://github.com/tannerhelland/vb6-code/tree/master/Hidden-Markov-model)**
