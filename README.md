# Considering Bias in Data

[DATA-512 | Homework 2 | Considering Bias in Data](https://docs.google.com/document/d/12Y4lPd5ORyK3s1vv-MQgF7-bYDpbpmKFKvSUgPmiLSs/edit#heading=h.k41ydxoqy1xs)

# Goal

The goal of this assignment is to explore the concept of bias in data using Wikipedia articles. This repository aims to perform an analysis of how the coverage of politicians on Wikipedia and the quality of articles about politicians varies among countries. Finally the notebook also generates a few tables which contain the following:

-   Top 10 countries by coverage: The 10 countries with the highest total articles per capita (in descending order) .
-   Bottom 10 countries by coverage: The 10 countries with the lowest total articles per capita (in ascending order) .
-   Top 10 countries by high quality: The 10 countries with the highest high quality articles per capita (in descending order) .
-   Bottom 10 countries by high quality: The 10 countries with the lowest high quality articles per capita (in ascending order).
-   Geographic regions by total coverage: A rank ordered list of geographic regions (in descending order) by total articles per capita.
-   Geographic regions by high quality coverage: Rank ordered list of geographic regions (in descending order) by high quality articles per capita.

# License

## Data source

The Wikipedia [Category:Politicians by nationality](https://en.wikipedia.org/wiki/Category:Politicians_by_nationality) was crawled to generate a list of Wikipedia article pages about politicians from a wide range of countries which is available in the [politicians_by_country.AUG.2024.csv](HCDS/data-512-homework_2/politicians_by_country_AUG.2024.csv) file.

The population data is available in CSV format as [population_by_country_AUG.2024.csv](HCDS/data-512-homework_2/population_by_country_AUG.2024.csv) used for analysis is downloaded from the [world population data sheet](https://www.prb.org/international/indicator/population/table/) published by the Population Reference Bureau.

## Data aquisition code

Snippets of the code under [Politician_analysis.ipynb](./data-512-homework_2/Politician_analysis.ipynb) were taken from a code example developed by Dr. David W. McDonald for use in DATA 512, a course in the UW MS Data Science degree program. This code is provided under the [Commons CC-BY license](https://creativecommons.org/licenses/by/4.0/). Revision 1.3 - August 16, 2024 license A copy of the reference code can be found in the reference_code folder of this project

# API Documentation

[MediaWiki PageInfo API](https://www.mediawiki.org/wiki/API:Info) : API to fetch page info for a given article title.

[ORES API](https://www.mediawiki.org/wiki/ORES) : API to fetch article rating for a given article's revision id.

[urllib](https://docs.python.org/3/library/urllib.request.html) : For fetching data from MediaWiki's PageInfo API

[Pandas](https://pandas.pydata.org/docs/reference/index.html): Python data processing library

[request](https://requests.readthedocs.io/en/latest/api/#) : For calling the MediaWiki and ORES APIs

# Usage

Entire code for reproducing the results are present in the [Politician_analysis.ipynb](data-512-homework_2/Politician_analysis.ipynb) file.
We just have to run the cells in order to produce the same results.

## Getting access token

To use Lift Wing (the machine learning API service), you’ll need a Wikimedia account. If you already have a Wikipedia account, it may work, but if not, create a new one to obtain an access token. Follow the official guide to generate an API key for your account. Be sure to select a Personal API token rather than a Server-side app key. After successfully creating the access token, you will receive a Client ID, Client Secret, and Access Token—be sure to save all three. If lost, you'll need to deactivate the token and generate a new one.

In the data acquisition code, use your username and the Access Token you generated.

You can use jupyter to run this file locally or even google colab (needs access to google colab). One can use the `Run All Cells` or `Restart Kernel` and `Run All Cells` option of the jupyter notebook.

Note: The data aquisition step where we use the ORES API to get the quality score for every article takes about 2-2.5 hours.

# Important considerations

You should be a little careful with the data. Crawling Wikipedia categories to identify relevant page subsets can result in misleading and/or duplicate category labels. Naturally, the data crawl attempted to resolve these, but not all may have been caught.
As well, Wikipedia categories are folksonomic, meaning there is very little control over how they are applied to pages. This means that the set of pages is very likely some kind of subset, and may have pages that are not actually about individual politicians. You should look for any data inconsistencies and document how you handle inconsistencies that you find.
