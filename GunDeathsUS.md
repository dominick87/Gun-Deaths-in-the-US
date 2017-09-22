
### Read the data in and take a look at it


```python
import csv
f = open("guns.csv",'r')
data = list(csv.reader(f))
data[:5]
```




    [['',
      'year',
      'month',
      'intent',
      'police',
      'sex',
      'age',
      'race',
      'hispanic',
      'place',
      'education'],
     ['1',
      '2012',
      '01',
      'Suicide',
      '0',
      'M',
      '34',
      'Asian/Pacific Islander',
      '100',
      'Home',
      '4'],
     ['2', '2012', '01', 'Suicide', '0', 'F', '21', 'White', '100', 'Street', '3'],
     ['3',
      '2012',
      '01',
      'Suicide',
      '0',
      'M',
      '60',
      'White',
      '100',
      'Other specified',
      '4'],
     ['4', '2012', '02', 'Suicide', '0', 'M', '64', 'White', '100', 'Home', '4']]



#### Extracting headers from a list of lists


```python
headers = data[0]
data = data[1:]
print(headers,"\n\n")
print(data[:5])
```

    ['', 'year', 'month', 'intent', 'police', 'sex', 'age', 'race', 'hispanic', 'place', 'education'] 
    
    
    [['1', '2012', '01', 'Suicide', '0', 'M', '34', 'Asian/Pacific Islander', '100', 'Home', '4'], ['2', '2012', '01', 'Suicide', '0', 'F', '21', 'White', '100', 'Street', '3'], ['3', '2012', '01', 'Suicide', '0', 'M', '60', 'White', '100', 'Other specified', '4'], ['4', '2012', '02', 'Suicide', '0', 'M', '64', 'White', '100', 'Home', '4'], ['5', '2012', '02', 'Suicide', '0', 'M', '31', 'White', '100', 'Other specified', '2']]
    

### Calculate how many gun deaths happened in each year


```python
years = [row[1] for row in data]
year_counts = {}
for year in years:
    if year not in year_counts:
        year_counts[year] = 1
    else:
        year_counts[year] += 1
year_counts
```




    {'2012': 33563, '2013': 33636, '2014': 33599}



### Exploring Gun Deaths By Month And Year

#### Extracting months


```python
import datetime
dates = [datetime.datetime(year=int(row[1]),month=int(row[2]),day=1) for row in data]
dates[:5]
```




    [datetime.datetime(2012, 1, 1, 0, 0),
     datetime.datetime(2012, 1, 1, 0, 0),
     datetime.datetime(2012, 1, 1, 0, 0),
     datetime.datetime(2012, 2, 1, 0, 0),
     datetime.datetime(2012, 2, 1, 0, 0)]



#### Unique deaths per month


```python
date_counts = {}
for item in dates:
    if item not in date_counts:
        date_counts[item] = 1
    else:
        date_counts[item] += 1
date_counts
```




    {datetime.datetime(2012, 1, 1, 0, 0): 2758,
     datetime.datetime(2012, 2, 1, 0, 0): 2357,
     datetime.datetime(2012, 3, 1, 0, 0): 2743,
     datetime.datetime(2012, 4, 1, 0, 0): 2795,
     datetime.datetime(2012, 5, 1, 0, 0): 2999,
     datetime.datetime(2012, 6, 1, 0, 0): 2826,
     datetime.datetime(2012, 7, 1, 0, 0): 3026,
     datetime.datetime(2012, 8, 1, 0, 0): 2954,
     datetime.datetime(2012, 9, 1, 0, 0): 2852,
     datetime.datetime(2012, 10, 1, 0, 0): 2733,
     datetime.datetime(2012, 11, 1, 0, 0): 2729,
     datetime.datetime(2012, 12, 1, 0, 0): 2791,
     datetime.datetime(2013, 1, 1, 0, 0): 2864,
     datetime.datetime(2013, 2, 1, 0, 0): 2375,
     datetime.datetime(2013, 3, 1, 0, 0): 2862,
     datetime.datetime(2013, 4, 1, 0, 0): 2798,
     datetime.datetime(2013, 5, 1, 0, 0): 2806,
     datetime.datetime(2013, 6, 1, 0, 0): 2920,
     datetime.datetime(2013, 7, 1, 0, 0): 3079,
     datetime.datetime(2013, 8, 1, 0, 0): 2859,
     datetime.datetime(2013, 9, 1, 0, 0): 2742,
     datetime.datetime(2013, 10, 1, 0, 0): 2808,
     datetime.datetime(2013, 11, 1, 0, 0): 2758,
     datetime.datetime(2013, 12, 1, 0, 0): 2765,
     datetime.datetime(2014, 1, 1, 0, 0): 2651,
     datetime.datetime(2014, 2, 1, 0, 0): 2361,
     datetime.datetime(2014, 3, 1, 0, 0): 2684,
     datetime.datetime(2014, 4, 1, 0, 0): 2862,
     datetime.datetime(2014, 5, 1, 0, 0): 2864,
     datetime.datetime(2014, 6, 1, 0, 0): 2931,
     datetime.datetime(2014, 7, 1, 0, 0): 2884,
     datetime.datetime(2014, 8, 1, 0, 0): 2970,
     datetime.datetime(2014, 9, 1, 0, 0): 2914,
     datetime.datetime(2014, 10, 1, 0, 0): 2865,
     datetime.datetime(2014, 11, 1, 0, 0): 2756,
     datetime.datetime(2014, 12, 1, 0, 0): 2857}



