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
<html lang="it">
  <!-- lang = la lingua della pagina -->
  <head>
    <!-- FIGLIO 1: informazioni per il browser, NON si vedono -->
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Il mio percorso</title>
    <!-- il testo nella scheda del browser -->
  </head>
  <body>
    <!-- FIGLIO 2: tutto quello che si vede nella pagina -->
    ...
  </body>
</html>
```

```
html
 ├── head     → title, meta, link al CSS
 └── body     → header, main, footer, commenti
```

Tra `</head>` e `<body>` non va niente. Dopo `</html>` si è fuori dal documento: anche i commenti vanno dentro il `body`.

---

## 2. Le 3 zone del `body`: fratelli, non uno dentro l'altro

```html
<body>
  <header>titolo (h1), logo, menu (nav)</header>
  <main>il contenuto: testi, liste, tabelle, form</main>
  <footer>copyright, contatti</footer>
</body>
```

`header`, `main`, `footer` sono **fratelli** (siblings): stesso genitore (`body`), stessa indentazione.

---

## 3. `title` vs `h1`

```html
<title>Il mio percorso</title>
<!-- nel head: scheda del browser -->
<h1>Il mio percorso da sviluppatore web</h1>
<!-- nel body: titolo visibile nella pagina -->
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
<ol type="I">
  <!-- ordered list: numerata. type="I" → numeri romani -->
  <li>HTML</li>
  <!-- list item -->
  <li>CSS</li>
</ol>

<ul>
  <!-- unordered list: pallini -->
  <li>Git</li>
</ul>
```

`li` sta **sempre** dentro `ol` o `ul`.

---

## 6. Tabella

```html
<table>
  <tr>
    <!-- table row: una riga -->
    <th>Argomento</th>
    <!-- table header: cella intestazione (grassetto) -->
    <th>Stato</th>
  </tr>
  <tr>
    <td>HTML</td>
    <!-- table data: cella normale -->
    <td>Fatto</td>
  </tr>
</table>
```

```
table
 └── tr  (riga)
      └── th / td  (celle)
```

`th` e `td` sono **celle**: la riga è sempre `tr`.

---

## 7. Immagini: locale vs remota

```html
<img
  src="./img/visual-studio-code-logo.webp"
  alt="Logo di Visual Studio Code"
/>
<!--      ↑ relative path: un file nel MIO progetto -->

<img src="https://picsum.photos/300/200" alt="Foto di esempio" />
<!--      ↑ absolute URL: un file su un altro sito -->
```

- `img` **non si chiude** (void element).
- `alt` = testo alternativo, se l'immagine non si carica. Sempre.
- `.webp` va bene: è un formato immagine moderno, leggero.

---

## 8. Form

```html
<form>
  <input type="text" placeholder="Il tuo nome" />
  <!-- testo su una riga -->
  <input type="email" placeholder="La tua email" />
  <!-- controlla che ci sia la @ -->
  <textarea placeholder="Il tuo messaggio"></textarea>
  <!-- testo su più righe -->
  <button type="submit">Invia</button>
  <!-- invia il form -->
</form>
```

`placeholder` = il testo grigio che sparisce quando scrivi.
L'attributo `type` si usa su `input` e `button`, **non** sulla `textarea`.

---

## 9. Link: absolute URL vs relative path

```html
<!-- absolute URL: un altro sito, inizia con https:// -->
<a href="https://github.com/MohamedZbidi95/htmlcss-wireframe">Wireframe card</a>

<!-- relative path: un file del MIO progetto, nella stessa cartella -->
<a href="progetti.html">Progetti</a>
<a href="./progetti.html">Progetti</a>
<!-- uguale: ./ = "questa cartella" -->
```

|            | Absolute URL  | Relative path            |
| ---------- | ------------- | ------------------------ |
| inizia con | `https://`    | il nome del file, o `./` |
| va verso   | un altro sito | un file del mio progetto |

Un link va in **una sola direzione**. Per andare e tornare tra 2 pagine servono **2 link**.

---

## 10. Il menu: `nav` + `ul` + `li` + `a`

```html
<header>
  <h1>I miei progetti</h1>
  <nav>
    <!-- navigation: il menu del sito -->
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
<ul>
  <!-- 8 spazi -->
  <li>...</li>
  <!-- 12 spazi: figlio di ul -->
  <li>...</li>
  <!-- 12 spazi: fratello del primo li -->
</ul>
<!-- 8 spazi: la chiusura sta SOTTO la sua apertura -->
```

I fratelli hanno sempre la **stessa** indentazione.
Scorciatoia VS Code: **Shift + Alt + F** = formatta tutto il file.

---

## 12. Coerenza (consistency)

```html
<a ...>Pagina libera</a> <a ...>Wireframe card</a>
<!-- stesso stile: iniziale maiuscola, nome completo -->
```

Elementi dello stesso tipo si scrivono nello **stesso modo**.

---

## 13. Privacy nei repo pubblici

Il repo è **public**: lo vede chiunque. Nei file vanno solo **dati finti** (telefono, email).

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
