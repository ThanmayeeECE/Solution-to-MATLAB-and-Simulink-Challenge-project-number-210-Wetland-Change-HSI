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

**MONSOON CODE**

%% NDWI CALCULATION FOR MONSOON SCENES (e.g., Monsoon 2019)

% Clear workspace and command window

clc;

clear;

%% Step 1: Set File Paths for Monsoon Scene

% Replace these with the full or relative path to your Landsat monsoon images

green_band_file = 'C:\\Users\\91998\\MATLAB Drive\\proooo\\2019-20\\LC08_L2SP_144053_20190601_20200828_02_T1_SR_B3.TIF'; % Band 3 (Green)

nir_band_file = 'C:\\Users\\91998\\MATLAB Drive\\proooo\\2019-20\\LC08_L2SP_144053_20190601_20200828_02_T1_SR_B5.TIF'; % Band 5 (NIR)

%% Step 2: Load Bands Using readgeoraster

\[green, R\] = readgeoraster(green_band_file); % Spatial reference info R

nir = readgeoraster(nir_band_file);

% Convert to double for calculation

green = double(green);

nir = double(nir);

%% Step 3: Compute NDWI

ndwi = (green - nir) ./ (green + nir + eps); % eps avoids division by zero

ndwi_2019_monsoon = ndwi;

save('ndwi_2019_monsoon.mat', 'ndwi_2019_monsoon');

%% Step 4: Display NDWI Map

figure;

imagesc(ndwi, \[-1, 1\]); % Typical NDWI range

colormap('jet');

colorbar;

title('NDWI Map - Vembanad Lake (Monsoon 2019)');

xlabel('Pixels');

ylabel('Pixels');

%% Step 5: Generate Water Mask from NDWI

% Adjust threshold if needed (e.g., 0.2 → 0.05 → 0.0)

water_mask = ndwi > 0.01;

% Display water mask as binary image

figure;

imshow(water_mask);

title('Water Pixels Mask (NDWI > 0.01)');

%% Step 6: Estimate Wetland Area (in sq.km)

% Each pixel = 30m × 30m = 900 m² = 0.0009 km²

num_water_pixels = sum(water_mask(:));

wetland_area_km2 = num_water_pixels \* 0.0009;

fprintf(' Estimated Wetland Area (Monsoon 2019): %.2f sq.km\\n', wetland_area_km2);

wetland_2019_summer = wetland_area_km2;

%% Step 7: Save Outputs for Later Comparison

% Save NDWI image (normalized to 0-1)

ndwi_image = mat2gray(ndwi);

imwrite(ndwi_image, 'NDWI_2019_Monsoon.png');

% Save water mask

imwrite(water_mask, 'WaterMask_2019_Monsoon.png');

save('NDWI_2019_Monsoon.mat', 'ndwi');

%% NDWI CALCULATION FOR MONSOON SCENES (e.g., Monsoon 2020)

% Clear workspace and command window

clc;

clear;

%% Step 1: Set File Paths for Monsoon Scene

% Replace these with the full or relative path to your Landsat monsoon images

green_band_file = 'C:\\Users\\91998\\MATLAB Drive\\proooo\\2020\\LC08_L2SP_144053_20200721_20200911_02_T1_SR_B3.TIF'; % Band 3 (Green)

nir_band_file = 'C:\\Users\\91998\\MATLAB Drive\\proooo\\2020\\LC08_L2SP_144053_20200721_20200911_02_T1_SR_B5.TIF'; % Band 5 (NIR)

%% Step 2: Load Bands Using readgeoraster

\[green, R\] = readgeoraster(green_band_file); % Spatial reference info R

nir = readgeoraster(nir_band_file);

% Convert to double for calculation

green = double(green);

nir = double(nir);

%% Step 3: Compute NDWI

ndwi = (green - nir) ./ (green + nir + eps); % eps avoids division by zero

% figure;

% histogram(ndwi(:), 50);

