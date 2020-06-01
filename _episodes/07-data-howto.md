---
title: "How to work with the data"
teaching: 0
exercises: 0
questions:
- What are the general rules about working with data?
- How to handle sensitive data?
objectives:
- Distinguish data at different stages of processing.
- Protect sensitive data with appropriate measures.
keypoints:
- Never modify raw data.
- Always keep CAT3 data on encrypted medium.
---

# Stages of data
Stage 0---_raw data_ is incoming data in whatever format. HTMLs scraped from the web, a large SQL dump from a data vendor, dBase files copied from a 200 DVDs (true story). Always store this for archival and replication purposes. This data is immutable, will be written once and read many times.

> Example: country names, capitals, areas and populations scraped from [scrapethissite.com](https://scrapethissite.com/pages/simple/), stored as a single HTML file.

Stage 1---_consistent_ data has the same information content as the raw data, but is in a preferred format with a consistent schema. You can harmonize inconsistent column names, correct missing value encodings, convert to CSV, that sort of thing. No judgmental cleaning yet. In our case, consistent data contains a handful of UTF-8 encoded CSV files with meaningful column and table names, generally following [tidy data principles](http://vita.had.co.nz/papers/tidy-data.html). The conversion involves no or minimal information loss.

> Example: A single CSV file with columns `country_name`, `capital`, `area`, `population`, in UTF-8 encoding.

Stage 2---_clean_ data is the best possible representation of information in the data in a way that can be reused in many applications. This conversion step involves substantial amount of cleaning, internal and external consistency checks. Some information loss can occur. Written a few times, read many times, frequently by many users for many different projects. When known entities are mentioned (firms, cities, agencies, individuals, countries), they should be referred to by canonical unique identifiers, such as [ISO-3166–1 codes](https://datahub.io/core/country-list) for countries.

> Example: Same as consistent, with additional columns for ISO-3166 code of countries and [geonames ID](https://www.geonames.org/) of cities. You can also add geocoordinates of each capital city.

Stage 3---_derived_ data usually contains only a subset of the information in the original data, but is built to be reused in different projects. You can aggregate to yearly frequency, select only a subset of columns, that sort of thing. Think SELECT, WHERE, GROUP BY clauses.

> Example: All countries in Europe.

Stage 4---_analysis sample_ contains all the variable definitions and sample limitations you need for your analysis. This data is typically only used in one project. You should only do JOINS with other clean or derived datasets at this stage, not before. This is written and read frequently by a small number of users.

> Example: The European country sample joined with population of capital cities ([from the UN](https://unstats.un.org/unsd/demographic/products/dyb/City_Page.htm)) so that you can calculate what fraction of population lives in the capital.

## How do you progress from one stage to the other?

**Automate all the data cleaning and transformation between stages**. This is often hardest between raw and consistent, what with the different formats raw data can be in. But from the consistent stage onwards, you really have no excuse not to automate. Have a better algorithm to deduplicate company names (in the clean stage)? Just rerun all the later scripts.

**Don’t skip a stage**. Much as with the five stages of grief, you have to go through all the stages to be at peace with your data in the long run. With exceptionally nicely formatted raw data, you may go directly to clean, but never skip any of the later stages. This follows from [modular thinking](https://dev.to/korenmiklos/the-tupperware-approach-to-coding-1g74): separate out whatever you or others can reuse later. What if you want to redo your country-capital analysis for Asian countries? If you write one huge script to go from your raw data to the analysis sample, none if it will be reused.

**Join late**. It may be tempting to join your city information to the country-capital dataset early. But you don’t know what other users will need the data for. And you don’t want to join before your own data is clean enough. A clean data should be as close to the [third normal form](https://en.wikipedia.org/wiki/Database_normalization#Normal_forms) as possible.

**Share your intermediate data products**. All the data cleaning you have done might be useful for others, too. If possible, share your intermediate products with other analysts by saving a (bead)[FIXME: ref].

# Categories od data protection
Privacy and ethical considerations necessitate good data protection practices. We have three categories of data:
## CAT1: Public data
The data is available publicly elsewhere. There is no embarrassment if accidentally made public. 

There are no restrictions on storage and sharing beyond common sense. Can be shared in response to a data request without approval.
## CAT2: Private data
The data is not available publicly. It is proprietary or has business value. (For example, company names, addresses and financials.) Some embarrassment and possible legal implications if accidentally made public. 

Access is limited to authorized individuals within CEU. Special care should be taken when sharing, transporting data. Sharing outside CEU may be allowed, but decided on a case-by-case basis.
## CAT3: Sensitive data
The data is not available publicly. It either has large business value or relates to sensitive information on individuals specifically protected by GDPR. (For example, addresses of individuals, political connections, names of company partners.) Major embarrassment and certain legal implications if accidentally made public. 

Access is limited to authorized individuals within CEU. Data can only be stored and transported on encrypted medium. Sharing outside CEU may be allowed, but decided on a case-by-case basis and encryption rules still apply.


{% include links.md %}

