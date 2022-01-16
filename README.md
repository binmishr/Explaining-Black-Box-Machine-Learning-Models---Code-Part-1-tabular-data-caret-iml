# Explaining-Black-Box-Machine-Learning-Models---Code-Part-1-tabular-data-caret-iml

The details of the codeset and plots are included in the attached Microsoft Word Document (.docx) file in this repository. 
You need to view the file in "Read Mode" to see the contents properly after downloading the same.

IML Package - A Brief Introduction
=====================================

iml is an R package that interprets the behavior and explains predictions of machine learning models. It implements model-agnostic interpretability methods - meaning they can be used with any machine learning model.

Features
=========
        Feature importance
        Partial dependence plots
        Individual conditional expectation plots (ICE)
        Accumulated local effects
        Tree surrogate
        LocalModel: Local Interpretable Model-agnostic Explanations
        Shapley value for explaining single predictions

Installation
=============
The package can be installed directly from CRAN and the development version from GitHub:

# Stable version
install.packages("iml")

First we train a Random Forest to predict the Boston median housing value. How does lstat influence the prediction individually and on average? (Accumulated local effects)

    library("iml")
    library("randomForest")
    data("Boston", package = "MASS")
    rf = randomForest(medv ~ ., data = Boston, ntree = 50)
    X = Boston[which(names(Boston) != "medv")]
    model = Predictor$new(rf, data = X, y = Boston$medv)
    effect = FeatureEffects$new(model)
    effect$plot(features = c("lstat", "age", "rm"))