### Exploring Gun Deaths By Race And Sex


```python
sex_counts = {}
race_counts = {}
for sexy in data:
    if sexy[5] not in sex_counts:
        sex_counts[sexy[5]] = 1
    else:
        sex_counts[sexy[5]] += 1
        
    if sexy[7] not in race_counts:
        race_counts[sexy[7]] = 1
    else:
        race_counts[sexy[7]] += 1
        
print(sex_counts, "\n\n", race_counts)
```

    {'M': 86349, 'F': 14449} 
    
     {'Asian/Pacific Islander': 1326, 'White': 66237, 'Native American/Native Alaskan': 917, 'Black': 23296, 'Hispanic': 9022}
    

### Findings 

So far, in the US, gun deaths affect more men(86%) than women(14%). They also affect more 'Black/White' races. Exploring deaths by months show that gun deaths peaks are in the summer and bottoms in the winter.

However, the analysis only gives us the total number of gun deaths by race in the US. Unless we know the proportion of each race in the US, we won't be able to meaningfully compare those numbers. 

What we really want to get is a rate of gun deaths per 100000 people (total amount of people in our dataset) of each race. In order to do this, we'll need to read in data ("census.csv") about what percentage of the US population falls into each racial category. 


### Reading In A Second Dataset


```python
census = list(csv.reader(open("census.csv",'r')))
census
```




    [['Id',
      'Year',
      'Id',
      'Sex',
      'Id',
      'Hispanic Origin',
      'Id',
      'Id2',
      'Geography',
      'Total',
      'Race Alone - White',
      'Race Alone - Hispanic',
      'Race Alone - Black or African American',
      'Race Alone - American Indian and Alaska Native',
      'Race Alone - Asian',
      'Race Alone - Native Hawaiian and Other Pacific Islander',
      'Two or More Races'],
     ['cen42010',
      'April 1, 2010 Census',
      'totsex',
      'Both Sexes',
      'tothisp',
      'Total',
      '0100000US',
      '',
      'United States',
      '308745538',
      '197318956',
      '44618105',
      '40250635',
      '3739506',
      '15159516',
      '674625',
      '6984195']]



### Computing Rates Of Gun Deaths Per Race


```python
mapping = {}
mapping["Asian/Pacific Islander"] = int(census[1][14]+census[1][15])
mapping["Black"] = int(census[1][12])
mapping["Native American/Native Alaskan"] = int(census[1][13])
mapping["Hispanic"] = int(census[1][11])
mapping["White"] = int(census[1][10])

race_per_hundredk = {}
for key,val in race_counts.items():
    race_per_hundredk[key] = (val/mapping[key])*100000
    
race_per_hundredk
```




    {'Asian/Pacific Islander': 8.746980714890115e-06,
     'Black': 57.8773477735196,
     'Hispanic': 20.220491210910907,
     'Native American/Native Alaskan': 24.521955573811088,
     'White': 33.56849303419181}



### Filtering By Homicide Intent


```python
intents = [loop[3] for loop in data]
races = [loop[7] for loop in data]
homicide_race_counts = {}
for i,race in enumerate(races):
    if intents[i] == 'Homicide':
        if race not in homicide_race_counts:
            homicide_race_counts[race] = 1
        else:
            homicide_race_counts[race] += 1
            
race_per_hundredk = {}
for key,val in homicide_race_counts.items():
    race_per_hundredk[key] = (val/mapping[key])*100000
    
race_per_hundredk
```




    {'Asian/Pacific Islander': 3.687452654316421e-06,
     'Black': 48.471284987180944,
     'Hispanic': 12.627161104219914,
     'Native American/Native Alaskan': 8.717729026240365,
     'White': 4.6356417981453335}



### Findings

It appears that gun related homicides in the US disproportionately affect people in the "Black" and "Hispanic" racial categories.

Here are some potential next steps:
* Figure out the link, if any, between month and homicide rate.
* Explore the homicide rate by gender.
* Explore the rates of other intents, like Accidental, by gender and race.
* Find out if gun death rates correlate to location and education.


```python

```
