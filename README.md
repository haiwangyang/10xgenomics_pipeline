# 10xgenomics_pipeline
single cell analysis to figure out the cell type of expressed pacbio novel isoform

## Data can be found in biowulf:
/data/Oliverlab/fastq/scRNA-seq/SV_1_10X_Te

## Step 1 Make reference:
https://support.10xgenomics.com/single-cell-gene-expression/software/pipelines/latest/advanced/references#single
sinteractive --mem=50g --cpus-per-task=20
module load STAR/2.5.3a
module load cellranger/2.0.2
cellranger mkref --genome=dmel_v3_plus_pacbio --fasta=../fa/dmel.fasta --genes=dmel.v3_plus_pacbio.gtf

## Step 2 Run cellranger count:
swarm -f cellranger.swarm -g 40 -t 16 --module cellranger/2.0.0 --time 24:00:00
cellranger count --id=testis1 --transcriptome=/data/yangh13/python/packages/CRoS/CRoS/species_FB2017_03/gtf/dmel_v3_plus_pacbio --fastqs=/data/Oliverlab/fastq/scRNA-seq/SV_1_10X_Te --sample=SV_1_10X_Te --localcores=16 --localmem=55
  
## Step 3 Downstream Analysis with Seurat Pipeline:
Settings are here: https://github.com/haiwangyang/PGMF/blame/master/PGMF/R/single_cell_analysis.testis1.seurat.Rmd
Based on this example: http://satijalab.org/seurat/pbmc3k_tutorial.html
 
