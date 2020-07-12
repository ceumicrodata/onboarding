---
title: "How to use csvkit"
teaching: 0
exercises: 0
questions:
- How to open data with csvkit?
- How to select certain rows and columns of the data? How to append them after filtering?
- How to sort and describe basic characteristics of the data?
objectives:
- Learn how to install csvkit and how to use csvlook
- Learn csvgrep, csvcut and csvstack commands
- Learn csvsort and csvstat commands
---

{% include links.md %}

## The use of csvkit

csvkit is a command-line tool written in Python to be used for simple data wrangling and analysis tasks. This tutorial presents the most important commands implemented in it. The following sections rely heavily on the official csvkit [tutorial](https://csvkit.readthedocs.io/en/1.0.5/tutorial.html). 

## Installing csvkit

The csvkit tool can be installed with the following command (if you use Python 2.7 you might type `sudo pip install csvkit` instead).

~~~
$ sudo pip3 install csvkit
~~~
{: .bash}

For illustration purposes an example [dataset](https://perso.telecom-paristech.fr/eagan/class/igr204/datasets) is also used in this tutorial. The data contain information on cars and their characteristics. To get the data you should type the following command.
The dataset has a second row with information on data type that is removed for later analysis purposes with the head and tail commands - an alternative way to do this is by using `sed 2,2d cars.csv > cars-tutorial.csv`.

~~~
$ wget https://perso.telecom-paristech.fr/eagan/class/igr204/data/cars.csv
$ head -1 cars.csv > cars-tutorial.csv
$ tail -n+3 cars.csv >> cars-tutorial.csv
~~~
{: .bash}


## The most important csvkit commands

The example dataset is semi-colon and not comma separated. For all the commands presented below the input delimiter can be set with the `-d` argument: in this case as -`d ";"`. Setting the input delimiter with `-d` changes the decimal separator in the ouput as well. To change it back to dot from comma, `csvformat -D "."` should be used after any command where it is relevant.

- `csvlook` shows the data in a Markdown-compatible format. `cat` may also be used instead of `csvlook` to open a csv file, but the latter is more readable.
  This command can be combined with `head` in order to have a look at the first few lines of the data. As seen here and in later examples, csvkit commands can be piped together and with other commands.

  ~~~
  $ csvlook -d ";" cars-tutorial.csv | csvformat -D "."
  $ head -5 cars-tutorial.csv | csvlook -d ";" | csvformat -D "."
  ~~~
  {: .bash}

  For the latter command the following output can be seen.

  ~~~
  | Car                       | MPG | Cylinders | Displacement | Horsepower | Weight | Acceleration | Model | Origin |
  | ------------------------- | --- | --------- | ------------ | ---------- | ------ | ------------ | ----- | ------ |
  | Chevrolet Chevelle Malibu |  18 |         8 |          307 |        130 |  3 504 |         12.0 |    70 | US     |
  | Buick Skylark 320         |  15 |         8 |          350 |        165 |  3 693 |         11.5 |    70 | US     |
  | Plymouth Satellite        |  18 |         8 |          318 |        150 |  3 436 |         11.0 |    70 | US     |
  | AMC Rebel SST             |  16 |         8 |          304 |        150 |  3 433 |         12.0 |    70 | US     |
  ~~~
  {: .output}

- `csvcut` shows the column names in the data if the `-n` argument is specified. It can also help to select certain columns of the data with the `-c` argument and the corresponding column numbers (or names).

  ~~~
  $ csvcut -n -d ";" cars-tutorial.csv
  ~~~
  {: .bash}

  The output is the following:

  ~~~
  1: Car
  2: MPG
  3: Cylinders
  4: Displacement
  5: Horsepower
  6: Weight
  7: Acceleration
  8: Model
  9: Origin
  ~~~
  {: .output}

  The following two commands have identical outputs: car, miles per gallon consumption and origin columns, as shown below. For space constraints only the first few rows are printed out.

  ~~~
  $ csvcut -c 1,2,9 -d ";" cars-tutorial.csv | head -5 | csvlook
  $ csvcut -c Car,MPG,Origin -d ";" cars-tutorial.csv | head -5 | csvlook
  ~~~
  {: .bash}

  ~~~
  | Car                       | MPG | Origin |
  | ------------------------- | --- | ------ |
  | Chevrolet Chevelle Malibu |  18 | US     |
  | Buick Skylark 320         |  15 | US     |
  | Plymouth Satellite        |  18 | US     |
  | AMC Rebel SST             |  16 | US     |
  ~~~
  {: .output}

- `csvstat` calculates summary statistics for all columns. It recognizes the data type of the column and prints out descriptive information accordingly. `csvstat` may be piped together with `csvcut` to calculate descriptive statistics only for certain columns.

  The following command shows the summary statistics for the car, miles per gallon consumption and origin columns.

  ~~~
  $ csvcut -c 1,2,9 -d ";" cars-tutorial.csv | csvstat | csvformat -D "."
  ~~~
  {: .bash}

  ~~~
  "  1. ""Car"""

	Type of data:          Text
	Contains null values:  False
	Unique values:         308
	Longest value:         36 characters
	Most common values:    Toyota Corolla (9x)
	                       Ford Pinto (6x)
	                       Ford Maverick (5x)
	                       AMC Matador (5x)
	                       Volkswagen Rabbit (5x)

  "  2. ""MPG"""

	Type of data:          Number
	Contains null values:  False
	Unique values:         130
	Smallest value:        0
	Largest value:         46.6
	Sum:                   9 358.8
	Mean:                  23.051
	Median:                22.35
	StDev:                 8.402
	Most common values:    13 (20x)
	                       14 (19x)
	                       18 (17x)
	                       15 (16x)
	                       26 (14x)

  "  3. ""Origin"""

	Type of data:          Text
	Contains null values:  False
	Unique values:         3
	Longest value:         6 characters
	Most common values:    US (254x)
	                       Japan (79x)
	                       Europe (73x)

  Row count: 406
  ~~~
  {: .output}

- `csvsort` sorts the rows for the column specified (either with a number or a name) after the argument `-c`. Reversed order can be set by using `-r`.

  Based on the previous example, the highest value in miles per gallon is 46.6. If you want to search for this very fuel efficient car, one way is to sort the data in a reversed order.

  ~~~
  $ csvcut -c 1,2 -d ";" cars-tutorial.csv | csvsort -c 2 -r | head -5 | csvlook | csvformat -D "."
  ~~~ 
  {: .bash}

  The output shows the four most fuel efficient cars. Mazda GLC, the most fuel efficient one has indeed a 46.6 miles per gallon consumption.

  ~~~
  | Car                          |  MPG |
  | ---------------------------- | ---- |
  | Mazda GLC                    | 46.6 |
  | Honda Civic 1500 gl          | 44.6 |
  | Volkswagen Rabbit C (Diesel) | 44.3 |
  | Volkswagen Pickup            | 44.0 |
  ~~~
  {: .output}

- `csvgrep` selects rows that match specific patterns, so in other words it can be used for filtering. The pattern may either be a string or an integer. The `-c` argument specifies the column in which the pattern is searched for (either the column number or name can be used), while -m defines the pattern.

  Following the previous examples, the car with the highest miles per gallon consumption (which is 46.6) is searched for.

  ~~~
  $ csvgrep -c MPG -m 46.6 -d ";" cars-tutorial.csv | csvlook | csvformat -D "."
  ~~~
  {: .bash}

  The command yields the following output showing only cars with a 46.6 miles per gallon consumption. There is only one such car: Mazda GLC.

  ~~~
  | Car       |  MPG | Cylinders | Displacement | Horsepower | Weight | Acceleration | Model | Origin |
  | --------- | ---- | --------- | ------------ | ---------- | ------ | ------------ | ----- | ------ |
  | Mazda GLC | 46.6 |         4 |           86 |         65 |  2 110 |         17.9 |    80 | Japan  |
  ~~~
  {: .output}

  It is also possible to filter and separate the file based on a string variable. In the following example three different csv files are created based on the origin variable. We know from the `csvstat` command that there are three possible categories for origin: US, Japan and Europe. 

  ~~~
  $ csvgrep -c Origin -m US -d ";" cars-tutorial.csv > cars-tutorial-us.csv
  $ csvgrep -c Origin -m Japan -d ";" cars-tutorial.csv > cars-tutorial-japan.csv
  $ csvgrep -c Origin -m Europe -d ";" cars-tutorial.csv > cars-tutorial-europe.csv
  ~~~
  {: .bash}

- `csvstack` appends datasets with identical column names. There might be cases where it makes sense to specify the `-g` argument which adds a column identifying the source csv. In the following example it is not needed.

  The three csv files created in the previous example can be stacked. Since there were three countries of origin, this command should have the same length as the original data.

  ~~~
  $ csvstack cars-tutorial-us.csv cars-tutorial-europe.csv cars-tutorial-japan.csv
  $ csvstack cars-tutorial-us.csv cars-tutorial-europe.csv cars-tutorial-japan.csv | wc -l
  $ wc cars-tutorial.csv -l
  ~~~
  {: .bash}

  Both files have 407 rows as expected (406 plus the header).

## Useful resources for learning csvkit:
- The csvkit tutorial and documentation: <https://csvkit.readthedocs.io/en/1.0.5/tutorial.html />

