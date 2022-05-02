# Predicting NYC Street Tree Health

The importance of city greenery is growing with the increasing urbanization of the world.
Urban trees provide many benefits like temperature regulation, stormwater runoff reduction, and
air pollutant removal. However, trees must grow to maturity before many of these advantages
can be realized. Keeping vegetation thriving in a city is difficult, especially so for street
trees that cannot benefit from an urban park ecosystem. From living in concrete root beds in
the shadows of tall buildings, to serving as pets’ toilets and humans’ trash cans, urban trees
face many obstacles to staying alive and healthy [10]; the average life of a street tree in a dense
urban environment is only 13 years. Gaining information on what factors affect the health
of urban street trees can help facilitate the growth of vitally important green ecosystems in our
cities.

This research shows that the future health of New York City’s half a million street trees
can be predicted on a relatively granular level with fairly high accuracy using data collected
from NYC street tree censuses and publicly available land use data. Given information about
trees and the surrounding buildings in a quarter block radius, my models can predict the average
health of trees in the given area 10 years later with greater than 90% accuracy.

A variety of models were trained on different feature groupings, with the highest model
achieving an accuracy of 91.7% and a Macro F1 score 85.1% on a 4-way categorical health
status classification task. Location information and nearby building size are shown to be the
most important features for accurate prediction.


**Project Structure**
- `journal.md` contains weekly progress updates
- The `doc/` directory contains 
  - the final paper
  - a pdf of all the model results
  - images that are included in the final paper
  - video presentation of part of the work.
- The `src/` directory contains
  - the raw data and parsed data
  - code for parsing the data
  - code for training models on the data
  - code for creating geo visualizations of trees and health statuses

