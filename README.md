# 🥇 Analyzing the Paris 2024 Olympic Dataset with Python and Power BI

The **Paris 2024 Summer Olympics** promises to be a grand event, and analyzing the related datasets can provide valuable insights into various aspects of the games. This guide demonstrates how to use **Python** to download and manage the dataset from **Kaggle**, and how to use **Power BI** for visualization and analysis.

## 📌 Project Steps Overview

This project involves several key steps, from downloading data to preparing it for visualization. Here’s a breakdown of the entire process:

1. [Setting Up Kaggle API and Python Environment](#step-1-setting-up-kaggle-api-and-python-environment)
2. [Python Script for Downloading the Dataset](#step-2-python-script-for-downloading-the-dataset)
3. [Importing Data into Power BI](#step-3-importing-data-into-power-bi)
4. [Creating Visualizations in Power BI](#step-4-creating-visualizations-in-power-bi)

---

## 🛠️ Step 1: Setting Up Kaggle API and Python Environment

To access and download datasets from **Kaggle**, you’ll need to set up the Kaggle API.

1. **Sign up on Kaggle**: If you don’t have a Kaggle account, sign up [here](https://www.kaggle.com/).
2. **Create an API Token**: In your Kaggle account settings, go to the **API** section and click **Create New API Token**. This will download a `kaggle.json` file containing your credentials.
3. **Save the API Token**: Place the `kaggle.json` file in a secure directory on your machine, where it will be used to authenticate the Kaggle API.

### 🔧 Python Environment Setup

Ensure that Python and the necessary libraries are installed:

```bash
pip install kaggle pandas
```

---

## 📥 Step 2: Python Script for Downloading the Dataset

The following script automates the download of the **Paris 2024 Olympic** dataset from Kaggle and loads it into **Pandas DataFrames** for analysis.

```python
import kaggle
import os
import pandas as pd

# Set Kaggle API credentials directory
os.environ['KAGGLE_CONFIG_DIR'] = 'C:/Users/yourusername/.kaggle'  # Update to your Kaggle config directory

# Specify the dataset identifier
dataset = 'piterfm/paris-2024-olympic-summer-games'

# Set the download path
download_path = 'C:/Users/yourusername/Downloads/OlympicDataset'  # Update to your preferred download directory

# Remove existing files in the folder to prevent duplicates or outdated files
for file in os.listdir(download_path):
    file_path = os.path.join(download_path, file)
    try:
        if os.path.isfile(file_path):
            os.unlink(file_path)
            print(f"Deleted {file_path}")
    except Exception as e:
        print(f"Error deleting {file_path}: {e}")

# Download the dataset using the Kaggle API and unzip the files
kaggle.api.dataset_download_files(dataset, path=download_path, unzip=True)

# List of CSV files to be imported
csv_files = [
    'athletes.csv', 'events.csv', 'medallists.csv', 'medals.csv', 'medals_total.csv',
    'schedules.csv', 'schedules_preliminary.csv', 'teams.csv', 'torch_route.csv', 'venues.csv'
]

# Initialize a dictionary to hold DataFrames
dataframes = {}

# Iterate through each CSV file and load it into a DataFrame
for file in csv_files:
    file_path = os.path.join(download_path, file)
    df = pd.read_csv(file_path)
    table_name = file.split('.')[0]  # Remove the .csv extension
    dataframes[table_name] = df
```

### 💡 Explanation of the Code

- **Environment Setup**: Sets the `KAGGLE_CONFIG_DIR` to authenticate with Kaggle.
- **Dataset Identifier**: Specifies the dataset identifier for download.
- **Clearing Existing Files**: Deletes existing files in the download directory to avoid duplicates.
- **Downloading and Loading**: Downloads and unzips the dataset, loading each CSV into a Pandas DataFrame for easy access.

---

## 📊 Step 3: Importing Data into Power BI

With the dataset downloaded, you can now import it into **Power BI** for visualization.

### 📝 Connecting Power BI to Python

1. **Open Power BI Desktop**.
2. **Get Data**: Click on “Get Data” in the Home tab and choose **Python script** as the data source.
3. **Load the Script**: Copy and paste the following Python script to load the DataFrames into Power BI:

```python
import pandas as pd
import os

# Define the path to the downloaded CSV files
download_path = 'C:/Users/yourusername/Downloads/OlympicDataset'

# Load the data into DataFrames
athletes = pd.read_csv(os.path.join(download_path, 'athletes.csv'))
events = pd.read_csv(os.path.join(download_path, 'events.csv'))
medallists = pd.read_csv(os.path.join(download_path, 'medallists.csv'))
medals = pd.read_csv(os.path.join(download_path, 'medals.csv'))
medals_total = pd.read_csv(os.path.join(download_path, 'medals_total.csv'))
schedules = pd.read_csv(os.path.join(download_path, 'schedules.csv'))
schedules_preliminary = pd.read_csv(os.path.join(download_path, 'schedules_preliminary.csv'))
teams = pd.read_csv(os.path.join(download_path, 'teams.csv'))
torch_route = pd.read_csv(os.path.join(download_path, 'torch_route.csv'))
venues = pd.read_csv(os.path.join(download_path, 'venues.csv'))
```

---

## 📈 Step 4: Creating Visualizations in Power BI

Now that the data is in Power BI, you can create visualizations to analyze the Olympic dataset. Here are a few examples:

1. **Athlete Participation by Country**  
   - **Type**: Bar Chart  
   - **Description**: Use the `athletes` table to plot the number of athletes from each country.

2. **Medal Count by Country**  
   - **Type**: Pie Chart  
   - **Description**: Use the `medals_total` table to display the total medals for each country.

3. **Event Schedule**  
   - **Type**: Table  
   - **Description**: Display event names, dates, and venues from the `schedules` table.

4. **Torch Route Map**  
   - **Type**: Map  
   - **Description**: Visualize the Olympic torch route using the `torch_route` table.

5. **Medal Trends Over Time**  
   - **Type**: Line Chart  
   - **Description**: Use the `medals` table to show trends in medals over time, by country or sport.

---

## 🏆 Conclusion

By leveraging Python and Power BI, we’ve successfully downloaded, organized, and visualized the **Paris 2024 Olympic dataset**. This project highlights the power of data analysis and visualization in understanding the dynamics of a global event.

---

## 🌟 Further Exploration

- **Advanced Analytics**: Apply machine learning models to predict medal outcomes or identify key performance indicators.
- **Dynamic Dashboards**: Enhance Power BI reports with dynamic, interactive dashboards.
