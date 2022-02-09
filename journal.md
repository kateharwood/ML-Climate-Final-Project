## 2/8
In keeping with the theme of urban planning, I have been scouring the NY Open Data site and exploring the datasets there. I have learned a lot about transportation, green space, green roofs, etc in NYC. One of the most interesting datasets to me is the NYC Street Tree dataset. This is a survey done every 10 years (1995, 2005, 2015) by volunteers mapping and gathering data about every single street tree in the city. There is extensive data about the tree and its health in these datasets (type of tree, if there are telephone wires in its canopy, cracks in the sidewalk, even if their are sneakers present in the branches). The overall health of the tree is also recorded on a categorical scale from Excellent to Dead (data also includes a category for "Stump"). There are >500,000 recorded trees.

My goal is to take the datasets from 2005 and 2015, and use the data recorded about the tree in 2005 to train a model to predict its health in 2015. If successful, this could be extrapolated and the tree data from 2015 could be fed into the model to predict tree health in 2025.

The biggest hurdle I've run into so far while exploring the data is that the treeId is not kept the same survey to survey, so there is no way to definitively match a tree across surveys. Each tree does have positional data: lat and long, as well as "state plane" coordinates, which seem to have roughly the same level of granularity as lat and long. Therefore I propose grouping the trees into sections based on their positional data. Each section could be a block long for example, or even half a block. I would then use all the data from the trees in that sector to predict the health of that sector (this could be by a majority vote of the trees in that area, an average, or some other decision method).

Other drawbacks I have identified about the data and this task: 
 - The data points recorded about the tree is not the same for each survey, so health data from 2015 would not be fed in to create the exact same features as the data from 2005.
 - There is a confounding factor in the time period between the data and the prediction. Not everything in the world in the span from 2015 to 2025 (or 2025 to 2035 etc) will be the held constant and match the span 2005 to 2015, so a model performing well on 2005 to 2015 data might not do as well on other decade spans.

The next step after data cleaning and grouping will be to decide what model types to experiment with. My first thought is to try out a linear regression model as the baseline, to get a number I can attempt to improve on. 

Datasets:
- 2005: https://data.cityofnewyork.us/Environment/2005-Street-Tree-Census/29bw-z7pj 
- 2015: https://data.cityofnewyork.us/Environment/2015-Street-Tree-Census-Tree-Data/uvpi-gqnh 



## 2/1

My initial idea is below:

Climate change is a polarizing topic, and many people still do not believe that it is real. Social media, and tweets in particular, are a great way to gauge the trending views on a topic over time. In this project, the aim will be to show not only how the trends of social media expressions of climate change belief/disbelief have changed over time, but also to compare how the trends in these beliefs vary with the occurrence of large-scale natural disasters. Are people more likely to talk about climate change when Texas experiences an unprecedented storm and a large swath of the state loses power? Or when Australia experiences one of the worst wildfire disasters in history? Do these events lead to an uptick in assertions of climate change belief, or an uptick in assertions of disbelief? Can we predict the public’s response to a natural disaster in terms of their expressions about climate change? As these natural disasters become more prevalent, understanding how they impact the public’s views on climate change could provide useful guidance on how best to target climate change related messaging. 

However, I’m also really interested in the urban planning aspect of climate science and how ML methods can help to create greener, more efficient cities. In the past week I have been spending many hours exploring urban transportation data in relation to climate change. I am interested in looking into different methods of transportation, including public transportation, ride-share services, and "last-mile" solutions like e-scooters and the new Revel moped scooters in NYC. I will continue exploring this dataspace this week before settling on a final project decision.
