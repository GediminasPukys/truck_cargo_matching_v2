# 4.9. Krovinių maršrutų suderinamumo analizės ir automatizavimo platformos maketo algoritmo eksperimentinis tyrimas su sintetiniais duomenimis

**Data:** 2024 m. lapkričio 25 d.  
**Parengė:** InoBranda tyrimų grupė  
**Projektas:** Automatizuotos krovinių maršrutų sandorių analizės sistema  
**Dokumento versija:** 1.0

## Santrauka

Ši ataskaita yra MTEP projekto "Krovinių maršrutų suderinamumo analizės ir automatizavimo platforma" dalis, atitinkanti MTEP ataskaitos (2025-06-12) 4.9 skyrių. Eksperimentinio tyrimo metu buvo sukurtas ir ištestuotas automatizuotos krovinių maršrutų sandorių analizės sistemos maketas su sintetiniais duomenimis. Tyrimas apėmė 54 sunkvežimių ir 229 krovinių priskyrimo optimizavimą, naudojant tiesinį priskyrimo algoritmą (Vengrų algoritmą). Rezultatai parodė 17.9% priskyrimo sėkmės rodiklį su vidutine 180.05 EUR kaina vienam priskyrimui.

## 1. Įvadas

### 1.1. Tyrimo kontekstas ir metodologija

Šis eksperimentinis tyrimas atliktas vadovaujantis MTEP projekto metodologija, aprašyta dokumente "MTEP_ataskaita_NFQ 2025-06-12". Tyrimas yra projekto "Krovinių maršrutų suderinamumo analizės ir automatizavimo platforma" sudedamoji dalis, skirta įvertinti algoritminių sprendimų efektyvumą realiose verslo situacijose.

### 1.2. Tyrimo tikslas
Sukurti ir eksperimentiškai išbandyti automatizuotos krovinių maršrutų sandorių analizės sistemos maketo algoritmą su sintetiniais duomenimis, siekiant:
- Įvertinti priskyrimo optimizavimo algoritmo efektyvumą
- Nustatyti parametrų jautrumo ribas
- Pagrįsti technologinį sprendimą tolimesniam prototipo kūrimui

### 1.3. Tyrimo uždaviniai
1. Suprojektuoti ir realizuoti optimizavimo algoritmo maketą
2. Sugeneruoti reprezentatyvius sintetinius duomenis
3. Atlikti eksperimentinius bandymus su skirtingais parametrais
4. Įvertinti algoritmo našumą ir efektyvumą
5. Vizualizuoti ir interpretuoti rezultatus
6. Pateikti rekomendacijas prototipo kūrimui

### 1.4. Tyrimo metodologija

Eksperimentinis tyrimas atliktas taikant kiekybinės analizės metodus:
- **Optimizavimo metodas**: Tiesinės priskyrimo problema (Linear Assignment Problem)
- **Algoritmas**: Vengrų algoritmas (Kuhn-Munkres algoritmas)
- **Duomenų tipas**: Sintetiniai duomenys, atspindintys realias Europos krovinių pervežimo situacijas
- **Vertinimo kriterijai**: Kaštų minimizavimas, priskyrimo sėkmės rodiklis, skaičiavimo našumas
- **Statistinė analizė**: Parametrų jautrumo analizė, aprašomoji statistika

## 2. Teorinis pagrindas

### 2.1. Algoritmo pasirinkimo pagrindimas

#### 2.1.1. Kodėl pasirinktas Vengrų (Hungarian) algoritmas?

Vengrų algoritmas pasirinktas remiantis šiais kriterijais:

1. **Optimalumo garantija**: Algoritmas garantuoja globaliai optimalų sprendimą tiesinės priskyrimo problemai, o ne tik lokalų optimumą.

2. **Polinominis sudėtingumas**: O(n³) laiko sudėtingumas yra praktiškai priimtinas iki 1000-5000 objektų, kas atitinka tipišką Lietuvos logistikos įmonės poreikį.

3. **Matematinis pagrįstumas**: Algoritmas paremtas dualumo teorija ir kombinatorine optimizacija, užtikrinant sprendimo stabilumą.

