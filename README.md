# Predicting Depression: An EDA into the impact of Poverty and Physical Activity
By Na Nguyen, James Hernandez, Jordy Marin Urbina, and Sylvain Zong-Naba"

Date: 2023-02-20

# Introduction

 We have probably heard the ongoing debate of whether money can make people happy. For our part, money might not make someone happy yet a significant portion of the things that make people happy requires money. Therefore, the lack of wealth might be at the origin of depression of an individual as they do not have the means necessary to do what makes them happy. Do people who are living in poverty experience depression more than those who are not? To get an idea of this relationship, it would be good to answer the question of how does poverty affect depression? 
 
Additionally, according to the American Journal of Preventive Medicine, 9.2% of Americans aged ≥12 years experienced a past-year major depressive episode. Particularly, the Covid-19 has impacted people’s mental health because of the social distancing rules, and the pandemic made it harder to workout. Thus, understanding some other unconventional factors that might have an effect on depression becomes crucial to act upon in at an individual and a collective level. Thus, we were wondering if there is relationship between exercising and depression? In fact, it would be interesting to explore if there is a relationship between physical activity and depression. Certainly, a person's ability to exercise might depend on their financial situation. Those who are higher compared to the poverty guidelines can afford some time to workout while some who are not in such a privileged situation might need to work more and harder, and in doing so have less time to workout. From this observation, one can wonder whether being physically active has an impact on the relationship between wealth depression. 

Our primary objective is to explore the variables related to depression by specifically looking at an individual's physical activity levels and the socioeconomic conditions of participants. The former will help our team identify if physical activity promotes a healthier mind, while the latter variable will help identify a trend on if and how financial situations impact one’s mental health. In sum, our final goal is to better understand the relationship between these factors so as to identify potential risk factors or protective factors that could help indicate mental health outcomes. 
 

# Research Question 

To explore these relationships stated in the introduction, we will try to answer the following question: 

How does poverty and physical activity affect the odds of having depression? 

To answer these questions, we will use the variables Poverty, Physical Active (PhysActive) and Depression. Further explanation will be provided later on how we chose these variables in the data section. The explanatory variables in our study are Poverty and Physical Active. The outcome variable is Depression and is a binary variable. 
The poverty variable is a ratio of family income to poverty guidelines. Smaller numbers indicate more poverty. This variable helps us to take into consideration the wealth of a person. The Physical Active (PhysActive) variable is used because it provides us information on whether a person is physically active or not.  The depression variable indicates the depression status of a person. 

# Data

## Context

The dataset NHANES contains 10000 units of observations or individuals of all ages from the “the non-institutionalized civilian population of the United States. This dataset includes 75 variables that include demographic, socioeconomic, dietary, and health related questions. In particular, the vast majority of the variables come from interviews, and the remaining variables are the results of medical, dental and physiological examinations.

As our research questions focus on predicting what variables might affect Depression of a person, we decided to explore the variable Physical Active (PhysActive) as our outcome variable. For the latter variable, study participants 12 years or older, responded as “Yes” or “No” if they did moderate or vigorous-intensity sports, fitness or recreational activities. In addition, we decided to use  the variable for Poverty, which is the ratio of the family’s income to poverty guidelines. 
Moreover, this survey is executed by the National Health and Nutrition survey (NHANES), which is a comprehensive study designed to assess the health and nutritional status of adults and children in the United States for the 2009-2012 sample years. Furthermore, the data collected aims at identifying emerging health issues among the target population, which enables policymakers, researchers and public health organizations to analyze trends in health and nutritional status, and assess the effectiveness of public policies. It is important to emphasize that the survey is conducted by a team of trained health professionals and researchers, who travel to various locations across the US to obtain from a representative sample of the target population. This team includes physicians, nurses, laboratory technicians, who conduct physical examinations, collect biological specimens, and perform the interviews and questionnaires.

According to the NHANES website, they used a four-stage study to collect the data. The first stage consisted of selecting the Primary Sampling Units (PSUs) from a frame of all U.S. counties, and a total of 15 counties were chosen for the 2009-2012 period. The second stage consisted of selecting Secondary sampling units (SSUs), within each PSU, segments were chosen based on geographical boundaries, and a total of 130 segments were selected during the sampling period. The third stage involved the random selections of households from the latter SSUs, from which all these households were invited to participate in the survey. Lastly, in the fourth stage the focus was on the selection of all individuals regardless of their eligibility for all components of the study, for instance, not all participants were eligible for laboratory tests. It is relevant to mention that the study has been carried out since 1960, and every sampling period has been adjusted to make the study more representative of the US population. Specifically, the data undergoes a statistical weighting adjustment to undo oversampling and undersampling of some population subgroups, including non-Hispanic Black people, Mexican Americans, and low income individuals. This process ensures there are no biases in the representation and provides a more reliable analysis. 

