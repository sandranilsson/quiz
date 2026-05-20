# Quizverktyg — GitHub Pages

## Mappstruktur

```
quiz-site/
├── index.html          ← Själva quizappen
└── quizzes/
    ├── index.json      ← Lista över alla quiz (uppdatera när du lägger till ett)
    └── fotosyntesen.json   ← Exempelquiz
```

---

## Del 1 — Sätt upp GitHub Pages (görs en gång)

### 1. Skapa ett GitHub-konto
Gå till https://github.com och skapa ett gratis konto om du inte har ett.

### 2. Skapa ett nytt repo
1. Klicka på **"New"** (gröna knappen uppe till vänster)
2. Namn: `quiz` (eller vad du vill)
3. Välj **Public**
4. Klicka **"Create repository"**

### 3. Ladda upp filerna
På din dator, öppna en terminal i mappen `quiz-site` och kör:

```bash
git init
git add .
git commit -m "Första version"
git branch -M main
git remote add origin https://github.com/DITT-ANVÄNDARNAMN/quiz.git
git push -u origin main
```

*(Byt ut `DITT-ANVÄNDARNAMN` mot ditt GitHub-användarnamn)*

### 4. Aktivera GitHub Pages
1. Gå till ditt repo på GitHub
2. Klicka **Settings** (kugghjulet uppe till höger)
3. Scrolla ned till **"Pages"** i vänstermenyn
4. Under **"Branch"**: välj `main` och mappen `/ (root)`
5. Klicka **Save**

Efter någon minut är sajten live på:
`https://DITT-ANVÄNDARNAMN.github.io/quiz`

---

## Del 2 — Lägga till ett nytt quiz

### Steg 1 — Generera quiz-JSON i Claude
Ladda upp ditt studiematerial i chatten och be Claude:

> "Generera 15 fritextfrågor och en quiz-JSON med 20 flervalsfrågor baserat på det här materialet. Använd det vanliga formatet."

Du får:
- 15 fritextfrågor direkt i chatten (kör dem direkt med Claude)
- En JSON-fil att ladda ned

### Steg 2 — Spara JSON-filen
Lägg den i mappen `quizzes/` med ett beskrivande namn, t.ex. `historia-kap4.json`

### Steg 3 — Uppdatera index.json
Öppna `quizzes/index.json` och lägg till en rad för det nya quizet:

```json
[
  {
    "id": "fotosyntesen",
    "title": "Fotosyntesen",
    "subject": "Biologi",
    "description": "Flervalsfrågor om fotosyntesen",
    "date": "2026-05-19",
    "questionCount": 20
  },
  {
    "id": "historia-kap4",
    "title": "Historia kapitel 4",
    "subject": "Historia",
    "description": "Andra världskriget",
    "date": "2026-05-20",
    "questionCount": 20
  }
]
```

**id** måste matcha filnamnet (utan `.json`).

**Tillgängliga ämnen** (ger automatisk ikon i appen):
`Biologi` 🌿 · `Historia` 📜 · `Matematik` 📐 · `Kemi` ⚗️ · `Fysik` ⚡ · `Geografi` 🌍 · `Svenska` 📖 · `Engelska` 🗣️

### Steg 4 — Pusha till GitHub

```bash
git add .
git commit -m "Lagt till historia-kap4"
git push
```

Klart! Quizet syns på sajten inom någon minut.

---

## JSON-format (referens)

```json
{
  "title": "Titel på quizet",
  "subject": "Biologi",
  "description": "Kort beskrivning",
  "generated": "2026-05-19",
  "questions": [
    {
      "id": 1,
      "question": "Frågetexten?",
      "options": ["Alt A", "Alt B", "Alt C", "Alt D"],
      "correct": 0,
      "explanation": "Förklaring av rätt svar kopplad till materialet."
    }
  ]
}
```

- `correct` är index 0–3 (0 = Alt A, 1 = Alt B, osv.)
- `explanation` visas efter att eleven svarat

---

## Prompt att använda i Claude

Klistra in detta när du laddar upp material:

> Baserat på det uppladdade materialet, skapa:
> 1. **15 fritextfrågor** som vi kan gå igenom direkt i chatten
> 2. **En quiz-JSON-fil** med 20 flervalsfrågor i exakt det här formatet:
>
> ```json
> {
>   "title": "...",
>   "subject": "...",
>   "description": "...",
>   "generated": "DATUM",
>   "questions": [
>     {
>       "id": 1,
>       "question": "...",
>       "options": ["...", "...", "...", "..."],
>       "correct": 0,
>       "explanation": "..."
>     }
>   ]
> }
> ```
> Gör frågorna varierade i svårighetsgrad. Varje fråga ska direkt baseras på materialet.
