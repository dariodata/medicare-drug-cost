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

### Figure 1: Most expensive drugs and indications by total spending in a 5-year interval

![Top 40 diseases and drugs by total spending](https://github.com/dariodata/medicare-drug-cost/blob/master/Top_40_disease_drug.png)

#### Indications (left part)

A look at the total spending for the 5-year period 2011-2015 reveals that the bulk of drug spending is covered by a 
small set of diseases/indications (left graph). The total spending per indication decreases rapidly by going down the 
list of drugs.

Diabetes occupies the first place in this list with a total 5-year spending exceding $50 billion. Following in the 
list, we find other chronic diseases such as schizophrenia, chronic obstructive pulmonary disease, hypertension (high
 blood pressure), hypercholesterolemia (high cholesterol), depression, hiv infections, multiple sclerosis, peptic 
 ulcer disease, and chronic HCV infection (hepatitis C). Interestingly, pain medications are also in the top 4 
 indications by total spending.
 
It makes sense that treatment of chronic diseases receives the highest investment in drug spending, as patients with 
these diseases can live long lives when medicated.

Interestingly, the first cancer reaches only the 19th place of this list (chronic myelogenous leukemia). However, it 
must be noted that _cancer is actually a collection of different diseases_ with different genetics, origin, and 
treatment options. These different cancers were not clustered in this analysis.

#### Drugs (right part)

When we look at the most expensive drugs for the total 5-year spending, we find on the top of the list: Lantus 
(insulin), nexium (peptic ulcer), and crestor(anti cholesterol). It makes sense as these are medicines to treat chronic 
diseases.

However, we cannot learn much on a high level from looking at the total spending only. Therefore, a closer look is 
needed.

### Figure 2: Drug spending is growing but at very heterogeneous rates

![Most expensive drugs in 2015](https://github.com/dariodata/medicare-drug-cost/blob/master/Top_bubble_disease_drug.png)

#### Annual spending development for top 10 drugs (left)

The drug landscape is not temporally static. Therefore, I analyzed the annual spending since 2011 for the 10 top drugs
 in 2015. Eight out of these ten drugs consistently received higher spending every year, a reflection of the general 
 health care spending panorama. However, the rate of growth for each drug is dramatically different. Particularly 
 striking is the case of the drug Harvoni, which exhibited a >7-fold growth in total spending between 2014 and 2015.
 
Harvoni is a medicine for the treatment of hepatitis C (HCV infection) that was launched in 2014. It is the first 
drug with _cure_ rates close to 100%. Harvoni practically cures a chronic disease and this is reflected in its 
pricing at over $90k for a 12 week treatment.

The remaining drugs in the figure are mostly used for the _treatment_ of chronic diseases.

But how can we more extensively evaluate the burden posed by the different diseases/indications?

#### Top 100 indications in 2015 (right)

In order to find out more about the distribution of the most expensive indications, I plotted the drug spendings 
grouped by indication for the year 2015 in a scatter plot. This way, we can not only look at the total spending but 
also at the number of beneficiaries for a particular indication. The size of the bubbles represents the relative number
 of claims. 
 
 From this graph we can assess the magnitude of how the most expensive diseases affect society. Diabetes is not only 
 the most expensive single indication by total spending but also affects a very large number of people.
 
 The indications with the most beneficiaries are hypertension, pain and high cholesterol. They also represent some of 
 the highest number of claims (bubble size). This indicates that the average cost associated with each claim is low, 
 as these are generally medications with expired patents that are priced very low.
 
Again it is interesting to take a look at chronic HCV infection. This is the indication for the drug Harvoni. Both 
the number of beneficiaries and claims are extremely low compared with other diseases. However, chronic HCV infection
 reached the second place in the highes total drug spending in 2015.
 
## Next steps

I have shown in this analysis that very interesting insights can be gained from analyzing a smaller set of publicly 
available data. It follows that a more detailed and deeper analysis could enable more targeted conclusions and 
recommendations for improving the health care system and the quality of life of patients suffering from disease.  
Access to non-public owned data would make even deeper analysis possible.

Additional analysis could include:

- Clustering of diseases/indications to higher-level categories (cancer, metabolic disease, circulatory disease, 
nervous system disease, etc.)
- Linking of price databases to compare drug costs for the same indication on a population level
- Analysis of population data registers that document life style characteristics of healthy and ill individuals to 
identify those at risk of developing high-cost diseases (e.g.
 [Medical Expenditure Panel Survey](https://meps.ahrq.gov/mepsweb/data_stats/download_data_files_detail.jsp?cboPufNumber=HC-170), 
 [Behavioral Risk Factor Surveillance System data](https://www.cdc.gov/brfss/annual_data/annual_2015.html)) 


## Limitations

One limitation from this analysis is that only Part D drugs were considered. A further analysis could include Part B drugs too.

Moreover it was assumed that the fuzzy logic matching was successful in most cases. A more detailed test is required 
to assess match success more stringently.

All conclusions are only valid for the 2011-2015 interval. No data for 2016 was analyzed.