# Automatizuotos krovinių maršrutų sandorių analizės sistemos maketo eksperimentinio tyrimo ataskaita

**Data:** 2024 m. lapkričio 25 d.  
**Parengė:** InoBranda tyrimų grupė  
**Projektas:** Automatizuotos krovinių maršrutų sandorių analizės sistema

## Santrauka

Ši ataskaita pristato automatizuotos krovinių maršrutų sandorių analizės sistemos maketo eksperimentinio tyrimo rezultatus. Maketas buvo sukurtas ir ištestuotas su sintetiniais duomenimis, siekiant įvertinti krovinių ir sunkvežimių priskyrimo optimizavimo galimybes. Eksperimento metu buvo analizuojami 54 sunkvežimiai ir 229 kroviniai, naudojant tiesinį priskyrimo algoritmą (Vengrų algoritmą).

## 1. Įvadas

### 1.1. Tyrimo tikslas
Sukurti ir išbandyti automatizuotos krovinių maršrutų sandorių analizės sistemos maketą, įvertinti jo efektyvumą su sintetiniais duomenimis ir pateikti rekomendacijas prototipo kūrimui.

### 1.2. Tyrimo uždaviniai
1. Suprojektuoti ir realizuoti sistemos maketą
2. Atlikti eksperimentinį tyrimą su sintetiniais duomenimis
3. Įvertinti maketo efektyvumą
4. Pateikti rekomendacijas tolimesniam vystymui

## 2. Maketo dokumentacija

### 2.1. Sistemos architektūra

Maketas realizuotas naudojant modulinę architektūrą:

```
truck_cargo_matching_v2/
├── streamlit_app.py          # Pagrindinis vartotojo sąsajos modulis
├── utils/
│   ├── time_cost_calculator.py   # Optimizavimo algoritmai
│   ├── route_planner.py          # Maršrutų planavimas
│   ├── visualization.py          # Vizualizacijos
│   └── data_loader.py           # Duomenų įkėlimas
├── analyzer.py               # Rezultatų analizė
└── data_sample/             # Sintetiniai duomenys
```

### 2.2. Pagrindiniai komponentai

#### 2.2.1. Optimizavimo modulis (time_cost_calculator.py)
- **Algoritmas:** scipy.optimize.linear_sum_assignment (Vengrų algoritmas)
- **Tikslo funkcija:** Minimizuoti bendrą kainą (atstumas + laukimo laikas)
- **Apribojimai:**
  - Maksimalus atstumas: 250 km (konfigūruojamas)
  - Maksimalus laukimo laikas: 24 val. (konfigūruojamas)
  - Tipų atitikimas (General/Frozen/Liquid)

#### 2.2.2. Maršrutų planavimo modulis (route_planner.py)
- **Funkcionalumas:** Daugiakrypčių maršrutų planavimas
- **ES reguliacijos:** Automatinis poilsio pertraukų skaičiavimas
  - Nepertraukiamas vairavimas: maks. 4.5 val.
  - Poilsio trukmė: 45 min.
  - Dienos vairavimo limitas: 9 val.

#### 2.2.3. Vartotojo sąsaja (streamlit_app.py)
- **Technologija:** Streamlit framework
- **Funkcijos:**
  - Duomenų įkėlimas (CSV formatai)
  - Parametrų konfigūravimas
  - Rezultatų vizualizacija
  - Interaktyvūs žemėlapiai (Folium)

### 2.3. Duomenų struktūra

#### Sunkvežimių duomenys:
- truck_id - unikalus identifikatorius
- truck type - tipas (General/Frozen/Liquid)
- Address (drop off) - iškrovimo vieta
- Latitude/Longitude - koordinatės
- Timestamp (dropoff) - iškrovimo laikas
- avg moving speed - vidutinis greitis (73 km/h)
- price per km - kaina už km (1 EUR)
- waiting time price per h - laukimo kaina (10 EUR/h)

#### Krovinių duomenys:
- Origin - pakrovimo vieta
- Origin_Latitude/Longitude - pakrovimo koordinatės
- Available_From/To - prieinamumo langas
- Delivery_Location - pristatymo vieta
- Delivery_Latitude/Longitude - pristatymo koordinatės
- Cargo_Type - krovinio tipas

