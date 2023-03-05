# UNIS-WxDisplay

The Isfjorden weather information network project (https://research.unis.no/iwin/) aims to increase the number of local weather measurements in the Isfjord area near Longyearbyen, Svalbard, Norway. In addition to stationary weather stations, there are a number of mobile stations mainly on smaller boats.
The weather stations have their own data logger as well as telemetry system to transmit data to the main databases at the University Centre in Svalbard (UNIS). This repo provides details of a realtime weather display to be installed in the boat Hanna Resvoll, which is used for research and education at UNIS.

## Desirables
- realtime weather data display
- possibly some historical data should be displayed (a simple plot to see trends in changes in weather)
- small(ish) platform
- sensor data: temperature (T), relative humidity (RH), air pressure (p), average wind speed (WS), maximum wind gust (WG), wind direction and standard deviation (WD, Wstd), photosynthetically active radiation sensor (PAR)
- auxiliary data: GNSS location & time, boat heading and speed

## Preliminary thoughts about the implementation

The weather station uses its own data logger, so there are no critical elements in either the hardware or the software. Only irritation of not seeing the weather data on the spot...

### Hardware

A simplistic platform could be a Single-Board Computer (SBC) such as a Raspberry PI with a touchscreen. However, the availability of RPs as of Spring 2023 does encourage looking for alternatives...

The (hardware) connections from the weather station logger and the boat's systems (NMEA2000?) need to be clarified. The good news is that one could probably use NMEA2000 to also power the SBC, see [PICAN-M](https://copperhilltech.com/pican-m-nmea-0183-nmea-2000-hat-for-raspberry-pi-with-smps/)

### Software

It makes sense to separate the data collection (weather station and boat) from the display. A simple way would be to use, for example, InfluxDB or MySQL, and then use [Grafana](https://grafana.com/) as the front-end to provide the graphics. This allows developing the "dashboard" without affecting the data collection. Also, if the SBC is connected to the boat's wifi, creating new dashboards or fixing errors in the display can be easily done.

For testing purposes, it would be nice to have artificial weather data generators that would simulate the data from the weather station and the boat. 