4. **Praktinis pritaikomumas**: Plačiai naudojamas logistikos sektoriuje (UPS, FedEx, DHL) baziniams priskyrimo uždaviniams.

5. **Paprastumas**: Lengvai suprantamas ir modifikuojamas specifiniams verslo poreikiams.

#### 2.1.2. Alternatyvų analizė

| Algoritmas | Privalumai | Trūkumai | Tinkamumas |
|------------|------------|----------|------------|
| **Vengrų algoritmas** | Optimalus, greitas mažiems duomenims | Netinka dinaminiam perplanavimui | ✓ Maketo fazei |
| **Genetiniai algoritmai** | Lankstūs sudėtingiems apribojimams | Negarantuoja optimalumo | ✗ Per sudėtingi maketui |
| **Tabu paieška** | Geri rezultatai dideliems duomenims | Reikalauja parametrų derinimo | ✗ Per daug konfigūracijos |
| **Auction algoritmas** | Tinka realaus laiko sistemoms | Sudėtingesnis įgyvendinimas | → Būsimam prototipui |

### 2.2. Praktiniai iššūkiai realioje logistikoje

Remiantis MTEP tyrimo rezultatais ir rinkos analize, identifikuoti šie pagrindiniai praktiniai iššūkiai:

#### 2.2.1. Dinamiškumo problema
- **Iššūkis**: Realūs kroviniai atsiranda dinamiškai, o ne statiškai
- **Poveikis**: Reikia nuolatinio perplanavimo
- **Sprendimas prototipe**: Realaus laiko integracija su krovinių biržomis

#### 2.2.2. Maršruto kompleksiškumas
- **Iššūkis**: Realūs keliai nėra tiesios linijos (spūstys, apylankos, kelio darbai)
- **Poveikis**: Faktinis atstumas 15-30% didesnis nei tiesinis
- **Sprendimas prototipe**: Integracija su kelių API (Google Maps, HERE)

#### 2.2.3. Kaštų modelio realumas
- **Iššūkis**: Kaštai priklauso nuo daugelio kintamųjų (kuras, muitai, kelių mokesčiai)
- **Poveikis**: Supaprastintas modelis duoda netikslias prognozes
- **Sprendimas prototipe**: Daugiafaktorinis kaštų modelis

#### 2.2.4. Vairuotojų darbo režimas
- **Iššūkis**: EU 561/2006 taisyklės, savaitiniai/mėnesiniai limitai
- **Poveikis**: Papildomi apribojimai priskyrimams
- **Sprendimas prototipe**: Pilnas tachografo duomenų integravimas

#### 2.2.5. Krovinių heterogeniškumas
- **Iššūkis**: Dalinis pakrovimas, konsolidacija, prioritetai
- **Poveikis**: Ne visi kroviniai vienodai svarbūs
- **Sprendimas prototipe**: Daugiatikslis optimizavimas

### 2.3. Tiesinės priskyrimo problemos formulavimas

Krovinių ir sunkvežimių priskyrimo problema matematiškai aprašoma kaip:

```
Minimizuoti: Σᵢⱼ cᵢⱼ × xᵢⱼ
Apribojimai:
- Σⱼ xᵢⱼ ≤ 1 ∀i (kiekvienas sunkvežimis priskirtas daugiausiai vienam kroviniui)
- Σᵢ xᵢⱼ ≤ 1 ∀j (kiekvienas krovinys priskirtas daugiausiai vienam sunkvežimiui)
- xᵢⱼ ∈ {0,1}
```

Kur:
- cᵢⱼ - kaštai priskiriant sunkvežimį i kroviniui j
- xᵢⱼ - dvejetainis kintamasis (1 jei priskiriama, 0 priešingu atveju)

### 2.4. Kaštų funkcijos struktūra

Bendra kaštų funkcija:
```
C_total = C_distance + C_waiting
```

Kur:
- C_distance = atstumas × kaina_už_km
- C_waiting = laukimo_valandos × laukimo_kaina_už_valandą

## 3. Maketo realizacija

