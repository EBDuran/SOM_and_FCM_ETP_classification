This is the repository of information used in the paper "Classifying the Seascape of the Eastern Tropical Pacific Based on Physicochemical Variables"  The satellite images used for the following analyses are located in the `01_Data` folder. Scripts in Rmarkdown format are located in the `02_Methods` folder.

The Eastern Tropical Pacific (ETP) is one of the most productive regions in the world, known for its biological richness and regional endemism. Classifying and describing the seascape is essential to develop policies and protect marine ecosystems. Managers’ interventions are more likely to be effective in seascapes with similar environmental characteristics. In this study, we compared three clustering algorithms and a neural network analysis:

1. **Fuzzy c-means**
    - Classic Fuzzy c-means (FCM)
    - Generalized Fuzzy c-means (GFCM)
    - Simplified Generalized Fuzzy c-means (SGFCM)
    
2. **Self-Organizing Map (SOM)**

The methods and workflow used in this study for ETP classification are shown below.

![figure01_methods_20_08_2023](https://github.com/EBDuran/SOM_and_FCM_ETP_classification/assets/113937473/3ff85ed5-b6d4-402a-975a-26a9fe68e0f3)

# 1.-Data processing
The firts step is proscesing the six
physicochemical variables: Sea Surface Temperature (SST), salinity, Chlorophyll concentration (Cha), pH, diffuse attenuation coefficient at 490 nm (KD490) as a proxy for turbidity, and sea current velocity (SCV). The description of the spatial and temporal resolution of each variable and the repository
that was retrieved is in Table 2 of the manuscrit. In the script **01_Daily_variables.Rmd** the overall mean (OM), overall standard deviation (OSD), the maximum monthly mean (MMMSST) and minimum monthly mean (mMMSST) of SST were calculated.  In **02_Monthly_variables.Rmd** script the same descriptors were calculated for the rest of variables. The rasters were masked with the ETP area  proposed by Spalding (**03_Masking_raster.Rmd**), then, acollinearity test was conducted using Pearson correlation coefficients (R), and high correlations variables (R> ±0.7) were identified and removed  (**04_Correlation_test.Rmd**)

# 2. Clustering Methods 
## 2.1. FCM Classifications 
Three soft clustering algorithms were used to classify the ETP seascape:
- a) FCM
- b) GFCM
- c) SGFCM

The critical parameter values of the three FCM algorithms were evaluated, including the number of clusters (K) and the fuzziness degree (m) for all FCM algorithms, the β parameter for GFCM and SGFCM, the α parameter, and the spatial windows (W) for SGFCM. Different value ranges were evaluated for each parameter to obtain the optimal values: 1) K from 5 to 20, 2) m from 1.1 to 2, 3) β from 0.1 to 0.9, 4) α from 0.5 to 2, and 5) W from 1 to 3. To assess the impact of each parameter value and decide the optimal value, the Silhouette Index (SI) and the Explained Inertia (EI) were calculated. For SGFCM, the Spatial Consistency (SC) was calculated for the α parameter and W. The best values were used to perform the FCM-based classification of the ETP seascape. Furthermore, data with membership values above 0.75 were considered for environmental group classification to ensure distinct clusters and high intra-cluster similarity. The FCM classification processes are detailed in the script **07_FCM_classification.Rmd**.

## 2.2. SOM-PAM Classification
### a) Data Reduction and SOM Map Size Selection 

The map size is an important parameter in SOM, as the output map will affect the final visualization. While too few nodes produce over-smoothed results, too many nodes result in an over-fitted model. A series of tests using different map arrangements ranging from 4x3 to 9x9 were performed to select the optimal map size and array of neurons in SOM. The Topography Error (TE) and the Percent Variance Explained (PVE) were calculated to select the best map size parameter. TE measures how well the topological patterns of the input data are preserved in the output layer of the SOM. TE ranges from 0 to 1, where 0 means perfect topology preservation in the map and 1 indicates a topology error characterizes each data point. The scripts for all tests and parameters of map size topology are in **05_SOM_grid_selection.Rmd**.

### b) SOM Partition Using PAM 

After selecting the best grid size in the previous step, data reduction using SOM was performed. In the next step, the best partition of the SOM map was found using the weight vectors of nodes with the Partitioning Around Medoids (PAM) algorithm. Both processes are detailed in **06_SOM_PAM.Rmd**.

### c) Selection of Optimal Clusters Using GAP 

Finally, the GAP statistic was used to find the optimal number of clusters.

# 3.-Selecting the best classification
Finally, the best environmental classification of the ETP seascapes was selected based on IS and IE values. The indices for the SOM-PAM classification were calculated using the PAM groups. The final step of the pipeline are in the script **08_Clustering_comparation.Rmd**.
