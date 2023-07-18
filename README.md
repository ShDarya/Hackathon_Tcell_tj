
# Preprocessing and explanatory data analysis
## Explanatory data analysis
Removing age outliers, missing samples of features: 'gender', 'region_id', 'date_of_birth'

![image](https://github.com/ShDarya/Hackathon_Tcell_tj/assets/91197981/f8e9d838-71c6-4c83-a3ad-11534c05b076)

![image](https://github.com/ShDarya/Hackathon_Tcell_tj/assets/91197981/23707763-f64c-43ac-b827-1340244d4aed)

The histogram of the ages presented in the data set shows that there are misses - a negative age and an age of more than 100 years. Visual analysis of the records contains misses, shows that an error was made when specifying the date of birth of the client. Data on the age of such patients are not expected.

According to the legislation of the Republic of Tajikistan and the security of T-cell, you can receive the services of the company if you have a passport, which in the republic can be obtained from the age of 16. This age should be chosen as the limit limit in the fence clipping. As a result, from 16 to 100 years, the maximum age is 86 years.

Missing values are observed in the region_id column, since this data is not functional in nature and is not temporary, it is also not possible to restore it.

The data in the date_of_birth column functions with the data in the age column and is not useful later on.

## Preprocessing and feature extraction

'device_type'  feature  

![image](https://github.com/ShDarya/Hackathon_Tcell_tj/assets/91197981/a14fa123-1ddd-4bfe-bfba-0672d85a5f6c)


![image](https://github.com/ShDarya/Hackathon_Tcell_tj/assets/91197981/56e3f276-6350-4845-bd8c-141d8fcdee49)

As a result of the analysis of the 'device_type' column, more than 1000 NaN objects were found, in this case NaN is equivalent to the 'Unidentified Devices' category.

df_data=df_data.fillna('Unidentified Devices')

Creation of an additional feature - opt_spend, containing information about the company's income from additional options (client's expenses). Data obtained from open sources.

![image](https://github.com/ShDarya/Hackathon_Tcell_tj/assets/91197981/0dc58313-80e7-4bef-a6a1-ef543b404861)

# Customer analysis

![image](https://github.com/ShDarya/Hackathon_Tcell_tj/assets/91197981/32011af2-ed0a-462f-a2e8-19dbd548852c)

Based on the histogram: the most frequent client is ~24 or ~32 years old, male; The most popular tariffs are 720 and 491. The user is ready to spend 10-20 somons per month for additional options, and also uses traffic up to 4,000 Mgbt 
Most preferred options: Bastai G1000, Messengers 2.0, Bastai G250.

![image](https://github.com/ShDarya/Hackathon_Tcell_tj/assets/91197981/433ec09e-d292-4486-bdb7-d20023be9626)

Sex among different age groups is distributed with the same frequency. User - a man is ready to make more expensive expenses for paid options than a woman; the median, as well as the upper and lower observed levels of traffic for users of different sexes are approximately the same.

 # Correlation analysis
 
 H0 - samples are not correlated; H1 - samples are correlated; H0 is rejected when pvalue< 95% of the level, i.e. 0.05

 #Correlation 'device_type' - age
 maximum correlation coefficient at pvalue<< 0.05 - H0 is rejected and these features are used in the future;

 #Correlation additional options with age

maximum correlation coefficient for feature Bastai G250: correlation=0.21530, pvalue=7.172865e-46; This feature is used in the future;

#Correlation between region number and age

statistic=3177695.0, pvalue=2.7847621299038445e-58

#Correlation between 'trpl_id' and 'age']

statistic=0.0, pvalue=0.0

# Options analysis

![image](https://github.com/ShDarya/Hackathon_Tcell_tj/assets/91197981/605563c8-1409-47fa-a102-fc71fb2d77e6)

# Creating a dataframe with valid features

Final DataFrame includes such feature as 'onnet_traffic', 'onnet_in_traffic', 'offnet_traffic','offnet_in_traffic', 'data_traffic', 'region_id','device_type_3G Modems/Routers', 'device_type_4G Smartphones',  'spend_option', 'Бастаи G250', 'age'

# Building Models

## Regression model

'mae_score': 0.15183979175121265,
'r2_score': 0.061534296000651745,
'mse_score': 0.03562789116430506

## Classification model
Split target 'age' into ranges [(15.999, 26.0] < (26.0, 38.0] < (38.0, 86.0]] and turning into classes [0, 1, 2]\

#Logistic regression

![image](https://github.com/ShDarya/Hackathon_Tcell_tj/assets/91197981/5e6c4981-3ae8-48b3-8717-b037d2af4b68)

#Nearest neighbors model

![image](https://github.com/ShDarya/Hackathon_Tcell_tj/assets/91197981/b332ba1c-4780-4915-84ff-d4698715332a)


#Decision tree model

![image](https://github.com/ShDarya/Hackathon_Tcell_tj/assets/91197981/64edd7dc-4d0f-40d1-99c7-3fdd0d27b97d)

#Random forest model

![image](https://github.com/ShDarya/Hackathon_Tcell_tj/assets/91197981/acae5786-32cd-4e80-b2db-fc153e7d8cc0)

#Gradient boosting model

![image](https://github.com/ShDarya/Hackathon_Tcell_tj/assets/91197981/3e26fb76-5b6a-42c3-9eb4-9736f99a10c0)

![image](https://github.com/ShDarya/Hackathon_Tcell_tj/assets/91197981/fff3095d-a447-49bf-a23e-bcdf2d46dd81)

The best classification model is conventional logistic regression. Its accuracy is 0.44, which, compared to basemodel 0.333, is 10% more accurate (relative to the max. accuracy of 100%)

# NEURAl

![image](https://github.com/ShDarya/Hackathon_Tcell_tj/assets/91197981/4bbd5382-620a-4006-ab7a-48911c8345f5)

![image](https://github.com/ShDarya/Hackathon_Tcell_tj/assets/91197981/d1725678-e317-4f80-a1f3-f8e7d4eb9ccf)

# Recommendations
When generating data sets by options, the absence of a connected option should be marked with a value of 0, not NaN. Since NaN values can be generated in case of failures in the algorithm;

If the provided data represent a representative sample, then we can conclude that the first and third groups of customers are not sufficiently involved. It can be solved by appropriate targeted incentives, the formation of an individual pricing policy, for example, tariffs for schoolchildren and pensioners;

If the region id is allocated separately for different localities, then it can be noted that in some localities t-cell is not sufficiently represented on the market of mobile operators. It is solved by expanding the geography of the availability of the t-cell network, all other things being equal for various settlements;

It would be interesting to explore customer data in dynamics, including income data. Perhaps the dynamics of client spending largely characterizes the age category of the client;

Tariff data (conditions) would help interpret the popularity of several tariffs and draw conclusions about the ways and the need to change the company's tariff policy;

Optimize additional paid options - many options are simply not used (rarely used)

