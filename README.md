# Using SCell

**SCell** is a tool for analyzing single-cell gene expression data.

## Load data and meta-data.

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/LoadData.png" width=300>


___Counts Table Sample___

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/CountsSample.png" width=550>

___Metadata Table Sample___

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/MetadataSample.png" width="300">

## Sample QC

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/libraryComplexityProgress.png" width="300">

___Sample Lorenz Curves___

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/Lorenz.png" width="300"> 

___Per-Cell Gene Expression Distribution___

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/GeneExpressionQuantiles.png" width="300"> 

___Simpson Diveristy and PRESEQ Coverage Boxplots___

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/QCBoxplots.png" width="300">


Select Lorenz or PRESEQ from the dropdown menu and set a threshold, then click on the **Filter by** button to exclude cells that do not pass the selected test. This will cause libraries that do not pass the specified test to be deselected and excluded form the analysis. You may also de-select libraries that you wish to exclude based on other criteria, such as live/dead image call or number of genes detected.

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/FIlterByButton.png" width="300">

#### Gene Selection and Library Normalization

Select the **Normalize selected libraries** button to choose from a range of options to perform normalization.

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/normTool.png" width="250">

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/geneVarianceProgress.png" width="250"> 

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/ZIprogress.png" width="250">

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/GeneSelection.png" width="250">


## Analyzing Selected Libraries
Select the **Analyze selected libraries** button to perform PCA of the normalized libraries.

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/AnalyzeButton.png" width="350"> 

#### PCA Sample Scores and Gene Loading Plots
___Sample Scores Plot___

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/PCAScores.png" width="300"> <img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/CellAnnotations.png" width="300">

___Gene Loadings Plot___


######Varimax Rotation

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/varimaxRotate.png" width=350>

######Refresh PCA Axes

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/refreshPCAaxes.png" width=350>

######View strongly loading Genes.

**Neuronal** genes loading PC1.

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/PCAGenesNeuronal.png" width="300">
<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/PCAGenesNeuronal2.png" width="300">

**Radial Glia** marker genes loading PC1.

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/PCAGenesRG.png" width="300">
<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/PCAGenesRG2.png" width="300">

Hover over genes in the Gene Loading plot to view their gene symbol, mean expression, IOD and % of cells expressing it in the **Gene Annotations** panel.

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/GeneAnnotations.png" width="300">


#### Visualizing Gene Expression across cells.

Enter the name of the gene whose expression you want to visualize. Select **surface** or **contour**, and a regression method from the drop-down menus, then click on **Plot expression** to generate the gene expression plots.


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

#### Gene Ontologies

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/geneOntologyButton.png" width="295">

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/geneOntologyProgress.png" width="295">

<img src= "https://dl.dropboxusercontent.com/u/9990581/SCell/SCell_Screenshots/GOmapWindow.png" width="400">

