# MagicMirror_config
Conffi tiedostot MagicMirror

##Setup
Asennettu viimeisin Raspbian Stretch with Desktop, ei recommended software https://www.raspberrypi.org/downloads/raspbian/
Asennettu 32Gb microSD-kortille Etcherillä https://www.balena.io/etcher/

Raspbian-configilla locale ja kieliasetukset kuntoon

Terminaalilla vaihdetaan salasana ja päivitetään RasPi
```
passwd
sudo apt update
sudo apt upgrade 
```

Ladattu MagicMirror2 käyttäen skriptiä https://magicmirror.builders/.

##Configuring
###HSL pysäkit
Ladattu HSL moduuli https://github.com/0EQUALIZERO/MMM-Hsl-stops
- konfiguroitu käyttämään koko suomen reittiopasta HSL sijasta
- korjattu ikonit toimimaan korjaamalla hsl_stops.js (LISÄTTY REPOON 24.2.2019) 
- oman pysäkin löytää https://beta.digitransit.fi ottamalla pysäkin URLista numero %3A jälkeen


__________
TODO 
- screen saver pois päältä
- spotify presonal tweak (UI styling)
- possibly kellon ja weathernowforecast fonttia isommaks
- herpsderps