% title('NDWI Histogram - Monsoon 2020');

% xlabel('NDWI Value');

% ylabel('Pixel Count');

ndwi_2020_monsoon = ndwi;

save('ndwi_2020_monsoon.mat', 'ndwi_2020_monsoon');

%% Step 4: Display NDWI Map

figure;

imagesc(ndwi, \[-1, 1\]); % Typical NDWI range

colormap('jet');

colorbar;

title('NDWI Map - Vembanad Lake (Monsoon 2020)');

xlabel('Pixels');

ylabel('Pixels');

%% Step 5: Generate Water Mask from NDWI

% Adjust threshold if needed (e.g., 0.2 → 0.05 → 0.0)

water_mask = ndwi > 0.01;

% Display water mask as binary image

figure;

imshow(water_mask);

title('Water Pixels Mask (NDWI > 0.05)');

%% Step 6: Estimate Wetland Area (in sq.km)

% Each pixel = 30m × 30m = 900 m² = 0.0009 km²

num_water_pixels = sum(water_mask(:));

wetland_area_km2 = num_water_pixels \* 0.0009;

fprintf(' Estimated Wetland Area (Monsoon 2020): %.2f sq.km\\n', wetland_area_km2);

wetland_2020_summer = wetland_area_km2;

%% Step 7: Save Outputs for Later Comparison

% Save NDWI image (normalized to 0-1)

ndwi_image = mat2gray(ndwi);

imwrite(ndwi_image, 'NDWI_2020_Monsoon.png');

% Save water mask

imwrite(water_mask, 'WaterMask_2020_Monsoon.png');

save('NDWI_2020_Monsoon.mat', 'ndwi');

%% NDWI CALCULATION FOR MONSOON SCENES (e.g., Monsoon 2022)

% Clear workspace and command window

clc;

clear;

%% Step 1: Set File Paths for Monsoon Scene

% Replace these with the full or relative path to your Landsat monsoon images

green_band_file = 'C:\\Users\\91998\\MATLAB Drive\\proooo\\2022-23\\LC09_L2SP_144053_20220921_20230328_02_T1_SR_B3.TIF'; % Band 3 (Green)

nir_band_file = 'C:\\Users\\91998\\MATLAB Drive\\proooo\\2022-23\\LC09_L2SP_144053_20220921_20230328_02_T1_SR_B5.TIF'; % Band 5 (NIR)

%% Step 2: Load Bands Using readgeoraster

\[green, R\] = readgeoraster(green_band_file); % Spatial reference info R

nir = readgeoraster(nir_band_file);

% Convert to double for calculation

green = double(green);

nir = double(nir);

%% Step 3: Compute NDWI

ndwi = (green - nir) ./ (green + nir + eps);% eps avoids division by zero

% figure;

% histogram(ndwi(:), 50);

% title('NDWI Histogram - Monsoon 2022');

% xlabel('NDWI Value');

% ylabel('Pixel Count');

ndwi_2022_monsoon = ndwi;

save('ndwi_2022_monsoon.mat', 'ndwi_2022_monsoon');

%% Step 4: Display NDWI Map

figure;

imagesc(ndwi, \[-1, 1\]); % Typical NDWI range

colormap('jet');

colorbar;

title('NDWI Map - Vembanad Lake (Monsoon 2022)');

xlabel('Pixels');

ylabel('Pixels');

%% Step 5: Generate Water Mask from NDWI

% Adjust threshold if needed (e.g., 0.2 → 0.05 → 0.0)

water_mask = ndwi > 0.01;

% Display water mask as binary image

figure;

imshow(water_mask);

title('Water Pixels Mask (NDWI > 0.05)');

%% Step 6: Estimate Wetland Area (in sq.km)

% Each pixel = 30m × 30m = 900 m² = 0.0009 km²

num_water_pixels = sum(water_mask(:));

wetland_area_km2 = num_water_pixels \* 0.0009;