### 3.1. Sistemos architektūra

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

### 3.2. Pagrindiniai komponentai

#### 3.2.1. Optimizavimo modulis (time_cost_calculator.py)
- **Algoritmas:** scipy.optimize.linear_sum_assignment (Vengrų algoritmas)
- **Tikslo funkcija:** Minimizuoti bendrą kainą (atstumas + laukimo laikas)
- **Apribojimai:**
  - Maksimalus atstumas: 250 km (konfigūruojamas)
  - Maksimalus laukimo laikas: 24 val. (konfigūruojamas)
  - Tipų atitikimas (General/Frozen/Liquid)

#### 3.2.2. Maršrutų planavimo modulis (route_planner.py)
- **Funkcionalumas:** Daugiakrypčių maršrutų planavimas
- **ES reguliacijos:** Automatinis poilsio pertraukų skaičiavimas
  - Nepertraukiamas vairavimas: maks. 4.5 val.
  - Poilsio trukmė: 45 min.
  - Dienos vairavimo limitas: 9 val.

#### 3.2.3. Vartotojo sąsaja (streamlit_app.py)
- **Technologija:** Streamlit framework
- **Funkcijos:**
  - Duomenų įkėlimas (CSV formatai)
  - Parametrų konfigūravimas
  - Rezultatų vizualizacija
  - Interaktyvūs žemėlapiai (Folium)

### 3.3. Duomenų struktūra

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

## 4. Eksperimentinio tyrimo rezultatai

### 4.1. Eksperimento parametrai

**Duomenų apimtis:**
- Sunkvežimių skaičius: 54
- Krovinių skaičius: 229
- Geografinė aprėptis: Europos miestai
- Laiko horizontas: 2 dienos (2024-11-24/25)

**Numatytieji parametrai:**
- Maksimalus atstumas: 250 km
- Maksimalus laukimo laikas: 24 val.
- Standartinis greitis: 73 km/h

### 4.2. Pagrindiniai rezultatai

#### 4.2.1. Priskyrimo efektyvumas
- **Sėkmingi priskyrimai:** 41 iš 229 (17.9%)
- **Bendra kaina:** 7,382.12 EUR
- **Bendras atstumas:** 5,254.39 km
- **Bendras laukimo laikas:** 212.77 val.
- **Vidutinė kaina vienam priskyrimui:** 180.05 EUR

#### 4.2.2. Kaštų pasiskirstymas

![Kaštų pasiskirstymas](legacy/experiment_results/plots/cost_distribution.png)
*1 pav. Priskyrimo kaštų pasiskirstymo histograma*

Kaštų pasiskirstymas rodo, kad dauguma priskyrimų kainuoja tarp 100-200 EUR, su vidurkiu 180.05 EUR. Pastebimas nedidelis skaičius brangesnių priskyrimų (>300 EUR), kurie susiję su ilgesniu laukimo laiku.

#### 4.2.3. Atmetimo priežasčių analizė

![Atmetimo priežastys](legacy/experiment_results/plots/rejection_reasons.png)
*2 pav. Atmetimo priežasčių pasiskirstymas*

| Priežastis | Kiekis | Procentas |
|------------|--------|-----------|
| Per didelis atstumas | 4,185 | 98.0% |
| Per ilgas laukimo laikas | 27 | 0.6% |
| Laiko langas | 61 | 1.4% |
| **Viso atmesta** | 4,273 | 100% |

### 4.3. Parametrų jautrumo analizė

#### 4.3.1. Atstumo limito įtaka

![Atstumo jautrumo analizė](legacy/experiment_results/plots/distance_sensitivity.png)
*3 pav. Priskyrimo skaičiaus ir kaštų priklausomybė nuo maksimalaus atstumo*

| Maks. atstumas (km) | Priskyrimai | Sėkmės rodiklis | Bendra kaina (EUR) |
|--------------------|-------------|-----------------|-------------------|
| 200 | 36 | 15.7% | 5,900.25 |
| 250 | 41 | 17.9% | 7,382.12 |
| 300 | 52 | 22.7% | 10,891.89 |
| 350 | 54 | 23.6% | 11,664.98 |

