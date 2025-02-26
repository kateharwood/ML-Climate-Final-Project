## 5/2
This week I wrote the final paper and cleaned up all the code. Thanks for a great semester!

## 4/27
This week I completed final validation of my best model, cleaned up the results slides and started creating a detailed outline for my paper.

Final Steps
- Write paper
- Clean up code
- Write README


## 4/20
(No entry last week because I was working on making the video presentation)

This week I worked on adding more data to my features, and trying different models. I dug into the NYC open data air quality dataset (really thorough, has everything like ozone, nitrogen, particulate matter, traffic density, even deaths from pollution), but realized that the geographical features were not granular enough (the smallest was on the UNH42 level) and the data did not go back far enough (earliest data was 2005). I realized that needing data from earlier than 2005 and as far bck as 1995 might be an issue since there wasn't as much data collection then as there is now! 

I searched the NYC open data site for datasets with lat and lon. I found the PLUTO dataset (Primary Land Use Tax Lot Output) which had relevant features like "land use" (what the lot is used for, ex: parkinglot, one family home, commercial, etc) and "num floors" (how many floors the building on the land plot has), and also went back further than 2005. I used the same methods as I did with the tree data to bin this data by lat and lon, and then joined it with the tree data. I also excluded buildings that were built after 2005, since we do not want to use that data.

I then experimented with using this data in the models. It is impt to note that because there were fewer lat/lon bins that were overlapping between the tree data and the PLUTO data, the overall dataset for this experiment had much fewer examples (3091 compared to over 500,000). In the paper I will dig much deeper into the methods and results I used to experiment with the new and old data and analyze the results, but a quick overview here:

The data including PLUTO features had better accuracy (.93) but a lower F1 score (.66) than the sole tree data (.81 and .75 respectively). I also analyzed which features were the most important (lat bin and num floors are most important, sidewalk cracks and wires are least important, more detail will be included in the paper). 

I also tried GradientBoosting and an SVM classifiers. The Gradient Boosting model performed about as well as the RandomForest, while the SVM did not perform as well.

I have a lot of ideas and more analysis that might give some insight into the *whys* of the results I obtained, which will be included in the paper.

Next Steps
- Create paper outline
- Run best models multiple times to get average results and stddev for final paper results
- Clean up code
- Write README
- Make the results slides better looking

## 4/6
I created geo visualizations of tree health and tree lat/lon bins to go along with the final project and to use in the video presentation.

Next Steps:
- Create video presentation
- Try adding air quality dataset
- Try another model type (maybe NN)
- Create paper outline

