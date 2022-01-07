#ADS-B Stats Logger

##Features

- Log all unique flights seen by the ADS-B receiver
- Log all unique operators seen by the ADS-B receiver
- Log the flight with the highest altitude seen by the ADS-B receiver
- Log the flight with the highest speed seen by the ADS-B receiver
- Log the flight the furthest away from the ADS-B receiver
- Log the flight closest from the ADS-B receiver
- Log the flight with the best signal strength seen by the ADS-B receiver
- Log the flight with the worst signal strength seen by the ADS-B receiver
- All data is available in Metric Units (by default) or Imperial Units

### WARNING: This is a highly in development script, things can and will change, your data.json file might break and need a manual fix if you update the script to a new version!

## Usage
1. Clone the git repo on your ADS-B server and enter its directory:
```bash
git clone https://github.com/nfacha/adsb-stats-logger.git
cd adsb-stats-logger
```
2. Copy the config file sample:
```bash
cp config.ini.sample config.ini
```
3. Edit the config to your liking, one easy way would be using nano
```bash
nano config.ini
```
4. Edit the config to your liking, one easy way would be using nano
```ini
[PATHS]
DATA_PATH = /run/dump1090-fa/ #The path to your dump1090 logs folder
[LOCATION]
STATION_LAT = 37.7 #Your base station latitude, used for distance calculations
STATION_LNG = 37.7 #Your base station longitude, used for distance calculations
[LOGGING]
SENTRY_DSN =#Sentry DSN for error logging, leave empry to disable
LOG_LEVEL = 20 #Log level, see https://docs.python.org/3/library/logging.html#logging-levels
[UNITS]
USE_METRIC_SYSTEM = true #Use metric system for distance calculations, else use imperial
```
5. Leave the script running in the background, one easy way would be to use screen
```bash
screen -S logger -dm python3 logger.py
```
6. By now the script should be running, wait a bit for data to gather and as soon as you have at least one plane in your range it shoudl start to gather data, to see this data use
```bash
python3 show.py
```
You will get an output similar to this:

```
INFO:root:Logging level: 20
INFO:root:Use metric system: True
--- Metrics ---
Data range: 2022-01-07 16:33:15 - 2022-01-07 13:26:54
Unique Flights: 5
Unique Operators: 3
Max Altitude: Flight IBE6317 11.879000304785126 km at 2022-01-07 13:39:43
Max Speed: Flight IBE6501 851.3644 kmh at 2022-01-07 13:36:00
Max Station Distance: Flight RYR28FF 5449.571199579309 km at 2022-01-07 15:34:44
Min Station Distance: Flight SAT571 12.83198307011012 km at 2022-01-07 16:33:14
Max Signal: Flight IBE6317 -16.3 db at 2022-01-07 13:39:43
Min Signal: Flight IBE6501 -24.0 db at 2022-01-07 13:39:43
--- Unique Flights Seen ---
SAT2500 last seen on 2022-01-07 13:26:54
IBE6317 last seen on 2022-01-07 13:39:48
IBE6501 last seen on 2022-01-07 13:39:48
RYR28FF last seen on 2022-01-07 15:40:59
SAT571 last seen on 2022-01-07 16:33:15
--- Unique Operators Seen ---
SAT last seen on 2022-01-07 16:33:15
IBE last seen on 2022-01-07 13:39:48
RYRFF last seen on 2022-01-07 15:40:59

Process finished with exit code 0

```

If you want to see the runtime logs, or to be able to Ctrl-C you can enter the screen with:
```bash
screen -x logger
```