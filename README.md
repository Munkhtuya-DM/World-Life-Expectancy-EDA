# World Life Expectancy Data Analysis

## Title Slide
**World Life Expectancy Trends**  
*A Data Exploration Project*  

---

## Project Overview
**Objective**: Analyze global life expectancy trends and influencing factors  
**Data Source**: World Life Expectancy dataset  
**Key Questions**:
- How has life expectancy changed over time?
- What's the relationship between GDP and life expectancy?
- How do developed vs. developing nations compare?

---

## Data Cleaning Process
**Key Steps Taken**:
1. Identified and removed 3 duplicate records (Row IDs: 1251, 2265, 2929)
2. Filled missing status values:
   - Countries with any "Developing" record → All blank = Developing
   - Countries with any "Developed" record → All blank = Developed
3. Imputed missing life expectancy values using average of neighboring years

---

## Life Expectancy Trends (2007-2022)
![Line chart showing average life expectancy by year]  
**Key Findings**:
- Steady global increase in life expectancy
- Small dip during pandemic years (2020-2021)
- Overall improvement of ~3 years across 15-year period

---

## Country Performance
**Biggest Improvers** (Top 5 life expectancy increases 2007-2022):
1. Zimbabwe: +22.3 years
2. Timor-Leste: +19.2 years
3. Malawi: +18.9 years
4. Rwanda: +18.4 years
5. Liberia: +17.6 years

**Correlation**: Most improvers are developing nations starting from low baselines

---

## GDP vs. Life Expectancy
**High GDP Countries** (≥1500):
- Average life expectancy: 79.2 years  
**Low GDP Countries** (<1500):
- Average life expectancy: 64.7 years  

**Strong positive correlation** between wealth and longevity

---

## Developed vs. Developing Nations
| Metric          | Developed | Developing |
|-----------------|----------|------------|
| Avg Life Exp    | 79.2     | 66.8       |
| # of Countries  | 32       | 138        |

**Insight**: 81% of countries are developing, with 12.4 year life expectancy gap

---

## BMI and Longevity
**Top 5 Countries by BMI**:
1. Nauru (35.8)
2. Cook Islands (35.0)
3. Palau (34.8)
4. Marshall Islands (34.6)
5. Tuvalu (34.2)

**Paradox**: High-BMI Pacific island nations maintain relatively good life expectancy (70-75 years)

---

## Adult Mortality Trends
**United States Case Study**:
- Rolling adult mortality shows concerning upward trend since 2015
- Contrasts with most developed nations showing steady declines

---

## Conclusions & Recommendations
**Key Takeaways**:
1. Global life expectancy continues to rise but inequalities persist
2. Economic development strongly correlates with longevity
3. Some developing nations making remarkable progress

**Recommendations**:
- Target healthcare investments in low-GDP countries
- Further study of "positive outlier" nations
- Monitor developed nations with worsening mortality

---

## Q&A
**Discussion Questions**:
1. What might explain the US mortality trend?
2. How can developing nations replicate top performers' success?
3. What other factors should we analyze?
