# Stata Weather Command

The following package processes remote sensing rainfall and temperature data and outputs 

## Data

The command can be used with either rainfall or temperature data from any source. The only requirements are that:

1. The data is “wide,” meaning each location is a row and each column is rainfall or temperature reading from a different day.
2. The data is measured daily.
3. The variable names for each column contain yyyymmdd. The variable names can have any prefix but must contain the year, month, and day.

## Command: set up

Using data sets as defined above, the weather command creates useful statistics in the same fashion for all years. The command together with an example do file is in the zipped folder weather_command. Place the file weather.ado into wherever Stata stores your .ado files. The file weather_wrapper.do provides an example of the syntax and how to run the command.

The general syntax of the command is as follows.

- After the command name, one has to define what variables contain the rain/temperature information. I provide examples for CHIRPS and ECMWF. For the CHIRPS datasets, the prefix on the weather variables is pic_ while in the case of ECMWF the prefix is y_.
- Next, one needs to tell the command whether the data is rain_data or temperature_data.
- One then has to select a season to study using the options ini_month(number), fin_month(number) and day_month(number), if not specified, the default is the first day of the month. For example, in the example .do file I chose a season from the middle of March to the middle of June. At this moment, we must be careful with seasons that contain months that contain two different years, such as November to February. In this case some renaming of the variables is necessary. (Sorry about that…)
- The option keep tells the command to keep the variables it creates plus some of the original variables in order to match them with other datasets.
- The save of option tells the program to save the dataset in a given location with a given name.

## Command: Results

1. **Rainfall variables**

When the rainfall option is chosen, the command generates the following variable for each season:

- Mean Daily Rainfall           `mean_season_'year'`
- Median Daily Rainfall         `median_season_'year'`
- Variance of Daily Rainfall    `sd_season_'year'`
- Skew of Daily Rainfall        `total_season_'year'`
- Total Rainfall                `skew_season_'year'`
- Deviation in Total Rainfall   `dev_total_season_'year'`
- Z-Score of Total Rainfall     `z_total_season_'year'`
- Rainy Days                    `raindays_'year'`
- Deviation in Rainy Days       `dev_raindays_'year'`
- No Rain Days                  `norain_'year'`
- Deviation in No Rain Days     `dev_norain_'year'`
- % Rainy Days                  `percent_raindays_'year'`
- Deviation in % Rainy Days     `dev_percent_raindays_'year'`
- Longest Dry Spell             `dry_'year'`

In addition to these basic statistics, the command also calculates the long-term averages for total_season, norain, raindays, and raindays_percent. It then uses these to generate variables that measure each seasons deviation from the long-term average and the deviation measured as a z-score.

2. **Temperatire variables**

When the temperature option is chosen, the command generates the following variable for each season:

- Mean Daily Temperature         `mean_season_'year'`
- Median Daily Temperature       `median_season_'year'`
- Variance of Daily Temperature  `sd_season_'year'`
- Skew of Daily Temperature      `skew_season_'year'`
- Growing Degree Days (GDD)      `gdd_'year'`
- Deviation in GDD               `dev_gdd_'year'`
- Z-Score of GDD                 `z_gdd_'year'`
- Maximum Daily Temperature      `max_season_'year'`

Growing degree days are calculated using the options growbase_low(number) and growbase_high(number) to determine the number of days where the temperature was between that range. As with the rainfall option, the temperature option also generates deviations in GDD from the long-term average and the deviation measured as a z-score.

Following Schlenker/Roberts, the command also calculates temperature bins as the percentage of days that fall in each temperature quintile during the season. It then generates the variables `tempbin'quintile''year'`.
