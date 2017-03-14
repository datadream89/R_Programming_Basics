##R Programming basics

#Evaluation
x<-1
x          # auto-printing
print(x)   # scripts , functions or longer programs


#basic objects- character, numeric, integer, complex, logical

char<-"We are learning R"
char

numeric<-1
numeric

integer<-1L
integer

complex<-(1+4i)**2
complex

infinitycal<-1/inf
infinitycal

Notanum<-0/0
Notanum

#Vectors

numeric_vector <- c(0.5, 0.6) ## numeric
numeric_vector

logical_vector<- c(TRUE, FALSE) ## logical
logical_vector

character_vector<- c("a", "b", "c") ## character
character_vector

integer_vector <- 9:29 ## integer
integer_vector

complex_vector<- c(1+0i, 2+4i) ## complex
complex_vector

vector_init<-vector("numeric", length = 10) ##vector initialization
vector_init

#coercion

implicit_coercion<-c("a",2)                #implicit
implicit_coercion

int<-1:6
class(int)
explicit_coercion<-as.numeric(int)         #explicit
explicit_coercion
class(explicit_coercion)

nonsense_coercion<-as.numeric(c("a","b","c"))    #nonsense
nonsense_coercion

#matrices

mat<-matrix(1:6, nrow = 2, ncol = 3)
dim(mat)

#attributes -metadata that describes the object
attributes(mat)

#naming the dimensions
dimnames(mat)<-list(c("a","b"),c("c","d","e"))
mat
colnames(mat)<-c("a","b","c")
rownames(mat)<-c("d","e")
mat

#rowbind and column bind
colrow1<-1:3
colrow2<-11:13

bindcol<-cbind(colrow1,colrow2)                     #bind columns
bindcol

bindrow<-rbind(colrow1,colrow2)                     #bind rows
bindrow

#lists- can contain elements of different classes

list1<-list(1,"a",TRUE,1+4i)
list1

list2<-vector("list",length=5)
list2

#Factors- used to represent categorical data- ordered or unordered

fact1<-factor(c("yes","yes","no","yes"), levels=c("yes","no"))
fact1
table(fact1)

#Missing values

missing<-c(1,2,NaN,NA,4)
is.na(missing)
is.nan(missing)

#Data Frames- every element(column) has the same length(rows)

dataframe<-data.frame("foo",1:2)
names(dataframe)<-c("character","integer")
row.names(dataframe)<-c("a","b")
dataframe

#accessing tables

conf_matrix<-table(c(1,2),c(2,3))
conf_matrix
conf_matrix[[1]]
conf_matrix[[2]]
conf_matrix[[3]]
conf_matrix[[4]]


##Tidy Data

#tidyverse includes ggplot2, magrittr, dplyr, tidyr, readr...

install.packages('tidyverse')
install.packages('psych')
library('tidyverse')
VADeaths

VADeaths %>%
  tbl_df() %>%
  mutate(age = row.names(VADeaths)) %>%
  gather(key, death_rate, -age) %>%
  separate(key, c("urban", "gender"), sep = " ") %>%
  mutate(age = factor(age), urban = factor(urban), gender = factor(gender))

#reading tabular data~readr

#datatypes
team_standings<-read_csv("C:/Users/Balan Gnanam/Desktop/team_standings.csv",col_types = "-ic",n_max=5)
team_standings

#first column only
teams2<-read_csv("C:/Users/Balan Gnanam/Desktop/team_standings.csv",col_types=cols_only(date = col_date()),n_max=5)
teams2

#Reading web based data

#1. Flat files online (extension (".csv", ".txt", or ".fwf"))

library(readr)
ext_tracks_file <- paste0("http://rammb.cira.colostate.edu/research/",
                          "tropical_cyclones/tc_extended_best_track_dataset/",
                          "data/ebtrk_atlc_1988_2015.txt")
ext_tracks_file

ext_tracks_colnames <- c("storm_id", "storm_name", "month", "day",
                         "hour", "year", "latitude", "longitude",
                         "max_wind", "min_pressure", "rad_max_wind",
                         "eye_diameter", "pressure_1", "pressure_2",
                         paste("radius_34", c("ne", "se", "sw", "nw"), sep = "_"),
                         paste("radius_50", c("ne", "se", "sw", "nw"), sep = "_"),
                         paste("radius_64", c("ne", "se", "sw", "nw"), sep = "_"),
                         "storm_type", "distance_to_land", "final")
ext_tracks_widths <- c(7, 10, 2, 2, 3, 5, 5, 6, 4, 5, 4, 4, 5, 3, 4, 3, 3, 3,
                       4, 3, 3, 3, 4, 3, 3, 3, 2, 6, 1)