**Išvada:** Didinant atstumo limitą nuo 200 iki 350 km, priskyrimo sėkmė padidėja 50%, tačiau kaina padvigubėja.

#### 4.3.2. Laukimo laiko limito įtaka

![Laukimo laiko jautrumo analizė](legacy/experiment_results/plots/waiting_time_sensitivity.png)
*4 pav. Priskyrimo skaičiaus priklausomybė nuo maksimalaus laukimo laiko*

| Maks. laukimas (val.) | Priskyrimai | Sėkmės rodiklis | Bendra kaina (EUR) |
|----------------------|-------------|-----------------|-------------------|
| 12 | 38 | 16.6% | 6,503.04 |
| 24 | 41 | 17.9% | 7,382.12 |
| 36 | 42 | 18.3% | 7,721.73 |
| 48 | 42 | 18.3% | 7,721.73 |

**Išvada:** Laukimo laiko didinimas virš 36 val. neduoda papildomos naudos.

#### 4.3.3. Atstumo ir laukimo laiko sąryšis

![Atstumo ir laukimo laiko sąryšis](legacy/experiment_results/plots/distance_vs_waiting.png)
*5 pav. Atstumo ir laukimo laiko tarpusavio priklausomybė priskyrimuose*

Scatter diagrama atskleidžia, kad didžioji dalis priskyrimų turi minimalų laukimo laiką, o brangesni priskyrimai (tamsesnė spalva) dažnai susiję su ilgesniu laukimo laiku arba didesniu atstumu.

### 4.4. Maršrutų planavimo rezultatai

![Maršrutų efektyvumas](legacy/experiment_results/plots/route_planning_efficiency.png)
*6 pav. Daugiakrypčių maršrutų pristatymų skaičius ir efektyvumas*

| Sunkvežimis | Pristatymai | Atstumas (km) | Poilsio stotelės |
|-------------|-------------|---------------|------------------|
| 1 | 2 | 321.2 | 0 |
| 2 | 5 | 729.7 | 1 |
| 3 | 8 | 978.3 | 2 |
| 4 | 6 | 1014.8 | 2 |
| 5 | 8 | 814.4 | 2 |

**Vidutiniškai:** 5.8 pristatymo vienam sunkvežimiui

## 5. Maketo efektyvumo įvertinimas

### 5.1. Techniniai rodikliai

**Našumas:**
- Skaičiavimo trukmė: ~5 sekundės pilnam optimizavimui
- Atminties naudojimas: < 100 MB
- Algoritmo sudėtingumas: O(n³)
- Masteliaviamumas: iki 1000 transporto priemonių

**Patikimumas:**
- Visi priskyrimai atitinka nustatytus apribojimus
- Detalus atmetimo priežasčių registravimas
- Sprendimo validavimas

### 5.2. Funkciniai privalumai

1. **Automatizacija:** Pilnai automatizuotas priskyrimo procesas
2. **Optimizavimas:** Garantuoja minimalią bendrą kainą
3. **Lankstumas:** Konfigūruojami parametrai
4. **Vizualizacija:** Interaktyvūs žemėlapiai ir grafikai
5. **ES atitiktis:** Integruotos vairavimo/poilsio taisyklės

### 5.3. Identifikuoti trūkumai

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

## 6. Praktinės rekomendacijos prototipo kūrimui

### 6.1. Kritiniai techniniai patobulinimai

#### 6.1.1. Realaus kaštų modelio įdiegimas
```
Realūs kaštai = Kuro sąnaudos(svoris, greitis, reljefas) + 
                Kelių mokesčiai(maršrutas) + 
                Vairuotojo darbo užmokestis(laikas, viršvalandžiai) +
                Transporto amortizacija + 
                Draudimas + 
                Administracinės išlaidos
```
**Įgyvendinimas:**
- Integruoti kuro sąnaudų API (pvz., Shell Fleet API)
- Kelių mokesčių skaičiuoklė (TollGuru API)
- Darbo laiko apskaitos sistema

