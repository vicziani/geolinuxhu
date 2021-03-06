# Geocaching Linuxon

Ez az oldal azoknak készült, akik geocache-elnek, és mellette Linuxot használnak. Ez sajnos azért nem triviális, mert Magyarországon a legelterjedtebb túrázáshoz, geocachinghez használt készüléktípus a Garmin, mely gyártó jelenleg a [BaseCampet](http://www.garmin.com/en-US/shop/downloads/basecamp) biztosítja az eszközeihez, mely jelenleg Windows és Mac operációs rendszereken érhető csak el. A BaseCamp a régebbi [MapSource](http://www8.garmin.com/support/download_details.jsp?id=209) programot váltotta le. Sajnos a Garmin által használt formátumok sem nyíltak.

Az oldal nem csak geocache-ereknek lehet hasznos, hanem túrázóknak, vagy bárkinek, aki Garmin GPS-t használ, vagy egyszerűen csak turistatérképeket akar kezelni Linux operációs rendszeren. Remélem az oldal Geocaching.hu és a Turistautak.hu oldalak felhasználói részére is tartalmaznak hasznos információkat.

Persze van lehetőség arra is, hogy a MapSource-t VirtualBox virtuális gépen Windows-on futtassuk, vagy Wine-vel Windows környezetet emuláljunk, de én inkább a natív megoldásokat szerettem volna megkeresni.

Az oldal létrehozója [Viczián István](http://about.jtechlog.hu/), bármi kérdéssel kapcsolatban elérsz a viczian.istvan címen a gmailen.

Én egy GPSMAP 60 GPS készülékkel rendelkezem, és Ubuntu 14.04 Linuxot futtatok, így a példák is ezen a környezeten lettek tesztelve, de bízom benne, hogy más eszközzel és más disztribúción is hasonlóképp fognak működni.

## Segíts nekem

Az oldal [MkDocs](http://www.mkdocs.org/) eszközzel készült, forrása elérhető a [GitHubon](https://github.com/vicziani/geolinuxhu). Így amennyiben segítenél az oldalak szerkesztésében, dobj egy Pull Requestet.

Ha nem akarsz ennyire belefolyni a technológiai részletekbe, dobj egy e-mailt.

Bármilyen pontosítás, technikai leírás, más GPS-szel vagy disztribúcióval szerzett tapasztalat hasznos lenne.

## Fogalmak

* Névvel, koordinátákkal és egyéb tulajdonsággal rendelkeznek az útpontok (waypoint). Pl. a geoládák és a ládaleírásban szereplő egyéb pontok is útpontként tölthetőek le. A térképekbe szerkesztett pontokat hívják POI-nak (Point of Interests). A GPS-szel is tudunk pontokat megjelölni.
* Az útpontok sorozata az útvonal (route). Általában tervezéshez használatos, ugyanis a GPS ezen tud könnyen végignavigálni minket. 
* A nyomvonalként (track) rögzíti a GPS az utunkat, mely nem más, mint pontok sorozata, melyhez időpont is hozzá van rendelve.
* A vektoros térkép különböző pontokat, vonalakat, területeket (poligon) tartalmaz, az őket alkotó pontok koordinátáinak megadásával. Így a térkép kirajzolása ezen objektumok kirajzolásával történik, melyeket a megfelelőképpen kell transzformálni, mely erőforrásigényesebb művelet. Viszont bizonyos funkcionalitásokat sokkal könnyebb implementálni, mint pl. nagyítás, objektumok/rétegek szűrése, útvonaltervezés, stb.
* A raszteres térkép gyakorlatilag képfájlok halmaza. Különböző nagyításhoz különböző képfájlok tartoznak. Megjelenítése gyors, de a vektoros térképnél leírt funkcionalitások megvalósítása sokkal bonyolultabb, ha nem lehetetlen.

## Fájlformátumok

Két fájlformátum típussal találkozhatunk, az egyik, melyben a térképek adatai kerülnek letárolásra, a másik a GPS által rögzített, vagy a GPS számára hasznos adatok, mint az útpontok, útvonalak és nyomvonalak.

A Garmin készülékek térképformátuma az .img kiterjesztésű állomány. Bár a formátum nem nyílt, [visszafejtették](http://wiki.openstreetmap.org/wiki/OSM_Map_On_Garmin/IMG_File_Format) és rengeteg szoftver képes kezelni. Ezért én is ezt javaslom, hiszen a [turistautak.hu](http://www.turistautak.hu/garmin.php) oldalról ebben a formátumban is le lehet letölteni a térképeket, és a később részletezett QLandkarte GT szoftver is képes kezelni. Az .img állományok mellett szerepelni szokott egy .tdb állomány is, mely összefoglaló információkat tartalmaz az .img fájlokról, és a QLandkarte GT is csak ennek megléte esetén tudja betölteni őket.

A GPS adatok kezelésére a [GPX, vagyis GPS Exchange Format](http://en.wikipedia.org/wiki/GPS_Exchange_Format) formátumot javaslom, ugyanis ez egy nyílt [kvázi szabvány](http://www.topografix.com/gpx.asp), mely XML alapú, és a legtöbb szoftver tudja kezelni. A geocaching.hu oldalon is többek között ebben a formátumban is le lehet tölteni a ládák adatait. Érdemes megjegyezni, hogy a Garmin a MapSource programban a saját .gdb formátumát preferálja, bár képes kezelni sok más formátumot is.

## Garmin eszköz használatba vétele

Csatlakoztassuk a GPS-t az USB porton, majd kapcsoljuk be.

Nyissunk egy terminált, és adjuk ki az `lsusb` parancsot, mely az USB portokra csatlakoztatott eszközöket listázza. Valahol egy ilyent is kell látnunk:

	Bus 003 Device 009: ID 091e:0003 Garmin International GPS (various models)

Itt meg kell jegyezni a busz számát, és az eszköz számát (003/009), ugyanis a következő parancs kiadásánál kelleni fog. Ugyanis alapesetben az eszközhöz tartozó device file úgy jön létre, hogy csak a root felhasználó férhet hozzá. Ez ellenőrizhető a következő paranccsal, használjuk az előbb megjegyzett számokat:

	$ ls -l /dev/bus/usb/003/009
	crw-rw-r-- 1 root root 189, 264 dec   20 21:37 /dev/bus/usb/003/009

A jogosultságokat jelző flageken látható (`crw-rw-r--`), hogy egy normál felhasználó csak olvasni tudja a device file-t. Ahhoz, hogy teljes joga legyen, meg kell mondani a rendszernek (pontosabban a Linux kernelben lévő udev eszközkezelőnek), hogy mikor létrehozza ezt a fájlt, a megfelelő jogosultságokkal tegye. Ehhez egy úgynevezett rule fájlt kell létrehozni a `/etc/udev/rules.d/51-garmin.rules` helyen a következő tartalommal.

	ATTRS{idVendor}=="091e", ATTRS{idProduct}=="0003", MODE="666"

Töltessük újra a szabályokat a következő paranccsal.

	sudo udevadm control --reload-rules

Majd csatlakoztassuk le, majd újra fel az eszközt, és nézzük meg, hogy a létrejött device file már a megfelelő jogosultságokat kapta.

	$ ls -l /dev/bus/usb/003/009
	crw-rw-rw- 1 root root 189, 264 dec   20 21:37 /dev/bus/usb/003/009

A harmadik blokkban megjelent w betű jelzi, hogy immár mindenki számára írható is az eszköz.

Részletesebb információkat az OpenStreetMap [wiki oldalán](http://wiki.openstreetmap.org/wiki/USB_Garmin_on_GNU/Linux) találsz.
