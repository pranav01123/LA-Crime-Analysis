# 🗺️ Los Angeles Crime Hotspot Analysis (2020-2023)

![Python](https://img.shields.io/badge/Python-3.x-blue.svg) ![Libraries](https://img.shields.io/badge/Libraries-Pandas%20%7C%20Scikit--learn%20%7C%20Folium-orange) ![Kaggle](https://img.shields.io/badge/Data-Kaggle-brightgreen.svg)

An in-depth geospatial analysis of crime data from the City of Los Angeles (2020-2023) to identify, rank, and visualize crime hotspots. This project moves beyond simple crime counts by implementing a custom **crime severity score** and using **KMeans clustering** to define and rank hotspots based on their weighted crime density.

---

### ✨ Key Features

* **Crime Severity Scoring**: A custom system to categorize and score crimes based on their nature (e.g., `Violent Crimes`, `Assault`, `Theft`).
* **KMeans Clustering**: Unsupervised machine learning is used to identify dense, geographically-defined crime clusters. The optimal number of clusters is determined using the "Elbow Method."
* **Geospatial Analysis**: Leverages `scipy.spatial.ConvexHull` and `geopandas` to calculate the precise geographical area and crime density of each hotspot.
* **Density-Based Ranking**: Hotspots are ranked by their **weighted crime density** (`Total Score per km²`), not just raw crime counts, to identify areas of high-impact criminal activity.
* **Interactive Visualization**: A beautiful, interactive map built with `folium` that displays hotspots as colored, concentric rings with detailed, styled popups.
* **Timeline Analysis**: An interactive timeline allows for dynamic filtering of crimes by category, time, date, month, and year.

---

### 🔬 Methodology

The project follows a multi-step analytical workflow to transform raw data into actionable insights.

**1. Data Processing & Feature Engineering**
The dataset is loaded using `pandas` and cleaned to handle missing `LAT` and `LON` values. To prioritize more serious crimes, a custom `Crime Severity` score is engineered by mapping over 100 unique crime descriptions into broader categories and assigning a weight to each category using a dictionary:

`severity_score_map = { 'Violent Crimes': 10, 'Assault': 8, 'Theft': 6, 'Property Crimes': 4, 'Other': 2 }`

This map is then applied to create the `Crime Severity` column in the dataframe.

**2. Hotspot Identification with KMeans**
The `KMeans` algorithm clusters crime incidents based on their geographical coordinates. The **Elbow Method** determined that **k=6** was the optimal number of clusters, with each cluster representing a distinct crime hotspot.

**3. Geospatial Density Calculation**
Once hotspots are identified, their geographical properties are analyzed:
* **Boundary Creation**: A **Convex Hull** is generated for each cluster to create the smallest possible polygon enclosing all crime incidents within it.
* **Area & Density**: The area of each polygon is calculated in km² using `geopandas`. The final density for each hotspot is then calculated as: `Density = Total Severity Score / Area (in km²)`

**4. Ranking and Visualization**
Hotspots are ranked by their calculated density and assigned a qualitative "Crime Level" (e.g., "Extreme", "Very High"). These are then plotted on an interactive `folium` map where each hotspot is represented by colored rings corresponding to its crime level.

---

### 📊 Analysis and Insights

* **Hotspot 1 (Extreme)**: The analysis identifies the **downtown area** as the highest-density hotspot, which is consistent with its high population, commercial activity, and nightlife.
* **Temporal Patterns**: The interactive timeline reveals clear peaks in crime during the **afternoon and evening hours**.
* **Seasonal Trends**: Filtering by month allows for the observation of seasonal trends, such as a potential increase in property crimes during the holiday season.

---

### 🖼️ Visualizations

Below is a preview of the final interactive map, showing the concentric ring hotspots across Los Angeles.

<img width="1068" height="637" alt="Screenshot 2025-08-01 002531" src="https://github.com/user-attachments/assets/af27ae70-9317-4af5-b92d-77a4015cd19f" />
<img width="1073" height="641" alt="Screenshot 2025-08-01 002552" src="https://github.com/user-attachments/assets/b93c0e92-5f35-4021-b327-b514c560a58b" />


*(Note: Interactive maps do not render in GitHub's file viewer. To see the live map, please see the "Live Demo" section below.)*

---

### 🚀 Live Demo

To view the fully interactive map, you can:
1.  Download the repository and open the `crime_hotspot_rings_map.html` file in your browser.
2.  (Recommended) Paste the URL of this repository's notebook into **[nbviewer](https://nbviewer.jupyter.org/)** for a fully rendered, interactive version.

---

### ⚙️ How to Run the Project

**1. Setup**
* Clone the repository:
    ```bash
    git clone [https://github.com/YourUsername/LA-Crime-Hotspot-Analysis.git](https://github.com/YourUsername/LA-Crime-Hotspot-Analysis.git)
    ```
* Install the required packages:
    ```bash
    pip install pandas scikit-learn geopandas folium scipy matplotlib seaborn
    ```
* Download the dataset from the link below and place the `.csv` file in the project's root directory.

**2. Execution**
* Run the Jupyter Notebook (`LA-Crime-Analysis.ipynb`) to execute the full analysis and generate the interactive map.

---

### 💾 Data Source

* **Dataset**: Los Angeles Crime Data 2020-2023
* **Source**: [Kaggle](https://www.kaggle.com/datasets/source-link-here)