#### 6.1.2. Maršruto kompleksiškumo sprendimas
- **Problema**: Tiesinis atstumas ≠ realus atstumas
- **Sprendimas**: 
  - HERE Maps Routing API integracija
  - Google Maps Distance Matrix API
  - Realaus laiko eismo duomenys
  - Istorinių duomenų analizė piko/ne piko valandoms

#### 6.1.3. Dinaminio perplanavimo sistema
```python
# Pseudo-kodas
while sistema_veikia:
    if naujas_krovinys or vėlavimas or gedimas:
        perplanuoti_maršrutus()
        informuoti_vairuotojus()
        atnaujinti_klientus()
```

### 6.2. Verslo procesų integracija

#### 6.2.1. Realių duomenų šaltiniai
1. **Krovinių biržos integracija:**
   - Timocom API
   - Trans.eu integracija  
   - Loads Today duomenų srautas
   - Realaus laiko krovinių monitoringas

2. **Transporto priemonių telematika:**
   - GPS pozicijos (Wialon, Mapon)
   - Tachografo duomenys (VDO, Stoneridge)
   - Kuro sąnaudų monitoringas
   - Techninės būklės stebėjimas

3. **Išorinės sistemos:**
   - ERP integracija (SAP, Navision)
   - WMS sąsaja sandėliams
   - CMR/eCMR dokumentų valdymas
   - Elektroninės sąskaitos

#### 6.2.2. Praktinių apribojimų valdymas

**Vairuotojų darbo režimas (pilnas modelis):**
```
- Dienos vairavimas: max 9h (10h 2x/savaitę)
- Savaitės vairavimas: max 56h
- 2 savaičių vairavimas: max 90h
- Nepertraukiamas vairavimas: max 4.5h
- Pertrauka: min 45min (arba 15+30min)
- Dienos poilsis: min 11h (9h 3x/savaitę)
- Savaitės poilsis: 45h (24h kas antrą savaitę)
```

### 6.3. Konkrečios įgyvendinimo rekomendacijos

#### 6.3.1. MVP (Minimum Viable Product) fazė
1. **Bazinė integracija** (1-2 mėn.):
   - Vienos krovinių biržos API
   - Google Maps maršrutizacija
   - Paprastas kaštų modelis
   - Web aplikacija

2. **Pilotinis testavimas** (2-3 mėn.):
   - 5-10 transporto priemonių
   - Viena geografinė zona (pvz., Lietuva-Lenkija)
   - Rankinis duomenų papildymas
   - Rezultatų matavimas

3. **Plėtra** (3-6 mėn.):
   - Automatinis duomenų srautas
   - Mobili aplikacija vairuotojams
   - Platesnis geografinis regionas
   - Dinaminis perplanavimas

#### 6.3.2. Rizikų valdymas
| Rizika | Tikimybė | Poveikis | Prevencija |
|--------|----------|----------|------------|
| API gedimai | Vidutinė | Didelis | Duomenų kešavimas, backup API |
| Netikslūs duomenys | Didelė | Vidutinis | Validacijos taisyklės, ML anomalijų aptikimas |
| Vairuotojų pasipriešinimas | Vidutinė | Didelis | Mokymai, paprastas UI, motyvacijos sistema |
| Konkurentų reakcija | Maža | Vidutinis | Greitas MVP, unikalūs funkcionalumai |

#### 6.3.3. Matavimo kriterijai (KPI)
1. **Techniniai:**
   - Priskyrimo sėkmės rodiklis (tikslas: >40%)
   - Vidutinis skaičiavimo laikas (<10s)
   - Sistema prieinamumas (>99.5%)

2. **Verslo:**
   - Tuščios ridos sumažinimas (>15%)
   - Vidutinė marža/km padidėjimas (>10%)
   - Vairuotojų pasitenkinimas (NPS >50)

3. **Operaciniai:**
   - Laiku pristatytų krovinių % (>95%)
   - Vidutinis laukimo laikas (<2h)
   - Maršruto nukrypimų skaičius (<5%)

### 6.4. Investicijų poreikis