fprintf(' Estimated Wetland Area (Monsoon 2022): %.2f sq.km\\n', wetland_area_km2);

wetland_2022_summer = wetland_area_km2;

%% Step 7: Save Outputs for Later Comparison

% Save NDWI image (normalized to 0-1)

ndwi_image = mat2gray(ndwi);

imwrite(ndwi_image, 'NDWI_2022_Monsoon.png');

% Save water mask

imwrite(water_mask, 'WaterMask_2022_Monsoon.png');

save('NDWI_2022_Monsoon.mat', 'ndwi');

%% NDWI CALCULATION FOR MONSOON SCENES (e.g., Monsoon 2024)

% Clear workspace and command window

clc;

clear;

%% Step 1: Set File Paths for Monsoon Scene

% Replace these with the full or relative path to your Landsat monsoon images

green_band_file = 'C:\\Users\\91998\\MATLAB Drive\\proooo\\2024\\LC08_L2SP_144053_20240918_20240923_02_T1_SR_B3.TIF'; % Band 3 (Green)

nir_band_file = 'C:\\Users\\91998\\MATLAB Drive\\proooo\\2024\\LC08_L2SP_144053_20240918_20240923_02_T1_SR_B5.TIF'; % Band 5 (NIR)

%% Step 2: Load Bands Using readgeoraster

\[green, R\] = readgeoraster(green_band_file); % Spatial reference info R

nir = readgeoraster(nir_band_file);

% Convert to double for calculation

green = double(green);

nir = double(nir);

%% Step 3: Compute NDWI

ndwi = (green - nir) ./ (green + nir + eps); % eps avoids division by zero

% figure;

% histogram(ndwi(:), 50);

% title('NDWI Histogram - Monsoon 2024');

% xlabel('NDWI Value');

% ylabel('Pixel Count');

ndwi_2024_monsoon = ndwi;

save('ndwi_2024_monsoon.mat', 'ndwi_2024_monsoon');

%% Step 4: Display NDWI Map

figure;

imagesc(ndwi, \[-1, 1\]); % Typical NDWI range

colormap('jet');

colorbar;

title('NDWI Map - Vembanad Lake (Monsoon 2024)');

xlabel('Pixels');

ylabel('Pixels');

%% Step 5: Generate Water Mask from NDWI

% Adjust threshold if needed (e.g., 0.2 → 0.05 → 0.0)

water_mask = ndwi > 0.05;

% Display water mask as binary image

figure;

imshow(water_mask);

title('Water Pixels Mask (NDWI > 0.05)');

%% Step 6: Estimate Wetland Area (in sq.km)

% Each pixel = 30m × 30m = 900 m² = 0.0009 km²

num_water_pixels = sum(water_mask(:));

wetland_area_km2 = num_water_pixels \* 0.0009;

fprintf(' Estimated Wetland Area (Monsoon 2024): %.2f sq.km\\n', wetland_area_km2);

wetland_2024_summer = wetland_area_km2;

%% Step 7: Save Outputs for Later Comparison

% Save NDWI image (normalized to 0-1)

ndwi_image = mat2gray(ndwi);

imwrite(ndwi_image, 'NDWI_2024_Monsoon.png');

% Save water mask

imwrite(water_mask, 'WaterMask_2024_Monsoon.png');

save('NDWI_2024_Monsoon.mat', 'ndwi');

**SUMMER CODE**

%% STEP 3: NDWI CALCULATION FOR ONE SCENE (e.g., Summer 2019)

% Clear previous data

clc;

clear;

%% Step 1: Set File Paths ( UPDATE YOUR FILE PATHS HERE)

% Replace these with the full path or relative path to your files

% Example: 'C:/Users/Keerthi/Documents/Vembanad/2016_Summer/LC08...B3.TIF'

green_band_file = 'C:\\Users\\91998\\MATLAB Drive\\pro\\2019\\LC08_L2SP_144053_20190313_20200829_02_T1_SR_B3.TIF'; % Band 3 (Green)

