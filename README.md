<img src='images/education_image.jpg' width="900">


# Predicting Test Performance in California Public Schools

### In-depth investigation of factors associated with student test performance

**Problem Statement:**

Research shows that high-poverty areas disproportionally educate children of color. A student’s race/ethnicity and social class are highly predictive of whether they will attend a high-poverty or high-minority school. For instance, African American and Hispanic students—even if they are not poor—are much more likely than White or Asian students to be in high-poverty schools. There is a growing body of evidence that shows that increased investment in education leads to better outcomes and that the positive effects are even larger among low-income students. On the other hand, it costs more to educate low-income students and provide them with a robust education capable of overcoming their initial disadvantages. There is a strong need to find more informed and granular causes that impact test achievement in schools. This investigation seeks to understand what other factors are associated with student performance and ultimately predict the proportion of students in each school that pass standardized tests.

**Objectives:**

- Understand the current demographics of wealthy to high-poverty schools across the state of California.
- Learn what factors are most correlated with student performance (pass rate).
- Create a predictive model to find the proportion of students passing standard tests per school.

**Beneficiaries:**

- School administrators and policy makers to effectively identify schools that need more support and allocate resources to address tutoring needs, mentoring, and extracurricular activities.
- Teachers can be oriented to provide more support for under-performing groups and reduce achievement gaps.
- From a parents perspective, the results can be used to select a high performing school that meets academic standards.
- Department of education/ federal government to gain insights and potentially innovate adult (parents) education.

## 1. Data Acquisition
[Data Wrangling Report](https://github.com/gabriellewald/education-project/blob/main/notebooks/1_data_wrangling.ipynb)

The dataset for this project is unique. It has been constructed using several publicly available data files regarding the academic year of 2018-2019. The files come from the California Assessment of Student and Progress (CAASPP), California Department of Education (CDE), and the National Center of Education Statistics (NCES). The assessment data refers to the Smarter Balanced Summative Assessment, a standardized test applied yearly to K-12 students of public schools in California. It contains student demographic information, and the response variable of interest (number of students who meet the standards per school). The other datasets include variables such as current expense per daily attendance, number of students per school receiving free or reduced price meals, total revenue and expenditure per pupil, and median household income per zip code.

- California Assessment of Student Performance and Progress (CAASPP)
    - Extracted data at school level keeping demographic information and percentage of students meeting the standards per school (response or target variable).
    - All the demographic information was contained in one column called subgroup ID, this data was remapped to create one feature per column.

- California Departament of Education (CDE)
    - Current expense per daily attendance merged with assessment data via district code.

- National Center for Educational Statistics (NCES)
    - Total Revenue and Total Expenditure per pupil.
    - Used string manipulation to remove punctuation and capitalize letters in order to merge to the assessement dataset via district name.

- California Median Household Income
    - Merged with assessment data via zip code.

## 2. Data Cleaning
[Data Cleaning Report](https://github.com/gabriellewald/education-project/blob/main/notebooks/2_data_cleaning.ipynb)

- Imputed missing values with the median or zero as appropriate.
- Created dummy columns to signal missing values.
- Updated data types to integer, string or float as appropriate.
- Transformed number of students to percentage of students in several feature columns to keep the same format as the response variable.

## 3. EDA
[Exploratory Data Analysis Report](https://github.com/gabriellewald/education-project/blob/main/notebooks/3_exploratory_data_analysis.ipynb)

**Overall distribution:**

- There is a higher proportion of disadvantaged students across K-12 public schools in CA (left skewed distribution).
- CA is a minority-majority state with a higher percent of students self-identifying as Hispanic.

An in-depth investigation of income distribution showed:

- HIGH INCOME (> 125k)
    - There is a higher percentage of students passing the standards (left skewed distribution).
    - Parents are much more likely to have completed a four year college or higher.
    - The most common degree achieved by parents in this income bracket is graduate school.
    - The most common ethnicities are White and Asian.
<img src='images/high-income-zipcodes.jpg' width="900">
    
- LOW INCOME (< 30K)
    - There is a lower percentage of students passing the standards (slight right skewed distribution).
    - Parents are more likely to have completed only high school or be drop-outs.
    - The most common level of education is less than high school or high school graduate.
    - Hispanic is the most common ethinicity in this income bracket.
<img src='images/low-income-zipcodes.jpg' width="900">

**Pairwise relationship:**

Strong linear relationship found between the dependent variable "PERCENTAGE OF STUDENTS PASSING" and the following independent variables:

- Socioeconomic status
    - As the percentage of students from disadvantaged status increase, the percentage of students passing the standards decrease.
- Parents Education
    - < High School and High School Grad: As the percentage of students whose parents education falls in this category increases, the number of students passing the standards decrease.
    - College Grad and Graduate School: As the percentage of students whose parents education falls in this category increases, the number of students passing the standards also increases.
- Median Household income
    - As median household income increases, so does the percentage of students passing the standards.
 

## 4. Machine Learning Models
[Pre Processing and Modeling Report](https://github.com/gabriellewald/education-project/blob/main/notebooks/5_pre_processing_modeling.ipynb)

In order to predict the proportion of students passing standards in California K-12 public schools, I have considered 31 features, either directly from the dataset or engineered/derived from the data. The most important ones in terms of relative importances are parents' level of education, students ethinicity (this might hint cultural and background differences) and socioeconomic status.

The response variable is numerical and represents a proportion of the total students per school. Here, this is treated as a Regression problem since the response variable is numerical. Nonetheless, there is no ideal model to predict proportions.

Here I have used the following Regression models:

- Linear Regression
- LASSO
- Decision (Regression) Tree
- Random Forest
- Gradient Boosting

Each model is evaluated using several metrics. For this project mean absolute error (MAE), root-mean square error (RMSE) and R-squared (R2) were chosen to measure model accuracy. R2 was plotted for test data, and MAE and RMSE were plotted for training and test data. 


<img src='images/r2-rmse-mae-evaluation.png' width="600">

Gradient Boosting, an ensemble method based on decision trees, is the best performing model  with r-squared equals to 81.5.

Gradient Boosting Feature Importance:

<img src='images/gb-feature-importance.png' width="800">

>*NOTE: In RMSE the errors are squared before they are averaged giving the RMSE a higher weight to >large errors. Thus, the RMSE is useful when large errors are undesirable. The >smaller the RMSE, the more accurate the prediction because the RMSE takes the square >root of the residual errors of the line of best fit.*


In order to predict the proportion of students passing standards in California K-12 public schools, I have considered 31 features, either directly from the dataset or engineered from the data. The most relevant features in terms of relative importances are parents' level of education, socioeconomic status, and students ethinicity followed by other demographics.

The response variable is numerical and represents a proportion of the total students per school. Here, this is treated as a Regression problem since the response variable is numerical. It's important to mention that there is no ideal model to predict proportions. Nonetheless, the predictions fall well into the range 0 to 1 and the metrics show well performing models. It's a good start, these can be further improved with the addition of new features.

Remembering the models used were Linear Regression, LASSO, Decision (Regression) Tree, Random Forest, and Gradient Boosting. Each model is evaluated using mean absolute error (MAE), root-mean square error (RMSE) and R-squared (R2) to measure model accuracy. R2 was plotted for test data, and MAE and RMSE were plotted for training and test data. The best performing model with r-square = 0.815 is the Gradient Boosting.


