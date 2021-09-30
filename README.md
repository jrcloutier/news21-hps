# News21, Unmasking America

Carnegie-Knight News21 is a national reporting initiative, headquartered at Arizona State University's Walter Cronkite School of Journalism and Mass Communication, which brings top journalism students from across the country to report and produce in-depth, multimedia projects. In 2021, 35 journalism students from 17 universities conducted a major summer investigation into the lingering impact of the pandemic.

For the project "Unmasking America," News21 investigated disparities in policies and practices that intensified under COVID-19 and may persist, exploring who has unequal access to health care, education, housing, and food.

## Household Pulse Survey

The News21 Overview team wanted to see if there was a racial and class disparity in how people experienced the pandemic. We turned to the Household Pulse Survey (HPS), a bi-weekly survey by the U.S. Census Bureau measuring the impact of the coronavirus pandemic from a social and economic perspective. The survey asks questions about childcare, education, employment, food security, health, housing, social security benefits, household spending, consumer spending associated with stimulus payments, intention to receive a COVID-19 vaccination, and transportation.

The HPS produces statistics at the **national** and **state** levels and for the following 15 largest Metropolitan areas:

-   Houston-The Woodlands-Sugar Land, TX Metro Area
-   Riverside-San Bernardino-Ontario, CA Metro Area
-   Los Angeles-Long Beach-Anaheim, CA Metro Area
-   San Francisco-Oakland-Berkeley, CA Metro Area
-   New York-Newark-Jersey City, NY-NJ-PA Metro Area
-   Detroit-Warren-Dearborn, MI Metro Area
-   Dallas-Fort Worth-Arlington, TX Metro Area
-   Miami-Fort Lauderdale-Pompano Beach, FL Metro Area
-   Philadelphia-Camden-Wilmington, PA-NJ-DE-MD Metro Area
-   Chicago-Naperville-Elgin, IL-IN-WI Metro Area
-   Phoenix-Mesa-Chandler, AZ Metro Area

There have been four phases covering the following time periods:

-   Phase 1 (Apr 23, 2020 - July 21, 2020)
-   Phase 2 (Aug 19, 2020 - Oct 26, 2020)
-   Phase 3.1 (Apr 14, 2021 - July 5, 2021)
-   Phase 3.2 (July 21, 2021 - early October)

Phase 1 was collected on a weekly basis, but that proceeding phases had two-week collection periods, even though the releases are still called "weekly" releases. Week 1 was also collected over two weeks.

The number of respondents for each collection period varies widely, as does the sample size and response rate. Technical documents, including source and accuracy statements for each release, are included [here](https://www.census.gov/programs-surveys/household-pulse-survey/technical-documentation.html). Overall response rates were low, but, according to a March 2020 [analysis](https://www2.census.gov/programs-surveys/demo/technical-documentation/hhp/2020_HPS_NR_Bias_Report-final.pdf) by the U.S. Census Bureau, weighting adjustment methods have helped mitigate non-response bias, a type of bias that occurs when people are unwilling or unable to respond to a survey due to a factor that makes them differ greatly from people who respond (e.g. internet access).

The U.S. Census Bureau releases the micro-data files containing individual responses to survey questions here: <https://www.census.gov/programs-surveys/household-pulse-survey/datasets.html>

Although we analyzed data from several different points in the pandemic, we settled on Week 22, January 6-18, 2021, when COVID-19 cases peaked in the U.S. The initial health and economic shock of the pandemic caught the country flat footed. By January, however, the U.S. government had been grappling with the pandemic and economic downtown for nine months, and COVID-19 relief under the Trump administration had been widely distributed. Disparities at this point in pandemic exposed systemic failure. We wanted to identify for whom federal aid wasn't enough.

## Analysis

As our colleague, Chase Hunter, has reported, the [poverty rate](https://unmaskingamerica.news21.com/extras/poverty-line/) is an imperfect measurement of the financial health and well-being of a family. The Overview team, therefore, reviewed responses to four questions --- regarding pandemic-related job losses, household expenses, food scarcity, and housing insecurity --- to gauge hardship.

The results of our analysis are in the output files, linked below. Our field [reporting](https://unmaskingamerica.news21.com/overview/) and data analysis indicate that while federal assistance forestalled an overall rise in poverty, families at opposite ends of America's racial and class divide experienced widely different outcomes. When new COVID-19 cases peaked in early January, low-wage workers and people of color were more likely to report hardship. Black and Hispanic individuals were each nearly twice as likely as white individuals to say they were having difficulty paying basic household expenses. 5.57% of white households were behind on their housing payments, compared to 18.89% of black households and 14.32% of Hispanic households.

These disparities persisted between income levels as well. The lowest earners were much more likely to report hardship, despite COVID-19 relief ostensibly aimed at supporting vulnerable families through the pandemic.

We recommend that anyone who wants to go through our analysis step-by-step download the [.Rmd](https://github.com/jrcloutier/news21-hps/blob/main/hps22.Rmd) file from the repository and open it in [R Studio](https://www.rstudio.com). There shouldn't be a need to download data from the Census Bureau; a line of code in the .Rmd will do this automatically, saving a SAS file with survey results, a SAS file with replicate weights, and a data dictionary, directly to the open project directory.

First, we re-coded the following demographic variables to get the information into a format that works for us: geography (state and metropolitan statistical area), race and ethnicity, gender, income, and education level. We also calculated the approximate age of each respondent from the birth year provided.

Re-coding essentially required us to create new factors based on the numeric responses/inputs to survey questions. In most cases, we also condensed responses. For example, we condensed the eight possible options for income into four buckets. We condensed race and ethnicity, two separate variables, into one, with Hispanic taking precedence (i.e. if a respondent marked that they were Hispanic and Black, they were recorded as being Hispanic).

We similarly re-coded responses to the questions we cared about: `EXPNS_DIF`, which indicated whether a respondent had difficulty paying household expenses in the last seven days; `CURFOODSUF`, which indicated whether a respondent had enough food in the last seven days; `MORTCUR` and `RENTCUR` which indicated whether a respondent was behind on their rent or mortgage payments; and `ANYWORK` and `RSNNOWRK`, which indicated whether a respondent was employed and, if not, why.

We then used [pollster](https://cran.r-project.org/web/packages/pollster/index.html), an R package that makes it easy to create topline and crosstab tables of simple weighted survey data, to compare responses between racial groups and income brackets.

## Files

[`recoded_hps22.csv`](https://github.com/jrcloutier/news21-hps/blob/main/recoded_hps22.csv) is a clean, re-coded version of the original dataset, containing select variables, including demographic information for each respondent and their responses to the questions we cared about (household expenses, food, housing, and employment).

[`hps22_byrace.csv`](https://github.com/jrcloutier/news21-hps/blob/main/hps22_byrace.csv) contains a pivot table showing responses by race, showing the percentage of people within each racial group who said they experienced difficulty paying household expenses, food or housing insecurity, etc.

[`hps22_byinc.csv`](https://github.com/jrcloutier/news21-hps/blob/main/hps22_byinc.csv) contains a pivot table showing responses by income, showing the percentage of people within each income bracket who said they experienced difficulty paying household expenses, food or housing insecurity, etc.

## Other uses

We were interested primarily in racial and class disparities during the pandemic, but we did re-code for several characteristics associated with each respondent, including age, gender, education, and whether there are children in a given household. We coud replicate our analysis above using different demographics.

Note that because the questionnaire evolved from one phase to the other, we would need to tweak the code to apply it to a release from a different phase.
