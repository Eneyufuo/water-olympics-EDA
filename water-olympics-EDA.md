Untitled
================
Eneye
8/25/2021

``` r
### Load Packages

library(tidyverse)
```

    ## -- Attaching packages --------------------------------------- tidyverse 1.3.1 --

    ## v ggplot2 3.3.5     v purrr   0.3.4
    ## v tibble  3.1.3     v dplyr   1.0.7
    ## v tidyr   1.1.3     v stringr 1.4.0
    ## v readr   2.0.0     v forcats 0.5.1

    ## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(ggplot2)
library(lubridate)
```

    ## 
    ## Attaching package: 'lubridate'

    ## The following objects are masked from 'package:base':
    ## 
    ##     date, intersect, setdiff, union

``` r
### Load Athletes data

seoul_1988_olympics_athletes <- read.csv("~/Eneye/Portfolio/water-olympics-EDA/Fina_Olympics_Data/Fina-Seoul-1988-Olympics-Athletes-Clean.csv")
barcelona_1992_olympics_athletes <- read.csv("~/Eneye/Portfolio/water-olympics-EDA/Fina_Olympics_Data/Fina-Barcelona-1992-Olympics-Athletes-Clean.csv")
atlanta_1996_olympics_athletes <- read.csv("~/Eneye/Portfolio/water-olympics-EDA/Fina_Olympics_Data/Fina-Atlanta-1996-Olympics-Athletes-Clean.csv")
sydney_2000_olympics_athletes <- read.csv("~/Eneye/Portfolio/water-olympics-EDA/Fina_Olympics_Data/Fina-Sydney-2000-Olympics-Athletes-Clean.csv")
athens_2004_olympics_athletes <- read.csv("~/Eneye/Portfolio/water-olympics-EDA/Fina_Olympics_Data/Fina-Athens-2004-Olympics-Athletes-Clean.csv")
beijing_2008_olympics_athletes <- read.csv("~/Eneye/Portfolio/water-olympics-EDA/Fina_Olympics_Data/Fina-Beijing-2008-Olympics-Athletes-Clean.csv")
london_2012_olympics_athletes <- read.csv("~/Eneye/Portfolio/water-olympics-EDA/Fina_Olympics_Data/Fina-London-2012-Olympics-Athletes-Clean.csv")
rio_2016_olympics_athletes <- read.csv("~/Eneye/Portfolio/water-olympics-EDA/Fina_Olympics_Data/Fina-Rio-2016-Olympics-Athletes-Clean.csv")
tokyo_2020_olympics_athletes <- read.csv("~/Eneye/Portfolio/water-olympics-EDA/Fina_Olympics_Data/Fina-Tokyo-2020-Olympics-Athletes-Clean.csv")
```

``` r
### Load Medals Data

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

``` r
### COnvert DOB from CHR to Date

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

``` r
### Insert Olympic date column

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

``` r
### Calculate athletes age during olympics in new column

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

``` r
### Merge All olympic records

all_olympics <- bind_rows(seoul_1988_olympics_athletes, barcelona_1992_olympics_athletes, atlanta_1996_olympics_athletes, sydney_2000_olympics_athletes, athens_2004_olympics_athletes, beijing_2008_olympics_athletes, london_2012_olympics_athletes, rio_2016_olympics_athletes, tokyo_2020_olympics_athletes)
```

``` r
### Summary and Visualizations

