# Analysis of Harvey-related TCEQ emissions reports — September update

This repository contains data and Python code used to analyze emissions reports submitted by industrial facilities to the Texas Commission on Environmental Quality's Air Emission Event Reporting Database. It updates, and slightly expands, a [similar analysis from late August](https://github.com/BuzzFeedNews/2017-08-harvey-emissions-reports).

Please see [this related article](https://www.buzzfeed.com/nidhisubbaraman/tropical-storm-harvey-emissions-pollution) for additional context.

## Table Of Contents

- [Data](#data)
    - [Inputs](#inputs)
    - [Outputs](#outputs)
- [Reproducibility](#reproducibility)
- [Feedback / Questions?](#feedback--questions)

# Data

## Inputs

The main inputs are the __TCEQ emissions reports__, scraped from [the commission's database](http://www2.tceq.texas.gov/oce/eer/index.cfm?fuseaction=main.searchForm). For __recent__ emissions reports, we started with [report number 265500](http://www2.tceq.texas.gov/oce/eer/index.cfm?fuseaction=main.getDetails&target=265500) and incremented the report number until we could find no more reports, as of the morning of Sept. 14, 2017. Those raw report pages, as HTML files, are available in the [`inputs/scraped-reports`](inputs/scraped-reports) folder.

For the 48 facilities we identified as reporting Harvey-related emissions, we also scraped their reports of emissions events that began or ended in 2015 or 2016, using TCEQ's Central Registry ([e.g.](http://www15.tceq.texas.gov/crpub/index.cfm?fuseaction=iwr.eeincdetail&addn_id=895600322009251&re_id=177634852002163)). Those __historical__ emissions reports can be found in the  [`inputs/scraped-reports-historical`](inputs/scraped-reports-historical) folder.

We also created a text file, [`disaster-declaration-counties.txt`](inputs/disaster-declaration-counties.txt), listing the 54 counties that Gov. Greg Abbott [included on the State Disaster Declaration through Aug. 27](https://gov.texas.gov/news/post/governor-abbott-adds-additional-4-texas-counties-to-state-disaster-declaration).

Finally, the file [`reports-to-ignore.txt`](inputs/reports-to-ignore.txt) includes emissions reports that, based on reporting, either appear to be duplicative of subsequent reports or appear to be unrelated to Harvey.

## Outputs

In the [`00-parse-reports`](notebooks/00-parse-reports.ipynb) notebook, we extract structured data from the raw HTML reports, and save it to two files: 

- [`outputs/report-metadata-raw.csv`](outputs/report-metadata-raw.csv)
- [`outputs/report-emissions-raw.csv`](outputs/report-emissions-raw.csv)
- [`outputs/report-metadata-raw-historical.csv`](outputs/report-metadata-raw-historical.csv)
- [`outputs/report-emissions-raw-historical.csv`](outputs/report-emissions-raw-historical.csv)

In the [`01-analyze-reports`](notebooks/01-analyze-reports.ipynb) notebook, we analyze the data extracted from the reports, limiting the findings to reports (a) in the 54 counties above, (b) indicating an event-beginning date of August 23 or later, and (c) of the type "AIR SHUTDOWN", "AIR STARTUP", or "EMISSIONS EVENT". The main results can be found in these two files:

- [`outputs/largest-emissions-in-lbs.csv`](outputs/largest-emissions-in-lbs.csv)
- [`outputs/facilities-with-most-emissions-lbs.csv`](outputs/facilities-with-most-emissions-lbs.csv)


# Reproducibility

To reproduce the findings, you'll need to do the following:

- Ensure that you have installed [Jupyter](http://jupyter.org/), [Python](https://www.python.org/), and the Python libraries listed in [`requirements.txt`](requirements.txt)
- Clear the [`output/`](output/) directory. (Shortcut: run `make clear`.)
- Use Jupyter to run each notebook in the [`notebooks/`](notebooks/) directory consecutively. (Shortcut: run `make reproduce`; requires Python 3.)

# Feedback / Questions?

Contact Jeremy Singer-Vine at [jeremy.singer-vine@buzzfeed.com](jeremy.singer-vine@buzzfeed.com).

Looking for more from BuzzFeed News? [Click here for a list of our open-sourced projects, data, and code](https://github.com/BuzzFeedNews/everything).
