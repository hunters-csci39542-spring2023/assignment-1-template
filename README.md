# Assignment 1: Turnstile Counts

Program Description
Program 1: Turnstile Counts.   Due 10am, Wednesday, 1 February.
Learning Objective: to build competency with dictionaries and string functions of core Python.
Available Libraries: Core Python 3.6+ only.
Data Sources: MTA's Turnstile Data.
Sample Datasets: Week ending 10/29/22 (turnstile_221029.txt), Week ending 6/11/22 (turnstile_220611.txt).

The NYC MTA provides counts of the number of entries and exits through every turnstile in every subway station, as well as daily counts for the entire system.

Write a program that will compute the number of entries at subway stations using the MTA turnstile dataset. To allow for unit testing, your program should have the following functions:

- make_dictionary(data, type = "min"): Depending on the type specified (min, max, or station), the resulting dictionary will store the minimum entry number seen (as an integer), the maximum entry number seen (as an integer), or the station name (as a string). Returns the resulting dictionary.
- get_turnstiles(station_dict, stations = None): Returns a dictionary of names with values the number of times each name occurs in the input, names_lst. If station is None, returns the names of all the turnstiles stored as keys in the inputted dictionary. stations is a list. If a station is specified, returns the keys which have value station in the inputed dictionary. Expected return value is a list.
- compute_ridership(min_dict,max_dict,turnstiles = None): Takes as input two dictionaries, min_dict and max_dict, and a list, turnstiles (possibly None) of stations. Returns a list of the ridership (the difference between the minimum and maximum values). If no value is passed for turnstile, the default value of None is used (that is, a list of the ridership for every station in the dictionaries).

For example, open the data file turnstile_220611.txt, storing the data in data:
```
file_name = 'turnstile_220611.txt'
#Store the file contents in data:
with open(file_name,encoding='UTF-8') as file_d:
  lines = file_d.readlines()
#Discard first line with headers:
data = lines[1:]
```

Next, lets use the functions above to set up the three dictionaries:
```
min_dict = make_dictionary(data, kind = "min")
max_dict = make_dictionary(data, kind = "max")
station_dict = make_dictionary(data, kind = "station")

#Print out the station names, alphabetically, without duplicates:
print(f'All stations: {sorted(list(set(station_dict.values())))}')
```

gives the output:

