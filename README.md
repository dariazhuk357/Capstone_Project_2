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

### Unsupervised Learning 

The final, clean dataset comprised of 966 careers and 466 features. To avoid the 'curse of dimensionality', a pricipal component analysis dimensionality reduction technique was performed. Approximately 40 components covered at least 70% of explained variance and were used in PCA. 

![Figure 1](https://github.com/dariazhuk357/Career-Insights/blob/master/Machine%20Learning/Images/PCA%20explained%20variance.png)

![Figure 2](https://github.com/dariazhuk357/Career-Insights/blob/master/Machine%20Learning/Images/KMeans%20Elbow%20Graph.png)
![Figure 3](https://github.com/dariazhuk357/Career-Insights/blob/master/Machine%20Learning/Images/TSNE-KMeans.png)
![Figure 4](https://github.com/dariazhuk357/Career-Insights/blob/master/Machine%20Learning/Images/Dendrogram%2C%20PCA%20.png)
![Figure 5](https://github.com/dariazhuk357/Career-Insights/blob/master/Machine%20Learning/Images/TSNE-Agglomerative%20Clustering.png)
![Figure 6](https://github.com/dariazhuk357/Career-Insights/blob/master/Machine%20Learning/Images/RSS%20vs.%20N_comp%20NMF.png)
![Figure 7](https://github.com/dariazhuk357/Career-Insights/blob/master/Machine%20Learning/Images/Dendrogram%2C%20NMF%20.png)
![Figure 8](https://github.com/dariazhuk357/Career-Insights/blob/master/Machine%20Learning/Images/TSNE%20-%20NMF.png)
![Figure 9](https://github.com/dariazhuk357/Career-Insights/blob/master/Machine%20Learning/Images/Heatmap%20-%20Cluster%20ID%20vs.%20Comp%2C%20NMF.png)
![Figure 10](https://github.com/dariazhuk357/Career-Insights/blob/master/Machine%20Learning/Images/Heatmap%20-%20Comp%20vs.%20Features%20%2C%20NMF.png)


