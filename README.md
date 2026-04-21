# Soddisfazione della vita in Italia: analisi dei predittori 
# socio-demografici e relazionali (R)

## Descrizione del progetto
Analisi statistica dei fattori socio-demografici e relazionali che 
influenzano la soddisfazione di vita della popolazione italiana, 
condotta con R sui microdati ISTAT "Aspetti della vita quotidiana" 
(2023, ~41.750 osservazioni, 708 variabili originali).

Questo progetto è il secondo modulo di un'analisi più ampia che include
una fase preliminare di data cleaning ed esplorazione condotta in SAS

---

## Domanda di ricerca
Quali fattori demografici e relazionali influenzano maggiormente 
il benessere soggettivo degli italiani? Le relazioni interpersonali 
hanno un impatto significativo sulla soddisfazione di vita al netto 
delle variabili demografiche?

---

## Dataset
- **Fonte:** ISTAT – "Aspetti della vita quotidiana" 2023
- **Osservazioni originali:** 41.750 record
- **Variabili selezionate per l'analisi:** 11
- **Variabile dipendente:** VOTOVI (soddisfazione di vita, scala 0–10)

### Variabili analizzate
| Variabile | Descrizione |
|-----------|-------------|
| VOTOVI | Soddisfazione di vita (0–10) — variabile dipendente |
| RELAM | Soddisfazione relazioni con gli amici |
| RELFAM | Soddisfazione relazioni familiari |
| AMICI2 | Presenza di amici su cui contare |
| ETAMi | Classe di età |
| SESSO | Genere |
| ISTRMi | Titolo di studio |
| STCIVMi | Stato civile |
| CONDMi | Condizione professionale |
| REGMf | Regione di residenza |
| FUTUASP | Aspettative sul futuro |

---

## Tecnologie e librerie
- **Linguaggio:** R
- **Librerie:** `dplyr`, `ggplot2`, `readr`, `knitr`, `broom`

---

## Metodologia

### Parte I — Data Cleaning
- Selezione di 11 variabili rilevanti da 708 disponibili
- Identificazione e trattamento dei valori mancanti (NA) e 
  codici non validi ("non disponibile", "non risponde", "non sa")
- Ricodifica dei codici numerici ISTAT in etichette descrittive 
  e fattori ordinati
- Rimozione dei codici aggregati geografici (555, 666, 777, 999) 
  per garantire analisi regionali accurate

### Parte II — Analisi demografica (Regressione Lineare Multipla)
- **Variabile dipendente:** soddisfazione di vita (0–10)
- **Predittori:** sesso, età, titolo di studio, stato civile, 
  condizione professionale
- Ogni coefficiente misura l'effetto isolato di ciascuna variabile 
  rispetto alla propria categoria di riferimento (baseline)

### Parte III — Analisi relazionale (ANOVA e Chi-quadro)
- **ANOVA** per confrontare le medie di soddisfazione di vita tra 
  gruppi definiti dalla qualità delle relazioni con gli amici
- **ANOVA multifattoriale** con soddisfazione relazioni amici, età, 
  titolo di studio e condizione professionale come predittori simultanei
- **Test Chi-quadro** per verificare l'associazione tra soddisfazione 
  di vita categorizzata e qualità delle relazioni amicali

---

## Principali risultati

### Distribuzione della variabile dipendente
- Soddisfazione media: **7,23/10**
- Moda: **8** — distribuzione asimmetrica negativa concentrata 
  sui valori alti
- Pochissime persone completamente insoddisfatte (score 0–2)

### Regressione lineare multipla
- **R² = 0,035** — le variabili demografiche spiegano solo il 3,5% 
  della varianza (predittori deboli del benessere individuale)
- **F = 66,64, p < 2,22e-16** — modello statisticamente significativo
- **34.929 gradi di libertà** — alta affidabilità delle stime

Coefficienti significativi (rispetto alla categoria di riferimento):

| Variabile | Effetto |
|-----------|---------|
| Essere in coppia | +0,38 sulla soddisfazione |
| Disoccupazione | −0,55 rispetto agli occupati |
| Inattività | −0,21 rispetto agli occupati |
| Basso titolo di studio | −0,26 (elementari o nessun titolo) |
| Genere femminile | −0,11 (effetto minimo) |
| Età | Declino progressivo con l'avanzare degli anni |

### ANOVA — Relazioni con gli amici
- **F = 1743, p < 2e-16** — differenza altamente significativa tra gruppi
- Chi è molto soddisfatto delle relazioni amicali ha soddisfazione 
  media di **7,93**; chi non lo è per niente ha media **5,34**

### ANOVA Multifattoriale
Tutti i predittori risultano altamente significativi (p < 2e-16):
- Soddisfazione relazioni amici: F = 1706,97
- Condizione professionale: F = 122,78
- Titolo di studio: F = 14,24
- Età: F = 7,48

### Conclusione chiave
Le variabili demografiche da sole hanno scarso potere predittivo sul 
benessere soggettivo (R² = 3,5%). La qualità delle relazioni 
interpersonali risulta il predittore più forte della soddisfazione 
di vita, suggerendo che fattori come salute, reddito e capitale 
sociale abbiano un peso determinante non catturato dalle sole 
variabili demografiche.

---

## 📌 Note metodologiche
I microdati ISTAT sono pubblici e disponibili sul portale ufficiale.  
Il dataset grezzo non è incluso nel repository per ragioni di dimensione.  
Per riprodurre l'analisi, scaricare il file `AVQ_Microdati_2023.txt` 
da ISTAT e aggiornare il percorso nella prima riga del codice.
