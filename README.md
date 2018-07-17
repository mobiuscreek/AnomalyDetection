# AnomalyDetection R package

[![Build Status](https://travis-ci.org/twitter/AnomalyDetection.png)](https://travis-ci.org/twitter/AnomalyDetection)
[![Pending Pull-Requests](http://githubbadges.herokuapp.com/twitter/AnomalyDetection/pulls.svg?style=flat)](https://github.com/twitter/AnomalyDetection/pulls)
[![Github Issues](http://githubbadges.herokuapp.com/twitter/AnomalyDetection/issues.svg)](https://github.com/twitter/AnomalyDetection/issues)

This function is different from the original twitter AD in that it is able to perform AD
in more than a 1D array.  

--------------

AnomalyDetection is an open-source R package to detect anomalies which is
robust, from a statistical standpoint, in the presence of seasonality and an
underlying trend. The AnomalyDetection package can be used in wide variety of
contexts. For example, detecting anomalies in system metrics after a new
software release, user engagement post an A/B test, or for problems in
econometrics, financial engineering, political and social sciences.

## How the package works

The underlying algorithm – referred to as Seasonal Hybrid ESD (S-H-ESD) builds
upon the Generalized ESD test for detecting anomalies. Note that S-H-ESD can
be used to detect both global as well as local anomalies. This is achieved by
employing time series decomposition and using robust statistical metrics, viz.,
median together with ESD. In addition, for long time series (say, 6 months of
minutely data), the algorithm employs piecewise approximation - this is rooted
to the fact that trend extraction in the presence of anomalies in non-trivial -
for anomaly detection.

Besides time series, the package can also be used to detect anomalies in a
vector of numerical values. We have found this very useful as many times the
corresponding timestamps are not available. The package provides rich
visualization support. The user can specify the direction of anomalies, the
window of interest (such as last day, last hour), enable/disable piecewise
approximation; additionally, the x- and y-axis are annotated in a way to assist
visual data analysis.

## How to get started

Install the R package using the following commands on the R console:

```
install.packages("devtools")
devtools::install_github("mobiuscreek/AnomalyDetection")
library(AnomalyDetection)
```

The function AnomalyDetectionTs is called to detect one or more statistically
significant anomalies in the input time series. The documentation of the
function AnomalyDetectionTs, which can be seen by using the following command,
details the input arguments and the output of the function AnomalyDetectionTs.

```
help(AnomalyDetectionTs)
```

## A simple example

```
load(file='test_data.RDa')

```

Data for this example were downloaded from the BGS website for shale gas monitoring <sup>[1](#foot1)</sup>

Here's a part of our sample dataset and its columns:

```

View(df)

![Fig_2](https://github.com/mobiuscreek/AnomalyDetection/blob/master/figs/Fig2.png)

```

Notice that datetime column should be in a single column otherwise we will get an error. For the moment merging the two columns should suffice.

If the datetime column isn't single we do:

```

df$Date <- paste(df$Col1, df$Col1) 

```

Now we can run the function:

```
result=AnomalyDetectionTs(df,max_anoms=0.02,direction='both',pdftitle="Graph")

```

After running the function, it will create a pdf file called "Graph.pdf" in our working directory.

Let's open it, our AD will look like the following:


```
![Fig_1](https://github.com/mobiuscreek/AnomalyDetection/blob/master/figs/Fig1.png)

```



For a more detailed explanation visit on the AD algorithm:

https://github.com/twitter/AnomalyDetection


<a name="foot1">1</a>: http://www.bgs.ac.uk/research/groundwater/shaleGas/monitoring/lancsDataSummary.html


## Copyright and License
Copyright 2015 Twitter, Inc and other contributors

Licensed under the GPLv3