## 3. Eksperimentinio tyrimo rezultatai

### 3.1. Eksperimento parametrai

**Duomenų apimtis:**
- Sunkvežimių skaičius: 54
- Krovinių skaičius: 229
- Geografinė aprėptis: Europos miestai
- Laiko horizontas: 2 dienos (2024-11-24/25)

**Numatytieji parametrai:**
- Maksimalus atstumas: 250 km
- Maksimalus laukimo laikas: 24 val.
- Standartinis greitis: 73 km/h

### 3.2. Pagrindiniai rezultatai

#### 3.2.1. Priskyrimo efektyvumas
- **Sėkmingi priskyrimai:** 41 iš 229 (17.9%)
- **Bendra kaina:** 7,382.12 EUR
- **Bendras atstumas:** 5,254.39 km
- **Bendras laukimo laikas:** 212.77 val.
- **Vidutinė kaina vienam priskyrimui:** 180.05 EUR

#### 3.2.2. Atmetimo priežasčių analizė
| Priežastis | Kiekis | Procentas |
|------------|--------|-----------|
| Per didelis atstumas | 4,185 | 98.0% |
| Per ilgas laukimo laikas | 27 | 0.6% |
| Laiko langas | 61 | 1.4% |
| **Viso atmesta** | 4,273 | 100% |

### 3.3. Parametrų jautrumo analizė

#### 3.3.1. Atstumo limito įtaka

| Maks. atstumas (km) | Priskyrimai | Sėkmės rodiklis | Bendra kaina (EUR) |
|--------------------|-------------|-----------------|-------------------|
| 200 | 36 | 15.7% | 5,900.25 |
| 250 | 41 | 17.9% | 7,382.12 |
| 300 | 52 | 22.7% | 10,891.89 |
| 350 | 54 | 23.6% | 11,664.98 |

**Išvada:** Didinant atstumo limitą nuo 200 iki 350 km, priskyrimo sėkmė padidėja 50%, tačiau kaina padvigubėja.

#### 3.3.2. Laukimo laiko limito įtaka

| Maks. laukimas (val.) | Priskyrimai | Sėkmės rodiklis | Bendra kaina (EUR) |
|----------------------|-------------|-----------------|-------------------|
| 12 | 38 | 16.6% | 6,503.04 |
| 24 | 41 | 17.9% | 7,382.12 |
| 36 | 42 | 18.3% | 7,721.73 |
| 48 | 42 | 18.3% | 7,721.73 |

**Išvada:** Laukimo laiko didinimas virš 36 val. neduoda papildomos naudos.

### 3.4. Maršrutų planavimo rezultatai

| Sunkvežimis | Pristatymai | Atstumas (km) | Poilsio stotelės |
|-------------|-------------|---------------|------------------|
| 1 | 2 | 321.2 | 0 |
| 2 | 5 | 729.7 | 1 |
| 3 | 8 | 978.3 | 2 |
| 4 | 6 | 1014.8 | 2 |
| 5 | 8 | 814.4 | 2 |

**Vidutiniškai:** 5.8 pristatymo vienam sunkvežimiui

## 4. Maketo efektyvumo įvertinimas

### 4.1. Techniniai rodikliai

**Našumas:**
- Skaičiavimo trukmė: ~5 sekundės pilnam optimizavimui
- Atminties naudojimas: < 100 MB
- Algoritmo sudėtingumas: O(n³)
- Masteliaviamumas: iki 1000 transporto priemonių

**Patikimumas:**
- Visi priskyrimai atitinka nustatytus apribojimus
- Detalus atmetimo priežasčių registravimas
- Sprendimo validavimas

### 4.2. Funkciniai privalumai

1. **Automatizacija:** Pilnai automatizuotas priskyrimo procesas
2. **Optimizavimas:** Garantuoja minimalią bendrą kainą
3. **Lankstumas:** Konfigūruojami parametrai
4. **Vizualizacija:** Interaktyvūs žemėlapiai ir grafikai
5. **ES atitiktis:** Integruotos vairavimo/poilsio taisyklės

