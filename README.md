## Executive Summary  
 -In this report, we will analyze `mtcars` data set and explore the relationship between a set of variables and miles per gallon (MPG). The data was extracted from the 1974 *Motor Trend* US magazine, and comprises fuel consumption and 10 aspects of automobile design and performance for 32 automobiles (1973–74 models). We will use regression models and exploratory data analyses to mainly explore how **automatic** (am = 0) and **manual** (am = 1) transmissions features affect the **MPG** feature. 
 +In this report, we will analyze `mtcars` data set and explore the relationship between a set of variables and miles per gallon (MPG). The data was extracted from the 1974 *Motor Trend* US magazine, and comprises fuel consumption and 10 aspects of automobile design and performance for 32 automobiles (1973–74 models). We use regression models and exploratory data analyses to mainly explore how **automatic** (am = 0) and **manual** (am = 1) transmissions features affect the **MPG** feature. The t-test shows that the performance difference between cars with automatic and manual transmission. And it is about 7 MPG more for cars with manual transmission than those with automatic transmission. Then, we fit several linear regression models and select the one with highest Adjusted R-squared value. So, given that weight and 1/4 mile time are held constant, manual transmitted cars are 14.079 + (-4.141)*weight more MPG (miles per gallon) on average better than automatic transmitted cars. Thus, cars that are lighter in weight with a manual transmission and cars that are heavier in weight with an automatic transmission will have higher MPG values.
  
  ## Exploratory Data Analysis  
  First, we load the data set `mtcars` and change some variables from `numeric` class to `factor` class.   
 @@ -31,38 +31,38 @@ At this step, we make the null hypothesis as the MPG of the automatic and manual
  ```{r}
  result <- t.test(mpg ~ am)
  result$p.value
 +result$estimate
  ```  
 -Since the p-value is 0.00137, we reject our null hypothesis. So, the automatic and manual transmissions are from different populations.  
 -
 +Since the p-value is 0.00137, we reject our null hypothesis. So, the automatic and manual transmissions are from different populations. And the mean for MPG of manual transmitted cars is about 7 more than that of automatic transmitted cars.  
  
  ## Regression Analysis  
  First, we fit the full model as the following.  
  ```{r, results='hide'}
  fullModel <- lm(mpg ~ ., data=mtcars)
  summary(fullModel) # results hidden
  ```  
 -This model has the Residual standard error as 2.833 on 15 degrees of freedom. And the Adjusted R-squared is 0.779, which means that the model can explain about 78% of the variance of the MPG variable. However, none of the coefficients are significant at 0.05 significant level.  
 +This model has the Residual standard error as 2.833 on 15 degrees of freedom. And the Adjusted R-squared value is 0.779, which means that the model can explain about 78% of the variance of the MPG variable. However, none of the coefficients are significant at 0.05 significant level.  
  
  Then, we use backward selection to select some statistically significant variables.  
  ```{r, results='hide'}
  stepModel <- step(fullModel, k=log(nrow(mtcars)))
  summary(stepModel) # results hidden
  ```  
 -This model is "mpg ~ wt + qsec + am". It has the Residual standard error as 2.459 on 28 degrees of freedom. And the Adjusted R-squared is 0.8336, which means that the model can explain about 83% of the variance of the MPG variable. All of the coefficients are significant at 0.05 significant level.    
 +This model is "mpg ~ wt + qsec + am". It has the Residual standard error as 2.459 on 28 degrees of freedom. And the Adjusted R-squared value is 0.8336, which means that the model can explain about 83% of the variance of the MPG variable. All of the coefficients are significant at 0.05 significant level.    
  
  Please refer to the **Appendix: Figures** section for the plots again. According to the scatter plot, it indicates that there appear to be an interaction term between "wt" variable and "am" variable, since automatic cars tend to weigh heavier than manual cars. Thus, we have the following model including the interaction term:  
  ```{r, results='hide'}
  amIntWtModel<-lm(mpg ~ wt + qsec + am + wt:am, data=mtcars)
  summary(amIntWtModel) # results hidden
  ```  
 -This model has the Residual standard error as 2.084 on 27 degrees of freedom. And the Adjusted R-squared is 0.8804, which means that the model can explain about 88% of the variance of the MPG variable. All of the coefficients are significant at 0.05 significant level. This is a pretty good one.  
 +This model has the Residual standard error as 2.084 on 27 degrees of freedom. And the Adjusted R-squared value is 0.8804, which means that the model can explain about 88% of the variance of the MPG variable. All of the coefficients are significant at 0.05 significant level. This is a pretty good one.  
  
  Next, we fit the simple model with MPG as the outcome variable and Transmission as the predictor variable.  
  ```{r, results='hide'}
  amModel<-lm(mpg ~ am, data=mtcars)
  summary(amModel) # results hidden
  ```  
 -It shows that on average, a car has 17.147 mpg with automatic transmission, and if it is manual transmission, 7.245 mpg is increased. This model has the Residual standard error as 4.902 on 30 degrees of freedom. And the Adjusted R-squared is 0.3385, which means that the model can explain about 34% of the variance of the MPG variable. The low Adjusted R-squared value also indicates that we need to add other variables to the model.  
 +It shows that on average, a car has 17.147 mpg with automatic transmission, and if it is manual transmission, 7.245 mpg is increased. This model has the Residual standard error as 4.902 on 30 degrees of freedom. And the Adjusted R-squared value is 0.3385, which means that the model can explain about 34% of the variance of the MPG variable. The low Adjusted R-squared value also indicates that we need to add other variables to the model.  
  
  Finally, we select the final model.  
  ```{r, results='hide'}
