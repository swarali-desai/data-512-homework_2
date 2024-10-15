# Considering Bias in Data

[DATA-512 | Homework 2 | Considering Bias in Data](https://docs.google.com/document/d/12Y4lPd5ORyK3s1vv-MQgF7-bYDpbpmKFKvSUgPmiLSs/edit#heading=h.k41ydxoqy1xs)

# Goal

The goal of this assignment is to explore the concept of bias in data using Wikipedia articles. This repository aims to perform an analysis of how the coverage of politicians on Wikipedia and the quality of articles about politicians varies among countries. Finally the notebook also generates a few tables which contain the following:

-   Top 10 countries by coverage: The 10 countries with the highest total articles per capita (in descending order).
-   Bottom 10 countries by coverage: The 10 countries with the lowest total articles per capita (in ascending order).
-   Top 10 countries by high quality: The 10 countries with the highest high quality articles per capita (in descending order).
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

Note: ChatGPT was used to for code generation help with syntax and improve code eficiency.

## Getting access token

To use Lift Wing (the machine learning API service), you’ll need a Wikimedia account. If you already have a Wikipedia account, it may work, but if not, create a new one to obtain an access token. Follow the official guide to generate an API key for your account. Be sure to select a Personal API token rather than a Server-side app key. After successfully creating the access token, you will receive a Client ID, Client Secret, and Access Token—be sure to save all three. If lost, you'll need to deactivate the token and generate a new one.

In the data acquisition code, use your username and the Access Token you generated.

You can use jupyter to run this file locally or even google colab (needs access to google colab). One can use the `Run All Cells` or `Restart Kernel` and `Run All Cells` option of the jupyter notebook.

Note: The data aquisition step where we use the ORES API to get the quality score for every article takes about 2-2.5 hours.

# Usage

Entire code for reproducing the results are present in the [Politician_analysis.ipynb](data-512-homework_2/Politician_analysis.ipynb) file.
We just have to run the cells in order to produce the same results.

## Intermediary files

The results for the page info API calls were stored in a [articles_page_info.json](HCDS/data-512-homework_2/intermediary_files/articles_page_info.json) with the following schema:

```
{
    "Abdul Baqi Turkistani": {
        "pageid": 27428272,
        "ns": 0,
        "title": "Abdul Baqi Turkistani",
        "contentmodel": "wikitext",
        "pagelanguage": "en",
        "pagelanguagehtmlcode": "en",
        "pagelanguagedir": "ltr",
        "touched": "2024-09-27T01:07:35Z",
        "lastrevid": 1231655023,
        "length": 1357,
        "talkid": 27595416,
        "fullurl": "https://en.wikipedia.org/wiki/Abdul_Baqi_Turkistani",
        "editurl": "https://en.wikipedia.org/w/index.php?title=Abdul_Baqi_Turkistani&action=edit",
        "canonicalurl": "https://en.wikipedia.org/wiki/Abdul_Baqi_Turkistani"
    }
}
```

The result from the ORES API call is stored in [articles_ores_scores.csv](HCDS/data-512-homework_2/intermediary_files/articles_ores_scores.csv). It has the following schema:

| Column Name          | Data Type | Description                                                                  |
| -------------------- | --------- | ---------------------------------------------------------------------------- |
| `revision_id`        | Integer   | Unique identifier for the revision of the article.                           |
| `quality_prediction` | String    | Predicted quality category of the article (e.g., Stub, Start, C, B, GA, FA). |
| `Probability B`      | Float     | Probability that the article belongs to quality class B.                     |
| `Probability C`      | Float     | Probability that the article belongs to quality class C.                     |
| `Probability FA`     | Float     | Probability that the article belongs to quality class FA (Featured Article). |
| `Probability GA`     | Float     | Probability that the article belongs to quality class GA (Good Article).     |
| `Probability Start`  | Float     | Probability that the article belongs to quality class Start.                 |
| `Probability Stub`   | Float     | Probability that the article belongs to quality class Stub.                  |

## Result files

[wp_countries-no_match.txt](HCDS/data-512-homework_2/result_files/wp_countries-no_match.txt): Contains the list of countries which have a mismatch, i.e. when we merge the wikipedia data and population data together these countries are not present is either.

[wp_politicians_by_country.csv](HCDS/data-512-homework_2/result_files/wp_politicians_by_country.csv): The countries which have a match.

_Feel free to use, modify, or contribute to this project while adhering to the MIT License._

### Research Reflection:

In this assignment, I gained valuable insights into the importance of combining domain knowledge with data analysis before embarking on a data science project. One key lesson learned is that the majority of data, especially on the internet, tends to have inherent biases. These biases can stem from various factors such as demographics, gender, or culture. Countries with lower literacy rates or limited internet access may also experience biases in data availability. Additionally, documentation and reproducibility are critical aspects of data science projects, carried over from previous lessons.

**What biases did you expect to find in the data (before you started working with it), and why?**

I expected to find biases related to regional representation, as smaller countries or regions with fewer internet users would likely have less content on Wikipedia but higher articles per capita. This assumption was confirmed as regions like Vermont and Alaska had disproportionately higher articles per capita due to their low population, while larger states like California and Arizona had lower articles per capita. Additionally, I discovered that non-native English-speaking regions tended to have fewer high-quality articles, suggesting a cultural-linguistic bias in the data.

**What might your results suggest about (English) Wikipedia as a data source?**

The results suggest that English Wikipedia, as a data source, is inherently biased due to its focus on English-language content. This creates a skewed view of the quality and coverage of topics, particularly for regions or communities where English is not the dominant language. Such biases can have implications for research or decision-making that rely on Wikipedia data, as it may not provide a fully accurate representation of global knowledge or perspectives.

**Can you think of a realistic data science research situation where using these data (to train a model, perform a hypothesis-driven research, or make business decisions) might create biased or misleading results, due to the inherent gaps and limitations of the data?**

Using this dataset to train a model could lead to biased or misleading results in real-world applications. For example, NLP tools trained on biased data like Wikipedia may amplify cultural and demographic biases. Models for content moderation or similar tasks may reflect the same biases found in internet-sourced data. The case of GPT-3 generating biased content against certain religions, like Islam, underscores the risks of training models on data with inherent cultural or ideological biases, which can have harmful outcomes, especially at scale.

By reflecting on these biases and understanding how they influence data-driven decisions, it becomes clear that qualitative considerations are just as important as quantitative ones. Both must be carefully balanced to produce meaningful, accurate, and fair results in data science research.

# Important considerations

In my analysis, I manually searched to determine if some individuals in our dataset were incorrectly identified as politicians. During this search, I found several notable figures, including Mohammad Khan, an Afghan athlete; Karen Sargsyan, an Armenian sociologist; Julius Lippert, an Austrian historian; and Rick James, an actor from Antigua and Barbuda. Although they come from diverse professions, each had engaged in political activities at some point. Given their political involvement, I decided to include them in my dataset for analysis.

One should be a little careful with the data. Crawling Wikipedia categories to identify relevant page subsets can result in misleading and/or duplicate category labels. Naturally, the data crawl attempted to resolve these, but not all may have been caught.

As well, Wikipedia categories are folksonomic, meaning there is very little control over how they are applied to pages. This means that the set of pages is very likely some kind of subset, and may have pages that are not actually about individual politicians. You should look for any data inconsistencies and document how you handle inconsistencies that you find.