```
All stations: ['1 AV', '103 ST', '103 ST-CORONA', '104 ST', '110 ST', '111 ST', '116 ST', '116 ST-COLUMBIA', '121 ST', '125 ST', '135 ST', '137 ST CITY COL', '138/GRAND CONC', '14 ST', '14 ST-UNION SQ', '145 ST', '149/GRAND CONC', '14TH STREET', '15 ST-PROSPECT', '155 ST', '157 ST', '161/YANKEE STAD', '163 ST-AMSTERDM', '167 ST', '168 ST', '169 ST', '170 ST', '174 ST', '174-175 STS', '175 ST', '176 ST', '18 AV', '18 ST', '181 ST', '182-183 STS', '183 ST', '190 ST', '191 ST', '2 AV', '20 AV', '207 ST', '21 ST', '21 ST-QNSBRIDGE', '215 ST', '219 ST', '225 ST', '23 ST', '231 ST', '233 ST', '238 ST', '25 AV', '25 ST', '28 ST', '3 AV', '3 AV 138 ST', '3 AV-149 ST', '30 AV', '33 ST', '33 ST-RAWSON ST', '34 ST-HERALD SQ', '34 ST-HUDSON YD', '34 ST-PENN STA', '36 AV', '36 ST', '39 AV', '4 AV-9 ST', '40 ST LOWERY ST', '42 ST-BRYANT PK', '42 ST-PORT AUTH', '45 ST', '46 ST', '46 ST BLISS ST', '47-50 STS ROCK', '49 ST', '4AV-9 ST', '5 AV/53 ST', '5 AV/59 ST', '5 AVE', '50 ST', '51 ST', '52 ST', '53 ST', '55 ST', '57 ST', '57 ST-7 AV', '59 ST', '59 ST COLUMBUS', '6 AV', '61 ST WOODSIDE', '63 DR-REGO PARK', '65 ST', '66 ST-LINCOLN', '67 AV', '68ST-HUNTER CO', '69 ST', '7 AV', '71 ST', '72 ST', '72 ST-2 AVE', '74 ST-BROADWAY', '75 AV', '75 ST-ELDERTS', '77 ST', '79 ST', '8 AV', '8 ST-NYU', '80 ST', '81 ST-MUSEUM', '82 ST-JACKSON H', '85 ST-FOREST PK', '86 ST', '86 ST-2 AVE', '88 ST', '9 AV', '90 ST-ELMHURST', '96 ST', '96 ST-2 AVE', '9TH STREET', 'ALABAMA AV', 'ALLERTON AV', 'AQUEDUCT N.COND', 'AQUEDUCT RACETR', 'ASTOR PL', 'ASTORIA BLVD', 'ASTORIA DITMARS', 'ATL AV-BARCLAY', 'ATLANTIC AV', 'AVENUE H', 'AVENUE I', 'AVENUE J', 'AVENUE M', 'AVENUE N', 'AVENUE P', 'AVENUE U', 'AVENUE X', "B'WAY-LAFAYETTE", 'BAY 50 ST', 'BAY PKWY', 'BAY RIDGE AV', 'BAY RIDGE-95 ST', 'BAYCHESTER AV', 'BEACH 105 ST', 'BEACH 25 ST', 'BEACH 36 ST', 'BEACH 44 ST', 'BEACH 60 ST', 'BEACH 67 ST', 'BEACH 90 ST', 'BEACH 98 ST', 'BEDFORD AV', 'BEDFORD PK BLVD', 'BEDFORD-NOSTRAN', 'BERGEN ST', 'BEVERLEY ROAD', 'BEVERLY RD', 'BLEECKER ST', 'BOROUGH HALL', 'BOTANIC GARDEN', 'BOWERY', 'BOWLING GREEN', 'BRIARWOOD', 'BRIGHTON BEACH', 'BROAD CHANNEL', 'BROAD ST', 'BROADWAY', 'BROADWAY JCT', 'BRONX PARK EAST', 'BROOK AV', 'BROOKLYN BRIDGE', 'BUHRE AV', 'BURKE AV', 'BURNSIDE AV', 'BUSHWICK AV', 'CANAL ST', 'CANARSIE-ROCKAW', 'CARROLL ST', 'CASTLE HILL AV', 'CATHEDRAL PKWY', 'CENTRAL AV', 'CENTRAL PK N110', 'CHAMBERS ST', 'CHAUNCEY ST', 'CHRISTOPHER ST', 'CHURCH AV', 'CITY / BUS', 'CITY HALL', 'CLARK ST', 'CLASSON AV', 'CLEVELAND ST', 'CLINTON-WASH AV', 'CONEY IS-STILLW', 'CORTELYOU RD', 'CORTLANDT ST', 'COURT SQ', 'COURT SQ-23 ST', 'CRESCENT ST', 'CROWN HTS-UTICA', 'CYPRESS AV', 'CYPRESS HILLS', 'DEKALB AV', 'DELANCEY/ESSEX', 'DITMAS AV', 'DYCKMAN ST', "E 143/ST MARY'S", 'E 149 ST', 'E 180 ST', 'EAST 105 ST', 'EAST BROADWAY', 'EASTCHSTER/DYRE', 'EASTN PKWY-MUSM', 'ELDER AV', 'ELMHURST AV', 'EUCLID AV', 'EXCHANGE PLACE', 'FAR ROCKAWAY', 'FLATBUSH AV-B.C', 'FLUSHING AV', 'FLUSHING-MAIN', 'FORDHAM RD', 'FOREST AVE', 'FOREST HILLS 71', 'FRANKLIN AV', 'FRANKLIN ST', 'FREEMAN ST', 'FRESH POND RD', 'FT HAMILTON PKY', 'FULTON ST', 'GATES AV', 'GRAHAM AV', 'GRAND ARMY PLAZ', 'GRAND ST', 'GRAND-NEWTOWN', 'GRANT AV', 'GRD CNTRL-42 ST', 'GREENPOINT AV', 'GROVE STREET', 'GUN HILL RD', 'HALSEY ST', 'HARLEM 148 ST', 'HARRISON', 'HEWES ST', 'HIGH ST', 'HOUSTON ST', 'HOWARD BCH JFK', 'HOYT ST', 'HOYT-SCHER', 'HUNTERS PT AV', 'HUNTS POINT AV', 'INTERVALE AV', 'INWOOD-207 ST', 'JACKSON AV', 'JAMAICA 179 ST', 'JAMAICA CENTER', 'JAMAICA VAN WK', 'JAY ST-METROTEC', 'JEFFERSON ST', 'JFK JAMAICA CT1', 'JKSN HT-ROOSVLT', 'JOURNAL SQUARE', 'JUNCTION BLVD', 'JUNIUS ST', 'KEW GARDENS', 'KINGS HWY', 'KINGSBRIDGE RD', 'KINGSTON AV', 'KINGSTON-THROOP', 'KNICKERBOCKER', 'KOSCIUSZKO ST', 'LACKAWANNA', 'LAFAYETTE AV', 'LEXINGTON AV/53', 'LEXINGTON AV/63', 'LIBERTY AV', 'LIVONIA AV', 'LONGWOOD AV', 'LORIMER ST', 'MARBLE HILL-225', 'MARCY AV', 'METROPOLITAN AV', 'METS-WILLETS PT', 'MIDDLETOWN RD', 'MONTROSE AV', 'MORGAN AV', 'MORISN AV/SNDVW', 'MORRIS PARK', 'MOSHOLU PKWY', 'MT EDEN AV', 'MYRTLE AV', 'MYRTLE-WILLOUGH', 'MYRTLE-WYCKOFF', 'NASSAU AV', 'NECK RD', 'NEPTUNE AV', 'NEREID AV', 'NEVINS ST', 'NEW LOTS', 'NEW LOTS AV', 'NEW UTRECHT AV', 'NEWARK BM BW', 'NEWARK C', 'NEWARK HM HE', 'NEWARK HW BMEBE', 'NEWKIRK AV', 'NEWKIRK PLAZA', 'NORTHERN BLVD', 'NORWOOD 205 ST', 'NORWOOD AV', 'NOSTRAND AV', 'OCEAN PKWY', 'ORCHARD BEACH', 'OZONE PK LEFFRT', 'PARK PLACE', 'PARKCHESTER', 'PARKSIDE AV', 'PARSONS BLVD', 'PATH NEW WTC', 'PATH WTC 2', 'PAVONIA/NEWPORT', 'PELHAM BAY PARK', 'PELHAM PKWY', 'PENNSYLVANIA AV', 'PRESIDENT ST', 'PRINCE ST', 'PROSPECT AV', 'PROSPECT PARK', 'QUEENS PLAZA', 'QUEENSBORO PLZ', 'RALPH AV', 'RECTOR ST', 'RIT-MANHATTAN', 'RIT-ROOSEVELT', 'ROCKAWAY AV', 'ROCKAWAY BLVD', 'ROCKAWAY PARK B', 'ROOSEVELT ISLND', 'SARATOGA AV', 'SENECA AVE', 'SHEEPSHEAD BAY', 'SHEPHERD AV', 'SIMPSON ST', 'SMITH-9 ST', 'SOUTH FERRY', 'SPRING ST', 'ST LAWRENCE AV', 'ST. GEORGE', 'STEINWAY ST', 'STERLING ST', 'SUTPHIN BLVD', 'SUTPHIN-ARCHER', 'SUTTER AV', 'SUTTER AV-RUTLD', 'THIRTY ST', 'THIRTY THIRD ST', 'TIMES SQ-42 ST', 'TOMPKINSVILLE', 'TREMONT AV', 'TWENTY THIRD ST', 'UNION ST', 'UTICA AV', 'V.CORTLANDT PK', 'VAN SICLEN AV', 'VAN SICLEN AVE', 'VERNON-JACKSON', 'W 4 ST-WASH SQ', 'W 8 ST-AQUARIUM', 'WAKEFIELD/241', 'WALL ST', 'WEST FARMS SQ', 'WESTCHESTER SQ', 'WHITEHALL S-FRY', 'WHITLOCK AV', 'WILSON AV', 'WINTHROP ST', 'WOODHAVEN BLVD', 'WOODLAWN', 'WORLD TRADE CTR', 'WTC-CORTLANDT', 'YORK ST', 'ZEREGA AV']
```

