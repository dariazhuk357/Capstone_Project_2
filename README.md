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

### Data Merging and Cleaning 

Data merging and cleaning code can be found in [Data Merging and Cleaning Notebook](https://github.com/dariazhuk357/Career-Insights/blob/master/Data%20Merging%20and%20Cleaning/Data%20Merging%20and%20Cleaning%20.ipynb) of this repository. 

Files cleaned off from most variables except: 

- Title - description of the career 
- Data Value - describing average data value of the scale for each career attributes (skills, abilities, interests...) 
- Element_Name - name of the career attribute (name of skill, ability, interest...)
- Scale_Name - scale for the data value - two options: Importance vs. Context (eg. importance of a certain skill) 

'Element_Name' and 'Scale_Name' were combined together into a new 'Element_Name' variable. 
The files were then concatenated row-wise and the final dataset was pivoted to allow each row to describe a separate career title with columns outlining the 'Element_Name' variable data values. 

Approximately 8 careers contained null values and were, therefore, dropped from the final dataset [Clean Data Frame.csv](https://github.com/dariazhuk357/Career-Insights/blob/master/Data%20Merging%20and%20Cleaning/Clean%20Data%20Frame.csv) which can be found in [Data Merging and Cleaning](https://github.com/dariazhuk357/Career-Insights/tree/master/Data%20Merging%20and%20Cleaning) section of this repository. 

### Exploratory Data Analysis (EDA) 

This project employs unsupervised machine learning techniques to maneuver around the dataset and the career features, and, therefore, part of EDA will be discussed in the Machine Learning section. 

For hands-on exploration of the different features of the careers, a BokehJS application was created portraying a bargraph version of data value for each career 