nir_band_file = 'C:\\Users\\91998\\MATLAB Drive\\pro\\2019\\LC08_L2SP_144053_20190313_20200829_02_T1_SR_B5.TIF'; % Band 5 (NIR)

%% Step 2: Load the Bands

\[green, R\] = readgeoraster(green_band_file); % Also gives spatial reference

nir = readgeoraster(nir_band_file);

% Convert to double for math operations

green = double(green);

nir = double(nir);

%% Step 3: NDWI Computation

ndwi = (green - nir) ./ (green + nir + eps); % eps prevents division by zero

% figure;

% histogram(ndwi(:), 50);

% title('NDWI Histogram - summer 2019');

% xlabel('NDWI Value');

% ylabel('Pixel Count');

ndwi_2019_summer = ndwi;

save('ndwi_2019_summer.mat', 'ndwi_2019_summer');

%% Step 4: Display NDWI Map

figure;

imagesc(ndwi, \[-1, 1\]); % NDWI typically ranges between -1 and 1

colormap('jet');

colorbar;

title('NDWI Map - Vembanad Lake (Summer 2019)');

xlabel('Pixels');

ylabel('Pixels');

%% Step 5: Water Mask Generation

% NDWI > 0.2 is commonly used as threshold for water bodies

water_mask = ndwi > 0.01;

% Show binary water map

figure;

imshow(water_mask);

title('Water Pixels Mask (NDWI > 0.01)');

%% Step 6: Estimate Wetland Area in sq.km

% Each Landsat pixel = 30m × 30m = 900 m² = 0.0009 km²

num_water_pixels = sum(water_mask(:));

wetland_area_km2 = num_water_pixels \* 0.0009;

fprintf(' Estimated Wetland Area (Summer 2019): %.2f sq.km\\n', wetland_area_km2);

wetland_2019_summer = wetland_area_km2;

%% Step 7: Save Outputs (Optional)

% Save NDWI map

ndwi_image = mat2gray(ndwi); % Normalize to \[0, 1\] for saving

imwrite(ndwi_image, 'NDWI_2019_Summer.png');

% Save water mask

imwrite(water_mask, 'WaterMask_2019_Summer.png');

save('NDWI_2019_Summer.mat', 'ndwi');

%% STEP 3: NDWI CALCULATION FOR ONE SCENE (e.g., Summer 2020)

% Clear previous data

%clc;

%clear;

%% Step 1: Set File Paths ( UPDATE YOUR FILE PATHS HERE)

% Replace these with the full path or relative path to your files

% Example: 'C:/Users/Keerthi/Documents/Vembanad/2020_Summer/LC08...B3.TIF'

green_band_file = 'C:\\Users\\91998\\MATLAB Drive\\pro\\2022\\LC09_L2SP_144053_20220209_20230428_02_T1_SR_B3.TIF'; % Band 3 (Green)

nir_band_file = 'C:\\Users\\91998\\MATLAB Drive\\pro\\2022\\LC09_L2SP_144053_20220209_20230428_02_T1_SR_B5.TIF'; % Band 5 (NIR)

%% Step 2: Load the Bands

\[green, R\] = readgeoraster(green_band_file); % Also gives spatial reference

nir = readgeoraster(nir_band_file);

% Convert to double for math operations

green = double(green);

nir = double(nir);

%% Step 3: NDWI Computation

ndwi = (green - nir) ./ (green + nir + eps); % eps prevents division by zero

% figure;

% histogram(ndwi(:), 50);

% title('NDWI Histogram - summer 2024');

% xlabel('NDWI Value');

% ylabel('Pixel Count');

ndwi_2020_summer = ndwi;

save('ndwi_2020_summer.mat', 'ndwi_2020_summer');

%% Step 4: Display NDWI Map

figure;

imagesc(ndwi, \[-1, 1\]); % NDWI typically ranges between -1 and 1