The original dataset can be found on the Center for Disease Control and Prevention (CDC) website by clicking on the Data & Stats button in the initial window displayed. To access the data, one could type “NHANES” on the search bar, and a link to the NHANES page will appear. Then, the user could click again on Survey Data and Documentation, and click on the dataset of interest (2009-2010 and 2011-2012), or by clicking on the following link: https://wwwn.cdc.gov/nchs/nhanes/Default.aspx. Nevertheless, the most straightforward method to obtain the clean data set is by downloading the R Package “NHANES”, and adding it to our R environment. This data set accounts for the period 2009-2012 with adjusted weighting, and it is the dataset that we used in the rest of our study. 


## Data Cleaning

Based on the NHANES dataset, we created a new dataset called `depressed_data` in which we selected only 3 variables we choose to examine for our research question: `Depressed`, `Poverty`, and `PhysActive`. 

The `Depressed` variable--which is a self-reported range of days where participants felt down, depressed or hopeless--carries 3 values: `None`, `Several`, `Most`. We converted `None` values to 0,`Several` and `Most` to 1. This allows us to support our logistic regression model with `Depressed` as our response variable and predict it as a binary categorical variable with two possible outcome values be $Y=0$ and $Y=1$.

We then filtered out any NA values under `Depressed` in order not to cause too much data noise.


# Exploratory Data Analysis 

