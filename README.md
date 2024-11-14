# Project3-stl

## An overview of the project and its purpose
Our project analyzed a government dataset of Heart Disease Mortality Data Among US Adults (35+) from 2019-2021 and explored trends of heart disease mortality rates across race, ethnicity, location, and gender.

All of our final code can be found in the **Final Code** folder.

This project was a group collaboration with the following individuals: Chad Coggins, Evan Robinson, Maura Tobin, Jordan Johnson-Williams, and Yolanda Williams

### Heart Disease Rates by Ethnicity Stacked Chart
The purpose of this part project is to:
* Aggregate heart disease rates by state and ethnicity.
* Create an interactive stacked bar chart that visually represents the data for better insights and interpretation.
* Data Filtering: Heart disease rates are then averaged by State and Race/Ethnicity, providing a simplified view of the data that highlights the average rates for each ethnic group per state.
* Chart Description:
    * The x-axis represents the State.
    * The y-axis represents the Heart Disease Rate (Per 100,000 Population).
    * Colors are used to differentiate between ethnic groups, making it easy to compare heart disease rates across racial/ethnic lines within each state.
    * The chart title is “Heart Disease Rates by Ethnicity Across States.”
    * The chart layout is customized with rotated x-axis labels and a visible legend to help interpret the colors associated with each ethnic group
* How to run the code: 
    1. Execute the code in a Python environment.
    2. The interactive chart will display within the environment and also save as an HTML file named heart_disease_rates_by_ethnicity.html.
    3. heart_disease_rates_by_ethnicity.html – An HTML file containing the interactive chart that can be opened in any web browser for exploration.

### Gender Heart Disease Rates Bar Chart
The purpose of this part project is to:
* Filter the data to include only records for “Male” and “Female” genders.
* Create an interactive grouped bar chart to visually compare heart disease rates for men and women across various states.
* Data Filtering: The data is filtered to include only records with gender specified as either “Male” or “Female.”
Visualization
* Chart Description:
    * The x-axis represents the State.
    * The y-axis represents the Heart Disease Rate (Per 100,000 Population).
    * Bars are colored by gender to distinguish between men and women.
    * Bars are grouped by gender for each state to facilitate a clear comparison.
    * The chart title is “Heart Disease Rates for Men and Women Across U.S. States.
    * The layout includes rotated x-axis labels for readability and a legend to differentiate the gender categories.
* How to run the code:
    1. Ensure Plotly is installed (pip install plotly).
    2. Run the code in a Python environment.
    3. The interactive chart will display in the environment and be saved as an HTML file Make sure you have Plotly installed (pip install plotly).
    4. gender_heart_disease_rates.html – An HTML file containing the interactive chart, which can be opened in a web browser for further exploration.

### Intro Pie Ethnicity Chart
I wanted to create a pie chart to see the percentage of the US Heart Mortality by Ethinicity.
I filtered the dataframe down to not include gender, and only include the overall rates for the different ethnicities.
This is my code for the pie chart:
```
data = Overall_df["Data Value (Per 100,000 Population)"]
labels = Overall_df["Race/Ethnicity"]
explode = [0.07,0,0,0,0,0,0]
colors = ["#3A8F9D", "#00B2B2", "#00B2B5", "#00C2C9", "#3BC6D9", "#6FD0E1", "#A0D8E6"]
plt.figure(figsize=(6,8))
plt.title("United States Heart Disease by Ethnicity", fontsize=18, fontweight="bold")
plt.pie(data, explode=explode, labels=labels, colors=colors, autopct= '%1.1f%%', textprops={'fontsize': 16}, pctdistance=0.75, labeldistance=1.1, startangle=120)
plt.axis('equal')
plt.show()
```
## States Choropleth with Plotly Dash
I then did some research on plotly express and plotly graph objects to create a Choropleth map of
the US States and the Overall Mortality Rates.
[https://plotly.com/python/plotly-express/](https://plotly.com/python/plotly-express/)

There is a section called Dash at the bottom of that page and I wanted to graph Male, Female, and Overall Rate on the map using Dash.
[https://dash.plotly.com/layout](https://dash.plotly.com/layout)

I watched mulitple video tutorials as well to help me create my Dash app Choropleth Map.
A tricky part was I had to create a new Dataframe where the Female, Male and Overall Rates where in seperate columns.
Below is the code that I used to complete this successfully.
```
state_df_pivoted = state_df.pivot(index='State', columns='Gender', values='Data Value (Per 100,000 Population)').reset_index()
state_df_pivoted.rename(columns={'Overall': 'Overall Rate', 'Male': 'Male Rate', 'Female': 'Female Rate'}, inplace=True)
```
Then I just had to setup my Dash layout, and then create the callback with the function to create the Dash app.
```
app.layout = html.Div([
    html.Div([
        html.Div('Select Gender:', style={'fontSize': 25, 'color': 'white'}),
        dcc.RadioItems(
            id='gender-selector',
            options=[
                {'label': 'Male', 'value': 'Male Rate'},
                {'label': 'Female', 'value': 'Female Rate'},
                {'label': 'Overall', 'value': 'Overall Rate'}
            ],
            value='Overall Rate',  # Default value
            labelStyle={'display': 'inline-block', 'margin': '10px', 'color': 'white'}  # Style for radio items
        )
    ], style={'textAlign': 'left', 'marginBottom': '10px'}),
    dcc.Graph(id='choropleth-map', style={'width': '100%', 'height': '400px'})  # Set the graph to full width
])
```
The RadioItems component allows you to click on one of the options for the Rate, and then the graph changes based on that option.

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

See **States Choropleth with Plotly Dash** section above for links used to complete that part of the project.

When attempting  the bar chart row facets this [link](https://plotly.com/python/plotly-express/) helped me with completing the code to create the visual. 

This [link](https://www.pygal.org/en/stable/documentation/types/index.html) helped me create a stacked bar chart to demonstrate how different ethnicities are affected by heart disease across the US. 

To complete the folium map of counties, we used a geojson from this [source](https://gist.github.com/sdwfrost/d1c73f91dd9d175998ed166eb216994a?short_path=bd97547).

We also reference [this article on folium](https://www.earthdatascience.org/tutorials/introduction-to-leaflet-animated-maps/) and had Xpert Learning assist help with refining our code and identifying syntax errors. To run the maps in the **database_and_folium.ipynb** took about 8 minutes per map, so finding the correct code before running all of the notebook code was important.

We used this [website](https://waldyrious.net/viridis-palette-generator/) for identifying a color scale for our maps. It was very helpful because you could choose a scheme and then indicate how many colors you needed.