colormap('jet');

colorbar;

title('NDWI Map - Vembanad Lake (Summer 2020)');

xlabel('Pixels');

ylabel('Pixels');

%% Step 5: Water Mask Generation

% NDWI > 0.2 is commonly used as threshold for water bodies

water_mask = ndwi > 0.01;

% Show binary water map

figure;

imshow(water_mask);

title('Water Pixels Mask (NDWI > 0.01)');

%% Step 6: Estimate Wetland Area in sq.km

% Each Landsat pixel = 30m × 30m = 900 m² = 0.0009 km²

num_water_pixels = sum(water_mask(:));

wetland_area_km2 = num_water_pixels \* 0.0009;

fprintf(' Estimated Wetland Area (Summer 2020): %.2f sq.km\\n', wetland_area_km2);

wetland_2020_summer = wetland_area_km2;

%% Step 7: Save Outputs (Optional)

% Save NDWI map

ndwi_image = mat2gray(ndwi); % Normalize to \[0, 1\] for saving

imwrite(ndwi_image, 'NDWI_2020_Summer.png');

% Save water mask

imwrite(water_mask, 'WaterMask_2020_Summer.png');

save('NDWI_2020_Summer.mat', 'ndwi');

%% STEP 3: NDWI CALCULATION FOR ONE SCENE (e.g., Summer 2022)

% Clear previous data

%clc;

%clear;

%% Step 1: Set File Paths (🔽 UPDATE YOUR FILE PATHS HERE)

% Replace these with the full path or relative path to your files

% Example: 'C:/Users/Keerthi/Documents/Vembanad/2016_Summer/LC08...B3.TIF'

green_band_file = 'C:\\Users\\91998\\MATLAB Drive\\pro\\2022\\LC09_L2SP_144053_20220209_20230428_02_T1_SR_B3.TIF'; % Band 3 (Green)

nir_band_file = 'C:\\Users\\91998\\MATLAB Drive\\pro\\2022\\LC09_L2SP_144053_20220209_20230428_02_T1_SR_B5.TIF'; % Band 5 (NIR)

%% Step 2: Load the Bands

\[green, R\] = readgeoraster(green_band_file); % Also gives spatial reference

nir = readgeoraster(nir_band_file);

% Convert to double for math operations

green = double(green);

nir = double(nir);

%% Step 3: NDWI Computation

ndwi = (green - nir) ./ (green + nir + eps); % eps prevents division by zero

% figure;

% histogram(ndwi(:), 50);

% title('NDWI Histogram - summer 2022');

% xlabel('NDWI Value');

% ylabel('Pixel Count');

ndwi_2022_summer = ndwi;

save('ndwi_2022_summer.mat', 'ndwi_2022_summer');

%% Step 4: Display NDWI Map

figure;

imagesc(ndwi, \[-1, 1\]); % NDWI typically ranges between -1 and 1

colormap('jet');

colorbar;

title('NDWI Map - Vembanad Lake (Summer 2022)');

xlabel('Pixels');

ylabel('Pixels');

%% Step 5: Water Mask Generation

% NDWI > 0.2 is commonly used as threshold for water bodies

water_mask = ndwi > 0.01;

% Show binary water map

figure;

imshow(water_mask);

title('Water Pixels Mask (NDWI > 0.01)');

%% Step 6: Estimate Wetland Area in sq.km

% Each Landsat pixel = 30m × 30m = 900 m² = 0.0009 km²

num_water_pixels = sum(water_mask(:));

wetland_area_km2 = num_water_pixels \* 0.0009;

fprintf(' Estimated Wetland Area (Summer 2022): %.2f sq.km\\n', wetland_area_km2);

wetland_2022_summer = wetland_area_km2;

%% Step 7: Save Outputs (Optional)

% Save NDWI map

ndwi_image = mat2gray(ndwi); % Normalize to \[0, 1\] for saving

