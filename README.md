Energy Use Info
-----------------------
## Introduction
* This roject gives insight on my house's energy use. It cleans dirty data and, creates intuitive graphs & conclusions from my house's weather & energy usage data.
### Data
* Energy Data was downloaded from [Comed's Green Button Download webpage](https://secure.comed.com/MyAccount/MyBillUsage/pages/secure/GreenButtonConnectDownloadMyData.aspx).
* Weather data was collected using [Meteostat](https://github.com/meteostat/meteostat-python).

Installation
----------------------
#### Clone this repo to your computer.
#### Download your ComEd Usage data
* create a folder titled "data"
* Download spreadsheet (csv) files into the "data" folder
    * create an account and download your data from [Comed's Green Button Download webpage](https://secure.comed.com/MyAccount/MyBillUsage/pages/secure/GreenButtonConnectDownloadMyData.aspx)
* Extract the '.csv' files from the `.zip` file you downloaded.
    * **On OSX:** run `find ./ -name \*.zip -exec unzip {} \;`.
    * you should have at least 1 csv file called `energy_use_M_D_Y.csv`
    * place that file in the "data" folder
#### Download your Weather data
* Install [Meteostat](https://github.com/meteostat/meteostat-python/tree/master#installation)
* Use meteostat to get your weather data (**python code below**):
    * replace the **start & end** with your **date range**
    * replace **x, y, z** with **longitude latitude and altitude** for the location you want weather
    * **suggestion:** do 1 year of data at your house
```python
# Import Meteostat library and dependencies
from datetime import datetime
from meteostat import Point, Hourly

# Set date range
start_y = 2022
start_m = 10
start_d = 21

end_y = 2023
end_m =10
end_d = 21
start = datetime(start_y, start_m, start_d)
end = datetime(end_y, end_m, end_d)

# Create Point for Weather Data
x=51.238428
y=-108.4281002
z=18.54
location = Point(x, y, z)

# Get daily data for 2018
data = Hourly(location, start, end)
data = data.fetch()
file_name = f'weather_{start_m}-{start_d}-{start_y}_to_{end_m}-{end_d}-{end_y}.csv'
data.to_csv(file_name)
```

### Install the requirements
* make sure you're in the main "project_title" folder with "requirements.txt"
* Install the requirements using `pip install -r requirements.txt`.
    * Make sure you use Python 3.
    * You may want to use a virtual environment for this.

Usage
----------------------
### Analyze your Data - (Run the Jupyter Notebooks)
-[ ] **TODO:** create a runnable python script from these Jupyter notebooks
In this order run the Jupyter notebooks
1. green_button_data_cleaning.ipynb
2. green_button_data_analysis.ipynb
3. weather_data_cleaning.ipynb
4. electricity_and_weather_analysis.ipynb
**example linux commands**
```console
jupyter nbconvert --execute --to notebook --inplace green_button_data_cleaning.ipynb
jupyter nbconvert --execute --to notebook --inplace green_button_data_analysis.ipynb
jupyter nbconvert --execute --to notebook --inplace weather_data_cleaning.ipynb
jupyter nbconvert --execute --to notebook --inplace electricity_and_weather_analysis.ipynb
```
