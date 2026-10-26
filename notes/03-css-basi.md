# 03 – CSS basics (L05 CSS Intro)

## Indice
1. class vs id
2. Specificity
3. Combinator `+` (ripasso)
4. Tre modi di aggiungere il CSS
5. Cascade: quale regola vince
6. CSS nel posto sbagliato
7. Attribute vs property
8. Proprietà più comuni (slide 23)
9. Dove cercare: la documentation (slide 24)
10. W3C CSS Validator (slide 25)
11. Termini del lavoro
12. TUTTI I MIEI ERRORI

---

## 1. class vs id

EN: A class is for **two or more** elements; an id is for **one** element only (unique).
IT: Una class è per **due o più** elementi; un id è per **un solo** elemento (unique).

EN: The tag doesn't decide: `class` and `id` are **universal attributes**, valid on any tag.
IT: Non decide il tag: `class` e `id` sono **universal attributes**, validi su qualsiasi tag.

```html
<li class="nav-item">Home</li>       <!-- 2 elementi → class -->
<li class="nav-item">Progetti</li>
<section id="contact">...</section>  <!-- 1 elemento → id -->
```

```css
.nav-item { color: blue; }       /* punto .     = class selector */
#contact  { background: gray; }  /* cancelletto # = id selector   */
```

| Quanti elementi? | Uso |
|---|---|
| 1 | `id` |
| 2 o più | `class` |

EN: The same id used twice is a **duplicate id**: the browser shows no error, but the HTML is **invalid**.
IT: Lo stesso id usato due volte è un **duplicate id**: il browser non dà errore, ma l'HTML è **invalid**.

> ⚠️ ATTENZIONE – errore mio (MISCONCEPTION)
> ❌ "la class si mette su div e nav, l'id sui form"
> ✅ decide solo il NUMERO di elementi, non il tag

> ⚠️ ATTENZIONE – errore mio (MISCONCEPTION)
> ❌ "l'id è per POCHI elementi"
> ✅ l'id è per UN SOLO elemento; 2 elementi sono già una class

> ⚠️ ATTENZIONE – errore mio (MISCONCEPTION)
> ❌ "con l'id lo chiamo da Node"
> ✅ gli elementi della pagina si selezionano con JavaScript NEL BROWSER (client-side); Node.js gira sul server

---

## 2. Specificity

EN: When two rules hit the same element, the stronger selector wins, whatever the order.
IT: Quando due regole colpiscono lo stesso elemento, vince il selector più forte, qualunque sia l'ordine.

```css
h1          { color: black; }  /* type selector  → debole */
.title      { color: blue;  }  /* class selector → medio  */
#page-title { color: red;   }  /* id selector    → forte  → VINCE: rosso */
```

`#id` > `.class` > `tag`

---

## 3. Combinator `+` (adjacent sibling combinator)

EN: `A + B` selects **B** only if it comes **immediately after** A, with the **same parent**. It never goes inside A.
IT: `A + B` seleziona **B** solo se viene **subito dopo** A, con lo **stesso genitore**. Non entra mai dentro A.

```html
<main>
    <h2>Cosa sto studiando</h2>          <!-- ⚫ è il riferimento, non viene colorato -->
    <p>Il corso è diviso...</p>          <!-- 🔴 p SUBITO DOPO h2 → preso            -->
    <div>
        <p>Dentro il div</p>             <!-- ⚫ è dentro il div, livello diverso     -->
    </div>
    <p>Lontano</p>                       <!-- ⚫ non è subito dopo h2                 -->
</main>
```

```css
h2 + p { color: red; }
```

| Selector | Prende |
|---|---|
| `div img` (spazio) | img **dentro** il div |
| `div > img` | img **figlia diretta** del div |
| `div + img` | img **subito dopo** il div, fuori |
| `div ~ img` | **tutte** le img dopo il div, fuori |

> ⚠️ ATTENZIONE – errore mio (RECALL FAILURE)
> ❌ `div+img` per "l'img dentro il div"
> ✅ `div img` (spazio)

> ⚠️ ATTENZIONE – errore mio (MISCONCEPTION)
> ❌ `+` letto come "dentro" o "primo figlio diretto"
> ✅ `+` = fratello SUBITO DOPO, fuori; il primo figlio diretto è `div > img:first-child`

---

## 4. Tre modi di aggiungere il CSS (slide 13, 14, 15)

