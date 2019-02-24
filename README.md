# MagicMirror_config
Conffi tiedostot MagicMirror

## Setup
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

Ladattu HSL moduuli https://github.com/0EQUALIZERO/MMM-Hsl-stops
```
cd ~/MagicMirror/modules
git clone https://github.com/0EQUALIZERO/MMM-Hsl-stops.git
cd MMM-Hsl-stops
npm install
```
- konfiguroitu käyttämään koko suomen reittiopasta HSL sijasta
- korjattu ikonit toimimaan korjaamalla hsl_stops.js (LISÄTTY REPOON 24.2.2019) 
- oman pysäkin löytää https://beta.digitransit.fi ottamalla pysäkin URLista numero %3A jälkeen

### Spotify Tweaking

Spotify UI paranneltu kun module ei ole käytössä 
- Modulen käynnistyksen aikana oleva logo poistettu
```
cd ~/MagicMirror/modules/MMM-NowPlayingOnSpotify/css 
nano css/styles
#.NPOS_initContent
display: none;

cd ~/MagicMirror/modules/MMM-NowPlayingOnSpotify/css 
nano css/styles
#.NPOS_loading
display: none;
```	

- Module ei käytössä logo poistetu
```
cd ~/MagicMirror/modules/MMM-NowPlayingOnSpotify/css 
nano css/styles
#.NPOS_nothingIsPlayingContent
display: none;
```


__________
TODO 
- korjattava HSL moduulin ajat sekä HTTP-ongelma (https://github.com/0EQUALIZERO/MMM-Hsl-stops/pull/2)
- spotify presonal tweak (UI styling)
- possibly kellon ja weathernowforecast fonttia isommaks
- herpsderps
