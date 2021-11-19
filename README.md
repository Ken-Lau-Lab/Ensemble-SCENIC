# Ensemble-SCENIC

## 1. Hopper

Hopper implements the greedy k-centers algorithm, iteratively generating a farthest-first traversal of the input data.\
To sketch a dataset, import the hopper class, and first pass the dataset into the Hopper constructor.

## 2. SCENIC Protocol

This notebook describes how to run a pySCENIC gene regulatory network inference analysis.\
See also the associated publication in Nature Protocols: https://doi.org/10.1038/s41596-020-0336-2.

### Installation of pySCENIC and dependencies
The environment of SCENIC Protocol can be installed through the included scenic_protocol.yml with the following command:
```console
conda env create -f scenic_protocol.yml
python -m ipykernel install --user --name=scenic_protocol
```

### Workflow
Briefly, the SCENIC pipeline consists of three steps. First, candidate regulatory modules are inferred from coexpression patterns between genes. Next, coexpression modules are refined by the elimination of indirect targets using TF motif information. Finally, the activity of these discovered regulons is measured in each individual cell and used for clustering.


## 3. Reuglons Aggregation

This notebook aims to aggregate results across pySCENIC runs. There are two items of interest: the regulons themselves (TFs) and the target genes of each regulon. First, we do an outer join, keeping all regulons. Then, we count the number of times each regulon occurred. This will give a distribution and some idea of how much variability there is. You can then select a threshold as needed. For example, in a 100x run, you'll find some regulons that occur 100% of the time, and others that only occur once (obviously these are low confidence). In this notebook, we took a threshold of 80% occurrence. As for the target genes, we calculated the average gene weight for each target gene in each regulon.

## 4. AUCell

Lastly, the activity of these regulons is quantified via an enrichment score for the regulon’s target genes (AUCell). An area under the curve (AUC) metric is used to assess significant recovery of a set of genes for a given whole-genome ranking. The AUC metric measures the relative biological activity of a regulon in a given cell.

