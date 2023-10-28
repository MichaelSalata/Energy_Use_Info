Energy Use Info
-----------------------
**Introduction**:
* This project is meant to give insight on my house's energy use.
* It cleans dirty data and, creates intuitive graphs & conclusions from my houses energy usage data.
* Data was downloaded from [Comed's Green Button Download webpage](https://secure.comed.com/MyAccount/MyBillUsage/pages/secure/GreenButtonConnectDownloadMyData.aspx).
* Currently downloading your data requires logging in using your comed account details.


Installation
----------------------
### Clone this repo to your computer.
### Download the data
* Download data files into a "data" folder 
    * create an account and download your data from [Comed's Green Button Download webpage](https://secure.comed.com/MyAccount/MyBillUsage/pages/secure/GreenButtonConnectDownloadMyData.aspx)
* Extract the '.csv' files from the `.zip` file you downloaded.
    * On OSX, you can run `find ./ -name \*.zip -exec unzip {} \;`.
    * At the end, you should have a bunch of csv files called `energy_use_M_D_Y.csv`
* delete all the '.zip' files

### Install the requirements
* make sure you're in the main "project_title" folder with "requirements.txt"
* Install the requirements using `pip install -r requirements.txt`.
    * Make sure you use Python 3.
    * You may want to use a virtual environment for this.

Settings  BELOW_THIS_IS_NOT_COMPLETE
--------------------

Look in `settings.py` for the configuration options.
Configuration Option Overview:

* `EXAMPLE_CONFIG0` -- config description
* `EXAMPLE_CONFIG1` -- config description
* `EXAMPLE_CONFIG2` -- config description

Private Settings
--------------------
* Create a file named `private.py` in this folder.
    * Add a value named `PRIVATE_TOKEN_EG`
    * Assign your API token to it.

Usage
-----------------------

* Run `mkdir processed` to create a directory for our processed datasets.
* Run `python assemble.py` to combine the `Acquisition` and `Performance` datasets.
    * This will create `Acquisition.txt` and `Performance.txt` in the `processed` folder.
* Run `python annotate.py`.
    * This will create training data from `Acquisition.txt` and `Performance.txt`.
    * It will add a file called `train.csv` to the `processed` folder.
* Run `python predict.py`.
    * This will run cross validation across the training set, and print the accuracy score.

Extending this
-------------------------

If you want to extend this work, here are a few places to start:

* Generate more features in `annotate.py`.
* Switch algorithms in `predict.py`.
* Add in a way to make predictions on future data.
* Try seeing if you can predict if a bank should have issued the loan.
    * Remove any columns from `train` that the bank wouldn't have known at the time of issuing the loan.
        * Some columns are known when Fannie Mae bought the loan, but not before
    * Make predictions.
* Explore seeing if you can predict columns other than `foreclosure_status`.
    * Can you predict how much the property will be worth at sale time?
* Explore the nuances between performance updates.
    * Can you predict how many times the borrower will be late on payments?
    * Can you map out the typical loan lifecycle?
