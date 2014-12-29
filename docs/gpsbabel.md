# GPSBabel

Ubuntun az alábbi paranccsal telepíthető.

	sudo apt-get install gpsbabel

## Feltöltés az eszközre

Először töltsünk le egy GPX állományt a geocaching.hu-ról, majd adjuk ki a következő parancsot.

	gpsbabel -i gpx -f caches.gpx -o garmin -F usb:

A `gpx` paraméter az input formátumra, a `garmin` paraméter az output formátumra utal. A `-f` paraméter mögött az input állomány, a `-F` paraméter mögött az output állomány áll, most speciálisan az `usb:` érték, hiszen a GPS az USB portra van rádugva.

## Letöltés az eszközről

Az előző parancs alapján kitalálható, hogyan töltsünk le adatot a GPS-ről a GPSBabel alapján.

	gpsbabel -i garmin -f usb: -o gpx -F output.gpx

