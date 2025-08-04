#  Solution to MATLAB and Simulink Challenge project number 210 Wetland Change-HSI


[Program link](https://github.com/mathworks/MATLAB-Simulink-Challenge-Project-Hub)

[link to the project :210](https://github.com/mathworks/MATLAB-Simulink-Challenge-Project-Hub/tree/main/projects/Change%20Detection%20in%20Hyperspectral%20Imagery)>


# Project details
A description of the implementation and the approached adopted.

🛰️ Project Details

This project focuses on detecting and mapping wetland loss using hyperspectral remote sensing. Multi-temporal hyperspectral data was analyzed in MATLAB to identify changes in water coverage over time.

✅ Implementation Overview

NDWI (Normalized Difference Water Index) was calculated from hyperspectral bands for multiple years.

ΔNDWI (change in NDWI over time) was used to detect waterbody shrinkage or expansion.

NDVI was optionally used to mask out vegetated areas and isolate open water.

The final output includes:

Wetland loss map

Binary change layer (wetland → non-wetland)

Area statistics showing total loss in square kilometers or percentage

This method helps quantify wetland shrinkage, track encroachment, and support environmental monitoring efforts.


# How to run section

Required Toolboxes and Resources

- **MATLAB Version:** R2021a or later (recommended for compatibility)
- **Image Processing Toolbox:** For image analysis and processing functions
- **Mapping Toolbox:** For geospatial data handling and visualization
- **Statistics and Machine Learning Toolbox (optional):** If classification or advanced analysis is included
- **Hyperspectral Dataset:** Sample data provided in the `data/` folder; use your own compatible hyperspectral imagery for custom analysis
- **Adequate System RAM and Storage:** Processing hyperspectral data can be memory-intensive; at least 8GB RAM recommended
- **Basic MATLAB Knowledge:** Familiarity with running scripts and managing the MATLAB environment
  
  How to run 
1. Ensure you have MATLAB (R2021a or later) installed with the Image Processing and Mapping Toolboxes.
2. Download or unzip the project files to your local machine.
3. Open MATLAB and add the project folder to your MATLAB path.
4. Open and run the main script (`main.m`) or the relevant script that executes the wetland degradation detection workflow.
5. The program will process the included sample data and generate output maps and statistics automatically.
6. Check the `output/` folder for generated results including degradation maps and area statistics.
   
# Demo
Add a video or animated gif/picture to showcase the code in operation.
  
# Reference
Add reference papers, data, or supporting material that has been used, if any.
