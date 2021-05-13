<img src='images/education_image.jpg' width="900">


# Passing the Standards Projection

Research shows that high-poverty areas disproportionally educate children of color. The chances of ending up in a high-poverty or high-minority school are highly determined by a student’s race/ethnicity and social class. For instance, African American and Hispanic students—even if they are not poor—are much more likely than White or Asian students to be in high-poverty schools.

There is a growing body of evidence that shows increased investment on education returns better outcomes and that the positive effects are even greater among low-income students. On the other hand, it costs more to educate low-income students and provide them with a robust education capable of overcoming their initial disadvantages.

**Goals:**

- Understand the current demographics of wealthy to high-poverty schools across the state of California.
- Identify how much funding is available per pupil in wealthy vs high-poverty areas.
- Learn what factors are most correlated with student performance.
- Create a predictive model to find the percentage of students passing the standards per school.

## 1. Data
[Data Wrangling Report](https://github.com/gabriellewald/education-project/blob/main/Capstone1_data_wrangling.ipynb)

The dataset for this project is unique. It has been constructed using several datasets from the California Department of Education and the National Center of Education Statistics. It concerns with California K-12 public education for the academic year of 2018-2019.

- [California Assessment of Student Performance and Progress](https://caaspp-elpac.cde.ca.gov/caaspp/ResearchFileList?ps=true&lstTestYear=2019&lstTestType=B&lstCounty=00&lstDistrict=00000&lstSchool=0000000)

- Extracted data at school level keeping demographic information and percentage of students meeting the standards per school.
- Two datasets were created, one for language arts and literature and one for mathematics.
- All the demographic information was contained in one column called subgroup ID, the data was reorganized to contain one feature per column and one observation per row.
- The final dataset contains number of students per demographic feature.
- There is one school per row.

- [California Median Household Income](http://www.usa.com/rank/california-state--median-household-income--zip-code-rank.htm?yr=9000&dis=&wist=&plow=&phigh=)

- Merged with assessment data via zip code. 

- [Current Expense Per Daily Attendance](https://www.cde.ca.gov/ds/fd/ec/currentexpense.asp)

- Merged with assessment data via district code.

- [Total Revenue, Total Revenue per Pupil and Total Expenditure](https://nces.ed.gov/ccd/elsi/default.aspx?agree=0)

- Used string manipulation to remove punctuation and capitalize letters in order to merge the data on district name with the assessement dataset.

- [Free or Reduced Price Meals](https://www.cde.ca.gov/ds/sd/sd/fsspfrpm.asp)

- Merged with assessment data via school code.


## 2. Data Cleaning
[Data Cleaning Report](https://github.com/gabriellewald/education-project/blob/main/Capstone1_data_cleaning.ipynb)



## 3. EDA
[Exploratory Data Analysis](https://github.com/gabriellewald/education-project/blob/main/Capstone1_exploratory_data_analysis.ipynb)



## 4. Machine Learning Models



## 5. Predictions


## 6. Conclusion


## 7. Next Steps

