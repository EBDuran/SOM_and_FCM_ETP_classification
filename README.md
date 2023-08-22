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
<P>The methods and workflow used in this study for ETP classification are shown below (Fig. 1).</p>

![figure01_methods_20_08_2023](https://github.com/EBDuran/SOM_and_FCM_ETP_classification/assets/113937473/3ff85ed5-b6d4-402a-975a-26a9fe68e0f3)
## 1.-Data processing
<p> The firts step is proscesing the six
physicochemical variables: Sea Surface Temperature (SST), salinity, Chlorophyll concentration (Cha), pH, diffuse attenuation coefficient at 490 nm (KD490) as a proxy for turbidity, and sea current velocity (SCV). The description of the spatial and temporal resolution of each variable and the repository
that was retrieved is in Table 1. In the script 01_Daily_variables.Rmd the overall mean (OM), overall standard deviation (OSD), the maximum monthly mean (MMMSST) and minimum monthly mean (mMMSST) of SST were calculated.  In 02_Monthly_variables.Rmd script the same descriptors were calculated for the rest of variables. The rasters were masked with the ETP area  proposed by Spalding (03_Masking_raster.Rmd), then, acollinearity test was conducted using Pearson correlation coefficients (R), and high correlations variables (R> ±0.7) were identified and removed  (04_Correlation_test.Rmd
)</P>

## 2.-Clustering methods 

### 2.2.-SOM

<p> **The map size is an important parameter in SOM**, because the output map will affect the final visualization. While a few numbers of nodes produce the over-smoothing results, too many nodes give an over-fitting model. A series of test using different map arrangement ranging from 4x3 to 9x9 were performed to select the map size and array of the neurons in SOM. </p>