imwrite(ndwi_image, 'NDWI_2022_Summer.png');

% Save water mask

imwrite(water_mask, 'WaterMask_2022_Summer.png');

save('NDWI_2022_Summer.mat', 'ndwi');

%% 🌿 STEP 3: NDWI CALCULATION FOR ONE SCENE (e.g., Summer 2024)

% Clear previous data

%clc;

%clear;

%% Step 1: Set File Paths ( UPDATE YOUR FILE PATHS HERE)

% Replace these with the full path or relative path to your files

% Example: 'C:/Users/Keerthi/Documents/Vembanad/2016_Summer/LC08...B3.TIF'

green_band_file = 'C:\\Users\\91998\\MATLAB Drive\\pro\\2024\\LC08_L2SP_144053_20240326_20240409_02_T1_SR_B3.TIF'; % Band 3 (Green)

nir_band_file = 'C:\\Users\\91998\\MATLAB Drive\\pro\\2024\\LC08_L2SP_144053_20240326_20240409_02_T1_SR_B5.TIF'; % Band 5 (NIR)

%% Step 2: Load the Bands

\[green, R\] = readgeoraster(green_band_file); % Also gives spatial reference

nir = readgeoraster(nir_band_file);

% Convert to double for math operations

green = double(green);

nir = double(nir);

%% Step 3: NDWI Computation

ndwi = (green - nir) ./ (green + nir + eps); % eps prevents division by zero

% figure;

% histogram(ndwi(:), 50);

% title('NDWI Histogram - summer 2024');

% xlabel('NDWI Value');

% ylabel('Pixel Count');

ndwi_2024_summer = ndwi;

save('ndwi_2024_summer.mat', 'ndwi_2024_summer');

%% Step 4: Display NDWI Map

figure;

imagesc(ndwi, \[-1, 1\]); % NDWI typically ranges between -1 and 1

colormap('jet');

colorbar;

title('NDWI Map - Vembanad Lake (Summer 2024)');

xlabel('Pixels');

ylabel('Pixels');

%% Step 5: Water Mask Generation

% NDWI > 0.2 is commonly used as threshold for water bodies

water_mask = ndwi > 0.01;

% Show binary water map

figure;

imshow(water_mask);

title('Water Pixels Mask (NDWI > 0.01)');

%% Step 6: Estimate Wetland Area in sq.km

% Each Landsat pixel = 30m × 30m = 900 m² = 0.0009 km²

num_water_pixels = sum(water_mask(:));

wetland_area_km2 = num_water_pixels \* 0.0009;

fprintf(' Estimated Wetland Area (Summer 2024): %.2f sq.km\\n', wetland_area_km2);

wetland_2024_summer = wetland_area_km2;

%% Step 7: Save Outputs (Optional)

% Save NDWI map

ndwi_image = mat2gray(ndwi); % Normalize to \[0, 1\] for saving

imwrite(ndwi_image, 'NDWI_2024_Summer.png');

% Save water mask

imwrite(water_mask, 'WaterMask_2024_Summer.png');

save('NDWI_2024_Summer.mat', 'ndwi');
   
# Demo

https://github.com/user-attachments/assets/5bfed483-5430-4eb2-86cf-af20d92e2c3a

# Reference

🛠️ Tools & Technologies
MATLAB (for image processing & visualization)
Landsat-8 Surface Reflectance data (USGS Earth Explorer)
NDWI (McFeeters, 1996) for water detection

🌐 Data Source
Satellite imagery was obtained from USGS Earth Explorer:
🔗 https://earthexplorer.usgs.gov
(Raw data is not included in this repository due to size and licensing restrictions.)

📖 References
1. McFeeters, S. K. (1996). The use of the Normalized Difference Water Index (NDWI) in the delineation of open water features. International Journal of Remote Sensing, 17(7), 1425–1432.
2. USGS Landsat-8 Data User Handbook.
Add reference papers, data, or supporting material that has been used, if any.
