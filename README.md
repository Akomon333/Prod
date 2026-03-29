A Python Flask API built in one week as a coding challenge. It analyzes uploaded images of meteorites to estimate their mineral composition, operational mining risk, and surface topology.
Because I didn't have much time, some values in calculations were taken randomly and may not be so accurate.


How it works:
Feature Extraction: The API uses OpenCV and Otsu's thresholding to separate the meteorite from the background. It calculates color averages (RGB), albedo, and surface depth (standard deviation).

Machine Learning Inference: The extracted stats are passed into a pre-trained XGBoost model to predict concentrations of Nickel, Iridium, and Gold. If the model file is missing or fails, the code uses a hardcoded fallback formula.

Operations Logic: The API takes UI inputs (orbit type and drill material) and applies multipliers to calculate the final value per ton, mission risk, and expected tool life.

Topology Mapping: It uses OpenCV's SimpleBlobDetector to find surface anomalies and creates a 128x128 pixel grid. This grid is smoothed with a Gaussian blur and returned as a list of lists to draw 3D terrain on a frontend.

Example of json:
{
  "composition": {
    "nickel_pct": 10.5,
    "iridium_ppm": 3.2,
    "gold_ppm": 0.8
  },
  "economics": {
    "value_usd_per_ton": 2500.0
  },
  "engineering": {
    "hardness_score": 80.0,
    "mission_risk": 45.0,
    "tool_life_hrs": 500.0,
    "abrasive_index": 12.0
  },
  "visual_params": {
    "albedo": 0.25,
    "displacement_scale": 0.5,
    "topology": [[0, 0, ...], [...]]
  }
}


![Dashboard Showcase 1](Photos/showcase2.PNG)

![Meteorite Photo](Photos/meteoritetest.jpg)

![Dashboard Showcase 2](Photos/showcase1.PNG)
