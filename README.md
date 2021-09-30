# News21 Analysis of Household Pulse Survey

For the 2021 project "Unmasking America," News21 investigated disparities in policies and practices that intensified under COVID-19 and may persist, exploring who has unequal access to health care, education, housing, and food.(You can learn more about Carnegie-Knight News21, a national reporting initiative, headquartered at Arizona State University's Walter Cronkite School of Journalism and Mass Communication, [here](https://news21.com/about/).

I was on a team that sought to identify whether there were racial and class disparities in outcomes during the coronavirus pandemic. We turned to the Household Pulse Survey (HPS), a bi-weekly survey by the U.S. Census Bureau measuring the impact of the coronavirus pandemic from a social and economic perspective. The survey asks questions about childcare, education, employment, food security, health, housing, social security benefits, household spending, consumer spending associated with stimulus payments, intention to receive a COVID-19 vaccination, and transportation.

There have been four phases to survey covering the following time periods:

-   Phase 1 (Apr 23, 2020 - July 21, 2020)
-   Phase 2 (Aug 19, 2020 - Oct 26, 2020)
-   Phase 3.1 (Apr 14, 2021 - July 5, 2021)
-   Phase 3.2 (July 21, 2021 - early October)

Phase 1 was collected on a weekly basis. The proceeding phases had two-week collection periods, even though the releases are still called "weekly" releases. (Week 1 was also collected over two weeks.)

Although we analyzed data from several different releases, covering different points in the pandemic, we settled on Week 22, January 6-18, 2021. That's when COVID-19 cases peaked in the U.S. The initial health and economic shock of the pandemic caught the country flat footed. By January, however, the U.S. government had been grappling with the pandemic and economic downtown for nine months, and COVID-19 relief under the Trump administration had been widely distributed. Lingering disparities would then suggest problems with the distribution of aid and/or an unequal recovery. 

## Analysis

As our colleague, Chase Hunter, reported, the [poverty rate](https://unmaskingamerica.news21.com/extras/poverty-line/) is an imperfect measurement of the financial health and well-being of a family. The Overview team, therefore, reviewed responses to four questions -- regarding pandemic-related job losses, household expenses, food scarcity, and housing insecurity -- to gauge hardship.

I recommend that anyone who wants to go through our analysis step-by-step download the [.Rmd](https://github.com/jrcloutier/news21-hps/blob/main/hps22.Rmd) file from the repository and open it in [R Studio](https://www.rstudio.com). There shouldn't be a need to download data from the Census Bureau; a line of code in the .Rmd will do this automatically, saving a SAS file with survey results, a SAS file with replicate weights, and a data dictionary, directly to the open project directory. (If you'd prefer to download the data directly from the U.S. Census Bureau, it releases the micro-data files containing individual responses to survey questions here: <https://www.census.gov/programs-surveys/household-pulse-survey/datasets.html>)

Otherwise, we basically did the following: 

First, we re-coded the following demographic variables to get the information into a format that works for us: geography (state and metropolitan statistical area), race and ethnicity, gender, income, and education level. We also calculated the approximate age of each respondent from the birth year provided.

Re-coding meant that we needed to create new factors based on the numeric responses/inputs to survey questions. In most cases, we also condensed responses. For example, we condensed the eight possible options for income into four buckets. We condensed race and ethnicity, two separate variables, into one, with Hispanic taking precedence (i.e. if a respondent marked that they were Hispanic and Black, they were recorded as being Hispanic).

We similarly re-coded responses to the questions we cared about: `EXPNS_DIF`, which indicated whether a respondent had difficulty paying household expenses in the last seven days; `CURFOODSUF`, which indicated whether a respondent had enough food in the last seven days; `MORTCUR` and `RENTCUR` which indicated whether a respondent was behind on their rent or mortgage payments; and `ANYWORK` and `RSNNOWRK`, which indicated whether a respondent was employed and, if not, why.

Using [pollster](https://cran.r-project.org/web/packages/pollster/index.html), an R package that makes it easy to create topline and crosstab tables of simple weighted survey data, we then compared responses between racial groups and income brackets.

Our data analysis, combined with field [reporting](https://unmaskingamerica.news21.com/overview/), indicated that when new COVID-19 cases peaked in early January, low-wage workers and people of color were more likely to report hardship. Black and Hispanic people were nearly twice as likely as whites to say they were having difficulty meeting basic household expenses. 5.57% of white households said they were behind on their housing payments, compared to 18.89% of Black households and 14.32% of Hispanic households. Black and Hispanic workers were also twice as likely as white workers to be out of work due to the pandemic. 

These disparities persisted between income levels as well. The lowest earners were much more likely to report hardship, despite COVID-19 relief ostensibly aimed at supporting vulnerable families through the pandemic.

We've exported the results in the three .csv files below. 

## Output files

[`recoded_hps22.csv`](https://github.com/jrcloutier/news21-hps/blob/main/recoded_hps22.csv) is a clean, re-coded version of the original dataset, containing select variables, including demographic information for each respondent and their responses to the questions we cared about (household expenses, food, housing, and employment).

[`hps22_byrace.csv`](https://github.com/jrcloutier/news21-hps/blob/main/hps22_byrace.csv) contains a pivot table showing responses by race, showing the percentage of people within each racial group who said they experienced difficulty paying household expenses, food or housing insecurity, etc.

[`hps22_byinc.csv`](https://github.com/jrcloutier/news21-hps/blob/main/hps22_byinc.csv) contains a pivot table showing responses by income, showing the percentage of people within each income bracket who said they experienced difficulty paying household expenses, food or housing insecurity, etc.

## Notes on accuracy

The number of respondents for each collection period varies widely, as does the sample size and response rate. Technical documents, including source and accuracy statements for each release, are included [here](https://www.census.gov/programs-surveys/household-pulse-survey/technical-documentation.html). 

Overall response rates were low, but, according to a March 2020 [analysis](https://www2.census.gov/programs-surveys/demo/technical-documentation/hhp/2020_HPS_NR_Bias_Report-final.pdf) by the U.S. Census Bureau, weighting adjustment methods have helped mitigate non-response bias, a type of bias that occurs when people are unwilling or unable to respond to a survey due to a factor that makes them differ greatly from people who respond (e.g. internet access). Still, be aware the sample size for the survey is small. 

The questionnaire also evolved from one phase to the other. Different questions were asked and different answer options were available. This, along with inconsistencies in sample size, make it difficult to measure any one variable over time. We decided against measuring how hardship evolved during the pandemic. Instead, we treated each release as an isolated snapshot of the country during a given two-week period. 


