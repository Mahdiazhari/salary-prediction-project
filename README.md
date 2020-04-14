# Salary Prediction Project

This project aims to create a salary prediction model, which predict salaries based on given job descriptions.

## Introduction

Considering the uncertainties and competitiveness in the job market, as job seekers, knowing how much employees are willing to pay for certain jobs would prove to be very beneficial to the job seekers. On the other hand, employers could benefit for this by having reference for the salaries in their company. It is beneficial for them both to know how factors such as educational qualifications, years of experience, job industry, etc affect their salary.

Thus, can we develop a model where salaries can be predicted based on the available features? If so, how accurate can the model get?Are the features available good enough for a predictive model?

## Dataset

The dataset is split into training and test data. It contains 'features' and 'target' for the training dataset.

Description of Features:

- jobId: The ID of the job.
- companyId: The ID of the company posting the job.
- jobType: The description of the position of the job within the company (Junior, Senior, CEO, etc).
- degree: The obtained degree of the employee.
- major: The formal education field of specialization of the employee.
- industry: The industry to which the company belongs.
- yearsExperience: The employee's years of experience.
- milesFromMetropolis: The distance in miles, from the employee's house to the metropolis.

Target Variable:

- Salary: Salary for the job.

## Exploratory Data Analysis

There are categorical and numerical features in the data. A check for duplicates and missing values revealed that there are no missing or duplicated data.

Categorical:

- jobId
- companyId
- jobType: CFO, CEO, VICE_PRESIDENT, MANAGER, JUNIOR, JANITOR, CTO, SENIOR
- degree: MASTERS, HIGH_SCHOOL, DOCTORAL, BACHELORS, NONE
- major: MATH, NONE, PHYSICS, CHEMISTRY, COMPSCI, BIOLOGY, LITERATURE, BUSINESS, ENGINEERING
- industry: HEALTH, WEB, AUTO, FINANCE, EDUCATION, OIL, SERVICE

Numerical:

- yearsExperience
- milesFromMetropolis

![numerical summaries](/images/numerical.png)

Here is the summary of the numerical features in the data.

#### Target Variable (Salary)

The target variable is a numerical variable representing annual salary (in USD).

![salary distribution](/images/distribution-salary.png)

From the distribution and boxplot above, we can see that salary is normally distributed. The boxplot also reveals some outliers.

### Removing Outliers

As revealed in the boxplot above, there are outliers in both sides.

![outlier salaries](/images/salary-0.png)

Further checks reveal that the outliers have a salary of 0, but the positions are not voluntary. Therefore it can be determined that they are outliers.

![outlier salaries 2](/images/salary-high.png)

These 16 juniors are from high value industries but with 20+ years of experience. Perhaps they are transitioning into new careers. We can determine that these values are also legitimate and not remove them from the training set.

Thus, the outliers to be removed are the 7 employees with 0 salaries.

### Summaries

![summaries numerics](/images/numerics-summary.png)

Here is a summary of the numeric variables in the cleaned dataset.

### Exploring Features and Salary

#### Job Type

![job type vs salary](/images/job-type-salary.png)

It seems that as the job position increases, salary increases as well. (CEOs have the highest salaries, while janitors have the lowest).

#### Degree

![degree vs salary](/images/degree-salary.png)

More advanced degrees are associated with higher salaries.

#### Major

![major vs salary](/images/major-salary.png)

Employees with a major in Math, Business, and Engineering generally have higher salaries compared to the rest. Employees with no major have the lowest salaries.

#### Industry

![industry vs salary](/images/industry-salary.png)

The Web, Finance, and Oil Industries are the top 3 industries with the highest salaries.

#### Years of Experience

![years of experience vs salary](/images/years-salary.png)

There is a clear association between years of experience and salary. The more years of experience, the higher the salary.

#### Distance in Miles from Metropolis

![distance vs salary](/images/distance-salary.png)

Salaries get smaller the further the employee is to the metropolis.

### Correlation

Here is the correlation between features and the target variable:

![corr numeric](/images/coor-numeric-salary.png)

We can observe that there's a small positive correlation between years of experience and salary. There is no correlation between numerical features.

## Hypothesize Solution/Baseline Results

### Baseline Results

The **baseline** results for this problem is a basic linear regression model with years of experience as a predictor of salary.
This model has an MSE of 1288.

### Hypothesis

The following models may be a good fit for the salary prediction problem:

1. Model pipeline using StandardScaler()-scaling to unit variance, PCA()-Projecting higher dimensional to lower dimensional space, LinearRegression()
2. RandomForestRegressor()- A random forest is a meta estimator that is good for predictive accuracy and could control over-fitting very well.
3. GradientBoostingRegressor()- This can be used for both regression and classification problems, which is an ensemble of weak prediction models, typically decision trees

## Solution Development

### Data Preparation

The categorical features were encoded using one-hot-encoding.
The Data was also normalized.

### Models

Three Models were trained on the data. One linear and two ensemble models:

- Linear Regression
- Random Forest Regression
- Gradient Boosting Regression

### Results (Without Hyperparameter Tuning)

#### Linear Regression

Average MSE:
384.4389794016031
Standard deviation during CV:
0.7765280635963165

#### Random Forest

Average MSE:
367.2183936856392
Standard deviation during CV:
0.6235201312820777

#### Gradient Boosting Regressor

Average MSE:
357.12352000277804
Standard deviation during CV:
0.8043960464617612

The best performing model is the Gradient Boosting Regressor with an average MSE of 357.

### Feature Importances

![feature importances](/images/Feature-importances.png)

We can see that for predicting salaries:

- Whether someone is a Janitor ranks as the most important feature
- Years of experience and Miles from the Metropolis comes in second and third
- Having a Major is ranked fourth

## Conclusions

- Developed a pretty accurate model with an average MSE of 357.
- Future solutions to the problem could employ more feature engineering of the features
- Feature importance ranks job position janitor, years of experience, and miles from metropolis as the three most important features