ext_tracks <- read_fwf(ext_tracks_file,
                       fwf_widths(ext_tracks_widths, ext_tracks_colnames),
                       na = "-99")
ext_tracks[1:3, 1:15]

#1.2 reading a secure document

zika_file <- paste0("https://raw.githubusercontent.com/cdcepi/zika/master/",
                    "Brazil/COES_Microcephaly/data/COES_Microcephaly-2016-06-25.csv")
zika_brazil <- read_csv(zika_file)
zika_brazil


#2. Requesting data through a web API ,
#Figure out the API rules for HTTP requests
#Write R code to create a request in the proper format
#Send the request using GET or POST HTTP methods
#API keys

# Iowa Environmental Mesonet example
library("tidyverse")
library("riem")
library("httr")
meso_url <- "https://mesonet.agron.iastate.edu/cgi-bin/request/asos.py/"
denver <- GET(url = meso_url,
              query = list(station = "DEN",
                           data = "sped",
                           year1 = "2016",
                           month1 = "6",
                           day1 = "1",
                           year2 = "2016",
                           month2 = "6",
                           day2 = "30",
                           tz = "America/Denver",
                           format = "comma")) %>%
  content() %>%
  read_csv(skip = 5, na = "M")
denver %>% slice(1:3)

#Scraping web data using rvest
library(rvest)
library(magrittr)
lego_movie <- read_html("http://www.imdb.com/title/tt1490017/")

rating <- lego_movie %>%
  html_nodes("strong span") %>%
  html_text() %>%
  as.numeric()
rating

#reading Json data

library(jsonlite)
mydata <- fromJSON("https://projects.propublica.org/forensics/geos.json", flatten = TRUE)
View(mydata)

## Data Manipulation

#Selecting(ends_with,starts_wirh,contains, matches) and filter

head(ext_tracks,5)

ext_tracks %>%
  select(storm_name, month, day, hour, latitude, longitude, max_wind) %>%
  filter(storm_name == "ANDREW" & max_wind >= 137)


#Summary and grouping

ext_tracks %>%
  group_by(storm_name,year) %>%
  summarize(n_obs = n(),
            worst_wind = max(max_wind),
            worst_pressure = min(min_pressure))

#Adding , changing and renaming columns

library(faraway)
data(worldcup)
#adding columns
worldcup <- worldcup %>%
  mutate(player_name = rownames(worldcup))
worldcup

#Changing columns

worldcup <- worldcup %>%
  group_by(Position) %>%
  mutate(ave_shots = mean(Shots)) %>%
  ungroup()
worldcup

#Renaming Columns
worldcup %>%
  rename(Name = player_name) %>%
  slice(1:3)
worldcup

#gather

VADeaths <- VADeaths %>%
  tbl_df() %>%
  mutate(age = row.names(VADeaths))
VADeaths

VADeaths %>%
  gather(key = key, value = death_rate, -age)

#summarize and spread

wc_table <- worldcup %>%
  filter(Team %in% c("Spain", "Netherlands", "Uruguay", "Germany")) %>%
  select(Team, Position, Passes) %>%
  group_by(Team, Position) %>%
  summarize(ave_passes = mean(Passes),
            min_passes = min(Passes),
            max_passes = max(Passes),
            pass_summary = paste0(round(ave_passes), " (",
                                  min_passes, ", ",
                                  max_passes, ")")) %>%
  select(Team, Position, pass_summary)
wc_table

library(knitr)
wc_table %>%
  spread(Position, pass_summary)%>%kable()

#Merging in R
team_standings<-read_csv("C:/Users/Balan Gnanam/Desktop/team_standings.csv",col_types = "-ic",n_max=5)
team_standings
data(worldcup)
worldcup %>%
  mutate(Name = rownames(worldcup),
         Team = as.character(Team)) %>%
  select(Name, Position, Shots, Team) %>%
  arrange(desc(Shots)) %>%
  slice(1:5) %>%
  left_join(team_standings, by = "Team") %>% rename("Team Standing" = Standing) %>%
  kable()

#Date & Time
library(tidyverse)
library("lubridate")  # check posixct
andrew_tracks <- ext_tracks %>%
  filter(storm_name == "ANDREW" & year == "1992") %>%
  select(year, month, day, hour, max_wind, min_pressure) %>%
  unite(datetime, year, month, day, hour) %>%
  mutate(datetime = ymd_h(datetime))

andrew_tracks

#2. year, month, yday, hour

andrew_tracks %>%
  select(datetime) %>%
  mutate(year = year(datetime),
         month = months(datetime),
         weekday = weekdays(datetime),
         yday = yday(datetime),
         hour = hour(datetime)) %>%
  slice(1:3)