### 4.3. Identifikuoti trūkumai

1. **Žemas priskyrimo rodiklis** (17.9%) dėl:
   - Griežtų atstumo apribojimų
   - Geografinio sunkvežimių/krovinių pasiskirstymo
   - Tipų atitikimo reikalavimų

2. **Statinis optimizavimas:**
   - Nėra dinaminės perplanavimo galimybės
   - Neatsižvelgia į realaus laiko pokyčius

3. **Ribotos galimybės:**
   - Nėra daugiataškių maršrutų optimizavimo
   - Neintegruoti kelių tinklo duomenys

## 5. Rekomendacijos prototipo kūrimui

### 5.1. Techninės rekomendacijos

1. **Algoritmo tobulinimas:**
   - Įdiegti daugiakriterinį optimizavimą
   - Pridėti dinaminį perplanavimą
   - Integruoti mašininio mokymosi prognozes

2. **Infrastruktūros plėtra:**
   - Pereiti prie mikroservisų architektūros
   - Įdiegti realaus laiko duomenų srautus
   - Užtikrinti horizontalų masteliaviamumą

3. **Integracija:**
   - Prijungti realius kelių tinklo duomenis
   - Integruoti su TMS/ERP sistemomis
   - Pridėti API kitų sistemų integracijai

### 5.2. Verslo modelio rekomendacijos

1. **Operaciniai patobulinimai:**
   - Padidinti atstumo limitą iki 300-350 km
   - Įdiegti perkrovimo taškų (hub) sistemą
   - Strategiškai pozicionuoti sunkvežimius

2. **Partnerystės:**
   - Kurti vežėjų tinklus platesnei aprėpčiai
   - Bendradarbiauti su logistikos platformomis
   - Integruoti su krovinių biržomis

3. **Kainodaros strategija:**
   - Diferencijuota kainodara pagal atstumą
   - Premijos už skubius krovinius
   - Dinaminė kainodara pagal paklausą

### 5.3. Funkcionalumo plėtra

1. **Vartotojo patirties gerinimas:**
   - Mobilioji aplikacija vairuotojams
   - Realaus laiko stebėjimo sistema
   - Automatiniai pranešimai

2. **Analitikos plėtra:**
   - KPI stebėjimo skydelis
   - Prognozavimo įrankiai
   - Efektyvumo ataskaitos

3. **Papildomos funkcijos:**
   - Krovinių konsolidavimas
   - Grįžtamųjų reisų optimizavimas
   - CO2 pėdsako skaičiavimas

## 6. Išvados

1. **Maketo sėkmė:** Automatizuotos krovinių maršrutų sandorių analizės sistemos maketas sėkmingai realizuotas ir ištestuotas su sintetiniais duomenimis.

2. **Efektyvumas:** Sistema efektyviai optimizuoja priskyrimus nustatytų apribojimų rėmuose, tačiau reikalingi operaciniai patobulinimai didesnei aprėpčiai.

3. **Potencialas:** Maketas demonstruoja didelį potencialą realaus pasaulio taikymui su atitinkamais patobulinimais.

4. **Tolimesni žingsniai:** Rekomenduojama pereiti prie prototipo kūrimo, integruojant realius duomenis ir plečiant funkcionalumą.

## Priedai

### A. Techninė specifikacija
- Programavimo kalba: Python 3.10
- Pagrindinės bibliotekos: pandas, numpy, scipy, streamlit, folium
- Optimizavimo algoritmas: scipy.optimize.linear_sum_assignment
- Vizualizacija: Folium žemėlapiai, Matplotlib grafikai

### B. Eksperimento duomenys
Visi eksperimento duomenys ir rezultatai saugomi:
- `experiment_results/` - rezultatų failai
- `experiment_results/plots/` - vizualizacijos
- `EXPERIMENT_DOCUMENTATION.md` - detali dokumentacija anglų kalba

### C. Kodo pavyzdžiai
Pilnas kodas prieinamas GitHub repozitorijoje su atitinkama dokumentacija.

---
*Ataskaitą parengė: InoBranda tyrimų grupė*  
*Data: 2024 m. lapkričio 25 d.*