# Adatforrások

## Geocaching.hu

A  [Geocaching.hu](http://geocaching.hu) a magyar geocache-erek első számú információforrása, ahová a ládák adatai vannak feltöltve. A ládák adatait innen sok formátumban le lehet tölteni, de nekünk a .gpx formátum az érdekes.

## Turistautak.hu

A [Turistautak.hu](http://turistautak.hu) oldal koordinálja egy lelkes csapat munkáját, mely GPS-es terepbejárások alapján, nonprofit alapon építik Magyarország térképét. Teljes közúthálózat, települések utca szintű térképei, POI-k, és ami számunkra a legfontosabb, a turistautak. Szigorú szabályok szerint működik, vektorosan csak megbízható szerkesztők tölthetik le és szerkeszthetik.

A térképek többféle [formátumban](http://www.turistautak.hu/wiki/Kimenetek) is megtekinthetőek és letölthetőek. Számunkra talán a böngészőből is nézhető [raszteres](http://terkep.turistautak.hu), valamint a letölthető, és [Garmin eszközökre feltölthető](http://www.turistautak.hu/garmin.php) formátum az érdekes. A letölthető .zip-ben megtalálható a leíró .tdb állomány, és a térképeket tartalmazó .img állományok.

A hátteréről csak annyit, hogy MapEdit nevű Windowson futó szerkesztőben készül a szerkesztés nyomvonalak alapján és .mp formátumban kerül mentésre (és utána ebből konvertálják különböző formátumokra). 

A térkép több [tájegységre](http://turistautak.hu/regions.php) van bontva, melyek külön .img állományban jelennek meg. Hasznos információforrás az oldal [wikije](http://www.turistautak.hu/wiki/Kezd%C5%91lap) is.

## OpenStreetMap

Az [OpenStreetMap](https://www.openstreetmap.org), röviden OSM egy hasonló kezdeményezés, mint a Turistautak.hu, azonban az egész világra koncentrál, és korántsem olyan szigorú szabályok szerint működik. Az OpenStreetMap XML alapú .osm vektoros térkép formátummal dolgozik, ami mindenki számára le is tölthető.

[Wikijén](http://wiki.openstreetmap.org/wiki/Main_Page) és [magyar nyelvű aloldalán](http://wiki.openstreetmap.org/wiki/Hu:Main_Page) rengeteg információ megtalálható.

Az oldalról elindulva lehet eljutni a [letöltésekig](http://www.openstreetmap.hu/letoltesek), általában átirányít egy másik oldalra. Így van ez Garmin GPS-ek esetén is, illetve van egy leírás is, hogy mi hogyan tudunk .osm adatokból .img állományokat konvertálni. Mivel a következő adatforrás, az Openmaps az OpenStreetMap alapján dolgozik, és biztosít Garmin .img formátumú letöltést, ezért inkább annak használatát javaslom.

## Openmaps

Az [Openmaps](http://openmaps.eu), röviden OMP kezdeményezés szintén a geocachingből nőtte ki magát, 2006-ban kezdett el egy lelkes csoport Erdély térképet fejleszteni, mely később az Erdély Térkép Projekt (ETP) nevet kapta. Felvetődött, hogy ugyanígy kéne egy Szlovákia térkép is, ekkor lett OMP a neve. Később egyre több terület került be. A magyarországi térképadatok forrása azonban ugyanúgy a Turistautak.hu. Online is böngészhetők a térképek, de le is letölthetők, többek közt .img formátumban is.

2015 január 1-től azonban csak az OSM adatbázisa alapján készítenek térképeket. Az OMP saját adatai, vagy a Turistautak.hu forrásból készített térképek az [archívumból](http://openmaps.eu/archive2014) elérhetőek. Az OSM-en nem szereplő adatok átvitele folyamatosan történik, mely munkához bárki csatlakozhat.

A térkép hetente kerül legenerálásra, és [letölthető](http://openmaps.eu/garmindownload) különböző formátumokban. Számunkra a `omphiking.zip` érdekes, mely tartalmazza a leíró .tdb állományt(`62product.tdb`), a rengeteg .img állományt, és három stílust is. A `N0000062.TYP` nem tartalmaz speciális kiemeléseket, a `R0000062.TYP` pirossal jeleníti meg a turistautakat, a `C0000062.TYP` pedig a turistautak színével jeleníti meg azokat. A térképp több mint 300 téglalap alapú részre van osztva, ennyi .img állományt tartalmaz a letölthető .zip állomány is.