| Nome (W3Schools) | Dove | Vale per |
|---|---|---|
| **External CSS** | file `.css` + `<link>` nell'`head` | tutte le pagine collegate |
| **Internal CSS** | tag `<style>` nell'`head` | solo quella pagina |
| **Inline CSS** | attributo `style=""` nel tag | solo quell'elemento |

```html
<head>
    <link rel="stylesheet" href="./css/style.css">  <!-- External CSS -->
    <style>
        h1 { color: green; }                        /* Internal CSS */
    </style>
</head>
<body>
    <h1 style="color: orange;">Titolo</h1>          <!-- Inline CSS  -->
</body>
```

EN: Professionals use External CSS: structure (HTML) and style (CSS) stay separate. This principle is called **separation of concerns**.
IT: I professionisti usano l'External CSS: struttura (HTML) e stile (CSS) restano separati. Questo principio si chiama **separation of concerns**.

EN: W3Schools rules: the `.css` file must not contain HTML tags; no space between value and unit (`20px`, not `20 px`).
IT: Regole W3Schools: il file `.css` non deve contenere tag HTML; nessuno spazio tra valore e unità (`20px`, non `20 px`).

---

## 5. Cascade: quale regola vince

EN: Same selector → the rule read **last** wins. The browser reads the `head` from top to bottom.
IT: Stesso selector → vince la regola letta **per ultima**. Il browser legge l'`head` dall'alto verso il basso.

EN: Trick: mentally replace the `<link>` line with the content of `style.css`, then read from top to bottom.
IT: Trucco: sostituisci mentalmente la riga del `<link>` con il contenuto di `style.css`, poi leggi dall'alto verso il basso.

```html
<!-- CASO 1: link sopra, style sotto → vince l'Internal CSS -->
<head>
    <link rel="stylesheet" href="./css/style.css">  <!-- h1 black (1° letto)       -->
    <style> h1 { color: brown; } </style>           <!-- h1 brown (2° letto) VINCE -->
</head>

<!-- CASO 2: style sopra, link sotto → vince l'External CSS -->
<head>
    <style> h1 { color: brown; } </style>           <!-- h1 brown (1° letto)       -->
    <link rel="stylesheet" href="./css/style.css">  <!-- h1 black (2° letto) VINCE -->
</head>
```

Metodo in 2 passi:
1. C'è un **Inline CSS** sull'elemento? → vince lui, fine.
2. Se no: chi è più **in basso** nell'`head`? → vince lui.

> ⚠️ ATTENZIONE – errore mio (MISCONCEPTION)
> ❌ "il file style.css è più importante" (tutto blu)
> ✅ decide la POSIZIONE nell'head, non il tipo

> ⚠️ ATTENZIONE – errore mio (MISCONCEPTION, correzione eccessiva)
> ❌ "vince sempre lo <style>"
> ✅ nessuno dei due vince sempre: vince chi è più in basso

---

## 6. CSS nel posto sbagliato

```html
<!-- <style> nel body: FUNZIONA ma è SBAGLIATO -->
<body>
    <style> h2 { color: green; } </style>   <!-- invalid HTML + rischio FOUC -->
</body>

<!-- CSS scritto come content: NON è CSS -->
<p>color: blue;</p>                          <!-- ⚫ appare come TESTO sulla pagina -->

<!-- CSS nell'attributo style: è Inline CSS -->
<p style="color: blue;">Testo</p>            <!-- 🔵 stile applicato -->
```

EN: **FOUC** (Flash Of Unstyled Content): the page appears without style, then "jumps" when the CSS arrives.
IT: **FOUC** (Flash Of Unstyled Content): la pagina appare senza stile, poi "salta" quando arriva il CSS.

> ⚠️ ATTENZIONE – errore mio (RECALL FAILURE)
> ❌ `align: center;`
> ✅ `text-align: center;`

---

## 7. Attribute vs property

```html
<img src="./img/logo.webp" alt="Logo">  <!-- src, alt = ATTRIBUTES (HTML) -->
```

```css
img { width: 300px; }                   /* width = PROPERTY (CSS) */
```

> ⚠️ ATTENZIONE – errore mio (TERMINOLOGIA)
> ❌ chiamare "attributi" le proprietà CSS
> ✅ HTML → attribute · CSS → property

---

## 8. Proprietà più comuni (slide 23)