summary(all_olympics$age)
```

    ##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    ##   -6.00   20.00   22.00   22.67   25.00   42.00

``` r
setNames(aggregate(all_olympics$age ~ all_olympics$Discipline + all_olympics$Gender + all_olympics$NOC, FUN = min), c("Discipline", "Gender", "NOC", "age"))
```

    ##                Discipline Gender                              NOC age
    ## 1                Swimming   Male                      Afghanistan  22
    ## 2                Swimming Female                          Albania  16
    ## 3                Swimming   Male                          Albania  16
    ## 4              Open Water Female                          Algeria  32
    ## 5                Swimming Female                          Algeria  19
    ## 6                Swimming   Male                          Algeria  19
    ## 7                Swimming Female                   American Samoa  19
    ## 8                Swimming   Male                   American Samoa  19
    ## 9                Swimming Female                          Andorra  15
    ## 10               Swimming   Male                          Andorra  18
    ## 11               Swimming Female                           Angola  13
    ## 12               Swimming   Male                           Angola  16
    ## 13               Swimming Female              Antigua and Barbuda  14
    ## 14               Swimming   Male              Antigua and Barbuda  15
    ## 15      Artistic Swimming Female                        Argentina  22
    ## 16                 Diving Female                        Argentina  21
    ## 17             Open Water Female                        Argentina  16
    ## 18               Swimming Female                        Argentina  15
    ## 19  Swimming - Open Water Female                        Argentina  27
    ## 20             Open Water   Male                        Argentina  27
    ## 21               Swimming   Male                        Argentina  17
    ## 22                 Diving Female                          Armenia  17
    ## 23               Swimming Female                          Armenia  18
    ## 24                 Diving   Male                          Armenia  18
    ## 25               Swimming   Male                          Armenia  19
    ## 26      Artistic Swimming Female                            Aruba  17
    ## 27               Swimming Female                            Aruba  15
    ## 28               Swimming   Male                            Aruba  17
    ## 29      Artistic Swimming Female                        Australia  17
    ## 30                 Diving Female                        Australia  16
    ## 31             Open Water Female                        Australia  17
    ## 32               Swimming Female                        Australia  15
    ## 33  Swimming - Open Water Female                        Australia  22
    ## 34             Water Polo Female                        Australia  19
    ## 35                 Diving   Male                        Australia  17
    ## 36             Open Water   Male                        Australia  21
    ## 37               Swimming   Male                        Australia  17
    ## 38             Water Polo   Male                        Australia  19
    ## 39      Artistic Swimming Female                          Austria  17
    ## 40                 Diving Female                          Austria  18
    ## 41               Swimming Female                          Austria  16
    ## 42                 Diving   Male                          Austria  20
    ## 43               Swimming   Male                          Austria  18
    ## 44               Swimming Female                       Azerbaijan  14
    ## 45                 Diving   Male                       Azerbaijan  18
    ## 46               Swimming   Male                       Azerbaijan  18
    ## 47                 Diving Female                          Bahamas  20
    ## 48               Swimming Female                          Bahamas  18
    ## 49               Swimming   Male                          Bahamas  18
    ## 50               Swimming Female                          Bahrain  12
    ## 51               Swimming   Male                          Bahrain  15
    ## 52               Swimming Female                       Bangladesh  14
    ## 53               Swimming   Male                       Bangladesh  19
    ## 54               Swimming Female                         Barbados  18
    ## 55                 Diving   Male                         Barbados  26
    ## 56               Swimming   Male                         Barbados  17
    ## 57      Artistic Swimming Female                          Belarus  18
    ## 58                 Diving Female                          Belarus  25
    ## 59               Swimming Female                          Belarus  16
    ## 60                 Diving   Male                          Belarus  21
    ## 61               Swimming   Male                          Belarus  18
    ## 62      Artistic Swimming Female                          Belgium  23
    ## 63               Swimming Female                          Belgium  15
    ## 64                 Diving   Male                          Belgium  26
    ## 65             Open Water   Male                          Belgium  24
    ## 66               Swimming   Male                          Belgium  18
    ## 67               Swimming Female                            Benin  15
    ## 68               Swimming   Male                            Benin  22
    ## 69                 Diving Female                          Bermuda  21
    ## 70               Swimming Female                          Bermuda  17
    ## 71               Swimming   Male                          Bermuda  17
    ## 72               Swimming   Male                           Bhutan  17
    ## 73               Swimming Female                          Bolivia  14
    ## 74                 Diving   Male                          Bolivia  23
    ## 75               Swimming   Male                          Bolivia  18
    ## 76               Swimming Female           Bosnia and Herzegovina  15
    ## 77               Swimming   Male           Bosnia and Herzegovina  17
    ## 78               Swimming Female                         Botswana  19
    ## 79               Swimming   Male                         Botswana  19
    ## 80      Artistic Swimming Female                           Brazil  17
    ## 81                 Diving Female                           Brazil  17
    ## 82             Open Water Female                           Brazil  16
    ## 83               Swimming Female                           Brazil  16
    ## 84             Water Polo Female                           Brazil  19
    ## 85                 Diving   Male                           Brazil  19
    ## 86             Open Water   Male                           Brazil  19
    ## 87               Swimming   Male                           Brazil  17
    ## 88             Water Polo   Male                           Brazil  22
    ## 89               Swimming Female           British Virgin Islands  16
    ## 90               Swimming   Male                           Brunei  16
    ## 91      Artistic Swimming Female                         Bulgaria  22
    ## 92                 Diving Female                         Bulgaria  20
    ## 93               Swimming Female                         Bulgaria  16
    ## 94                 Diving   Male                         Bulgaria  20
    ## 95             Open Water   Male                         Bulgaria  25
    ## 96               Swimming   Male                         Bulgaria  18
    ## 97  Swimming - Open Water   Male                         Bulgaria  31
    ## 98               Swimming Female                     Burkina Faso  18
    ## 99               Swimming   Male                     Burkina Faso  21
    ## 100              Swimming Female                          Burundi  19
    ## 101              Swimming   Male                          Burundi  19
    ## 102              Swimming Female                         Cambodia  12
    ## 103              Swimming   Male                         Cambodia  18
    ## 104              Swimming Female                         Cameroon  12
    ## 105              Swimming   Male                         Cameroon  21
    ## 106     Artistic Swimming Female                           Canada  16
    ## 107                Diving Female                           Canada  16
    ## 108            Open Water Female                           Canada  21
    ## 109              Swimming Female                           Canada  14
    ## 110            Water Polo Female                           Canada  19
    ## 111                Diving   Male                           Canada  15
    ## 112            Open Water   Male                           Canada  22
    ## 113              Swimming   Male                           Canada  17
    ## 114            Water Polo   Male                           Canada  19
    ## 115              Swimming Female                       Cape Verde  16
    ## 116              Swimming   Male                       Cape Verde  22
    ## 117              Swimming Female                   Cayman Islands  15
    ## 118              Swimming   Male                   Cayman Islands  16
    ## 119              Swimming Female         Central African Republic  16
    ## 120              Swimming   Male         Central African Republic  18
    ## 121              Swimming Female                            Chile  19
    ## 122 Swimming - Open Water Female                            Chile  23
    ## 123              Swimming   Male                            Chile  17
    ## 124     Artistic Swimming Female                            China  16
    ## 125                Diving Female                            China  13
    ## 126            Open Water Female                            China  19
    ## 127              Swimming Female                            China  13
    ## 128            Water Polo Female                            China  17
    ## 129                Diving   Male                            China  14
    ## 130            Open Water   Male                            China  21
    ## 131              Swimming   Male                            China  16
    ## 132            Water Polo   Male                            China  19
    ## 133                Diving Female                   Chinese Taipei  15
    ## 134              Swimming Female                   Chinese Taipei  15
    ## 135                Diving   Male                   Chinese Taipei  18
    ## 136              Swimming   Male                   Chinese Taipei  15
    ## 137     Artistic Swimming Female                         Colombia  21
    ## 138                Diving Female                         Colombia  16
    ## 139              Swimming Female                         Colombia  16
    ## 140                Diving   Male                         Colombia  17
    ## 141              Swimming   Male                         Colombia  15
    ## 142              Swimming Female                          Comoros  17
    ## 143              Swimming   Male                          Comoros  25
    ## 144              Swimming Female                     Cook Islands  17
    ## 145              Swimming   Male                     Cook Islands  18
    ## 146                Diving Female                       Costa Rica  20
    ## 147              Swimming Female                       Costa Rica  16
    ## 148              Swimming   Male                       Costa Rica  18
    ## 149                Diving Female                          Croatia  19
    ## 150            Open Water Female                          Croatia  20
    ## 151              Swimming Female                          Croatia  16
    ## 152              Swimming   Male                          Croatia  17
    ## 153            Water Polo   Male                          Croatia  20
    ## 154     Artistic Swimming Female                             Cuba  19
    ## 155                Diving Female                             Cuba  19
    ## 156              Swimming Female                             Cuba  17
    ## 157                Diving   Male                             Cuba  18
    ## 158              Swimming   Male                             Cuba  16
    ## 159            Water Polo   Male                             Cuba  21
    ## 160              Swimming Female                           Cyprus  14
    ## 161              Swimming   Male                           Cyprus  17
    ## 162     Artistic Swimming Female                   Czech Republic  18
    ## 163            Open Water Female                   Czech Republic  27
    ## 164              Swimming Female                   Czech Republic  16
    ## 165                Diving   Male                   Czech Republic  24
    ## 166            Open Water   Male                   Czech Republic  25
    ## 167              Swimming   Male                   Czech Republic  17
    ## 168     Artistic Swimming Female                   Czechoslovakia  17
    ## 169                Diving Female                   Czechoslovakia  27
    ## 170              Swimming Female                   Czechoslovakia  16
    ## 171              Swimming   Male                   Czechoslovakia  17
    ## 172            Water Polo   Male                   Czechoslovakia  18
    ## 173              Swimming   Male Democratic Republic of the Congo  34
    ## 174              Swimming Female                          Denmark  15
    ## 175              Swimming   Male                          Denmark  17
    ## 176              Swimming   Male                         Djibouti  18
    ## 177              Swimming Female                         Dominica  25
    ## 178              Swimming   Male                         Dominica  20
    ## 179              Swimming Female               Dominican Republic  15
    ## 180                Diving   Male               Dominican Republic  30
    ## 181              Swimming   Male               Dominican Republic  18
    ## 182              Swimming Female                       East Timor  22
    ## 183              Swimming   Male                       East Timor  17
    ## 184            Open Water Female                          Ecuador  21
    ## 185              Swimming Female                          Ecuador  16
    ## 186                Diving   Male                          Ecuador  20
    ## 187            Open Water   Male                          Ecuador  20
    ## 188              Swimming   Male                          Ecuador  19
    ## 189     Artistic Swimming Female                            Egypt  15
    ## 190                Diving Female                            Egypt  17
    ## 191            Open Water Female                            Egypt  20
    ## 192              Swimming Female                            Egypt  14
    ## 193                Diving   Male                            Egypt  18
    ## 194            Open Water   Male                            Egypt  21
    ## 195              Swimming   Male                            Egypt   5
    ## 196            Water Polo   Male                            Egypt  21
    ## 197              Swimming Female                      El Salvador  15
    ## 198              Swimming   Male                      El Salvador  17
    ## 199              Swimming Female                Equatorial Guinea  20
    ## 200              Swimming   Male                Equatorial Guinea  22
    ## 201              Swimming   Male                          Eritrea  25
    ## 202              Swimming Female                          Estonia  14
    ## 203              Swimming   Male                          Estonia  19
    ## 204              Swimming Female                         Eswatini  15
    ## 205              Swimming   Male                         Eswatini  17
    ## 206              Swimming Female                         Ethiopia  18
    ## 207              Swimming   Male                         Ethiopia  24
    ## 208              Swimming   Male                    Faroe Islands  25
    ## 209              Swimming Female   Federated States of Micronesia  15
    ## 210              Swimming   Male   Federated States of Micronesia  19
    ## 211              Swimming Female                             Fiji  14
    ## 212              Swimming   Male                             Fiji  16
    ## 213     Artistic Swimming Female                          Finland  18
    ## 214              Swimming Female                          Finland  15
    ## 215                Diving   Male                          Finland  18
    ## 216              Swimming   Male                          Finland  17
    ## 217     Artistic Swimming Female                           France  17
    ## 218                Diving Female                           France  18
    ## 219            Open Water Female                           France  18
    ## 220              Swimming Female                           France  15
    ## 221                Diving   Male                           France  19
    ## 222            Open Water   Male                           France  20
    ## 223              Swimming   Male                           France  16
    ## 224 Swimming - Open Water   Male                           France  24
    ## 225            Water Polo   Male                           France  21
    ## 226              Swimming Female                            Gabon  17
    ## 227              Swimming   Male                            Gabon  18
    ## 228                Diving Female                          Georgia  16
    ## 229              Swimming Female                          Georgia  18
    ## 230                Diving   Male                          Georgia  22
    ## 231              Swimming   Male                          Georgia  17
    ## 232     Artistic Swimming Female                          Germany  20
    ## 233                Diving Female                          Germany  15
    ## 234            Open Water Female                          Germany  24
    ## 235              Swimming Female                          Germany  14
    ## 236                Diving   Male                          Germany  16
    ## 237            Open Water   Male                          Germany  25
    ## 238              Swimming   Male                          Germany  17
    ## 239 Swimming - Open Water   Male                          Germany  23
    ## 240            Water Polo   Male                          Germany  18
    ## 241              Swimming Female                            Ghana  14
    ## 242              Swimming   Male                            Ghana  16
    ## 243     Artistic Swimming Female                    Great Britain  18
    ## 244                Diving Female                    Great Britain  15
    ## 245            Open Water Female                    Great Britain  24
    ## 246              Swimming Female                    Great Britain  15
    ## 247 Swimming - Open Water Female                    Great Britain  20
    ## 248            Water Polo Female                    Great Britain  19
    ## 249                Diving   Male                    Great Britain  14
    ## 250            Open Water   Male                    Great Britain  20
    ## 251              Swimming   Male                    Great Britain  16
    ## 252 Swimming - Open Water   Male                    Great Britain  23
    ## 253            Water Polo   Male                    Great Britain  21
    ## 254     Artistic Swimming Female                           Greece  17
    ## 255                Diving Female                           Greece  17
    ## 256            Open Water Female                           Greece  25
    ## 257              Swimming Female                           Greece  15
    ## 258            Water Polo Female                           Greece  17
    ## 259                Diving   Male                           Greece  17
    ## 260            Open Water   Male                           Greece  22
    ## 261              Swimming   Male                           Greece  16
    ## 262 Swimming - Open Water   Male                           Greece  28
    ## 263            Water Polo   Male                           Greece  19
    ## 264              Swimming Female                          Grenada  16
    ## 265              Swimming   Male                          Grenada  18
    ## 266              Swimming Female                             Guam  15
    ## 267            Open Water   Male                             Guam  16
    ## 268              Swimming   Male                             Guam  16
    ## 269              Swimming Female                        Guatemala  16
    ## 270              Swimming   Male                        Guatemala  17
    ## 271              Swimming Female                           Guinea  19
    ## 272              Swimming   Male                           Guinea  22
    ## 273              Swimming Female                           Guyana  15
    ## 274              Swimming   Male                           Guyana  17
    ## 275              Swimming Female                            Haiti  19
    ## 276              Swimming   Male                            Haiti  19
    ## 277              Swimming Female                         Honduras  16
    ## 278              Swimming   Male                         Honduras  17
    ## 279            Open Water Female                 Hong Kong, China  19
    ## 280              Swimming Female                 Hong Kong, China  13
    ## 281                Diving   Male                 Hong Kong, China  15
    ## 282            Open Water   Male                 Hong Kong, China  18
    ## 283              Swimming   Male                 Hong Kong, China  16
    ## 284     Artistic Swimming Female                          Hungary  17
    ## 285                Diving Female                          Hungary  16
    ## 286            Open Water Female                          Hungary  22
    ## 287              Swimming Female                          Hungary  12
    ## 288 Swimming - Open Water Female                          Hungary  26
    ## 289            Water Polo Female                          Hungary  18
    ## 290                Diving   Male                          Hungary  18
    ## 291            Open Water   Male                          Hungary  19
    ## 292              Swimming   Male                          Hungary   9
    ## 293            Water Polo   Male                          Hungary  19
    ## 294              Swimming Female                          Iceland  16
    ## 295              Swimming   Male                          Iceland  17
    ## 296     Artistic Swimming Female Independent Olympic Participants  21
    ## 297              Swimming Female Independent Olympic Participants  20
    ## 298              Swimming   Male Independent Olympic Participants  19
    ## 299              Swimming Female                            India  16
    ## 300              Swimming   Male                            India  16
    ## 301                Diving Female                        Indonesia  16
    ## 302              Swimming Female                        Indonesia  14
    ## 303                Diving   Male                        Indonesia  18
    ## 304              Swimming   Male                        Indonesia  16
    ## 305              Swimming   Male                             Iran  16
    ## 306              Swimming Female                             Iraq  21
    ## 307              Swimming   Male                             Iraq  15
    ## 308                Diving Female                          Ireland  19
    ## 309              Swimming Female                          Ireland  17
    ## 310                Diving   Male                          Ireland  23
    ## 311              Swimming   Male                          Ireland  17
    ## 312     Artistic Swimming Female                           Israel  16
    ## 313              Swimming Female                           Israel  15
    ## 314            Open Water   Male                           Israel  22
    ## 315              Swimming   Male                           Israel  19
    ## 316     Artistic Swimming Female                            Italy  18
    ## 317                Diving Female                            Italy  15
    ## 318            Open Water Female                            Italy  19
    ## 319              Swimming Female                            Italy  15
    ## 320            Water Polo Female                            Italy  19
    ## 321                Diving   Male                            Italy  17
    ## 322            Open Water   Male                            Italy  25
    ## 323              Swimming   Male                            Italy  -6
    ## 324 Swimming - Open Water   Male                            Italy  26
    ## 325            Water Polo   Male                            Italy  20
    ## 326              Swimming Female                      Ivory Coast  16
    ## 327              Swimming   Male                      Ivory Coast  16
    ## 328              Swimming Female                          Jamaica  15
    ## 329                Diving   Male                          Jamaica  21
    ## 330              Swimming   Male                          Jamaica  20
    ## 331     Artistic Swimming Female                            Japan  18
    ## 332                Diving Female                            Japan  16
    ## 333            Open Water Female                            Japan  27
    ## 334              Swimming Female                            Japan  -2
    ## 335            Water Polo Female                            Japan  18
    ## 336                Diving   Male                            Japan  14
    ## 337            Open Water   Male                            Japan  22
    ## 338              Swimming   Male                            Japan  16
    ## 339            Water Polo   Male                            Japan  21
    ## 340              Swimming Female                           Jordan  13
    ## 341              Swimming   Male                           Jordan  15
    ## 342     Artistic Swimming Female                       Kazakhstan  18
    ## 343                Diving Female                       Kazakhstan  20
    ## 344              Swimming Female                       Kazakhstan  13
    ## 345            Water Polo Female                       Kazakhstan  20
    ## 346                Diving   Male                       Kazakhstan  20
    ## 347            Open Water   Male                       Kazakhstan  21
    ## 348              Swimming   Male                       Kazakhstan  17
    ## 349            Water Polo   Male                       Kazakhstan  18
    ## 350              Swimming Female                            Kenya  14
    ## 351              Swimming   Male                            Kenya  17
    ## 352              Swimming Female                           Kosovo  16
    ## 353              Swimming   Male                           Kosovo  18
    ## 354              Swimming Female                           Kuwait  17
    ## 355                Diving   Male                           Kuwait  18
    ## 356              Swimming   Male                           Kuwait  16
    ## 357              Swimming Female                       Kyrgyzstan  15
    ## 358              Swimming   Male                       Kyrgyzstan  14
    ## 359              Swimming Female                             Laos  14
    ## 360              Swimming   Male                             Laos  15
    ## 361              Swimming Female                           Latvia  15
    ## 362              Swimming   Male                           Latvia  18
    ## 363              Swimming Female                          Lebanon  14
    ## 364              Swimming   Male                          Lebanon  13
    ## 365              Swimming Female                          Lesotho  25
    ## 366              Swimming Female                            Libya  17
    ## 367              Swimming   Male                            Libya  16
    ## 368     Artistic Swimming Female                    Liechtenstein  21
    ## 369              Swimming Female                    Liechtenstein  19
    ## 370              Swimming   Male                    Liechtenstein  23
    ## 371              Swimming Female                        Lithuania  15
    ## 372              Swimming   Male                        Lithuania  16
    ## 373              Swimming Female                       Luxembourg  18
    ## 374              Swimming   Male                       Luxembourg  16
    ## 375              Swimming Female                       Madagascar  13
    ## 376              Swimming   Male                       Madagascar  20
    ## 377              Swimming Female                           Malawi  14
    ## 378              Swimming   Male                           Malawi  19
    ## 379                Diving Female                         Malaysia  14
    ## 380            Open Water Female                         Malaysia  23
    ## 381              Swimming Female                         Malaysia  14
    ## 382                Diving   Male                         Malaysia  14
    ## 383              Swimming   Male                         Malaysia  15
    ## 384              Swimming Female                         Maldives  13
    ## 385              Swimming   Male                         Maldives  16
    ## 386              Swimming Female                             Mali  17
    ## 387              Swimming   Male                             Mali  18
    ## 388              Swimming Female                            Malta  16
    ## 389              Swimming   Male                            Malta  18
    ## 390              Swimming Female                 Marshall Islands  16
    ## 391              Swimming   Male                 Marshall Islands  19
    ## 392              Swimming Female                        Mauritius  15
    ## 393              Swimming   Male                        Mauritius  16
    ## 394     Artistic Swimming Female                           Mexico  14
    ## 395                Diving Female                           Mexico  15
    ## 396            Open Water Female                           Mexico  18
    ## 397              Swimming Female                           Mexico  17
    ## 398                Diving   Male                           Mexico  16
    ## 399            Open Water   Male                           Mexico  23
    ## 400              Swimming   Male                           Mexico  17
    ## 401              Swimming Female                          Moldova  16
    ## 402              Swimming   Male                          Moldova  16
    ## 403              Swimming Female                           Monaco  19
    ## 404              Swimming   Male                           Monaco  16
    ## 405              Swimming Female                         Mongolia  16
    ## 406              Swimming   Male                         Mongolia  17
    ## 407              Swimming Female                       Montenegro  17
    ## 408              Swimming   Male                       Montenegro  20
    ## 409            Water Polo   Male                       Montenegro  20
    ## 410              Swimming Female                          Morocco  18
    ## 411              Swimming   Male                          Morocco  18
    ## 412              Swimming Female                       Mozambique  15
    ## 413              Swimming   Male                       Mozambique  15
    ## 414              Swimming Female                          Myanmar  19
    ## 415              Swimming   Male                          Myanmar  14
    ## 416              Swimming Female                          Namibia  17
    ## 417            Open Water   Male                          Namibia  23
    ## 418              Swimming   Male                          Namibia  23
    ## 419              Swimming Female                            Nepal  13
    ## 420              Swimming   Male                            Nepal  17
    ## 421     Artistic Swimming Female                      Netherlands  17
    ## 422                Diving Female                      Netherlands  23
    ## 423            Open Water Female                      Netherlands  35
    ## 424              Swimming Female                      Netherlands  15
    ## 425 Swimming - Open Water Female                      Netherlands  22
    ## 426            Water Polo Female                      Netherlands  19
    ## 427                Diving   Male                      Netherlands  21
    ## 428            Open Water   Male                      Netherlands  24
    ## 429              Swimming   Male                      Netherlands  18
    ## 430            Water Polo   Male                      Netherlands  18
    ## 431              Swimming   Male             Netherlands Antilles  18
    ## 432     Artistic Swimming Female                      New Zealand  23
    ## 433                Diving Female                      New Zealand  18
    ## 434              Swimming Female                      New Zealand  15
    ## 435                Diving   Male                      New Zealand  21
    ## 436            Open Water   Male                      New Zealand  25
    ## 437              Swimming   Male                      New Zealand  17
    ## 438              Swimming Female                        Nicaragua  16
    ## 439              Swimming   Male                        Nicaragua  16
    ## 440              Swimming Female                            Niger  14
    ## 441              Swimming   Male                            Niger  16
    ## 442              Swimming Female                          Nigeria  17
    ## 443              Swimming   Male                          Nigeria  21
    ## 444     Artistic Swimming Female                      North Korea  17
    ## 445                Diving Female                      North Korea  15
    ## 446                Diving   Male                      North Korea  16
    ## 447              Swimming Female                  North Macedonia  15
    ## 448              Swimming   Male                  North Macedonia  17
    ## 449                Diving Female                           Norway  19
    ## 450              Swimming Female                           Norway  17
    ## 451                Diving   Male                           Norway  21
    ## 452              Swimming   Male                           Norway  19
    ## 453              Swimming   Male                             Oman  14
    ## 454              Swimming Female                         Pakistan  13
    ## 455              Swimming   Male                         Pakistan  17
    ## 456              Swimming Female                            Palau  15
    ## 457              Swimming   Male                            Palau  19
    ## 458              Swimming Female                        Palestine  17
    ## 459              Swimming   Male                        Palestine  17
    ## 460              Swimming Female                           Panama  15
    ## 461              Swimming   Male                           Panama  19
    ## 462              Swimming Female                 Papua New Guinea  17
    ## 463              Swimming   Male                 Papua New Guinea  15
    ## 464              Swimming Female                         Paraguay  16
    ## 465              Swimming   Male                         Paraguay  17
    ## 466              Swimming Female                             Peru  16
    ## 467                Diving   Male                             Peru  28
    ## 468              Swimming   Male                             Peru  18
    ## 469                Diving Female                      Philippines  14
    ## 470              Swimming Female                      Philippines  13
    ## 471                Diving   Male                      Philippines  16
    ## 472              Swimming   Male                      Philippines  15
    ## 473            Open Water Female                           Poland  19
    ## 474              Swimming Female                           Poland  15
    ## 475                Diving   Male                           Poland  16
    ## 476              Swimming   Male                           Poland  17
    ## 477            Open Water Female                         Portugal  19
    ## 478              Swimming Female                         Portugal  15
    ## 479            Open Water   Male                         Portugal  22
    ## 480              Swimming   Male                         Portugal  17
    ## 481     Artistic Swimming Female                      Puerto Rico  22
    ## 482                Diving Female                      Puerto Rico  23
    ## 483              Swimming Female                      Puerto Rico  16
    ## 484                Diving   Male                      Puerto Rico  22
    ## 485              Swimming   Male                      Puerto Rico  17
    ## 486              Swimming Female                            Qatar  17
    ## 487              Swimming   Male                            Qatar  14
    ## 488              Swimming Female             Refugee Olympic Team  23
    ## 489              Swimming   Male             Refugee Olympic Team  21
    ## 490              Swimming Female            Republic of the Congo  17
    ## 491              Swimming   Male            Republic of the Congo  16
    ## 492                Diving Female                          Romania  13
    ## 493              Swimming Female                          Romania  13
    ## 494                Diving   Male                          Romania  14
    ## 495              Swimming   Male                          Romania  16
    ## 496            Water Polo   Male                          Romania  19
    ## 497     Artistic Swimming Female                           Russia  17
    ## 498                Diving Female                           Russia  15
    ## 499            Open Water Female                           Russia  19
    ## 500              Swimming Female                           Russia  15
    ## 501 Swimming - Open Water Female                           Russia  21
    ## 502            Water Polo Female                           Russia  17
    ## 503                Diving   Male                           Russia  18
    ## 504            Open Water   Male                           Russia  24
    ## 505              Swimming   Male                           Russia   1
    ## 506            Water Polo   Male                           Russia  19
    ## 507              Swimming Female                           Rwanda  14
    ## 508              Swimming   Male                           Rwanda  20
    ## 509              Swimming Female                      Saint Lucia  17
    ## 510              Swimming   Male                      Saint Lucia  18
    ## 511              Swimming Female Saint Vincent and the Grenadines  15
    ## 512              Swimming   Male Saint Vincent and the Grenadines  16
    ## 513              Swimming Female                            Samoa  17
    ## 514              Swimming   Male                            Samoa  18
    ## 515              Swimming Female                       San Marino  16
    ## 516              Swimming   Male                       San Marino  16
    ## 517              Swimming   Male                     Saudi Arabia  19
    ## 518              Swimming Female                          Senegal  16
    ## 519              Swimming   Male                          Senegal  14
    ## 520              Swimming Female                           Serbia  16
    ## 521              Swimming   Male                           Serbia  17
    ## 522            Water Polo   Male                           Serbia  18
    ## 523              Swimming Female            Serbia and Montenegro  15
    ## 524                Diving   Male            Serbia and Montenegro  23
    ## 525              Swimming   Male            Serbia and Montenegro  17
    ## 526            Water Polo   Male            Serbia and Montenegro  18
    ## 527              Swimming Female                       Seychelles  14
    ## 528              Swimming   Male                       Seychelles  13
    ## 529              Swimming Female                     Sierra Leone  18
    ## 530              Swimming   Male                     Sierra Leone  20
    ## 531                Diving Female                        Singapore  23
    ## 532            Open Water Female                        Singapore  22
    ## 533              Swimming Female                        Singapore  13
    ## 534                Diving   Male                        Singapore  24
    ## 535              Swimming   Male                        Singapore  10
    ## 536     Artistic Swimming Female                         Slovakia  19
    ## 537              Swimming Female                         Slovakia  19
    ## 538              Swimming   Male                         Slovakia  20
    ## 539 Swimming - Open Water   Male                         Slovakia  23
    ## 540            Water Polo   Male                         Slovakia  17
    ## 541            Open Water Female                         Slovenia  17
    ## 542              Swimming Female                         Slovenia  15
    ## 543              Swimming   Male                         Slovenia  18
    ## 544              Swimming   Male                  Solomon Islands  20
    ## 545     Artistic Swimming Female                     South Africa  19
    ## 546                Diving Female                     South Africa  18
    ## 547            Open Water Female                     South Africa  19
    ## 548              Swimming Female                     South Africa  17
    ## 549            Water Polo Female                     South Africa  18
    ## 550                Diving   Male                     South Africa  28
    ## 551            Open Water   Male                     South Africa  18
    ## 552              Swimming   Male                     South Africa  17
    ## 553            Water Polo   Male                     South Africa  21
    ## 554     Artistic Swimming Female                      South Korea  16
    ## 555                Diving Female                      South Korea  14
    ## 556              Swimming Female                      South Korea  13
    ## 557                Diving   Male                      South Korea  14
    ## 558              Swimming   Male                      South Korea   0
    ## 559            Water Polo   Male                      South Korea  18
    ## 560     Artistic Swimming Female                     Soviet Union  18
    ## 561                Diving Female                     Soviet Union  14
    ## 562              Swimming Female                     Soviet Union  17
    ## 563                Diving   Male                     Soviet Union  18
    ## 564              Swimming   Male                     Soviet Union  16
    ## 565            Water Polo   Male                     Soviet Union  21
    ## 566     Artistic Swimming Female                            Spain  18
    ## 567                Diving Female                            Spain  17
    ## 568            Open Water Female                            Spain  22
    ## 569              Swimming Female                            Spain  14
    ## 570 Swimming - Open Water Female                            Spain  28
    ## 571            Water Polo Female                            Spain  16
    ## 572                Diving   Male                            Spain  17
    ## 573            Open Water   Male                            Spain  23
    ## 574              Swimming   Male                            Spain  17
    ## 575            Water Polo   Male                            Spain  19
    ## 576              Swimming Female                        Sri Lanka  16
    ## 577                Diving   Male                        Sri Lanka  31
    ## 578              Swimming   Male                        Sri Lanka  18
    ## 579              Swimming Female                            Sudan  16
    ## 580              Swimming   Male                            Sudan  19
    ## 581              Swimming Female                         Suriname  15
    ## 582              Swimming   Male                         Suriname  17
    ## 583     Artistic Swimming Female                           Sweden  23
    ## 584                Diving Female                           Sweden  14
    ## 585            Open Water Female                           Sweden  24
    ## 586              Swimming Female                           Sweden  14
    ## 587                Diving   Male                           Sweden  17
    ## 588              Swimming   Male                           Sweden  18
    ## 589     Artistic Swimming Female                      Switzerland  17
    ## 590                Diving Female                      Switzerland  19
    ## 591            Open Water Female                      Switzerland  22
    ## 592              Swimming Female                      Switzerland  15
    ## 593                Diving   Male                      Switzerland  19
    ## 594              Swimming   Male                      Switzerland  18
    ## 595              Swimming Female                            Syria  18
    ## 596            Open Water   Male                            Syria  22
    ## 597              Swimming   Male                            Syria  17
    ## 598                Diving Female                       Tajikistan  18
    ## 599              Swimming Female                       Tajikistan  14
    ## 600                Diving   Male                       Tajikistan  17
    ## 601              Swimming   Male                       Tajikistan  16
    ## 602              Swimming Female                         Tanzania  17
    ## 603              Swimming   Male                         Tanzania  15
    ## 604                Diving Female                         Thailand  14
    ## 605              Swimming Female                         Thailand  14
    ## 606                Diving   Male                         Thailand  17
    ## 607              Swimming   Male                         Thailand  16
    ## 608              Swimming   Male                       The Gambia  19
    ## 609              Swimming Female                             Togo  13
    ## 610              Swimming   Male                             Togo  17
    ## 611              Swimming Female                            Tonga  18
    ## 612              Swimming   Male                            Tonga  22
    ## 613              Swimming Female              Trinidad and Tobago  13
    ## 614              Swimming   Male              Trinidad and Tobago  17
    ## 615              Swimming Female                          Tunisia  21
    ## 616            Open Water   Male                          Tunisia  37
    ## 617              Swimming   Male                          Tunisia  16
    ## 618 Swimming - Open Water   Male                          Tunisia  28
    ## 619              Swimming Female                           Turkey  15
    ## 620              Swimming   Male                           Turkey  14
    ## 621              Swimming Female                     Turkmenistan  14
    ## 622              Swimming   Male                     Turkmenistan  18
    ## 623              Swimming Female                           Uganda  15
    ## 624              Swimming   Male                           Uganda  19
    ## 625     Artistic Swimming Female                          Ukraine  19
    ## 626                Diving Female                          Ukraine  16
    ## 627            Open Water Female                          Ukraine  23
    ## 628              Swimming Female                          Ukraine  14
    ## 629                Diving   Male                          Ukraine  15
    ## 630            Open Water   Male                          Ukraine  26
    ## 631              Swimming   Male                          Ukraine  16
    ## 632            Water Polo   Male                          Ukraine  21
    ## 633     Artistic Swimming Female                     Unified Team  19
    ## 634                Diving Female                     Unified Team  18
    ## 635              Swimming Female                     Unified Team  15
    ## 636                Diving   Male                     Unified Team  18
    ## 637              Swimming   Male                     Unified Team  18
    ## 638            Water Polo   Male                     Unified Team  20
    ## 639              Swimming Female             United Arab Emirates  18
    ## 640              Swimming   Male             United Arab Emirates  15
    ## 641     Artistic Swimming Female                    United States  19
    ## 642                Diving Female                    United States  15
    ## 643            Open Water Female                    United States  16
    ## 644              Swimming Female                    United States  14
    ## 645            Water Polo Female                    United States  17
    ## 646                Diving   Male                    United States  18
    ## 647            Open Water   Male                    United States  23
    ## 648              Swimming   Male                    United States  15
    ## 649 Swimming - Open Water   Male                    United States  22
    ## 650            Water Polo   Male                    United States  18
    ## 651                Diving Female                          Uruguay  17
    ## 652              Swimming Female                          Uruguay  15
    ## 653              Swimming   Male                          Uruguay  18
    ## 654              Swimming Female                       Uzbekistan  14
    ## 655              Swimming   Male                       Uzbekistan  15
    ## 656     Artistic Swimming Female                        Venezuela  19
    ## 657                Diving Female                        Venezuela  16
    ## 658            Open Water Female                        Venezuela  23
    ## 659              Swimming Female                        Venezuela  19
    ## 660 Swimming - Open Water Female                        Venezuela  16
    ## 661                Diving   Male                        Venezuela  18
    ## 662            Open Water   Male                        Venezuela  25
    ## 663              Swimming   Male                        Venezuela  17
    ## 664              Swimming Female                          Vietnam  15
    ## 665              Swimming   Male                          Vietnam  15
    ## 666              Swimming Female                   Virgin Islands  15
    ## 667              Swimming   Male                   Virgin Islands  16
    ## 668              Swimming Female                            Yemen  16
    ## 669              Swimming   Male                            Yemen  23
    ## 670              Swimming Female                       Yugoslavia  16
    ## 671              Swimming   Male                       Yugoslavia  16
    ## 672            Water Polo   Male                       Yugoslavia  20
    ## 673              Swimming Female                           Zambia  16
    ## 674              Swimming   Male                           Zambia  17
    ## 675                Diving Female                         Zimbabwe  22
    ## 676              Swimming Female                         Zimbabwe  16
    ## 677                Diving   Male                         Zimbabwe  17
    ## 678              Swimming   Male                         Zimbabwe  16

``` r
all_olympics %>% 
  group_by(Discipline, Gender) %>% 
  summarise(Athlete = n()) %>% 
  arrange(desc(Athlete, NOC))
```

    ## `summarise()` has grouped output by 'Discipline'. You can override using the `.groups` argument.

    ## # A tibble: 11 x 3
    ## # Groups:   Discipline [6]
    ##    Discipline            Gender Athlete
    ##    <chr>                 <chr>    <int>
    ##  1 Swimming              Male      4245
    ##  2 Swimming              Female    3308
    ##  3 Water Polo            Male      1401
    ##  4 Artistic Swimming     Female     794
    ##  5 Water Polo            Female     624
    ##  6 Diving                Male       580
    ##  7 Diving                Female     573
    ##  8 Open Water            Male        90
    ##  9 Open Water            Female      88
    ## 10 Swimming - Open Water Female      12
    ## 11 Swimming - Open Water Male        11
