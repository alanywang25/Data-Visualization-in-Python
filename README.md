# Visualization in Python for Duke Data Scientists

**Authors:** [Alan Wang](https://www.linkedin.com/in/alan-wang-4100681bb/), [Juan Cruz Assad](https://www.linkedin.com/in/juan-cruz-assad)

**Note**: The contents of this repository were imported from the [original Gitlab repository](https://gitlab.oit.duke.edu/ayw14/code-plus-team-will-dcc).

## Project Introduction
This project was part of the [Duke University Code+ 2022 Program](https://codeplus.duke.edu/projects/visualization-python-duke-data-scientists). The primary goal of this project was to develop interactive visualization tools and workflows to help Duke researchers analyze and visualize their large datasets. The visualizations developed and documented for this project were created using Holoviews and Datashader in JupyterLab notebooks that were hosted in OnDemand sessions on the [Duke Compute Cluster](https://dcc.duke.edu/OpenOnDemand/). 

<p float="left">
  <img src="/images/03_affluence_map_img.gif" width = "400" height = "200"/>
  <img src="/images/05_gpu_posts_map_img.gif" width = "440" height = "200"/> 
</p>

These were some of the visualizations created through this project. To see more of these visualizations, see the `Visualizations` section of the README.

## Our Researcher
The researcher that we worked with is [Dr. William Meyerson](https://psychiatry.duke.edu/william-meyerson-md), a Yale School of Medicine graduate who is currently studying to become a physician-scientist at Duke Medical Center. Dr. Meyerson is interested in analyzing the effects of social media on mental health, specifically if late Reddit posting times have an influence on the development of sleep disorders. 

## About the Data
Dr. Meyerson provided multiple datasets to be visualized and analyzed for this project. 

The first and largest dataset contains information about over 200 million Reddit posts, divided up into 63 `.tsv` files. This dataset was pulled from the PushShift Reddit Dataset [^1].

The second dataset, provided in a `.csv` file format, contained demographic information about around 10,000 subreddits grouped into 30 subreddit clusters, including affluence, age, partisanship, sociality, and gender. This dataset was pulled from _Quantifying social organization and political polarization in online platforms_ [^2].

The third dataset, provided in a `.tsv` file format, contained geographical information in terms of longitude and latitude about where approximately 75,000 Reddit users revealed their location to be. The fourth dataset, also provided in a `.tsv` file format, also provided geographical information about where approximately 75,000 Reddit users revealed their location to be, but in terms of names of states/cities/countries. These two datasets were both pulled from "Geocoding Without Geotags: A Text-based Approach for reddit", excerpted from _Proceedings of the 2018 EMNLP Workshop W-NUT: The 4th Workshop on Noisy User-Generated Text_ [^3].

## Tools
We used a variety of Python libraries and packages to clean, process, manipulate and visualization datasets with thousands to millions of observations.

### Data Manipulation and Processing: `Pandas`, `GeoPandas`, `NumPy`

[**Pandas**](https://pandas.pydata.org): an open-source Python library that provides an easy and intuitive way to read, process, and write data. We use `Pandas` to read in our data from `.csv`, `.txt` or `.parquet` files as a dataframe, then manipulate this dataframe through a variety of easy-to-use tools provided by the library.

[**GeoPandas**](https://geopandas.org/en/stable/): an open-source Python library specifically focused on working with geospatial data. It provides much of the same functionality for manipulating and processing data as the `Pandas` libraries, but allows users to work with geospatial data (like points and geometries). We use `GeoPandas` to manipulate our spatial data in order to create visualizations.

[**NumPy**](https://numpy.org/): an open-source Python library used for scientific computing. It allows for fast and easy manipulation of data through the use of arrays. We use `NumPy` to process and manipulate a lot of our data before we visualize it through `GeoPandas` or the `Cuxfilter` libraries.

### Visualizations: `HoloViews` and `GeoViews`

[**HoloViews**](https://holoviews.org/): an open-source Python library specializing in data analysis and visualization. It incorporates visualization tools like `bokeh` and `matplotlib` to allow users to work seamlessly with the data and its visualization. We use it in order to process and visualize our large amounts of data, as it provides an immediate, automatic visualization rendered by a variety of supported plotting libraries, including `Bokeh` or `Matplotlib`.

[**GeoViews**](https://geoviews.org/): an open-source Python library built on the `HoloViews` library allowing users to easily visualize multidimensional and geographical data. We use it to plot and visualize geographical data.

### Visualizations using Graphical-Processing Units (GPUs): `Cuxfilter`

[**Cuxfilter**](https://docs.rapids.ai/api/cuxfilter/stable/): an open-source Python library, part of the `RAPIDS` suite of open-source software libraries built to work with data science on GPUs. This specific library seamlessly connects different visualization libraries such as `bokeh` and `datashader` to a GPU dataframe. We use this library to plot amounts of data orders of magnitudes larger than that we plot on `HoloViews` and `GeoViews`, all within seconds.

## Data Manipulation and Processing Workflow Overview
This is an overview of our workflow for manipulating our data. Because of data privacy reasons, we created synthetic data to run our data manipulation demos, which can found be in the `synthetic_data` folder. To see how we created the synthetic data, click [here](synthetic_data/README.md). The code and documentation for our data manipulation demos can be found in the `data_wrangling` folder. To see more detailed descriptions of our workflow, click [here](data_wrangling/README.md).

<p align="center">
<img src="/images/data_wrangling_workflow.jpeg" width = "750" height = "900">
</p>

## Visualizations
These were the final visualizations created after running the aforementioned data manipulations, listed in the order in which they were developed. These visualizations shown below in the animated GIFs were made with our full processed datasets. The code and documentation for each visualization using synthetic data can be found in the `visualizations` folder of the Gitlab repository, listed in the same order as they are below. To see more detailed descriptions of each visualization, click [here](visualizations/README.md). 

### Sociality vs. Age of Subreddits
This is an interactive scatterplot displaying the relationship between sociality and age for each of the subreddits in our data, grouped by subreddit cluster.

<p align="center">
<img src="/images/01_dem_scatter_img.gif" width = "810" height = "300">
</p>

### Worldwide Location Reveals of Reddit Users by Day of the Week
This interactive visualization displays when and where Reddit users revealed themselves to be by the day of the week and hour of day.

<p align="center">
<img src="/images/02_loc_reveal_map_img.gif" width = "890" height = "400">
</p>

### Affluence of Reddit Users Around the World
This is an interactive geographical visualization of the affluence of Reddit users around the world, grouped by subreddit cluster name.

<p align="center">
<img src="/images/03_affluence_map_img.gif" width = "720" height = "380">
</p>

### Relative Frequencies of Posts by Hour of Day
This is an interactive stacked bar chart that displays the relative frequencies of Reddit posts by hour of day for each of the subreddit clusters adjusted by timezone. 

<p align="center">
<img src="/images/04_post_freq_chart_img.gif" width = "810" height = "400">
</p>

### Worldwide Reddit Post Activity
This interactive GPU visualization displays where and when all 200+ million Reddit posts were made, grouped by day of the week and hour of day, kept in universal timezone.

<p align="center">
<img src="/images/05_gpu_posts_map_img.gif" width = "930" height = "400">
</p>

### Affluence and Frequency of Posting of Reddit Users by US State 
These interactive choropleth map visualizations display the affluence and frequency of posting of Reddit users in the US by US state.

<p float="left">
  <img src="/images/06_choropleth_map_1_img.gif" width = "440" height = "160"/>
  <img src="/images/06_choropleth_map_2_img.gif" width = "440" height = "160"/> 
</p>

## User Instructions
### Step 1: Set up environment for project in the Duke Compute Cluster
Create a JupyterLab Singularity instance in an OnDemand session with or without GPUs and the amount of time, CPU cores (max is 40 cores), and RAM (max is 208 GB), depending on which visualizations you want to run. Only visualizations that require GPUs (such as our Worldwide Reddit Post Activity visualization) will need gpu-scavenger or gpu-common as the partition. Make sure to ask for GPUs (max of 2) if you want to run a GPU visualization.

### Step 2: Clone Gitlab repository
Copy the following command into your terminal once you are inside the directory you want this project folder to be in:

```
git clone git@gitlab.oit.duke.edu:ayw14/code-plus-team-will-shared.git
```

### Step 3: Open JupyterLab Notebooks + Run Code
Once the repository has been cloned, you can open the JupyterLab notebooks and begin running the code. For any visualizations that need GPUs to run, make sure under the Kernel tab that the `rapids` kernel is selected, otherwise, select the `Python 3` kernel. 

If you encounter any issues with a Python library not being available, you can go to your terminal and run the command `pip install “name of library”` and that should install the library. In addition, if you experience any issues with a Python library not being up-to-date and compatible, you can go to your terminal and run the command `pip3 install --upgrade requests` in your terminal, which will make sure all of your packages are updated.

To see what packages you would need to install to run our visualizations, click [here](https://gitlab.oit.duke.edu/OIT-DCC/codeplus).

## References
[^1]: Baumgartner, J., Zannettou, S., Keegan, B., Squire, M., &amp; Blackburn, J. (n.d.). _The Pushshift Reddit Dataset_. Proceedings of the International AAAI Conference on Web and Social Media. Retrieved July 22, 2022, from https://ojs.aaai.org/index.php/ICWSM/article/view/7347.

[^2]: Waller, I., & Anderson, A. (2021, December 1). _Quantifying social organization and political polarization in online platforms_. Nature News. Retrieved July 22, 2022, from https://www.nature.com/articles/s41586-021-04167-x.

[^3]: Harrigian, K. (2018). Geocoding without geotags: A text-based approach for Reddit. _Proceedings of the 2018 EMNLP Workshop W-NUT: The 4th Workshop on Noisy User-Generated Text_, 17–27. https://doi.org/10.18653/v1/w18-6103.