![image](https://github.com/gnguyen87/logDepressionPovertyPhysicalActivity/assets/134335069/dcc8f30a-53a0-4ffc-9af2-3336cea42ce7)

From this visualization, we can see that the median poverty values for people who are not physically active are lower (around 2.8 for not depressed and 1.5 for depressed) than the median poverty values for those who are physically active (around 3.5 for not depressed and 2.9 for depressed). The interquartile lengths and ranges between observations that are physically active and are not are noticeably different. While the bins describing those who are physically inactive have their interquartile ranges from about 1.3 to 4.3 for not depressed and from 1 to 2.0 for depressed, those of observations that reported physically active ranges from 1.9 to 5 for not depressed and from 1.4 to 5 for depressed. It is also significant to note that for batches of data under physically active are left-skewed, the batches for data under physically inactive are right-skewed for those that reported for depression yet left-skewed for those that reported for no depression. 

# Logistic Regression

## Model Creation

As we wanted to predict the probability of an individual based on whether or not they are physically active and depending on their poverty status we decided to use a logistic regression model instead of a liner regression model. For convenience, we proceeded to use a logistic regression model as our final model since our outcome variable `Depressed` is a binary variable. 

Moreover, at first we wanted to use the variables Poverty and Physical Activity as explanatory variables without an interaction term. However, during our EDA we noticed that poverty might have an interaction effect with the Physical Active variable. To elaborate on this, Figure 1 shows that the median of those individuals who are physically active, regardless of whether or not they are depressed seem to be concentrated in a higher number of the poverty level variable, which might suggest that physically active individuals may have a lower poverty. Hence, in order to account for these subtle differences, we allowed poverty to interact with the variable Physical Active. 

Thus, our final model can be expressed as follows:


$$Odds[Depressed | PhysActive,Poverty] = 0.75 + 0.50 * PhysActiveYes + 0.72*Poverty + 1.14(PhysActiveYes * Poverty)$$

## Fitted Model

The table below shows the exponentiated estimated coefficients for our model and the Standard Errors (Lower Bound and Upper Bound) using the Classical Approach:

<img width="681" alt="Screenshot 2024-01-10 at 3 08 55 PM" src="https://github.com/gnguyen87/logDepressionPovertyPhysicalActivity/assets/134335069/c5376190-f5b5-4c60-bf94-072f8f67566e">

## Model Interpretation

### Odds ratio
> Intercept Coefficient is approximately equal to 0.75.

The coefficient of 0.75 represents the odds of being depressed when an individual is not physically active and living in poverty (level 1) when all the other predictor variables are equal to zero.  

The SE for the Intercept is 0.08: The standard error of the exponentiated intercept coefficient is significantly small. This value might indicate that we have a high precision in estimating the odds of being depressed for the individuals who are not physically active and are in poverty (level 1).

>Poverty Coefficient: is approximately equal to 0.720. 

Holding all other variables constant, the multiplicative change in estimated odds of being depressed is 0.72 for each unit increase in poverty. Because the odds ratio is less than 1, the odds of being depressed are less with each unit increase in poverty.

The SE for the Poverty Coefficient is 0.03.: The standard error of the poverty coefficient falls is a relatively small value. This value might indicate that there might a high precision in estimating the effect of poverty on the odds of being depressed. 

>PhysActiveYes Coefficient is approximately equal to 0.505. 

Holding all other variables constant, the multiplicative change in estimated odds of being depressed for individuals who are physically active are about 0.505 times less than the estimated odds ratio of being depressed for individuals who are not physically active. In other words, because the odds ratio is less than 1, the estimated odds of being depressed is less with those who are physically active as compared to those who are not physically active.

The SE for the PhysActive Coefficient is 0.12: The standard error of the physical active coefficient falls in a relatively small value. Yet, it is roughly higher in comparison to the aforementioned values for the SE of the other coefficients. We can say that there might be some uncertainty in estimating the effects on physical activity on the odds of being depressed. 

>Poverty:PhysActiveYes Coefficient is approximately equal to 1.14. 

The effect of physical activity on the odds of being depressed differs depending on the level of poverty. 

1.14 is the multiplicative difference in estimated odds of being depressed between those who are physically active and physically inactive. In other words, 1.14 is the multiplicative change in the estimated effect of poverty on estimated odds of being depressed between those who are physically active and those who are not, where the effect of poverty on the estimated odds of being depressed is a one unit change in poverty, or the ratio between household income to poverty guidelines. This means that the estimated odds of depression are expected to increase by 114% among individuals who are physically active and living in poverty than those who are not physically active and not living in poverty. 

The SE for the Poverty:PhysActive Coefficient is 0.04: The standard error of the interaction coefficient between poverty and physical activity is significantly small, suggesting that there might be a high precision in estimating the effect of the interaction between physical activity and poverty on the odds of being depressed. 

### 95% Confidence Intervals
> The 95 % Confidence Interval (CI) for the Exponentiated Poverty Coefficient:

The CI for the poverty coefficient is (0.68, 0.76), which means that we are 95 % confident that the true population of odds ratio for the Poverty Coefficient is between 0.68 and 0.76. Since the interval does not include the null value of 1 and controlling for the other variables, we can say that Poverty is a significant predictor of the odds of being depressed, In other words, since the interval provided plausible values for the true odds ratio population, we have evidence that suggests that there is a true relationship between poverty and the odds of being depressed. 

>The 95 % Confidence Interval (CI) for the Exponentiated PhysActiveYes Coefficient:

The CI for the PhysActiveYes coefficient is (0.40, 0.64), indicating that we are 95 % confident that the true population of odds ration lies within (0.40, 0.64). As this interval does not include 1 and controlling for the other variables, we can say that the physical activity coefficient is a relevant variable at predicting the odds of being depressed, as it suggests that there is a true relationship between the Physical Activity and the odds of being depressed. 

>The 95 % Confidence Interval (CI) for the Exponentiated Poverty: PhysActiveYes Coefficient:

The CI for the Poverty:PhysActiveYes coefficient is (1.06, 1.24). This suggests that we are 95 % confident that the true population of the odds ratio lies within (1.06 and 1.24). Since the interval does not include 1, we can say that there is a true relationship between the effects of physical activity depending on the poverty status on the odds of being depressed.  


## Model Evaluation

As the first step for evaluating our fitted logistic regression model, we used the augment function to obtain these predicted probabilities for each individual from our dataset, based on the fitted model. Then, we created a box plot that compares our model’s predicted probabilities: one for people who actually self-reported as depressed, and one for people who did not self-report as depressed. Preferably, we would like to observe that our fitted logistic model predicts a higher probability of being depressed for people who actually self-reported as being depressed, and a lower probability of being depressed for those who did not self-report as depressed.  

![image](https://github.com/gnguyen87/logDepressionPovertyPhysicalActivity/assets/134335069/89b5b538-b246-4c7f-9618-99e4180b4a65)

From the boxplot above, we can see that the median probability of the predicted outcome `Depressed` is higher for people who self-reported as Depressed, at around 0.24. As compared to the median of 0.17 for the predicted outcome of being `Depressed` for people who did not self-report as `Depressed`. Furthermore, we can observe that both boxplots are not significantly skewed, which could show that the predicted probabilities are relatively distributed around the median mentioned above. In particular, we can observe that most of the predicted probabilities are lower than 50 percent.


### Selecting a Threshold

The next step in our model’s evaluation was to select a threshold that helped us to turn our model’s predicted probabilities into a binary decision. After considering the context of our data, and the significance of the outcomes of this fitted model, we opted to use a threshold of 0.20 which falls in between the two median predicted probabilities for both actual outcomes. Specifically, we acknowledge that it is our priority to have a low rate of false negatives, but also we want to be careful about not having a high number of false positives. For instance, we do not intend to have a high incidence of false negatives that will incorrectly classify many of the individuals as not depressed, when in fact they self-reported as depressed. By looking at it from a wider perspective, such misclassification by our model might have a further impact on the individual’s wellbeing, but also in the way they seek assistance or the type of support they receive. Conversely, we also aim to avoid any high incidence of false positives that will incorrectly classify individuals as depressed, when they actually self-reported otherwise, which might oppositely lead to unnecessary interventions. 

![image](https://github.com/gnguyen87/logDepressionPovertyPhysicalActivity/assets/134335069/3d82236f-b2da-457f-a2ec-e09de4f62b0a)

The boxplot above shows the same predicted probabilities for both actual outcomes of `Depressed` and `Not Depressed`. The dashed line corresponds to the threshold of 0.20 set in between the medians of the predicted probabilities for both actual outcomes. 


### Calculating the Model Quality Metrics

After selecting the threshold, we moved onto computing the binary predictions from the logistic model. This process allowed us to classify each person in our dataset based on their predicted probability of being `Depressed`: our model predicted that everyone with a probability higher than our threshold is `Depressed`, while the rest are not. The contingency table below enables us to compare our model’s predictions to the true outcome, determining whether the individuals were indeed `Depressed` or not. 

<img width="616" alt="Screenshot 2024-01-10 at 3 10 38 PM" src="https://github.com/gnguyen87/logDepressionPovertyPhysicalActivity/assets/134335069/0c296d9f-f842-4530-a437-8d155e32afa2">

Then, we proceeded to calculate the binary predictions, as shown by the table below:
<img width="662" alt="Screenshot 2024-01-10 at 3 11 11 PM" src="https://github.com/gnguyen87/logDepressionPovertyPhysicalActivity/assets/134335069/0812bdbf-67be-41cc-999a-d696afba8303">

### Interpreting the Model Quality Metrics 

Accuracy: The model’s accuracy falls in a moderate range of 0.5905 that tells us that the model correctly predicted the presence or absence of depression in 59.05% of the cases. 

Sensitivity: This is a moderate proportion of actual `Depressed` cases that were accurately identified as `Depressed` by the model. In this case, the sensitivity  of 0.6277 means that the model correctly identified 62.77 % of the actual `Depressed` cases. 

Specificity: This is the proportion of actual `Not Depressed` cases that were accurately predicted as `Not Depressed` by the model. Based on the results, the specificity of the model is somewhat average is 0.5807 meaning that the model correctly identified 58.07 % of the actual `Not-Depressed` cases. 

False Negative Rate (FRN): The proportion of individuals who are actually `Depressed` but that are predicted by our model as `Not Depressed`. In this case, 0.3723, which means that among the cases predicted as `Not Depressed` by the model, 37.23% are actually `Depressed`. This still relatively high false negative rate means that the model is incorrectly classifying many individuals as `Not Depressed`, when indeed they self-reported as such. 

False Positive Rate (FPR): The proportion of individuals who are actually `Not Depressed` but are classified as `Depressed` by the model. In this case, the false positive rate is 0.4193, which means that among the cases predicted as depressed by the model, 41.93 % are actually not depressed. This rate is roughly higher than the FPR, and in this context, this could indicate that the model is incorrectly classifying many individuals as depressed, when they are not, leading to unnecessary interventions or treatment. 

# Conclusions

## General Takeaways

To conclude, our group decided to look at how the ratio between household incomes and national poverty guidelines and physical activity play into an individual's mental health. We chose to look into this largely because of the current discussions on mental health and how external socioeconomic factors have a major role in impacting this. We decided to look into this curiosity by using the NHANEs data, and looking at the variables surrounding poverty, physical activity, and depression through the use of a logistical regression analysis. The two former of the three act as the explanatory variables, while the latter of the three is both the outcome variable and a binary variable. With this, we created a logistical regression model and analysis so as to better understand this issue, splitting our analysis into modeling and interpreting. We were able to see that the physical activity levels and poverty status of individuals do play a role in predicting if they do or do not suffer from depression. In sum, our logistical regression model shows that, when all other variables are constant, the odds of suffering from depression are higher when living closer to the poverty line. At the same time, the odds of being depressed are higher when there is a lack of physical activity. These two results were consistent with what we had expected to find; We initially think these results are due to the mental strain of financial stressors on top of a low physical activity, which is commonly accepted to lead to less depression. On another note, the interaction term shows that the odds of being depressed is higher for individuals who live further from the national poverty guidelines and who have a higher level of physical activity. Thus, it would be helpful to look at other potential explanatory variables from the dataset to better understand what causes this unexpected result. 

We interpreted our confidence intervals to reaffirm that, when alone, conditions of poverty and levels of physical activity are correlated with the odds of an individual suffering from depression. However, we were also able to reaffirm that the state of depression is still largely influenced by the poverty status of the individual as well as their physical activity status interactively. At the same time, our box-plot showed that the median probability of being depressed was higher for those who actually self-reported depression. When adding a threshold to account for the medians of the predicted probabilities for both actual outcomes, we were able to compute that the model was 59% accurate, 63% sensitive and 58% specific. However, the model unfortunately provided many false positives as well as false negatives, falsely classifying many individuals as both depressed and not depressed.  

All in all, the NHANEs data can be utilized to conclude that an individual's proximity to poverty and their level of physical activity clearly play major roles in determining their mental health outcomes as indicated by self-reported depression. 


## Limitations

After working with the NHANES data set, we identified some limitations that might have an effect on our model. Although this survey strives to collect data from a representative sample of the US population, the sample size is still small in comparison to the actual population, which limits to some extent the scope of our model predictions. Hence, some groups might still be underrepresented. In addition, two of the variables we used to fit our model: Physical Active and Depression are self-reported variables. Indeed, these types of variables are prompt self-biases as the survey respondents might over-report or under-report their behaviors, affecting the accuracy of the data. To illustrate this, some people might have different perspectives on differences in levels, frequency or intensity of physical activity. Furthermore, while self-reporting depression, there might be some stigma or cultural biases associated with mental health which might impact how individuals report their symptoms. In a similar way, there might be a lack of knowledge of the symptoms of depression that contribute to the under-report of depression. Overall, it is important to consider the aforementioned limitations while drawing conclusions from our findings. 

Regarding the model quality metrics, we can say that these values are moderate. However, they are not relatively high to conclude that our model can accurately provide a perfect fit to the data given that the predicted probabilities are not closely matching the actual outcomes. For instance, our fitted model performs adequately, but not exceptionally in terms of accuracy, which is the metric that determines how well our model can predict the case for depression and not depression. Furthermore, we acknowledge that when choosing the threshold we aimed at reducing the false negatives produced by our model. Hence, we can say that there are further implications in doing so. An example of this is that the False Positive Rate is moderately high, which indicates that among the individuals who self-reported as not depressed, there is 41.93 % of individuals who are predicted as `Depressed` by our model.

Therefore, from a personal point of view, this might impact their well-being by creating unnecessary stress on the individuals and the way they seek assistance. Moreover, this effect might potentially put a strain on the healthcare system, which might lead to overburdening of the healthcare system, and it might decrease the quality for those who actually need it. 

Lastly, our model did not account for important variables such as gender, age and ethnicity/race. Therefore, for future work it would be interesting to explore other explanatory variables, and see how this might affect the outcome of Depression. As an example, age can have an effect on depression. In fact, a study published by the Journal of Abnormal Psychology found that U.S teens and young adults' depression has risen significantly over the past decade in comparison with adults 26 or older. Thus, having age as another explanatory variable might improve the metrics of our model. 

# Appendix

## Works Cited

Centers for Disease Control and Prevention. (n.d.). Nhanes questionnaires, datasets, and related documentation. Centers for Disease Control and Prevention. Retrieved April 7, 2023, from https://wwwn.cdc.gov/nchs/nhanes/Default.aspx 

Goodwin, R. D., Dierker, L. C., Wu, M., Galea, S., Hoven, C. W., & Weinberger, A. H. (2022, September 19). Trends in U.S. depression prevalence from 2015 to 2020: The widening treatment gap. American Journal of Preventive Medicine. Retrieved April 8, 2023, from https://www.ajpmonline.org/article/S0749-3797(22)00333-6/fulltext#:~:text=An%20increase%20in%20depression%20from,SE%3D0.31%5D%20to%202019%3A 

Neighmond, P. (2019, March 14). A rise in depression among teens and young adults could be linked to social media use. NPR. Retrieved April 8, 2023, from https://www.npr.org/sections/health-shots/2019/03/14/703170892/a-rise-in-depression-among-teens-and-young-adults-could-be-linked-to-social-medi 

