# QLandkarte GT

A dokumentáció írásakor a QLandkarte GT legfrissebb verziója az 1.7.7, mely 2014 júliusában jelent meg, azonban az Ubuntu szoftver repository-jában csak a 1.7.5. verzió volt fenn. A [changelog](http://sourceforge.net/p/qlandkartegt/code/HEAD/tree/QLandkarteGT/trunk/changelog.txt) alapján azonban semmi lényegesebb változtatás nem került bele közben.

A QLandkarte GT utódja a [QMapShack](https://bitbucket.org/maproom/qmapshack/wiki/Home), mely fejlesztése 2014. augusztusában indult, és a QLandkarte teljes újraírását ígérik. Azonban még nincs olyan stabil állapotban, hogy egyszerűen telepíteni lehessen Ubuntura (forrásból fordítva kipróbálható). Főbb újdonságok a több workspace és a projekt alapú adatkezelés lesz.

Ez a leírás nem egy teljes dokumentáció, csupán csak felvillantani szeretné az alkalmazás képességeit, és egy két tippet-trükköt adni.

## Telepítés és használatba vétel

Az alábbi paranccsal telepíthető:

	sudo apt-get install qlandkartegt

A képernyő két fő része a tool-view bal oldalt, és a térkép a jobb oldalt.

Nekem abszolút helypazarlásnak tűnik a tool-view-n az un. option list, hiszen az összes funkció elérhető a térképen jobb klikkre, vagy a menüből. Ezért az alatta lévő részt megfogva és felhúzva el lehet tüntetni. Másrészt hogy az egérgörgő pont ugyanabban az irányban nagyítson, mint a MapSource, a Setup/General menüben kell a Mouse Wheel panelen a Flip jelölőnégyzetet bepipálni.

## Dokumentáció

Egy jó kis [esettanulmány](http://sourceforge.net/p/qlandkartegt/qlandkartegt/A_Grand_Day_Out/) található a QLandkarte GT oldalán, mely egy túrázás előkészítését és utómunkálatait mutatja be részletes leírással, képekkel gazdagon illusztrálva. Az alkalmazás súgója ugyan nem működik, de a két leghasznosabb oldal a [wiki](http://sourceforge.net/p/qlandkartegt/qlandkartegt/QLandkarte_GT/) valamint a [FAQ](http://sourceforge.net/p/qlandkartegt/qlandkartegt/FAQ/). 

## Eszköz csatlakoztatása

A Setup/General menüpontban kell a Device & Xfer fület kiválasztani, és ki kell választani a megfelelő GPS eszközt.

## Térképek kezelése

A QLandkarte GT képes vektoros és raszteres térképeket is kezelni, valamint képes folyamatosan is letölteni az internetről. Kezelni a bal oldali tool-view-n lehet a Maps fülön. Alapból az Open Street Map van benne, de a Google Mapet is könnyű bekötni. Jobb klikk, Add TMS map..., és a következő címek valamelyikét kell beírni.

	Google map
	http://mt.google.com/vt/x=%2&y=%3&z=%1

	Satellite map
	http://mt.google.com/vt/lyrs=s&x=%2&y=%3&z=%1

	Terrain map
	http://mt.google.com/vt/lyrs=t&x=%2&y=%3&z=%1 

Amennyiben a Turistautak.hu oldalról letöltött térképet szeretnénk használni, töltsük le a megfelelő [oldalról](http://turistautak.hu/garmin.php) a .zip állományt, és csomagoljuk ki. Több .img állományt és egy .tdb állományt tartalmaz. A File/Load map menüpontban válasszuk ki először a .tdb állományt, majd a vele megegyező nevű .img állományt. Ekkor a térkép megjelenik a Vector fülön.

A Turistautak.hu térképei alapesetben nem jelennek meg, csak ha nagyon ránagyítunk. Ezt úgy kell kiküszöbölni, hogy alul a részletességet növelni kell, a comboboxban a Detail 5 értéket kell kiválasztani. Alul van egy Night kapcsoló is, ezzel egy más színsémát tudunk alkalmazni.

Ugyanígy kell tenni az OMP térképekkel is. Ennek annyi az érdekessége, hogy három stílust is tartalmaz, melyek között a térkép alatt, a részletesség mellett megjelenő legördülő menüben lehet választani. A turistaútvonalak színezése csak bizonyos nagyítás mellett látható.

Az alsó menüben lehet a POI labels kapcsolóval a POI-k nevének megjelenítését be- és kikapcsolni, valamint a Grid kapcsolóval a térképen a rácsot bekapcsolni (mely a mellette lévő gombbal konfigurálható).

Azt is meg lehet csinálni, hogy alul egy streamelt raszteres térkép jelenik meg, és felette a vektoros. Ehhez először dupla klikk a streamelt térképen, majd a vektoros térképen az első oszlopban (M azaz Mode oszlop) kell egy klikket nyomni (use a single click to activate map as overlay).

## Geoládák adatainak betöltése

Először a Geocaching.hu oldalon kell a geoládák adatait .gpx formátumban letölteni, majd a File/Load Geo Data menüpontban betölteni. Ekkor a már meglévő objektumok törlődni fognak. Be lehet tölteni adatokat a már meglévő objektumok mellé is a File/Add Geo Data menüpontban. 

## Útvonaltervezés

Overlay/Distance Polyline menüpontot kell kiválasztani, majd egyenként klikkelgetni az útpontokat. Ha az egy útra esik, akkor a QLandkarte GT megpróbálja az útra illeszteni. Majd bal oldalon jobb klikk a polyline-on, és Make Route a felugró menüben az útvonal elkészítéséhez.

## Feltöltés az eszközre

A Waypoint, Track és Route menüpontban is van Upload menüpont.

## Térkép feltöltése az eszközre

Ki kell választani a térképet a Map/Select Sub Map menüpontban. Ezt akkor lehet, ha a térkép nem overlay módban van megjelenítve. A Maps fülön megjelenik egy Selected Maps lista, ahol látható a kiválasztott szelvény mérete is. A Map/Upload menüpont használatával lehet feltölteni az eszközre.

## Adatok letöltése a GPS-ről

A Waypoint, Track és Route menüpontban is van Download menüpont.

## Adatok utófeldolgozása

A rögzített nyomvonalat fel lehet vágni kisebb nyomvonalakra, de szerkeszteni közvetlenül nem nagyon lehet. Át lehet konvertálni Overlay-jé, azt lehet szerkeszteni, majd visszakonvertálni nyomvonallá, de ekkor elvesznek az idő adatok.