## 3/31
I played around with balancing the dataset in different ways: oversampling and undersampling. The undersampling performed poorly, but the oversampling boosted the accuracy of the RandomForestClassifier (the best performing model of the ones I tried last week) a few points to 81%. I then performed grid search cross validation, tuning the hyperparams (# of trees and decision criterion). The grid search ran for hours, and the best model used 1000 trees and entropy as the decision criteria, however there was no actual bump in scores when that model was run on test data vs. the model using the default params (100 trees and gini).

I also parsed and included the "wires" and "sidewalk cracked / raised" data from the original tree data. These are the only other non-location based features that both the 1995 and 2005 data have. Oddly, including this data made the accuracy of the RandomForestClassifier decrease slightly (81% -> 79%). I tried training on more trees to see if this would help since there were more features now, but it didn't improve the numbers.

The results from all these trials are included in the slides in the etc/ directory.

Next Steps:
- Create visualization of the trees and their health and lat/lon binning
- Start planning video presentation
- Look into adding another dataset (air quality)
- Potentially try other model types


## 3/23
Today I started playing with some baseline models using a few features (zip code, tree species, tree diameter, lat and lon bins). The target variable was the average health status of the lat/lon bin group of trees (rounded to one of 0,1,2,3). The dataset is unbalanced (way fewer 0s and 1s in the target variables), which could be something to fix in the future. (A note: each lat/lon bin group is approx the size of 1/4 a square city block.)

The logistic regression acheived 51% accuracy. A random forest classifier acheived 77% accuracy. I also tried linear regression and random forest regression. The target variables were the average health status of the lat/lon bin group of trees, unrounded (roughly ~350 distinct numbers). The linear regression achieved a R2 score of 0.01 and the random forest regression achieved a score of 0.41. Lat and lon bin values had the most influence as features in the random forest regressor.

TL;DR:
- Ran logistic reg, linear reg, random forest classifiction and regression models
- Random forest classifier showing some promise 

Next Steps (need to decide the order of importance of these):
- Potentially balance dataset?
- Look into adding more features (they are very messy and categorical and all over the place, this will be tricky)
- Try other model types on these features
- Try adding another dataset, like air quality. This requires matching on lat and lon again, and figuring out how I want the years to match up (am I still predicting future or not?)
- Later on: create visualization of trees and health statuses for presentation

## 3/9
Just saw the below note, thanks!

I spent today trying to finalize the data into something usable. I realized I had made a mistake on the lat / lon binning earlier, and had to rework my methodology. This took a while both in coming up with the right algorithm and figuring out the fancy pandas logic to make it work (in the end my implementation wasn't quite as magical as it could have been in pandas - I used a for loop!)

Now I have the parsed data ready to feed into a model. Next steps:
- Try logistic regression
- Check pairwise comparison of features
- Try random forest
- Either: add more features from tree dataset or add features from air quality dataset (this requires matching on lat/lon again...)

## 2022-03-07 check in: alp

Great. Would strongly encourage trying to cut corners to get to an initial model, no matter how bad it might be. Then you can swing back into the data wrangling with an additional set of ideas for new features etc.

## 3/1
I've spent this week really digging into the data wrangling. Learning and re-learning some aspects of pandas has taken some time. Figuring out how to normalize differently recorded features and values across datasets is a challenge, but it has been an interesting problem to grapple with.  I am focused for now on predicting tree health using the tree data itself, starting with a small set of the tree features, and will then hopefully be able to incorporate more tree features as well as other dataset(s).

The geospatial binning has also been an interesing problem to think about. I experimented with changing the size of the "box" I bin/group the trees by, but regardless of the size of the lat/lon box, there are some bins that include 100s of trees and some that include 1 tree. There doesn't seem to be a way around this, so I chose a "box" size that is roughly the same as 1/4 to 1/2 a city block. This is purely a subjective decision on what a reasonable grouping would look like; I believe that trees in the same part of a city block will probably have similar impacting factors on their health.

Next steps include:
- Continuing to parse the data into a format that is digestable by a model
- Trying out a simple logistic regression model using some tree data to get a baseline
- Based on these results, moving forward with other models and eventually other features/data



## 2/22
I've explored some other potential datasets for use as predictive features. The new datasets need to be able to join with the tree data on location, specifically lat and long. There is a temperature dataset on NYC Open Data that includes lat and long, and an air quality dataset that does not (but that might still be able to be joined with some extra code to parse the location data and transform it to lat and long coords). 

I've also been working more with the tree data, wrangling the data into featuresets that are usable. This will be my main focus moving forward now, as I'd like to see if it is feasible to predict tree health in the future using the tree data itself, before moving to use other datasets to predict contemporary tree health (rather than tree health in the future).

Next steps include:
- Figuring out how to get the same set of features across all tree datasets, given that the data collected are different for each census
- Feeding the finalized features and classes into a simple logistic regression model to get a baseline, then based on those results moving forward with other models if it seems like this approach is a good direction



## 2/15
Nicolas gave some good feedback: the fact that there are only two time periods in the data (1995-2005 and 2005-2015) poses an issue since effectively I am trying to do a time based prediction with only 3 time points. The result will probably be inconclusive results due to noise. Other options:
- Use this data (potentially augmented with other data that might pertain to tree health) to predict tree health (in the same time period)
- Use other data to predict tree health. The other data would need to at least have geospatially granular values on the street level for the 2005-2015 period and 2015-present period (and perhaps even good estimates extrapolating into the future to 2025). This could be air quality data, temperature data, noise data, etc.

Currently I am thinking I might try out multiple of these approaches. I am still curious about using the tree data to predict future tree health, and might try that first. If that shows inconclusive results due to not having enough time points, I can pivot to one of the other options.

Next steps include:
 - Finalizing parsing the tree data into groups
 - Potentially creating a visualization of the groupings (and tree health)
 - Exploring model and feature selection options
 - Exploring other potential datasets for use as predictive features


## 2/8
In keeping with the theme of urban planning, I have been scouring the NY Open Data site and exploring the datasets there. I have learned a lot about transportation, green space, green roofs, etc in NYC. One of the most interesting datasets to me is the NYC Street Tree dataset. This is a survey done every 10 years (1995, 2005, 2015) by volunteers mapping and gathering data about every single street tree in the city. There is extensive data about the tree and its health in these datasets (type of tree, if there are telephone wires in its canopy, cracks in the sidewalk, even if there are sneakers present in the branches). The overall health of the tree is also recorded on a categorical scale from Excellent to Dead (data also includes a category for "Stump"). There are >500,000 recorded trees.

My goal is to take the datasets from 2005 and 2015, and use the data recorded about the tree in 2005 to train a model to predict its health in 2015. If successful, this could be extrapolated and the tree data from 2015 could be fed into the model to predict tree health in 2025.

The biggest hurdle I've run into so far while exploring the data is that the treeId is not kept the same survey to survey, so there is no way to definitively match a tree across surveys. Each tree does have positional data: lat and long, as well as "state plane" coordinates, which seem to have roughly the same level of granularity as lat and long. Therefore I propose grouping the trees into sections based on their positional data. Each section could be a block long for example, or even half a block. I would then use all the data from the trees in that sector to predict the health of that sector (this could be by a majority vote of the trees in that area, an average, or some other decision method).

Other drawbacks I have identified about the data and this task: 
 - The data points recorded about the tree are not the same for each survey, so health data from 2015 would not be fed in to create the exact same features as the data from 2005.
 - There is a confounding factor in the time period between the data and the prediction. Not everything in the world in the span from 2015 to 2025 (or 2025 to 2035 etc) will be the held constant and match the span 2005 to 2015, so a model performing well on 2005 to 2015 data might not do as well on other decade spans.

The next step after data cleaning and grouping will be to decide what model types to experiment with. My first thought is to try out a linear regression model as the baseline, to get a number I can attempt to improve on. 

Datasets:
- 2005: https://data.cityofnewyork.us/Environment/2005-Street-Tree-Census/29bw-z7pj 
- 2015: https://data.cityofnewyork.us/Environment/2015-Street-Tree-Census-Tree-Data/uvpi-gqnh 



## 2/1

My initial idea is below:

Climate change is a polarizing topic, and many people still do not believe that it is real. Social media, and tweets in particular, are a great way to gauge the trending views on a topic over time. In this project, the aim will be to show not only how the trends of social media expressions of climate change belief/disbelief have changed over time, but also to compare how the trends in these beliefs vary with the occurrence of large-scale natural disasters. Are people more likely to talk about climate change when Texas experiences an unprecedented storm and a large swath of the state loses power? Or when Australia experiences one of the worst wildfire disasters in history? Do these events lead to an uptick in assertions of climate change belief, or an uptick in assertions of disbelief? Can we predict the public’s response to a natural disaster in terms of their expressions about climate change? As these natural disasters become more prevalent, understanding how they impact the public’s views on climate change could provide useful guidance on how best to target climate change related messaging. 

However, I’m also really interested in the urban planning aspect of climate science and how ML methods can help to create greener, more efficient cities. In the past week I have been spending many hours exploring urban transportation data in relation to climate change. I am interested in looking into different methods of transportation, including public transportation, ride-share services, and "last-mile" solutions like e-scooters and the new Revel moped scooters in NYC. I will continue exploring this dataspace this week before settling on a final project decision.
