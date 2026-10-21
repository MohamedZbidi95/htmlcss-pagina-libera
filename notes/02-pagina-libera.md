# Appunti 02 – Pagina libera (HTML)

Sessioni: ottobre 2026 (finito il 21/10)
Esercizio del prof: pagina libera (consegna del 20/09) + seconda pagina collegata
Repo: `github.com/MohamedZbidi95/htmlcss-pagina-libera`

```
htmlcss-pagina-libera/
 ├── index.html        ← pagina 1
 ├── progetti.html     ← pagina 2
 ├── img/
 │    └── visual-studio-code-logo.webp
 └── notes/
      └── 02-pagina-libera.md
```

---

## 1. Lo scheletro: `html` ha solo 2 figli

```html
<!DOCTYPE html>
<html lang="it">              <!-- lang = la lingua della pagina -->
<head>                        <!-- FIGLIO 1: informazioni per il browser, NON si vedono -->
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Il mio percorso</title>   <!-- il testo nella scheda del browser -->
</head>
<body>                        <!-- FIGLIO 2: tutto quello che si vede nella pagina -->
    ...
</body>
</html>
```

```
html
 ├── head     → title, meta, link al CSS
 └── body     → header, main, footer, commenti
```

> ⚠️ **ATTENZIONE – errore mio (KNOWLEDGE GAP)**
> Ho messo un commento **dopo `</html>`**, poi **tra `</head>` e `<body>`**.
> Tra `</head>` e `<body>` non c'è posto per niente. Dopo `</html>` sei fuori dal documento.
>
> ```html
> </head>
> <!-- RICORDA ... -->     <!-- ❌ terra di nessuno -->
> <body>
> ```
> ```html
> </head>
> <body>
>     <!-- RICORDA ... -->  <!-- ✅ dentro il body -->
> ```

> ⚠️ **ATTENZIONE – errore mio (CARELESS)**
> Dopo `-->` avevo lasciato un `\`. Fuori dal commento, il browser lo mostra come testo.

---

## 2. Le 3 zone del `body`: fratelli, non uno dentro l'altro

```html
<body>
    <header>   titolo (h1), logo, menu (nav)          </header>
    <main>     il contenuto: testi, liste, tabelle, form </main>
    <footer>   copyright, contatti                    </footer>
</body>
```

`header`, `main`, `footer` sono **fratelli** (siblings): stesso genitore (`body`), stessa indentazione.

> ⚠️ **ATTENZIONE – errore mio (MISCONCEPTION)**
> In `progetti.html` avevo messo il `main` **dentro** l'`header`.
>
> ```html
> <header>
>     <h1>I miei progetti</h1>
>     <main> ... </main>      <!-- ❌ main figlio di header -->
> </header>
> ```
> ```html
> <header>
>     <h1>I miei progetti</h1>
> </header>                   <!-- ✅ header si chiude subito dopo h1 -->
> <main> ... </main>          <!-- ✅ main fratello di header -->
> ```

---

## 3. `title` vs `h1`

```html
<title>Il mio percorso</title>              <!-- nel head: scheda del browser -->
<h1>Il mio percorso da sviluppatore web</h1> <!-- nel body: titolo visibile nella pagina -->
```

Un solo `h1` per pagina. I sottotitoli sono `h2`.

---

## 4. Testo: `strong` e `i`

```html
<p>... con <strong>VS Code</strong> e <i>GitHub</i>.</p>
<!-- strong → importante (grassetto)     i → corsivo -->
```

`strong` e `i` sono **inline**: stanno dentro la riga, non vanno a capo.

---

## 5. Liste

```html
<ol type="I">          <!-- ordered list: numerata. type="I" → numeri romani -->
    <li>HTML</li>      <!-- list item -->
    <li>CSS</li>
</ol>

<ul>                   <!-- unordered list: pallini -->
    <li>Git</li>
</ul>
```

`li` sta **sempre** dentro `ol` o `ul`.

---

## 6. Tabella

```html
<table>
    <tr>                    <!-- table row: una riga -->
        <th>Argomento</th>  <!-- table header: cella intestazione (grassetto) -->
        <th>Stato</th>
    </tr>
    <tr>
        <td>HTML</td>       <!-- table data: cella normale -->
        <td>Fatto</td>
    </tr>
</table>
```

```
table
 └── tr  (riga)
      └── th / td  (celle)
```

> ⚠️ **ATTENZIONE – errore mio (MISCONCEPTION)**
> Avevo usato `th` come se fosse una riga, con `colspan`.
>
> ```html
> <th colspan="3">Argomento Lezioni Stato</th>   <!-- ❌ th è una CELLA, non una riga -->
> ```
> ```html
> <tr>                                            <!-- ✅ la riga è tr -->
>     <th>Argomento</th><th>Lezioni</th><th>Stato</th>
> </tr>
> ```

---

## 7. Immagini: locale vs remota

```html
<img src="./img/visual-studio-code-logo.webp" alt="Logo di Visual Studio Code">
<!--      ↑ relative path: un file nel MIO progetto -->

