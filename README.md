# Assignment_DHINEU_Colab

# Assignment_DHINEU

For this project the notebook is created in Google colab and the libraries are also imported from google colab.

First of all to get the buffer and the spectral Indices, we need to connect google earth engine on the google colab.
1. To connect the google earth engine we need to create a google cloud project and give permission to the google earth engine api and register for a project.
2. Import the relevent libraries like,
import ee
import json
import geemap
import geopandas as gpd
import pandas as pd
import matplotlib.pyplot as plt
from shapely.geometry import Point
3. The authenticate the project using the ee.Authenticate() command.
4. Then using the ee.Initialize(project='carbide-sensor-434209-k7') acctivate the project and then carru out the processess.

5. Then Using this code create a point and a buffer from the point:
   # Latitude and longitude of the point
  lat, lon = 23.861443376832728, 91.34147139064376
  # Create a point geometry
  point = Point(lon, lat)
  # Create a GeoDataFrame in WGS 84 (EPSG:4326)
  gdf = gpd.GeoDataFrame([1], geometry=[point], crs="EPSG:4326")
  # Reproject the GeoDataFrame to a suitable UTM CRS (e.g., EPSG:32646 for UTM zone 46N)
  gdf = gdf.to_crs("EPSG:32646")
  # Define the buffer distance in meters (e.g., 5000 meters for ~5km)
  buffer_distance = 5000
  # Create the buffer in the projected CRS
  buffer = gdf.buffer(buffer_distance)
  # Reproject the buffer back to WGS 84 (EPSG:4326) for visualization in Folium
  buffer = buffer.to_crs("EPSG:4326")
  # Create a Folium map centered on the original point
  mymap = folium.Map(location=[lat, lon], zoom_start=12)
  # Convert the buffer to GeoJSON and add it to the map
  folium.GeoJson(buffer).add_to(mymap)
  # Optionally, add a marker at the original point
  folium.Marker([lat, lon], popup='Center Point').add_to(mymap)
  # Display the map directly in Google Colab
  mymap
6. The created buffer is converted to ee. geometry for getting the study area using is compatible with the google earth engine.
7. In the next step the Sentinel2 data is filtered out for a specific date range and the indices are calculated for NDVI and NDWI.
8. Sentinel2 data is downloaded and saved in the drive for using it in the CNN model.
9. Next the Line graph is created to show visualize the condition of the Indices in NDVI and NDWI.
10. Later cnn model is developed for LULC classification using the existing datasets from eurosat dataset from tensorflow.
11. The datasets are normalized and set for training.
12. Then the training command is passed to start training.
13. After the trainig is complete the downloaded sentinel2 image is used for prediction.
