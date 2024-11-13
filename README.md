# Project3-stl

## An overview of the project and its purpose
Our project analyzed a government dataset of Heart Disease Mortality Data Among US Adults (35+) from 2019-2021 and explored trends of heart disease mortality rates across race, ethnicity, location, and gender.

All of our final code can be found in the **Final Code** folder.

Our data came in a csv file that we cleaned loading it into **DB Browser** and saving it as a database file. We read the database using ```sqlalchemy``` and ```create_engine``` and created a dataframe for to create a map using Folium and our GeoJSON of US counties. If you would like to run the code in **database_and_folium.ipynb** make sure you run ```pip install folium``` first.

## Instructions on how to use and interact with the project
We made several graphs and maps for this project. [Follow this link](https://mftobin.github.io/Project3-stl/) to see the following files:
* County Female Map
* County Male Map
* County Overall Map
* Gender Heart Disease Rates
* Heart Disease Rates by Ethnicity

To view heart disease mortality rates by state, please see the **plotly_chloropleth_dash_app.ipynb** file in the Final Code folder. The interactive map is found at the end of the notebook, however, make sure you run ``` pip install dash ``` in your Terminal prior to running the notebook.

## Ethical Considerations
When visualizing and analyzing public health data such as heart disease rates, it is essential to consider a number of ethical considerations. These considerations ensure that the analysis is conducted in a responsible, respectful, and meaningful way.

### Context of Data: 
When comparing heart disease rates across states, it’s important to provide context about the data sources. For instance, do the heart disease rates reflect access to healthcare, socioeconomic factors, or public health policies? Without this context, the bar chart could mislead people into attributing differences solely to state policies or practices, without considering broader social determinants.

### Potential for Stigmatization: 
Some states may appear to have higher heart disease rates due to systemic issues, like poverty or healthcare access. It is important not to stigmatize particular regions or populations. Data should be presented in a way that focuses on solutions and improvements, rather than blaming particular regions.

### Data Privacy and Anonymity: 
If the data includes information that could identify individuals (e.g., specific counties or small populations), ensure that the data is anonymized to protect people's privacy. 

### Conclusion: 
When visualizing heart disease rates across different dimensions, it's important to handle the data ethically by providing context, avoiding stigmatization, being sensitive to cultural and social implications, and ensuring that the visualization promotes positive social change. Clear explanations of the data, its limitations, and its broader implications will help ensure that the visualization is ethical, responsible, and effective.

## References for the data source(s)

Our dataset that we used for this project is called ["Heart Disease Mortality Data Among US Adults (35+) by State/Territory and County 2019-2021"](https://catalog.data.gov/dataset/heart-disease-mortality-data-among-us-adults-35-by-state-territory-and-county-2019-2021).

## References for any code used that is not your own

To complete the folium map of counties, we used a geojson from this [source](https://gist.github.com/sdwfrost/d1c73f91dd9d175998ed166eb216994a?short_path=bd97547).

We also reference [this article on folium](https://www.earthdatascience.org/tutorials/introduction-to-leaflet-animated-maps/) and had Xpert Learning assist help with refining our code and identifying syntax errors. To run the maps in the **database_and_folium.ipynb** took about 8 minutes per map, so finding the correct code before running all of the notebook code was important.

We used this [website](https://waldyrious.net/viridis-palette-generator/) for identifying a color scale for our maps. It was very helpful because you could choose a scheme and then indicate how many colors you needed.