
<img src="man/figures/ShinyQDA.png" align="right" width="120" align="right" />

# ShinyQDA: R Package and Shiny Application for the Analysis of Qualitative Data

<!-- badges: start -->

[![](https://img.shields.io/badge/devel%20version-0.5.0-blue.svg)](https://github.com/jbryer/ShinyQDA)
[![](https://www.r-pkg.org/badges/version/ShinyQDA)](https://cran.r-project.org/package=ShinyQDA)
[![Project Status: Active - The project has reached a stable, usable
state and is being actively
developed.](https://www.repostatus.org/badges/latest/active.svg)](https://www.repostatus.org/#active)
[![](https://img.shields.io/github/last-commit/jbryer/ShinyQDA.svg)](https://github.com/jbryer/ShinyQDA/commits/main)
[![R-CMD-check](https://github.com/jbryer/ShinyQDA/actions/workflows/R-CMD-check.yaml/badge.svg)](https://github.com/jbryer/ShinyQDA/actions/workflows/R-CMD-check.yaml)
<!-- badges: end -->

The `ShinyQDA` package is designed to assist researchers with the
analysis of qualitative data. As the name suggests, the premise is that
much of the interaction with the package will be done through a
[Shiny](https://shiny.rstudio.com) application. However, all the
functionality in the Shiny application is available through through the
R command line as well. `ShinyQDA` attempts to set in between
traditional qualitative data analysis that involves researchers coding
and/or scoring (using rubrics) documents/text and natural language
processing such as sentiment analysis, topic modeling, and text encoding
(i.e. tokenization). By using Shiny, multiple researchers can access the
application to code and/or score documents.

*Note: Qualitative data researchers tend to refer to the text they
analyze as documents. Natural language processing researchers tend to
refer to the data as text data. We try to prefer to use the phrase most
appropriate for how a feature may be used, but they can often be used
interchangeably. *

![Screencast of ShinyQDA](man/figures/ShinyQDA_screencast.gif)

To install, use the `remotes` package:

    remotes::install_github('jbryer/ShinyQDA')

Run the Shiny app with:

    ShinyQDA::shinyQDA()

## Setup

    qda_data <- qda(file = 'ShinyQDA.sqlite')

## Sentiment Analysis

    app_dir <- './'
    textdata::lexicon_afinn(dir = app_dir)
    textdata::lexicon_bing(dir = app_dir)
    textdata::lexicon_loughran(dir = app_dir)
    textdata::lexicon_nrc(dir = app_dir)

## Authentication

Authentication is handled by the
[`shinymanager`](https://datastorm-open.github.io/shinymanager/) R
package. By default, if authentication is enabled, ShinyQDA will create
an administrator user with `admin` and `pass` as the username and
password. We recommend changing the password after your first sign-in.
User management (including password changing) is handled by clicking the
plus (`+`) icon in the lower right hand corner. This will take you into
`shinymanager`’s user management mode. All data entered into ShinyQDA
has a username associated with it. When in authentication mode the
username will be retrieved from `shinymanager`, otherwise ShinyQDA will
use the value of `Sys.info()['user']`.

## Current Features

Data entry features

- User management via the
  [`shinymanager`](https://datastorm-open.github.io/shinymanager/)
  package to allow multiple coders to work on the same dataset over the
  internet.
- Define an arbitrary set of questions/codes to assign to each document.
  Current question types include checkbox (for multiple selections),
  radio (for choose one from a list), and open text.
- Highlight text (e.g. word, sentence, paragraph, etc.) of text to code.
  This will open a modal dialog to add codes.
- Define an arbitrary set of questions/codes to assign to each coding
  (i.e. highlighted text). Current question types include checkbox (for
  multiple selections), radio (for choose one from a list), and open
  text.
- Score documents using a rubric.

Analysis features:

- Basic descriptive information for individual documents including
  character, word, sentence, and paragraph counts.
- Sentiment analysis at the individual document level. Words within the
  document that appear in the specified sentiment dictionary are
  highlighted and color coded to correspond to a histogram of the
  sentiments within a single document.
- Sentiment analysis across the entire database. Varying plots are
  provided approproate to the sentiment dictionary specified.
- Co-occurrence plot to examine how codes co-occur across documents.
- Word frequency analysis across the entire database.
- Code frequency analysis across all codes entered.
- Word clouds.

Data export features:

- A data table view showing all documents along with imported metadata,
  codes, code question responses, document descriptive statistics, and
  sentiment. Data can be exported/downloaded as CSV or Excel.
- A raw database view is provided with the ability to export/download as
  Excel (using multiple tabs) or raw SQLite database.

## Roadmap

- Merge coding results into data export tab. Allow user to choose
  aggregation method.
- Inter-rater reliability analysis
- Topic modeling
- Tokenization - allow the user to define and export/download various
  tokenization schemes.
- Predictive modeling - use any data (including sentiment, topics,
  tokenizations, etc.) to predict an outcome.
- Queuing and user roles - Create a scheme to limit access to certain
  features depending on user role. Allow documents to be assigned to
  users to code/score.
- Make the app prettier / improve the design. An alternative design has
  been started in inst/bs4dash/
- Convert the coding tab to use the Shiny module framework.
- New hex logo (my design skills are not great, looking for a volunteer
  😜)
- Submit to CRAN when development is stable.
