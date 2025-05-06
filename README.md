# Comparing HAND-Based and Random Forest Flood Models Using Sentinel-1 Ground Truth

This project evaluates the accuracy of two flood prediction models against a reference flood extent derived from Sentinel-1 SAR change detection. The study area is Harris County, Texas, during the 2017 Hurricane Harvey. 

## Summary of Workflow

- **Study Area**  
  Used a local GeoJSON file for Harris County and uploaded it to Earth Engine as a FeatureCollection to define the area of interest (AOI).

- **Ground Truth Creation**  
  - Generated a flood extent map using Sentinel-1 Synthetic Aperture Radar (SAR) imagery from before and after the flooding event.  
  - Applied a  change detection technique to identify likely inundated areas.  
  - This Sentinel-derived map served as the ground truth for evaluating both models.

- **Model 1: HAND-Based Prediction**  
  - Used a HAND (Height Above Nearest Drainage) raster.  
  - Applied a threshold to identify potentially inundated areas.  
  - Optimized the threshold by iterating over values and selecting the one that maximized the F1 score compared to the Sentinel-1 ground truth.

- **Model 2: Random Forest Classification**  
  - Built a Random Forest model using GEE’s `ee.Classifier.smileRandomForest`.  
  - Input features included land cover type and accumulated precipitation.  
  - Labeled pixels using the Sentinel-1 flood map and trained the model on a stratified random sample of points within the AOI.  
  - Evaluated its prediction across the full AOI.

- **Evaluation**  
  - For both models, compared predicted flood maps to the Sentinel-1 reference.  
  - Generated true positive, false positive, false negative, and true negative maps.  
  - Calculated accuracy, precision, recall, and F1 scores.  
