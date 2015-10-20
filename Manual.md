# Using SCell

**SCell** is an an integrated software tool to analyze single-cell RNA-seq datasets.

SCell can perform quality filtering, normalization, feature selection, iterative dimensionality reduction, clustering, and gene-expression gradient estimation from large ensembles of single-cell RNA-seq datasets.

For the purpose of this manual, we used single cell RNA-seq data from from three different human developing neocortex samples:

| Sample     | Age          |
| -----------|--------------|
| O5         | GW10         |
| O1         | GW 20.5      |
| O2         | GW 20.5      |
| S44        | GW 24.5      |
| S46        | GW 23.5      |


### Loading data and metadata.

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/LoadData.png" width=300>


___Counts Table Example___

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/CountsSample.png" width=550>

___Metadata Table Example___

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/MetadataSample.png" width="300">

## Library QC

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/QCButton.png" width="350">

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/libraryComplexityProgress.png" width="300">

___Sample Lorenz Curves___

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/Lorenz.png" width="300">

___Per-Cell Gene Expression Distribution___

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/GeneExpressionQuantiles.png" width="300">

___Simpson Diveristy and PRESEQ Coverage Boxplots___

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/QCBoxplots.png" width="300">


Select Lorenz or PRESEQ from the dropdown menu and set a threshold, then click on the **Filter by** button to exclude cells that do not pass the selected test. This will cause libraries that do not pass the specified test to be deselected and excluded form the analysis. You may also de-select libraries that you wish to exclude based on other criteria, such as live/dead image call or number of genes detected.

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/FIlterByButton.png" width="300">

#### Gene Panel Selection and Library Normalization

SCell can perform normalization of your libraries in several ways:

a) Normalization by Library Size (counts per million)

b) Cell-cycle regression based on cyclin/CDK expression

c) Mutual background

#### a. Feature Selection and Normalization by Library size (CPM)

To normalize samples by library size and select meaningful genes for analysis, follow these steps:

1. In the main panel, select the **Normalize selected libraries** button to launch the **normalization tool** window.

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/NormalizeButton.png" width="300">

2. Once in the normalization tool, click on **Select Genes**.

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/normTool.png" width="250">

3. SCell will perform gene variance and zero-inflation analysis, and a **Gene Selection Tool** window will be launched.

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/geneVarianceProgress.png" width="250">

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/ZIprogress.png" width="250">

Here, you can set an Index of Dispersion threshold for genes, as well as a threshold for the fraction of cells expressing a gene. You can also set a zero-inflation power threshold. On the lower panel, you can see and export a list of the genes and their values for these metrics.

4. Once you have chosen the thresholds for your gene panel, click **Use these genes**. Only the genes that meet your criteria will be used for further analysis.

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/GeneSelection.png" width="350">

5. Back in the **Normalization Tool** window, click **Done**.

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/normToolDone.png" width="250">

Your libraries are now normalized by library size (in counts per million) and you can proceed to data analysis.

#### b. Normalization by Human Cyclins and Cyclin-Dependent Kinases (Cell Cycle Regression)

SCell can estimate the percentage of genome-wide variance explained by cyclin/CDKs, the specific cyclins/CDKs that explain the highest percentage of variance and the genes that correlate most strongly with cyclin/CDKs.

To regress out the effect of cell cycle on gene expression (remove unwanted variation due to cell cycle state) , in addition to normalizing libraries by size, follow these steps:

1. Follow steps 1 to 4 from the **Normalization by Library size (CPM)** instructions, in order to select genes to include in the analysis.

2. On the **Normalization Tool** window, check the **Human cyclins/CDKs** box, then click **Normalize samples**.

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/cyclinNormalization.png" width="250">

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/cyclinNormProgress.png" width="250">

A barchart is produced, showing Cyclin/CDK contribution to variance in gene expression.

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/cyclinCorrelations.png" width="400">

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/saveCyclinCorr.png
" width="300">   <img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/saveGeneCorrToCyclins.png
" width="300">   

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/cyclinCorrTSV.png
" width="300">    <img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/geneCorrWithCyclinsTSV.png
" width="300">

After specifying a location to save the gene-cyclin correlation and cyclin-cyclin correlation TSV files, normalization will take place. Allow a few minutes for its completion.

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/normalizationCyclins_Progress.png
" width="300">

Once the libraries have been normalized, you will be taken back to the Main Panel, where you can proceed with the analysis of the selected, normalized libraries.


SCell can produce counts normalized by any combination of:
1. Cyclins and cyclin-dependent kinases (a model of cell cycle state)
2. A user supplied count matrix (enabling an arbitrary set of controls).

## Data Analysis
On the main panel, select **Analyze selected libraries** to perform PCA on the QC-filtered and normalized libraries.

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/AnalyzeButton.png" width="350">