| Property | Cosa fa | Esempio |
|---|---|---|
| `background` | sfondo dell'elemento | `background: #2c3e50;` |
| `color` | colore del testo | `color: white;` |
| `width` | larghezza del blocco | `width: 300px;` |
| `height` | altezza del blocco | `height: 150px;` |
| `border` | spessore, stile e colore del bordo | `border: 1px solid #ddd;` |

EN: `background` and `border` are **shorthand properties**: one line sets many values.
IT: `background` e `border` sono **shorthand properties**: una riga imposta tanti valori.

```css
/* border: versione lunga = versione corta */
.card {
    border-width: 1px;       /* spessore                                  */
    border-style: solid;     /* tipo: solid, dashed, dotted, none          */
    border-color: #ddd;      /* colore                                     */
}
.card { border: 1px solid #ddd; }  /* stesso risultato */

/* senza border-style il bordo NON compare (default: none) */
.card { border: 1px #ddd; }        /* ❌ niente bordo */
```

```css
/* background-color vs background */
header { background-color: #2c3e50; }  /* imposta SOLO il colore                         */
header { background: #2c3e50; }        /* shorthand: colore + riporta il resto al default */
```

EN: Properties influence each other: a fixed `height` with too much text creates **overflow**; the fix is `min-height`.
IT: Le proprietà si influenzano a vicenda: un'`height` fissa con troppo testo crea **overflow**; la soluzione è `min-height`.

---

## 9. Dove cercare (slide 24)

W3Schools · MDN Web Docs · Stack Overflow · Google · AI
EN: At work, "check the docs" means: look it up in the official **documentation**.
IT: Al lavoro, "controlla la docs" significa: cercalo nella **documentation** ufficiale.

---

## 10. W3C CSS Validator (slide 25)

Indirizzo: https://jigsaw.w3.org/css-validator/#validate_by_input

EN: The browser ignores wrong CSS in silence; the validator shows the line and the reason.
IT: Il browser ignora il CSS sbagliato in silenzio; il validator mostra la riga e il motivo.

| Modo | Cosa fai |
|---|---|
| By URI | indirizzo di una pagina online |
| By File Upload | carichi `style.css` |
| By Direct Input | incolli il CSS (solo CSS, niente `<style>`) |

Esempio reale (mio test):
```
7    h1   Parse Error : color darkblue          → mancavano i due punti
12   p    valori non riconosciuti : 16 px       → spazio tra valore e unità
13   p    La proprietà align non esiste         → è text-align
```

| Tipo | Significato |
|---|---|
| **Error** | codice sbagliato, il browser lo ignora → da correggere |
| **Warning** | funziona ma non è buona pratica |

Nessun errore → "Congratulations! No Error Found." = **valid CSS**

---

## 11. Termini del lavoro

| Termine | Significato |
|---|---|
| homepage | la pagina principale (`index.html`) |
| stylesheet | il file `.css` |
| styling | il lavoro di applicare lo stile |
| override | una regola che sovrascrive un'altra |
| hardcoded | valore fisso in un punto difficile da cambiare |
| maintainability | quanto è facile modificare il codice in futuro |
| codebase | tutto il codice di un progetto |
| refactor | riscrivere il codice per migliorarlo, stesso risultato |
| code review | un collega controlla il tuo codice prima del merge |
| release | la pubblicazione di una versione |
| debug style | stile temporaneo per controllare qualcosa (es. test del giallo) |
| naming convention | regola comune per i nomi (es. `nav-item`) |
| validation | controllo del codice rispetto allo standard |
| linter | strumento nell'editor che valida mentre scrivi |

---

## 12. TUTTI I MIEI ERRORI

| # | Errore | Corretto | Tipo |
|---|---|---|---|
| 1 | class su div/nav, id sui form | decide il numero di elementi | MISCONCEPTION |
| 2 | id per "pochi" elementi | id = UN solo elemento | MISCONCEPTION |
| 3 | selezionare elementi "con Node" | JavaScript nel browser | MISCONCEPTION |
| 4 | `div+img` per "img dentro il div" | `div img` | RECALL FAILURE |
| 5 | `+` = "dentro" / "primo figlio" | `+` = fratello subito dopo | MISCONCEPTION |
| 6 | "il file style.css vince sempre" | vince chi è più in basso | MISCONCEPTION |
| 7 | "lo `<style>` vince sempre" | vince chi è più in basso | MISCONCEPTION |
| 8 | `align: center` | `text-align: center` | RECALL FAILURE |
| 9 | "attributi" CSS | properties | TERMINOLOGIA |