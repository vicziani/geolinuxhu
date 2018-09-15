# Telepítés

Az mkgmap ugyan fenn van az Ubuntu központi repository-jában, azonban nem
javaslom innen telepíteni, mert egyrészt régi, nekem hibásan is működött, valamint
mivel Javat is telepít, elrontotta az eddigi Java beállításaimat. Én tehát inkább
a következő módszert javaslom.

Töltsük le a megfelelő állományt a [Java.com](https://java.com/en/download/) oldalról.
Legyen ez pl. a `jre-8u31-linux-x64.tar.gz`.

Másoljuk a `/opt` könyvtárba a letöltött fájlt, és csomagoljuk ki a következő paranccsal:

	tar zxvf jre-8u31-linux-x64.tar.gz

Ekkor megjelenik a `/opt/jre1.8.0_31` könyvtár.

Töltsük le az mkgmapet is a [hivatalos oldalról](http://www.mkgmap.org.uk/download/mkgmap.html).
Legyen ez a `mkgmap-r3435.zip`. Másoljuk a `/opt` könyvtárba, és tömörítsük ki a következő paranccsal.

	unzip mkgmap-r3435.zip

Ekkor megjelenik a `/opt/mkgmap-r3435` könyvtár.

Ellenőrizzük a telepítés sikerességét.

	/opt/jre1.8.0_31/bin/java -jar /opt/mkgmap-r3435/mkgmap.jar --version

# .tdb állományok generálása

Abban az esetben, ha csak egy vagy több .img állomány áll rendelkezésünkre,
a QLandkarte GT alkalmazással nem tudjuk őket megnyitni, ahhoz még kell
egy leíró .tdb állomány is. Ilyent tud generálni az mkgmap a következő 
parancs kiadásával.

	/opt/jre1.8.0_31/bin/java -jar /opt/mkgmap-r3435/mkgmap.jar --tdbfile turistautak.img

# .img állományok összevonása

Mivel az OMP letöltésben sok kis .img állomány szerepel, szükségünk lehet arra, hogy összevonjuk
ezeket egy nagy .img állománnyá. Ez a következő parancs kiadásával lehet:

	find /opt/omphiking/ -type f -name 0*.img | xargs /opt/jre1.8.0_31/bin/java -jar /opt/mkgmap-r3435/mkgmap.jar --gmapsupp --description="OMP hiking 2015-02-02"

A parancs eleje kigyűjti a `/opt/omphiking/` könyvtárban lévő összes `0` karakterrel kezdődő `.img` kiterjesztésű állományt,
majd átadja az mkgmapnek paraméterül. A `--gmapsupp` kapcsoló mondja meg, hogy hozza létre a `gmapsupp.img` állományt, amit fel lehet másolni a GPS-re. A `--description` kapcsoló hatására amennyiben a GPS-en megjelenítjük a térképet, az `OMP hiking 2015-01-30` szöveg fog megjelenni. (Azért jó beletenni a frissítés dátumát, mert akkor a GPS-re pillantva is meg tudjuk azt nézni.) Ugyanez a parancs a Turistautak.hu térképre a következőképp néz ki.

	find /opt/tohu/ -type f -name 9*.img | xargs /opt/jre1.8.0_31/bin/java -jar /opt/mkgmap-r3435/mkgmap.jar --gmapsupp --description="Turistautak.hu 2015-02-02"

