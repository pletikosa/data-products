Estimating a House Price in San Francisco
=================================================================

**_Author: Irena Pletikosa Cvijikj_**

### Application Overview

This application provides a possibility for estimation of a price for a house located in San Francisco. It consists of three tabs:

1. House Price Estimation
2. Previous House Sales
3. About This App

In the continuation, a brief overview of the functionality covered on each of these tabs will be provided. 

***

**House Price Estimation**. This tab provides the results of the estimation. In order to estimate the price of a house, the user needs to provide the following information:

1. The year when the house of interest was built.
2. Number of bedrooms in the house
3. The size of the house, measured in square feet.
4. The size of the lot, measured in square feet.
5. The neighborhood in which the house is located.
6. The month when the house is planned to be sold/bought.

Based on this information, a price is calculated and displayed in the main part of the app. 

In addition, to gain an understanding on why this price was selected, a table is generated which contains records about previous sales for houses with similar characteristics. Similarity is measured based on the year when the house was built, the number of bedrooms and the neighborhood where the house is located. If at least any of these characteristics is the same as those chosen by the user, this historical record will be shown in the table.

***

**Previous House Sales**. This tab provides insights into the complete dataset used for the prediction task. In addition to the features used for the price prediction part, several additional characteristics are provided, such as the exact address of the house. 

On this tab the user has a possibility to search for specific records, by entering the information of interest, such as the neighborhood name, in the Search field provided in the top right corner.

***

**About This App**. This tab provides an explanation to the users about the possibilities provided in this app (i.e. it shows the current document).

***

### Price Prediction

**Dataset**. The model used for price estimation is based on the `nutshell::sanfrancisco.home.sales` dataset which contains 3281 observations of 15 variables. The listing given in continuation provides insights into the dataset structure:

```{r}
'data.frame':  3281 obs. of  15 variables:
 $ line        : int  65083 4893 4959 27880 78680 17110 11363 56564 4964 30465 ...
 $ county      : Factor w/ 1 level "San Francisco County": 1 1 1 1 1 1 1 1 1 1 ...
 $ street      : Factor w/ 3227 levels "1 Burnett Avenue",..: 1 2 3 4 5 6 7 8 9 10 ...
 $ city        : Factor w/ 1 level "San Francisco": 1 1 1 1 1 1 1 1 1 1 ...
 $ zip         : int  94131 94134 94107 94109 94109 94107 94124 94103 94117 94110 ...
 $ date        : Date, format: "2008-06-11" "2009-06-12" "2009-06-12" "2009-01-13" ...
 $ price       : int  1470000 385000 1043000 560000 419000 552000 228000 2200000 1475000 565000 ...
 $ bedrooms    : int  3 0 2 2 NA NA 0 3 0 2 ...
 $ squarefeet  : int  2424 1304 1400 1149 NA NA 1060 2873 1225 660 ...
 $ lotsize     : int  NA 2143 NA NA NA NA 2247 3140 NA 2365 ...
 $ year        : int  1983 1945 1997 1988 1988 NA NA 1919 1918 1918 ...
 $ latitude    : num  37.8 37.7 37.8 37.8 37.8 ...
 $ longitude   : num  -122 -122 -122 -122 -122 ...
 $ month       : Factor w/ 18 levels "2008-02-01","2008-03-01",..: 5 17 17 12 2 14 16 7 17 11 ...
 $ neighborhood: Factor w/ 34 levels "Bayview","Bernal Heights",..: 31 32 30 34 34 30 1 16 13 2 ...
```

More details on the dataset can be found [here](http://www.inside-r.org/packages/cran/nutshell/docs/sanfrancisco.home.sales).

***

**Prediction Model**. The model used for prediction is a simple linear model defined as follows:

```{r}
model <- lm(price ~ bedrooms + squarefeet + lotsize + month + neighborhood + year, data = sanfrancisco.home.sales)
```

***

**Code**. The complete code used for this application is available under [https://github.com/pletikosa/data-products](https://github.com/pletikosa/data-products).

