# Bias in Data -- A Study on Wikipedia Political Articles bewteen Countries

### Project Goal  
This project aims to explore the concept of 'bias' through data on English-language Wikipedia articles within the category of "Politicians by nationality" and subcategories.

### Project Overview  
This project is consisted of three steps:
* #### Data acquision
  Three datasets were acquired in this project:
  1. Data on most English-language Wikipedia articles within the category "Category:Politicians by nationality" and subcategories. ([Figshare](https://figshare.com/articles/Untitled_Item/5513449)). 
  2. Quality of articles obtained using a machine learning service called Objective Revision Evaluation Service ([ORES](https://www.mediawiki.org/wiki/ORES), [documentation](https://ores.wikimedia.org/v3/#!/scoring/get_v3_scores_context_revid_model)) to estimate the quality of each article.
  3. A dataset of country populations on the [Population Research Bureau website](http://www.prb.org/DataFinder/Topic/Rankings.aspx?ind=14).
* #### Data processing 
  After retrieving and including the ORES data for each article (result stored in 'article_quality.csv', the wikipedia data and population data were merged together. Entries that cannot be merged were removed. The final output was exported to 'hcds-a2-bias.csv'.
* #### Data analysis
  Two main calculations were performed in this step:
  1. The proportion (as a percentage) of articles-per-population 
  2. The proportion (as a percentage) of high-quality articles for each country. By "high quality" articles, in this case we mean the number of articles about politicians in a given country that ORES predicted would be in either the "FA" (featured article) or "GA" (good article) classes.

  Four tables as well as visualizations were produced in this step and embeded in the 'hcds-a2-bias.ipynb':
  1. Top 10 countries of coverage of politician articles on Wikipedia compared to their population.
  2. Bottom 10 countries of coverage of politician articles on Wikipedia compared to their population.
  3. Top 10 countries in terms of proportion of high quality articles about politicians
  4. Bottom 10 countries in terms of proportion of high quality articles about politicians
  The details of each step is illustrated in the "hcds-a2-bias.ipynb".  

  Note: There are 39 countries with 0 percent high quality articles about politicians (list printed in the notebook). The bar graph visualization was produced by randomly choosing 10 out of these 39 countries of 0 percent high quality articles. The list of bottom 10 countries with larger than 0 percent high quality articles about politicians is also produced in the notebook. 

### Project Structure
```
Bias in Data -- A Study on Political Articles bewteen Countries/  
  |- Data/  
     |- page_data.csv  
     |- Population Mid-2015.csv   
     |- article_quality.csv
     |- hcds-a2-bias.csv  
  |- LICENSE
  |- README.md
  |- hcds-a2-bias.ipynb
  |- politician_article_coverage.png
  |- high_quality_proportion.png  
```

### Source Data Licensing 
Both data on most English-language Wikipedia articles within the category "Category:Politicians by nationality" and subcategories, along with the code used to generate that data are released under the CC-BY-SA 4.0 license

For data gathered from the Wikimedia ORES API:
Wikimedia Foundation, 2017. CC-BY-SA 3.0.
See the Wikimedia Terms of Use for more details:
https://wikimediafoundation.org/wiki/Terms_of_Use/en

### Source Data documentation
1. Data on most English-language Wikipedia articles within the category "Category:Politicians by nationality" and subcategories can be found here: [Figshare](https://figshare.com/articles/Untitled_Item/5513449). 
2. Population data can be found here: [Population Research Bureau website](http://www.prb.org/DataFinder/Topic/Rankings.aspx?ind=14).
3. ORES API [documentation](https://ores.wikimedia.org/v3/#!/scoring/get_v3_scores_context_revid_model).

### Data Output 
The analyzed results were stored in a single CSV file named "hcds-a2-bias.csv"


|        Column         |       Data type     |
|-----------------------|---------------------|
|    country   	        |         text        |
|    article_name       |         text        |
|    revision_id      	|         integer     |
|    article_quality    |         text        |
|    population         |         integer     |

**country**: containing the sanitised country name, extracted from the category name

**article_name**: containing the unsanitised page title 

**revision_id**: containing the edit ID of the last edit to the page

**article_quality**: the quality of an article (at a particular point of time). There are 6 options: FA - Featured article, GA - Good article, B - B-class article, C - C-class article, Start - Start-class article, Stub - Stub-class article

**population**: population of countries Mid-2015  


### Reflections
* ##### Bias are embeded in algorithms
The quality of articles were determined from  a machine learning service called Objective Revision Evaluation Service (ORES). The assessment was done by  training a model to replicate the article quality assessments that humans perform, so that every article and every revision can be automatically accessed with a computer. Although ORES is an example of a fairly transparent and interpretable modle, still, the assessment algorithm itself could be biased. We should be careful about algorithm bias in any data science research when utilizing external algorithms. 

* ##### Bias exist in original data resources
The politician articles are obtained from English-language Wikipedia articles within the category "Category:Politicians by nationality" and subcategories. The segmentation of politicians may be biased, e.g. the editor is reluctant to label the category as politician. Due to such bias in original data resources, one should be careful about drawing definitive conclusions from the analysis. 

* ##### Bias exist in data analysis
As I reflect on the result of proportion of politician articles on Wikipedia compared to their population, I noticed that most top countries are with smaller population (e.g. Andorra, Tonga), while most top countries are with large population (e.g. China, India). Since this calculation of proportion of politian articles per population itself is biased towards smaller population countries, the resulted rank is therefore biased. We should be careful of the bias in defined metrics in any data science research especially when using defined metrics to compare different objects. 