#### PCA Sample Scores and Gene Loading Plots

Selecting **Analyze selected libraries** will produce two plots: a PCA score plot, and a gene loading plot.

___Sample Scores Plot___

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/PCAScores.png" width="300"> <img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/CellAnnotations.png" width="300">

___Gene Loadings Plot___

###### Explore strongly loading genes.

**Neuronal** genes loading negative PC1.

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/PCAGenesNeuronal.png" width="300">
<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/PCAGenesNeuronal2.png" width="300">

**Radial Glia** marker genes loading PC1 positive.

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/PCAGenesRG.png" width="300">
<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/PCAGenesRG2.png" width="300">

Hover over genes in the Gene Loading plot to view their gene symbol, mean expression, IOD and the percentage of cells expressing the gene in the **Gene Annotations** panel.

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/GeneAnnotations.png" width="300">

###### Refresh PCA Axes

Enter the axes you would like to plot, and select **Refresh PCA axes** to retun new Sample Scores and Gene Loadings plots.

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/refreshPCAaxes.png" width=350>

###### Varimax Rotation

You can choose to apply Varimax Rotation to post-process the PCA. This rotates the PCA axes in order to reduce the number of genes strongly loading two axes.

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/varimaxRotate.png" width=350>


#### Visualizing Gene Expression across cells.

Enter the name of the gene whose expression you want to visualize. Select **surface** or **contour**, and a regression method from the drop-down menu, then click on **Plot expression** to generate a plot of gene expression across cells.


<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/VisGeneExpressionButton.png" width="300">

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/VIMExpressionContourPlot.png" width="300"> <img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/VIMExpressionSurface.png" width="297">

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/DCXExpressionContourPlot.png" width="300">
<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/DCXExpressionSurfacePlot.png" width="297">

#### Clustering Cells

SCell can implement five different clustering  algorithms: k-means, Gaussian mixture, Minkowski weighted k-means, or DBSCAN.

Select a clustering algorithm from the drop-down menu, then click  ** Cluster cells**.

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/ClusterMenu.png" width="300">

A new window will prompt you to enterthe desired number of clusters, as well as the number of replicates and distance metric to use. Enter these parameters, then click **Done** to cluster.

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/kmeansParameters.png" width="302">

######K-means Cluster Assignments

A plot will appear with samples colored according to their assigned cluster. In the main panel, you can see information about the samples by hovering over them on the plot. You can also select samples by clicking on them, and they will be added to the **Working sample list**, which you can export or use to run a new iteration of PCA.

<img src= "https://dl.dropboxusercontent.com/u/9990581/Scell/SCell_Screenshots/kmeansClusters.png" width="600">


#### Fitting a Minimum Spanning Tree

Once cells have been clustered, SCell can compute a Minimum Spanning Tree to predict lineage relationships across clusters.
Select a "root" cluster, then click **Fit Tree** to create a minimum spanning tree.

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/MSTButton.png" width="300">

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/MST_withVarimax.png" width=300>

######Visualize Gene Expression Across MST Clusters
<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/VisualizeExpressionButtonPAX6.png" width=350>

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/PAX6Surface.png" width=350>

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/PAX6expressionClusters.png" width="300"> <img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/PAX6ExpressionClusters2.png" width="295">

### Iterative PCA

SCell can perform PCA on a subset of libraries from the first round of analysis.

Select the cells form the group you would like to further analyze on the cell cluster plot.

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/iterativePCAselect.png" width="400">

The selected samples will appear on the **Working Sample List** in the main panel. Click **Refresh PCA using samples** to perform PCA on the selected libraries only.

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/iterativePCArefresh.png" width="400">

___New Gene Loading Plot___

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/iterativePCAplot.png" width="400"><img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/iterativePCAsampleList.png" width="400">

___New Gene Loading Plot___

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/iterativePCAsampleScores.png" width="600">

You can visualize the expression of genes across this subset of samples, as well as perform clustering and compute a new minimum-spanning tree once again to further analyze this cell group.

#### Gene Ontologies

SCell can Query DAVID for gene ontologies associated with the genes selected on the PCA gene loading plot.

On the **Working gene list** panel, add genes to the list by selecting them on the gene loading plot, or enter them manually. You can also choose a percentile of genes from one principal component, loading positively or negatively.

Once you have selected a set of genes, click **Compute gene ontology** to load these genes into the **GO map** tool.

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/geneOntologyButton.png" width="295">

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/geneOntologyProgress.png" width="295">

Enter an e-mail address registered with DAVID, or select **Register with DAVID** to go to the registration webpage.
Once a valid registered address has been entered, click **Query DAVID** to return a map of ontologies associated with your gene list.

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/GOmapWindow.png" width="400">
