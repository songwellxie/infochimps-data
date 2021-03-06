# ASA SC/SG Data Expo 2009 Data: Air Flight Delays, Airports, Airlines and Aircraft

> This data set is from the [ASA Statistical Computing / Statistical Graphics](http://stat-computing.org/dataexpo/2009/the-data.html) section 2009 contest, "Airline Flight Status -- Airline On-Time Statistics and Delay Causes". The documentation below is largely adapted from that site.

## Overview

The U.S. Department of Transportation's (DOT) Bureau of Transportation Statistics (BTS) tracks the on-time performance of domestic flights operated by large air carriers. Summary information on the number of on-time, delayed, canceled and diverted flights appears in DOT's monthly Air Travel Consumer Report, published about 30 days after the month's end, as well as in summary tables posted on this website. BTS began collecting details on the causes of flight delays in June 2003. Summary statistics and raw data are made available to the public at the time the Air Travel Consumer Report is released.

The data consists of flight arrival and departure details for all commercial flights within the USA, from October 1987 to April 2008. This is a large dataset: there are nearly 120 million records in total, and takes up 1.6 gigabytes of space compressed and 12 gigabytes when uncompressed.

The data comes originally from the DOT's [Research and Innovative Technology Administration (RITA)](http://www.transtats.bts.gov/OT_Delay/OT_DelayCause1.asp) group, where it is [described in detail](http://www.transtats.bts.gov/Fields.asp?Table_ID=236). You can download the original data there. The files here have derivable variables removed, are packaged in yearly chunks and have been more heavily compressed than the originals.

Here are a few ideas to get you started exploring the data:

* When is the best time of day/day of week/time of year to fly to minimise delays?
* Do older planes suffer more delays?
* How does the number of people flying between different locations change over time?
* How well does weather predict plane delays?
* Can you detect cascading failures as delays in one airport create delays in others? Are there critical links in the system?

## Fields


     1	Year             	int       	1987-2008
     2	Month            	int       	1-12
     3	DayofMonth       	int       	1-31
     4	DayOfWeek        	int       	1 (Monday) - 7 (Sunday)
     5	DepTime          	int       	actual departure time (local, hhmm)
     6	CRSDepTime       	int       	scheduled departure time (local, hhmm)
     7	ArrTime          	int       	actual arrival time (local, hhmm)
     8	CRSArrTime       	int       	scheduled arrival time (local, hhmm)
     9	UniqueCarrier    	varchar(5)	unique carrier code
    10	FlightNum        	int       	flight number
    11	TailNum          	varchar(8)	plane tail number
    12	ActualElapsedTime	int       	in minutes
    13	CRSElapsedTime   	int       	in minutes
    14	AirTime          	int       	in minutes
    15	ArrDelay         	int       	arrival delay, in minutes
    16	DepDelay         	int       	departure delay, in minutes
    17	Origin           	varchar(3)	origin IATA airport code
    18	Dest             	varchar(3)	destination IATA airport code
    19	Distance         	int       	in miles
    20	TaxiIn           	int       	taxi in time, in minutes
    21	TaxiOut          	int       	taxi out time in minutes
    22	Cancelled        	int       	was the flight cancelled?
    23	CancellationCode 	varchar(1)	reason for cancellation (A=carrier,B=weather,C=NAS, D = security)
    24	Diverted         	varchar(1)	1 = yes, 0 = no
    25	CarrierDelay     	int       	in minutes
    26	WeatherDelay     	int       	in minutes
    27	NASDelay         	int       	in minutes
    28	SecurityDelay    	int       	in minutes
    29	LateAircraftDelay	int       	in minutes


## Supplementary data

* **Airports**: `dataexpo_airports-raw.csv` describes the locations of US airports. The majority of this data comes from the FAA, but a few extra airports (mainly military bases and US protectorates) were collected from other web sources by Ryan Hafen and Hadley Wickham. Its fields:

    iata    	the international airport abbreviation code
    name     	of the airport
    city     	city in which the airport is located
    state     	state in which the airport is located
    country 	country in which airport is located
    lat      	latitude of the airport
    lng      	longitude of the airport

* **Carrier codes**: Listing of carrier codes with full names: `dataexpo_airlines-raw.csv`
* **Planes**: You can find out information about individual planes by googling the tail number or by looking it up in the [FAA database](http://registry.faa.gov/aircraftinquiry/NNum_inquiry.asp). `dataexpo_airplanes-raw.csv` ([original](http://stat-computing.org/dataexpo/2009/plane-data.csv)) is a csv file produced from the (some of) the data on that page.
* **Weather**: Meteorological data is available from (among many others) NOAA and weather underground. The call sign for airport weather stations can be constructed by adding K to the airport code, e.g. KORD, KLAX, KSEA.

#### Fetching the data

Felds from the original source:

        -- Time Period
        Year                                                           	Year
        Quarter                                                        	Quarter (1-4)
        Month                                                          	Month
        DayofMonth                                                     	Day of Month
        DayOfWeek                                                      	Day of Week
        FlightDate                                                     	Flight Date (yyyymmdd)

        -- Airline
        UniqueCarrier                                                  	Unique Carrier Code. When the same code has been used by multiple carriers, a numeric suffix is used for earlier users, for example, PA, PA(1), PA(2). Use this field for analysis across a range of years.	Analysis
        AirlineID                                                      	An identification number assigned by US DOT to identify a unique airline (carrier). A unique airline (carrier) is defined as one holding and reporting under the same DOT certificate regardless of its Code, Name, or holding company/corporation.	Analysis
        Carrier                                                        	Code assigned by IATA and commonly used to identify a carrier. As the same code may have been assigned to different carriers over time, the code is not always unique. For analysis, use the Unique Carrier Code.
        TailNum                                                        	Tail Number
        FlightNum                                                      	Flight Number

        -- Origin
        OriginAirportID                                                	Origin Airport, Airport ID. An identification number assigned by US DOT to identify a unique airport. Use this field for airport analysis across a range of years because an airport can change its airport code and airport codes can be reused.	Analysis
        OriginAirportSeqID                                             	Origin Airport, Airport Sequence ID. An identification number assigned by US DOT to identify a unique airport at a given point of time. Airport attributes, such as airport name or coordinates, may change over time.
        OriginCityMarketID                                             	Origin Airport, City Market ID. City Market ID is an identification number assigned by US DOT to identify a city market. Use this field to consolidate airports serving the same city market.	Analysis
        Origin                                                         	Origin Airport
        OriginCityName                                                 	Origin Airport, City Name
        OriginState                                                    	Origin Airport, State Code
        OriginStateFips                                                	Origin Airport, State Fips
        OriginStateName                                                	Origin Airport, State Name
        OriginWac                                                      	Origin Airport, World Area Code

        -- Destination
        DestAirportID                                                  	Destination Airport, Airport ID. An identification number assigned by US DOT to identify a unique airport. Use this field for airport analysis across a range of years because an airport can change its airport code and airport codes can be reused.	Analysis
        DestAirportSeqID                                               	Destination Airport, Airport Sequence ID. An identification number assigned by US DOT to identify a unique airport at a given point of time. Airport attributes, such as airport name or coordinates, may change over time.
        DestCityMarketID                                               	Destination Airport, City Market ID. City Market ID is an identification number assigned by US DOT to identify a city market. Use this field to consolidate airports serving the same city market.	Analysis
        Dest                                                           	Destination Airport
        DestCityName                                                   	Destination Airport, City Name
        DestState                                                      	Destination Airport, State Code
        DestStateFips                                                  	Destination Airport, State Fips
        DestStateName                                                  	Destination Airport, State Name
        DestWac                                                        	Destination Airport, World Area Code

        -- Departure Performance
        CRSDepTime                                                     	CRS Departure Time (local time: hhmm)
        DepTime                                                        	Actual Departure Time (local time: hhmm)
        DepDelay                                                       	Difference in minutes between scheduled and actual departure time. Early departures show negative numbers. Analysis
        DepDelayMinutes                                                	Difference in minutes between scheduled and actual departure time. Early departures set to 0.
        DepDel15                                                       	Departure Delay Indicator, 15 Minutes or More (1=Yes)
        DepartureDelayGroups                                           	Departure Delay intervals, every (15 minutes from \<-15 to >180)
        DepTimeBlk                                                     	CRS Departure Time Block, Hourly Intervals
        TaxiOut                                                        	Taxi Out Time, in Minutes
        WheelsOff                                                      	Wheels Off Time (local time: hhmm)

        -- Arrival Performance
        WheelsOn                                                       	Wheels On Time (local time: hhmm)
        TaxiIn                                                         	Taxi In Time, in Minutes
        CRSArrTime                                                     	CRS Arrival Time (local time: hhmm)
        ArrTime                                                        	Actual Arrival Time (local time: hhmm)
        ArrDelay                                                       	Difference in minutes between scheduled and actual arrival time. Early arrivals show negative numbers.	Analysis
        ArrDelayMinutes                                                	Difference in minutes between scheduled and actual arrival time. Early arrivals set to 0.
        ArrDel15                                                       	Arrival Delay Indicator, 15 Minutes or More (1=Yes)
        ArrivalDelayGroups                                             	Arrival Delay intervals, every (15-minutes from <-15 to >180)
        ArrTimeBlk                                                     	CRS Arrival Time Block, Hourly Intervals

        -- Cancellations and Diversions
        Cancelled                                                      	Cancelled Flight Indicator (1=Yes)
        CancellationCode                                               	Specifies The Reason For Cancellation
        Diverted                                                       	Diverted Flight Indicator (1=Yes)

        -- Flight Summaries
        CRSElapsedTime                                                 	CRS Elapsed Time of Flight, in Minutes
        ActualElapsedTime                                              	Elapsed Time of Flight, in Minutes
        AirTime                                                        	Flight Time, in Minutes
        Flights                                                        	Number of Flights
        Distance                                                       	Distance between airports (miles)
        DistanceGroup                                                  	Distance Intervals, every 250 Miles, for Flight Segment

        -- Cause of Delay (Data starts 6/2003)
        CarrierDelay                                                   	Carrier Delay, in Minutes
        WeatherDelay                                                   	Weather Delay, in Minutes
        NASDelay                                                       	National Air System Delay, in Minutes
        SecurityDelay                                                  	Security Delay, in Minutes
        LateAircraftDelay                                              	Late Aircraft Delay, in Minutes

        -- Gate Return Information at Origin Airport (Data starts 10/2008)
        FirstDepTime                                                   	First Gate Departure Time at Origin Airport
        TotalAddGTime                                                  	Total Ground Time Away from Gate for Gate Return or Cancelled Flight
        LongestAddGTime                                                	Longest Time Away from Gate for Gate Return or Cancelled Flight

        -- Diverted Airport Information (Data starts 10/2008)
        DivAirportLandings                                             	Number of Diverted Airport Landings
        DivReachedDest                                                 	Diverted Flight Reaching Scheduled Destination Indicator (1=Yes)
        DivActualElapsedTime                                           	Elapsed Time of Diverted Flight Reaching Scheduled Destination, in Minutes. The ActualElapsedTime column remains NULL for all diverted flights.	Analysis
        DivArrDelay                                                    	Difference in minutes between scheduled and actual arrival time for a diverted flight reaching scheduled destination. The ArrDelay column remains NULL for all diverted flights.	Analysis
        DivDistance                                                    	Distance between scheduled destination and final diverted airport (miles). Value will be 0 for diverted flight reaching scheduled destination.	Analysis
        Div1Airport                                                    	Diverted Airport Code1
        Div1AirportID                                                  	Airport ID of Diverted Airport 1. Airport ID is a Unique Key for an Airport
        Div1AirportSeqID                                               	Airport Sequence ID of Diverted Airport 1. Unique Key for Time Specific Information for an Airport
        Div1WheelsOn                                                   	Wheels On Time (local time: hhmm) at Diverted Airport Code1
        Div1TotalGTime                                                 	Total Ground Time Away from Gate at Diverted Airport Code1
        Div1LongestGTime                                               	Longest Ground Time Away from Gate at Diverted Airport Code1
        Div1WheelsOff                                                  	Wheels Off Time (local time: hhmm) at Diverted Airport Code1
        Div1TailNum                                                    	Aircraft Tail Number for Diverted Airport Code1
        Div2Airport                                                    	Diverted Airport Code2
        Div2AirportID                                                  	Airport ID of Diverted Airport 2. Airport ID is a Unique Key for an Airport
        Div2AirportSeqID                                               	Airport Sequence ID of Diverted Airport 2. Unique Key for Time Specific Information for an Airport
        Div2WheelsOn                                                   	Wheels On Time (local time: hhmm) at Diverted Airport Code2
        Div2TotalGTime                                                 	Total Ground Time Away from Gate at Diverted Airport Code2
        Div2LongestGTime                                               	Longest Ground Time Away from Gate at Diverted Airport Code2
        Div2WheelsOff                                                  	Wheels Off Time (local time: hhmm) at Diverted Airport Code2
        Div2TailNum                                                    	Aircraft Tail Number for Diverted Airport Code2
        Div3Airport                                                    	Diverted Airport Code3
        Div3AirportID                                                  	Airport ID of Diverted Airport 3. Airport ID is a Unique Key for an Airport
        Div3AirportSeqID                                               	Airport Sequence ID of Diverted Airport 3. Unique Key for Time Specific Information for an Airport
        Div3WheelsOn                                                   	Wheels On Time (local time: hhmm) at Diverted Airport Code3
        Div3TotalGTime                                                 	Total Ground Time Away from Gate at Diverted Airport Code3
        Div3LongestGTime                                               	Longest Ground Time Away from Gate at Diverted Airport Code3
        Div3WheelsOff                                                  	Wheels Off Time (local time: hhmm) at Diverted Airport Code3
        Div3TailNum                                                    	Aircraft Tail Number for Diverted Airport Code3
        Div4Airport                                                    	Diverted Airport Code4
        Div4AirportID                                                  	Airport ID of Diverted Airport 4. Airport ID is a Unique Key for an Airport
        Div4AirportSeqID                                               	Airport Sequence ID of Diverted Airport 4. Unique Key for Time Specific Information for an Airport
        Div4WheelsOn                                                   	Wheels On Time (local time: hhmm) at Diverted Airport Code4
        Div4TotalGTime                                                 	Total Ground Time Away from Gate at Diverted Airport Code4
        Div4LongestGTime                                               	Longest Ground Time Away from Gate at Diverted Airport Code4
        Div4WheelsOff                                                  	Wheels Off Time (local time: hhmm) at Diverted Airport Code4
        Div4TailNum                                                    	Aircraft Tail Number for Diverted Airport Code4
        Div5Airport                                                    	Diverted Airport Code5
        Div5AirportID                                                  	Airport ID of Diverted Airport 5. Airport ID is a Unique Key for an Airport
        Div5AirportSeqID                                               	Airport Sequence ID of Diverted Airport 5. Unique Key for Time Specific Information for an Airport
        Div5WheelsOn                                                   	Wheels On Time (local time: hhmm) at Diverted Airport Code5
        Div5TotalGTime                                                 	Total Ground Time Away from Gate at Diverted Airport Code5
        Div5LongestGTime                                               	Longest Ground Time Away from Gate at Diverted Airport Code5
        Div5WheelsOff                                                  	Wheels Off Time (local time: hhmm) at Diverted Airport Code5
        Div5TailNum                                                    	Aircraft Tail Number for Diverted Airport Code5
