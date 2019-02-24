# MagicMirror_config
Conffi tiedostot MagicMirror

## Setup
Asennettu viimeisin Raspbian Stretch with Desktop, ei recommended software https://www.raspberrypi.org/downloads/raspbian/.

Siirretty .img tiedosto 32Gb microSD-kortille Etcherillä https://www.balena.io/etcher/.

**HUOM!** Vaaditaan tästä eteenpäin setuppaamiseen näppäimistö, hiiri ja näyttö ellet hoida asioita SSH:n kautta terminaalilla lisäämällä SD-kortin juureen tiedosto "ssh" ilman tiedostopäätettä ennen sen asettamista raspiin etchauksen jälkeen

Raspbian-configilla vaihdetaan kieliasetukset kuntoon, vaihdetaan salasana(tai `passwd`) ja enabloidaan sekä VNC että SSH.
Oletuksena käyttäjänä on pi ja salasana raspberry (:D).

Päivitetään Raspbian
```
sudo apt update
sudo apt upgrade 
```

Ladattu MagicMirror2 käyttäen skriptiä https://magicmirror.builders/.

## Configuring

### Screensaver pois

Kokeiltu summamutikassa https://www.raspberrypi.org/forums/viewtopic.php?f=91&t=57552.

Kopioi repon file lightdm.conf polkuun /etc/lightdm/lightdm.conf TAI lisää itse puuttuva rivi [Seat:*] alle
```
sudo cp lightdm.conf /etc/lightdm/lightdm.conf
#TAI lisää itse rivi samaan tiedostoon [Seat:*] alle:
xserver-command=X -s 0 dpms
```
JA reboot.

### HSL pysäkit

Ladattu HSL moduuli https://github.com/0EQUALIZERO/MMM-Hsl-stops.
- korjattu ikonit toimimaan korjaamalla hsl_stops.js (LISÄTTY REPOON 24.2.2019) 
```
cd ~/MagicMirror/modules
git clone https://github.com/0EQUALIZERO/MMM-Hsl-stops.git
cd MMM-Hsl-stops
npm install
```
#### Konffi
- konfiguroitu käyttämään koko suomen reittiopasta HSL sijasta (kts. konffi)
- oman pysäkin löytää https://beta.digitransit.fi kaivamalla oma pysäkki ja ottamalla pysäkin URLista numero %3A jälkeen
```
                {
                        module: 'MMM-Hsl-stops',
                        position: 'top_right',
                        config: {
                        stopId: 'HSL:1070425',  // Id of the stop you want to display, give id test to use test data JSON
                        debug: false, // Increase log output
                        testMode: false, // Activate module in test-mode using provided static JSON test data
                        testJSON: 'test',
                        hurryTime: 2, // In minutes apply hurrytime is passenger has to hurry, 0-x minutes
                        stopNickName: 'TARKKIS', // Personalize stop name with a nickname
                        routeIdFilter: [], // Routes filters, retain only the routes listed here
                        maxListedDepartures: '4', // Max number of departures listed on screen
                        maxFetchedDepartures: '100', // Max number of departures fetched from API to dataset
                        timeRange: 12 * 60 * 60, // Range of trips to be polled in seconds
                        timeToStop: 2, // Time to get to the stop in minutes
                        humanizeTimeTreshold: 15,
                        apiUrl: 'https://api.digitransit.fi/routing/v1/routers/finland/index/graphql' // HSL digirtransit API url        
                        }
                },
```

### IP:n näyttäminen ruudulla

IP:n kaivaminen on aika aamuinen homma, joten kiva olisi näyttää sitä näytöllä omalla modulellaan.
Ladattu MMM-ip (https://github.com/fewieden/MMM-ip) ja asetettu seuraava konffiin.
```
cd ~/MagicMirror/modules
git clone https://github.com/fewieden/MMM-ip.git
cd MMM-ip
npm install
```
#### Konffi
Halutaan vain IPv4 osoite
```
                {
                        module: 'MMM-ip',
                        position: 'bottom_left',
                        config: {
                                fontSize: '8',
                                showFamily: 'IPv4'
                        }
                },
```
__________
TODO 
- korjattava HSL moduulin ajat sekä HTTP-ongelma (https://github.com/0EQUALIZERO/MMM-Hsl-stops/pull/2)
- spotify presonal tweak (UI styling)
- possibly kellon ja weathernowforecast fonttia isommaks
- herpsderps
