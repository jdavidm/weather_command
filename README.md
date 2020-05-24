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

## Command: Results

