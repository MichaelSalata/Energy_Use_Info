Energy Use Info
-----------------------
## Introduction
* This project creates insight on energy usage patterns in relation to time & weather.
    * It requires (downloadable) [ComEd](https://secure.comed.com/MyAccount/MyBillUsage/pages/secure/GreenButtonConnectDownloadMyData.aspx) & [Meteostat](https://github.com/meteostat/meteostat-python) data spreadsheets.
    * Cleans dirty data
    * Creates intuitive graphs & conclusions


Example Graphs
-----------------------
![](https://i.imgur.com/2qTrv9n.png)
![](https://i.imgur.com/J4BfXVa.png)
![](https://i.imgur.com/MIfk2kF.png)
### Data Used
* **Energy data** is downloaded from [Comed's Green Button Download webpage](https://secure.comed.com/MyAccount/MyBillUsage/pages/secure/GreenButtonConnectDownloadMyData.aspx).
* **Weather data** is downloaded using [Meteostat](https://github.com/meteostat/meteostat-python).

Installation
----------------------
#### Clone this repo
#### Download your Data
##### Download your ComEd Usage Data
* create a folder titled "**data**" inside this project
* Download spreadsheet(csv) files into the "**data**" folder
    * Navigate to [Comed's Green Button Download webpage](https://secure.comed.com/MyAccount/MyBillUsage/pages/secure/GreenButtonConnectDownloadMyData.aspx)
    * Log in using your ComEd account
    * Under `Download my data`
        * Click `Green Button Download my data`
        * Set `Format` to `CSV`
        * Use `Export usage for a range of days` (1 Month or 1 Year is recommended)

* Extract '**.csv**' files from the `.zip` file you downloaded.
    * **On OSX:** run `find ./ -name \*.zip -exec unzip {} \;`.
    * example: **cec_electric_interval_data_Service**_M1_D1_Y1_to_M2_D2_Y2.csv
* Rename the '.csv' to **energy_use**_M1_D1_Y1_to_M2_D2_Y2.csv
* place that file in the **data** folder
##### Download your Weather data
* Install [Meteostat](https://github.com/meteostat/meteostat-python/tree/master#installation)
```sh
pip install meteostat
```
* Use meteostat to get your weather data (**python code below**):
    * replace the **start** & **end** dates with your ComEd Data **date range**
    * replace **x, y, z** with **longitude, latitude, altitude** for the location you want weather
```python
# Import Meteostat library and dependencies
from datetime import datetime
from meteostat import Point, Hourly

# Set date range
start_y = your_start_year
start_m = your_start_month
start_d = your_start_day
start = datetime(start_y, start_m, start_d)

end_y = your_end_year
end_m = your_end_month
end_d = your_end_day
end = datetime(end_y, end_m, end_d)

# Create Point for Weather Data
x=your_longitude
y=your_latitude
z=your_altitude
location = Point(x, y, z)

# Get daily data
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
FUTURE IMPROVEMENTS
-----------------------
-[ ] Create an script that pulls the date range of the ComEd so that it only requires the location
-[ ] combine jupyter notebooks into runnable python script to for easy public use 
-[ ] Generalize the code to run on arbitrary weather & electricity values
-[ ] Research how to parse Green Button XML data, then any company with Green Button is compatible (many)
