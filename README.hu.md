# IPAS – Intelligens Szennyezés Analitikai Rendszer

## Áttekintés

Az IPAS (Intelligent Pollution Analysis System) egy moduláris környezeti monitorozó rendszer, amely szenzorok segítségével adatokat gyűjt, majd ezeket feldolgozza és megjeleníti.

A projekt célja egy skálázható prototípus létrehozása okosvárosi és környezetkutatási alkalmazásokhoz.

---

## Célok

- Valós idejű környezeti adatgyűjtés
- Szenzor alapú szennyezettség mérése
- Adatfeldolgozás és trendek elemzése
- Levegőminőség vizualizálása
- Moduláris felépítés (IoT / későbbi AI bővítés)

---

## Rendszer felépítése

A rendszer az alábbi részekből áll:

- **Szenzor réteg** – adatgyűjtés (pl. levegőminőség, hőmérséklet, páratartalom)
- **Feldolgozó réteg** – nyers adatok tisztítása és elemzése
- **Tároló réteg** – strukturált adatok mentése
- **Vizualizációs réteg** – grafikonok és megjelenítés

---

## Projekt struktúra
IPAS/
├── README.md
├── README.hu.md
├── CONTRIBUTORS.md
│
├── docs/
│ ├── en/
│ └── hu/
│
├── src/
│ ├── sensors/
│ ├── data_processing/
│ └── visualization/
│
├── hardware/
├── data/
├── tests/
│
├── .gitignore
├── LICENS

---

## Indítás

### Követelmények

- Python 3.x (vagy beágyazott C/C++ a hardverhez)
- `requirements.txt` fájlban lévő függőségek

### Telepítés

```bash
git clone https://github.com/your-repo/IPAS.git
cd IPAS
pip install -r requirements.txt