# Article.DatastreamEikonAPI.Python.ForecastingInflationRomanianCaseStudyUsingSARIMAModels

## [See original article here](https://developers.refinitiv.com/en/article-catalog/article/forecasting-inflation-romanian-case-study-using-sarima-models)

In this article, we look at (i) how to merge [Datastream](https://www.refinitiv.com/en/products/datastream-macroeconomic-analysis) and [Eikon](https://developers.refinitiv.com/en/api-catalog/eikon/eikon-data-api) / [Refinitiv Data Platform (RDP)](https://developers.refinitiv.com/en/api-catalog/refinitiv-data-platform/refinitiv-data-platform-apis) data in Python and (ii) how one may choose an optimal SARIMA model by selecting the one with lowest in-sample errors. We also look into how one may use both Eikon and Datastream data together, as well as statistical concepts of stationarity and differencing among others. We also investigate and compare models only using comparative months (*e.g.*: Jan. with Jan., Feb. with Feb., *etc.*).

We find that the optimal model is a SARIMA(5,0,4)(4,0,0)12}.

To do so we look at (i) how one may check for stationarity graphically and via (ADF, KPSS & PP) test statistics, (ii) differencing, (iii) ex-ante (before modelling) parameter identification via autocorrelation & partial autocorrelation functions, (iv) the difference between Autoregressive Moving Average (ARMA) & Seasonal Integrated ARMA (SARIMA) models, (v) ex-post (after modelling) parameter identification via information criteria and mean of absolute & squared errors (as well as the use of Python's 'pickle' library), (vi) how one may choose an optimal model specification - reducing errors, (vii) recursive one-step-ahead out-of-sample forecasts, and finally (iix) corresponding month models before concluding.

As a precursor to ARMA modelling, the reader is advised to look read '[Information Demand and Stock Return Predictability (Coded in R): Part 2: Econometric Modelling of Non-Linear Variances](https://developers.refinitiv.com/en/article-catalog/article/information-demand-and-stock-return-predictability-coded-in-r-part-2)' - an article without coding that looks into our methods of modelling.

## Contents

* [What are SARIMA Models?](#whataresarimamodels)
* [Get to Coding](#gettothecoding)
    * [Development Tools & Resources](#developmenttoolsandresources)
    * [Import Libraries](#importlibraries)
* [Data Sets](#datasets)
    * [Collecting Datastream Data](#collectingdatastreamdata)
    * [Collecting Eikon data](#collectingeikondata)
    * [Joining the Datastream and Eikon data-frames together](#joiningthedatastreamandeikondataframestogether)
* [Stationarity](#stationarity)
    * [Checking For Stationarity Via Graphical Analysis](#checkingforstationarityviagraphicalanalysis)
    * [Checking For Stationarity Via Test Statistics](#checkingforstationarityviateststatistics)
        * [Interpreting the stationarity table](#Interpretingthestationaritytable)
    * [Differencing](#differencing)
* [Modelling](#modelling)
    * [Ex-Ante Parameter Identification: Autocorrelation and Partial Autocorrelation Functions](#exanteparameteridentification)
        * [ARMA(5,2)](#ARMA52)
        * [SARIMA(5,0,2)(1, 0, 0)12](#SARIMA50210012)
    * [Ex-Post Parameter Identification: Information Criteria and Mean of Absolute & squared Errors](#expostparameteridentification)
        * [Graphical Analysis](#graphicalanalysis)
        * [Information Criteria](#informationcriteria)
        * [Mean Squared Errors and Sum of squared Errors](#meansquarederrorsandsumofsquarederrors)
            * [Pickle](#pickle)
            * [pmdarima](#pmdarima)
    * [Optimal Model](#optimalmodel)
        * [Fitted values of our 'Optimal Model'](#Fittedvaluesofouroptimalmodel)
        * [Recursive One-Step-Ahead Out-of-Sample Forecasts](#recursiveonestepaheadoutofsampleforecasts)
    * [corresponding Month Model](#correspondingmonthmodel)
        * [Check the best SAMIMA model with ARMA(0,0) imposed](#first)
        * [Fit the sarima0,0,0,3,0,0,12 model](#second)
        * [Recursive One-Step-Ahead Out-of-Sample Forecasts](#third)
    * [Comparing Models](#comparingmodels)
* [Conclusion](#conclusion)
* [References](#references)
