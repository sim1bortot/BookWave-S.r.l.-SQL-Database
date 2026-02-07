
che consenta di:

- memorizzare clienti, libri e ordini
- associare più libri a ogni ordine
- associare ogni ordine a un solo cliente
- calcolare il totale economico di un ordine
- ottenere statistiche sulle vendite

---

## 🧱 Requisiti strutturali

Il database deve contenere **almeno 4 tabelle**:

1. `clienti`
2. `libri`
3. `ordini`
4. `dettaglio_ordini` (tabella ponte)

---

## 📋 Specifiche delle tabelle

### 1. CLIENTI

| Campo | Tipo | Vincoli |
|------|------|---------|
| id_cliente | INT | PRIMARY KEY, AUTO_INCREMENT |
| nome | VARCHAR(50) | NOT NULL |
| email | VARCHAR(100) | UNIQUE, NOT NULL |
| data_registrazione | DATE | DEFAULT CURRENT_DATE |

**Vincoli aziendali:**
- non possono esistere due clienti con la stessa email
- ogni cliente deve avere almeno un nome
- la data di registrazione non può essere NULL

---

### 2. LIBRI

| Campo | Tipo | Vincoli |
|------|------|---------|
| id_libro | INT | PRIMARY KEY, AUTO_INCREMENT |
| titolo | VARCHAR(100) | NOT NULL |
| autore | VARCHAR(100) | NOT NULL |
| prezzo | DECIMAL(6,2) | CHECK (prezzo > 0) |

**Vincoli aziendali:**
- ogni libro deve avere titolo e autore
- il prezzo deve essere positivo
- i prezzi devono supportare due decimali

---

### 3. ORDINI

| Campo | Tipo | Vincoli |
|------|------|---------|
| id_ordine | INT | PRIMARY KEY, AUTO_INCREMENT |
| id_cliente | INT | FOREIGN KEY REFERENCES clienti(id_cliente) |
| data_ordine | DATE | NOT NULL |

**Vincoli aziendali:**
- ogni ordine deve appartenere a un cliente esistente
- un cliente può avere più ordini
- un ordine non può esistere senza cliente

---

### 4. DETTAGLIO_ORDINI

| Campo | Tipo | Vincoli |
|------|------|---------|
| id_dettaglio | INT | PRIMARY KEY, AUTO_INCREMENT |
| id_ordine | INT | FOREIGN KEY REFERENCES ordini(id_ordine) |
| id_libro | INT | FOREIGN KEY REFERENCES libri(id_libro) |
| quantita | INT | CHECK (quantita > 0) |

**Vincoli aziendali:**
- un ordine può contenere più libri
- lo stesso libro può apparire in più ordini
- la quantità deve essere almeno 1
- non devono esistere righe con libro o ordine inesistenti

---

## 🔗 Relazioni richieste

- `clienti` 1 —— N `ordini`
- `ordini` N —— N `libri` (tramite `dettaglio_ordini`)

---

## 🧪 Dati minimi di test (obbligatori)

Inserire almeno:

- **3 clienti**
- **5 libri**
- **2 ordini**
- ogni ordine deve contenere **almeno 2 libri diversi**

---

## 🔍 Query richieste

Lo sviluppatore deve fornire query SQL per:

1. Elenco di tutti i clienti  
2. Elenco di tutti gli ordini con:
   - nome cliente  
   - data ordine  
3. Elenco dei libri contenuti in un ordine specifico  
4. Calcolo del totale economico di un ordine  
   (prezzo × quantità)  
5. Cliente che ha speso di più in totale  

---

## 📦 Materiale da consegnare

1. Script SQL contenente:
   - `CREATE DATABASE`
   - `CREATE TABLE`
   - `INSERT INTO`
2. Script SQL con le query richieste
3. (opzionale ma consigliato) Schema ER del database

---

## 🧠 Competenze richieste

Il progetto deve dimostrare l’uso di:

- PRIMARY KEY  
- FOREIGN KEY  
- relazioni  
- JOIN  
- SUM  
- GROUP BY  
- CHECK  
- UNIQUE  

---

## 🟢 Livello di difficoltà

Base / Intermedio  
Progetto adatto a:
- studenti
- tirocinanti
- junior developer

---

## ✅ Criteri di valutazione

Il progetto è considerato corretto se:

- il database viene creato senza errori
- i vincoli sono rispettati
- le query restituiscono risultati coerenti
- la struttura è normalizzata
- non esistono dati orfani (ordini senza cliente, dettagli senza libro)

---

## 📌 Nota finale dell’azienda

> Il database dovrà essere facilmente estendibile in futuro  
> (es. aggiunta di pagamenti, spedizioni, magazzino).

---

FINE CONSEGNA