We can print all the turnstiles from the data:

```
print(f'All turnstiles: {get_turnstiles(station_dict)}')
```

Or, a subset, for example, only those for Hunter & Roosevelt Island stations:

```
print(get_turnstiles(station_dict, stations = ['68ST-HUNTER CO','ROOSEVELT ISLND']))
```

which would print:
```
['R259,00-00-00', 'R259,00-00-01', 'R259,00-00-02', 'R259,00-00-03', 'R259,00-05-00', 'R259,00-05-01', 'R177,00-00-00', 'R177,00-00-01', 'R177,00-00-02', 'R177,00-00-03', 'R177,00-00-04', 'R177,00-00-05', 'R177,00-00-06', 'R177,00-03-00', 'R177,00-03-01', 'R177,00-03-02', 'R177,00-03-03', 'R177,00-03-04', 'R177,00-03-05', 'R177,00-03-06']
```

Checking the ridership for a station:
```
hunter_turns = get_turnstiles(station_dict, stations = ['68ST-HUNTER CO'])
ridership = compute_ridership(min_dict,max_dict,turnstiles=hunter_turns)
print(f'Ridership for Hunter College: {ridership}.')
```
gives the output:
```
Ridership for turnstile, R051,02-00-00:  3096.
Ridership for Hunter College: 49669.  
```

Notes:

- You should submit a file with only the standard comments at the top, this function, and any helper functions you have written. The grading scripts will then import the file for testing. If your file includes code outside of functions, either comment the code out before submitting or use a main function that is conditionally executed (see Think CS: Section 6.8 for details).
- Below is a template for this program, including function stubs and testing in a (conditionally executed) main function:
