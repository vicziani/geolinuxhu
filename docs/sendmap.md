# sendmap

A sendmap szabadon [letölthető](http://cgpsmapper.com/buy.htm), válasszuk a legutolsó verziót: Free sendMap20 rev 4.2 BETA for Linux with experimental USB support. Ez egy darab `sendmap20.gz` állomány, tömörítsük ki, majd a kapott állományt tegyük futtathatóvá.

	gunzip sendmap20.gz
	chmod +x sendmap20

Egyszerűen tölthetünk fel .img állományokat Garmin készülékre a következő paranccsal:

	sendmap20 -tUSB file1.img file2.img file3.img ...
