# Career Insights 

All the files used for this project and their descriptions can be obtained from [O*Net Resource Center](https://www.onetcenter.org/database.html#all-files)

The specific files used for creating this project's dataset were:  

- Abilities.xslx
- Interests.xslx
- Knowledge.xslx
- Skills.xslx
- Work Activities.xslx
- Work Context.xslx

and can be found in [Origina Files](https://github.com/dariazhuk357/Career-Insights/tree/master/Original%20Files) section of this repository. 

## Data Merging and Cleaning 

Data merging and cleaning code can be found in [Data Merging and Cleaning Notebook](https://github.com/dariazhuk357/Career-Insights/blob/master/Data%20Merging%20and%20Cleaning/Data%20Merging%20and%20Cleaning%20.ipynb) of this repository. 

Files cleaned off from most variables except: 

- Title - description of the career 
- Data Value - describing average data value of the scale for each career attributes (skills, abilities, interests...) 
- Element_Name - name of the career attribute (name of skill, ability, interest...)
- Scale_Name - scale for the data value - two options: Importance vs. Context (eg. importance of a certain skill) 

'Element_Name' and 'Scale_Name' were combined together into a new 'Element_Name' variable. 
The files were then concatenated row-wise and the final dataset was pivoted to allow each row to describe a separate career title with columns outlining the 'Element_Name' variable data values. 

Approximately 8 careers contained null values and were, therefore, dropped from the final dataset [Clean Data Frame.csv](https://github.com/dariazhuk357/Career-Insights/blob/master/Data%20Merging%20and%20Cleaning/Clean%20Data%20Frame.csv) which can be found in [Data Merging and Cleaning](https://github.com/dariazhuk357/Career-Insights/tree/master/Data%20Merging%20and%20Cleaning) section of this repository. 

## Exploratory Data Analysis (EDA) 

This project employs unsupervised machine learning techniques to maneuver around the dataset and the career features, and, therefore, part of EDA will be discussed in the next section: Machine Learning section 

For hands-on exploration of the different features of the careers, the following BokehJS application was created and can be accessed in the [EDA Notebook](https://github.com/dariazhuk357/Career-Insights/blob/master/EDA/EDA%20.ipynb) of [EDA](https://github.com/dariazhuk357/Career-Insights/tree/master/EDA) section of this repository.  

![BokehJS_Career_Insights_App](https://github.com/dariazhuk357/Career-Insights/blob/master/EDA/Bokeh-Career_Insights%20App.gif)

## Machine Learning 

Find all the machine learning work here [Machine Learning](https://github.com/dariazhuk357/Career-Insights/tree/master/EDA)

### Unsupervised Machine Learning 

The final, clean dataset comprised of 966 careers and 466 features and can be found here [Clean Data Frame](https://github.com/dariazhuk357/Career-Insights/blob/master/Data%20Merging%20and%20Cleaning/Clean%20Data%20Frame.csv). To avoid the 'curse of dimensionality', a pricipal component analysis dimensionality reduction technique was performed. Approximately 40 PCA components covered at least 80% of explained variance and were used downstream in PCA to shrink the dataset for unsupervised machine learning. 

![Figure 1](https://github.com/dariazhuk357/Career-Insights/blob/master/Machine%20Learning/Images/PCA%20explained%20variance.png)

Non-hierarchial, as well as hierarchial clustering methods were used on the dataset for comparison. Below each method is described in detail. 

#### KMeans (non-hierarchial clustering)

In order to perform KMeans clustering on the clean dataframe (with PCA dimensionality reduction), the elbow graph was first generate. This graph showed the inertia loss with increasing number of clusters. The number of clusters where the inertia no longer droped significanly was chose as the number of clusters for the KMeans model. 

![Figure 2](https://github.com/dariazhuk357/Career-Insights/blob/master/Machine%20Learning/Images/KMeans%20Elbow%20Graph.png)

TSNE representation of this clutering revealed a decent clustering scheme with distinct cluster centers. 
![Figure 3](https://github.com/dariazhuk357/Career-Insights/blob/master/Machine%20Learning/Images/TSNE-KMeans.png)

#### Agglomearative Clustering (hierarchial clustering) with PCA. 

Using Scipy package a dendrogram was first created out of the clean dataset (reduced by PCA). 
![Figure 4](https://github.com/dariazhuk357/Career-Insights/blob/master/Machine%20Learning/Images/Dendrogram%2C%20PCA%20.png)

Dendrogram revealed potentially 6 clusters in the dataset. Using Agglomerative clustering with n_clusters setting to 6, cluster IDs for each career were generated. The TSNE representation of the clustering revealed, once again a decent clustering scheme with clear cluster centers. 

![Figure 5](https://github.com/dariazhuk357/Career-Insights/blob/master/Machine%20Learning/Images/TSNE-Agglomerative%20Clustering.png)

In both, the agglomerative and KMeans clustering, the generated cluster IDs corresponded to intuitive grouping of some careers. 
For instance, it made sense to put Accountants and Acutaries together into the same cluster or Accupuncturists and Acute Care Nurses into another cluster. 

#### Agglomerative Clustering (hierarchial clustering) with NMF. 

NMF is another dimensionality reduction technque, however, it is different by its ability to provide interpretable features. Herein NMF was used for dimensionality reduction leading up to hierarchial clustering. First, the number of of components for NMF was determined using the Nimfa package. The number of components were approximated by checking for where the residual sum of squares no long dropped significantly. The number was approximated to around 50. 

![Figure 6](https://github.com/dariazhuk357/Career-Insights/blob/master/Machine%20Learning/Images/RSS%20vs.%20N_comp%20NMF.png)

The W matrix of the NMF transformation (containing the NMF components) was clustered using agglomerative clustering. The number of clusters, 8, was determined through the dendrogram of the W matrix. 

![Figure 7](https://github.com/dariazhuk357/Career-Insights/blob/master/Machine%20Learning/Images/Dendrogram%2C%20NMF%20.png)

The TSNE yeilded fairly centered clusters considering the amount of clusters present: 8. 

![Figure 8](https://github.com/dariazhuk357/Career-Insights/blob/master/Machine%20Learning/Images/TSNE%20-%20NMF.png)

The careers matched the clusters intuitively. The highest ranking components (with value >.15) where used for describing the 7 clusters (see heatmap below).  

![Figure 9](https://github.com/dariazhuk357/Career-Insights/blob/master/Machine%20Learning/Images/Heatmap%20-%20Cluster%20ID%20vs.%20Comp%2C%20NMF.png)

Using the major components selected as described above, the H matrix of NMF was filtered for highest features (>.8). The major components vs. major features is represented by the heatmap below. 

![Figure 10](https://github.com/dariazhuk357/Career-Insights/blob/master/Machine%20Learning/Images/Heatmap%20-%20Comp%20vs.%20Features%20%2C%20NMF.png)

The initial dataframe was then filtered on the major features for supervised learning part of this project and can be accessed here: [Final_Supervised_DataFrame] (https://github.com/dariazhuk357/Career-Insights/blob/master/Machine%20Learning/Final_Supervised_DataFrame.csv). 

### Supervised Machine Learning 

Multiple supervised models were fitted on dataset generated in the unsupervised machine learning part of this proeject. The models included Logistic Regression, SGDClassifier, SVC, RandomForest, XGBClassifier, AdaBoostClassifier. 

Basic logistic regression was tuned using layered gridsearch (fit with multiple dimensionality reductions models and scaling methods) and the best esimator yeilded 85% accuracy. The detailed parameters can be viewed in the [Supervised_Learning Notbook](https://github.com/dariazhuk357/Career-Insights/blob/master/Machine%20Learning/Supervised_Learning.ipynb). The dimensionality reduction chosen was NMF with 20 components. The logistic regression coefficients for each of the NMF components can be seen in the graph below: 

![Figure 11](https://github.com/dariazhuk357/Career-Insights/blob/master/Machine%20Learning/Images/Logistic%20Regression%20Coefficients%20.png) 

To impove accuracy. The dataset was fit to a layered gridsearch with more advanced models listed above. The best estimator model was chosen to be SVC with an average accuracy of 88%. The detailed parameters can be viewed in the Supervised_Learning Notbook](https://github.com/dariazhuk357/Career-Insights/blob/master/Machine%20Learning/Supervised_Learning.ipynb).

Generating the cross tabulation from the SVC model preditions on the test set of the full dataset revealed a well centered classification.

![Figure 12](https://github.com/dariazhuk357/Career-Insights/blob/master/Machine%20Learning/Images/Cross%20Tabulation%20SVC.png) 

Moreover, the classification report revealed acceptable precision and recall scores for all cluster IDs. 

![Figure 12](https://github.com/dariazhuk357/Career-Insights/blob/master/Machine%20Learning/Images/Classification%20Report%20SVC.png) 



