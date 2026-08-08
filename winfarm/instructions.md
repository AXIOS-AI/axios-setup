# Istruzioni Business — Farmacia Winfarm

## Database
Database Winfarm farmacia su SQLite (~8.9 GB, 286 tabelle) accessibile via DuckDB+SQLite bridge.

## Tabelle principali

| Modello | Descrizione |
|---------|-------------|
| `anapro` | Anagrafica Prodotti (4.4M righe). Catalogo completo dei prodotti in farmacia. |
| `magazzino` | Giacenze e stock per prodotto. Collegato ad anapro via KM10. |
| `anaforn` | Anagrafica Fornitori |
| `anagr` | Anagrafica Clienti |
| `anaforn` | Anagrafica Fornitori |
| `medici` | Anagrafica Medici |
| `lg_testa` | Vendite — testata (intestazione scontrino/fattura) |
| `lg_righe` | Vendite — righe (prodotti venduti) |
| `ord_testa` | Ordini a grossisti — testata |
| `ord_righe` | Ordini a grossisti — righe |
| `ricettex` | Ricette mediche — testata |
| `righe_ricettex` | Ricette mediche — righe |
| `nre_testa` | Ricette NRE (Numero Ricetta Elettronica) — testata |
| `nre_righe` | Ricette NRE — righe |
| `sospesi` | Ordini in sospeso |
| `giostat` | Statistiche vendite |
| `prontuario` | Farmaci in prontuario SSN |
| `circolari_bd` | Promozioni e circolari |

## Relazioni chiave

- `magazzino.km10` → `anapro.km10` (giacenze → prodotto)
- `lg_righe.km10` → `anapro.km10` (vendite → prodotto)
- `lg_righe.cod_testa` → `lg_testa.codice` (riga → testata vendita)
- `lg_testa.cod_anag` → `anagr.codice` (vendita → cliente)
- `ord_righe.km10` → `anapro.km10` (ordini → prodotto)
- `ord_righe.cod_testa` → `ord_testa.codice` (riga → testata ordine)
- `ricettex.cod_medico` → `medici.codice` (ricetta → medico)
- `righe_ricettex.km10` → `anapro.km10` (ricetta → prodotto)
- `righe_ricettex.cod_testa` → `ricettex.codice` (riga → testata ricetta)
- `prontuario.km10` → `anapro.km10` (prontuario → prodotto)

## Colonne importanti

- **KM10**: Codice prodotto univoco (stringa, chiave principale in ANAPRO)
- **KEAN**: Codice EAN/barcode a 13 cifre
- **KDES**: Descrizione prodotto
- **GIAC_TOTALE**: Giacenza totale = GIAC_MAG1 + GIAC_MAG2 + GIAC_FARM
- **PREZZO**: Prezzo di vendita (in Euro, IVA inclusa)
- **CODICE**: Chiave primaria nelle tabelle testata (LG_TESTA, ORD_TESTA, ecc.)

## Regole business

1. KM10 è la chiave di join universale per i prodotti in tutte le tabelle
2. I prezzi sono in Euro con IVA inclusa salvo diversa indicazione
3. Le giacenze: GIAC_TOTALE = GIAC_MAG1 + GIAC_MAG2 + GIAC_FARM
4. Una riga di vendita (LG_RIGHE) appartiene a una testata (LG_TESTA) via COD_TESTA → CODICE
5. Le ricette possono essere SSN (NRE) o libere (RICETTEX)
6. Data convention: formato DATE nelle tabelle SQLite
