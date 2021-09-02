Untitled
================
Eneye
8/25/2021

### Introduction

FINA is a body that regulates aquatic sports. This personal case-study
aims to do an exploratory data analysis on aquatic sports in Olympic
events for the past 10 Olympics: 1984 - 2021.

### Data Source

The data for this analysis was copied from [Fina’s official
website](https://www.fina.org/).

So…lets dive in!

#### Set Up Environment

Install and load packages that will be required.

#### Load Athletes data

#### Load Medals Data

``` r
### Load Medals Data

losangeles_1984_olympics_medals <- read.csv("~/Eneye/Portfolio/water-olympics-EDA/Fina_Olympics_Data/Fina-LosAngeles-1984-Olympics-Medals-Clean.csv")
seoul_1988_olympics_medals <- read.csv("~/Eneye/Portfolio/water-olympics-EDA/Fina_Olympics_Data/Fina-Seoul-1988-Olympics-Medals-Clean.csv")
barcelona_1992_olympics_medals <- read.csv("~/Eneye/Portfolio/water-olympics-EDA/Fina_Olympics_Data/Fina-Barcelona-1992-Olympics-Medals-Clean.csv")
atlanta_1996_olympics_medals <- read.csv("~/Eneye/Portfolio/water-olympics-EDA/Fina_Olympics_Data/Fina-Atlanta-1996-Olympics-Medals-Clean.csv")
sydney_2000_olympics_medals <- read.csv("~/Eneye/Portfolio/water-olympics-EDA/Fina_Olympics_Data/Fina-Sydney-2000-Olympics-Medals-Clean.csv")
athens_2004_olympics_medals <- read.csv("~/Eneye/Portfolio/water-olympics-EDA/Fina_Olympics_Data/Fina-Athens-2004-Olympics-Medals-Clean.csv")
beijing_2008_olympics_medals <- read.csv("~/Eneye/Portfolio/water-olympics-EDA/Fina_Olympics_Data/Fina-Beijing-2008-Olympics-Medals-Clean.csv")
london_2012_olympics_medals <- read.csv("~/Eneye/Portfolio/water-olympics-EDA/Fina_Olympics_Data/Fina-London-2012-Olympics-Medals-Clean.csv")
rio_2016_olympics_medals <- read.csv("~/Eneye/Portfolio/water-olympics-EDA/Fina_Olympics_Data/Fina-Rio-2016-Olympics-Medals-Clean.csv")
tokyo_2020_olympics_medals <- read.csv("~/Eneye/Portfolio/water-olympics-EDA/Fina_Olympics_Data/Fina-Tokyo-2020-Olympics-Medals-Clean.csv")
```

#### Clean and process data

``` r
### Convert DOB from CHR to Date

losangeles_1984_olympics_athletes <- losangeles_1984_olympics_athletes %>% 
  mutate(DOB = as.Date(DOB, format = "%m/%d/%Y"))
seoul_1988_olympics_athletes <- seoul_1988_olympics_athletes %>% 
  mutate(DOB = as.Date(DOB, format = "%m/%d/%Y"))
barcelona_1992_olympics_athletes <- barcelona_1992_olympics_athletes %>% 
  mutate(DOB = as.Date(DOB, format = "%m/%d/%Y"))
atlanta_1996_olympics_athletes <- atlanta_1996_olympics_athletes %>% 
  mutate(DOB = as.Date(DOB, format = "%m/%d/%Y"))
sydney_2000_olympics_athletes <- sydney_2000_olympics_athletes %>% 
  mutate(DOB = as.Date(DOB, format = "%m/%d/%Y"))
athens_2004_olympics_athletes <- athens_2004_olympics_athletes %>% 
  mutate(DOB = as.Date(DOB, format = "%m/%d/%Y"))
beijing_2008_olympics_athletes <- beijing_2008_olympics_athletes %>% 
  mutate(DOB = as.Date(DOB, format = "%m/%d/%Y"))
london_2012_olympics_athletes <- london_2012_olympics_athletes %>% 
  mutate(DOB = as.Date(DOB, format = "%m/%d/%Y"))
rio_2016_olympics_athletes <- rio_2016_olympics_athletes %>% 
  mutate(DOB = as.Date(DOB, format = "%m/%d/%Y"))
tokyo_2020_olympics_athletes <- tokyo_2020_olympics_athletes %>% 
  mutate(DOB = as.Date(DOB, format = "%m/%d/%Y"))
```

*To calculate athletes age as at the time of the Olympics, we will add a
column showing the Olympics start date.*

``` r
### Insert Olympic date column

losangeles_1984_olympics_athletes$olympics_start_date= as.Date("1984-07-28")
seoul_1988_olympics_athletes$olympics_start_date= as.Date("1988-09-17")
barcelona_1992_olympics_athletes$olympics_start_date= as.Date("1992-07-26")
atlanta_1996_olympics_athletes$olympics_start_date= as.Date("1996-07-20")
sydney_2000_olympics_athletes$olympics_start_date= as.Date("2000-09-15")
athens_2004_olympics_athletes$olympics_start_date= as.Date("2004-08-13")
beijing_2008_olympics_athletes$olympics_start_date= as.Date("2008-08-09")
london_2012_olympics_athletes$olympics_start_date= as.Date("2012-07-27")
rio_2016_olympics_athletes$olympics_start_date= as.Date("2016-08-05")
tokyo_2020_olympics_athletes$olympics_start_date= as.Date("2021-07-23")
```

*Calculate athletes age*

``` r
### Calculate athletes age during olympics in new column

losangeles_1984_olympics_athletes$age <- as.integer(time_length(difftime(losangeles_1984_olympics_athletes$olympics_start_date, losangeles_1984_olympics_athletes$DOB), "years"))

seoul_1988_olympics_athletes$age <- as.integer(time_length(difftime(seoul_1988_olympics_athletes$olympics_start_date, seoul_1988_olympics_athletes$DOB), "years"))

barcelona_1992_olympics_athletes$age <- as.integer(time_length(difftime(barcelona_1992_olympics_athletes$olympics_start_date, barcelona_1992_olympics_athletes$DOB), "years"))

atlanta_1996_olympics_athletes$age <- as.integer(time_length(difftime(atlanta_1996_olympics_athletes$olympics_start_date, atlanta_1996_olympics_athletes$DOB), "years"))

sydney_2000_olympics_athletes$age <- as.integer(time_length(difftime(sydney_2000_olympics_athletes$olympics_start_date, sydney_2000_olympics_athletes$DOB), "years"))

athens_2004_olympics_athletes$age <- as.integer(time_length(difftime(athens_2004_olympics_athletes$olympics_start_date, athens_2004_olympics_athletes$DOB), "years"))

beijing_2008_olympics_athletes$age <- as.integer(time_length(difftime(beijing_2008_olympics_athletes$olympics_start_date, beijing_2008_olympics_athletes$DOB), "years"))

london_2012_olympics_athletes$age <- as.integer(time_length(difftime(london_2012_olympics_athletes$olympics_start_date, london_2012_olympics_athletes$DOB), "years"))

rio_2016_olympics_athletes$age <- as.integer(time_length(difftime(rio_2016_olympics_athletes$olympics_start_date, rio_2016_olympics_athletes$DOB), "years"))

tokyo_2020_olympics_athletes$age <- as.integer(time_length(difftime(tokyo_2020_olympics_athletes$olympics_start_date, tokyo_2020_olympics_athletes$DOB), "years"))
```

*Merge all olympic athlete records into one dataset*

``` r
### Merge All olympic records

all_olympics <- bind_rows(losangeles_1984_olympics_athletes, seoul_1988_olympics_athletes, barcelona_1992_olympics_athletes, atlanta_1996_olympics_athletes, sydney_2000_olympics_athletes, athens_2004_olympics_athletes, beijing_2008_olympics_athletes, london_2012_olympics_athletes, rio_2016_olympics_athletes, tokyo_2020_olympics_athletes)
```

*Check the minimum and maximum ages of athletes to find any outlying
figures*

``` r
### Check the minimum and maximum ages of athletes
summary(all_olympics$age)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
    ##   -6.00   19.00   22.00   22.55   25.00   42.00      11

*Search for the actual ages of these outlying figures and correct them*

``` r
### Check for correct DOB and modify
head(all_olympics[order(all_olympics$age),])
```

    ##      Country         NOC         Athlete Gender        DOB Discipline
    ## 1311     ITA       Italy AndreaCECCARINI   Male 1995-04-07   Swimming
    ## 1357     JPN       Japan  ChiakiNAKAMORI Female 1991-09-12   Swimming
    ## 1396     KOR South Korea    Young-HoPARK   Male 1989-05-26   Swimming
    ## 3538     RUS      Russia AleksandrPOPKOV   Male 1994-12-27   Swimming
    ## 1006     EGY       Egypt   MoustafaAHMED   Male 1983-09-01   Swimming
    ## 1254     HUN     Hungary    RichardBODOR   Male 1979-03-10   Swimming
    ##      olympics_start_date age
    ## 1311          1988-09-17  -6
    ## 1357          1988-09-17  -2
    ## 1396          1988-09-17   0
    ## 3538          1996-07-20   1
    ## 1006          1988-09-17   5
    ## 1254          1988-09-17   9

``` r
all_olympics[1311,5] = "1964-04-14"
all_olympics[1357,3] = "ChikakoNAKAMORI"
all_olympics[1357,5] = "1967-04-11"
all_olympics[1396,3] = "Yeong-cheolPARK"
all_olympics[1396,5] = "1969-04-16"
all_olympics[3538,3] = "AlexanderPOPOV"
all_olympics[3538,5] = "1971-11-16"
all_olympics[1006,5] = "1967-09-01"
all_olympics[1254,3] = "Richard MihalyBODOR"
all_olympics[1254,5] = "1962-03-04"
all_olympics[2501,3] = "GaryTAN"
all_olympics[2501,5] = "1973-09-23"

### Recalculate age in new column to effect changes
all_olympics$age <- as.integer(time_length(difftime(all_olympics$olympics_start_date, all_olympics$DOB), "years"))


### Check summary again to see changes
summary(all_olympics$age)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
    ##   12.00   19.00   22.00   22.56   25.00   42.00      11

*To enable us plot a world map, we need to include the latitude and
longitude information of each NOC*

``` r
### Scrape countries lat and long

world_countries <- read_html("https://developers.google.com/public-data/docs/canonical/countries_csv")

noc_coordinates <- world_countries %>%
                          html_nodes("table") %>%
                          extract2(1) %>%
                          html_table()
```

*Join the coordinates dataframe with the olympics athletes dataframe*

``` r
### Include lat and long in olympics table

all_olympics_coordinates <- left_join(all_olympics, noc_coordinates, by = c("NOC" = "name"))
```

\*Filter to see if there are null fields as a result of the join

``` r
### Filter null values

missing_coordinates <- all_olympics_coordinates %>% 
  filter(is.na(latitude))

table(missing_coordinates$NOC)
```

    ## 
    ##                   Chinese Taipei                   Czechoslovakia 
    ##                               67                               29 
    ## Democratic Republic of the Congo                       East Timor 
    ##                                1                                2 
    ##                         Eswatini   Federated States of Micronesia 
    ##                               12                               12 
    ##                    Great Britain                 Hong Kong, China 
    ##                              469                               75 
    ## Independent Olympic Participants                      Ivory Coast 
    ##                                7                                9 
    ##                          Myanmar                  North Macedonia 
    ##                                4                               20 
    ##                        Palestine             Refugee Olympic Team 
    ##                               10                                2 
    ##            Republic of the Congo            Serbia and Montenegro 
    ##                               13                               39 
    ##                     Soviet Union                       The Gambia 
    ##                               51                                2 
    ##                     Unified Team                   Virgin Islands 
    ##                               53                               26 
    ##                       Yugoslavia 
    ##                               53

*Some country names appear differently in the imported NOC coordinates,
we need to make them the same with the IOC names for seamless join*

*Countries like Czechoslovakia, Yugoslavia, Soviet union, Unified team
and Independent Olympic Participants that are no longer in existence
were renamed to the counterpart counties with the most participants,
this is to have them represented on the map*

``` r
### Rename countries to match IOC countries

noc_coordinates_renamed <- noc_coordinates %>% 
  mutate(name = recode(name,"United Kingdom" = "Great Britain")) %>% 
  mutate(name = recode(name,"Hong Kong" = "Hong Kong, China")) %>% 
  mutate(name = recode(name,"U.S. Virgin Islands" = "Virgin Islands")) %>% 
  mutate(name = recode(name,"Swaziland" = "Eswatini")) %>% 
  mutate(name = recode(name,"Taiwan" = "Chinese Taipei")) %>% 
  mutate(name = recode(name,"Congo [DRC]" = "Democratic Republic of the Congo")) %>% 
  mutate(name = recode(name,"Congo [Republic]"  = "Republic of the Congo")) %>% 
  mutate(name = recode(name,"Côte d'Ivoire" = "Ivory Coast")) %>% 
  mutate(name = recode(name,"Micronesia" = "Federated States of Micronesia")) %>% 
  mutate(name = recode(name,"Macedonia [FYROM]" = "North Macedonia")) %>% 
  mutate(name = recode(name,"Myanmar [Burma]" = "Myanmar")) %>% 
  mutate(name = recode(name,"Palestinian Territories" = "Palestine")) %>% 
  mutate(name = recode(name,"Timor-Leste" = "East Timor")) %>% 
  mutate(name = recode(name,"Gambia" = "The Gambia"))

all_olympics_renamed <- all_olympics %>% 
  mutate(NOC = recode(NOC, "Soviet Union" = "Russia")) %>% 
  mutate(NOC = recode(NOC, "Czechoslovakia" = "Czech Republic")) %>% 
  mutate(NOC = recode(NOC, "Yugoslavia" = "Croatia")) %>% 
  mutate(NOC = recode(NOC, "Unified Team" = "Russia")) %>% 
  mutate(NOC = recode(NOC, "Independent Olympic Participants" = "Serbia")) %>% 
  mutate(NOC = recode(NOC, "Serbia and Montenegro" = "Serbia"))
```

*Join the modified dataframes*

``` r
all_olympics_coordinates <- left_join(all_olympics_renamed, noc_coordinates_renamed, by = c("NOC" = "name"))
```

``` r
### Summary and Visualizations

summary(all_olympics$age)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
    ##   12.00   19.00   22.00   22.56   25.00   42.00      11

``` r
  setNames(aggregate(all_olympics_coordinates$age ~ all_olympics_coordinates$Discipline + all_olympics_coordinates$Gender, FUN = mean), c("Discipline", "Gender", "age"))
```

    ##               Discipline Gender      age
    ## 1      Artistic Swimming Female 22.55872
    ## 2                 Diving Female 22.12171
    ## 3             Open Water Female 24.80682
    ## 4               Swimming Female 20.47911
    ## 5  Swimming - Open Water Female 23.58333
    ## 6             Water Polo Female 25.27724
    ## 7                 Diving   Male 23.02244
    ## 8             Open Water   Male 25.50000
    ## 9               Swimming   Male 22.22535
    ## 10 Swimming - Open Water   Male 25.81818
    ## 11            Water Polo   Male 26.77200

``` r
all_olympics_coordinates %>% 
  group_by(Discipline, Gender) %>% 
  summarise(Athlete = n()) %>% 
  arrange(desc(Athlete)) %>% 
  ggplot(aes(x = Discipline, y = Athlete, fill = Gender)) +
  geom_col() +labs(title = "Number of athletes") + theme(axis.text.x = element_text(angle = 50, vjust = 1, hjust = 1, size = 12))
```

    ## `summarise()` has grouped output by 'Discipline'. You can override using the `.groups` argument.

![](water-olympics-EDA_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

``` r
all_olympics_coordinates %>% 
  group_by(NOC) %>% 
  summarise(Athlete = n()) %>% 
  arrange(desc(Athlete))
```

    ## # A tibble: 196 x 2
    ##    NOC           Athlete
    ##    <chr>           <int>
    ##  1 United States     806
    ##  2 Australia         690
    ##  3 Russia            571
    ##  4 Italy             565
    ##  5 China             540
    ##  6 Canada            496
    ##  7 Germany           490
    ##  8 Great Britain     469
    ##  9 Japan             425
    ## 10 Spain             413
    ## # ... with 186 more rows
