# HR-Analytics
Objective
- This study is done to demonstrate how EDA can be used in a real-world business situation.
- In this study, objective is to identify the best source of recruitment for a client (tech startup), based on previous data of candidate sources and recruitment strategies.

- 
HR Analytics EDA

Yugendra Rao K N
Objective

This HR Analytics case study tries to demonstrate how EDA can be used in a real-world business situation.
In this study, objective is to identify the best source of recruitment for a client (tech startup), based on previous data of candidate sources and recruitment strategies.
#Filtering out the warnings
import warnings
warnings.filterwarnings('ignore')
#Importing Libraries
import numpy as np
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
#Reading data from Recruitment_Data.csv
recruitment_data = pd.read_csv('Recruitment_Data.csv')
recruitment_data.head()
attrition	performance_rating	sales_quota_pct	recruiting_source
0	1	3	1.088190	Applied Online
1	0	3	2.394173	NaN
2	1	2	0.497530	Campus
3	0	2	2.513958	NaN
4	0	3	1.424789	Applied Online
#checking shape of the data frame
recruitment_data.shape
(446, 4)
#checking info of Recruitment_data
recruitment_data.info(verbose=True, show_counts=True)
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 446 entries, 0 to 445
Data columns (total 4 columns):
 #   Column              Non-Null Count  Dtype  
---  ------              --------------  -----  
 0   attrition           446 non-null    int64  
 1   performance_rating  446 non-null    int64  
 2   sales_quota_pct     446 non-null    float64
 3   recruiting_source   241 non-null    object 
dtypes: float64(1), int64(2), object(1)
memory usage: 14.1+ KB
1. performance_rating
#checking distribution of performance rating
recruitment_data["performance_rating"].value_counts()
3    263
2    106
4     67
1      7
5      3
Name: performance_rating, dtype: int64
sns.countplot(recruitment_data["performance_rating"])
plt.show()

Maximum employees received performance rating as 3.
Rating 5 is received by only 3 employees.
2. recruiting_source
#checking distribution of recruting source
recruitment_data["recruiting_source"].value_counts()
Applied Online    130
Campus             56
Referral           45
Search Firm        10
Name: recruiting_source, dtype: int64
recruitment_data["recruiting_source"].value_counts(dropna = False)
NaN               205
Applied Online    130
Campus             56
Referral           45
Search Firm        10
Name: recruiting_source, dtype: int64
sns.countplot(recruitment_data["recruiting_source"])
plt.show()

Maximum employees joined organization through Applied Online.
Minimum employees joined organization through Search Firm.
3. illustration of Attrition numbers differences by the Recruiting_Source
#The average Attrition Number grouped by Recruiting Source
recruitment_data.groupby('recruiting_source')['attrition'].mean()
recruiting_source
Applied Online    0.246154
Campus            0.285714
Referral          0.333333
Search Firm       0.500000
Name: attrition, dtype: float64
sns.countplot(data = recruitment_data, x = 'recruiting_source', hue = "attrition" )
plt.show()

Applied Online is having lowest Attrition Rate.
Search firm is having highest Attrition Rate.
4. illustration of Performance Rating differences by Recruiting Source
#The average Sales Number grouped by Recruiting Source
recruitment_data.groupby(['recruiting_source'])['performance_rating'].mean()
recruiting_source
Applied Online    2.930769
Campus            2.928571
Referral          2.844444
Search Firm       2.700000
Name: performance_rating, dtype: float64
sns.countplot(data = recruitment_data, x = 'recruiting_source', hue = "performance_rating" )
plt.show()

Applied Online and Campus recruits have highest performance rating.
Search Firm recruits have lowest performance rating.
Conclusion

Sources that have high Sales numbers and low Attrition numbers.

Applied Online
Campus