#### 6.4.1. Pradinės investicijos (MVP)
- Programinės įrangos kūrimas: 40,000-60,000 EUR
- API licencijos: 500-1,000 EUR/mėn
- Infrastruktūra: 200-500 EUR/mėn
- Testavimas ir diegimas: 10,000-15,000 EUR

#### 6.4.2. Grąžos skaičiavimas
```
Metinė nauda = (Sutaupytos tuščios ridos km × 0.5 EUR/km) +
               (Papildomi kroviniai × vidutinė marža) +
               (Sumažintas administravimo laikas × valandinis tarifas)

ROI = (Metinė nauda - Metinės išlaidos) / Pradinė investicija × 100%
Atsipirkimo laikas: 12-18 mėn.
```

## 7. Išvados

1. **Maketo sėkmė:** Automatizuotos krovinių maršrutų sandorių analizės sistemos maketas sėkmingai realizuotas ir ištestuotas su sintetiniais duomenimis.

2. **Efektyvumas:** Sistema efektyviai optimizuoja priskyrimus nustatytų apribojimų rėmuose, tačiau reikalingi operaciniai patobulinimai didesnei aprėpčiai.

3. **Potencialas:** Maketas demonstruoja didelį potencialą realaus pasaulio taikymui su atitinkamais patobulinimais.

4. **Tolimesni žingsniai:** Rekomenduojama pereiti prie prototipo kūrimo, integruojant realius duomenis ir plečiant funkcionalumą.

## 8. Tyrimo atitikimas MTEP metodologijai

### 8.1. Metodologinė atitiktis

Šis eksperimentinis tyrimas atliktas griežtai laikantis MTEP projekto metodologijos:

1. **Eksperimentinis tyrimas**: Atitinka MTEP metodologijos 4.9 skyriaus reikalavimus eksperimentiniams tyrimams su sintetiniais duomenimis
2. **Inovatyvumas**: Naujas algoritmas krovinių-sunkvežimių priskyrimo optimizavimui Lietuvos kontekste
3. **Praktinis pritaikomumas**: Tiesiogiai taikomas logistikos sektoriuje
4. **Mokslinis pagrįstumas**: Naudojami pripažinti optimizavimo metodai (Vengrų algoritmas)

### 8.2. Rezultatų verifikavimas

Tyrimo rezultatai verifikuoti pagal šiuos kriterijus:
- **Atkartojamumas**: Visi eksperimentai dokumentuoti ir gali būti atkartoti
- **Validumas**: Rezultatai atitinka teorinius lūkesčius
- **Patikimumas**: Stabilus veikimas su skirtingais parametrais

## Priedai

### A. Techninė specifikacija
- Programavimo kalba: Python 3.10
- Pagrindinės bibliotekos: pandas, numpy, scipy, streamlit, folium
- Optimizavimo algoritmas: scipy.optimize.linear_sum_assignment
- Vizualizacija: Folium žemėlapiai, Matplotlib grafikai

### B. Eksperimento duomenys
Visi eksperimento duomenys ir rezultatai saugomi:
- `experiment_results/` - rezultatų failai
- `experiment_results/plots/` - vizualizacijos (1-6 pav.)
- `EXPERIMENT_DOCUMENTATION.md` - detali dokumentacija anglų kalba

### C. Statistinė suvestinė
- Vidutinis priskyrimo kaštas: 180.05 EUR (σ = 90.08)
- Medianas: 176.38 EUR
- Min/Max: 3.81 / 383.78 EUR
- Vidutinis atstumas: 125.69 km
- Vidutinis laukimo laikas: 5.82 val.

### D. Literatūra ir šaltiniai
1. MTEP_ataskaita_NFQ 2025-06-12 - Projekto metodologija
2. Kuhn, H.W. (1955). "The Hungarian method for the assignment problem"
3. EU Regulation (EC) No 561/2006 - Vairavimo ir poilsio laikai

---
*Ataskaitą parengė: InoBranda tyrimų grupė*  
*Data: 2024 m. lapkričio 25 d.*  
*Ataskaita yra MTEP projekto "Krovinių maršrutų suderinamumo analizės ir automatizavimo platforma" dalis*