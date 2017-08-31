# Analysis of Harvey-related TCEQ emissions reports

This repository contains data and Python code used to analyze emissions reports submitted by industrial facilities to the Texas Commission on Environmental Quality's Air Emission Event Reporting Database.

Please see the [related article](https://www.buzzfeed.com/zahrahirji/damage-from-harvey-has-caused-millions-of-pounds-of-toxic) for additional context.

## Table Of Contents

- [Data](#data)
    - [Inputs](#inputs)
    - [Outputs](#outputs)
- [Reproducibility](#reproducibility)
- [Feedback / Questions?](#feedback--questions)

# Data

## Inputs

The main inputs are the __TCEQ emissions reports__, scraped from [the commission's database](http://www2.tceq.texas.gov/oce/eer/index.cfm?fuseaction=main.searchForm). We started with [report number 265500](http://www2.tceq.texas.gov/oce/eer/index.cfm?fuseaction=main.getDetails&target=265500) and incremented the report number until we could find no more reports. The raw report pages, as HTML files, are available in the [`inputs/scraped-reports`](inputs/scraped-reports) folder.

We also created a text file, [`disaster-declaration-counties.txt`](inputs/disaster-declaration-counties.txt), listing the 54 counties that Gov. Greg Abbott [included on the State Disaster Declaration through Aug. 27](https://gov.texas.gov/news/post/governor-abbott-adds-additional-4-texas-counties-to-state-disaster-declaration).

Finally, the file [`reports-to-ignore.txt`](inputs/reports-to-ignore.txt) includes five emissions reports that either (a) predated Harvey's landfall and didn't clearly indicate a connection to the storm, or (b) appeared to be duplicative of previous reports.

## Outputs

In the [`00-parse-reports`](notebooks/00-parse-reports.ipynb) notebook, we extract structured data from the raw HTML reports, and save it to two files: 

- [`outputs/report-metadata-raw.csv`](outputs/report-metadata-raw.csv)
- [`outputs/report-emissions-raw.csv`](outputs/report-emissions-raw.csv)

In the [`01-analyze-reports`](notebooks/01-analyze-reports.ipynb) notebook, we analyze the data extracted from the reports, limiting the findings to reports (a) in the 54 counties above, (b) indicating an event-beginning date of August 23 or later, and (c) of the type "AIR SHUTDOWN" or "EMISSIONS EVENT". The main results can be found in these two files:

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
