📈 Los Angeles Crime Hotspot Analysis (2020-2023)
<p align="center">
<img src="https://img.shields.io/badge/Language-Python-blue.svg" alt="Language">
<img src="https://img.shields.io/badge/Library-Pandas-brightgreen.svg" alt="Pandas">
<img src="https://img.shields.io/badge/Library-Scikit--learn-orange.svg" alt="Scikit-learn">
<img src="https://img.shields.io/badge/Library-Folium-red.svg" alt="Folium">
<img src="https://img.shields.io/badge/Data-Kaggle-cyan.svg" alt="Data Source">
</p>

<p align="center">
  <strong><a href=https://pranav01123.github.io/LA-Crime-Analysis/>🚀 View the Live Interactive Map!</a></strong>
</p>

📍 Project Overview
This project performs an in-depth analysis of crime data from the City of Los Angeles (2020-2023) to identify and visualize crime hotspots. Moving beyond simple crime counts, this analysis introduces a crime severity score to weigh different types of crimes based on their seriousness.

Using the KMeans clustering algorithm, crime incidents are grouped into spatial hotspots. Each hotspot is then evaluated based on a custom-weighted crime score, its geographical area, and its crime density (Total Score per km²). The final output is a beautiful, interactive Folium map that visualizes these hotspots as colored, concentric rings, providing a rich and insightful view of crime patterns in Los Angeles.

✨ Key Features
Crime Severity Scoring: A system to categorize and score crimes based on their nature (e.g., Theft, Assault, Violent Crimes).

KMeans Clustering: Unsupervised machine learning to identify dense, geographically-defined crime clusters.

Geospatial Analysis: Use of scipy.spatial.ConvexHull and geopandas to calculate the geographical area and density of each hotspot.

Density-Based Ranking: Hotspots are ranked by their weighted crime density, not just crime count, to identify areas of high-impact crime.

Interactive Visualization: An interactive map built with folium that displays hotspots with detailed, styled popups.

Timeline Analysis: An interactive timeline that allows for filtering crimes by category, time, date, month, and year.

🛠 Table of Contents
Methodology

Analysis and Insights

Visualizations

How to Run the Project

Data Source

Live Demo

🔬 Methodology
The project follows a multi-step analytical workflow:

1. Data Loading and Preprocessing
The dataset is loaded using pandas and cleaned to handle missing values, particularly in the LAT and LON columns which are essential for geospatial analysis.

2. Feature Engineering: Crime Severity Scoring
To ensure the analysis prioritizes more serious crimes, a custom scoring system was developed. Over 100 unique crime descriptions were first mapped into broader categories, and then each category was assigned a Severity Score.

# Define the severity scores for each crime category
severity_score_map = {
    'Violent Crimes': 10,
    'Assault': 8,
    'Theft': 6,
    'Property Crimes': 4,
    'Other': 2
}

# Create the 'Crime Severity' column by mapping the categories
df_clean['Crime Severity'] = df_clean['Crime Category'].map(severity_score_map)

3. Hotspot Identification with KMeans Clustering
The KMeans algorithm was used to identify hotspots based on the geographical coordinates of crimes. The "Elbow Method" was used to determine the optimal number of clusters, which was found to be k=6. Each cluster represents a distinct geographical crime hotspot.

4. Geospatial Analysis: Area and Density Calculation
Once hotspots were identified, their geographical properties were analyzed:

Boundary Creation: A Convex Hull was generated for each cluster to create the smallest possible polygon enclosing all crime incidents.

Area Calculation: The area of each hull polygon was calculated in square kilometers using geopandas.

Density Calculation: The final density for each hotspot was calculated as:

Density = Total Severity Score / Area (in km²)
This metric provides a much more insightful view than crime count alone.

5. Ranking and Visualization
The hotspots were ranked based on their calculated density to determine a final "Crime Level."

Ranking & Labeling: Clusters were sorted by Density and assigned a qualitative label: "Extreme", "Very High", "High", etc.

Interactive Mapping: The final results were plotted on an interactive folium map:

Each hotspot is represented by a series of concentric, transparent rings centered on its geographical centroid.

The color of the rings corresponds to the hotspot's Crime Level.

Clicking on any ring reveals a detailed, styled HTML popup displaying its rank, crime level, total crime count, total severity score, and density.

📊 Analysis and Insights
The analysis reveals several key insights into the crime patterns of Los Angeles:

Hotspot 1 (Extreme): This hotspot, located in the downtown area, has the highest crime density. This is likely due to the high population density, commercial activity, and nightlife in the area.

Timeline Analysis: The interactive timeline shows that crime rates are not uniform throughout the day. There are clear peaks in the afternoon and evening hours, which can be further analyzed by crime category.

Seasonal Trends: By filtering by month, it's possible to observe seasonal trends in crime. For example, property crimes may increase during the holiday season.

🖼 Visualizations
Below is a preview of the final interactive map, showing the concentric ring hotspots across Los Angeles.

(Note: Interactive maps do not render in GitHub's file viewer. To see the live map, please see the "Live Demo" section below.)

<img width="1074" height="641" alt="image" src="https://github.com/user-attachments/assets/8617b926-ef28-4fdc-9601-6df47a726ea0" />

<img width="1073" height="641" alt="image" src="https://github.com/user-attachments/assets/e49f58d3-61ff-4799-a5b3-04380beedc2e" />


🚀 How to Run the Project
Prerequisites
The project requires Python 3 and the following libraries:

pandas

scikit-learn

geopandas

folium

scipy

matplotlib

seaborn

Setup
Clone the repository:

git clone https://github.com/YourUsername/LA-Crime-Hotspot-Analysis.git

Install the required packages:

pip install pandas scikit-learn geopandas folium scipy matplotlib seaborn

Data: Download the dataset from the link below and place the .csv file in the project's root directory.

Run the Jupyter Notebook (LA-Crime-Analysis.ipynb) to execute the analysis and generate the map.

💾 Data Source
Dataset: Los Angeles Crime Data 2020-2023

Source: Kaggle

🌐 Live Demo
To view the fully interactive map, you can:

Download the repository and open the crime_hotspot_rings_map.html file in your browser.

(Recommended) Paste the URL of this repository's notebook into nbviewer for a fully rendered, interactive version.
