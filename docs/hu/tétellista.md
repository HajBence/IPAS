# IPAS V1 – Intelligens Időjárás Megfigyelő Állomás

## Projekt áttekintés

Az IPAS V1 egy alacsony fogyasztású, napelemes működésre tervezett intelligens időjárás-megfigyelő rendszer. A cél egy autonóm kültéri mérőállomás létrehozása, amely képes hosszú távon környezeti adatokat gyűjteni és tárolni.

A rendszer fő funkciói:

* Hőmérséklet mérés
* Páratartalom mérés
* Légnyomás mérés
* Levegőminőség (VOC) mérés
* Adatnaplózás microSD kártyára
* Akkumulátoros működés
* Napelemes töltés
* Alacsony fogyasztású üzemmódok
* Későbbi vezeték nélküli kommunikáció támogatása

---

# Rendszerarchitektúra

## Fő komponensek

| Komponens              | Típus                    | Funkció                              |
| ---------------------- | ------------------------ | ------------------------------------ |
| ESP32-C3-SUPERMINI     | ESP32 fejlesztőpanel     | Központi vezérlő                     |
| BME680-M               | Környezeti szenzor modul | Hőmérséklet, pára, nyomás, VOC mérés |
| MICROSD-M              | microSD illesztő modul   | Adattárolás                          |
| CN3791-M6V             | MPPT töltő modul         | Akkumulátor töltés                   |
| XTAR-18650-2600-BT     | 18650 Li-Ion akkumulátor | Energia tárolás                      |
| PV150x130-5V/2.5W      | Napelem panel            | Energia termelés                     |
| SS12D00G2              | Tolókapcsoló             | Főkapcsoló                           |
| 1 X 18650 W            | Akkumulátortartó         | Akku rögzítés                        |
| PHR-2                  | 2P csatlakozó            | Tápcsatlakozás                       |
| ESP32-C3-SUPERMINI-EXP | Kifejtő panel            | Fejlesztési és prototípus platform   |

---

# Alkatrészlista (BOM)

| Cikkszám   | Megnevezés             | Darab |
| ---------- | ---------------------- | ----- |
| 100.480.18 | ESP32-C3-SUPERMINI     | 1     |
| 100.407.70 | BME680-M               | 1     |
| 100.374.57 | 1 X 18650 W            | 1     |
| 100.480.19 | ESP32-C3-SUPERMINI-EXP | 1     |
| 100.420.63 | SS12D00G2              | 1     |
| 100.442.23 | XTAR-18650-2600-BT     | 1     |
| 100.416.79 | PV150x130-5V/2.5W      | 1     |
| 100.366.30 | MICROSD-M              | 1     |
| 100.407.04 | CN3791-M6V             | 1     |
| 100.385.21 | PHR-2                  | 1     |

---

# Hardver specifikáció

## Mikrokontroller

### ESP32-C3 Super Mini

Főbb paraméterek:

* 32 bites RISC-V architektúra
* 160 MHz órajel
* 4 MB Flash memória
* Wi-Fi 2.4 GHz
* Bluetooth 5
* Deep Sleep támogatás
* Alacsony fogyasztás
* USB-C csatlakozás

Feladatai:

* Szenzorok kezelése
* Adatfeldolgozás
* Energiafelügyelet
* microSD kezelés
* Alvó mód vezérlés

---

## Környezeti szenzor

### BME680

Mért adatok:

* Hőmérséklet
* Relatív páratartalom
* Légnyomás
* VOC / levegőminőség

Kommunikáció:

* I2C
* SPI

Tervezési megjegyzések:

* Közvetlen napsütéstől védeni kell
* Szellőző ház szükséges
* Távol kell elhelyezni a hőtermelő komponensektől

---

## Energiaellátás

### 18650 Li-Ion akkumulátor

Típus:

* XTAR 18650
* 2600mAh
* Védett kivitel

Feladat:

* Éjszakai működés biztosítása
* Energia tárolása
* Rövid idejű nagyobb áramfelvétel kiszolgálása

---

## Napelem

### 5V 2.5W polikristályos panel

Paraméterek:

* 5V névleges feszültség
* 500mA maximális áram
* 2.5W teljesítmény

Tervezési megjegyzések:

* Téli időszakban csökkent teljesítmény várható
* Árnyékolás jelentősen rontja a hatásfokot
* Optimális dőlésszög ajánlott

---

## Töltésvezérlés

### CN3791 MPPT modul

Feladata:

* Napelemes töltés optimalizálása
* Li-Ion akkumulátor kezelése
* MPPT töltésvezérlés

Előnyök:

* Hatékonyabb töltés változó fényviszonyok mellett
* Stabilabb energiaellátás
* Jobb rendszerhatásfok

---

## Adattárolás

### microSD modul

Feladat:

* Mérési adatok tárolása
* Hosszú távú adatnaplózás

Kommunikáció:

* SPI

Tervezési megjegyzések:

* SD íráskor nagyobb áramfelvétel jelentkezik
* Ajánlott pufferkondenzátor használata
* Sleep módban leválasztható tápellátás ajánlott

---

# Energiafogyasztási stratégia

## V1 működési mód

