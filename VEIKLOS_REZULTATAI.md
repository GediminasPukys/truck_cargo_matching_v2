# Veiklos Nr. 3 Rezultatai: Automatizuotos krovinių maršrutų sandorių analizės sistemos maketas

## Veiklos aprašymas
Pagal InoBranda verslo planą, Veikloje Nr. 3 buvo atlikta:
- Automatizuotos krovinių maršrutų sandorių analizės sistemos maketo projektavimas
- Automatizuotos krovinių maršrutų sandorių analizės sistemos maketo realizavimas
- Automatizuotos krovinių maršrutų sandorių analizės sistemos maketo eksperimentinis tyrimas su sintetiniais duomenimis

## Pateikiami veiklos rezultatai

### 1. Realizuotas maketas

**Maketo struktūra ir komponentai:**

```
truck_cargo_matching_v2/
├── streamlit_app.py              # Vartotojo sąsajos realizacija
├── utils/
│   ├── time_cost_calculator.py   # Optimizavimo algoritmai
│   ├── route_planner.py          # Maršrutų planavimo modulis
│   ├── visualization.py          # Vizualizacijos komponentai
│   └── data_loader.py           # Duomenų valdymo modulis
├── run_experiment.py            # Eksperimento vykdymo skriptas
├── analyzer.py                  # Rezultatų analizės įrankis
└── data_sample/                 # Sintetiniai duomenys
    ├── trucks.csv              # 54 sunkvežimių duomenys
    └── cargos.csv              # 229 krovinių duomenys
```

**Pagrindinės maketo funkcijos:**
- Automatinis krovinių priskyrimas sunkvežimiams
- Kaštų optimizavimas (atstumas + laukimo laikas)
- Maršrutų planavimas su ES vairavimo taisyklėmis
- Interaktyvi vizualizacija ir rezultatų analizė

### 2. Parengta ataskaita

**Ataskaitos turinys atitinka visus reikalavimus:**

#### 2.1. Dokumentuotas maketas
- Detali sistemos architektūros dokumentacija
- Visų modulių funkcijų aprašymai
- Duomenų struktūrų specifikacijos
- Techniniai parametrai ir konfigūracijos

#### 2.2. Įvertintas maketo efektyvumas su sintetiniais duomenimis

**Eksperimento rezultatai:**
- Ištestuota su 54 sunkvežimiais ir 229 kroviniais
- Priskyrimo sėkmės rodiklis: 17.9% (41 iš 229)
- Optimizacijos efektyvumas: 7,382.12 EUR bendra kaina
- Skaičiavimo našumas: < 5 sekundės

**Parametrų jautrumo analizė:**
- Atstumo limito įtaka (200-350 km diapazone)
- Laukimo laiko limito įtaka (12-48 val. diapazone)
- Maršrutų planavimo efektyvumas

#### 2.3. Pateiktos rekomendacijos prototipo kūrimui

**Techninės rekomendacijos:**
1. Daugiakriterinio optimizavimo įdiegimas
2. Dinaminio perplanavimo galimybės
3. Realaus laiko duomenų integracija
4. Mikroservisų architektūros perėjimas

**Verslo rekomendacijos:**
1. Atstumo limito didinimas iki 300-350 km
2. Perkrovimo taškų sistemos sukūrimas
3. Partnerysčių tinklo formavimas
4. Diferencijuotos kainodaros strategija

**Funkcionalumo plėtros rekomendacijos:**
1. Mobilioji aplikacija
2. Realaus laiko stebėjimas
3. KPI analizės įrankiai
4. Krovinių konsolidavimo funkcijos

## Pristatomi failai

### Pagrindiniai dokumentai:
1. **EKSPERIMENTO_ATASKAITA.md** - Pilna ataskaita lietuvių kalba (atitinka verslo plano reikalavimus)
2. **EXPERIMENT_DOCUMENTATION.md** - Detali techninė dokumentacija anglų kalba
3. **EXPERIMENT_DELIVERABLES.md** - Visų rezultatų suvestinė

### Eksperimento rezultatai:
1. **experiment_results/** - Visi eksperimento duomenys
   - experiment_results_20250725_233953.json
   - assignments_20250725_233953.csv
   - experiment_report_20250725_233953.md

### Vizualizacijos:
1. **experiment_results/plots/** - Grafikai ir diagramos
   - distance_sensitivity.png
   - waiting_time_sensitivity.png
   - cost_distribution.png
   - distance_vs_waiting.png
   - rejection_reasons.png
   - route_planning_efficiency.png

### Programinis kodas:
1. Pilnai funkcionalus maketas (visi .py failai)
2. Eksperimento vykdymo skriptai
3. Vizualizacijų generavimo įrankiai

## Išvada

Veikla Nr. 3 "Automatizuotos krovinių maršrutų sandorių analizės sistemos maketo sukūrimas" sėkmingai įvykdyta. Visi planuoti rezultatai pasiekti:

✓ Realizuotas funkcionalus maketas  
✓ Atliktas eksperimentinis tyrimas su sintetiniais duomenimis  
✓ Parengta išsami ataskaita su dokumentacija  
✓ Įvertintas maketo efektyvumas  
✓ Pateiktos konkrečios rekomendacijos prototipo kūrimui  

Maketas patvirtina automatizuotos krovinių maršrutų optimizacijos galimybes ir paruošia pagrindą tolimesniam prototipo kūrimui.

---
*Dokumentą parengė: InoBranda projekto grupė*  
*Data: 2024 m. lapkričio 25 d.*