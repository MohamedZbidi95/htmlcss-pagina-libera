# 04 – Pagina libera: Fase II (CSS) + tag della lista del prof

## Indice
1. Il metodo del prof
2. body vs * (inheritance)
3. Font stack e fallback
4. User agent stylesheet
5. Virgola vs spazio
6. I 3 selettori base
7. Compound selector e specificity bassa
8. width vs max-width (+ responsive)
9. DevTools
10. Headings h1–h6
11. br e hr
12. div e span
13. strong, i, u
14. article vs section vs div
15. Più class sullo stesso elemento (modifier)
16. Git: commit e messaggi
17. Termini del lavoro

---

## 1. Il metodo del prof (Fase II)

obiettivo → selezione (tag, .classe, #id) → regola

```css
/* obiettivo: header blu scuro con testo bianco */
header {                         /* selezione */
    background-color: #2c3e50;   /* regola    */
    color: #fff;
}
```

---

## 2. body vs * (inheritance)

`*` (universal selector) dà la regola DIRETTAMENTE a ogni elemento → blocca l'ereditarietà.
`body` dà la regola a UN elemento → i figli la EREDITANO (inheritance).

```css
body { font-family: arial, sans-serif; }  /* stile generale della pagina */
* { margin: 0; padding: 0; }              /* * solo per il RESET          */
```

Regola diretta > valore ereditato.

---

## 3. Font stack e fallback

```css
font-family: arial, sans-serif;
/* 1ª scelta: Arial, SE è installato sul dispositivo
   2ª scelta: sans-serif = generic family, esiste SEMPRE (fallback) */
```

Il browser ne usa UNO solo: il primo disponibile.

---

## 4. User agent stylesheet

Il CSS interno del browser: dà gli stili di default.
- h1 grande e in grassetto
- link (a) blu e sottolineati → regola DIRETTA, non ereditano il colore dell'header
- body con margin 8px

```css
header a { color: #fff; }   /* serve una regola diretta sui link */
```

Si vede nel DevTools: pannello Styles → "user agent stylesheet".

---

## 5. Virgola vs spazio

| Simbolo | Nome | Significato |
|---|---|---|
| `header, footer` | selector list | header E ANCHE footer |
| `header a` | descendant combinator | le a DENTRO l'header (qualsiasi livello) |
| `nav > a` | child combinator | solo figli DIRETTI |

Il bersaglio di un selettore è sempre l'ultimo a destra: `nav a` = "le a dentro un nav".

Principio **DRY** (Don't Repeat Yourself): una regola per due elementi invece di due regole uguali.

---

## 6. I 3 selettori base

| Nell'HTML | Nel CSS | Nome |
|---|---|---|
| (niente, è il tag) | `body` | type selector |
| `class="status"` | `.status` | class selector |
| `id="contact"` | `#contact` | id selector |

Guarda l'attributo nell'HTML → scegli il simbolo nel CSS.
class = 2 o più elementi · id = UN solo elemento.

---

## 7. Compound selector e specificity bassa

```css
img.page-img { }   /* compound: img E class → solo sulle immagini, più forte */
.page-img { }      /* best practice: valida su qualsiasi tag, più debole      */
```

La class stessa è il filtro. Usa il selettore più semplice che fa il lavoro (specificity bassa) → si evita la **specificity war**. Class **reusable**.

---

## 8. width vs max-width

| | width | max-width |
|---|---|---|
| Cosa fa | IMPONE la misura | mette solo un TETTO |
| Elemento più piccolo | lo ingrandisce | lo lascia com'è |
| Su schermo piccolo | esce: horizontal overflow | si restringe |

- elemento GRANDE che deve adattarsi (main, section, testo) → `max-width`
- elemento PICCOLO e sempre uguale (icona, logo) → `width`

**Responsive** = si adatta da solo alla dimensione dello schermo.

---

## 9. DevTools (F12 / tasto destro → Ispeziona)

- **Elements**: l'HTML ad albero; mouse sopra una riga = elemento colorato + misure
- **Styles**: le regole applicate; `element.style` = CSS temporaneo (come inline)
- **Computed**: misure reali (box model)
- **spunta** accanto a una property = accendi/spegni
- **Device Toolbar** (Ctrl + Shift + M): simula telefono/tablet
- **Dock side** (⋮): sposta il pannello in basso
- le modifiche NON toccano i file: spariscono ricaricando

---

## 10. Headings h1–h6

```html
<h2>Cosa sto studiando</h2>       <!-- sezione       -->
<h3>Cosa ho imparato finora</h3>  <!-- sotto-parte   -->
<h4>HTML</h4>                     <!-- sotto-sotto   -->
```

1. Non saltare livelli.
2. Il tag dice l'IMPORTANZA, la grandezza si cambia con il CSS.

Servono a **screen reader** (accessibility) e motori di ricerca (SEO).

---

## 11. br e hr (void elements)

```html
<p>Email: nome@esempio.com<br>Telefono: +39 000 000 0000</p>  <!-- br: a capo DENTRO lo stesso testo -->
<hr>                                                           <!-- hr: cambio di ARGOMENTO          -->
```

br NON serve per fare spazio tra blocchi: lo spazio si fa con il margin nel CSS.

---

## 12. div e span (tag generici, senza significato)

```html
<div class="box-img">...</div>                                          <!-- BLOCK: raggruppa elementi -->
<p>... diventare <span class="highlight">sviluppatore web</span>.</p>   <!-- INLINE: pezzo di testo    -->
```

Prima del div chiediti se esiste un tag semantico adatto. Solo div = **div soup** (cattiva pratica).

`text-align: center` sul div centra le immagini perché sono INLINE (align-items è Flexbox, L09).

---

## 13. strong, i, u

| Tag | Aspetto | Significato |
|---|---|---|
| strong | grassetto | testo importante |
| i | corsivo | tono diverso (nome, termine tecnico) |
| u | sottolineato | annotazione (es. parola sbagliata) |

u NON per decorare: si confonde con i link (per decorare: `text-decoration`, L07).

---

## 14. article vs section vs div

Domanda: "Questo blocco, da solo, si capisce?"

| Il blocco da solo... | Tag | Esempio |
|---|---|---|
| si capisce anche fuori dalla pagina | `article` | una ricetta, una scheda progetto, una notizia |
| è una parte della pagina (un argomento) | `section` | il ricettario, "Offerte della settimana" |
| non ha significato, serve solo per lo stile | `div` | il contenitore delle immagini |

Una section può contenere tanti article. Article sta DENTRO il main (la posizione dentro il main non conta).
Il browser li mostra uguali: la differenza è il significato (screen reader, SEO, colleghi).

**section** = sezione (*-tion* / *-zione*) · selection = selezione, un'altra cosa.

---

## 15. Più class sullo stesso elemento (modifier)

```html
<td class="status status-done">Fatto</td>
<!--      ↑      ↑
        comune   modifier       SPAZIO separa le class, TRATTINO unisce le