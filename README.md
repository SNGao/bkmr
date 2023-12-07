### Basic information

**Title:** BKMR

**Package Author**: Jennifer F. Bobb

**Website Author:** Sunan Gao

**Description:** The R package `bkmr` implements Bayesian kernel machine
regression, a statistical approach for estimating the joint health
effects of multiple concurrent exposures. Additional information on the
statistical methodology and on the computational details are provided in
[Bobb et al.
2015](https://academic.oup.com/biostatistics/article/16/3/493/269719).
More recent extensions, details on the software, and worked-through
examples are provided in [Bobb et al.
2018](https://ehjournal.biomedcentral.com/articles/10.1186/s12940-018-0413-y).

**Original R package came from** [Link](https://github.com/jenfb/bkmr)

**Deployed Website** [Link]()

### Customized things in pkgdown website

``` r
  theme: breeze-light  # using the "breeze-light" theme
  bslib:
    bg: '#202123' # Specifies the background color for the website.
    fg: '#B8BCC2' # Specifies the foreground (text) color for the website.
    primary: '#306cc9' # Specifies the primary color used for links and other elements.
  navbar:
    bg: primary # Sets the background color of the navigation bar
    structure:
      left: search # Places a search bar on the left side of the navigation bar.
      right:
      - reference
      - articles
  footer:
    structure:
      left: developed_by # Specifies content on the left side of the footer
      right: built_with # Specifies content on the right side of the footer
```

#### Exported function list
```r
ComputePostmeanHnew():  #Compute the posterior mean and variance of h at a
new predictor values

ExtractEsts(): #Extract summary statistics

ExtractPIPs(): #Extract posterior inclusion probabilities (PIPs) from
BKMR model fit

ExtractSamps(): #Extract samples

InvestigatePrior(): #Investigate prior

OverallRiskSummaries(): #Calculate overall risk summaries

PlotPriorFits(): #Plot of exposure-response function from univariate KMR
fit

PredictorResponseBivar(): #Predict the exposure-response function at a
new grid of points

PredictorResponseBivarLevels(): #Plot cross-sections of the bivariate predictor-response function

PredictorResponseBivarPair(): #Plot bivariate predictor-response function on a new grid of points

PredictorResponseUnivar(): #Plot univariate predictor-response function on a new grid of points

SamplePred(): #Obtain posterior samples of predictions at new points
SimData(): #Simulate dataset

SingVarIntSummaries(): #Single Variable Interaction Summaries

SingVarRiskSummaries(): #Single Variable Risk Summaries

TracePlot(): #Trace plot

kmbayes(): #Fit Bayesian kernel machine regression

print(<bkmrfit>): #Print basic summary of BKMR model fit

summary(<bkmrfit>): #Summarizing BKMR model fits
```

### A basic example with one of the functions (fitkm).

``` r
library(bkmr)
library(ggplot2)

set.seed(111)
dat <- SimData(n = 50, M = 4)
y <- dat$y
Z <- dat$Z
X <- dat$X
set.seed(111)
fitkm <- kmbayes(y = y, Z = Z, X = X, iter = 10000, verbose = FALSE, varsel = TRUE)
TracePlot(fit = fitkm, par = "beta")
ggplot(pred.resp.univar, aes(z, est, ymin = est - 1.96*se, ymax = est + 1.96*se)) + 
    geom_smooth(stat = "identity") + 
    facet_wrap(~ variable) +
  ylab("h(z)")
```

### Install instructions

You can install the latest released version of `bkmr` from CRAN with:

``` r
install.packages("bkmr")
```

Or the latest development version from github with:

``` r
install.packages("devtools")
devtools::install_github("jenfb/bkmr")
```

For a general overview and guided examples, go to
<https://jenfb.github.io/bkmr/overview.html>.

For examples from the software paper, please see

-   <https://jenfb.github.io/bkmr/SimData1>
-   <https://jenfb.github.io/bkmr/ProbitEx>
