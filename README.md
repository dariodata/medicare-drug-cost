# Analysis of Medicare drug cost data 2011-2015

Project proposal for The Data Incubator Challenge

_Dario Arcos-Diaz_

_February 6, 2017_

## Summary

Health care sytems are under growing cost pressure world-wide. Particularly in developed countries, the availability of the latest advancements in medicine contrasts with the challenge of making those medicines available to as many patients as possible. It is imperative to find ways to minimize costs and maximize the positive impact on the quality of life of patients. For this purpose I performed an analysis of the Medicare system spending on drugs in the USA. Furthermore I used a drug-disease matching open database to classify spending according to disease treated. After this analysis I propose the in-depth analysis of further open data. 

## Relevance

Health care costs amount to a considerable part of the national budgets all over the world. In 2015, $3.2 trillion were spent for health care in the USA ([17.8% of its GDP](https://www.cms.gov/research-statistics-data-and-systems/statistics-trends-and-reports/nationalhealthexpenddata/nationalhealthaccountshistorical.html)).  In Germany, the health care spending reached [11.3% of GDP in 2014](http://data.worldbank.org/indicator/SH.XPD.TOTL.ZS?locations=DE). On the one hand, this high health care costs can be explained by the population growth, particularly the elderly proportion, requiring higher investments to secure quality of life. On the other hand, new medicines are continously being discovered enabling the treatment of diseases that were once a sentence of death. This has as a consequence that many once fatal diseases have now become chronic with a high burden on the health care costs.

But how can governments and insurers make sure that patients receive the care they need, including latest technology advances, without bankrupting the system? One first step is the identification of high-cost diseases and drugs. This insights can then be used to identify population segments at high-risk of developing a disease, who can then be the focus of prevention measures.

Governments, insurers, patient organizations, pharmaceutical and biotech companies need all to leverage their available data, if we are to improve the health of patients now and in future generations.

## Methods

### Data sources

- [Medicare Drug Spending Data 2011-2015](https://www.cms.gov/Research-Statistics-Data-and-Systems/Statistics-Trends-and-Reports/Information-on-Prescription-Drugs/2015MedicareData.html): drug spending and utilization data. _In this analysis only Medicare Part D drugs were considered (drugs patients generally administer themselves)_
- [Therapeutic Targets Database](http://bidd.nus.edu.sg/BIDD-Databases/TTD/TTD_Download.asp): Drug-to-disease mapping with ICD identifiers.

### Tools

- pandas for data crunching
- fuzzywuzzy for fuzzy logic matching
- git for version control

### Data preprocessing

First, I cleaned up and processed the drug spending data available from Medicare for the years 2011-2015. This data includes the total spending, claim number, and beneficiary number --among others-- for each drug identified by its brand and generic names.

I also processed the data from the Therapeutic Targets Database, which presents the indications (diseases) associated with a drug generic name. 

Then, I used a fuzzy logic algorithm to match each drug generic name of the Medicare data with the closest element from the Therapeutic Targets Database. After having a list of exact matches, I assigned the first associated indication to each Medicare drug.

## Results

### Diabetes is the disease with the highest drug spending in the 5-year interval

Diabetes has the largest single-disease drug spending costs. However, it must be noted that _cancer is a very high-cost disease too._ The reason for this is that _cancer is actually a group of a multitude of different diseases_ with different genetics, origin, and treatment options. These diseases were not clustered in this analysis.

Harvoni is the most expensive drug.

![Top 40 diseases and drugs by total spending](https://github.com/dariodata/medicare-drug-cost/blob/master/Top_40_disease_drug.png)

### Drug spending is growing but the cost weight is not evenly distributed


## Limitations

One limitation from this analysis is that only Part D drugs were considered. A further analysis could include Part B drugs too.

Moreover it was assumed that the fuzzy logic matching was successful in most cases. A more detailed test is required to assess match success more stringently.

All conclusions are only valid for the 2011-2015 interval. No data for 2016 was analyzed.