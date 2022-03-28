# precision_toxicology

Analysis of scRNA-seq data of primary human hepatocytes (PHHs) to uncover cellular heterogeneity in a seemingly homogeneous cell type and its functional relevance for metabolizing a phenotyping drug cocktail.

Background

The current state-of-the-art to assess drug efficacy, safety and toxicity in the early phases of drug development is to perform bulk analyses. This approach assumes a homogeneous population of cells that respond uniformly to xenobiotics. However, it remains unclear whether individual cells possess the same metabolic capacity for drug detoxification and biomolecule synthesis, especially in response to environmental factors. For instance, chronic lipid accumulation in liver has been associated to an overall diminished hepatic capacity for drug metabolism, yet its effects remain to be dissected at single-cell resolution. 

Therefore, we here use single-cell RNA sequencing on PHHs from four human donors to disentagle cellular heterogeneity in hepatocytes and its role in metabolizing a phenotyping five-drug cocktail. Moreover, we mimic chronic lipid accumulation in vitro by incubating cells with free fatty acids. Thereby, we investigate the impact of hepatic steatosis, a hallmark of non-alcoholic fatty liver disease (NAFLD), on the overall cellular heterogeneity and its impact on drug-related metabolic capacity.

Data accessibility

The raw data can be found at: https://www.ebi.ac.uk/arrayexpress/experiments/E-MTAB-11530

Preprocessing

Reads were aligned to GRCh38 and counted using 10X Genomics Cellranger 4.0.0 with standard parameters individually for each batch

Analysis pipeline

1. Filtering

    Cells were kept if they had at least 1,000 counts and 500 genes.
    Genes were kept if they were present in at least 5 cells and had fewer than 5 million reads.
    Scrublet was used to identify doublets, where a lenient cutoff of 0.15 was used, leading to 1.7% of cells being annotated as doublets and subsequetly being removed. 
    Cells with more than 1% mitochondrial reads were removed.

2. Normalisation

    Scran was used for normalization with min.mean = 0.05

Additional filtering: after normalization, cells with more than 20,000 normalized counts were removed.

3. Batch correction

    Harmony was used to integrate the cells from the two batches.

4. Downstream analysis

    Visualisation, clustering and differential expression analysis was done using scanpy functions
    Analysis of the 4 human donors separately to find similar hepatocyte subgroups in all donors
    Cluster annotation based on differential expression and marker genes
    Gene ontology analysis using gprofiler and ShinyGO
    Gene set enrichment analysis using gseapy
    Calculation of transcriptional variability per subgroup and treatment condition by using the coefficient of variation calculated on log-transformed data
    Comparison to in vivo data sets from Aizarani et al., 2019 and MacParland et al., 2018
    Custom code for further visualization