<img src="https://picsum.photos/300/200" alt="Foto di esempio">
<!--      ↑ absolute URL: un file su un altro sito -->
```

- `img` **non si chiude** (void element).
- `alt` = testo alternativo, se l'immagine non si carica. Sempre.
- `.webp` va bene: è un formato immagine moderno, leggero.

---

## 8. Form

```html
<form>
    <input type="text" placeholder="Il tuo nome">     <!-- testo su una riga -->
    <input type="email" placeholder="La tua email">   <!-- controlla che ci sia la @ -->
    <textarea placeholder="Il tuo messaggio"></textarea> <!-- testo su più righe -->
    <button type="submit">Invia</button>              <!-- invia il form -->
</form>
```

`placeholder` = il testo grigio che sparisce quando scrivi.

> ⚠️ **ATTENZIONE – errore mio (MISCONCEPTION)**
> ```html
> <textarea type="textarea">   <!-- ❌ textarea NON ha l'attributo type -->
> <textarea>                   <!-- ✅ type si usa su input e button -->
> ```

---

## 9. Link: absolute URL vs relative path

```html
<!-- absolute URL: un altro sito, inizia con https:// -->
<a href="https://github.com/MohamedZbidi95/htmlcss-wireframe">Wireframe card</a>

<!-- relative path: un file del MIO progetto, nella stessa cartella -->
<a href="progetti.html">Progetti</a>
<a href="./progetti.html">Progetti</a>   <!-- uguale: ./ = "questa cartella" -->
```

| | Absolute URL | Relative path |
|---|---|---|
| inizia con | `https://` | il nome del file, o `./` |
| va verso | un altro sito | un file del mio progetto |

Un link va in **una sola direzione**. Per andare e tornare tra 2 pagine servono **2 link**.

---

## 10. Il menu: `nav` + `ul` + `li` + `a`

```html
<header>
    <h1>I miei progetti</h1>
    <nav>                                          <!-- navigation: il menu del sito -->
        <ul>
            <li><a href="index.html">Home</a></li>
            <li><a href="progetti.html">Progetti</a></li>
        </ul>
    </nav>
</header>
```

- `nav` sta **dentro l'`header`**, dopo l'`h1`.
- `ul > li > a` è il **pattern professionale** per i menu.
- Lo **stesso menu** va su **tutte le pagine**.

---

## 11. Indentazione

```html
<ul>                <!-- 8 spazi -->
    <li>...</li>    <!-- 12 spazi: figlio di ul -->
    <li>...</li>    <!-- 12 spazi: fratello del primo li -->
</ul>               <!-- 8 spazi: la chiusura sta SOTTO la sua apertura -->
```

Scorciatoia VS Code: **Shift + Alt + F** = formatta tutto il file.

> ⚠️ **ATTENZIONE – errore mio (CARELESS)**
> ```html
>     <header>...</header>
>         <main>        <!-- ❌ 8 spazi: sembra figlio di header -->
>     <main>            <!-- ✅ 4 spazi: fratello di header -->
> ```

---

## 12. Coerenza (consistency)

```html
<a ...>Pagina libera</a>
<a ...>wireframe</a>        <!-- ❌ minuscolo, diverso dall'altro -->
<a ...>Wireframe card</a>   <!-- ✅ stesso stile -->
```

---

## 13. Privacy nei repo pubblici

> ⚠️ **ATTENZIONE – errore mio**
> Nel footer avevo messo il mio **telefono e email veri**. Il repo è **public**: lo vede chiunque.
> ```html
> <p>Telefono: +39 000 000 0000</p>    <!-- ✅ dati finti -->
> ```

---

## 14. Git: cosa ho imparato

```
M  → Modified:  il file esisteva, l'ho cambiato
U  → Untracked: file nuovo, Git non l'ha mai salvato
●  → nella scheda: file NON salvato
```

> ⚠️ **ATTENZIONE**
> Se il file ha il pallino ●, VS Code chiede prima del commit.
> ✅ **Save All & Commit Changes** → salva, poi fa il commit.
> ❌ **Commit Changes** → fa il commit della versione VECCHIA.

Commit di questo esercizio:
```
first commit
feat: add semantic structure
feat: add local image
feat: add local and remote images
feat: add study plan table
feat: add contact info in footer
feat: add contact form
feat: add projects page and navigation
```

`feat:` = nuova funzionalità. `fix:` = correzione. `docs:` = documentazione (questi appunti).

