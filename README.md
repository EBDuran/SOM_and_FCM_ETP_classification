# Performing a Eastern Tropical Pacific  physicochemical classification usign two methods: Self-Organization Maps and Fuzzy c-means approaches.  
<p>The Eastern Tropical Pacific (ETP) is one of the most productive regions in the world, with biological richness and regional endemism. Classifying and describing the seascape is essential to develop policies and protect marine ecosystems. Managers’ interventions
are more likely to be effective in seascapes with similar environmental characteristics. In this study, we compared four clustering approaches.  </p>

<li> 1.- Self-Organizing Map  (SOM)</li>
  <li> 2.- Fuzzy c-means
  <ul>
  		<li>2.1.-Classsic Fuzzy c-means (FCM </li>
  		<li>2.2.- Generalized Fuzzy c-means (GFCM) </li>
  		<li>2.3.-Generalized Fuzzy c-means (SGFCM) </li>
    </ul>
  </li>
<P>The methods and workflow used in this study for ETP classification are shown below.</p>

![figure01_methods_20_08_2023](https://github.com/EBDuran/SOM_and_FCM_ETP_classification/assets/113937473/3ff85ed5-b6d4-402a-975a-26a9fe68e0f3)
## 1.-Data processing
The firts step is proscesing the six
physicochemical variables: Sea Surface Temperature (SST), salinity, Chlorophyll concentration (Cha), pH, diffuse attenuation coefficient at 490 nm (KD490) as a proxy for turbidity, and sea current velocity (SCV). The description of the spatial and temporal resolution of each variable and the repository
that was retrieved is in Table 1. In the script **01_Daily_variables.Rmd** the overall mean (OM), overall standard deviation (OSD), the maximum monthly mean (MMMSST) and minimum monthly mean (mMMSST) of SST were calculated.  In **02_Monthly_variables.Rmd** script the same descriptors were calculated for the rest of variables. The rasters were masked with the ETP area  proposed by Spalding (03_Masking_raster.Rmd), then, acollinearity test was conducted using Pearson correlation coefficients (R), and high correlations variables (R> ±0.7) were identified and removed  (**04_Correlation_test.Rmd**)

## 2.-Clustering methods 
## 2.1 FCM classifications 
Three soft clustering algorithms were performed to classify the ETP seascape: a) FCM, b)GFCM, and c)SGFCM .The critical parameter values of the three FCM algorithms were evaluated. Those include the number of clusters (K) and the fuzziness degree (m) for all FCM algorithms, the β parameter for GFCM and SGFCM, the α parameter, and the spatial windows (W) for SGFCM. Different value windows were evaluated for each parameter to obtain the optimal values: 1) for K were from 5 to 20, 2) for m were from 1.1 to 2, 3) for β were from 0.1 to 0.9, 4) for α parameter were from 0.5 to 2, and 5) W were searched with values from 1 to 3. To assess the impact of the value of each parameter and decide the optimal value, the Silhouette Index (IS) and the Explained Inertia (EI) were calculated. In the case of SGFCM, the Spatial Consistency (SC) was calculated for the α parameter and W using the same functio. The best values were used to perform the FCM-based classification of the ETP seascape. Furthermore, data with membership values above 0.75 were considered for environmental group classification to ensure distinct clusters and high intra-cluster similarity.The FCM classification processes are in the script **07_FCM_classification.Rmd**.

### 2.2.-SOM-PAM classification

<li> a) and b) Data reduction and  SOM map size selection </li>

**The map size is an important parameter in SOM**, because the output map will affect the final visualization. While a few numbers of nodes produce the over-smoothing results, too many nodes give an over-fitting model. A series of test using different map arrangement ranging from 4x3 to 9x9 were performed to select the map size and array of the neurons in SOM. 
The Topography Error (TE) and the percent of variance explained (PVE) were calculated to select the best map size parameter. The TE measures how well the topological patterns of the input data are preserved in the output layer of the SOM. It is calculated as the proportion of observations for which the BMU is not a neighbor of the second BMU. TE ranges from 0 to 1, where 0 means perfect topology preservation in the map and 1 means that a topology error characterizes each data point.The script for the all test and parameters of map size topoloy  are in **05_SOM_grid_selection.Rmd**.

<li> c) SOM partition using PAM </li>

After selection of the best grid size in the last step, the data reduction using SOM was perfomed. In a second step we found the best partition of SOM map using the weight vectors of nodes using Partitioning Around Medoids (PAM) algorithm, both proceses are in **06_SOM_PAM.Rmd**.

<li> d) Selection of optimal cluster using GAP </li>

Finally we used GAP statistic to find the optimal number
of  cluster (K) in PAM of the SOM. The selection of K is in **06_SOM_PAM.Rmd**.