#3. time zone with day as a number and abrreviated month

andrew_tracks %>%
  mutate(datetime = with_tz(datetime, tzone = "America/New_York"),
         date = format(datetime, "%b %d"))

#Basic String manipulation techniques

paste("Square", "Circle", "Triangle")

paste("Square", "Circle", "Triangle", sep = "+")

paste0("Square", "Circle", "Triangle")

shapes <- c("Square", "Circle", "Triangle")

paste("My favorite shape is a", shapes)

paste(shapes, collapse = " ")

#numberf of characters in a string
nchar("Supercalifragilisticexpialidocious")

##Regular Expressions

head(state.name)
grepl(".", "Maryland")
grepl("a.b", c("aaa", "aab", "abb", "acadb"))
grepl("x+", "Maryland")
grepl("x*", "Maryland")
grepl("s{2,3}", "Mississippi")
# Does "Mississippi" contain the pattern of an "i" followed by
# 2 of any character, with that pattern repeated three times adjacently?
grepl("(i.{2}){3}", "Mississippi")

grepl("\\w", "abcdefghijklmnopqrstuvwxyz0123456789")
grepl("\\d", "0123456789")
grepl("\\s", "\n\t ")
grepl("[aeiou]", "rhythms")
grepl("[^aeiou]", "rhythms")
grepl("\\+", "tragedy + time = humor")
grepl("^a", c("bab", "aab"))
grepl("^[ab]+$", c("bab", "aab", "abc"))
grepl("North|South", c("South Dakota", "North Carolina", "West Virginia"))

#Regex Functions

grep("[Ii]", c("Hawaii", "Illinois", "Kentucky"))
sub("[Ii]", "1", c("Hawaii", "Illinois", "Kentucky"))
gsub("[Ii]", "1", c("Hawaii", "Illinois", "Kentucky"))
#strsplit
two_s <- state.name[grep("ss", state.name)]
two_s
strsplit(two_s, "ss")

#string manipulation using stringR
library(stringr)
state_tbl <- paste(state.name, state.area, state.abb)
head(state_tbl)
str_extract(state_tbl, "[0-9]+")
str_pad("Thai", width = 8, side = "left", pad = "-")
cases <- c("CAPS", "low", "Title")
str_to_title(cases)
to_trim <- c(" space", "the ", " final frontier ")
str_trim(to_trim)

pasted_states <- paste(state.name[1:20], collapse = " ")
cat(str_wrap(pasted_states, width = 80))

a_tale <- "It was the best of times it was the worst of times it was the age of wisdom it was\
the age of foolishness"
word(a_tale, end = 3)

##Memory check

library(pryr)

ls()  #show objects in workspace
object_size(worldcup)

##detour apply functions

#apply- used on arrays
X<-matrix(rnorm(30), nrow=5, ncol=6)
apply(X,2 ,sum)

#lapply- dataframes, lists and vectors

A<-matrix(1:9, 3,3)
B<-matrix(4:15, 4,3)
C<-matrix(8:10, 3,2)
MyList<-list(A,B,C)
MyList

lapply(MyList,"[", , 2)
lapply(MyList,"[", 1, )
lapply(MyList,"[", 1, 2)

#sapply- returns a vector

sapply(MyList,"[", 2,1 )

#mapply- mapply applies a Function to Multiple List or multiple Vector Arguments

Q<-matrix(c(rep(1, 4), rep(2, 4), rep(3, 4), rep(4, 4)),4,4)
Q
Q1<-mapply(rep,1:4,4)
Q1

#tapply(Summary Variable, Group Variable, Function)

medical.example <-
  data.frame(patient = 1:100,
             age = rnorm(100, mean = 60, sd = 12),
             treatment = gl(2, 50,
                            labels = c("Treatment", "Control")))

tapply(medical.example$age, medical.example$treatment, mean)

#back to memory

library(magrittr)
sapply(ls(), function(x) object.size(get(x))) %>% sort %>% tail(5)

rm(titanic,titanic_train)
mem_used()

str(.Machine)

#Roughly, R will periodically cycle through all of the objects that have been
#created and see if there are still any references to the object somewhere in
#the session. If there are no references, the object is garbage-collected and
#the memory returned.

gc()

## in memory strategies data.table
library(tidyverse)
library(hflights)
library(data.table)
DT <-as.data.table(hflights)
DT[Month==10,mean(na.omit(AirTime)), by=UniqueCarrier]

fread("C:/Users/Balan Gnanam/Desktop/team_standings.csv")%>%dplyr::slice(1:3)

#...............................................................#
































































