---
feature_text: |
  ## Genomic Visualization and Interpretations
title: Introduction to ProteinPaint
categories:
    - Module 1
feature_image: "assets/genvis-dna-bg_optimized_v1a.png"
date: 0001-07-01
---

[ProteinPaint](https://pecan.stjude.org/proteinpaint) is a tool made available as part of the [PeCan Data Portal](https://pecan.stjude.org/home). The principle goal of the this data portal is to facilitate exploration of childhood cancer genomics data. However, some tools such as ProteinPaint are generally useful for visualizing the recurrence of any set of variants in a gene in the context of protein domains and other information.

This section will provide a brief introduction to ProteinPaint features and demonstrate its use with a few examples and exercises.

The tool is entirely web based. First navigate to the tool's homepage: [ProteinPaint](https://pecan.stjude.org/proteinpaint). Note that is has its own [simple tutorial](https://docs.google.com/document/d/1JWKq3ScW62GISFGuJvAajXchcRenZ3HAvpaxILeGaw0/edit). Go through the following exercise to explore the functionality of this resource.

* Choose an example gene to explore.
* Select the gene name (top left) to view a summary of the gene.
* Use the CONFIG option to change between display modes.
* Select pre-loaded data to display (Pediatric, COSMIC, and ClinVar). Select COSMIC for this example. Use the ABOUT popup to learn more about each data source. 
* Zoom In on a mutation hotspot and navigate around that region. Once done, Zoom Out x50 to return to a view of the entire gene.

Use the Tracks button to view the list of available tracks and turn on the RefGene track. 

Under the More menu, Select a region to highlight. Select a region contain a hotspot mutation. 

Use the + add protein domain button to add a custom domain of interest.

Mouse over the gene diagram to view details on individual domains and amino acid positions.

Select specific variants to learn more about what diseases they occur in. For example, load ERBB2 and the COSMIC track. Two of the most common mutations are S310F and L755S. Select both of these. Which is more common in breast cancer? Use the `List` option to learn more about individual variant observations.

Use the Microarray and RNA-seq expression tracks (if collapsed these appear as <em>e</em> in the track list) to determine what kind of childhood tumors tend to have high ERBB2 expression.

Lets load a custom data set into ProteinPaint. We'll use CIViC's list of VHL variants as an example. To get that list go to www.civicdb.org, select `SEARCH`, select the `Variants` tab, create a query where `Gene` `is` `VHL`, and hit the `Search` button. Once the query completes, use the `Get Data` option to `Download CSV`. Save this file. Rename it to CIViC-VHL-Variants.csv. We'll need to reformat the data before inporting into ProteinPaint.

Open this file in R and perform the following clean-up.

```R
# Load the data downloaded from CIViC
setwd("~/Downloads/")
dir()
x = read.csv(file = "CIViC-VHL-Variants.csv", as.is=1:4)

# Store only the variant names that we will parse for protein coordinates
vhl_variants1 = x[,2] 

# Tidy up the names to remove the c. notations
vhl_variants2 = gsub("\\s+\\(.*\\)", "", vhl_variants, perl=TRUE)

# Limit to only those variants with a format like: L184P
vhl_variants3 = vhl_variants2[grep("^\\w+\\d+\\w+", vhl_variants2, ignore.case = TRUE, perl=TRUE)]

# Store the variant names for later
vhl_variant_names = vhl_variants3

# Extract the amino acid position numbers
vhl_variant_positions = gsub("\\D+(\\d+)\\D+", "\\1", vhl_variants3, perl=TRUE)

# Create a variant types list
# M=MISSENSE, N=NONSENSE, F=FRAMESHIFT, I=PROTEININS, D=PROTEINDEL, S=SILENT
types = vector(mode = "character", length = length(vhl_variant_names))
types[1:length(vhl_variant_names)] = "M"
types[grep("\\*", vhl_variant_names, ignore.case = TRUE, perl=TRUE)] = "N"
types[grep("fs", vhl_variant_names, ignore.case = TRUE, perl=TRUE)] = "F"
types[grep("ins", vhl_variant_names, ignore.case = TRUE, perl=TRUE)] = "I"
types[grep("del", vhl_variant_names, ignore.case = TRUE, perl=TRUE)] = "D"

# Store the values we care about in a new data frame
vhl_variants_final = data.frame(vhl_variant_names, vhl_variant_positions, types)
head(output)

# Create the final format strings requested for ProteinPaint of the form: R200W;200;M
format_string = function(x){
  t = paste (x["vhl_variant_names"], x["vhl_variant_positions"], x["types"], sep = ";")  
  return(t)
}
output = apply(vhl_variants_final, 1, format_string)

# Write the output to a file
write(output, file="CIViC-VHL-Variants.formatted.csv")
```

Open the resulting file (CIViC-VHL-Variants.formatted.csv). In ProteinPaint use the + button to add add, and choose the SNV/Indel option. Then paste the variant formatted in R into that box. Compare the VHL variants in CIViC compared to those in ClinVar.