Az IPAS V1 jelenlegi verziójában a deep sleep funkció még nincs bekapcsolva.

A rendszer folyamatos működésre van tervezve a fejlesztési és tesztelési időszak alatt.

A cél a következők stabil tesztelése:

* Szenzor kommunikáció
* SD kártya adatmentés
* Tápellátás stabilitása
* Napelemes töltés
* Akkumulátor viselkedés
* Hosszú távú működés

A folyamatos működés egyszerűbb hibakeresést és stabilabb fejlesztési környezetet biztosít a korai prototípus fázisban.

---

## Tervezett energiaoptimalizálás

A deep sleep támogatás hardveresen rendelkezésre áll az ESP32-C3 platformon, azonban a funkció csak későbbi szoftververzióban kerül aktiválásra.

A későbbi verziókban várható funkciók:

* Időszakos mérési ciklusok
* Deep sleep mód
* Automatikus ébresztés
* Alacsony fogyasztású üzemmód
* Intelligens energiafelügyelet

A deep sleep implementáció célja:

* Hosszabb akkumulátor üzemidő
* Stabilabb téli működés
* Kisebb átlagos energiafogyasztás
* Hatékonyabb napelemes üzem

---

# Tervezett GPIO kiosztás

| Funkció    | GPIO   |
| ---------- | ------ |
| BME680 SDA | GPIO 8 |
| BME680 SCL | GPIO 9 |
| SD CS      | GPIO 7 |
| SD MOSI    | GPIO 6 |
| SD MISO    | GPIO 5 |
| SD SCK     | GPIO 4 |
| Akku mérés | GPIO 0 |

A végleges kiosztás prototípus tesztelés során módosulhat.

---

# Akku feszültségmérés

## Cél

Az akkumulátor állapotának monitorozása.

## Megvalósítás

Feszültségosztó használata:

* 100kΩ
* 100kΩ

Az osztott feszültség ADC bemenetre kerül.

---

# Mechanikai kialakítás

## Követelmények

A háznak biztosítania kell:

* Eső elleni védelmet
* UV állóságot
* Szellőzést
* Kondenzáció csökkentését
* Szenzor légáramlását
* Rovarvédelmet

---

# Szoftver architektúra

## Fő modulok

| Modul            | Funkció             |
| ---------------- | ------------------- |
| Sensor Manager   | Szenzorok kezelése  |
| Power Manager    | Energiafelügyelet   |
| SD Logger        | Adatmentés          |
| Sleep Controller | Deep sleep vezérlés |
| Error Handler    | Hibakezelés         |

---

# Adatformátum

## CSV naplózás

Példa:

```csv
2026-05-17 12:00:00,24.1,58.2,1008.4,120
```

Adatok sorrendje:

1. Időbélyeg
2. Hőmérséklet
3. Páratartalom
4. Légnyomás
5. VOC index

---

# Tervezett jövőbeli fejlesztések

## IPAS V2

Tervezett fejlesztések:

* PM2.5 / PM10 szenzor
* RTC modul
* OTA frissítés
* Webes dashboard
* MQTT kommunikáció
* Saját PCB
* Jobb energiahatékonyság
* Hosszabb üzemidő
* Külső antenna

---

# Kockázatok és problémák

## Energiahiány

Lehetséges okok:

* Téli időszak
* Árnyékolás
* Túl gyakori mérés
* Magas Wi-Fi használat

Megoldások:

* Hosszabb sleep idő
* Ritkább adatmentés
* Nagyobb napelem
* Nagyobb akkumulátor

---

## Szenzor torzítás

Lehetséges okok:

* Napfény
* Rossz szellőzés
* Elektronikai melegedés

Megoldások:

* Árnyékolt szenzorház
* Távolság az ESP32-től
* Passzív légáramlás

---

# Tesztelési terv

## Elektronikai tesztek

* Tápfeszültség stabilitás
* SD írás stabilitás
* Folyamatos működés stabilitás
* Töltési folyamat
* Szenzor kommunikáció

---

## Kültéri tesztek

* Hőmérséklet viselkedés
* Esőállóság
* Napelemes töltés
* Akkumulátor üzemidő
* Szenzor pontosság

---

# Projekt cél

Az IPAS V1 célja:

* Beágyazott rendszerek tanulása
* Energiahatékony IoT rendszer fejlesztése
* Szenzorhálózatok megismerése
* Környezeti adatgyűjtés
* Hosszú távon bővíthető platform létrehozása

---

# Verzióinformáció

| Verzió  | Állapot                      |
| ------- | ---------------------------- |
| IPAS V0 | Korai prototípus             |
| IPAS V1 | Első működő autonóm rendszer |
| IPAS V2 | Továbbfejlesztett platform   |

---

# Összegzés

Az IPAS V1 egy alacsony fogyasztású, autonóm időjárás-megfigyelő rendszer prototípusa. A projekt célja egy stabil, bővíthető és energiahatékony kültéri mérőállomás létrehozása.

A rendszer fejlesztése során kiemelt szempont:

* energiahatékonyság
* moduláris felépítés
* hosszú távú adatgyűjtés
* kültéri megbízhatóság
* jövőbeli bővíthetőség