---

## 15. ⚠️ TUTTI I MIEI ERRORI – da non ripetere

### Errore 1 – `main` dentro `header` (MISCONCEPTION)
```html
<header>
    <h1>I miei progetti</h1>
    <main>...</main>        <!-- ❌ main figlio di header -->
</header>
```
```html
<header>
    <h1>I miei progetti</h1>
</header>
<main>...</main>            <!-- ✅ fratelli, tutti e due figli di body -->
```

### Errore 2 – ho cambiato `h1` in `h2` per "farlo stare" (MISCONCEPTION)
```html
<header><h2>I miei progetti</h2></header>   <!-- ❌ il titolo principale è h1 -->
<header><h1>I miei progetti</h1></header>   <!-- ✅ un h1 per pagina, nel header -->
```

### Errore 3 – mancava `</body>` (CARELESS)
```html
    </main>
</html>             <!-- ❌ body aperto e mai chiuso -->
```
```html
    </main>
</body>             <!-- ✅ ogni tag che apro, lo chiudo -->
</html>
```

### Errore 4 – commento dopo `</html>` (KNOWLEDGE GAP)
```html
</html>
<!-- RICORDA ... -->      <!-- ❌ fuori dal documento -->
```

### Errore 5 – commento tra `</head>` e `<body>` (KNOWLEDGE GAP)
```html
</head>
<!-- RICORDA ... -->      <!-- ❌ html ha solo 2 figli: head e body -->
<body>
```
```html
</head>
<body>
    <!-- RICORDA ... -->  <!-- ✅ dentro il body -->
```

### Errore 6 – un `\` dopo il commento (CARELESS)
```html
<!-- RICORDA ... -->\     <!-- ❌ il \ è fuori dal commento: si vede nella pagina -->
<!-- RICORDA ... -->      <!-- ✅ -->
```

### Errore 7 – indentazione dei fratelli (CARELESS)
```html
            <li>Pagina libera</li>
                <li>wireframe</li>   <!-- ❌ fratello spostato a destra -->
            </ul>                    <!-- ❌ non allineato con <ul> -->
```
```html
        <ul>
            <li>Pagina libera</li>
            <li>Wireframe card</li>  <!-- ✅ stesso spazio del fratello -->
        </ul>                        <!-- ✅ sotto la sua apertura -->
```
Trucco: **Shift + Alt + F**.

### Errore 8 – testo dei link non coerente (CARELESS)
```html
<a ...>wireframe</a>          <!-- ❌ -->
<a ...>Wireframe card</a>     <!-- ✅ maiuscola come "Pagina libera" -->
```

### Errore 9 – `th` usato come riga (MISCONCEPTION)
```html
<th colspan="3">Argomento Lezioni Stato</th>    <!-- ❌ th è una cella -->
<tr><th>Argomento</th><th>Lezioni</th><th>Stato</th></tr>  <!-- ✅ tr è la riga -->
```

### Errore 10 – `type` sulla `textarea` (MISCONCEPTION)
```html
<textarea type="textarea"></textarea>   <!-- ❌ textarea non ha type -->
<textarea></textarea>                   <!-- ✅ -->
```

### Errore 11 – copiare l'esempio invece di applicarlo (TRANSFER FAILURE)
```
❌ Copio la frase/immagine dell'esempio così com'è.
✅ L'esempio mostra il METODO. Lo applico ai MIEI contenuti.
```

### Errore 12 – dati veri in un repo pubblico
```html
<p>Telefono: +39 [numero vero]</p>    <!-- ❌ lo vede chiunque -->
<p>Telefono: +39 000 000 0000</p>     <!-- ✅ dati finti -->
```

### Errore 13 – copiare/committare senza salvare (CARELESS)
```
❌ Incollo il codice in chat senza Ctrl + S → mando la versione vecchia.
❌ "Commit Changes" con il pallino ● → commit della versione vecchia.
✅ Prima Ctrl + S. Nel popup: "Save All & Commit Changes".
```

---

## 16. Stato dei concetti

| Concetto | Stato |
|---|---|
| struttura html (head + body) | STABLE |
| header / main / footer fratelli | DEVELOPING |
| title vs h1 | DEVELOPING |
| liste (ol, ul, li) | DEVELOPING |
| tabella (table, tr, th, td) | DEVELOPING |
| img locale vs remota, alt | DEVELOPING |
| form (input, textarea, button, placeholder) | DEVELOPING |
| absolute URL vs relative path | DEVELOPING |
| nav + ul + li + a | DEVELOPING |
| indentazione | DEVELOPING |
| Git: M / U / ● | INITIAL |

Prossimo ripasso: domani (indentazione, header/main/footer), senza guardare questi appunti.
