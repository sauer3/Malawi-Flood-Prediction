# Predicting Flood in Malawi

## Notebook Workflow
1. Feature-Extraction - This notebook extracts features from data generated with Google Earth Engine to use in modeling flood extent for Malawi.
2. Flood-Modeling - Trained regression model on data from 2015 flood and tested on 2019 flood. Tried several different algorithms and Catboost produced the best results. 
3. Visualization done in a variety of programs, mainly QGIS and Tableau.

## Overview
In recent decades, countries across Africa have experienced an increase in the frequency and severity of floods. Malawi is particularly vulnerable to flooding. In March 2019, Cyclone Idai impacted more than 922,900 people, with 56 deaths, 577 injuries, and more than 82,700 people were displaced. Food insecurity also rose sharply due to the destruction of crops in a country that is highly dependent on rainfed agriculture. 

## Goal
The vulnerability of this region is projected to increase with climate change. So, the goal of this project is to create a flood prediction model which will eventually lead to a flood planning app that governments can use to prepare for future flood impacts. 


## Data
Southern Malawi experienced major flooding in 2015 and again in 2019. So I used data from the flood of 2015 to train my model and then tested it with the flood data from 2019. 

#### Target
For the target variable I started with a polygon of the area that was flooded for each year. The map of southern Malawi is broken into 1 km sq rectangles and overlayed onto the flood exent. The percent area flooded was calculated for each rectangle and was used as the value for my target. 

#### Features:
Several of the features were extracted for the study area using Google Earth Engine code editor which allows processing on google cloud. 

- [Soil organic carbon](http://www.masdap.mw/layers/geonode:malawi_national_soil_organic_carbon0#more) (proxy for soil health and ecosystem condition)
- [% clay content of soil at 10cm](https://developers.google.com/earth-engine/datasets/catalog/OpenLandMap_SOL_SOL_CLAY-WFRACTION_USDA-3A1A1A_M_v02)
- Distance to [wetlands](http://www.masdap.mw/maps/523)
- [Landcover classes](https://developers.google.com/earth-engine/datasets/catalog/MODIS_006_MCD12Q1)
- [Elevation]( https://developers.google.com/earth-engine/datasets/catalog/USGS_SRTMGL1_003)
- [Topographic position index](https://developers.google.com/earth-engine/datasets/catalog/CSP_ERGo_1_0_Global_SRTM_mTPI)
- Total weekly precipitation 2 months before event

## Results

I ran several models and the best performing one was Catboost. 

The most important features were distance to wetlands, elevation, and clay content. 

I chose RMSE because it gives a relatively high weight to large errors. For this project large errors in any given cell are undesirable so I want to weigh them heavily. 
>My final RMSE score = .11

This means that my model can be off by 11% (percent area flooded) in any given rectangle over the map of Southern Malawi. 

